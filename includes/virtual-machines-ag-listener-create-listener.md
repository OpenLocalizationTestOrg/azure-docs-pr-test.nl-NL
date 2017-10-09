<span data-ttu-id="9f593-101">In deze stap moet u handmatig Hallo beschikbaarheidsgroep-listener in Failoverclusterbeheer en SQL Server Management Studio maken.</span><span class="sxs-lookup"><span data-stu-id="9f593-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="9f593-102">Open Failoverclusterbeheer op Hallo-knooppunt dat als host fungeert voor de primaire replica Hallo.</span><span class="sxs-lookup"><span data-stu-id="9f593-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="9f593-103">Selecteer Hallo **netwerken** knooppunt en Opmerking Hallo clusternetwerknaam.</span><span class="sxs-lookup"><span data-stu-id="9f593-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="9f593-104">Deze naam wordt gebruikt in de variabele Hallo $ClusterNetworkName in Hallo PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="9f593-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="9f593-105">Hallo clusternaam uitvouwen en klik vervolgens op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="9f593-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="9f593-106">In Hallo **rollen** deelvenster, klik met de rechtermuisknop Hallo beschikbaarheidsgroep naam en selecteert u vervolgens **Resource toevoegen** > **Client Access Point**.</span><span class="sxs-lookup"><span data-stu-id="9f593-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Toevoegen van Client Access Point voor de beschikbaarheidsgroep](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="9f593-108">In Hallo **naam** vak, een naam op voor deze nieuwe listener te maken, klikt u op **volgende** tweemaal, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="9f593-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="9f593-109">Worden niet weergegeven in Hallo listener of bron online op dit moment.</span><span class="sxs-lookup"><span data-stu-id="9f593-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="9f593-110">Klik op Hallo **Resources** tabblad uit en vouw vervolgens Hallo clienttoegangspunt u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9f593-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="9f593-111">Hallo IP-adres resource voor elk clusternetwerk in het cluster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9f593-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="9f593-112">Als dit een Azure-only-oplossing, wordt slechts één IP-adres resource wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9f593-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="9f593-113">Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="9f593-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="9f593-114">een hybride oplossing tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="9f593-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="9f593-115">a.</span><span class="sxs-lookup"><span data-stu-id="9f593-115">a.</span></span> <span data-ttu-id="9f593-116">Hallo IP-adres resource die overeenkomt met tooyour lokale subnet met de rechtermuisknop en selecteer vervolgens **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="9f593-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="9f593-117">Houd er rekening mee naam Hallo IP-adres- en netwerknaambronnen.</span><span class="sxs-lookup"><span data-stu-id="9f593-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="9f593-118">b.</span><span class="sxs-lookup"><span data-stu-id="9f593-118">b.</span></span> <span data-ttu-id="9f593-119">Selecteer **statisch IP-adres**, een niet-gebruikte IP-adres toewijzen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f593-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="9f593-120">tooconfigure een Azure-only-oplossing:</span><span class="sxs-lookup"><span data-stu-id="9f593-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="9f593-121">a.</span><span class="sxs-lookup"><span data-stu-id="9f593-121">a.</span></span> <span data-ttu-id="9f593-122">Met de rechtermuisknop op Hallo IP-adres resource die overeenkomt met tooyour Azure-subnet en selecteer vervolgens **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="9f593-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="9f593-123">Als u online toocome listener hello later mislukt vanwege een conflicterende IP-adres geselecteerd door DHCP, kunt u een geldig statisch IP-adres configureren in dit eigenschappenvenster.</span><span class="sxs-lookup"><span data-stu-id="9f593-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="9f593-124">b.</span><span class="sxs-lookup"><span data-stu-id="9f593-124">b.</span></span> <span data-ttu-id="9f593-125">Hallo in dezelfde **IP-adres** eigenschappenvenster, wijziging Hallo **naam IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="9f593-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="9f593-126">Deze naam wordt gebruikt in de variabele Hallo $IPResourceName Hallo PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="9f593-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="9f593-127">Als uw oplossing meerdere virtuele Azure-netwerken omvat, Herhaal deze stap voor elke IP-resource.</span><span class="sxs-lookup"><span data-stu-id="9f593-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

