---
title: een externe-Listener voor AlwaysOn-beschikbaarheidsgroepen aaaConfigure | Microsoft Docs
description: Deze zelfstudie helpt u bij de stappen voor het maken van een altijd op beschikbaarheidsgroep-Listener in Azure die extern toegankelijk is via de openbare virtuele IP-adres van Hallo Hallo gekoppelde cloud-service.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Een externe-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure
> [!div class="op_single_selector"]
> * [Interne Listener](../classic/ps-sql-int-listener.md)
> * [Externe-Listener](../classic/ps-sql-ext-listener.md)
> 
> 

Dit onderwerp leest u hoe tooconfigure een listener voor een AlwaysOn-beschikbaarheidsgroep die extern toegankelijk is via internet Hallo. Dit wordt mogelijk gemaakt door Hallo cloudservice te koppelen **openbare virtuele IP-adres (VIP)** adres met Hallo listener.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

De beschikbaarheidsgroep kunt replica's die zich on-premises alleen Azure alleen, of bevatten zowel on-premises en Azure span voor hybride configuraties. Azure replica's kunnen zich bevinden in Hallo dezelfde regio of tussen meerdere regio's met meerdere virtuele netwerken (vnet's). Hallo onderstaande stappen wordt ervan uitgegaan dat u al hebt [geconfigureerd een beschikbaarheidsgroep](../classic/portal-sql-alwayson-availability-groups.md) maar een listener niet hebt geconfigureerd.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Richtlijnen en beperkingen voor externe listeners
Houd er rekening mee Hallo volgen richtlijnen over Hallo beschikbaarheidsgroep-listener in Azure wanneer u implementeert met behulp Hallo cloud service symphysis VIP-adres:

