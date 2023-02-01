subject_schemes
================
The table `subject_schemes <https://schema.astromat.org/ada/tables/subject_schemes.html>`_ is to hold unambiguous subject schemes allowed by ADA system.

It is used with table ``record_subjects`` to store more scientific metadata related to the ``record``, etc. SAMIS data product.

**term conventions**

Mandatory (**M**)
  The property must always be present in the metadata. An empty value for the property is not allowed.

Mandatory if Applicable (**MA**)
  When the property value can be obtained it must be present.

Recommended (R)
  The use of the property is recommended.

Optional (O)
  It is not important whether the property is used or not, but if used it may provide complementary information about the resource

subject_scheme_name (M)
-----------------------

All schemes can be found in SAMIS data product metadata.

* ``sample``
* ``analysis.general``
* ``analysis.technique``
* ``analysis.instrument``
* ``analysis.laboratory``

subject_scheme_template (M)
---------------------------
To hold the JSON schema for different subject schemes. It will be used to create JSON object for column ``subject`` in the table ``record_subjects``.

* ``analysis.general template`` 

.. code-block:: json

   {
      "$schema": "https://json-schema.org/draft/2019-09/schema",
      "type": "object",
      "title": "Analysis Technique Schema",
      "required": [
         "sessionId",
         "analysisDate"
      ],
      "properties": {
         "sessionId": {
               "type": "string",
               "examples": [
                  ""
               ]
         },
         "analysisDate": {
               "type": "string",
               "examples": [
                  "2023-01-02"
               ]
         }
      },
      "examples": [{
         "sessionId": "20230102_EMPA_UAZ_OREX-8",
         "analysisDate": "2023-01-02"
      }]
   }

* ``analysis.technique template`` 

.. code-block:: json

   {
      "$schema": "https://json-schema.org/draft/2019-09/schema",
      "type": "object",
      "title": "Analysis Technique Schema",
      "required": [
         "name",
         "identifier"
      ],
      "properties": {
         "name": {
               "type": "string",
               "examples": [
                  "Electron Microprobe Analysis"
               ]
         },
         "identifier": {
               "type": "string",
               "examples": [
                  "EMPA"
               ]
         }
      },
      "examples": [{
         "name": "Electron Microprobe Analysis",
         "identifier": "EMPA"
      }]
   }

* ``analysis.instrument template`` 

.. code-block:: json

   {
      "$schema": "https://json-schema.org/draft/2019-09/schema",
      "type": "object",
      "title": "Analysis Instrument Schema",
      "required": [
         "name",
         "identifier"
      ],
      "properties": {
         "name": {
               "type": "string",
               "examples": [
                  "Cameca 100X"
               ]
         },
         "identifier": {
               "type": "string",
               "examples": [
                  "CAM100"
               ]
         }
      },
      "examples": [{
         "name": "Cameca 100X",
         "identifier": "CAM100"
      }]
   }

* ``analysis.laboratory template`` 

.. code-block:: json

   {
      "$schema": "https://json-schema.org/draft/2019-09/schema",
      "type": "object",
      "title": "Analysis Laboratory Schema",
      "required": [
         "name",
         "abbreviation",
         "ror"
      ],
      "properties": {
         "name": {
               "type": "string",
               "examples": [
                  "University of Arizona"
               ]
         },
         "abbreviation": {
               "type": "string",
               "examples": [
                  "UAZ"
               ]
         },
         "ror": {
               "type": "string",
               "examples": [
                  "https://ror.org/03m2x1q45"
               ]
         }
      },
      "examples": [{
         "name": "University of Arizona",
         "abbreviation": "UAZ",
         "ror": "https://ror.org/03m2x1q45"
      }]
   }

   .. note::
   The schemas showed here are all based on the product.yaml from a SAMIS's presentation. They will be updated once we have SAMIS final specification in site.
   