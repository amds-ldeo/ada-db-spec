Generate metadata compliant with Datacite requirements
========================================================

**schema references**

``datacite``: https://schema.datacite.org/meta/kernel-4.4/


datacite:creator (M)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The view `view_datacite_creators <https://schema.astromat.org/ada/tables/view_datacite_creators.html>`_ is to create JSON object with datacite required metadata for creator based on datacite metadata schema.


+-----------+----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| record_id | name_entity_id | creator                                                                                                                                                                                |
+===========+================+========================================================================================================================================================================================+
| 1         | 1              | {"name": "JI, PENG", "nameType": "Personal", "givenName": "PENG", "familyName": "JI", "nameIdentifiers": [{"nameIdentifier": "0000-0003-1868-5004", "nameIdentifierScheme": "ORCID"}]} |
+-----------+----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+



datacite:contributor (R)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The view `view_datacite_contributors <https://schema.astromat.org/ada/tables/view_datacite_contributors.html>`_ is to create JSON object with datacite required metadata for contributor based on datacite metadata schema.

+-----------+----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| record_id | name_entity_id | contributor                                                                                                                                                                      |
+===========+================+==================================================================================================================================================================================+
| 1         | 2              | {"name": "JI, test1", "nameType": "Personal", "contributorType": "RelatedPerson", "nameIdentifiers": []}                                                                         |
+-----------+----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 1         | 3              | {"name": "JI, test2", "nameType": "Personal", "contributorType": "DataCurator", "nameIdentifiers": [{"nameIdentifier": "0000-0003-1868-5005", "nameIdentifierScheme": "ORCID"}]} |
+-----------+----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 1         | 4              | {"name": "SAMIS", "nameType": "Organizational", "contributorType": "RightsHolder", "nameIdentifiers": [{"nameIdentifier": "027ka1x80", "nameIdentifierScheme": "ROR"}]}          |
+-----------+----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
