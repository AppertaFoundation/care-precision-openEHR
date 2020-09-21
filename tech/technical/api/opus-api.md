---
tags: documentation
title: "API Calls for C19 application (DITO)"
subtitle: "API Calls for C19"
author: Paul Webster <paul.webster@opusvl.com>
date: "08/09/2020"
fao: "Development group"
clientname: C19 Application
classification: "Company Shared, Aperrta, OpusVL"
overview: [ Documentation ]
docver: v0.1
watermark: "DRAFT - Multi"
documentclass: report
toc: true 
toc-depth: 2
secnumdepth: 2
breaks: false
lang: en-gb
---


[TOC]


# Overview

This work-in-progress document details the API.

# Paths

## Root paths

### /

* State: READY
* Handler: Base daemon
* Reasoning: Test response for application accessibility
* Method: GET
* Reachability: Public
* Auth: None
* Response: 200, text/html
* Data: "Open eReact API - Unauthorized access is strictly forbidden."
* Implementation: 100%
* Example call for ehrbase as curl: `not required`

Request

```
curl -X GET "https://api.c19.devmode.xyz/" -H "accept: */*" -H "Content-Type: application/json" -c cookies -b cookies
```
Response

```
Open eReact API - Unauthorized access strictly forbidden.
```

### /c19-alpha/0.0.1/ (API ROOT)

* State: READY
* Handler: 'handler_c19_alpha_0_0_1_'
* Reasoning: API base with known end points
* Method: GET
* Reachability: public
* Auth: Token optional
* Response: 200, application/javascript
* Data: ```[List,of,handlers,on,api,relative]```
* Implementation: 100%
* Example call for ehrbase as curl: `not required`

Request

```curl -X GET "https://api.c19.devmode.xyz/c19-alpha/0.0.1/" -H "accept: */*" -H "Content-Type: application/json" -c cookies -b cookies```

Response

```["/c19-alpha/0.0.1/","/c19-alpha/0.0.1/_/auth"]```

## API relative paths

All paths are relative to the API root

### /

This is relatively void / based on the API root, so is the same handler. (See API Root section above)

### /_/auth

* State: REPRESENTATIVE
* Handler: 'handler__auth'
* Reasoning: API Authentification
* Method: POST
* Reachability: Public
* Auth: Token optional
* Response: 200, application/javascript
* Response: 400, text/plain
* Implementation: 75%
* Data: ```{token=>UUID}```
* Body arguments: {token=>'authme'}
* Example call for ehrbase as curl: `not required`
* NOTES: 
    * Cannot be 100% implemented at this time, but is functionally representative
    * Sends 400 on BAD AUTH, not sure this is the HTTP right CODE!
    * Processing should be done to determined ALLOWED types from the client and the response should be sent in the correct format, but would be for the larger project as to costly for benefit at present


Request:
```
curl -vv -X POST "https://api.c19.devmode.xyz/c19-alpha/0.0.1/_/auth" -H "accept: */*" -H "Content-Type: application/json" -d "{\"token\":\"authme\"}" -c cookies -b cookies
```

Response(success):
```
HTTP/200 javascript/application
{"session":"3BBFF4CA-F1DF-11EA-8904-C27F5E058BE1","authentification":"success","id":"testuser"}
```

Response(bad):
```
HTTP/400 text/plain
Bad request%
```

### /meta/demographics/patient_list

* AWAITING-RESOLUTION: 
    * Does this list require authorisation?
    * UUID's are NOT static as data source is not established
* Reachability: ?
* Auth: ?
* Method: GET
* Response: 200, application/javascript
* Implementation: 50%
* Example call for ehrbase as curl: `not required`

Request
```
 curl -X GET "https://api.c19.devmode.xyz/c19-alpha/0.0.1/meta/demographics/patient_list" -H "accept: */*" -H "Content-Type: application/json" -c cookies -b cookies
 ```

Response(success):

