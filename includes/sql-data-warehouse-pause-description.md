
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
toosave kosten, u kunt onderbreken en hervatten compute-bronnen op aanvraag. Bijvoorbeeld als u niet Hallo database tijdens nacht hello en in het weekend gebruikt, kunt u tijdens de tijdstippen onderbreken en hervatten tijdens Hallo dag. U geen afgeschreven voor dwu's tijdens het Hallo-database is onderbroken.

Wanneer u een database onderbreken:

* Reken-en geheugenbronnen worden toohello pool van beschikbare resources in het datacenter Hallo geretourneerd
* DWU-kosten zijn nul gedurende Hallo Hallo onderbreken.
* Opslag van gegevens wordt niet beïnvloed en uw gegevens intact blijven. 
* SQL Data Warehouse annuleert alle bewerkingen voor actieve of in de wachtrij.

