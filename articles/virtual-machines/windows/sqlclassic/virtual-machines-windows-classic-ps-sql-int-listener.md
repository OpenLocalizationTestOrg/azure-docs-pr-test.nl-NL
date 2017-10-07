---
title: aaaConfigure een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen in Azure | Microsoft Docs
description: Deze zelfstudie maakt gebruik van bronnen die zijn gemaakt met het klassieke implementatiemodel Hallo en er een altijd op beschikbaarheidsgroep-listener gemaakt in Azure die gebruikmaakt van een interne load balancer.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure
> [!div class="op_single_selector"]
> * [Interne listener](../classic/ps-sql-int-listener.md)
> * [Externe-listener](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Overzicht

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over gebruik van het klassieke implementatiemodel Hallo Hallo. U wordt aangeraden de meeste nieuwe implementaties Hallo Resource Manager-model gebruiken.

tooconfigure een listener voor een beschikbaarheidsgroep altijd op in de Resource Manager-model hello, Zie [een load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

De beschikbaarheidsgroep kan de replica's die alleen op lokale of Azure alleen, of die zowel on-premises en Azure voor hybride configuraties omvatten bevatten. Azure replica's kunnen zich bevinden in Hallo dezelfde regio of tussen meerdere regio's die gebruikmaken van meerdere virtuele netwerken. Hallo procedures in dit artikel wordt ervan uitgegaan dat u al hebt [geconfigureerd een beschikbaarheidsgroep](../classic/portal-sql-alwayson-availability-groups.md) maar nog niet zijn ingesteld op een listener.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Richtlijnen en beperkingen voor interne listeners
Hallo-gebruik van een interne load balancer (ILB) met een beschikbaarheidsgroep-listener in Azure wordt onderwerp toohello richtlijnen te volgen:

* Hallo beschikbaarheidsgroep-listener wordt ondersteund op Windows Server 2008 R2, Windows Server 2012 en Windows Server 2012 R2.
* Alleen een interne beschikbaarheidsgroep-listener wordt ondersteund voor elke cloudservice omdat Hallo-listener is toohello ILB is geconfigureerd en er is slechts één ILB voor elke cloudservice. Het is echter mogelijk toocreate meerdere externe listeners. Zie voor meer informatie [een externe-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Hallo toegankelijkheid van Hallo listener bepalen
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Dit artikel is gericht op het maken van een listener die gebruikmaakt van een ILB. Als u een openbare of externe-listener moet, Zie Hallo-versie van dit artikel dat instelling van bespreekt een [externe listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>VM-eindpunten taakverdeling met direct server return maken
U eerst maken een ILB door het uitvoeren van script hello later in deze sectie.

Maak een eindpunt taakverdeling voor elke virtuele machine die als host fungeert voor een Azure-replica. Als u replica's in meerdere regio's hebt, elke replica voor deze regio moet in dezelfde cloudservice in Hallo Hallo hetzelfde virtuele Azure-netwerk. Maken van replica's die meerdere Azure-regio's omvatten voor beschikbaarheid, moet meerdere virtuele netwerken configureren. Zie voor meer informatie over het configureren van cross-virtuele netwerkverbindingen [virtueel netwerk toovirtual netwerkconnectiviteit configureren](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Ga in hello Azure-portal, tooeach virtuele machine die als host fungeert voor een replica tooview Hallo details.

2. Klik op Hallo **eindpunten** tabblad voor elke virtuele machine.

3. Controleer of deze Hallo **naam** en **openbare poort** van Hallo-listener-eindpunt dat u wilt dat toouse zijn niet al in gebruik. In voorbeeld Hallo in deze sectie, is de naam van de Hallo *MyEndpoint*, en poort Hallo *1433*.

4. Op de lokale client downloaden en installeren Hallo meest recente [PowerShell-module](https://azure.microsoft.com/downloads/).

5. Azure PowerShell te starten.  
    Een nieuwe PowerShell-sessie wordt geopend, hello Azure beheerdersrechten modules waren geladen.

6. Voer `Get-AzurePublishSettingsFile` uit. Deze cmdlet stuurt tooa browser toodownload een publiceren instellingen bestand tooa lokale map. U mogelijk gevraagd om uw referenties aanmelden om uw Azure-abonnement.

7. Voer de volgende Hallo `Import-AzurePublishSettingsFile` opdracht met Hallo pad Hallo bestand publicatie-instellingen die u hebt gedownload:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Nadat Hallo publiceren instellingenbestand is geïmporteerd, kunt u uw Azure-abonnement in de PowerShell-sessie Hallo beheren.

8. Voor *ILB*, een statisch IP-adres toewijzen. Hallo huidige virtuele netwerkconfiguratie controleren door het uitvoeren van de volgende opdracht Hallo:

        (Get-AzureVNetConfig).XMLConfiguration
9. Opmerking Hallo *Subnet* naam in voor het Hallo-subnet dat Hallo virtuele machines die als host Hallo replica's fungeren bevat. Deze naam wordt gebruikt in de parameter Hallo $SubnetName in Hallo-script.

10. Opmerking Hallo *VirtualNetworkSite* een naam geven en Hallo starten *AddressPrefix* voor Hallo-subnet dat Hallo virtuele machines die als host Hallo replica's fungeren bevat. Zoek naar een beschikbaar IP-adres door het doorgeven van beide waarden toohello `Test-AzureStaticVNetIP` opdracht en door te onderzoeken Hallo *AvailableAddresses*. Bijvoorbeeld, als hello virtueel netwerk met de naam *MyVNet* en heeft een subnet-adresbereik dat begint bij *172.16.0.128*, Hallo volgende opdracht zou lijst beschikbare adressen:

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Selecteer een van de beschikbare adressen Hallo en deze gebruiken in Hallo $ILBStaticIP-parameter van het script in de volgende stap Hallo Hallo.

12. Kopiëren van de volgende PowerShell-script tooa teksteditor Hallo en stel Hallo waarden van variabelen toosuit uw omgeving. Standaardwaarden zijn opgegeven voor een aantal parameters.  

    Bestaande implementaties die gebruikmaken van affiniteitsgroepen kunnen een ILB niet toevoegen. Zie voor meer informatie over de vereisten voor de ILB [interne load balancer overzicht](../../../load-balancer/load-balancer-internal-overview.md).

    Ook als de beschikbaarheidsgroep Azure-regio's omvat, moet u Hallo script uitvoeren één keer in elk datacenter voor het Hallo-cloudservice en de knooppunten die zich in dat datacenter bevinden.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. Nadat u de variabelen Hallo hebt ingesteld, kopie Hallo script uit Hallo text editor tooyour PowerShell-sessie toorun deze. Als de prompt Hallo nog steeds  **>>** , druk op Enter toomake ervoor Hallo script opnieuw wordt gestart.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Controleer of KB2854082 wordt indien nodig geïnstalleerd
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Hallo firewall-poorten openen in de beschikbaarheid van groepsknooppunten
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Hallo beschikbaarheidsgroep-listener maken

Maak Hallo beschikbaarheidsgroep-listener in twee stappen. Eerst Hallo client access point-clusterbron maken en configureren van afhankelijkheden. Ten tweede Hallo clusterbronnen in PowerShell configureren.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Hallo clienttoegangspunt maken en configureren van Hallo cluster afhankelijkheden
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Hallo-clusterbronnen configureren in PowerShell
1. Voor de ILB, moet u Hallo IP-adres van Hallo ILB die eerder is gemaakt. tooobtain dit IP-adres in PowerShell, gebruik Hallo script volgen:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. Op een van de virtuele machines Hallo Hallo PowerShell-script kopiëren voor uw besturingssysteem tooa-teksteditor en stel Hallo variabelen toohello waarden die u eerder hebt genoteerd.

    Voor Windows Server 2012 of hoger, gebruikt u Hallo script volgen:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Gebruik voor Windows Server 2008 R2 Hallo script volgen:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. Nadat u hebt ingesteld Hallo variabelen, open een Windows PowerShell-venster met verhoogde bevoegdheid, plakken Hallo script in de teksteditor Hallo in uw PowerShell-sessie toorun deze. Als de prompt Hallo nog steeds  **>>** , druk op Enter opnieuw toomake ervoor dat Hallo script wordt gestart.

4. Herhaal de vorige stappen voor elke VM Hallo.  
    Dit script Hallo IP-adres resource met Hallo IP-adres van de cloudservice Hallo configureert en stelt u andere parameters, zoals Hallo testpoort. Wanneer de bron van het IP-adres Hallo online is gebracht, reageert het toohello polling op Hallo testpoort van Hallo taakverdeling eindpunt dat u eerder hebt gemaakt.

## <a name="bring-hello-listener-online"></a>Hallo-listener online brengen
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Items worden opgevolgd
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Test Hallo beschikbaarheidsgroep-listener (Hallo binnen hetzelfde virtuele netwerk)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
