Lifecycle of the record
========================

.. note::
  Suitable for both conventional and SAMIS scenarios

1. Record creation process
------------------------

* 1.1 User send request ``create record`` to ADA API endpoint with minimum metadata requirement(title, submissionType, creators)

The JSON schema of minimum metadata for record creation

.. code-block:: json

  {
      "$schema": "https://json-schema.org/draft/2019-09/schema",
      "type": "object",
      "title": "Minimum metadata for record creation",
      "required": [
          "title",
          "submissionType",
          "creators"
      ],
      "properties": {
          "title": {
              "type": "string"
          },
          "submissionType": {
              "type": "string",
              "enum": [
                  "Regular",
                  "BundleDelivery"
              ]
          },
          "creators": {
              "type": "array",
              "items": {
                  "type": "object",
                  "required": [
                      "name",
                      "nameType",
                      "ORCID",
                      "email"
                  ],
                  "properties": {
                      "name": {
                          "type": "string"
                      },
                      "nameType": {
                          "type": "string",
                          "enum": [
                              "Personal",
                              "Organizational"
                          ]
                      },
                      "ORCID": {
                          "type": "string"
                      },
                      "email": {
                          "type": "string"
                      }
                  }
              },
              "minItems": 1,
              "uniqueItems": true
          }
      }
  }

The example of minimum metadata 

.. code-block:: json

   {
     "title": "create a samis record in ADA",
     "submissionType": "BundleDelivery",
     "creators" : [
         {
            "name": "JI, PENG",
            "nameType": "Personal",
            "ORCID": "0000-0003-1868-5004",
            "email": "pengji@ldeo.columbia.edu"
         }
     ]
   }

* 1.2 ADA API endpoint send request ``create draft record`` to datacite API endpoint and get the responding from datacite looks like below(partial), find full example at https://support.datacite.org/docs/api-create-dois

.. code-block:: json

   {
     "data": {
       "id": "10.5438/0012",
       "type": "dois",
       "attributes": {
         "doi": "10.5438/0012",
         "prefix": "10.5438",
         "suffix": "0012",
         "state": "draft",
         "created": "2016-09-19T21:53:56.000Z",
       },
     },
   }

