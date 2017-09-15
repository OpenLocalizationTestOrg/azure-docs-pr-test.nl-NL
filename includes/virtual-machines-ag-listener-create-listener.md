<span data-ttu-id="90639-101">In deze stap moet u handmatig de beschikbaarheidsgroeplistener in Failoverclusterbeheer en SQL Server Management Studio maken.</span><span class="sxs-lookup"><span data-stu-id="90639-101">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="90639-102">Open Failoverclusterbeheer vanuit het knooppunt dat als host fungeert voor de primaire replica.</span><span class="sxs-lookup"><span data-stu-id="90639-102">Open Failover Cluster Manager from the node that hosts the primary replica.</span></span>

2. <span data-ttu-id="90639-103">Selecteer de **netwerken** knooppunt en de clusternetwerknaam opmerking.</span><span class="sxs-lookup"><span data-stu-id="90639-103">Select the **Networks** node, and then note the cluster network name.</span></span> <span data-ttu-id="90639-104">Deze naam wordt gebruikt in de variabele $ClusterNetworkName in het PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="90639-104">This name is used in the $ClusterNetworkName variable in the PowerShell script.</span></span>

3. <span data-ttu-id="90639-105">De clusternaam uitvouwen en klik vervolgens op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="90639-105">Expand the cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="90639-106">In de **rollen** deelvenster met de rechtermuisknop op de naam van de beschikbaarheidsgroep en selecteer vervolgens **Resource toevoegen** > **Client Access Point**.</span><span class="sxs-lookup"><span data-stu-id="90639-106">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Toevoegen van Client Access Point voor de beschikbaarheidsgroep](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="90639-108">In de **naam** vak, een naam op voor deze nieuwe listener te maken, klikt u op **volgende** tweemaal, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="90639-108">In the **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="90639-109">Worden niet weergegeven in de listener of de bron online op dit moment.</span><span class="sxs-lookup"><span data-stu-id="90639-109">Do not bring the listener or resource online at this point.</span></span>

6. <span data-ttu-id="90639-110">Klik op de **Resources** tabblad uit en vouw vervolgens het clienttoegangspunt dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="90639-110">Click the **Resources** tab, and then expand the client access point you just created.</span></span> 
    <span data-ttu-id="90639-111">De bron van de IP-adres voor elke clusternetwerk in het cluster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="90639-111">The IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="90639-112">Als dit een Azure-only-oplossing, wordt slechts één IP-adres resource wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="90639-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="90639-113">Voer een van de volgende bewerkingen uit:</span><span class="sxs-lookup"><span data-stu-id="90639-113">Do either of the following:</span></span>
   
   * <span data-ttu-id="90639-114">Een hybride oplossing configureren:</span><span class="sxs-lookup"><span data-stu-id="90639-114">To configure a hybrid solution:</span></span>
     
        <span data-ttu-id="90639-115">a.</span><span class="sxs-lookup"><span data-stu-id="90639-115">a.</span></span> <span data-ttu-id="90639-116">Met de rechtermuisknop op de bron van IP-adres dat overeenkomt met het lokale subnet en selecteer vervolgens **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="90639-116">Right-click the IP address resource that corresponds to your on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="90639-117">Noteer de naam IP-adres en de netwerknaam.</span><span class="sxs-lookup"><span data-stu-id="90639-117">Note the IP address name and network name.</span></span>
   
        <span data-ttu-id="90639-118">b.</span><span class="sxs-lookup"><span data-stu-id="90639-118">b.</span></span> <span data-ttu-id="90639-119">Selecteer **statisch IP-adres**, een niet-gebruikte IP-adres toewijzen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="90639-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="90639-120">Een Azure-only-oplossing configureren:</span><span class="sxs-lookup"><span data-stu-id="90639-120">To configure an Azure-only solution:</span></span>

        <span data-ttu-id="90639-121">a.</span><span class="sxs-lookup"><span data-stu-id="90639-121">a.</span></span> <span data-ttu-id="90639-122">Met de rechtermuisknop op de bron van IP-adres dat overeenkomt met uw Azure-subnet en selecteer vervolgens **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="90639-122">Right-click the IP address resource that corresponds to your Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="90639-123">Als de listener later mislukt on line vanwege een conflicterende IP-adres geselecteerd door DHCP, kunt u een geldig statisch IP-adres configureren in dit eigenschappenvenster.</span><span class="sxs-lookup"><span data-stu-id="90639-123">If the listener later fails to come online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="90639-124">b.</span><span class="sxs-lookup"><span data-stu-id="90639-124">b.</span></span> <span data-ttu-id="90639-125">In dezelfde **IP-adres** wijziging van het eigenschappenvenster de **naam IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="90639-125">In the same **IP Address** properties window, change the **IP Address Name**.</span></span>  
        <span data-ttu-id="90639-126">Deze naam wordt gebruikt in de variabele $IPResourceName van het PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="90639-126">This name is used in the $IPResourceName variable of the PowerShell script.</span></span> <span data-ttu-id="90639-127">Als uw oplossing meerdere virtuele Azure-netwerken omvat, Herhaal deze stap voor elke IP-resource.</span><span class="sxs-lookup"><span data-stu-id="90639-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

