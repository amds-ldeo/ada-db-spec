funders
========
The table `licenses <https://schema.astromat.org/ada/tables/funders.html>`_ is to hold different funder information allowed by ADA system.

funders allowed by ADA
-----------------------

============== ============================================= ==================================
funder_abbrev  funder_name                                   funder_url
============== ============================================= ==================================
NASA   	       National Aeronautics and Space Administration https://doi.org/10.13039/100000104
NSF   	       US National Science Foundation      	         https://doi.org/10.13039/100000001
============== ============================================= ==================================

Metadata mappings
-----------------
**schema references**

``datacite``: https://schema.datacite.org/meta/kernel-4.4/

======================= =========================
ADA Column              Datacite property   
======================= =========================
funder_name             datacite:funderName
funder_url              datacite:funderIdentifier
======================= =========================
