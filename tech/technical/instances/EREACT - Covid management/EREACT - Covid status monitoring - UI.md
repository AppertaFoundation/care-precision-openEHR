### Header

```json
    "template_id": "open_eREACT-Care", //Fixed
    "start_time": "2020-09-07T21:04:10.789Z", //ISO DateTime
    "setting": "other care", //Fixed
    "healthcare_facility": "Glen Carse Care Home", // Institution name
    "composer": {  //Clinical author of the document
        "name": "RN Joyce Brown",
        "id": {
            "type": "NMC", // From Demographics
            "id": "12342341", //From demographics
            "namespace": "uk.org.nmc" //from demographics
        }
    },
```
```json
    "current_covid_status": { 
            "problem_diagnosis_name": { //FIXED
            "|code": "1240761000000102", //FIXED
            "|value": "Suspected Covid-19",
            "|terminology": "SNOMED-CT" //FIXED
        },
        
        "diagnostic_certainty": "Negative (Tested Negative)"
    },     
```    
#### diagnostic_certainty valueset
   Suspected Symptoms (Assessed but no test)
   Exposure to COVID (Assessed but no test)
   Positive (Tested Positive)
   Negative (Tested Negative)
   Recovered (Tested Negative following previous positive test)


### Isolation status
```json

"isolation_status": {
        "service_name": {
        "|code": "170499009", //FIXED
        "|value": "Isolation of infection contact", //FIXED
        "|terminology": "SNOMED-CT" //FIXED
        },
        "reason_for_request": {
            "|code": "840539006", //FIXED
            "|value": "Disease caused by 2019-nCoV", //FIXED
            "|terminology": "SNOMED-CT" //FIXED
        },
        "reason_for_isolation": "Tested positive (10 days)",
        "isolation duration" : "P3D", // use ISO 1861 Duration syntax P3D = 5 days P10D = 10 days etc https://www.digi.com/resources/documentation/digidocs/90001437-13/reference/r_iso_8601_duration_format.htm
        "date_isolation_due_to_start": "2020-11-10T22:39:31.826Z",
        "date_isolation_due_to_end": "2020-11-10T22:39:31.826Z"
        },
```
#### `reason_for_isolation` Valueset

### Current status
```json
    "health_risk_assessment": {
        "health_risk": {
            "|code": "1240761000000102", //FIXED
            "|value": "Suspected Covid-19", //FIXED
            "|terminology": "SNOMED-CT" //FIXED
        },
        "rationale": "Negative (Tested Negative)"
    }    
```
#### `rationale` Valueset    
