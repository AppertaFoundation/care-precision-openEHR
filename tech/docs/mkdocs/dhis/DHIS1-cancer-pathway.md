# Overview

This section covers some examples that are very specific to the DHI-Scotland Cancer pathways project.

The demonstrator use-cases are ...

### 1. Work with the NDP ReSPECT form

Access a patient record from an openEHR CDR that simulates the National Digital Platform (NDP-CDR), identify the current ReSPECT form, and query for some limited information for display in the PHR app (Cohesion). Allow a third-party PDS(Mydex) to access this composition, by supplying a suitable access token and the compositionID of the Respect form)

The initial proposed dataset is
- the uid of the ReSPECT composition
- the date last committed and status and author name
- the clinical leads responsible for the form.
- The patient preferences.
- the clinical recommendation, including the specific CPR (resuscitation) decision

The exact details to be discussed with McMillan  but the principles will not change.
  
#### Technical requirements

##### For PHR (Cohesion)

 - Retrieve the patients NDP-CDR `ehrId` from their CHI Number - see [Retrieving the patient's ehrID](DHIS2-retrieving-an-ehrId.md) 
 - run an AQL query to find the current ReSPECT form (if it exists) and display the queryed data (as above) - see [Querying NDP ReSPECT](DHIS3-querying-ndp-respect.md)
 - Pass an access token and compositionId to PDS, so that PDS can access the composition from NDP-CDR (or perhaps proxied through PHR).


##### For PDS (Mydex)

 - Retrieve the patients NDP `ehrId` from their CHI Number - see [Retrieving an ehrID](DHIS2-retrieving-an-ehrId.md) 
 - Retrieve the composition from NDP-CDR (perhaps proxied through PHR) - see [Retrieving NHP ReSPECT composition](DHIS4-retrieving-ndp-respect.md)


### 2. Work with NDP-stored Cancer-specific PROMS

Allow patient to enter some cancer-specific PROMS information via their PHR app (Cohesion) and have it stored in the NDP-CDR. Potentially also display all recent PROMS data (however committed) via a query to the NDP-CDR. Allow third parties (e.g. MyClinicalOutcomes to add and query data in the same way, to demonstrate app independence).


#### Technical requirements

##### For PHR (Cohesion) PROMS app (MCO)

 - Retrieve the patients NDP `ehrId` from their CHI Number - see [Retrieving the patient's ehrId](DHIS2-retrieving-an-ehrId.md) 
 - run an AQL query to find recent PROMS records and display subset of results (table or graph) - see [Querying PROMS data](DHIS5-querying-proms-data.md)
 - Commit a composition to the NDP-CDR via a composition (STRUCTURED format) - see [Committing PROMS data](DHIS6-committing-proms-data.md)
 - Retrieve that composition - see [retrieving PROMS data](DHIS7-retrieving-proms-data.md)


!!! important "Better Ehrscape API vs. openEHR REST API"

   For now, we suggest that we make use of the Better Ehrscape API, rather than the openEHR REST API, even though the latter is what will be used by the actual NDP-CDR which use the ehrBase CDR and not the Better CDR. 

   The primary reason is that, right now, Better support some simplified data formats which are easier for third-party vendors to work with. We know that ehrBase is actively working on support for these formats, and an early release is imminent, so this advice may change.

   We will supply some documentation to show how, once committed, the same data can be accessed and queried via the openEHR REST API.






