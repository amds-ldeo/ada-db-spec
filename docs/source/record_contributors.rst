record_contributors
====================
The table `record_contributors <https://schema.astromat.org/ada/tables/record_contributors.html>`_ is to hold contributors of the record.

Definition and Usage Instruction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The definition of contributor in ADA is same as `Datacite <https://support.datacite.org/docs/datacite-metadata-schema-v44-recommended-and-optional-properties#7-contributor>`_. Every record can have one or multiple contributors, or no contributor at all. Each contributor can have identifier (ORCID, ROR, email), or no identifier at all.

Generate a contributor of the record
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    * 1 Check if the person/institution exist in ADA

      .. code-block:: sql

        select * from v_name_entities where identifier_type='ORCID' and identifier='0000-0003-1868-5004' returing *
      
      Or,

      .. code-block:: sql

        select * from v_name_entities where identifier_type='ROR' and identifier='027ka1x80' returing *
    
    * 2 The person/institution does not exist

        * 2.1 Create name tag for the person/institution in the table name_entities
       
        .. code-block:: sql

            insert into name_entities(full_name, family_name, given_name) values ('JI, PENG', 'JI', 'PENG') returning id;
        
        Or,

        .. code-block:: sql

            insert into name_entities(full_name, name_type) values ('SAMIS', 'Organizational') returning id;
       
        * 2.2 Add identifiers of the person/institution in the table name_entity_identifiers if have

        .. code-block:: sql

            insert into name_entity_identifiers(name_entity_id, external_identifier_scheme_id, identifier) values (1, 2, '0000-0003-1868-5004'), (1, 5, 'pengji@ldeo.columbia.edu') returning *;
        
        Or,

        .. code-block:: sql

            insert into name_entity_identifiers(name_entity_id, external_identifier_scheme_id, identifier) values (4, 3, '027ka1x80') returning *;

        * 2.3 Create relationship between the person/institution and the record in the table record_contributors
        
        .. code-block:: sql

            insert into record_creators(record_id, name_entity_id,contributor_type) values (1, 1,'DataCurator') returning *;
    
    * 3 The person/institution exist

        * 3.1 Create relationship between the person and the record in the table record_creators
        
        .. code-block:: sql

            insert into record_creators(record_id, name_entity_id,contributor_type) values (1, 1,'DataCurator') returning *;

**schema references**

``datacite``: https://schema.datacite.org/meta/kernel-4.4/

.. _ada:contributorType:

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
