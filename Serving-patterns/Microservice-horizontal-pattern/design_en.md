# Microservice Horizontal Pattern

## Use Case

- Multiple inferences which will be executed in parallel.
    - Required to run several predictions to one request
- Prediction results are integrated at the end of some other computation

## Architecture

The Microservice Horizontal Pattern allows you to run multiple models in parallel.

You can send a single request to each model simultaneously to acquire multiple
predictions which can be optionally integrated together in some way and returned to the
user either in aggregate or as a subset.

- May be synchronous or asynchronous depending on your use case.
    - If synchronous, the response may be blocked on the aggregated predictions from all
      the models.
    - If asynchronous, then a dataflow model may be followed wherein downstream requests
      or responses are triggered upon the receipt of a specific prediction
      (`Asynchronized horizontal`)
- A reverse proxy between the client and prediction services is responsible for handling
  requests and responses, coordinating inference execution ordering and result
  aggregation. Additional data retrieval may also be done by the proxy or each
  predictor (`Synchronized horizontal with data retrieval`)
- An advantage of the reverse proxy is that it provides an implicit caching mechanism
  which reduces latency and the number of requests to a data warehouse or other backend
  storage. Additionally, it abstracts away more complicated application logic from the
  prediction services themselves, allowing for complex/robust workflows.

## Diagram

### Synchronized horizontal

![diagram1](diagram1.png)

### Synchronized horizontal with data retrieval

![diagram2](diagram2.png)

### Asynchronized horizontal

![diagram3](diagram3.png)

## Pros

- Resource usage can be tuned independently
- Failures can be isolated within corresponding services
- Models may be designed independently of one another and the overall system due to
  their mutually independent nature.

## Cons

- Increased system complexity
- For synchronous predictions, the slowest inference becomes the bottleneck.
- For asynchronous predictions, postprocessing must account for time lag.

## Considerations

- Synchronous vs. asynchronous.
- Synchronous inference latency management: timeout or wait.
- Asynchronous time lag management.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter4_serving_patterns/horizontal_microservice_pattern
