# Online Bigsize Anti-Pattern

## Case

- Average prediction latency does not meet the corresponding non-functional requirement.

- in batch systems, the number of predictions and average prediction latency is longer
  than expected.

- In an online service or system that requires realtime responses, a bigsize model with
  significant inference times is being used.

## Situation

In general, in any business or system, time is limited and has an associated cost.
Additionally, any service has a completion time requirement or expectation.

- In a web service, the requirement might be mean time to respond/resolve (MTTR) for
  each request.
- For a batch system, the requirement might be successfully processing 100M records in
  six hours, with a midnight deadline.

A common metric for machine learning systems is average prediction time (in seconds).
When an explicit time is codified in a concrete SLO, any model or prediction system must
meet this requirement.

This is especially difficult in the context of computationally intensive models with
long prediction times, such as deep learning models. In this case, the system must be
optimized in some way to meet the non-functional requirements of the system, and
consequently, corresponding SLOs.

- Scaling resources up or out, or using specialized hardware such as GPUs or TPUs, may
  sufficiently improve inference times.
    - Caveat: both solutions have associated costs.
- Finally, using a simpler model may provide the appropriate tradeoff between cost,
  performance, and latency.

There is no single best answer to address the model evaluation and speed tradeoff.

It is important to define service level of the evaluation and speed according to
business and system needs.

## Diagram

![diagram](diagram.png)

## Pros

- Evaluation may be better on a big and complex model.
- It is fun making a complex model.

## Cons

- Need to take balance of speed, cost and accuracy.
- It is also fun making a simple and reasonable model.

## Work around

- Define latency or speed required for business use or system to evaluate the model
  quality, not only of accuracy.
- Try using GPU, or scale out, if it is cost-effective.

## Related design pattern

- [Prediction Cache Pattern](./../../Prediction-cache-pattern/design_en.md)
- [Data Cache Pattern](./../../Data-cache-pattern/design_en.md)
- [Loading test pattern](./../../../QA-patterns/Loading-test-pattern/design_en.md)
- [Prediction Log Pattern](./../../../Operation-patterns/Prediction-log-pattern/design_en.md)
- [Prediction Monitoring Pattern](./../../../Operation-patterns/Prediction-monitoring-pattern/design_en.md)
