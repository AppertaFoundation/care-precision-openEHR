---
title: "openEHR Datatypes" 
summary: This section provides a basic overview of key openEHR reference model datatypes 
---

![](../images/construction.jpg)

# Key openEHR datatypes

The openEHR Reference model defines a relatively small set of information model constructs which openEHR back-ends must support. This includes a number of generic classes and datatypes.

The Reference model contains virtually no clinical content e.g concepts for Medication, or Diagnosis. These are defined and managed separately as `archetypes`.

openEHR has a very rich set of allowable datatypes. A full definition is beyond the scope of this document but developers new to this field may find the following notes helpful. You can refer to the  [openEHR Specification](https://specifications.openehr.org/releases/RM/latest/data_types.html)  and [UML]() for full details.

The formal Class names for all datatypes in openEHR start with `DV_`

## Datatype: **text** (`DV_TEXT`)

Allows the recording of simple, unformatted text. Newlines and carriage returns are allowed.
openEHR does not normally constrain the length of string.

The example shows how a multiple occurrence Element is handled.

=== "RM Specs"
    
    The [rm.data_types.text package](https://specifications.openehr.org/releases/RM/latest/data_types.html#_text_package) contains classes for representing all textual values in the health record, including plain text, coded terms, and narrative text.
    ![UML - openEHR RM-datatypes.text package](https://specifications.openehr.org/releases/UML/latest/diagrams/diagram_Diagrams___18_1_83e026d_1433773264006_931575_5971.svg)

=== "CANONICAL JSON"
    ```json
       {
        {
                            "items": [
                                {
                                    "_type": "ELEMENT",
                                    "name": {
                                        "_type": "DV_TEXT",
                                        "value": "What matters to me"
                                    },
                                    "archetype_node_id": "at0004",
                                    "value": {
                                        "_type": "DV_TEXT",
                                        "value": "Parents"
                                    }
                                },
                                {
                                    "_type": "ELEMENT",
                                    "name": {
                                        "_type": "DV_TEXT",
                                        "value": "What matters to me #2"
                                    },
                                    "archetype_node_id": "at0004",
                                    "value": {
                                        "_type": "DV_TEXT",
                                        "value": "Mood"
                                    }
                                },
                                {
                                    "_type": "ELEMENT",
                                    "name": {
                                        "_type": "DV_TEXT",
                                        "value": "What matters to me #3"
                                    },
                                    "archetype_node_id": "at0004",
                                    "value": {
                                        "_type": "DV_TEXT",
                                        "value": "Isolation"
                                    }
                                }
                            ]
                        }
         
        
    ```
=== "STRUCTURED JSON"
    ```json
         "what_matters_to_me": [
              "Parents",
              "Mood",
              "Isolation"
             ]
            }
    ```
=== "FLAT JSON"
    ```json

        ```json
          {
           "what_matters_to_me:0": "Parents",
           "what_matters_to_me:1": "Mood",
           "what_matters_to_me:2": "Isolation"
          }
    ```
  
!!! hint
    `DV_TEXT` can always be sub-classed to `DV_CODED_TEXT`, so when you see a **text** constraint in an archetype , this can normally always be converted to a **codedText** in a template or at run-time.  As an example, the primary element in the [Adverse reaction risk]() archetype is a `DV_TEXT` but in most circumstances a DV_CODED_TEXT will actually be used.

## Datatype: **codedText** (`DV_CODED_TEXT`)

Is a commonly used datatype in openEHR systems and is a sub-class of **text**. i.e wherever **text** is specified **codedText** can be used instead.

Codes may be 'external' e.g. SNOMED CT, LOINC, ICD-10 or 'local', where they are defined within archetypes, have the form `atxxxxx` and are commonly referred to as **'atCodes'**.

A **codedText** element always includes the terminologyID, the code itself and the text of the coded concept (Rubric). In the patient data this is a carried in the `defining_code` attribute of the datatype.

=== "RM Specs"
   The [rm.data_types.text package](https://specifications.openehr.org/releases/RM/latest/data_types.html#_text_package) contains classes for representing all textual values in the health record, including plain text, coded terms, and narrative text.
    ![UML - openEHR RM-datatypes.text package](https://specifications.openehr.org/releases/UML/latest/diagrams/diagram_Diagrams___18_1_83e026d_1433773264006_931575_5971.svg)

=== "CANONICAL JSON"
    ```json
       {
            "_type": "ELEMENT",
            "name": {
                "_type": "DV_TEXT",
                "value": "Status"
            },
            "archetype_node_id": "at0004",
            "value": {
                "_type": "DV_CODED_TEXT",
                "value": "Unknown",
                "defining_code": {
                    "_type": "CODE_PHRASE",
                    "terminology_id": {
                        "_type": "TERMINOLOGY_ID",
                        "value": "local"
                    },
                    "code_string": "at0007"
                }
            }
        }
    ```
=== "STRUCTURED JSON"
    ```json
        "legal_welfare_proxy_in_place": [
                                        {
                                            "status": [
                                                {
                                                    "|code": "at0007",
                                                    "|value": "Unknown",
                                                    "|terminology": "local"
                                                }
                                            ],
                                        }
        ]
    ```
=== "FLAT JSON"
    ```json
      "legal_welfare_proxy_in_place/status|value": "Unknown",
      "legal_welfare_proxy_in_place/status|code": "at0007",
      "legal_welfare_proxy_in_place/status|terminology": "local"
    ```


#### Using local 'atCodes' 

e.g `local::at0007| normal|`

When a **codedText** item is added to a FLAT or STRUCTURED JSON format document, you must give the code, value and terminology, unless this is a local 'atCode', in which case only the code needs to be provided, as the terminologyId and text value will be supplied as defaults, based on the known values in the template. 

Only the code needs to be specified - the value and terminology are not required since they are pre-defined in the openEHR template..

=== "FLAT JSON"
    ```json
    asthma_diary_entry/examination_findings:0/pulmonary_function_testing:0/result_details/pulmonary_flow_rate_result/test_result_name|code': 'at0071'
    ```



#### Using external terminology 

e.g. `SNOMED-CT::23924001| chest tightness |`

If an external terminology is used, the code, terminology and value must be specified

=== "FLAT JSON"
    ```json
       'asthma_diary_entry/history:0/story_history/symptom:0/symptom_name|code': '23924001',
       'asthma_diary_entry/history:0/story_history/symptom:0/symptom_name|value': 'chest tightness',
       'asthma_diary_entry/history:0/story_history/symptom:0/symptom_name|terminology': 'SNOMED-CT',
   ```

#### Handling multiple codes - Mappings

Both DV_TEXT and DV_CODED_TEXT allow for other codes to be recorded in the patient record alongside the text value or defining code. THis is done via the `mappings` attribute in the DV_TEXT/DV_CODED_TEXT datatype.

=== "RM Specs"
[openEHR DV_TEXT mappings](https://specifications.openehr.org/releases/RM/latest/data_types.html#_mappings)
![](https://specifications.openehr.org/releases/RM/latest/data_types/diagrams/coded_text_mappings.png)
=== "CANONICAL JSON"
    ```json
    ```
=== "STRUCTURED JSON"
    ```json
    ```
=== "FLAT JSON"
    ```json
    ```





## Datatype: **ordinal** `DV_ORDINAL`and **scale** `DV_SCALE`

Combines **codedText** with a score, expressed as an integer (DV_ORDINAL) or a real number (DV_SCALE). 

DV_SCALE is just being introduced in the latest version of the Reference Model to support the small number of scales and scores that need real numbers. We expect DV_SCALE to be used in preference to DV_ORDINAL for new archetypes. 


    0: Green  `local::at0022::Green`
    1: Amber  `local::at0023::Amber`
    2: Red    `local::at0024::Red`

    'community_dental_final_assessment_letter/assessment_scales/dental_rag_score:0/caries_tooth_decay/caries_risk|code': 'at0024',
    'community_dental_final_assessment_letter/assessment_scales/dental_rag_score:0/caries_tooth_decay/caries_risk|ordinal': 2,
    'community_dental_final_assessment_letter/assessment_scales/dental_rag_score:0/caries_tooth_decay/caries_risk|value': 'Red',

## Datatype: *count*

***count*** is a simple integer.

    'community_dental_final_assessment_letter/investigations_and_results:0/imaging_examination_result:0/result_group/decayed_teeth/decayed_teeth': 4,

## Datatype: *datetime*

Records a date or date and time using the [ISO8061
format](http://www.w3.org/TR/NOTE-datetime).

    'ctx/time': '2014-09-23T00:11:02.518+02:00'

## Datatype: *quantity*

Records a physical quantity along with the appropriate SI units, which
should normally be compliant with [UCUM](http://unitsofmeasure.org).

    "asthma_diary_entry/examination_findings:0/pulmonary_function_testing:0/result_details/pulmonary_flow_rate_result/actual_result|magnitude": 550,
    "asthma_diary_entry/examination_findings:0/pulmonary_function_testing:0/result_details/pulmonary_flow_rate_result/actual_result|unit": "l/min",


# Key openEHR Reference model attributes

A number of key data points need to be populated in an openEHR
composition, which may not be apparent from the archetypes or templates.
Developers can largely use the example instance documents and APIs for
guidance but these notes may give useful background in addition to
viewing the [UML view of the openEHR reference
model.](http://www.openehr.org/local/releases/1.0.1/uml/index.html)

## *committer*

This is the name of the person physically committing the document ie.
the person logged on to the account. If omitted from API calls, Ehrscape
will use the domain login name.

## *composition/composer*

This is the clinical author of the document i.e the person with clinical
responsibility. Ehrscape FLAT and STRCTURTED formats handle this as
`composer_name`.

## *composition/context/start\_time*

This is the time that the clinical interaction with the patient began.
Ehrscape FLAT and STRUCTURED formats handle this as ctx/time.

## *composition/context/health\_care\_facility*

This is the healthcare facility / oragnisation under who’s remit the
encounter took place.

## *observation/time*

This is the time that a patient’s signs and symptoms were observed or a
test was run. It is set automatically by the value of the ctx/time
attribute. If you need to set the time of a specific observation you can
use

The Ehrscape FLAT and STRUCTURED formats hide much of the complexity of
these attributes, providing sensible defaults. In particular the `ctx`
header common to both JSON STRUCTURED and FLAT formats, considerably
simplifies the composition header …

    'ctx/composer_name': 'Rebecca Wassall',
    'ctx/health_care_facility|id': '999999-345',
    'ctx/health_care_facility|name': 'Northumbria Community NHS',
    'ctx/id_namespace': 'NHS-UK',
    'ctx/id_scheme': '2.16.840.1.113883.2.1.4.3',
    'ctx/language': 'en',
    'ctx/territory': 'GB',
    'ctx/time': '2014-09-23T00:11:02.518+02:00',

# Handling specific openEHR datatypes

## *text*

Text handling is normally straightforward.

FLAT + STRUCTURED

    "synopsis": [
     "Significant dental issues."
     ]

## *codedText*

For an external terminology, the terminologyId, code and text value must
be supplied but in JSON FLAT and STRUCTURED formats only the local
'atcode' needs to be supplied.

STRUCTURED JSON format

``` 
 Internal (local) code:
 "dental_swelling": [
 {
 "|code": "at0006",
 }
 ]

 External terminology:
 "symptom_name": [
 {
 "|code": "102616008",
 "|terminology": "SNOMED-CT",
 "|value": "Painful mouth"
 }
 ]
```

FLAT JSON format

```json 
 Internal (local) code:
 "community_dental_final_assessment_letter/examination_findings:0/physical_examination_findings:0/oral_examination/dental_swelling|code": "at0006"

 External terminology:
 "community_dental_final_assessment_letter/history:0/story_history:0/symptom:0/symptom_name|value": "Painful mouth",
 "community_dental_final_assessment_letter/history:0/story_history:0/symptom:0/symptom_name|code": "102616008",
 "community_dental_final_assessment_letter/history:0/story_history:0/symptom:0/symptom_name|terminology": "SNOMED-CT"
```

## *ordinal*

For JSON FLAT and STRUCTURED formats only the local 'atcode' needs to be supplied although the ordinal and text value are also
accepted FLAT JSON format

    "community_dental_final_assessment_letter/assessment_scales/dental_rag_score:0/caries_tooth_decay/caries_risk|code": "at0024"

STRUCTURED format

```json 
 "caries_risk": [
    {
    "|code": "at0024",
    }
    ]
```

or

```json 
 "caries_risk": [
 {
    "|code": "at0024",
    "|ordinal": 2,
    "|value": "Red"
 }
 ]
```

## *date*

Dates need to be persisted in the [ISO8061format](http://www.w3.org/TR/NOTE-datetime) and should be displayed in CUI format e.g. 12-Nov-1958

# Tricky issues

## Converting UI checkboxes to/from codedText

In a number of places, the UI may best be represented as a set of checkboxes, while the underlying data is modelled as codedText.

e.g. Symptoms

While it may seem more easier and more logical to use a boolean datatype, this is a common pattern in openEHR datasets which are
designed to be interoperable and extensible. Experience has shown that expansion of the target valueset and alignment to external terminologies is easier if an enumerated list of codedText is used rather than boolean.

In the case of 'Symptom' the rule is …

  - If the checkbox is ticked, populate the Symptom name with the
    SNOMED-CT term

  - If the checkbox is unticked, omit the Symptom name element
    completely.

Conversely when loading a persisted dataset, the checkbox should only be checked if the Symptom name element is present and contains SNOMED-CT term 102616008.

## Multiple occurrence data

Some aspects of the form e.g Symptoms are handled as multiple
occurrences of the same data point in the underlying dataset.
