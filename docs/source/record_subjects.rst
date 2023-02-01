record_subjects
================
The table `record_subjects <https://schema.astromat.org/ada/tables/record_subjects.html>`_ is to hold unambiguous subjects related to the record.

It is used with table ``subject_schemes`` to store more scientific metadata related to the ``record``, etc. SAMIS data product.

**term conventions**

Mandatory (**M**)
  The property must always be present in the metadata. An empty value for the property is not allowed.

Mandatory if Applicable (**MA**)
  When the property value can be obtained it must be present.

Recommended (R)
  The use of the property is recommended.

Optional (O)
  It is not important whether the property is used or not, but if used it may provide complementary information about the resource


subject_scheme_id (M)
---------------------

* :ref:`ada:subjectSchemeName`

subject (M)
-----------