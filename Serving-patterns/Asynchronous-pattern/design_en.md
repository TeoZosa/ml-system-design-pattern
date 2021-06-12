# ASynchronous Pattern

## Use Case

- The immediate process does not depend on an inference result.
- To isolate the client making the prediction request from the response destination.

## Architecture

The aSynchronous Pattern realizes separates a prediction requests from retrievals by
placing an intermediate data store (a queue or cache) between the client and predictor.

This allows the client to continue processing new requests asynchronously and avoid
experiencing inference latency.

- In order for the client to get the prediction, polling must be implemented so that
  results can be pulled from the queue
- If the prediction result is to be retrieved by a resource other than the client
  (as in `Diagram2`), polling can be skipped
- The client can `Diagram1` and `Diagram2`, 
  the client can instruct the prediction
  server to push the result to another component, however you have to carefully consider
  its use case for the system as this can make the workflow quite complex.

## Diagram

### Diagram1

![diagram1](diagram1.png)

### Diagram2

![diagram2](diagram2.png)

## Pros

- The client and predictions are separate.
- The client can avoid being affected by prediction latency.

## Cons

- Requires an intermediate data store such as a queue, cache or other type of proxy.
- Not appropriate for real-time use cases.

## Considerations

- How to trigger prediction:
    - Queue: prediction will be FIFO
    - Cache: depends on existence of cache
    - PubSub: predictor's subscription to run prediction
- Needs consideration for prediction error:
    - If you need to retry, consider triggering retry in the prediction server or return
      to queue.
    - If the error is caused by data or programmatical issue, there may be a chance that
      the request keeps retrying until you manually disposes the request.
- Since the pattern does not support ordered predition, you have to consider the
  workflow if you need concrete order for input or event in the use case.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter4_serving_patterns/asynchronous_pattern
