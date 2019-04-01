# Overview

Based on the recent feedback received from the stakeholders, hackathon participants, it was identified that there is a need to improve the event delivery mechanism.

The problems faced during the recent events and day-to-day interaction with Kyma in regards to event delivery can be categorized into following:

## Missing troubleshooting support
At present, there is some support for developers using tracing to identify any mistakes commited with regards to:

* Configuration errors.
* Errors in services written by developers.

However, this does not cover all aspects of how things can go wrong. This includes some situations such as:

* Invalid Subscription custom resource. 
There is no feedback at present for developers to know if they have some syntax error in Subscription custom resource.

* No Status information.
There is no feedback for the developer to know if the system has set up everything correctly and it is in a state where the events will start getting delivered to his lambda or microservice.

In the technical terms this implies following:
* Event activation check was performed and status was updated.
* NATS Streaming subscription was started successfully.
  At present, only the event activation status is updated, but the low level NATS Streaming Subscription started or not stays unknown to developers.

**Proposal**
* Implement validation for Subscription custom resource. 
  * This will provide early feedback and enable developers to fix any issues with the custom resource.
  * The validation of Custom Resoirce is available via the [Validation beta feature](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/) avaialble in K8S v1.13.

* Update subscription custom resource status.
  * This will provide a feedback channel for the developers to understand if the system has done correct setup so they can receive events. 
  * The [status subresoure feature](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/#subresources) can be used.
  * This will also be integrated into the lambda UI.

## Missing relevant examples
The examples that we have today are:
* Self-contained
* Assume all steps being done via CLI.

However, in the actual integration scenarios e.g `Kyma <---> CCV2` and similiar, many steps are either already done or done via the Kyma Console UI.
This creates confusion among the developers when they refer current Kyma examples thus duplicating or misdoing some steps and ending up with unexpected errors.

**Proposal**
* Have examples to write lambda and microservice that are triggered by external events.
  The example should provide a script that is same to the one in a normal integration scenario.


## Unstable system
It was observed during the hackathon events that at some point, the applications stopped reacting to Subscription custom resource creation. The actual technical reason still stays unknown.
However, one aspect observed is that we do not have controllers implemented with the best standards. 
The controllers are supposed to react to Subscription custom resources lifecycle events to perform the backend work such as NATS Streaming susbcription creation or deletion.

**Proposal**
* Use #sig-quality group to set up best practices and guidelines for writing controllers.
* Apply the best practices for the controllers used in event-bus.
* Improve logging in the controllers.
