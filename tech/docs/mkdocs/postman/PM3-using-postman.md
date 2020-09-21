---
title: Using Postman with Ehrscape
---

# Create Session (Ripple Ethercis only)

You can skip this step if you are not using the Ripple Ethercis CDR.

The first step is to create an openEHR session and retrieve
the **sessionId** token. This allows subsequent API calls to be
made without needing to login on each occasion.

Navigate to the *session* folder and highlight **Create Session**
on the left, then click on the **Send** button. The required
credentials are automatically filled in from the Pre-sets file (see
**Navigating Postman** section above)

![Create Session](/images/CreateSession.jpg)

Click the **Scroll to responses** button in the bottom right hand
corner to display the response details.

The screenshot below shows the session Id which has been returned in the
call.

![Session ID](/images/CreateSessionResult.jpg)

# Get EHR Identifier

The next step is to get the patient’s internal EHR identifier by sending
their external identifier (in this case an NHS Number). The ehrId is a
unique string which, for security reasons, cannot be associated with the
patient, if for instance their openEHR records were leaked.

Select **Get ehrStatus from subjectId** in the **ehr** folder and
then click on the **Send** button. Again, the patient’s NHS number is
taken from the Pre-sets file and is therefore filled in automatically.

![Get EHRId](/images/GetEhrId.jpg)

Click on the **Scroll to responses** button in the bottom right hand
corner to display the response details.

The JSON snippet below shows the ehrId for our dummy patient.

![Display EHRId](/images/GetEhrIdResult.jpg)

To store the returned ehrId as a pre-set for the selected environment,
highlight the string in the response details, right mouse click, set the
environment (**C4H Ripple OSI in this example**) and then select
**ehrId** from the list of attributes.

![Store EHRId](/images/StoreEhrIDAsPreset.jpg)

# Retrieve Composition ID

Now that we have the patient’s EHR identifier, we can use it to locate
and retrieve some clinical details. We use an Archetype Query Language
(AQL) call to retrieve a list of the identifiers and dates of
existing Nursing Vital Signs Observations Composition records.
Compositions are document-level records which act as the container for
all openEHR patient data.

The name/value of the Composition is the root name of the templates
composition archetype (case-sensitive). In a real-world example we would
query on other factors to ensure we had the ‘correct’ list.

The query we need to run in order to get the composition Id for the most
recent vital signs composition for the selected patient is as follows:

![Retrieve compositionId explanation](/images/RetrieveCompositionIdExplanation.jpg)

At this stage you don’t need to worry about the exact syntax and how to
create an AQL query. These topics are covered elsewhere, and the
Specifications provide the required details.

Open the **query** folder and select **Ad-hoc query**

![Retrieve CompositionId](/images/RetrieveCompositionIdFolderSelect.jpg)

This is the query string in a format which can be copied and pasted:

``` sql
select
 a/uid/value as compositionId,
 a/context/start_time/value as start_time
from EHR e[ehr_id/value='{{ehrId}}']
 contains COMPOSITION a[openEHR-EHR-COMPOSITION.encounter.v1]
where a/name/value= 'Nursing Vital Signs Observations'
order by a/context/start_time/value desc
offset 0 limit 1
```

In the Ad-hoc Query window click on **Param** and paste the query
string above into the **Value** field, then click on the **Send** button.

![Get CompositionId](/images/RetrieveCompositionIdString.jpg)

Click the **Scroll to response** button in the bottom right hand
corner to display the response details. The **compositionId** element
in the response is the unqique identifier for the composition and the
**start\_time** is the time that the document was authored.

![Get CompositionID result](/images/RetrieveCompositionIdResult.jpg)

We will use the results of this query to retrieve the full composition,
so the final action is to store the composition Id as a pre-set.

Highlight the string in the response details, right mouse click, set the
environment (**C4H Ripple OSI** in this example) and then select
**compositionId** from the list of attributes

![Store compositionId](/images/StoreCompositionIdAsPreset.jpg)

# Retrieve Composition

The next step is to retrieve the composition itself, based on the
compositionId we stored in the previous step.

Navigate to the **composition** folder and highlight **Read
Composition JSON FLAT**, then click the **Send** button

![Retrieve composition](/images/RetrieveComposition.jpg)

The result is shown as a FLAT JSON file below

![Retrieve composition result](/images/RetrieveCompositionResult.jpg)

Other formats are JSON RAW, XML RAW or JSON STRUCTURED – the snippets
below show part of the Pulse data

![JSON RAW](/images/RetrieveCompositionResultOtherFormats1.jpg)

![XML RAW](/images/RetrieveCompositionResultOtherFormats2.jpg)

![JSON STRUCTURED](/images/RetrieveCompositionResultOtherFormats3.jpg)

# Persist Composition

The next step is to persist a new composition. The data in the
composition is validated against a template, and the first action is to
set the correct template Id for composition to be persisted.

Navigate to the **Template** folder and highlight **List available
templates**, then click the **Send** button. Highlight the **Vital
Signs Encounter template** in the list of available templates, right
mouse click, set the environment (***C4H Ripple OSI*** in this
example) and then select **templateId** from the list of attributes

![Set templateId](/images/ListTemplates.jpg)

