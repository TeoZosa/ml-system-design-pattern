# Training-To-Serving Pattern

## Use Case

- To design end-to-end workflow of machine learning model into production.
- To release a model right after training.
- To automatically deploy a model into production.
- When your model training is stable enough.
- When you need to update models frequently.

## Architecture

When you want to design an architecture and workflow to connect training and serving,
you will be combining the training patterns and serving patterns. If your model needs to
be continuously deployed after training pipeline runs, you can use the
Training-To-Serving Pattern.

The aim of the pattern is to build and release the model server automatically once
training completes. If your use case requires frequent model updates and manual
evaluation is unnecessary, then this pattern is a good fit.

For the training pipeline, you may choose
the [Batch Training Pattern](../../Training-patterns/Batch-training-pattern/design_en.md)
or
the [Pipeline Training Pattern](../../Training-patterns/Pipeline-training-pattern/design_en.md)
.

It is a bit risky to select
the [Parameter and Architecture Search Pattern](../../Training-patterns/Parameter-and-architecture-search-pattern/design_en.md)
for its trained model quality may not be stable.<br>

### Operation Patterns

To connect the training and serving workflows, either
the [Model-Load Pattern](../../Operation-patterns/Model-load-pattern/design_en.md) or
the [Model-In-Image Pattern](../../Operation-patterns/Model-in-image-pattern/design_en.md)
can be used. Selection criteria depend on model and prediction server management
desiderata.

- The [Model-Load Pattern](../../Operation-patterns/Model-load-pattern/design_en.md) is
  appropriate if you want to update the model without changing the current server
- while
  the [Model-In-Image Pattern](../../Operation-patterns/Model-in-image-pattern/design_en.md)
  is a good choice if you need to update the whole server along with the model.

For service management,
the [Prediction Log Pattern](../../Operation-patterns/Prediction-log-pattern/design_en.md)
and
the [Prediction Monitoring Pattern](../../Operation-patterns/Prediction-monitoring-pattern/design_en.md)
are mandatory.

### Serving Patterns

For serving, a potentially good starting point is
the [Microservice Horizontal Pattern](../../Serving-patterns/Microservice-horizontal-pattern/design_en.md)
. This pattern aims to deploy a new prediction server in parallel with the others, and
the reverse proxy discovers the new service to be added to the prediction target via 
a service discovery mechanism.

The model can be automatically released after training once model training and
evaluation pipelines are in a stable, fully-automated state.

- If the pipeline is not stable, then the whole workflow would be unstable.
- If the quality of the trained model fluctuate between releases, the pattern may be
  risky.

It is also important to consider whether or not specific models should be in production.
If a model is not necessary or useful for any reason, e,g, it is out of date or has
degraded performance, it must be eliminated.

- Operation becomes simple if prediction servers are removed after a predefined amount
  of time has elapsed, though this also poses the risk of a model still in use being
  removed prematurely.
- On the other hand, if possible, regularly evaluating the production model against an
  outdated one may be a good idea, though this increases the operational complexity
  associated with managing the evaluation process and risk of a stale model remaining in
  production.
  
## Diagram

![diagram](diagram.png)

## Pros

- Release right after training.
- Frequent release.

## Cons

- Requires training pipeline, auto release, and service discovery.
- Not suitable for unstable training.

## Considerations

- Stabilize training, automate pipelines and requires service level on each phase.
- Service discovery and removal policy for serving.
