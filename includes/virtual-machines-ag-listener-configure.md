<span data-ttu-id="02e51-101">Hallo beschikbaarheidsgroep-listener is een IP-adres en het netwerk de naam die SQL Server-beschikbaarheidsgroep luistert op Hallo.</span><span class="sxs-lookup"><span data-stu-id="02e51-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="02e51-102">toocreate hello beschikbaarheidsgroeplistener, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="02e51-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="02e51-103"><a name="getnet"></a>Naam van de clusterbron netwerk Hallo Hallo verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="02e51-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="02e51-104">a.</span><span class="sxs-lookup"><span data-stu-id="02e51-104">a.</span></span> <span data-ttu-id="02e51-105">RDP tooconnect toohello Azure virtuele machine die als host fungeert voor de primaire replica hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02e51-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="02e51-106">b.</span><span class="sxs-lookup"><span data-stu-id="02e51-106">b.</span></span> <span data-ttu-id="02e51-107">Open Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="02e51-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="02e51-108">c.</span><span class="sxs-lookup"><span data-stu-id="02e51-108">c.</span></span> <span data-ttu-id="02e51-109">Selecteer Hallo **netwerken** knooppunt en de opmerking Hallo clusternetwerknaam.</span><span class="sxs-lookup"><span data-stu-id="02e51-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="02e51-110">Gebruik deze naam in Hallo `$ClusterNetworkName` variabele in Hallo PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="02e51-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="02e51-111">In Hallo na installatiekopie Hallo clusternetwerknaam is **Cluster netwerk 1**:</span><span class="sxs-lookup"><span data-stu-id="02e51-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![De clusternetwerknaam](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="02e51-113"><a name="addcap"></a>Hallo clienttoegangspunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="02e51-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="02e51-114">Hallo clienttoegangspunt is Hallo netwerknaam dat toepassingen tooconnect toohello databases in een beschikbaarheidsgroep gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02e51-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="02e51-115">Maak Hallo clienttoegangspunt in Failoverclusterbeheer.</span><span class="sxs-lookup"><span data-stu-id="02e51-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="02e51-116">a.</span><span class="sxs-lookup"><span data-stu-id="02e51-116">a.</span></span> <span data-ttu-id="02e51-117">Hallo clusternaam uitvouwen en klik vervolgens op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="02e51-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="02e51-118">b.</span><span class="sxs-lookup"><span data-stu-id="02e51-118">b.</span></span> <span data-ttu-id="02e51-119">In Hallo **rollen** deelvenster, klik met de rechtermuisknop Hallo beschikbaarheidsgroep naam en selecteert u vervolgens **Resource toevoegen** > **Client Access Point**.</span><span class="sxs-lookup"><span data-stu-id="02e51-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Client Access Point](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="02e51-121">c.</span><span class="sxs-lookup"><span data-stu-id="02e51-121">c.</span></span> <span data-ttu-id="02e51-122">In Hallo **naam** vak, maakt u een naam op voor deze nieuwe listener.</span><span class="sxs-lookup"><span data-stu-id="02e51-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="02e51-123">Hallo-naam voor de nieuwe listener Hallo is Hallo netwerknaam dat toepassingen in SQL Server-beschikbaarheidsgroep Hallo tooconnect toodatabases gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02e51-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="02e51-124">d.</span><span class="sxs-lookup"><span data-stu-id="02e51-124">d.</span></span> <span data-ttu-id="02e51-125">toofinish maken Hallo listener, klikt u op **volgende** tweemaal, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="02e51-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="02e51-126">Worden niet weergegeven in Hallo listener of bron online op dit moment.</span><span class="sxs-lookup"><span data-stu-id="02e51-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="02e51-127"><a name="congroup"></a>Hallo IP-resource voor de beschikbaarheidsgroep Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="02e51-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="02e51-128">a.</span><span class="sxs-lookup"><span data-stu-id="02e51-128">a.</span></span> <span data-ttu-id="02e51-129">Klik op Hallo **Resources** tabblad uit en vouw vervolgens Hallo clienttoegangspunt u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="02e51-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="02e51-130">Hallo clienttoegangspunt is offline.</span><span class="sxs-lookup"><span data-stu-id="02e51-130">hello client access point is offline.</span></span>

   ![Client Access Point](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="02e51-132">b.</span><span class="sxs-lookup"><span data-stu-id="02e51-132">b.</span></span> <span data-ttu-id="02e51-133">Hallo IP-resource met de rechtermuisknop en klik vervolgens op Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="02e51-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="02e51-134">Noteer de naam Hallo van Hallo IP-adres en deze gebruiken in Hallo `$IPResourceName` variabele in Hallo PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="02e51-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="02e51-135">c.</span><span class="sxs-lookup"><span data-stu-id="02e51-135">c.</span></span> <span data-ttu-id="02e51-136">Onder **IP-adres**, klikt u op **statisch IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="02e51-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="02e51-137">Hallo IP-adres instellen als hello hetzelfde adres dat u gebruikt wanneer u Hallo load balancer-adres op Hallo Azure-portal instellen.</span><span class="sxs-lookup"><span data-stu-id="02e51-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![IP-Resource](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="02e51-139"><a name = "dependencyGroup"></a>Maak Hallo SQL Server-beschikbaarheidsgroepresource afhankelijk van het clienttoegangspunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="02e51-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="02e51-140">a.</span><span class="sxs-lookup"><span data-stu-id="02e51-140">a.</span></span> <span data-ttu-id="02e51-141">In Failoverclusterbeheer klikt u op **rollen**, en klik vervolgens op de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="02e51-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="02e51-142">b.</span><span class="sxs-lookup"><span data-stu-id="02e51-142">b.</span></span> <span data-ttu-id="02e51-143">Op Hallo **Resources** tabblad onder **andere Resources**, met de rechtermuisknop op Hallo beschikbaarheid resourcegroep en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="02e51-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="02e51-144">c.</span><span class="sxs-lookup"><span data-stu-id="02e51-144">c.</span></span> <span data-ttu-id="02e51-145">Voeg op het tabblad Afhankelijkheden Hallo Hallo-naam van Hallo client access point (Hallo listener) resource.</span><span class="sxs-lookup"><span data-stu-id="02e51-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![IP-Resource](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="02e51-147">d.</span><span class="sxs-lookup"><span data-stu-id="02e51-147">d.</span></span> <span data-ttu-id="02e51-148">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="02e51-148">Click **OK**.</span></span>

5. <span data-ttu-id="02e51-149"><a name="listname"></a>Hallo-client toegang afhankelijk Hallo IP-adres van bron wijzen.</span><span class="sxs-lookup"><span data-stu-id="02e51-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="02e51-150">a.</span><span class="sxs-lookup"><span data-stu-id="02e51-150">a.</span></span> <span data-ttu-id="02e51-151">In Failoverclusterbeheer klikt u op **rollen**, en klik vervolgens op de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="02e51-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="02e51-152">b.</span><span class="sxs-lookup"><span data-stu-id="02e51-152">b.</span></span> <span data-ttu-id="02e51-153">Op Hallo **Resources** tabblad, met de rechtermuisknop op Hallo client access point bron op onder **servernaam**, en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="02e51-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![IP-Resource](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="02e51-155">c.</span><span class="sxs-lookup"><span data-stu-id="02e51-155">c.</span></span> <span data-ttu-id="02e51-156">Klik op Hallo **afhankelijkheden** tabblad. Controleer of een afhankelijkheid is Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="02e51-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="02e51-157">Als dit niet het geval is, stelt u een afhankelijkheid op Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="02e51-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="02e51-158">Controleer of Hallo IP-adressen hebt of niet als er meerdere resources die worden vermeld, en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="02e51-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="02e51-159">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="02e51-159">Click **OK**.</span></span> 

   ![IP-Resource](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="02e51-161">d.</span><span class="sxs-lookup"><span data-stu-id="02e51-161">d.</span></span> <span data-ttu-id="02e51-162">Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik vervolgens op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="02e51-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="02e51-163">U kunt valideren die Hallo afhankelijkheden juist zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="02e51-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="02e51-164">In Failoverclusterbeheer, gaat u tooRoles, met de rechtermuisknop op het Hallo-beschikbaarheidsgroep, klik op **meer acties**, en klik vervolgens op **Afhankelijkheidsrapport weergeven**.</span><span class="sxs-lookup"><span data-stu-id="02e51-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="02e51-165">Hallo afhankelijkheden juist zijn geconfigureerd, Hallo-beschikbaarheidsgroep is afhankelijk van de netwerknaam Hallo als Hallo netwerknaam is afhankelijk van Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="02e51-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="02e51-166"><a name="setparam"></a>In PowerShell Hallo Clusterparameters zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="02e51-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="02e51-167">a.</span><span class="sxs-lookup"><span data-stu-id="02e51-167">a.</span></span> <span data-ttu-id="02e51-168">Kopieer Hallo volgende PowerShell-script tooone van uw SQL Server-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="02e51-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="02e51-169">Hallo variabelen voor uw omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="02e51-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="02e51-170">b.</span><span class="sxs-lookup"><span data-stu-id="02e51-170">b.</span></span> <span data-ttu-id="02e51-171">Hallo Clusterparameters door Hallo PowerShell-script uitgevoerd op een van de clusterknooppunten Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="02e51-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="02e51-172">Als uw SQL Server-exemplaren in afzonderlijke regio's, moet u toorun Hallo PowerShell-script twee keer.</span><span class="sxs-lookup"><span data-stu-id="02e51-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="02e51-173">Hallo eerst, gebruikt u Hallo `$ILBIP` en `$ProbePort` van Hallo eerste gebied.</span><span class="sxs-lookup"><span data-stu-id="02e51-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="02e51-174">tweede keer Hello, gebruikt u Hallo `$ILBIP` en `$ProbePort` van Hallo tweede regio.</span><span class="sxs-lookup"><span data-stu-id="02e51-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="02e51-175">Hallo clusternetwerknaam en IP-Hallo-resource clusternaam zijn Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="02e51-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
