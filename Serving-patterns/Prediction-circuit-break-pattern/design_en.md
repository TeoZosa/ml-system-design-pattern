# Prediction Circuit Breaker Pattern

## Use Case

- When there is a possibility that the amount or frequency of prediction requests will
  suddenly increase
- If immediate scale out to respond the sudden request is not needed.
- If a 100% response-rate is not necessary.

## Architecture

There are occasions when the number of access to the web service (or related service)
suddenly increases due to a campaign or external event. If you are using a cloud
provider and/or Kubernetes, you can auto-scale your service to respond to the requests.
However, there are many cases when the increased number of requests can outpace the
scale-out speed. This is especially true when the server or container image contains a
model file and launching or downloading the file has a significant setup time.

The prediction circuit breaker pattern is an architecture to avoid `complete outage`
until the scale out event succeeds.

- Prediction services faced with too many requests may fail and restart, temporarily
  reducing the resource pool. Therefore, in order to stabilize the current prediction
  service until the scale out completes, we service as many prediction requests as
  possible, terminating requests above a certain limit at the reverse proxy server, only
  forwarding remaining requests to the prediction server.
- The important point of the pattern is to have a fallback plan for cancelled requests.
  User experience degradations must be minimized and client activity should not stop. It
  is recommended to consider a workflow for cancellation.

## Diagram

![diagram](diagram.png)

## Pros

- Avoid complete outage of the service; a partial outage is preferable to a complete
  outage.
- Prediction servers can be scaled out without lowering the current resource
  availability.

## Cons

- Requires a fallback plan for cancelled requests.

## Considerations

- Fallback plan and workflow for cancellation.
- The circuit breaking limit should be high enough to respond to usual increases in
  service requests.
