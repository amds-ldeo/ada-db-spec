Lifecycle of the record
========================

1. Record creation process
------------------------

* 1.1 SAMIS send request ``create record`` to ADA API endpoint with minimum metadata requirement(title)

.. code-block:: json

   {
     "title": "create a samis record in ADA",
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

* 1.3 ADA API excute ``create operation`` on table ``records`` of ADA database

.. code-block:: sql

   insert into records(title, submission_type, doi, doi_status, doi_issued_date) values('create a samis record in ADA','BundleDelivery','10.5438/0012','Draft','2016-09-19') returing *;

The record created like below

+----+------------------------------+-------------+-----------------+--------------+---------------+--------------+--------------------+-----------------+------------+----------------+-------------------------+-------------------------+
| id | title                        | description | submission_type | general_type | specific_type | doi          | days_until_release | doi_issued_date | doi_status | process_status | created_at              | updated_at              |
+====+==============================+=============+=================+==============+===============+==============+====================+=================+============+================+=========================+=========================+
| 1  | create a samis record in ADA |             | BundleDelivery  | Dataset      |               | 10.5438/0012 | 0                  | 2016-09-19      | Draft      | Accepted       | 2023-02-13 10:20:38.372 | 2023-02-13 10:20:38.372 |
+----+------------------------------+-------------+-----------------+--------------+---------------+--------------+--------------------+-----------------+------------+----------------+-------------------------+-------------------------+

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

* 2.6 ADA ? endpoint execute ``update operation`` on table ``records`` of ADA database with response from datacite, change ``process_status`` to ``Published``  and send back to SAMIS