# Overview

Konduit project requested support for SAP specific Cloud Events compliant extension (`comSap*` event attributes as documented [here](https://jam4.sapjam.com/groups/OYbHBAQTuZvNhJcgKTSoJZ/documents/ki7YH4FdrvyM31Zon6o97a/slide_viewer)) and SAP Passport (as specified [here](https://jam4.sapjam.com/groups/OYbHBAQTuZvNhJcgKTSoJZ/documents/qtwddT6iIjJnmEqKLgLebf/slide_viewer)).

**Proposal**
* Near term (i.e. for Sapphire 2019) solution
  * Implement support for configuring OSS Kyma EventBus (Event Service API and Event publishing API) with whitelist of (patterns of) optional headers which if present should be passed through, from event publishing request to event consumption/delivery request
    * Note: `comSAPRefObjectIDs` map should be serialized by event producer as [exploded](https://swagger.io/docs/specification/serialization/#header) header value
  * Configure SAP CP XF EventBus installations to pass through `comSap*` and `SAP-PASSPORT` headers
* Long term solution
  * Work with CNCF Serverless-WG to release Cloud Events specification 1.0
  * Work with Knative on supporting Cloud Events compliant event ingress API, with custom extension support
  * Migrate users from legacy custom EventBus APIs to Cloud Events compliant Knative eventing APIs
