Common Columns
=============
There are two timestamp fields ``created_at`` and ``updated_at`` present in all tables.
Both of them are set to ``NOW()`` defaultly in each table. Each table also has a 
trigger ``set_timestamp`` that will execute the `trigger_set_timestamp<https://schema.astromat.org/ada/routines/trigger_set_timestamp___8ec213b3.html>`_ function 
, which will do so whenever a row is updated in the table. So,both the ``created_at`` and 
``updated_at`` columns will be saved correctly whenever insert and update rows in the table.
And you dont need to populate either the ``created_at`` or ``updated_at`` columns when
insert and update rows in the table.

