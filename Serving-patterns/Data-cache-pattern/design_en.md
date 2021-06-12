# Data Cache Pattern

## Use Case

- Duplicate prediction requests (i.e., same and repeated data) can be detected.
- The input data is identifiable with a cache key.
- When you want to accelerate data retrieval and processing.

## Architecture

The Data Cache Pattern will cache **input data** (as opposed to prediction results as in
the [Prediction Cache Pattern](../Prediction-cache-pattern/design_en.md)) that would
otherwise need to be read from a database, disk, or any other storage resource with
high-latency access. This also useful when data preprocessing occurs to help reduce
load/latency for duplicate preprocessing requests.

There are two architectures for the pattern:

1. Input data is cached directly by the reverse proxy server (see `Input Data Cache`).
   The cache search and backend storage search will be executed in parallel to minimize
   the overall latency.
    1. If a cache hit occurs, the cached data is immediately forwarded to the prediction
       service with the prediction request without waiting for the backend storage query
       to complete.
    2. On a cache miss, the data returned from backend storage will be added into the
       cache, possibly after any preprocessing to decrease future preprocessing service
       load, and then forwarded to the prediction service with the prediction request as
       in (i).
    3. This shortens prediction latency observed by the client at the expense of
       potentially redundant load on the backend storage server.

2. Input data is cached by a data-generating or preprocessing service to increase cache
   rate and thus improve latency (see `Prepared Data Cache`).
    1. Data can be cached prior to the prediction request to the reverse proxy server
       (i.e., we pre-populate the cache to preempt the cold start problem, or update the
       cache at predefined intervals) or after the reverse proxy submits a data
       generation/preprocessing request to the corresponding cache-filling service
       (either asynchronously with the cache search or in response to a cache miss).
    2. Once a prediction request on the data is received, the reverse proxy will
       retrieve the data from the cache and forward it to the prediction service with
       the prediction request.

## Diagram

### Input Data Cache

![diagram1](diagram1.png)

### Prepared Data Cache

![diagram2](diagram2.png)

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
        - For the Data Cache Pattern in particular, evicting entries with relatively few
          accesses (Least Frequently Used; LFU) is often a good first choice.
    2. An effective data **cache invalidation** policy
        - If data change over time, stale cache entries must be cleared to prevent
          responding with outdated data, for instance, by clearing/updating cache
          entries past a certain time interval (Time-To-Live; TTL) or using a reverse
          write-back policy whereby updates to a cache entry's corresponding DWH entry
          triggers a data-generation/preprocessing job to update that cache entry.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter4_serving_patterns/data_cache_pattern