```json
[
   {
      "name":[
         {
            "family":"Dora",
            "given":[
               "Praveen"
            ],
            "prefix":[
               "Miss"
            ]
         }
      ],
      "id":"4D043CCC-F1EA-11EA-81DB-169F5E058BE1"
   },
   {
      "name":[
         {
            "given":[
               "Horatio"
            ],
            "prefix":[
               "Mr"
            ],
            "family":"Samson"
         }
      ],
      "id":"4D043D94-F1EA-11EA-81DB-169F5E058BE1"
   },
   {
      "name":[
         {
            "given":[
               "Elsie"
            ],
            "prefix":[
               "Mrs"
            ],
            "family":"Mills-Samson"
         }
      ],
      "id":"4D043E0C-F1EA-11EA-81DB-169F5E058BE1"
   },
   {
      "name":[
         {
            "given":[
               "Fredrica"
            ],
            "prefix":[
               "Mrs"
            ],
            "family":"Smith"
         }
      ],
      "id":"4D043E5C-F1EA-11EA-81DB-169F5E058BE1"
   },
   {
      "id":"4D043EA2-F1EA-11EA-81DB-169F5E058BE1",
      "name":[
         {
            "family":"Munoz",
            "prefix":[
               "Mrs"
            ],
            "given":[
               "Vicky"
            ]
         }
      ]
   },
   {
      "id":"4D043EE8-F1EA-11EA-81DB-169F5E058BE1",
      "name":[
         {
            "prefix":[
               "Miss"
            ],
            "given":[
               "Kendra"
            ],
            "family":"Fitzgerald"
         }
      ]
   },
   {
      "id":"4D043F2E-F1EA-11EA-81DB-169F5E058BE1",
      "name":[
         {
            "family":"Taylor",
            "given":[
               "Christine"
            ],
            "prefix":[
               "Mrs"
            ]
         }
      ]
   },
   {
      "id":"4D043F74-F1EA-11EA-81DB-169F5E058BE1",
      "name":[
         {
            "given":[
               "Delisay"
            ],
            "prefix":[
               "Miss"
            ],
            "family":"Santos"
         }
      ]
   },
   {
      "name":[
         {
            "prefix":[
               "Miss"
            ],
            "given":[
               "Darlene"
            ],
            "family":"Cunningham"
         }
      ],
      "id":"4D043FB0-F1EA-11EA-81DB-169F5E058BE1"
   },
   {
      "id":"4D043FF6-F1EA-11EA-81DB-169F5E058BE1",
      "name":[
         {
            "family":"Tengku",
            "prefix":[
               "Miss"
            ],
            "given":[
               "Zara"
            ]
         }
      ]
   }
]

```

        
### /meta/demographics/patient?patientId=<PATIENT_ID>
* AWAITING-RESOLUTION: 
    * Auth required for this function
* Method: GET
* Example call for ehrbase as curl: `not required`
* Correct implementation?

Request(UUID MUST BE VALID, Retrieved from patient_list call)
```
curl -X GET "https://api.c19.devmode.xyz/c19-alpha/0.0.1/meta/demographics/patient?patientId=0794228C-F1F5-11EA-8D1E-76B95E058BE1" -H "accept: */*" -H "Content-Type: application/json" -c cookies -b cookies
```

Response
```json
{
   "gender":"female",
   "date_of_birth":"1923-08-14",
   "location":[
      {
         "district":"West Yorkshire",
         "postalCode":"LS15 8BD",
         "type":"both",
         "line":[
            "24 Church Lane"
         ],
         "use":"home",
         "city":"Leeds"
      }
   ],
   "id":"0794228C-F1F5-11EA-8D1E-76B95E058BE1",
   "nhsnumber":"LOCAL1003"
}
```

## Calls awaiting introduction (Missing info or general plan)

Calls here are generally under planned and require validation from some level.

### /calculation/endpoint?
* AWAITING-RESOLUTION: 
    * Is this the correct API path
    * IAN: Possibly a parameter to identify the algorithm e.g &calc=news2
    * 
    * Does this call have to talk to EHRBase? if it does can we have an example of that call please.
    IAN : No this is purely middleware - no dependency on the CDR.

* Method POST
* Example call for ehrbase as curl: ????
* Data: it's OK just sending the same stucture like in submited version? or maybe even can I more cut this and send to you only assesment data?:

IAN: I would suggest passing the whole NEWS2 structure in the body - the input object and the output object - then return the whole thing. THis is how the GDL calls work. For info this is the GDL - https://github.com/gdl-lang/common-clinical-models/blob/master/gdl2/NEWS2.v1.gdl2.json

Basically that describes the bindings to the archetype nodes and the calculations - there is some very complex stuff in their version around 'hypercapnia' that we can ignore.


```json
{
    "temperature": {
        "|magnitude": 90.7,
        "|unit": "°C"
    },
    "SpO2": 91.0,
    "pulse": 110,
    "respirations": 34.4,
    "acvpu": {
        "|code": "at0015",
    },
    "systolic": 98,
    "diastolic": 58,
    "news2_score": {
        "respiration_rate": {
            "|code": "at0020",
        },
        "spo_scale_1": {
            "|code": "at0031",
        },
        "spo_scale_2": {
            "|code": "at0050",
        },
        "air_or_oxygen": {
            "|code": "at0036",
        },
        "systolic_blood_pressure": {
            "|code": "at0017",
        },
        "pulse": {
            "|code": "at0013",
        },
        "consciousness": {
            "|code": "at0024",
        },
        "temperature": {
            "|code": "at0023",
        },
        "total_score": 14,
        "clinical_risk_category": {
            "|code": "at0059",
        }
    }
}
```


