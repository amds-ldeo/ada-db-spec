Record Deletion
====================

Delete a row from the referenced/parent table will also automatically delete the referencing rows from the child tables by using **DELETE CASCADE** option in Postgres on `related constraints <https://schema.astromat.org/ada/constraints.html>`_ .

Convention
~~~~~~~~~~~~~

  * **Parent table**
  
    * ``records``

  * **child table**
  
    * ``record_contributors``
    * ``record_creators``
    * ``record_files``
    * ``record_fundings``
    * ``record_licenses``
    * ``record_subjects``
    * ``record_trails``