Once the template Id is set, we can commit a composition. The following
string is an example of a vital signs composition:

    "ctx/language": "en",
    "ctx/territory": "GB",
    "ctx/composer_name": "Hazel Smith",
    "ctx/time": "2015-12-10T02:19:00.000Z",
    "ctx/health_care_facility|id": "999999-345",
    "ctx/health_care_facility|name": "Northumbria Community NHS",
    "ctx/id_namespace": "NHS-UK",
    "ctx/id_scheme": "2.16.840.1.113883.2.1.4.3",
    "nursing_vital_signs_observations/vital_signs:0/respirations:0/any_event:0/rate|magnitude": 22,
    "nursing_vital_signs_observations/vital_signs:0/respirations:0/any_event:0/rate|unit": "/min",
    "nursing_vital_signs_observations/vital_signs:0/pulse:0/any_event:0/heart_rate|magnitude": 101,
    "nursing_vital_signs_observations/vital_signs:0/pulse:0/any_event:0/heart_rate|unit": "/min",
    "nursing_vital_signs_observations/vital_signs:0/body_temperature:0/any_event:0/temperature|magnitude": 36.6,
    "nursing_vital_signs_observations/vital_signs:0/body_temperature:0/any_event:0/temperature|unit": "°C",
    "nursing_vital_signs_observations/vital_signs:0/blood_pressure:0/any_event:0/systolic|magnitude": 100,
    "nursing_vital_signs_observations/vital_signs:0/blood_pressure:0/any_event:0/systolic|unit": "mm[Hg]",
    "nursing_vital_signs_observations/vital_signs:0/blood_pressure:0/any_event:0/diastolic|magnitude": 60,
    "nursing_vital_signs_observations/vital_signs:0/blood_pressure:0/any_event:0/diastolic|unit": "mm[Hg]",
    "nursing_vital_signs_observations/vital_signs:0/indirect_oximetry:0/any_event:0/spo2|numerator": 94,
    "nursing_vital_signs_observations/vital_signs:0/indirect_oximetry:0/any_event:0/spo2|denominator": 100,
    "nursing_vital_signs_observations/vital_signs:0/national_early_warning_score_rcp_uk:0/total_score": 3_*

As mentioned before, the exact syntax and how to create a composition
will be covered elsewhere. At this stage you should just use the syntax
string provided above.

Navigate to the **Composition** folder and highlight **Commit
Composition JSON FLAT**. Paste the text above into the Body text box on
the right hand side and click on the **Send** button.

![Commit composition](/images/CommitComposition.jpg)

The result shows the composition Id for the newly committed composition.

![Commit composition result](/images/CommitCompositionResult.jpg)

# Run AQL Query

The next step is to run a query on recent vital signs compositions and
return a set of key data.

Navigate to the **query** folder and select **Ad-hoc Query**.

This is the query string we are going to use to retrieve the last 5
vital signs compositions and return the relevant readings. Once again,
just to clarify: the exact syntax and how to create an AQL query will be
covered elsewhere. At this stage you can just copy and paste the query
syntax string shown below:

```sql
select
 a/uid/value as compositionId,
 a/context/start_time/value as start_time,
 b_a/data[at0001]/events[at0002]/data[at0003]/items[at0004]/value/magnitude as Rate_magnitude,
 b_b/data[at0002]/events[at0003]/data[at0001]/items[at0004]/value/magnitude as Heart_Rate_magnitude,
 b_c/data[at0002]/events[at0003]/data[at0001]/items[at0004]/value/magnitude as Temperature_magnitude,
 b_f/data[at0001]/events[at0006]/data[at0003]/items[at0004]/value/magnitude as Systolic_magnitude,
 b_f/data[at0001]/events[at0006]/data[at0003]/items[at0005]/value/magnitude as Diastolic_magnitude,
 b_g/data[at0001]/events[at0002]/data[at0003]/items[at0006]/value/numerator as spO2_numerator,
 b_h/data[at0001]/events[at0002]/data[at0003]/items[at0028]/value/magnitude as Total_Score_magnitude
from EHR e[ehr_id/value='{{ehrId}}']
 contains COMPOSITION a[openEHR-EHR-COMPOSITION.encounter.v1]
 contains (OBSERVATION b_a[openEHR-EHR-OBSERVATION.respiration.v1]
  or OBSERVATION b_b[openEHR-EHR-OBSERVATION.pulse.v1]
  or OBSERVATION b_c[openEHR-EHR-OBSERVATION.body_temperature.v1]
  or OBSERVATION b_f[openEHR-EHR-OBSERVATION.blood_pressure.v1]
  or OBSERVATION b_g[openEHR-EHR-OBSERVATION.indirect_oximetry.v1]
  or OBSERVATION b_h[openEHR-EHR-OBSERVATION.news_rcp_uk.v1])
where a/name/value= 'Nursing Vital Signs Observations'
order by a/context/start_time/value desc
```

In the Ad-hoc query window click on **Params** and enter the query
string into the **Value** field on the right hand side, then click the
**Send** button.

![Run AQL Query](/images/RunAQLQuery.jpg)

The result set contains the last 5 vital signs compositions and the data
points within the compositions.

![AQL Query Result](/images/RunAQLQueryResult.jpg)

# Close Session(Ripple EtherCis only)

The final step is to close the openEHR session.

To do this, navigate to the **session** folder and select **Delete
Session**. Click on the **Send** button.

The result will show a null sessionId, indicating that there is no open
session.

![Close Session](/images/CloseSession.jpg)
