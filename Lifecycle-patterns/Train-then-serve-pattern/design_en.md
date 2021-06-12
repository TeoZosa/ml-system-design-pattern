# Train-Then-Serve Pattern

## Use Case

- To design end-to-end workflow of machine learning model into production.
- When you want to separate training and release into different workflows.
- To manually evaluate model for release quality.
- To evaluate models in production.

## Architecture

When you want to design an architecture and workflow to connect training and serving,
you will be combining the training patterns and serving patterns. You can use this
Train-Then-Serve Pattern, a mixture of multiple patterns, to manually release a trained
model after evaluation. Since the workflow includes a human-in-the-loop QA component to
ensure high model and system quality, it is _not suitable for requirement with frequent
model release_.

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

For production serving,
the [Parameter-Based Serving Pattern](../../Operation-patterns/Parameter-based-serving-pattern/design_en.md)
enables prediction behavior updates simply by modifying an environment variable in the
reverse proxy.

For service management,
the [Prediction Log Pattern](../../Operation-patterns/Prediction-log-pattern/design_en.md)
and
the [Prediction Monitoring Pattern](../../Operation-patterns/Prediction-monitoring-pattern/design_en.md)
are mandatory.

### Serving & QA Patterns

The specific serving and QA patterns depend on the production requirement which will
naturally imply a specific combination. The diagram shows usage of
the [Web Single Pattern](../../Serving-patterns/Web-single-pattern/design_en.md) for
serving and
the [online AB testing pattern](../../QA-patterns/Online-ab-test-pattern/design_en.md)
for QA.

The log will be recorded into a DWH to be used to improve the model and retraining.

An advantage of separating training and serving phases is the ability to evaluate your
model before release.

- If the evaluation based only on your test dataset is not good enough for release, or
  if manual QA is required, then this pattern may be a good fit.
- In addition, the pattern separates the training and serving phases to isolate issues
  in the training pipeline from the release and serving systems, strengthening service
  availability.
- On the other hand, it is not suitable for use cases which require frequent or realtime
  model updates.

## Diagram

![diagram](diagram.png)

## Pros

- Manual model evaluation before release.
- Isolate workflow and failure in each phase.

## Cons

- Not automated.

## Considerations

- Combination of training, QA, operation and serving patterns.
- Release standard.
- Release frequency.
