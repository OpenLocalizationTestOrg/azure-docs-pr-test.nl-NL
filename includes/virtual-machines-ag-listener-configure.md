Hallo beschikbaarheidsgroep-listener is een IP-adres en het netwerk de naam die SQL Server-beschikbaarheidsgroep luistert op Hallo. toocreate hello beschikbaarheidsgroeplistener, Hallo te volgen:

1. <a name="getnet"></a>Naam van de clusterbron netwerk Hallo Hallo verkrijgen.

    a. RDP tooconnect toohello Azure virtuele machine die als host fungeert voor de primaire replica hello gebruiken. 

    b. Open Failoverclusterbeheer.

    c. Selecteer Hallo **netwerken** knooppunt en de opmerking Hallo clusternetwerknaam. Gebruik deze naam in Hallo `$ClusterNetworkName` variabele in Hallo PowerShell-script. In Hallo na installatiekopie Hallo clusternetwerknaam is **Cluster netwerk 1**:

   ![De clusternetwerknaam](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Hallo clienttoegangspunt toevoegen.  
    Hallo clienttoegangspunt is Hallo netwerknaam dat toepassingen tooconnect toohello databases in een beschikbaarheidsgroep gebruiken. Maak Hallo clienttoegangspunt in Failoverclusterbeheer.

    a. Hallo clusternaam uitvouwen en klik vervolgens op **rollen**.

    b. In Hallo **rollen** deelvenster, klik met de rechtermuisknop Hallo beschikbaarheidsgroep naam en selecteert u vervolgens **Resource toevoegen** > **Client Access Point**.

   ![Client Access Point](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. In Hallo **naam** vak, maakt u een naam op voor deze nieuwe listener. 
   Hallo-naam voor de nieuwe listener Hallo is Hallo netwerknaam dat toepassingen in SQL Server-beschikbaarheidsgroep Hallo tooconnect toodatabases gebruiken.
   
    d. toofinish maken Hallo listener, klikt u op **volgende** tweemaal, en klik vervolgens op **voltooien**. Worden niet weergegeven in Hallo listener of bron online op dit moment.

3. <a name="congroup"></a>Hallo IP-resource voor de beschikbaarheidsgroep Hallo configureren.

    a. Klik op Hallo **Resources** tabblad uit en vouw vervolgens Hallo clienttoegangspunt u hebt gemaakt.  
    Hallo clienttoegangspunt is offline.

   ![Client Access Point](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Hallo IP-resource met de rechtermuisknop en klik vervolgens op Eigenschappen. Noteer de naam Hallo van Hallo IP-adres en deze gebruiken in Hallo `$IPResourceName` variabele in Hallo PowerShell-script.

    c. Onder **IP-adres**, klikt u op **statisch IP-adres**. Hallo IP-adres instellen als hello hetzelfde adres dat u gebruikt wanneer u Hallo load balancer-adres op Hallo Azure-portal instellen.

   ![IP-Resource](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Maak Hallo SQL Server-beschikbaarheidsgroepresource afhankelijk van het clienttoegangspunt Hallo.

    a. In Failoverclusterbeheer klikt u op **rollen**, en klik vervolgens op de beschikbaarheidsgroep.

    b. Op Hallo **Resources** tabblad onder **andere Resources**, met de rechtermuisknop op Hallo beschikbaarheid resourcegroep en klik vervolgens op **eigenschappen**. 

    c. Voeg op het tabblad Afhankelijkheden Hallo Hallo-naam van Hallo client access point (Hallo listener) resource.

   ![IP-Resource](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. Klik op **OK**.

5. <a name="listname"></a>Hallo-client toegang afhankelijk Hallo IP-adres van bron wijzen.

    a. In Failoverclusterbeheer klikt u op **rollen**, en klik vervolgens op de beschikbaarheidsgroep. 

    b. Op Hallo **Resources** tabblad, met de rechtermuisknop op Hallo client access point bron op onder **servernaam**, en klik vervolgens op **eigenschappen**. 

   ![IP-Resource](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Klik op Hallo **afhankelijkheden** tabblad. Controleer of een afhankelijkheid is Hallo IP-adres. Als dit niet het geval is, stelt u een afhankelijkheid op Hallo IP-adres. Controleer of Hallo IP-adressen hebt of niet als er meerdere resources die worden vermeld, en afhankelijkheden. Klik op **OK**. 

   ![IP-Resource](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik vervolgens op **Online brengen**. 

    >[!TIP]
    >U kunt valideren die Hallo afhankelijkheden juist zijn geconfigureerd. In Failoverclusterbeheer, gaat u tooRoles, met de rechtermuisknop op het Hallo-beschikbaarheidsgroep, klik op **meer acties**, en klik vervolgens op **Afhankelijkheidsrapport weergeven**. Hallo afhankelijkheden juist zijn geconfigureerd, Hallo-beschikbaarheidsgroep is afhankelijk van de netwerknaam Hallo als Hallo netwerknaam is afhankelijk van Hallo IP-adres. 


6. <a name="setparam"></a>In PowerShell Hallo Clusterparameters zijn ingesteld.
    
    a. Kopieer Hallo volgende PowerShell-script tooone van uw SQL Server-exemplaren. Hallo variabelen voor uw omgeving bijwerken.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Hallo Clusterparameters door Hallo PowerShell-script uitgevoerd op een van de clusterknooppunten Hallo instellen.  

    > [!NOTE]
    > Als uw SQL Server-exemplaren in afzonderlijke regio's, moet u toorun Hallo PowerShell-script twee keer. Hallo eerst, gebruikt u Hallo `$ILBIP` en `$ProbePort` van Hallo eerste gebied. tweede keer Hello, gebruikt u Hallo `$ILBIP` en `$ProbePort` van Hallo tweede regio. Hallo clusternetwerknaam en IP-Hallo-resource clusternaam zijn Hallo dezelfde. 
