
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="e942b-101">toosave kosten, u kunt onderbreken en hervatten compute-bronnen op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e942b-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="e942b-102">Bijvoorbeeld als u niet Hallo database tijdens nacht hello en in het weekend gebruikt, kunt u tijdens de tijdstippen onderbreken en hervatten tijdens Hallo dag.</span><span class="sxs-lookup"><span data-stu-id="e942b-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="e942b-103">U geen afgeschreven voor dwu's tijdens het Hallo-database is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="e942b-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="e942b-104">Wanneer u een database onderbreken:</span><span class="sxs-lookup"><span data-stu-id="e942b-104">When you pause a database:</span></span>

* <span data-ttu-id="e942b-105">Reken-en geheugenbronnen worden toohello pool van beschikbare resources in het datacenter Hallo geretourneerd</span><span class="sxs-lookup"><span data-stu-id="e942b-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="e942b-106">DWU-kosten zijn nul gedurende Hallo Hallo onderbreken.</span><span class="sxs-lookup"><span data-stu-id="e942b-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="e942b-107">Opslag van gegevens wordt niet beïnvloed en uw gegevens intact blijven.</span><span class="sxs-lookup"><span data-stu-id="e942b-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="e942b-108">SQL Data Warehouse annuleert alle bewerkingen voor actieve of in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="e942b-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

