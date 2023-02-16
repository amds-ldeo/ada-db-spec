record_creators
====================
The table `record_creators <https://schema.astromat.org/ada/tables/record_creators.html>`_ is to hold creators of the record.

Definition and Usage Instruction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
A creator is someone who creates and maintains a record. Every record must have at least one creator. Each creator must provide ORCID and email.

Generate a creator of the record
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    * 1 Check if the person exist in ADA

      .. code-block:: sql

        select * from v_name_entities where identifier_type='ORCID' and identifier='0000-0003-1868-5004' returing *
    
    * 2 The person does not exist

        * 2.1 Create name tag for the person in the table name_entities
       
        .. code-block:: sql

            insert into name_entities(full_name, family_name, given_name) values ('JI, PENG', 'JI', 'PENG') returning id;
       
        * 2.2 Add ORCID and email of the person in the table name_entity_identifiers

        .. code-block:: sql

            insert into name_entity_identifiers(name_entity_id, external_identifier_scheme_id, identifier) values (1, 2, '0000-0003-1868-5004'), (1, 5, 'pengji@ldeo.columbia.edu') returning *;

        * 2.3 Create relationship between the person and the record in the table record_creators
        
        .. code-block:: sql

            insert into record_creators(record_id, name_entity_id) values (1, 1) returning *;
    
    * 3 The person exist

        * 3.1 Create relationship between the person and the record in the table record_creators
        
        .. code-block:: sql

            insert into record_creators(record_id, name_entity_id) values (1, 1) returning *;