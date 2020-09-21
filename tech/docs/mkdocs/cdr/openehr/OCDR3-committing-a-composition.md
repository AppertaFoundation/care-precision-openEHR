# Committing openEHR data

All data commited to an openEHR CDR is done so via a POST /composition call - as a JSON or XML 'blob'. 

As it is committed, the data will be validated against both the appropriate openEHR template and the underlying Reference model schema.

If the data is valid, it will be stored in the CDR and is allocated a unique ID, which is returned by the POST /composition call

This section will submit an example Composition to the CDR by running a `POST / composition` call.

A number of data serialisation options, can be used. In this case we will use the Better `STRUCTURED JSON` format, as it is somewhat easier to use than the current openEHR `CANONICAL JSON` format.

!!! note
Note that this first example uses the Better `Better Ehrscape API` which has a slightly different base URL and parameters than the `openEHR REST API`,though the data is stored identically and can be accessed from both end points.

#### Ehrscape POST /composition example

##### Parameters

`ehrId`: 

This is is the internal CDR identifier for a specific patient. When a patient is registered with the CDR,an EHR object is created with a unique `ehr_id` identifier, and is associated with an external `subjectId` and subjectNamespace e.g an NHS Number, CHI number, or a local hospital number.

We will find out how to work out the correct ehrId for a patient in the next section.

Generally when you first open a patient record session, you will retrieve their `ehrId` via their `subjectID` and `subjectNamespace`. We will explain how to do that in the next section.

For testing purposes, you should use a known `ehrId`. If you have a Postman environment file, an example will be in there, otherwise you can find out how to identify valid ehrIds [here]()


`templateId`: 

This is the identifier of the openEHR template, against which you need to validate the composition. Use `DHI - Urology_PROMs-v0` for this example.  


`format`: 

This defines the format of JSON or XML that you are sending. Use `STRUCTURED` for this example.




## A. Commit an openEHR Composition (`STRUCTURED JSON`)

