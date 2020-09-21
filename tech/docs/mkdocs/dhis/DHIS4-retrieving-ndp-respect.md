# Retrieving a ReSPECT Composition

All data committed to an openEHR CDR is done so via a POST or PUT /composition call - as a JSON or XML 'blob'. 

This section will cover how to retrieve the current ReSPECT Composition by running a `GET / composition` call.

A number of data serialisation options, can be used on retrieval. In this case we will ask for the Better `STRUCTURED JSON` format, as this is what we used when committing the composition, but you can commit and retrieve using different formats if you wish.

#### Better Ehrscape `GET /composition - Retrieve a composition`

##### Parameters

`compositionId`: 

This is is the composition UID for the composition you wish to retrieve. Don't worry about how we find that out for now. Just use the UID for the composition you just committed in the last section 

We will find out how to find compositionIds in a subsequent section.

`format`:

This defines the format of JSON or XML that you are requesting. Use `STRUCTURED` for this example.

=== "cURL" 
    ```bash  
       curl --location --request GET '{{cdr.ehrscapeBaseUrl}}/composition/12d53bf8-3abb-43a7-9621-b3d9638d7790::a81f47c6-a757-4e34-b644-3ccc62b4a01c::1?format=STRUCTURED' \
        --header 'Content-Type: application/json' \
        --header 'Authorization': '{{cdr.authToken}}'
    ```

=== "NodeJS/Axios"
    ```js

      var axios = require('axios');

      var config = {
        method: 'get',
         url: '{{cdr.ehrscapeBaseUrl}}/composition/12d53bf8-3abb-43a7-9621-b3d9638d7790::a81f47c6-a757-4e34-b644-3ccc62b4a01c::1?format=STRUCTURED',
         headers: { 
            'Content-Type': 'application/json', 
            'Authorization': '{{cdr.authToken}}'
         }
      };

      axios(config)
      .then(function (response) {
        console.log(JSON.stringify(response.data));
      })
      .catch(function (error) {
        console.log(error);
      });
    ```

=== "Python/requests"
    ```python

        import requests

        url = "{{cdr.ehrscapeBaseUrl}}1/composition/12d53bf8-3abb-43a7-9621-b3d9638d7790::a81f47c6-a757-4e34-b644-3ccc62b4a01c::1?format=STRUCTURED"

        payload = {}
        headers = {
        'Content-Type': 'application/json',
        'Authorization': '{{cdr.authToken}}'
        }

        response = requests.request("GET", url, headers=headers, data = payload)

        print(response.text.encode('utf8'))
    ```

#### Response

If the composition is found, a `200` code will be returned along with the composition object, which you will note now includes the `compositionUid`, but should otherwise be identical to the json which you previously submitted.

```json
 {
    "meta": {
        "href": "https://cdr.code4health.org/rest/v1/composition/12d53bf8-3abb-43a7-9621-b3d9638d7790::a81f47c6-a757-4e34-b644-3ccc62b4a01c::1"
    },
    "compositionUid": "12d53bf8-3abb-43a7-9621-b3d9638d7790::a81f47c6-a757-4e34-b644-3ccc62b4a01c::1",
    "format": "STRUCTURED",
    "templateId": "ReSPECT_v3-6-7",
    "composition": {
        "respect_v3-6-7": {
            "_uid": [
                "12d53bf8-3abb-43a7-9621-b3d9638d7790::a81f47c6-a757-4e34-b644-3ccc62b4a01c::1"
            ],
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
                    "start_time": [
                        "2020-07-17T14:09:02.229Z"
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
            "respect_headings": [
                {
                    "a2._shared_understanding": [
                        {
                            "respect_summary": [
                                {
                                    "narrative_summary": [
                                        "Something goes in here"
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
                            "details_of_other_relevant_care_planning_documents_and_where_to_find_them": [
                                {
                                    "reference_to_advance_care_directives_composition": [
                                        {
                                            "advance_planning_documentation": [
                                                {
                                                    "summary": [
                                                        "And in here"
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
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "reference_to_legal_welfare_proxies_composition": [
                                {
                                    "legal_welfare_proxy_in_place": [
                                        {
                                            "status": [
                                                {
                                                    "|code": "at0007",
                                                    "|value": "Unknown",
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
                                    ]
                                }
                            ],
                            "legal_welfare_proxy_in_place": [
                                {
                                    "status": [
                                        {
                                            "|code": "at0005",
                                            "|value": "Yes",
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
                            ]
                        }
                    ],
                    "a3._what_matters_to_me": [
                        {
                            "what_matters_to_me": [
                                {
                                    "what_i_most_value": [
                                        "Beer"
                                    ],
                                    "what_i_most_fear": [
                                        "My wife"
                                    ],
                                    "respect_care_priority_scale": [
                                        {
                                            "care_priority_scale": [
                                                99
                                            ]
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
                            ]
                        }
                    ],
                    "a4._clinical_recommendations": [
                        {
                            "cpr_decision": [
                                {
                                    "cpr_decision": [
                                        {
                                            "|code": "at0004",
                                            "|value": "CPR attempts recommended adult or child",
                                            "|terminology": "local"
                                        }
                                    ],
                                    "date_of_cpr_decision": [
                                        "2020-07-09T00:00+01:00"
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
                            ]
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
                    "|name": "a81f47c6-a757-4e34-b644-3ccc62b4a01c"
                }
            ]
        }
    },
    "deleted": false,
    "lastVersion": true,
    "tags": [
        {
            "tag": "formVersion",
            "aqlPath": "/",
            "value": "1.0.0"
        },
        {
            "tag": "formName",
            "aqlPath": "/",
            "value": "ReSPECT"
        }
    ],
    "ehrId": "3e674739-950c-4b8a-976b-5aef21c618c5",
    "lifecycleState": "COMPLETE"
}
```

!!! hint 

    #### Other data formats

    The Better Ehrscape API offers several other serialisation formats. You can have a look at these by simply changing the `format` parameter on the `GET / composition` call, and the call Header `Accept` to switch between JSON and XML.

    Right now , EhrBase only support the 'canonical formats but we understand they will be releasing support for the Better formats 'imminently'

    ##### 'RAW JSON'

    This is very similar to, but not identical to the openEHR Canonical JSON format, which essentially supersedes it. It very closely adheres to the openEHR Reference model specification but is pretty voluminous

    ```
    format=RAW
    Accept : `application/json'
    ```


    ##### 'RAW XML'

    This is 'canonical' openEHR XML which is also accepted by the openEHR REST  API. It is the lingua-franca for all openEHR CDRs, even those which do not support the REST CDR API, will normally accept and expose data in this XML format. 

    ```
    format=RAW
    Accept : `application/xml'
    ```









