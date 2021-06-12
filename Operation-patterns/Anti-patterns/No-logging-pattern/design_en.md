# No Logging Pattern

## Case

- Not logging or profiling service

## Situation

Logging and monitoring to analyze, improve, and effectively operate your service is
crucial for all production services and systems. Without logging, the system becomes a
blackbox which makes it very difficult, if not impossible, to identify and troubleshoot
errors or improve the system.

For machine learning systems in particular, tracing inference results with related event
logging enables system and model improvement as well as clear business planning.

An interesting and challenging aspect of working with machine learning is that machine
learning in nature is tightly related to business goals and/or user experience. Machine
learning can deliver high-value business insight or sophisticated automation  
more effectively, easily, and reliably than traditional if-else statements.

Note that influencing business or user behavior, or even physical world, requires
alignment with the actual environment, which needs traceability from both the model and
system.

## Diagram

![diagram](diagram.png)

## Pros

- You don't have to pay for log storage.

## Cons

- You cannot operate and improve your system.

## Work around

- At least, get logs of fatal, error, warning and info levels.
- Define traceable event logs and implement.

## Related design pattern

- [Prediction Log Pattern](./../../Prediction-log-pattern/design_en.md)
- [Prediction Monitoring Pattern](./../../Prediction-monitoring-pattern/design_en.md)
