# Prediction Monitoring Pattern

## Use Case

- Prediction monitoring and automated alerting on unexpected trends
- Prediction trend and statistics management

## Architecture

System-level logging and monitoring to both analyze and improve your service is a
mandatory cross-cutting concern for production service operations. Additionally,
prediction results monitoring may also be prudent, especially for a production system
with service level to the model.

In the Prediction Monitoring Pattern, inferences are monitored for suspicious results,
i.e.,

- When there are too few or too many predictions of a certain class in a given length of
  time, e.g., too many anomalies detected by an anomaly detector.
- When there are too few or too many requests compared to what is typically expected,
  e.g.,
    - 1000 RPS happening on 100 RPS-expected service
    - 0 requests for an extended period of time
- Continuous requests on the same input data, e.g., continuous retries for a certain
  input or a DDOS attack.

In all cases, it is necessary to analyze incident to normalize the service which
requires a clear definition of normal and abnormal conditions on which to monitor and
alert.

- While it depends on request frequency, it is generally uncommon to assume a low number
  of predictions in a web service constitutes an anomaly. More often, long-term trends
  are determined from empirical observations of the logs and used to determine what
  constitutes an anomaly in the context of the specific system being observed. This can
  be achieved via regular log storage queries/monitoring or even via a log-visualization
  dashboard.

Monitoring and alerting configurations and operations depends on the service level of
the specific service. It is important that your team address alerts by priority 
of the service level and importance of the service.

- If it is critical to a large business or users, then even small anomalies may require
  alerts with an SRE on-call 24/7 for immediate incident resolution.
- On the other hand, if the service is not critical, then daytime-only alerting may be
  sufficient.

## Diagram

![diagram](diagram.png)

## Pros

- Observe anomaly and start fixing an incident with alert.

## Cons

- Unnecessary alert may cause increase in operational cost.

## Considerations

- Service level.
- Monitoring and alert configuration and operation based on the level.
- Playbook.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter5_operations/prediction_monitoring_pattern
