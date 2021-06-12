# Multistage Prediction Pattern

## Use Case

- ML prediction for interactive applications.
- When you have lightweight prediction and heavy prediction for one purpose.

## Architecture

The Multistage Prediction Pattern is available when a workflow is amenable to multiple
predictions, each of which is to be returned to clients at different stages.

Oftentimes, prediction quality scales with model size, and consequently, inference time.

For web and interactive applications specifically, it is important to maintain a balance
of speed and accuracy. In some cases, a good strategy is to initially return a fast,
sufficient prediction which can be replaced/added onto by a longer but better prediction
in the next screen or later on in the user flow.

The pattern leverages two prediction servers; one which provides a quick, synchronous
response, and another which provides a longer, asynchronous response.

- The first provides fairly accurate and fast response, typically via a REST or gRPC
  API.
- The second provides a richer prediction at the cost of a much longer inference time,
  so it is typically served by an asynchronous queue or messaging service.

The choice of models to be used in each stage primarily depend on prediction quality and
response speed requirements. In the multimodal case, this may also correspond to the
categories of the data ingested/predicted.

In general, model size (and thus prediction time) tends to be smaller for table and
numerical data and larger for unstructured data, such as image and text.

Some services require to have a quick response times with improved user experience via
better prediction a future concern.

For instance, the quick, synchronous prediction may operate on numerical and categorical
data while longer, asynchronous prediction may operate on image and text data.

## Diagram

![diagram](diagram.png)

## Pros

- Exploits both quick predictions and longer but better predictions.

## Cons

- Multiple services and interfaces required which increases overall complexity.

## Considerations

- Balance of speed, accuracy and user experience.
- How to provide the heavy predictions.
