---
title: Overview of openEHR REST APIs
summary: This section provides an overview of the various REST APIS used to access openEHR CDRs.
---

# Introduction

Although the basic approach of interacting with openEHR CDRs via a simple service layer has been well established for some time, until recently, each CDR vendor had their own RESTful API, albeit these worked in a very similar fashion.

In recent years the CDR implementer community has agreed a common standardised [openEHR REST API](https://specifications.openehr.org/releases/ITS-REST/latest/index.html)

This has now been implemented by a number of CDR providers, though most continue to make use of their 'proprietary variants' alongside the standard API.

This documentation and related technical artefacts will cover the standard openEHR REST API, as well as the equivalent calls to the [Better Ehrscape API](https://dev.ehrscape.com/api-explorer.html), which is widely used in the UK, and in particular is supported by the Ripple Ethercis CDR.

One significant difference is that Better Ehrscape API allows openEHR records to be submitted via some simplified JSON formats which are very helpful to those new to openEHR. Work is underway to bring this kind of 'simplified JSON' into the openEHR standard space and we also anticipate some other vendors to emulate the Better Ehrscape JSON formats until the standardised simplified format is agreed.

To be clear, these simplified formats are used for convenience only, and within the CDR the data is stored and can be retrieved and queried in a completely standard fashion via the openEHR REST API.

### Differences between Better Ehrscape and openEHR REST APIs

Conceptually these APIS are very similar with almost identical REST resources.

For example the `List templates` call in Better Ehrscape is 

```bash
curl --location --request GET 'https://cdr.code4health.org/rest/v1/template' \
--header 'Accept: application/json' \
--header 'Authorization: {{authToken}}'
```

while in the openEHR REST API it is 

```bash
curl --location --request GET 'https://cdr.code4health.org/rest/v1/definition/template/adl1.4' \
--header 'Accept: application/json' \
--header 'Prefer: return=minimal' \
--header 'Authorization: {{authToken}}'
```

The basic message is that if you become familiar with the Better Ehrscape API, jumping to, or intermixing with, the openEHR REST API will not be too difficult.







