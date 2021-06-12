# Prediction Log Pattern

## Use Case

- Service improvement via data gleaned from prediction, latency, and other logs
- DWH log-storage volume is a concern
- Log-based monitoring and alerting

## Architecture

Logging to both analyze and improve your service is a mandatory cross-cutting concern.
The log may include prediction result along with input, latency, the client event, and
any other related activities.

- Even though separate logs may be produced by each system component, recording them in
  a single DWH is often appropriate.
- Using a queue to aggregate log may reduce DWH load and prevent logs from being lost,
  though one must consider if log processing latency affects log freshness.

Logs are useful in many situations. For instance,

- Good logging enables workflow anomaly detection for unexpected or historically odd
  predictions or user behaviours. In these situations, automated alerting to analyze and
  resolve these anomalies are highly valuable.

- Input data format may change with very little change in client code; if you can
  observe a system outage with that change, you can quickly identify the precipitating
  factor.

- A model may produce an erroneous prediction despite no obvious failure of the overall
  system. An alert for the prediction system and model prediction log can significantly
  improve both the mean time to respond and mean time to resolve.

## Diagram

![diagram](diagram.png)

## Pros

- Able to analyze prediction effect.
- Alerting

## Cons

- Log storage may increase cost.

## Considerations

- Log frequency and log level.
- Storing frequency and backup.
- Purpose of analysis.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter5_operations/prediction_log_pattern
