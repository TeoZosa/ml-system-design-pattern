# Model-Load Pattern

## Use Case

- Model update cadence is more frequent than server image update cadence.
- Reuse a single server image to serve multiple models.

## Architecture

In the Model-Load Pattern, the prediction server image is decoupled from the model
file (in contrast to
the [Model-In-Image Pattern](../Model-in-image-pattern/design_en.md)), and consequently,
from model management (and vice versa). This reduces the image size and, when combined
with model-agnostic development, enables reuse of the image across various compatible
prediction models.

While productionizing an ML service on a cloud platform (or on containers) becomes a
common practice, it is still an important consideration to manage and version machine
learning model along with its server image.

To release a prediction service using this pattern, the prediction server is first
deployed onto the platform, downloading the model file as its initial task before
starting the prediction process.

- An environmental variable can be used to configure which model needs to be run on the
  server.
- One issue is model library management as the library in the server image must match
  the library used by the model, and vice versa.
    - A table of supported libraries for each image and models needs to be maintained,
      resulting in increased operational complexity.

## Diagram

![diagram](diagram.png)

## Pros

- Model and image versioning decoupling.
- Server image reuse
- Minimal image size
- Simplified server image change management

## Cons

- Service start times may suffer.
- The server should only pass health checks once the model is successfully loaded
- Additional overhead of tracking supported library versions between images and models

## Considerations

- Dependent version management of server image and model file.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter3_release_patterns/model_load_pattern
