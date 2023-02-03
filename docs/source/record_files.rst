record_files
================
The table `record_files <https://schema.astromat.org/ada/tables/record_files.html>`_ is to hold metadata of files related to the record.


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

file_name (M)
--------------
samis:dataProduct:manifest:fileName

file_checksum (M)
-----------------
samis:dataProduct:manifest:checksum

.. _ada:recordFileGeneralType:

general_type (MA)
--------------------------------
`samis:DSD <https://osiris-rex.atlassian.net/wiki/spaces/SDPD/pages/449216529/Data+Standards+Documents+DSD>`_

general type allowd by ADA
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* ``Image``

* ``Document``

* ``TabularData``

* ``DataCube``

* ``DataCollection`` 

specific_type (MA)
--------------------------------
samis:dataComponentType