* 1.3 ADA API ingest data into ADA database

  * 1.3.1 Excute ``create operation`` on table ``records``

  .. code-block:: sql

    insert into records(title, submission_type, doi, doi_status, doi_issued_date) values('create a samis record in ADA','BundleDelivery','10.5438/0012','Draft','2016-09-19') returing *;

  The record created like below

  +----+------------------------------+-------------+-----------------+--------------+---------------+--------------+--------------------+-----------------+------------+----------------+-------------------------+-------------------------+
  | id | title                        | description | submission_type | general_type | specific_type | doi          | days_until_release | doi_issued_date | doi_status | process_status | created_at              | updated_at              |
  +====+==============================+=============+=================+==============+===============+==============+====================+=================+============+================+=========================+=========================+
  | 1  | create a samis record in ADA |             | BundleDelivery  | Dataset      |               | 10.5438/0012 | 0                  | 2016-09-19      | Draft      | Accepted       | 2023-02-13 10:20:38.372 | 2023-02-13 10:20:38.372 |
  +----+------------------------------+-------------+-----------------+--------------+---------------+--------------+--------------------+-----------------+------------+----------------+-------------------------+-------------------------+

  * 1.3.2 Ingest creator infomation into ADA database
    * 1.3.2.1 Excute ``read operation`` on view ``v_name_entities``

    .. code-block:: sql
      select * from v_name_entities where identifier_type='ORCID' and identifier='0000-0003-1868-5004'
    
    * 1.3.2.2 Excute ``create operation`` on table ``name_entities`` if the person does not exist in ADA database

    .. code-block:: sql

      insert into name_entities(full_name, family_name, given_name) values ('JI, PENG', 'JI', 'PENG') returning *;

    The row created like below

    +----+-----------+-----------+-------------+------------+-------------------------+-------------------------+
    | id | full_name | name_type | family_name | given_name | created_at              | updated_at              |
    +====+===========+===========+=============+============+=========================+=========================+
    | 1  | JI, PENG  | Personal  | JI          | PENG       | 2023-02-14 08:59:01.568 | 2023-02-14 08:59:01.568 |
    +----+-----------+-----------+-------------+------------+-------------------------+-------------------------+

    * 1.3.2.3 Excute ``create operation`` on table ``name_entity_identifiers`` 

    .. code-block:: sql

      insert into name_entity_identifiers(name_entity_id, external_identifier_scheme_id, identifier) values (1, 2, '0000-0003-1868-5004'), (1, 5, 'pengji@ldeo.columbia.edu') returning *;

    The row created like below

    +----+----------------+-------------------------------+--------------------------+-------------------------+-------------------------+
    | id | name_entity_id | external_identifier_scheme_id | identifier               | created_at              | updated_at              |
    +====+================+===============================+==========================+=========================+=========================+
    | 1  | 1              | 2                             | 0000-0003-1868-5004      | 2023-02-14 09:09:06.905 | 2023-02-14 09:09:06.905 |
    +----+----------------+-------------------------------+--------------------------+-------------------------+-------------------------+
    | 2  | 1              | 5                             | pengji@ldeo.columbia.edu | 2023-02-14 15:23:40.141 | 2023-02-14 15:23:40.141 |
    +----+----------------+-------------------------------+--------------------------+-------------------------+-------------------------+

    Check view ``v_name_entities`` again, returning like below

    +----+-----------+-----------+-------------+------------+-----------------+--------------------------+
    | id | full_name | name_type | family_name | given_name | identifier_type | identifier               |
    +====+===========+===========+=============+============+=================+==========================+
    | 1  | JI, PENG  | Personal  | JI          | PENG       | ORCID           | 0000-0003-1868-5004      |
    +----+-----------+-----------+-------------+------------+-----------------+--------------------------+
    | 1  | JI, PENG  | Personal  | JI          | PENG       | email           | pengji@ldeo.columbia.edu |
    +----+-----------+-----------+-------------+------------+-----------------+--------------------------+

    * 1.3.2.4 Excute ``create operation`` on table ``record_creators`` 

    .. code-block:: sql

      insert into record_creators(record_id, name_entity_id) values (1, 1) returning *;

    The row created like below

    +----+-----------+----------------+-------------------------+-------------------------+
    | id | record_id | name_entity_id | created_at              | updated_at              |
    +====+===========+================+=========================+=========================+
    | 1  | 1         | 1              | 2023-02-14 09:22:38.372 | 2023-02-14 09:22:38.372 |
    +----+-----------+----------------+-------------------------+-------------------------+

* 1.4 ADA API send record created in ADA back to SAMIS

2. Record submission process
-----------------------------

* 2.1 SAMIS send request ``submit record`` to ADA API endpoint with required metada

.. note::
   Must ensure all relevant files have been uploaded to S3 before sending the request

.. code-block:: json

   {
     "doi": "10.5438/0012",
     "process_status": "Submitted"
   }

* 2.2 ADA API endpoint excute ``update operation`` on table ``records`` of ADA database, change ``process_status`` to ``Submitted`` and send back to SAMIS

.. code-block:: sql
   update records set process_status='Submitted' where doi='10.5438/0012';

* 2.3 SAMIS data validation process is triggered and the ``procss_status`` is changed to ``InReview``
  
  * 2.3.1 if data is not validated, the ``process_status`` is changed to ``Reject``, request ``modify and re-submit`` is sent back to SAMIS
  
  * 2.3.2 if data is validated, metadata extraction process is triggered.

* 2.4 Extraction process ingest required metada into various tables of ADA database

* 2.5 ADA ? endpoint scoop datacite required metadata from ADA database and send it with request ``update doi``, change state to ``findable``

* 2.6 ADA ? endpoint execute ``update operation`` on table ``records`` of ADA database with response from datacite, change ``doi_status`` to ``Findable`` and ``process_status`` to ``Published``, then send back to SAMIS