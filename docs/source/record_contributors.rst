record_contributors
====================
The table `record_contributors <https://schema.astromat.org/ada/tables/record_contributors.html>`_ is to hold contributors of the digital resources.

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


contributor_type (M)
--------------------

datacite:contributorType

Allowed value
  
  * ``ContactPerson``
  * ``DataCollector``
  * ``DataCurator``
  * ``DataManager``
  * ``Distributor``
  * ``Editor``
  * ``HostingInstitution``
  * ``Producer``
  * ``ProjectLeader``
  * ``ProjectManager``
  * ``ProjectMember``
  * ``RegistrationAgency``
  * ``RegistrationAuthority``
  * ``RelatedPerson``
  * ``Researcher``
  * ``ResearchGroup``
  * ``RightsHolder``
  * ``Sponsor``
  * ``Supervisor``
  * ``WorkPackageLeader``
  * ``Other``