* Hallo beschikbaarheidsgroep-listener wordt ondersteund op Windows Server 2008 R2, Windows Server 2012 en Windows Server 2012 R2.
* Hallo-clienttoepassing moet zich bevinden op een andere cloudservice dan Hallo een bestand met uw virtuele machines van de beschikbaarheidsgroep. Azure biedt geen ondersteuning voor direct server return is met de client en server in Hallo dezelfde cloudservice.
* Standaard Hallo stappen in dit artikel wordt weergegeven hoe tooconfigure één listener toouse Hallo cloud serviceadres virtuele IP-adres (VIP). Het is echter mogelijk tooreserve en meerdere VIP-adressen voor uw cloudservice maken. Hiermee kunt u toouse Hallo stappen in dit artikel toocreate meerdere listeners die elk zijn gekoppeld aan een andere VIP. Voor informatie over hoe toocreate meerdere VIP-adressen, Zie [meerdere VIP's per cloudservice](../../../load-balancer/load-balancer-multivip.md).
* Als u een listener voor een hybride omgeving maken wilt, Hallo on-premises netwerk toohello verbinding moet hebben tot Internet in toevoeging toohello site-naar-site VPN met Hallo virtuele Azure-netwerk. Hallo beschikbaarheidsgroep-listener is in de Azure-subnet hello, bereikbaar alleen voor openbaar IP-adres van de respectieve cloudservice Hallo Hallo.
* Het wordt niet ondersteund in Hallo dezelfde cloudservice waar hebt u ook een interne listener met behulp van een externe-listener toocreate Hallo interne Load Balancer (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Hallo toegankelijkheid van Hallo listener bepalen
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

In dit artikel is gericht op het maken van een listener die gebruikmaakt van **externe load balancing**. Als u een listener die persoonlijke tooyour virtuele netwerk wilt, raadpleegt u Hallo-versie van dit artikel die voorziet in stappen voor het instellen van een [listener met ILB](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>VM-eindpunten taakverdeling met direct server return maken
Externe load balancing Hallo virtuele Hallo openbare virtuele IP-adres van de cloudservice Hallo die als host fungeert voor uw virtuele machines gebruikt. Zodat u niet toocreate moet of Hallo load balancer in dit geval configureren.

U moet een eindpunt met gelijke taakverdeling maken voor elke virtuele machine die als host fungeert voor de replica van een Azure. Als u replica's in meerdere regio's hebt, elke replica voor deze regio moet in dezelfde cloudservice in Hallo Hallo hetzelfde VNet. Beschikbaarheidsgroep maken van replica's die meerdere Azure-regio's omvatten is vereist voor het configureren van meerdere VNets. Zie voor meer informatie over het configureren van cross-VNet-connectiviteit [VNet configureren tooVNet connectiviteit](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Navigeer in hello Azure-portal, tooeach VM die als host fungeert voor een Hallo replica en de weergave details.
2. Klik op Hallo **eindpunten** tabblad voor elk van de VM Hallo.
3. Controleer of deze Hallo **naam** en **openbare poort** Hallo-listener-eindpunt dat u wilt toouse nog niet in gebruik. In onderstaande Hallo voorbeeld, Hallo-naam 'MyEndpoint' en Hallo poort "1433".
4. Op de lokale client downloaden en installeren [Hallo nieuwste PowerShell-module](https://azure.microsoft.com/downloads/).
5. Start **Azure PowerShell**. Een nieuwe PowerShell-sessie is geopend met hello Azure beheerdersrechten modules waren geladen.
6. Voer **Get-AzurePublishSettingsFile**. Deze cmdlet stuurt tooa browser toodownload een publiceren instellingen bestand tooa lokale map. U mogelijk gevraagd om uw referenties aanmelden voor uw Azure-abonnement.
7. Voer Hallo **importeren AzurePublishSettingsFile** opdracht met Hallo pad Hallo bestand publicatie-instellingen die u hebt gedownload:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Nadat Hallo publiceren instellingenbestand is geïmporteerd, kunt u uw Azure-abonnement in de PowerShell-sessie Hallo beheren.
    
1. Kopieer onderstaande Hallo PowerShell-script in een teksteditor en stel Hallo waarden van variabelen toosuit uw omgeving (standaardwaarden zijn opgegeven voor sommige parameters). Houd er rekening mee dat als uw beschikbaarheidsgroep Azure-regio's omvat, moet u Hallo script uitvoeren één keer in elk datacenter voor het Hallo-cloudservice en de knooppunten die zich in dat datacenter bevinden.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Zodra u Hallo variabelen hebt ingesteld, kopie Hallo script in de teksteditor Hallo in uw Azure PowerShell-sessie toorun deze. Als de prompt Hallo nog steeds >>, typt u ENTER opnieuw toomake ervoor Hallo script wordt gestart.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Controleer of KB2854082 wordt indien nodig geïnstalleerd
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Hallo firewall-poorten openen in de beschikbaarheid van groepsknooppunten
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Hallo beschikbaarheidsgroep-listener maken

Maak Hallo beschikbaarheidsgroep-listener in twee stappen. Eerst Hallo client access point-clusterbron maken en configureren van afhankelijkheden. Ten tweede Hallo clusterbronnen configureren met PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Hallo clienttoegangspunt maken en configureren van Hallo cluster afhankelijkheden
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Hallo-clusterbronnen configureren in PowerShell
1. Externe load balancing, moet u Hallo openbare virtuele IP-adres van de cloudservice Hallo met replica's. Meld u aan bij hello Azure-portal. Navigeer toohello cloudservice die uw beschikbaarheidsgroep VM bevat. Open Hallo **Dashboard** weergeven.
2. Houd er rekening mee Hallo-adres die wordt weergegeven onder **adres van de openbare virtuele IP-adres (VIP)**. Als uw oplossing VNets omvat, moet u deze stap herhalen voor elke cloudservice die een virtuele machine die als host fungeert voor een replica bevat.
3. Op een van de virtuele machines Hallo, Hallo onderstaande PowerShell-script kopiëren in een teksteditor en stel Hallo variabelen toohello waarden die u eerder hebt genoteerd.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Eenmaal u Hallo variabelen hebt ingesteld, opent u een Windows PowerShell-venster met verhoogde bevoegdheid, en vervolgens Hallo script in de teksteditor Hallo kopiëren en plakken in uw Azure PowerShell-sessie toorun. Als de prompt Hallo nog steeds >>, typt u ENTER opnieuw toomake ervoor Hallo script wordt gestart.
5. Herhaal deze procedure op elke virtuele machine. Dit script Hallo IP-adres resource met Hallo IP-adres van de cloudservice Hallo configureert en stelt u andere parameters zoals Hallo testpoort. Wanneer de bron van het IP-adres Hallo online is gebracht, reageert deze vervolgens toohello polling op Hallo testpoort van Hallo taakverdeling eindpunt eerder in deze zelfstudie hebt gemaakt.

## <a name="bring-hello-listener-online"></a>Hallo-listener online brengen
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Items worden opgevolgd
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Test Hallo beschikbaarheidsgroep-listener (Hallo binnen hetzelfde VNet)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Test Hallo beschikbaarheidsgroep-listener (via internet Hallo)
In de volgorde tooaccess Hallo-listener van het virtuele netwerk buiten hello, moet u extern/openbare load balancing (in dit onderwerp beschreven) in plaats van een ILB, dit alleen toegankelijk binnen Hallo is hetzelfde VNet. In de verbindingsreeks hello, moet u Hallo cloudservicenaam opgeven. Bijvoorbeeld, als u een cloudservice met de naam van de Hallo had *mycloudservice*, Hallo sqlcmd-instructie zijn als volgt:

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

In tegenstelling tot vorige voorbeeld Hallo SQL-verificatie moet worden gebruikt omdat de aanroeper Hallo windows-verificatie niet kan via Hallo gebruiken internet. Zie voor meer informatie [AlwaysOn-beschikbaarheidsgroep in Azure VM: Client-scenario's voor connectiviteit](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx). Wanneer u SQL-verificatie gebruikt, zorg ervoor dat u, Hallo maakt dezelfde aanmelding op beide replica's. Zie voor meer informatie over het oplossen van aanmeldingen met beschikbaarheidsgroepen [hoe toomap aanmeldingen of gebruik SQL bevat Databasereplica's gebruiker tooconnect tooother en het toewijzen tooavailability databases](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

Als zich in verschillende subnetten bevinden Hallo altijd op de replica's, moeten clients opgeven **MultisubnetFailover = True** in Hallo-verbindingsreeks. Dit resulteert in parallelle verbinding pogingen tooreplicas in verschillende subnetten Hallo. Houd er rekening mee dat dit scenario een regio-overschrijdende altijd op beschikbaarheidsgroep-implementatie bevat.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

