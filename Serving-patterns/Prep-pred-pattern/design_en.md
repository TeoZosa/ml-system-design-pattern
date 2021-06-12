# Preprocess-Prediction Pattern

## Use Case

- Preprocessing and prediction have different codebases, libraries or resource load
  requirements.
- When you want to improve availability by separating preprocessing from prediction,
  isolating failures within associated resources.

## Architecture

There are cases when the requirements for the preprocessing stage and the prediction
stage are different.

- Examples of steps in a preprocessing stage include normalization or standardization
  for numerical data, one-hot encoding for categorical data, vocabulary filtering for
  text data, resizing for image data, and so forth, and these steps can be pretrained or
  rule-based.
- On the other hand, a prediction stage typically serves a pretrained model or
  binarized model file which returns a prediction given input from the preprocessing
  stage.
    - For example, the preprocessing steps may be implemented in Python while the
      prediction model may be a binary built with Tensorflow or ONNX.
- Given these differences, explicitly separating these services into discrete
  servers/containers allows us to independently optimize the development and operation
  of each resource.
    - Note: you need to consider tuning, network connection, versioning for each
      resource independently.

While this makes the system complex than
the [Web Single Pattern](../Web-single-pattern/design_en.md), the Preprocess-Prediction
Pattern enables independent development, fault isolation, and efficient prediction
serving resource utilization.

This pattern is applicable across many use cases, especially when using deep learning
models.

`Diagram2` depicts the Microservice Prep-Pred Pattern which deploys a reverse proxy in
front of the preprocessing and prediction services so that each may be treated as a
discrete microservice. In this case, the proxy will mediate data retrieval and calls to
the preprocessing and prediction services.

- This architectures allows independent development, with independent libraries,
  languages, and infrastructure for each resource.
- However, the additional components increase overall system complexity. Managing and
  troubleshooting issues within these components requires a deep understanding of each
  component and their interactions.

## Diagram

### Simple Prep-Pred Pattern

![diagram1](diagram1.png)

### Microservice Prep-Pred Pattern

![diagram2](diagram2.png)

## Pros

- Efficient resource utilization and fault isolation
- Resource usage and scalability flexibility
- Each component may use separate libraries, languages, and infrastructure.

## Cons

- Increased operational cost due to increased system complexity.
- Network latency between preprocessing and prediction services may become a performance
  bottleneck.

## Considerations

- Not aligned with the model training stage; during development, it is more appropriate
  to strongly couple preprocessing and prediction stages.
- If preprocessing and prediction stages are developed separately, they may lead to
  incorrect (buggy) predictions even though the system as a whole may _seem_ to be
  functioning correctly.
- Resources must be tuned separately.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter4_serving_patterns/prep_pred_pattern
