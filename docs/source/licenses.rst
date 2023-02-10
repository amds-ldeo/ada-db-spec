licenses
========
The table `licenses <https://schema.astromat.org/ada/tables/licenses.html>`_ is to hold different license information allowed by ADA system.

Licenses allowed by ADA
-----------------------
All licenses are seleted from `SPDX License List <https://spdx.org/licenses/>`_

======================= ============================================================================= ============================================
abbreviation            name                                                                          url
======================= ============================================================================= ============================================
CC-BY-NC-SA-3.0   	   Creative Commons Attribution-NonCommercial-Share Alike 3.0 United States 	   https://spdx.org/licenses/CC-BY-SA-4.0
CC-BY-NC-SA-4.0   	   Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International      	https://spdx.org/licenses/CC-BY-NC-SA-4.0
CC-BY-SA-4.0  	         Creative Commons Attribution-ShareAlike 4.0 International	                  https://spdx.org/licenses/CC-BY-SA-4.0
CC0-1.0  	            Creative Commons Zero v 1.0 Universal	                                       https://spdx.org/licenses/CC0-1.0
CC-BY-4.0  	            Creative Commons Attribution 4.0 International	                              https://spdx.org/licenses/CC-BY-4.0
======================= ============================================================================= ============================================

Metadata mappings
-----------------
**schema references**

``datacite``: https://schema.datacite.org/meta/kernel-4.4/

======================= =======================
ADA Column              Datacite property   
======================= =======================
abbreviation            datacite:rightsIdentifier
name                    datacite:Rights
url                     datacite:rightsURI
======================= =======================

Example (datacite)
~~~~~~~~~~~~~~~~~~~~~
.. code-block:: json

  "rightsList": [
    {
      "rightsIdentifier":"CC-BY-SA-4.0",
      "rights": "Creative Commons Attribution-ShareAlike 4.0 International",
      "rightsUri": "https://spdx.org/licenses/CC-BY-SA-4.0"
    }
  ]