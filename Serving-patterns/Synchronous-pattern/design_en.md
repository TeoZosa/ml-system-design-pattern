# Synchronous Pattern

## Use Case

- Business logic depends on model inference, thus making it a bottleneck
- When your workflow depends on the inference result

## Architecture

As its name suggests, the Synchronous Pattern is used to run predictions synchronously.
In this patten, workflows are blocked until predictions are complete.

- REST or gRPC APIs often leverage the Synchronous Pattern
- This is one of the simplest patterns to use and its workflow can be visualized in a
  simple step-by-step fashion

## Diagram

![diagram](diagram.png)

## Pros

- Easy to manage due to its simplicity. Operational aspects such as tracing and
  monitoring become easy as well
- Service workflow is simplified as the process won't proceed until the prediction
  completes

## Cons

- Prediction latency can become a performance bottleneck. Workarounds to avoid user
  experience degradation introduce additional complexity
- If the client of your service is itself a service, then this pattern will lead to
  blocked threads on the client side

## Considerations

- Prediction latency workarounds introduce additional complexity
- Timeout logic may be necessary for slow/stalled prediction requests

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter4_serving_patterns/synchronous_pattern
