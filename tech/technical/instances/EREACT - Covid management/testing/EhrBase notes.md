	Order of xsi:schema attribute
	Section UID missing
	ns2: namespace redundant

FLAT JSON Commit

- UID missing on SECTION,ENTRY locatables

 "covid_status_monitoring/suspected_covid/_uid": "",
    <uid xsi:type="HIER_OBJECT_ID">
                <value>69ae4dd0-3b1e-45e3-8a4c-d7f5909741e2</value>
            </uid>

- action_archetype missing

               <action_archetype_id>/.*/</action_archetype_id>
- Careflow step missing


    "covid_status_monitoring/lab_testing/covid_test_tracking/ism_transition/careflow_step|code": "at0026",
    "covid_status_monitoring/lab_testing/covid_test_tracking/ism_transition/careflow_step|value": "Service request sent",
    "covid_status_monitoring/lab_testing/covid_test_tracking/ism_transition/careflow_step|terminology": "local",
  ```
        <careflow_step>
                    <value>Service request sent</value>
                    <defining_code>
                        <terminology_id>
                            <value>local</value>
                        </terminology_id>
                        <code_string>at0026</code_string>
                    </defining_code>
                </careflow_step>
				```