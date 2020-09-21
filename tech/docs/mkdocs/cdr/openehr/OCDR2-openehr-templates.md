# Working with openEHR Templates

openEHR templates are aggregations of logical archetype models that along with the basic Reference model, act as the validation schema for any patient data submitted to the CDR.

This section will test our connection the CDR by running a `List templates` call, then upload a new template to the CDR via an `Upload a template` call


## A. List templates

=== "cURL"
    ```bash
        curl 
        --locations 
        --request GET '{{openehrBaseUrl}}/definition/template/adl1.4' \
        --header 'Accept: application/json' \
        --header 'Prefer: return=minimal' \
        --header 'Authorization: {{authToken}}'
    ```

=== "NodeJS/Axios"  
    ```js
    var axios = require('axios');

    var config = {
      method: 'get',
      url: '{{openehrBaseUrl}}/definition/template/adl1.4',
      headers: { 
        'Accept': 'application/json', 
        'Prefer': 'return=minimal', 
        'Authorization': '{{authToken}}'
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

      url = "{{openehrBaseUrl}}/definition/template/adl1.4"

      payload = {}
      headers = {
        'Accept': 'application/json',
        'Prefer': 'return=minimal',
        'Authorization': '{{authToken}}'
      }

      response = requests.request("GET", url, headers=headers, data = payload)

      print(response.text.encode('utf8'))
    ```

#### Response

If your CDR is already provisioned with some templates, you will a 200 code and some output like this.

```json
[
    {
        "concept": "IDCR - Vital Signs Encounter.v1",
        "template_id": "IDCR - Vital Signs Encounter.v1",
        "archetype_id": "openEHR-EHR-COMPOSITION.encounter.v1",
        "created_timestamp": "2020-06-26T17:03:11.518Z"
    },
    {
        "concept": "DENWIS_Observations",
        "template_id": "DENWIS_Observations",
        "archetype_id": "openEHR-EHR-COMPOSITION.encounter.v1",
        "created_timestamp": "2020-06-29T11:26:33.055Z"
    },
    {
        "concept": "Suspected Covid-19 Assessment.v0.1",
        "template_id": "Suspected Covid-19 Assessment.v0.1",
        "archetype_id": "openEHR-EHR-COMPOSITION.encounter.v1",
        "created_timestamp": "2020-07-06T14:24:33.974Z"
    }
]
```

otherwise you should get a 200 code and an empty array.

If you get some other error, this is likely to be that you have not set the baseURL correctly, or that the Authorization token is incorrect.


## B. Upload a new template

You will find an example 'operational' template here in the templates folder. This example is for a simple data-entry dataset to allow patients to record how they are feeling, and then share this with their care team.

Don't worry for now about the format of the file itself. It follows the Archetype Object Model (1.4) but is always generated automatically by tools such as the openEHR Archetype Designer. 

=== "cURL"
    ```bash
    curl 
    --location 
    --request POST '{{openehrBaseUrl}}/definition/template/adl1.4' \
    --header 'Accept: application/xml' \
    --header 'Content-Type: application/xml' \
    --header 'Prefer: return=minimal' \
    --header 'Authorization: {{authToken}}' \
    --data-raw '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <template xmlns="http://schemas.openehr.org/v1">
        <language>
            <terminology_id>
                <value>ISO_639-1</value>
            </terminology_id>
            <code_string>en</code_string>
        </language>
        <description>
      .... // Snipped for brevity //
    </template>
    '
    ```

=== "NodeJS axios"
    ```js
    var axios = require('axios');
    var data = '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>\n<template xmlns="http://schemas.openehr.org/v1">\n    <language>\n        <terminology_id>\n            <value>ISO_639-1</value>\n        </terminology_id>\n        <code_string>en</code_string>\n    </language>\n    <description>\n        <original_author id="name">Ian McNicoll</original_author>\n        <original_author id="organisation">freshEHR Clinical Informatics Ltd.</original_author>\n        <original_author id="email">ian@freshehr.com</original_author>\n        <original_author id="date">2020-02-27</original_author>\n        <lifecycle_state>release_candidate</lifecycle_state>\n        <other_details id="licence> TRIMMED for Brevity...... </template>\n';

    var config = {
      method: 'post',
      url: '{{openehrBaseUrl}}/definition/template/adl1.4',
      headers: { 
        'Accept': 'application/json', 
        'Content-Type': 'application/xml', 
        'PREFER': 'return=minimal', 
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
=== "Python/requests" 
    ```python 
      import requests

    url = "{{openehrBaseUrl}}/definition/template/adl1.4"

    payload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>\n<!--Operational template XML automatically generated by Ocean Template Designer Version 2.8.94Beta-->\n<template xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\" xmlns=\"http://schemas.openehr.org/v1\">\n  <language>\n    <terminology_id>\n      <value>ISO_639-1</value>\n    </terminology_id>\n    <code_string>en</code_string>\n  </language>\n  <description>\n    <original_author id=\"Original Author\">Not Specified</original_author>\n    <lifecycle_state>Initial</lifecycle_state>\n    <other_details id=\"MetaDataSet:Sample Set \">Template metadata sample set </other_details>\n    <other_details id=\"Acknowledgements\"></other_details>\n    <other_details id=\"Business Process Level\"></other_details>\n    <other_details id=\"Care setting\"></other_details>\n    <other_details id=\"Client group\"></other_details>\n    <other_details id=\"Clinical Record Element\"></other_details>\n    <other_details id=\"Copyright\"></other_details>\n    <other_details id=\"Issues\"></other_details>\n    <other_details id=\"Owner\"></other_details>\n    <other_details id=\"Sign off\"></other_details>\n    <other_details id=\"Speciality\"></other_details>\n ... Snipped for brevity ... \n</template>"
    headers = {
      'Accept': 'application/xml',
      'Content-Type': 'application/xml',
      'PREFER': 'return=minimal',
      'Authorization': '{{authToken}}',
    }

    response = requests.request("POST", url, headers=headers, data = payload)

    print(response.text.encode('utf8'))
    ```





#### Response

Currently the response for a successful upload is a little inconsistent between CDRs.

1. ehrBase will give a 204 no response code but the upload has been successful.

2. BetterCDR will give a 201 response code.


### Overwriting an existing template

The current REST specification prohibits overwriting an existing template - issuing a `409 conflict` code and while this makes sense for deployments it has proven to be over-restrictive during early development where a template may change repeatedly.

1. BetterCDR allows templates to be over-written and simply returns a `201` code.

2. ehrBase prohibits template over-writing by default but does allow a server configuration to be set which loosens this restriction.


## More on templates

As well as being used to validate patient records when they arecommited to the CDR, templates are used as the basis for many other types of technical artefact, such as automatic forms builders, class library generation, and for client-side validation in UI.

Although formally aligned with the in-momory AOM, the operational template can be hard to parse and understand, particularly if you are just trying to understand the various schema constraints.

For this purpose, you may find it helpful to gnerate a 'Web template' - this is a much simpler JSON format, itself based on the operational template, and which can be exported from the openEHR Archetype Designer via the Export menu.

Now that we have a valid template uploaded, we can [Commit a Composition](OCDR3-committing-a-composition.md) of patient data to the CDR.