IAN: I don't think we need this - just use the single POST above
### /calculation/endpoint=<id of calculatin result>
* Method GET
* Data:
    Even just like this will perfect for me (I recognize that 'ordinal' value is associated with score of singe parametr which is substitude of news2 total score). But you can optimaize to the way which will be the best to return it to me. 
The most important for me is a clinical risk and total score if its a news2 and ordinal/score for single parrametr, value will be also good but its not necessary.


    
```json
{
  "respiration_rate": {
    "|code": "at0020",
    "|value": "21-24",
    "|ordinal": 2
  },
  "spo_scale_1": {
    "|code": "at0031",
    "|value": "94-95",
    "|ordinal": 1
  },
  "spo_scale_2": {
    "|code": "at0050",
    "|value": "84-85",
    "|ordinal": 2
  },
  "air_or_oxygen": {
    "|code": "at0036",
    "|value": "Air",
    "|ordinal": 0
  },
  "systolic_blood_pressure": {
    "|code": "at0017",
    "|value": "≤90",
    "|ordinal": 3
  },
  "pulse": {
    "|code": "at0013",
    "|value": "51-90",
    "|ordinal": 0
  },
  "consciousness": {
    "|code": "at0024",
    "|value": "Alert",
    "|ordinal": 0
  },
  "temperature": {
    "|code": "at0023",
    "|value": "35.1-36.0",
    "|ordinal": 1
  },
  "total_score": 14,
  "clinical_risk_category": {
    "|code": "at0059",
    "|value": "Medium",
    "|terminology": "local"
  }
}

```
    
