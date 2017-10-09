
<span data-ttu-id="d1903-101">U kunt meer informatie over Azure Cosmos DB globale distributiepunten in deze Azure vrijdag video met Scott Hanselman en Principal Engineering Manager Karthik Raman.</span><span class="sxs-lookup"><span data-stu-id="d1903-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="d1903-102">Zie voor meer informatie over hoe globale databasereplicatie in Cosmos DB werkt, [Distribueer gegevens globaal met Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="d1903-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="d1903-103"><a id="addregion"></a>Globale database gebieden met hello Azure-Portal toevoegen</span><span class="sxs-lookup"><span data-stu-id="d1903-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="d1903-104">Azure Cosmos DB is beschikbaar in alle [Azure-regio's] [ azureregions] wereldwijd.</span><span class="sxs-lookup"><span data-stu-id="d1903-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="d1903-105">Na het selecteren van Hallo standaardniveau consistentie voor het account van uw database, koppelt u een of meer regio's (afhankelijk van uw keuze standaard consistentie niveau en globale distributie moet).</span><span class="sxs-lookup"><span data-stu-id="d1903-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="d1903-106">In Hallo [Azure-portal](https://portal.azure.com/), Hallo linkerbalk in, klik op **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="d1903-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="d1903-107">In Hallo **Azure Cosmos DB** blade, selecteer Hallo database account toomodify.</span><span class="sxs-lookup"><span data-stu-id="d1903-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="d1903-108">Klik in de blade Hallo-account op **globaal gegevens repliceren** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="d1903-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="d1903-109">In Hallo **globaal gegevens repliceren** blade Hallo regio's tooadd selecteren of door te klikken op gebieden in kaart Hallo verwijderen en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d1903-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="d1903-110">Er is een kosten tooadding regio's, raadpleegt u Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/documentdb/) of Hallo [Distribueer gegevens globaal met DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d1903-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Hallo gebieden in Hallo kaart tooadd klikt u op of verwijder ze][1]
    
<span data-ttu-id="d1903-112">Als u een tweede regio toevoegt, Hallo **handmatige Failover** optie is ingeschakeld op Hallo **globaal gegevens repliceren** blade in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d1903-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="d1903-113">U kunt dit proces optie tootest Hallo failover gebruiken of Hallo primaire schrijven regio wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d1903-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="d1903-114">Als u een derde regio toevoegt, Hallo **Failover prioriteiten** optie is ingeschakeld op dezelfde blade Hallo zodat u kunt Hallo failover-volgorde voor leesbewerkingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d1903-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="d1903-115">Globale database regio's selecteren</span><span class="sxs-lookup"><span data-stu-id="d1903-115">Selecting global database regions</span></span>
<span data-ttu-id="d1903-116">Er zijn twee algemene scenario's voor het configureren van twee of meer gebieden:</span><span class="sxs-lookup"><span data-stu-id="d1903-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="d1903-117">Lage latentie toegang leveren toodata tooend gebruikers ongeacht waar ze zich hele Hallo wereld bevinden</span><span class="sxs-lookup"><span data-stu-id="d1903-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="d1903-118">Toevoegen van regionale tolerantie voor bedrijfscontinuïteit en herstel na noodgevallen (BCDR)</span><span class="sxs-lookup"><span data-stu-id="d1903-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="d1903-119">Voor gebruikers-leveren lage latentie tooend, wordt aangeraden toodeploy beide toepassing hello en toe te voegen Azure Cosmos DB in regio's Hallo behorend toowhere Hallo toepassing gebruikers zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="d1903-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="d1903-120">BCDR, wordt aangeraden tooadd regio's op basis van Hallo regio paren beschreven in Hallo [zakelijke continuïteit en herstel na noodgevallen (BCDR): Azure-gebieden gekoppeld] [ bcdr] artikel.</span><span class="sxs-lookup"><span data-stu-id="d1903-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
