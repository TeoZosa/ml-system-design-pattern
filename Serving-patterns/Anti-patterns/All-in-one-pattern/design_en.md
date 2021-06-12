# All-In-One Anti-Pattern

## Case

- Multiple inference models deployed in a single container, server, or server group.

## Situation

While there are situations where multiple inference models must be deployed for a single
product, they should not be deployed in the same container, server, server group.

Running multiple models in a monolithic environment may yield a negligible cost
reduction but does so at the expense of increased operational cost due to increased
system complexity.

- One disadvantage of this anti-pattern is that all models share the same libraries.
  Given the rapid pace of ML library and algorithm development, tightly coupling models
  together in this way prevents models from using the exact libraries and versions that
  are most appropriate for each model.

- Another disadvantage arises during incident resolution. Root-cause analysis in a
  monolithic architecture necessitates log tracing across logs for the entire monolith
  regardless of the number of culprit components. Isolating faults and troubleshooting
  invalid model predictions becomes extremely difficult, increasing the mean time to
  repair.

- Finally, another disadvantage occurs during system or model updates. Depending on how
  the models themselves are
  deployed, [Model-In-Image Pattern](../../../Operation-patterns/Model-in-image-pattern/design_en.md)
  or [Model-Load Pattern](../../../Operation-patterns/Model-load-pattern/design_en.md),
  a system update for one component will require an unnecessary model update for all
  models, and vice versa. Despite the fact that system and model release cadences may
  differ, in a monolithic system updates will nevertheless be triggered simultaneously,
  increasing operational cost.

It is recommended to deploy in microservice architecture of one model per one server on
running multiple models.

## Diagram

![diagram](diagram.png)

## Pros

- Negligible cost savings

## Cons

- Increase in dev and ops cost.

## Work around

- Adhere to the Single-Responsibility Principle, using microservices to enforce the 
  separation of concerns between servers and models. 

## Related design pattern

- [Prep-pred pattern](./../../Prep-pred-pattern/design_en.md)
- [Microservice vertical pattern](./../../Microservice-vertical-pattern/design_en.md)
- [Microservice Horizontal Pattern](./../../Microservice-horizontal-pattern/design_en.md)
