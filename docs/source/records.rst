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

doi_status (MA)
-----------------------

Specify the states of DOI assigned by datacite. It must be populated with one of the following controlled list once the doi is assigned by datacite.

* ``Draft``
* ``Findable``

doi_issued_date (MA)
-----------------------

It represent the date that the doi is assigned by datacite, must be populated with the format ``YYYY-MM-DD`` once the doi is assigned by datacite.

Example
~~~~~~~
.. code-block:: sql

   UPDATE records SET doi_issued_date = '2023-01-31';

publication_date (MA)
-----------------------
datacite:date (R) with datacite:dateType:Available

The format is ``YYYY-MM-DD``, should be populated with the value of column ``updated_at`` when doi_status is changed to ``Findable`` if user does not provide it.

Example (datacite)
~~~~~~~~~~~~~~~~~~~
.. code-block:: json

  "dates": [
    {
      "date": "2023-01-30",
      "dateType": "Available"
    },
  ]