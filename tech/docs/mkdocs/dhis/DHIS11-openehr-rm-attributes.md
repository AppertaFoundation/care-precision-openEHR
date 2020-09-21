---
title: "Key openEHR RM attributes" 
summary: This section provides a basic overview of key openEHR reference model attributes 
---

![](../images/construction.jpg)

# Key openEHR RM attributes

The openEHR Reference model defines a relatively small set of information model constructs which openEHR back-ends must support. This includes a number of generic classes and datatypes.

The Reference model contains virtually no clinical content e.g concepts for Medication, or Diagnosis. These are defined and managed separately as `archetypes`.

A number of key data points need to be populated in an openEHR composition, which may not be apparent from the archetypes or templates.
Developers can largely use the example instance documents and APIs for guidance but these notes may give useful background in addition to viewing the [UML view of the openEHR reference model.](http://www.openehr.org/local/releases/1.0.1/uml/index.html)

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

