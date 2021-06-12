# Model-In-Image Pattern

## Use Case

- Service environment and prediction model versioning unification.

## Architecture

In the Model-In-Image Pattern, you build a server or container image which directly
contains the model file. This enables unified versioning and management of a particular
machine learning model along with its server image which is an increasingly important
consideration Given that productionizing an ML service on a cloud platform and/or
containers is a common practice

- This unifies model training and image building within a single workflow, implicitly
  guaranteeing model and image version alignment.

- Images are built after the model training completes. To deploy the prediction service,
  you simply pull and run the image on the production platform.

One issue with this pattern is that the image size, and consequently, image build and
download times increase proportionally with model size.

- Since images are built immediately after training completes, you will want to make a
  standardized (preferably automated) workflow to preempt errors and enable rollbacks.

- You must factor in image download times for deployments.

## Diagram

![diagram](diagram.png)

## Pros

- Uniquely identify a model file version by the server/container image version.

## Cons

- A model training and image building pipeline must be defined.
- Image building and deployment latency may be problematic.

## Considerations

- The exact design of the standardized, ideally automated, image building/deployment
  pipeline.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter3_release_patterns/model_in_image_pattern
