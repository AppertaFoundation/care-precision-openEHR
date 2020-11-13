

### Header

```json
    "template_id": "EREACT - Covid Lab Testing.v0",
    "start_time": "2020-09-07T21:04:10.789Z", //ISO DateTime
    "setting": "other care", //Fixed
    "healthcare_facility": {  //Identifier of the facility - could be handled server-side
        "name": "Glen Carse Care Home",
        "id": {
            "type": "CQC", // CQC number
            "id": "12342341", 
            "namespace": "uk.org.cqc" 
        }
    },
    "composer": {  //Clinical author of the document
        "name": "RN Joyce Brown",
        "id": {
            "type": "NMC", // From practitioner Demographics
            "id": "12342341", //From practitioner demographics
            "namespace": "uk.org.nmc" //from practitioner demographics
        }
    },

```
### Situation

```
{

    "covid_test_request": {
        "service_name": 
            {
                "|code": "1240471000000102",
                "|value": "Measurement of severe acute respiratory syndrome coronavirus 2 antigen",
                "|terminology": "SNOMED-CT"
            },
    
        "reason_for_request": "Routine Test"
    },

    "covid_test_tracking": {
        "current_state": {
            "|code": "532",
            "|value": "completed",
            "|terminology": "openehr"
        },
        "careflow_step": {
            "|code": "at0026",
            "|value": "Service request sent",
            "|terminology": "local"
        },
        "service_name": {
            "|code": "1240471000000102",
            "|value": "Measurement of severe acute respiratory syndrome coronavirus 2 antigen",
            "|terminology": "SNOMED-CT"
        },
        "time": "2020-10-28T13:39:53.007Z"
    },

    "covid_test_result": {
        "test_name": 
            {
                "|code": "1240471000000102",
                "|value": "Measurement of severe acute respiratory syndrome coronavirus 2 antigen",
                "|terminology": "SNOMED-CT"
            },
        "test_result": 
            {
                "|code": "1300721000000109",
                "|value": "COVID-19 confirmed by laboratory test",
                "|terminology": "SNOMED-CT"
            },
        "time":  "2020-10-28T13:39:53.007Z"
    }
    
}
```
```json
    "situation": {
        "soft_signs": [ //Multiple signs
            "Just not themselves",
            "Loss of appetite"
        ],
        "notes": "Has refused all meals today"
    },
```

##### Constraints

```json
"soft_signs": {
        [ 
            "Just not themselves",
            "Dehydration",
            "Dizziness",
            "Had a fall"
            "Increased anxiety/agitation",
            "Loss of appetite",
            "Reduced mobility/coordination",
            "Skin changes (colour/puffiness)",
            "Withdrawn",
            "Recently lost consciousness",
            "Recently lost consciousness"
        ],
        listOpen" : true
    }
```

### Background

```json
    "background": {
        "height": 170.3,
        "weight": 77.34,
        "frailty": {
            "|code": "at0010",
            "|value": "Moderately Frail",
            "|ordinal": 6
        },
        "past_history": "Angina, Diabetes Type 2 and COPD",
        "medication": "Aspirin, Ventolin inhaler and Glipazide",
        "allergies": "No known allergies"
    },
```

### Assessment

```json
        "denwis": {
            "q1_breathing": {
                "|code": "at0031",
                "|value": "Change in breathing",
                "|ordinal": 1
            },
            "breathing_indicator": [
                {
                    "|code": "at0070",
                    "|value": "Use accessory muscles",
                    "|terminology": "local"
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
                    "|value": "Coldness",
                    "|terminology": "local"
                }
            ],
            "q3_temperature": {
                "|code": "at0042",
                "|value": "No change in temperature",
                "|ordinal": 0
            },
            "temperature_indicator": [
                {
                    "|code": "at0100",
                    "|value": "Rigors",
                    "|terminology": "local"
                }
            ],
            "q4_mentation": {
                "|code": "at0045",
                "|value": "Change in mentation",
                "|ordinal": 1
            },
            "mentation_indicator": [
                {
                    "|code": "at0101",
                    "|value": "Lethargic",
                    "|terminology": "local"
                }
            ],
            "q5_agitation": {
                "|code": "at0048",
                "|value": "No agitation",
                "|ordinal": 0
            },
            "agitation_indicator": [
                {
                    "|code": "at0104",
                    "|value": "Anxious",
                    "|terminology": "local"
                }
            ],
            "q6_pain": {
                "|code": "at0052",
                "|value": "Change in pain",
                "|ordinal": 1
            },
            "pain_indicator": [
                {
                    "|code": "at0107",
                    "|value": "Increasing or consisting pain",
                    "|terminology": "local"
                }
            ],
            "q7_trajectory": {
                "|code": "at0055",
                "|value": "Change in trajectory",
                "|ordinal": 1
            },
            "trajectory_indicator": [
                {
                    "|code": "at0108",
                    "|value": "No progress",
                    "|terminology": "local"
                }
            ],
            "q8_patient_subjective": {
                "|code": "at0057",
                "|value": "No subjective patient indicator",
                "|ordinal": 0
            },
            "patient_indicator": [
                {
                    "|code": "at0110",
                    "|value": "Not feeling well",
                    "|terminology": "local"
                }
            ],
            "q9_nurse_subjective": {
                "|code": "at0061",
                "|value": "Nurse subjective indicator",
                "|ordinal": 1
            },
            "nurse_subjective_indicator": [
                {
                    "|code": "at0112",
                    "|value": "Change in behaviour",
                    "|terminology": "local"
                }
            ],
            "q_10_other_comment": "Just off her food",
            "total_score": 3
        },
```
##### Sepsis screening
```json
"sepsis_screening": {
  
            "risk_factors_for_sepsis": [
                {
                    "|code": "at0009",
                    "|value": "Recent trauma / surgery / invasive procedure",
                    "|terminology": "local"
                }
            ],

            "likely_source_of_infection": [
                { //Pattern for Coded text
                    "|code": "at0027",
                    "|value": "Indwelling device",
                    "|terminology": "local"
                },
                {//Pattern for Coded text
                    "|code": "at0015",
                    "|value": "Surgical",
                    "|terminology": "local"
                },
                { //Pattern for non-coded text
                    "|value": "Covid-19"
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
```
##### NEWS2
```json

        "news2": {
            "temperature": {
                "|magnitude": 90.7,
                "|unit": "°C"
            },
            "spO2": 91.0,
            "inspired_oxygen":  {
                "flow_rate":
                    {
                        "|magnitude": 23.5,
                        "|unit": "l/min"
                    },
                "method_of_oxygen_delivery": "Mask"
            },
            "pulse": 110,
            "respirations": 34.4,
            "acvpu": {
                "|code": "at0015",
                "|value": "Confusion",
            },
            "systolic": 98,
            "diastolic": 58,

```
##### NEWS2 Score

These are calculated values that are returned by the middleware, then submitted as part of the composition commit.

```json

            "news2_score": {
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
        }
    },
```
##### Response
```json

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
                "date_isolation_due_to_end": [
                    "2020-09-14T13:19:30.700Z"
                ],
            }
        ],
        "narrative": "Isolation of infection contact"
    },
    "service": [
        {
            "ism_transition": {
                "current_state": {
                    "|code": "526",
                    "|value": "planned",
                    "|terminology": "openehr"
                },
                "careflow_step": {
                    "|code": "at0002",
                    "|value": "Service planned",
                    "|terminology": "local"
                }
            },
            "service_name": {
                "|code": "170499009",
                "|value": "Isolation of infection contact",
                "|terminology": "SNOMED-CT"
            }
        }
    ]
}
```