=== "cURL"
  
  ```bash
      curl 
      --location 
      --request POST '{{ehrscapeBaseUrl}}/composition?ehrId={{ehrId}}&templateId={{templateId}}&format=STRUCTURED' \
      --header 'Content-Type: application/json' \
      --header 'Authorization: {{auth_token}}' \
      --data-raw '{
      "prostate_cancer_proms_report": {
          "language": [
              {
                  "|code": "en",
                  "|terminology": "ISO_639-1"
              }
          ],
          "territory": [
              {
                  "|code": "EN",
                  "|terminology": "ISO_3166-1"
              }
          ],
          "context": [
              {
                  "xds_metadata": [
                      {
                          "document_type": [
                              "Patient recorded outcome measures"
                          ]
                      }
                  ],
                  "start_time": [
                      "2020-07-05T13:32:56.186Z"
                  ],
                  "setting": [
                      {
                          "|code": "238",
                          "|value": "other care",
                          "|terminology": "openehr"
                      }
                  ]
              }
          ],
           "eortc_qlq-c30": [
            {
                "any_event": [
                    {
                        "trouble_doing_strenuous_activities": [
                            {
                                "|code": "at0007",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "trouble_taking_a_long_walk": [
                            {
                                "|code": "at0040",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "trouble_taking_a_short_walk_outside_of_the_house": [
                            {
                                "|code": "at0044",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "need_to_stay_in_bed_or_a_chair_during_the_day": [
                            {
                                "|code": "at0049",
                                "|value": "Very much",
                                "|ordinal": 4
                            }
                        ],
                        "need_help_with_eating_dressing_washing_yourself_or_using_the_toilet": [
                            {
                                "|code": "at0051",
                                "|value": "A little",
                                "|ordinal": 2
                            }
                        ],
                        "during_the_past_week_were_limited_in_doing_either_work_or_other_daily_activities": [
                            {
                                "|code": "at0056",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "during_the_past_week_were_limited_in_pursuing_hobbies_or_other_leisure_time_activities": [
                            {
                                "|code": "at0060",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "during_the_past_week_had_short_of_breath": [
                            {
                                "|code": "at0064",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "during_the_past_week_had_pain": [
                            {
                                "|code": "at0067",
                                "|value": "A little",
                                "|ordinal": 2
                            }
                        ],
                        "during_the_past_week_need_to_rest": [
                            {
                                "|code": "at0072",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "during_the_past_week_had_trouble_sleeping": [
                            {
                                "|code": "at0076",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "during_the_past_week_felt_weak": [
                            {
                                "|code": "at0078",
                                "|value": "Not at all",
                                "|ordinal": 1
                            }
                        ],
                        "during_the_past_week_lacked_appetite": [
                            {
                                "|code": "at0084",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "during_the_past_week_felt_nauseated": [
                            {
                                "|code": "at0086",
                                "|value": "Not at all",
                                "|ordinal": 1
                            }
                        ],
                        "during_the_past_week_had_vomited": [
                            {
                                "|code": "at0090",
                                "|value": "Not at all",
                                "|ordinal": 1
                            }
                        ],
                        "during_the_past_week_have_been_constipated": [
                            {
                                "|code": "at0097",
                                "|value": "Very much",
                                "|ordinal": 4
                            }
                        ],
                        "during_the_past_week_had_diarrhea": [
                            {
                                "|code": "at0099",
                                "|value": "A little",
                                "|ordinal": 2
                            }
                        ],
                        "during_the_past_week_were_tired": [
                            {
                                "|code": "at0102",
                                "|value": "Not at all",
                                "|ordinal": 1
                            }
                        ],
                        "during_the_past_week_pain_interfere_with_daily_activities": [
                            {
                                "|code": "at0109",
                                "|value": "Very much",
                                "|ordinal": 4
                            }
                        ],
                        "during_the_past_week_had_difficulty_in_concentrating": [
                            {
                                "|code": "at0110",
                                "|value": "Not at all",
                                "|ordinal": 1
                            }
                        ],
                        "during_the_past_week_felt_tense": [
                            {
                                "|code": "at0115",
                                "|value": "A little",
                                "|ordinal": 2
                            }
                        ],
                        "during_the_past_week_were_worried": [
                            {
                                "|code": "at0121",
                                "|value": "Very much",
                                "|ordinal": 4
                            }
                        ],
                        "during_the_past_week_felt_irritable": [
                            {
                                "|code": "at0123",
                                "|value": "A little",
                                "|ordinal": 2
                            }
                        ],
                        "during_the_past_week_felt_depressed": [
                            {
                                "|code": "at0128",
                                "|value": "Quite a bit",
                                "|ordinal": 3
                            }
                        ],
                        "during_the_past_week_had_difficulty_remembering_things": [
                            {
                                "|code": "at0133",
                                "|value": "Very much",
                                "|ordinal": 4
                            }
                        ],
                        "during_the_past_week_physical_condition_or_medical_treatment_interfered_with_family_life": [
                            {
                                "|code": "at0135",
                                "|value": "A little",
                                "|ordinal": 2
                            }
                        ],
                        "during_the_past_week_physical_condition_or_medical_treatment_interfered_with_social_activities": [
                            {
                                "|code": "at0138",
                                "|value": "Not at all",
                                "|ordinal": 1
                            }
                        ],
                        "during_the_past_week_physical_condition_or_medical_treatment_caused_financial_difficulties": [
                            {
                                "|code": "at0143",
                                "|value": "A little",
                                "|ordinal": 2
                            }
                        ],
                        "rate_overall_health_during_the_past_week": [
                            {
                                "|code": "at0147",
                                "|value": "2",
                                "|ordinal": 2
                            }
                        ],
                        "rate_overall_quality_of_life_during_the_past_week": [
                            {
                                "|code": "at0157",
                                "|value": "5",
                                "|ordinal": 5
                            }
                        ],
                        "total_score": [
                            61
                        ],
                        "time": [
                            "2020-07-15T16:47:06.320Z"
                        ]
                    }
                ],
                "scoring_method": [
                    {
                        "|code": "at0164",
                        "|value": "Linear transformation",
                        "|terminology": "local"
                    }
                ],
                "language": [
                    {
                        "|code": "en",
                        "|terminology": "ISO_639-1"
                    }
                ],
                "encoding": [
                    {
                        "|code": "UTF-8",
                        "|terminology": "IANA_character-sets"
                    }
                ]
            }
        ],
        "i-pss_prostate_score": [
              {
                  "a1._incomplete_emptying": [
                      {
                          "|code": "at0015",
                          "|value": "Less Than 1 Time In 5",
                          "|ordinal": 1
                      }
                  ],
                  "a2._frequency": [
                      {
                          "|code": "at0016",
                          "|value": "Less Than Half The Time",
                          "|ordinal": 2
                      }
                  ],
                  "a3._intermittency": [
                      {
                          "|code": "at0017",
                          "|value": "About Half The Time",
                          "|ordinal": 3
                      }
                  ],
                  "a4._urgency": [
                      {
                          "|code": "at0017",
                          "|value": "About Half The Time",
                          "|ordinal": 3
                      }
                  ],
                  "a5._weak_stream": [
                      {
                          "|code": "at0016",
                          "|value": "Less Than Half The Time",
                          "|ordinal": 2
                      }
                  ],
                  "a6._straining": [
                      {
                          "|code": "at0018",
                          "|value": "More Than Half The Time",
                          "|ordinal": 4
                      }
                  ],
                  "a7._nocturia": [
                      {
                          "|code": "at0060",
                          "|value": "3 times",
                          "|ordinal": 3
                      }
                  ],
                  "total_i-pss_score": [
                      18
                  ],
                  "i-pss_score_grade": [
                      {
                          "|code": "at0087",
                          "|value": "8-19 Moderate",
                          "|terminology": "local"
                      }
                  ],
                  "time": [
                      "2020-07-05T13:32:56.186Z"
                  ],
                  "language": [
                      {
                          "|code": "en",
                          "|terminology": "ISO_639-1"
                      }
                  ],
                  "encoding": [
                      {
                          "|code": "UTF-8",
                          "|terminology": "IANA_character-sets"
                      }
                  ]
              }
          ],
          "category": [
              {
                  "|code": "433",
                  "|value": "event",
                  "|terminology": "openehr"
              }
          ],
          "composer": [
              {
                  "|name": "John Smith"
              }
          ]
      }
  }'
  ```


