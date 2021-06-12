# Microservice Vertical Pattern

## Use Case

- Multiple inferences which will be executed in cascade, either by choice or out of
  necessity due to ordering dependencies between inferences (i.e. some topological
  ordering)

## Architecture

The Microservice Vertical Pattern allows you to run multiple models in order. The
pattern deploys prediction models are deployed as separate services (in separate servers
or containers).Prediction requests are executed synchronously and in order, with results
aggregated and returned to the client

- Each prediction service has a separate maintenance lifecycle and provides a level of
  fault isolation for deploying the servers independently
- A reverse proxy between the client and prediction services is responsible for handling
  requests and responses, coordinating inference execution ordering and result
  aggregation. Additional data retrieval may also be done by the proxy or each
  predictor (`Diagram2`)
- An advantage of the reverse proxy is that it provides an implicit caching mechanism
  which reduces latency and the number of requests to a data warehouse or other backend
  storage. Additionally, it abstracts away more complicated application logic from the
  prediction services themselves, allowing for complex/robust workflows.

## Diagram

### Diagram1

![diagram1](diagram1.png)

### Diagram2 (additional data retrieval by the proxy server or prediction services)

![diagram2](diagram2.png)

## Pros

- Multiple predictions may be executed in any order.?
- Prediction services may be conditionally selected based on predictions of other
  services.
- Resource usage efficiency gains are possible as the proxy server and independent
  prediction services can be given a separate set of resources conditioned upon their
  particular workloads (i.e., GPUs for some prediction services, lots of RAM for the
  proxy servers' in-memory cache)
- A failure in a single service can be isolated from the overall system and remediated
  conditionally (i.e., prediction services can have redundant replicas behind a load
  balancer), improving uptime and availability.

## Cons

- Significant prediction latency due to synchronous execution which may become a
  performance bottleneck
- Relatively more complex system architecture and workflow.

## Considerations

- Explicit performance tuning may be needed to ensure compliance with your SLA.
- Standardized interfaces and servers become a necessity to deal with the more complex
  system architecture and workflow
