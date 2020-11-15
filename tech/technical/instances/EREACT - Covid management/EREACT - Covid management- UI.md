### Header

```json
    "start_time": "2020-09-07T21:04:10.789Z", //ISO DateTime
    "setting": "nursing home care", //Fixed
    "composer": {  //Clinical author of the document
        "name": "RN Joyce Brown",
        "id_scheme": "NMC", // From Demographics
        "id": "12342341", //From demographics
        "id_namespace": "uk.org.nmc" //from demographics
    }
   "healthcare_facility": {  //Clinical author of the document
        "|name": "Glen Carse Care Home",
        "|id_scheme": "CQC", // From Demographics
        "|id": "44832", //From demographics
        "id_namespace": "uk.org.cqc" //from demographics
    }
 ```

### Suspected covid
```json
     "suspected_covid": "Negative (Tested Negative)",
```    
#### `suspected_covid` valueset
   
   Suspected Symptoms (Assessed but no test)
   Exposure to COVID (Assessed but no test)
   Positive (Tested Positive)
   Negative (Tested Negative)
   Recovered (Tested Negative following previous positive test)


### Isolation request
```json

   "isolation_request": {
        "reason_for_request": {
            "|code": "840539006",
            "|value": "Disease caused by 2019-nCoV",
            "|terminology": "SNOMED-CT"
        },
        "reason_for_isolation": "Tested positive (10 days)",
        // use ISO 1861 Duration syntax P3D = 5 days P10D = 10 days etc https://www.digi.com/resources/documentation/digidocs/90001437-13/reference/r_iso_8601_duration_format.htm
        "isolation duration": "P3D",
        "date_isolation_due_to_start": "2020-11-10T22:39:31.826Z",
        "date_isolation_due_to_end": "2020-11-10T22:39:31.826Z"
    },
```
#### `reason_for_request` Valueset

```json
  "list" : [ {
              "|code" : "840544004",
              "|value" : "Suspected disease caused by 2019 novel coronavirus",
               "|terminology" : "SNOMED-CT"
            },
            {
              "|code" : "840546002",
              "|value" : "Exposure to 2019 novel coronavirus",
              "|terminology" : "SNOMED-CT"
            },
            {
              "|code" : "840539006",
              "|value" : "Disease caused by 2019-nCoV",
              "|terminology" : "SNOMED-CT"
            } ],
```
   
### Covid test request
```json

    "covid_test_request": {
        "reason_for_request": "Recovery Check",
        "status": {
            "|code": "at0026",
            "|value": "Service request sent",
            "|terminology": "local"
        },
        "status_time": "2020-11-13T16:57:22.995Z"
    },
```
#### `reason_for_request` Valueset

Symptoms
Recovery Check
Contact with symptoms
Routine Test


#### `status` Valueset

```json
           "list" : [ {
              "|code" : "at0026",
              "|value" : "Service request sent",
             
            }, 
            {
              "|code" : "at0005",
              "|value" : "Service activity complete",
              "|terminology": "local"           
              },
```

### Covid test result
```json
      "covid_test_result": {
        "test_result": {
            "|code": "1321111000000101",
            "|value": "COVID-19 excluded by laboratory test",
            "|terminology": "SNOMED-CT"
        },
        "specimenTakenTime": "2020-11-13T16:57:22.995Z"
    }
```
#### `test_result` Valueset

```json
          "list" : [ {
            "|code" : "1300721000000109",
            "|value" : "COVID-19 confirmed by laboratory test",
            "|terminology" : "SNOMED-CT"
            }
          }, 
          {
            "|code" : "1321111000000101",
            "|value" : "COVID-19 excluded by laboratory test",
            "|terminology" : "SNOMED-CT"
          } ],
```


   