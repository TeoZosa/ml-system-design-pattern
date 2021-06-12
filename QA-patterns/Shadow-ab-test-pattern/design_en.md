# Shadow AB Test Pattern

## Use Case

- To confirm the a new prediction model works with the production data.
- To verify a new prediction server can load the production access info.

## Architecture

The Shadow AB Test Pattern is an architecture to verify multiple prediction models with
the **production data and load**.

- In this pattern, you will deploy _multiple_ prediction servers, sending requests to
  **all** the services but only forwarding the response from the current model to the
  client; predictions from other models will not be sent to the client.

- The reverse proxy server will store all the prediction results with profile to DWH,
  recording predictions along with latency to verify quality of the new model service
  without affecting client experience.

If there are any issue with the new model, the prediction service will be eliminated
from AB testing and not be deployed to the production environment.

- You need to consider the term-length of testing. If the service has seasonal effect,
  you may need to run longer term, while if the service is used every day in a similar
  manner, the performance can be concluded in a few weeks. There may be a chance that
  you may find the result in shorter term. It is important to make the go or no-go
  decision based on the effect of the new model replacing the current one.
- In contrast to the [Online AB Test Pattern](../Online-ab-test-pattern/design_en.md),
  the Shadow AB Test Pattern will allow you to compare the current and new models with
  less risk. On the other hand, since the pattern will not send the new model prediction
  to the client, it is difficult to measure its business impact.
- It is recommended to apply
  the [Online AB Test Pattern](../Online-ab-test-pattern/design_en.md) once the model
  goes through the Shadow AB Test Pattern.

## Diagram

![diagram](diagram.png)

## Pros

- You can verity the new model performance without affecting the production service.
- It is possible to record multiple predictions.

## Cons

- Additional cost.

## Considerations

- Evaluation and decision policy producing the go or no-go decision for the new model

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter6_operation_management/shadow_ab_pattern
