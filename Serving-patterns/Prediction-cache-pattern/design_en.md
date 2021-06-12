# Prediction Cache Pattern

## Use Case

- Predictions do not change frequently and duplicate prediction requests can be
  detected.
- The input data is identifiable with a cache key.

## Architecture

In the Prediction Cache Pattern, predictions are stored in cache for later requests to
query in the case of a duplicate prediction request. If your service gets requests for
the same data, and if it is possible to identify it is the same, you can take advantage
of this pattern.

The proxy (or prediction server) will store the input data as the cache key (if the key
does not exist) and the prediction as the value.

Two strategies may be used:

1. The cache search and prediction will be executed in sequence to minimize the
   prediction service load.
    1. If a cache miss occurs, the prediction request will be forwarded to the
       prediction service.
    2. This eliminates duplicate predictions by the prediction server, thereby reducing
       load at the expense of increasing latency observed by the client

    - Latency:
        - Cache Hit: `cache search time`
        - Cache Miss: `cache search time + prediction time` <= Worse
    - Load:
        - Cache Hit: `cache search load` <= Better
        - Cache Miss: `cache search load + prediction load`
2. The cache search and prediction will be executed in parallel to minimize the overall
   latency.
    1. If a cache hit occurs, the cached result is returned immediately without waiting
       for the prediction to complete.
    2. This shortens prediction latency observed by the client at the expense of
       potentially redundant load on the prediction server.

    - Latency: (assuming `cache search time < prediction time`)
        - Cache Hit: `cache search time`
        - Cache Miss: `prediction time` <= Better
    - Load:
        - Cache Hit: `cache search load + prediction load` <= Worse
        - Cache Miss: `cache search load + prediction load`

In either case, on a cache miss the cache will be updated with the prediction generated
by the prediction service, either by the reverse proxy or by the prediction service
itself.

- To reduce overall latency, this may be done asynchronously, with results
  simultaneously forwarded to the upstream service/client and written to the cache.

## Diagram

### Prediction Cache

![diagram](diagram.png)

## Pros

- Improves latency for duplicate requests.
- Reduces load on preprocessing/prediction servers if preprocessing/prediction requests
  are only forwarded on cache misses.

## Cons

- Increased complexity due to the need for cache eviction and cache invalidation
  policies
- Additional cost incurred by the addition of a cache server.

## Considerations

- The input data must identifiable with a cache key.
- The tradeoff between speed, cost, and volume.
- Cache-related considerations:
    1. An effective **cache eviction** policy.
        - The volume of data to cache must be balanced against cost as the per-unit
          price of cache space tends to be much higher than permanent storage or a
          database. Caches can grow very quickly, especially when the service is under
          heavy load. To keep the cache reasonably sized, a cache eviction policy needs
          to be carefully chosen.
        - For the Prediction Cache Pattern in particular, evicting entries with
          relatively few accesses (Least Frequently Used; LFU) is often a good first
          choice.
    2. An effective **cache invalidation** policy
        - If prediction results change over time, stale cache entries must be cleared to
          prevent responding with outdated prediction, for instance, by clearing cache
          entries past a certain time interval (Time-To-Live; TTL).
        - Note that this differs from traditional cache invalidation where the source of
          truth is a permanent storage resource (e.g, a database).

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter4_serving_patterns/prediction_cache_pattern
