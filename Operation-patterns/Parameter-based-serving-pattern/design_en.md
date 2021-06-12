# Parameter-Based Serving Pattern

## Use Case

- Rule-based predictions governed by parameters (feature flags)

## Architecture

In general, it is impossible to edit parameters in a trained model. On the other hand, a
model may not always align with business logic or system requirements.

- If the model in production is giving negative effect on your business for some reason,
  you may need to update the model, or remove prediction functionality from the service.
- If it takes long to retrain and deploy the model to production, prediction
  functionality may need to be removed temporarily. There may be a chance that your
  prediction is anomalous only for a certain input data, and all the others are right.
  In that case, you still need to either retrain the model, or eliminate prediction for
  that particular kind of data.
- When you need to implement a machine learning prediction into a production service,
  high accuracy does not always directly translate into high business impact; edge cases
  or systematic issues may need to be mitigated in some rule-based ways.<br>

For those cases, it is useful to add feature flags: a mechanism in your code to change
behaviour of all or a part of the predictions, including stopping, retrying or
timing-out.

These may be passed into the application directly via arguments to the initial execution
command or via environmental variables (especially useful in container-native
application).

Since it is difficult to maintain highly-accurate, error-free model predictions for
every possible input, it is better to anticipate possible anomalies and implement
failure-recovery mechanisms backed by corresponding feature flags. Given that it is
impossible to anticipate and address every pathological state, a general `Activate` flag
which can be used to completely disable prediction functionality is often recommended.

## Diagram

![diagram](diagram.png)

## Pros

- To avoid abnormal prediction for edge cases.

## Cons

- Impossible to cover all the cases.
- Rules increase operational complexity given the number of now possible system states.

## Considerations

- Which cases to control with what variable.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter6_operation_management/paramater_based_pattern
