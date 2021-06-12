# Online AB Test Pattern

## Use Case

- To confirm the a new prediction model works with the production data.
- To verify a new prediction server can load the production access.
- To test business impact of the model in production.
- To test the model will not worsen the impact than the current one.

## Architecture

The Online AB Test Pattern is an architecture to verify multiple prediction models with
the **production data and load**.

- In this pattern, you will deploy _multiple_ prediction servers, load balance among
  them with higher load initially on the current model, and gradually increase the
  access to the new server, akin to a rolling deployment.

Load balancing will be managed by the proxy server. The proxy will gather the request
data and prediction along with originating server identity, and record them in a DWH.

- You may need to trace the client event log to compare the impact of the new model.
- The load balancing rule may be considered depending on the objective.
    - If your aim is to compare user activity, it might be better to assign users to a
      constant model.
    - If your aim is to log the prediction result, you may choose to randomly balance or
      send request to all the predictions.


If there are any issue with the new model, either in terms of prediction quality,
latency, or availability, the deployment should be rolled back with new prediction
servers eliminated from the production environment.

- You need to consider the term-length of testing. If the service has seasonal effect,
  you may need to run longer term, while if the service is used every day in a similar
  manner, the performance can be concluded in a few weeks. There may be a chance that
  you may find the result in shorter term. It is important to make the go or no-go
  decision based on the effect of the new model replacing the current one.
- In contrast to the [Shadow AB Test Pattern](../Shadow-ab-test-pattern/design_en.md),
  the Online AB Test Pattern enables direct measurement of business impact through the
  comparison of the effects of current and new model predictions on user behavior,
  though doing so at the expense of increased risk.
- It is recommended to apply the Online AB Test Pattern _after_ the model goes through
  the [Shadow AB Test Pattern](../Shadow-ab-test-pattern/design_en.md).

You will let the new model to be online with responding the prediction to the client. It
is important to note that it will affect business or user experience.

## Diagram

![diagram](diagram.png)

## Pros

- You can verify the new model performance without affecting the production service.
- It is possible to record multiple predictions.

## Cons

- It may make a negative impact on your business if the model or server is not good.
- Additional cost

## Considerations

- Load balancing policy.
- Evaluation and decision policy of go or no go for the new model.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter6_operation_management/online_ab_pattern