=== "NodeJS + Axios"
  ```js

    var axios = require('axios');

    var data = JSON.stringify({"prostate_cancer_proms_report": // trimmed for brevity}");

    var config = {
      method: 'post',
      url: '{{ehrscapeBaseUrl}}/composition?ehrId={{ehrId}}&templateId={{templateId}}&format=STRUCTURED',
      headers: { 
        'Content-Type': 'application/json', 
        'Authorization': '{{authToken}}'
      },
      data : data
    };

    axios(config)
    .then(function (response) {
      console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
      console.log(error);
    });

```


### Response for POST /composition

```json
{
    "meta": {
        "href": "https://cdr.code4health.org/rest/v1/composition/59e8f5a2-6fb6-47d5-9acd-ae6309d0f1dd::a81f47c6-a757-4e34-b644-3ccc62b4a01c::1"
    },
    "action": "CREATE",
    "compositionUid": "59e8f5a2-6fb6-47d5-9acd-ae6309d0f1dd::a81f47c6-a757-4e34-b644-3ccc62b4a01c::1"
}
```

#### The `Composition Id`

The compositionUid is the unique identifier allocated to (and held within) every composition by the CDR.

You will see that it ends in `...::1`. The `1` is the version of this composition instance. If you need to update the instance (perhaps because of an error), you need to do so via a PUT / composition call and if succesful the composition version number will clock up to `::2`.

In essence every commit is versioned and retained for medico-legal reasons. 

Similarly when a composition is deleted, this is a logical delete and the composition can always be retreived, though is not normally accessible via querying.

We will go through the process of updating a composition later.

For now let's just [retrieve the composition](OCDR4-retrieving-a-composition.md) we just committed, via the GET /composition call.