### /cdr/something?
* Method POST
* Data denepnds on kind of assesment
* 
* IAN - no that's not correct - their is only one set of data that includes the main assessment and any other sub- assessments
  #### Clinical assessment
    ```json
    {
  "template_id": "open_eREACT-Care",
  "start_time": "2020-09-07T21:04:10.789Z",
  "setting": "other care",
  "healthcare_facility": "Glen Carse Care Home",
  "composer": {
    "name": "Dr Joyce Brown",
    "id": {
      "type": "GMC",
      "id": "12342341",
      "namespace": "uk.gmc"
    }
  },
  "situation": {
    "soft_signs": ["Just not themselves", "Loss of appetite"],
    "notes": "Has refused all meals today"
  },
  "background": {
    "height": 170.3,
    "weight": 77.34,
    "frailty": "at0010",
    "past_history": "Angina, Diabetes Type 2 and COPD",
    "medication": "Aspirin, Ventolin inhaler and Glipazide",
    "allergies": "No known allergies"
  },
  "assessment": {
       "assessment": {
        "denwis": {

             "q1_breathing": {
                "|code": "at0031"
            },
             "breathing_indicator": [
                {
                    "|code": "at0067",
                },
                  {
                    "|code": "at0068",
                },
                  {
                    "|value": "Blue lips",
                }
            ],
            "q2_circulation": {
                "|code": "at0037",
                "|value": "No change in circulation",
                "|ordinal": 0
            },
            "circulation_indicator": [
                {
                    "|code": "at0098",
                }
            ],
            "q3_temperature": {
                "|code": "at0042",

            },
            "temperature_indicator": [
                {
                    "|code": "at0100"

                }
            ],
            "q4_mentation": {
                "|code": "at0045"
            },
            "mentation_indicator": [
                {
                    "|code": "at0101"
                }
            ],
            "q5_agitation": {
                "|code": "at0048",

            },
            "agitation_indicator": [
                {
                    "|code": "at0104"
                }
            ],
            "q6_pain": {
                "|code": "at0052"

            },
            "pain_indicator": [
                {
                    "|code": "at0107"
                }
            ],
            "q7_trajectory": {
                "|code": "at0055"
            },
            "trajectory_indicator": [
                {
                    "|code": "at0108"

                }
            ],
            "q8_patient_subjective": {
                "|code": "at0057"

            },
            "patient_indicator": [
                {
                    "|code": "at0110"

                }
            ],
            "q9_nurse_subjective": {
                "|code": "at0061"

            },
            "nurse_subjective_indicator": [
                {
                    "|code": "at0112"

                }
            ],
            "q_10_other_comment": "Just off her food",
            "total_score": 3
        },
  },
         "sepsis_screening": {
            "risk_factors_for_sepsis": [
                {
                    "|code": "at0009",
                    "|value": "Recent trauma / surgery / invasive procedure",
                    "|terminology": "local"
                }
            ],
            "likely_source_of_infection": [
                {
                    "|code": "at0027",
                    "|value": "Indwelling device",
                    "|terminology": "local"
                }
            ],
            "red_flag_acute": [
                {
                    "|code": "at0080",
                    "|value": "Lactate ≥ 2 mmol/l",
                    "|terminology": "local"
                }
            ],
            "amber_flag_acute": [
                {
                    "|code": "at0093",
                    "|value": "Respiratory rate 21-24",
                    "|terminology": "local"
                }
            ]
        },
    "news2": {
      "temperature":  90.7,
      "SpO2": 91.0,
      "pulse": 110,
      "respirations": 34.4,
      "acvpu": {
        "|code": "at0015"
      },
      "systolic": 98,
      "diastolic": 58,
      "news2_score": {
                "respiration_rate": {
                    "|code": "at0020"
   
                },
                "spo_scale_1": {
                    "|code": "at0031"
               
                },
                "spo_scale_2": {
                    "|code": "at0050"
 
                },
                "air_or_oxygen": {
                    "|code": "at0036"
   
                },
                "systolic_blood_pressure": {
                    "|code": "at0017"
  
                },
                "pulse": {
                    "|code": "at0013"

                },
                "consciousness": {
                    "|code": "at0024"

                },
                "temperature": {
                    "|code": "at0023"

                },
                "total_score": 14,
                "clinical_risk_category": {
                    "|code": "at0059",
                }
            }
        }
    }

  },
  "response": {
    "recommendation": "No action required",
    "service_request": [
      {
        "service_name": {
          "|code": "170499009",
          "|value": "Isolation of infection contact",
          "|terminology": "SNOMED-CT"
        },
        "reason_for_request": {
          "|code": "840546002",
          "|value": "Exposure to 2019 novel coronavirus",
          "|terminology": "SNOMED-CT"
        },
        "reason_for_isolation": "Contact",
        "date_isolation_due_to_start": "2020-08-25T13:19:30.700Z",
        "date_isolation_due_to_end": ["2020-09-14T13:19:30.700Z"]
      }
    ],
    "narrative": "Isolation of infection contact"
  }
}

```
#### => SEPSIS- NO INFECTION
```json
{
    "template_id": "open_eREACT-Care",
    "start_time": "2020-09-07T21:04:10.789Z",
    "setting": "other care",
    "healthcare_facility": "Glen Carse Care Home",
    "composer": {
      "name": "Dr Joyce Brown",
      "id": {
        "type": "GMC",
        "id": "12342341",
        "namespace": "uk.gmc"
      }
    },
    "situation": {
      "soft_signs": ["Just not themselves", "Loss of appetite"],
      "notes": "Has refused all meals today"
    },
    "background": {
      "height": 170.3,
      "weight": 77.34,
      "frailty": "at0010",
      "past_history": "Angina, Diabetes Type 2 and COPD",
      "medication": "Aspirin, Ventolin inhaler and Glipazide",
      "allergies": "No known allergies"
    },
    "assessment": {
      "sepsis_screening": {
        "risk_factors_for_sepsis": ["at0009"],
      }
    },
    "response": {
      "recommendation": "No action required",
      "service_request": [
        {
          "service_name": {
            "|code": "170499009",
            "|value": "Isolation of infection contact",
            "|terminology": "SNOMED-CT"
          },
          "reason_for_request": {
            "|code": "840546002",
            "|value": "Exposure to 2019 novel coronavirus",
            "|terminology": "SNOMED-CT"
          },
          "reason_for_isolation": "Contact",
          "date_isolation_due_to_start": "2020-08-25T13:19:30.700Z",
          "date_isolation_due_to_end": ["2020-09-14T13:19:30.700Z"]
        }
      ],
      "narrative": "Isolation of infection contact"
    }
  }
  
```
#### => SEPSIS- RED FLAG
```json
 ...
"assessment": {
    "sepsis_screening": {
      "risk_factors_for_sepsis": ["at0009"],
      "likely_source_of_infection": ["at0027"],
      "red_flag_acute": ["at0080"],
    }
  },
  ...
```

#### => SEPSIS- AMBER FLAG
```json
...
"assessment": {
    "sepsis_screening": {
      "risk_factors_for_sepsis": ["at0009"],
      "likely_source_of_infection": ["at0027"],
      "amber_flag_acute": ["at0093"]
    }
  },
 ...
```

## open-eReact txt/coded text and ordinal constraints

__Moved to: https://codimd.opusvl.com/6MDRebxPReyuNFlpNAG5Mw due to size__