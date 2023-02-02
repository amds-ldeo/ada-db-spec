name_entities
=============
The table `name_entities <https://schema.astromat.org/ada/tables/name_entities.html>`_ is to hold different funder information allowed by ADA system.

**term conventions**

Mandatory (**M**)
  The property must always be present in the metadata. An empty value for the property is not allowed.

Mandatory if Applicable (**MA**)
  When the property value can be obtained it must be present.

Recommended (R)
  The use of the property is recommended.

Optional (O)
  It is not important whether the property is used or not, but if used it may provide complementary information about the resource

**schema references**

``datacite``: https://schema.datacite.org/meta/kernel-4.4/

.. _ada:nameType:

name_type (M)
--------------

datacite:nameType

Allowed value
  
  * ``Personal`` (default)

  * ``Orgnizational``

Usage

  * The column ``full_name``, ``family_name`` and ``given_name`` need to be populated if ``name_type`` is ``Personal``.

  * Only the column ``full_name`` need to be populated if ``name_type`` is set to ``Orgnizational``.
