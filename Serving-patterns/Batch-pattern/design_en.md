# Batch Pattern

## Use Case

- No real-time/near-real-time prediction requirements.
- Non-streaming (e.g., Batch) predictions
- Batch predictions jobs can be scheduled (hourly, daily, weekly, monthly, etc.)

## Architecture

If real-time predictions are not needed, you may choose the Batch Pattern to run
prediction requests at desired intervals. In the Batch Pattern, you can schedule batch
prediction jobs to regularly process batches of data and store the results.

- This pattern requires a _job management server_ to trigger the batch jobs, which will
  launch the prediction server, as per your defined rules.
- If you are using a cloud service or Kubernetes, the Batch Pattern enables you to
  reduce your costs drastically as the prediction server is ephemeral; it is not running
  24x7.

## Diagram

![diagram](diagram.png)

## Pros

- Server resource management flexibility; on-demand server provisioning
- Simple error recovery; non-pathological failed prediction jobs may simply be rerun
- Server system does **not** need to provide high _availability_

## Cons

- Requires a job management server.

## Considerations

- Batch jobs may need to be split into mini-batch jobs depending on their size; if the
  batch size for the defined interval is too large then it needs to be split and
  coordinated among several mini-jobs.
- Batch job schedule and server resources need to be balanced against any prediction
  result deadlines. For example, a nightly batch may need to be finished by the next
  morning.
- Options to rerun the job in case of failure:
    - **Complete retry**: rerun prediction on the entire batch.
        - Used when there are dependencies between predictions or data.
    - **Partial retry**: rerun prediction only on failed jobs.
        - Used when there are no dependencies between predictions or data.
    - **No retry**: run prediction on the failed jobs on the **next** batch.
        - Used when there is no strict prediction result deadline.
- If the batch interval is considerable (e.g, once a month/year), it is recommended to
  run and monitor test batch jobs in the interim to ensure the model or system is not
  outdated.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter4_serving_patterns/batch_pattern
