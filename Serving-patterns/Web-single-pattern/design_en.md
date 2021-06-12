# Web Single Pattern

## Use Case

- You want to quickly release a predictor using the simplest architecture.

## Architecture

In the Web Single Pattern, all prediction model artifacts and code are bundled together
within a single web server. Since the preprocessing pipeline, trained model, and web
service (e.g, REST or RPC-based) are contained in a single application, they can be
deployed together to quickly deliver a useful prediction service.

- For RPC-based APIs (as in gRPC), you need to consider client-side load balancing or
  layer-7 load balancer.
- To deploy multiple replicas, they must be deployed behind a load balancer or proxy.
- For production deployments, you can either adopt
  the [Model-In-Image Pattern](./../../Operation-patterns/Model-in-image-pattern/design_en.md)
  or
  the [Model-Load Pattern](./../../Operation-patterns/Model-load-pattern/design_en.md).

## Diagram

![diagram](diagram.png)

## Pros

- Less development complexity; the same programming language (e.g., Python) can be used
  for the web server, preprocessing, and inference components and they can be
  implemented in the same address space.
- Easy to manage and troubleshoot due to its inherent simplicity.
- Minimal time-to-production post model training.
- The simplest, and thus recommended, starting point for a production architecture when
  deploying models in a synchronous serving fashion.

## Cons

- Since all components are packed in a single server or docker image, applying a small
  patch will require updating and restarting the whole application and/or image.
- Updates will also require a service deployment. In larger organizations, this often is
  necessitates adhering to a hefty SDLC

## Considerations

- Update and maintenance procedures for each component.
- Scaling change management of the web server.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter4_serving_patterns/web_single_pattern
