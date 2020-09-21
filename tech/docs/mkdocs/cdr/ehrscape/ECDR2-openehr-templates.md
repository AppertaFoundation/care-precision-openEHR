# Working with openEHR Templates

openEHR templates are aggregations of logical archetype models that along with the basic Reference model, act as the validation schema for any patient data submitted to the CDR. You cannot submit any information to a CDR without first registering the template which will be used to validate it.

This section will test our connection the CDR by running a `List templates` call, then upload a new template to the CDR via an `Upload a template` call.


## A. List available templates

This call simply returns a list of the templates currently registered with the CDR, each with a unique `templateId`.

=== "cURL"
    ```bash
      curl --location --request GET '{{ehrscapeBaseUrl}}/template' \
      --header 'Content-Type: application/json' \
      --header 'Authorization: {{authToken}}'
    ```

=== "NodeJS/Axios"
    ```js
      var axios = require('axios');

      var config = {
        method: 'get',
        url: '{{ehrscapeBaseUrl}}/template',
        headers: { 
          'Accept': 'application/json', 
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

    url = "{{ehrscapeBaseUrl}}/template"

    payload = {}
    headers = {
      'Content-Type': 'application/json',
      'Authorization': ' {{authToken}}'
    }

    response = requests.request("GET", url, headers=headers, data = payload)

    print(response.text.encode('utf8'))
    ```

#### Response

If your CDR is already provisioned with some templates, you will get a `200` code and some output like this...

```json
{
    "templates": [
        {
            "templateId": "DHCI - Suspected Covid-19 assessment.v0",
            "createdOn": "2020-03-03T18:26:47.943Z"
        },
        {
            "templateId": "Vital Signs Encounter (Composition)",
            "createdOn": "2019-10-29T18:01:30.819Z"
        },
        {
            "templateId": "WHO - Suspected Covid-19 assessment.v0",
            "createdOn": "2020-02-28T18:46:29.960Z"
        }
    ]
}
```

otherwise you should get a `204` code and an empty array.

If you get some other error, this is likely to be that you have not set the baseEhrscapeURL correctly, or that the Authorization token is incorrect.

## B. Upload an operational template (XML)

You should be able to find an example 'operational' template in the `\technical\templates` folder. This is an XML file which contains the 'constraints' information required by the CDR to correctly validate anty information that is committed.
 
 The template example with `templateId : 'DHI - Urology_PROMs-v0'` represents a simple data-entry dataset to allow patients with Prostate cancer to record how they are feeling, and then share this with their care team.

Don't worry for now about the format of the file itself. It follows the Archetype Object Model (1.4), but is always generated automatically by tools such as the openEHR Archetype Designer. 


=== "cURL"
    ```bash
        curl --location --request POST '{{ehrscapeBaseUrl}}/template/' \
        --header 'Content-Type: application/xml' \
        --header 'Authorization: {{authToken}}' \
        --data-raw '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
        <template xmlns="http://schemas.openehr.org/v1">
          <!-- Snipped for brevity -->
        </template>
        '
    ```
=== "NodeJS/Axios"
    ```js
      var axios = require('axios');
      var data = '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>\n<template xmlns="http://schemas.openehr.org/v1">\n<!-- Snipped for brevity -->\n</template> TRIMMED for Brevity...... </template>\n';

      var config = {
        method: 'post',
        url: '{{ehrscapeBaseUrl}}/template/',
        headers: { 
          'Accept': 'application/json', 
          'Content-Type': 'application/xml',  
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
    ``
=== "Python/requests"
    ```python
    import requests

    url = "{{ehrscapeBaseUrl}}/template/"

    payload = "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n<template xmlns=\"http://schemas.openehr.org/v1\">\n    <language>\n        <terminology_id>\n            <value>ISO_639-1</value>\n        </terminology_id>\n        <code_string>en</code_string>\n    </language>\n    <description>\n -- Trimmed for brevity --- </template>"
    headers = {
      'Content-Type': 'application/xml',
      'Authorization': '{{authToken}}'
    }

    response = requests.request("POST", url, headers=headers, data = payload)

    print(response.text.encode('utf8'))

    ```

#### Response

Better CDR will give a `201` response code and return the `templateID`.

```json
{
    "action": "CREATE",
    "templateId": "NES-ACP_COVID.v0.0"
}
```

### Overwriting an existing template

The BetterCDR allows templates to be over-written by simply re-sending the `POST` call and returns a `201` code.


## Better 'Web templates'

As well as being used to validate patient records when they are commited to the CDR, templates are used as the basis for many other types of technical artefact, such as automatic forms builders, class library generation, and for client-side validation in UI.

Although formally aligned with the in-memory AOM, the operational template can be hard to parse and understand, particularly if you are just trying to understand the various schema constraints.

For this purpose, you may find it helpful to generate a **'Web template'** - this is a much simpler JSON format, itself based on the operational template, and which can be exported from the openEHR Archetype Designer via the Export menu or retrieved via the Get Web Template (JSON) call.

=== "cURL"
    ```bash
      curl --location --request GET '{{ehrscapeBaseUrl}}/template/{{templateId}}' \
      --header 'Content-Type: application/json' \
      --header 'Authorization: {{authToken}}
      ```
=== "NodeJS/Axios"
    ```js
    var axios = require('axios');

    var config = {
      method: 'get',
      url: '{{ehrscapeBaseUrl}}/template/{{templateId}}',
      headers: { 
        'Content-Type': 'application/json', 
        'Authorization': '{{authToken}}', 
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

      url = "{{ehrscapeBaseUrl}}/template/{{templateId}}"

      payload = {}
      headers = {
        'Content-Type': 'application/json',
        'Authorization': '{{authToken}}',
      }

      response = requests.request("GET", url, headers=headers, data = payload)

      print(response.text.encode('utf8'))
    
    ```

Now that we have a valid template uploaded, we can [Commit a Composition](ECDR3-committing-a-composition.md) of patient data to the CDR.
