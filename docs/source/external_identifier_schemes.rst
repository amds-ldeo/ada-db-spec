external_identifier_schemes
============================
The table `external_identifier_schemes <https://schema.astromat.org/ada/tables/external_identifier_schemes.html>`_ is to hold different identifier schemes allowed by ADA system.

identifier schemes allowed by ADA
---------------------------------

============ =====================
name         url
============ =====================
DOI	         https://doi.org/
ORCID	     https://orcid.org/
ROR	         https://ror.org/
IGSN	     https://igsn.org/
email        
============ =====================

Metadata mappings
-----------------
**schema references**

``datacite``: https://schema.datacite.org/meta/kernel-4.4/

======================= =========================
ADA Column              Datacite property   
======================= =========================
name                    datacite:identifierType/affiliationIdentifierScheme/nameIdentifierScheme
url                     datacite:schemeURI
======================= =========================
