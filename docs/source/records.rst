records
========
The table `records <https://schema.astromat.org/ada/tables/records.html>`_ is to hold unambiguous digital resources, etc. dataset.

**term conventions**

Mandatory (**M**)
  The property must always be present in the metadata. An empty value for the property is not allowed.

Mandatory if Applicable (**MA**)
  When the property value can be obtained it must be present.

Recommended (R)
  The use of the property is recommended.

Optional (O)
  It is not important whether the property is used or not, but if used it may provide complementary information about the resource

**schema reference**

``samis``: https://osiris-rex.atlassian.net/wiki/spaces/SDPD/pages/449544195/Bundle+Delivery+Documents+BDD

``datacite``: https://schema.datacite.org/meta/kernel-4.4/

.. note::

   Each row in the table ``records`` represent an unique SAMIS Data product.


title (M)
-----------------

datacite:title (M)

samis:dataProduct:title

Example (datacite)
~~~~~~~~~~~~~~~~~~~
.. code-block:: json

  "titles": [
    {
      "title": "SAMIS data product title.",
    }
  ]

.. _ada:recordGeneralType:

general_type (M)
-----------------------

datacite:resourceTypeGeneral (M)

general_types allowed by ADA are part of datacite resourceTypeGeneral controlled list:

* ``Collection``
* ``Dataset``
* ``Event``
* ``Image``
* ``InteractiveResource``
* ``Model``
* ``PhysicalObject``
* ``Service``
* ``Software``
* ``Text``
* ``Workflow``
* ``Other``


.. note::
   It has default value ``Dataset``, don't need to populate for SAMIS data product.

specific_type (M)
-----------------------

datacite:resourceType (M)

samis:dataProductType

Example (datacite)
~~~~~~~~~~~~~~~~~~~
.. code-block:: json

  "types": [
    {
      "resourceType": "EMPA Secondary Electron Image",
      "resourceTypeGeneral": "Dataset"
    }
  ]

description (MA)
-----------------------

datacite:description (R)

samis:dataProduct:abstract

Example (datacite)
~~~~~~~~~~~~~~~~~~~
.. code-block:: json

  "descriptions": [
    {
      "description": "SAMIS data product abstract.",
      "descriptionType": "Abstract"
    }
  ]

record_doi (MA)
-----------------------

It must be populated once the doi is assigned by datacite.

.. _ada:doiStatus:

doi_status (MA)
-----------------------

Specify `the states of DOI <https://support.datacite.org/docs/doi-states>`_ assigned by datacite. It must be populated with one of the following controlled list once the doi is assigned by datacite.

* ``Draft``
* ``Findable``

doi_issued_date (MA)
-----------------------

It represent the date that the doi is assigned by datacite, must be populated with the format ``YYYY-MM-DD``.

Example
~~~~~~~
.. code-block:: sql

   UPDATE records SET doi_issued_date = '2023-01-31';

days_until_release (M)
-----------------------
Indicate how many days after ``doi_status`` is changed to ``Findable`` the resource, especially associated data files are publicly accessiable and downloadable. The default value is 0 means both record's metadata and associated data files are publicly accessiable and downloadable once the state of DOI is set to ``Findable``.

.. _ada:submissionType:

submission_type (M)
-----------------------

* ``Regular`` (default): Indicate the record was submitted by an individual
* ``BundleDelivery``: Indicate the record was submitted by SAMIS

.. _ada:processStatus:

process_status (M)
-----------------------

* ``Accepted`` (default): A new record is created in ADA.
* ``Submitted``: The record is submitted by user for review when have finished uploading data files and filling in all required metadata. 
* ``InReview``
* ``Published``
* ``Rejected``
* ``Archived``