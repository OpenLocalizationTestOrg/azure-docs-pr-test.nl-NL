---
title: aaaExtend HDInsight met het virtuele netwerk - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Azure Virtual Network tooconnect HDInsight tooother cloud resources of resources in uw datacenter
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Azure HDInsight met behulp van een Azure-netwerk uitbreiden

Meer informatie over hoe HDInsight toouse met een [Azure Virtual Network](../virtual-network/virtual-networks-overview.md). Een virtueel netwerk van Azure kunt Hallo volgen scenario's:

* Verbinding tooHDInsight rechtstreeks vanuit een on-premises netwerk.

* Verbinding maken met HDInsight toodata worden opgeslagen in een virtueel Azure-netwerk.

* Rechtstreeks toegang tot Hadoop-services die niet openbaar meer dan beschikbaar Hallo internet. Kafka-API's of Hallo HBase Java API.

> [!WARNING]
> Hallo-informatie in dit document is een goed begrip van TCP/IP-netwerken vereist. Als u niet bekend met TCP/IP-netwerken bent, moet u samenwerken met iemand die dit voordat u wijzigingen tooproduction netwerken.

## <a name="planning"></a>Planning

Hallo volgen Hallo vragen die u bij het plannen van tooinstall HDInsight in een virtueel netwerk moet beantwoorden:

* Moet u tooinstall HDInsight in een bestaand virtueel netwerk? Of maakt u een nieuw netwerk?

    Als u een bestaand virtueel netwerk gebruikt, moet u mogelijk toomodify Hallo netwerkconfiguratie voordat u HDInsight kunt installeren. Zie voor meer informatie, Hallo [HDInsight tooan bestaand virtueel netwerk toevoegen](#existingvnet) sectie.

* Wilt u tooconnect Hallo virtueel netwerk met HDInsight tooanother virtueel netwerk of uw on-premises netwerk?

    tooeasily werk met bronnen in netwerken, u kunt toocreate een aangepaste DNS-server nodig en doorsturen van DNS-configureren. Zie voor meer informatie, Hallo [meerdere netwerken met elkaar verbinden](#multinet) sectie.

* Wilt u toch toorestrict/omleiden tooHDInsight binnenkomend of uitgaand verkeer?

    HDInsight moet hebben onbeperkte communicatie met specifieke IP-adressen in hello Azure-Datacenter. Er zijn ook verschillende poorten die moeten worden toegestaan via firewalls voor clientcommunicatie. Zie voor meer informatie, Hallo [netwerkverkeer beheren](#networktraffic) sectie.

## <a id="existingvnet"></a>HDInsight tooan bestaand virtueel netwerk toevoegen

Gebruik Hallo stappen in deze sectie toodiscover hoe tooadd een nieuwe HDInsight tooan bestaande Azure Virtual Network.

> [!NOTE]
> U kunt een bestaand HDInsight-cluster in een virtueel netwerk niet toevoegen.

1. Gebruikt u een klassiek of Resource Manager-implementatiemodel voor Hallo virtuele netwerk?

    HDInsight 3,4 en groter vereist een virtueel netwerk van Resource Manager. Eerdere versies van HDInsight vereist een klassiek virtueel netwerk.

    Als uw bestaande netwerk een klassiek virtueel netwerk is, moet u een virtueel netwerk van Resource Manager maken en sluit vervolgens Hallo twee. [Klassieke vnet's toonew VNets verbinden](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

    Zodra het is toegevoegd, wordt HDInsight geïnstalleerd in Hallo Resource Manager-netwerk kan communiceren met resources in de klassieke netwerk Hallo.

2. Geforceerde tunneling gebruiken Geforceerde tunneling is subnetinstelling dat ervoor zorgt dat de uitgaande Internet verkeer tooa apparaat voor controle en logboekregistratie. HDInsight biedt geen ondersteuning voor geforceerde tunneling. Verwijder geforceerde tunneling voordat u HDInsight installeert in een subnet, of een nieuw subnet maken voor HDInsight.

3. Gebruik je netwerkbeveiligingsgroepen, de gebruiker gedefinieerde routes of virtuele netwerkapparaten toorestrict verkeer van of naar Hallo virtuele netwerk?

    Als een beheerde service vereist HDInsight onbeperkte toegang tooseveral IP-adressen in hello Azure-Datacenter. tooallow communicatie met deze IP-adressen, eventuele bestaande netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes bijwerken.

    HDInsight als host fungeert voor meerdere services, die verschillende poorten gebruiken. Verkeer toothese poorten niet blokkeren. Zie voor een lijst met poorten tooallow via virtueel apparaat firewalls, Hallo [beveiliging](#security) sectie.

    toofind uw bestaande beveiligingsconfiguratie gebruik hello Azure PowerShell of Azure CLI-opdrachten te volgen:

    * Netwerkbeveiligingsgroepen

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        Zie voor meer informatie, Hallo [netwerkbeveiligingsgroepen oplossen](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.

        > [!IMPORTANT]
        > Netwerkbeveiligingsgroepen worden toegepast in volgorde op basis van Regelprioriteit. Hallo eerste regel die overeenkomt met Hallo verkeer patroon wordt toegepast en geen andere voor dat verkeer wordt toegepast. De regels van de volgorde van meest strikte tooleast strikte. Zie voor meer informatie, Hallo [filteren van netwerkverkeer met netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) document.

    * Door de gebruiker gedefinieerde routes

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        Zie voor meer informatie, Hallo [routes oplossen](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.

4. Maken van een HDInsight-cluster en hello Azure Virtual Network selecteren tijdens de configuratie. Gebruik Hallo stappen in Hallo aanmaakproces voor documenten toounderstand Hallo-cluster te volgen:

    * [Maken van HDInsight met behulp van hello Azure-portal](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [HDInsight maken met Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [Maken van HDInsight met behulp van Azure CLI 1.0](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [HDInsight met behulp van een Azure Resource Manager-sjabloon maken](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > Toevoegen van HDInsight is tooa virtueel netwerk een optionele configuratie-stap. Ervoor tooselect Hallo virtueel netwerk worden bij het Hallo-cluster configureren.

## <a id="multinet"></a>Meerdere netwerken met elkaar verbinden

Hallo grootste uitdaging met een configuratie met meerdere is naamomzetting tussen Hallo netwerken.

Azure biedt naamomzetting voor Azure-services die zijn geïnstalleerd in een virtueel netwerk. Deze ingebouwde naamomzetting kunt HDInsight tooconnect toohello resources met behulp van een volledig gekwalificeerde domeinnaam (FQDN) te volgen:

* Een resource die beschikbaar is op Hallo internet. Bijvoorbeeld microsoft.com, google.com.

* Een resource die is in Hallo hetzelfde virtuele netwerk van Azure, met behulp van Hallo __interne DNS-naam__ van Hallo resource. Wanneer u Hallo standaard naamomzetting gebruikt, zijn Hallo volgende voorbeeld interne DNS-namen toegewezen tooHDInsight worker-knooppunten:

    * wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    Deze beide knooppunten kunnen communiceren rechtstreeks met elkaar en andere knooppunten in HDInsight, met behulp van de interne DNS-namen.

Hallo standaard naamomzetting biedt __niet__ HDInsight tooresolve Hallo namen van bronnen in netwerken die gekoppeld toohello virtueel netwerk zijn toestaan. Bijvoorbeeld, het algemene toojoin is uw on-premises netwerk toohello virtueel netwerk. Met alleen Hallo standaard naamomzetting HDInsight kan geen toegang krijgen tot bronnen in Hallo on-premises netwerk met de naam. Hallo tegengestelde geldt ook resources in uw on-premises netwerk heeft geen toegang tot resources in Hallo virtueel netwerk met de naam.

> [!WARNING]
> U moet Hallo aangepaste DNS-server maken en configureren van Hallo virtueel netwerk toouse deze voordat u Hallo HDInsight-cluster.

naamomzetting tooenable tussen Hallo virtueel netwerk en bronnen in gekoppelde netwerken, moet u Hallo volgende acties uitvoeren:

1. Maak een aangepaste DNS-server in hello Azure Virtual Network waar u van plan tooinstall HDInsight bent.

2. Hallo virtueel netwerk toouse Hallo aangepaste DNS-server configureren.

3. Azure DNS-achtervoegsel voor het virtuele netwerk toegewezen Hallo zoeken. Deze waarde is te vergelijkbare`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`. Zie voor informatie over het zoeken naar Hallo DNS-achtervoegsel Hallo [voorbeeld: aangepaste DNS](#example-dns) sectie.

4. Doorsturen tussen Hallo DNS-servers configureren. Hallo-configuratie, is afhankelijk van Hallo-type van het externe netwerk.

    * Als het externe netwerk Hallo een on-premises netwerk is, configureren van DNS als volgt:
        
        * __Aangepaste DNS__ (in Hallo virtueel netwerk):

            * Aanvragen voor Hallo DNS-achtervoegsel van Hallo virtueel netwerk toohello Azure recursieve naamomzetting (168.63.129.16) doorsturen. Aanvragen voor bronnen in het virtuele netwerk hello Azure worden verwerkt

            * Doorsturen van alle andere aanvragen toohello lokale DNS-server. Hallo lokale DNS verwerkt alle andere aanvragen voor naamomzetting, zelfs aanvragen voor internetbronnen zoals Microsoft.com.

        * __Lokale DNS__: doorsturen van aanvragen voor Hallo virtueel netwerk DNS-achtervoegsel toohello aangepaste DNS-server. Hallo aangepaste DNS-server stuurt toohello Azure recursieve resolver.

        Deze configuratie routes aanvragen voor FQDN-namen die Hallo DNS-achtervoegsel van Hallo virtueel netwerk toohello aangepaste DNS-server bevatten. Alle andere verzoeken (zelfs voor openbare internet-adressen) worden verwerkt door Hallo lokale DNS-server.

    * Als het externe netwerk Hallo een ander virtueel netwerk van Azure is, configureren van DNS als volgt:

        * __Aangepaste DNS__ (in elk virtueel netwerk):

            * Aanvragen voor Hallo DNS-achtervoegsel van de virtuele netwerken Hallo doorgestuurd toohello aangepaste DNS-servers. Hallo DNS in elk virtueel netwerk is verantwoordelijk voor het oplossen van resources binnen het netwerk.

            * Alle andere aanvragen toohello Azure recursieve resolver doorsturen. Hallo recursieve resolver is verantwoordelijk voor het oplossen van lokale en internetbronnen.

        Hallo DNS-server voor elk netwerk verzendt aanvragen toohello andere, op basis van DNS-achtervoegsel. Andere aanvragen worden omgezet met behulp van hello Azure recursieve resolver.

    Zie voor een voorbeeld van elke configuratie Hallo [voorbeeld: aangepaste DNS](#example-dns) sectie.

Zie voor meer informatie, Hallo [naamomzetting voor VM's en Rolexemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.

## <a name="directly-connect-toohadoop-services"></a>TooHadoop services rechtstreeks verbinding te maken

De meeste documentatie op HDInsight wordt ervan uitgegaan dat u toegang toohello cluster via Hallo internet. Bijvoorbeeld, kunt u de cluster toohello op https://CLUSTERNAME.azurehdinsight.net koppelen. Dit adres Hallo openbare-gateway niet beschikbaar is als u nsg's hebt gebruikt of udr's toorestrict toegang vanaf internet Hallo gebruikt.

tooconnect tooAmbari en andere webpagina's via Hallo virtueel netwerk, gebruikt u Hallo stappen te volgen:

1. toodiscover hello interne volledig gekwalificeerde domeinnamen (FQDN) van clusterknooppunten Hallo HDInsight, een van de volgende methoden hello gebruiken:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    Hallo FQDN-naam vinden voor Hallo hoofdknooppunten in Hallo lijst met knooppunten die zijn geretourneerd, en Hallo FQDN's tooconnect tooAmbari en andere webservices gebruiken. Bijvoorbeeld: `http://<headnode-fqdn>:8080` tooaccess Ambari.

    > [!IMPORTANT]
    > Sommige services die worden gehost op Hallo hoofdknooppunten zijn alleen actief is op één knooppunt tegelijk. Als u probeert toegang tot een service op één hoofdknooppunt en een 404-fout retourneert, overschakelen toohello andere hoofdknooppunt.

2. toodetermine hello knooppunt en de poort die een service is beschikbaar op, Zie Hallo [poorten die worden gebruikt door de services van Hadoop op HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.

## <a id="networktraffic"></a>Beheren van netwerkverkeer

Netwerkverkeer in een virtuele Azure-netwerken kan worden beheerd met behulp van de volgende methoden Hallo:

* **Netwerkbeveiligingsgroepen** (NSG) kunt u toofilter binnenkomend en uitgaand verkeer toohello netwerk. Zie voor meer informatie, Hallo [filteren van netwerkverkeer met netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) document.

    > [!WARNING]
    > HDInsight biedt geen ondersteuning voor uitgaand verkeer te beperken.

* **Gebruiker gedefinieerde routes** (UDR) definiëren hoe verkeer tussen resources in Hallo netwerk loopt. Zie voor meer informatie, Hallo [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md) document.

* **Virtuele apparaten** Hallo-functionaliteit van apparaten, zoals firewalls en routers repliceren. Zie voor meer informatie, Hallo [netwerkapparaten](https://azure.microsoft.com/solutions/network-appliances) document.

Als een beheerde service moet HDInsight onbeperkte toegang tooAzure status en beheer van services in hello Azure-cloud. Wanneer u nsg's en udr's, moet u ervoor zorgen dat HDInsight deze services nog steeds met HDInsight communiceren kunnen.

HDInsight beschrijft de services op verschillende poorten. Wanneer u een virtueel apparaat firewall gebruikt, moet u verkeer op Hallo poorten die worden gebruikt voor deze services toestaan. Zie Hallo [vereiste poorten] sectie voor meer informatie.

### <a id="hdinsight-ip"></a>HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes

Als u gebruiken wilt **netwerkbeveiligingsgroepen** of **gebruiker gedefinieerde routes** toocontrol netwerkverkeer, voert u Hallo van de volgende activiteiten voor de installatie van HDInsight:

1. Identificeer hello Azure dat u van plan toouse voor HDInsight bent-regio.

2. Hallo IP-adressen vereist voor HDInsight identificeren. Zie voor meer informatie, Hallo [IP-adressen die zijn vereist voor HDInsight](#hdinsight-ip) sectie.

3. Hallo netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes voor Hallo subnet dat u van plan tooinstall HDInsight bent maakt of wijzigt in.

    * __Netwerkbeveiligingsgroepen__: toestaan __inkomende__ verkeer op poort __443__ van Hallo IP-adressen.
    * __Gebruiker gedefinieerde routes__: maken van een route tooeach IP-adres en Hallo __volgende hop type__ too__Internet__.

Zie voor meer informatie over netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes Hallo documentatie te volgen:

* [Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md)

* [Gebruiker gedefinieerde routes](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>Geforceerde tunneling

Geforceerde tunneling is een door de gebruiker gedefinieerde routering configuratie waarbij alle verkeer van een subnet geforceerde tooa specifieke netwerk- of locatie, zoals uw on-premises netwerk. HDInsight biedt __niet__ ondersteuning geforceerde tunneling.

## <a id="hdinsight-ip"></a>Vereiste IP-adressen

> [!IMPORTANT]
> Hallo Azure health en beheerservices moet kunnen toocommunicate met HDInsight. Als u netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes gebruikt, kunt u verkeer van Hallo IP-adressen voor deze services tooreach HDInsight.
>
> Als u netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes toocontrol verkeer niet gebruikt, kunt u deze sectie overslaan.

Als u netwerkbeveiligingsgroepen of de gebruiker gedefinieerde routes gebruikt, moet u het verkeer van hello Azure status- en management services tooreach HDInsight toestaan. Gebruik Hallo volgende stappen toofind Hallo IP-adressen die moeten worden toegestaan:

1. U moet altijd verkeer van Hallo volgende IP-adressen toestaan:

    | IP-adres | Toegestane poort | Richting |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | Inkomend |
    | 23.99.5.239 | 443 | Inkomend |
    | 168.61.48.131 | 443 | Inkomend |
    | 138.91.141.162 | 443 | Inkomend |

2. Als uw HDInsight-cluster zich in een van de volgende regio's hello, moet u verkeer van Hallo IP-adressen die worden vermeld voor Hallo regio toestaan:

    > [!IMPORTANT]
    > Als u gebruikmaakt van Azure-regio Hallo niet wordt weergegeven, klikt u vervolgens alleen gebruiken Hallo vier IP-adressen uit stap 1.

    | Land | Regio | Toegestane IP-adressen | Toegestane poort | Richting |
    | ---- | ---- | ---- | ---- | ----- |
    | Azië | Oost-Azië | 23.102.235.122</br>52.175.38.134 | 443 | Inkomend |
    | &nbsp; | Zuidoost-Azië | 13.76.245.160</br>13.76.136.249 | 443 | Inkomend |
    | Australië | Australië - oost | 104.210.84.115</br>13.75.152.195 | 443 | Inkomend |
    | &nbsp; | Australië - zuidoost | 13.77.2.56</br>13.77.2.94 | 443 | Inkomend |
    | Brazilië | Brazilië - zuid | 191.235.84.104</br>191.235.87.113 | 443 | Inkomend |
    | Canada | Canada - oost | 52.229.127.96</br>52.229.123.172 | 443 | Inkomend |
    | &nbsp; | Canada - midden | 52.228.37.66</br>52.228.45.222 | 443 | Inkomend |
    | China | China - noord | 42.159.96.170</br>139.217.2.219 | 443 | Inkomend |
    | &nbsp; | China - oost | 42.159.198.178</br>42.159.234.157 | 443 | Inkomend |
    | Europa | Noord-Europa | 52.164.210.96</br>13.74.153.132 | 443 | Inkomend |
    | &nbsp; | West-Europa| 52.166.243.90</br>52.174.36.244 | 443 | Inkomend |
    | Duitsland | Duitsland - centraal | 51.4.146.68</br>51.4.146.80 | 443 | Inkomend |
    | &nbsp; | Duitsland - noordoost | 51.5.150.132</br>51.5.144.101 | 443 | Inkomend |
    | India | Centraal-India | 52.172.153.209</br>52.172.152.49 | 443 | Inkomend |
    | Japan | Japan - oost | 13.78.125.90</br>13.78.89.60 | 443 | Inkomend |
    | &nbsp; | Japan - west | 40.74.125.69</br>138.91.29.150 | 443 | Inkomend |
    | Korea | Korea - centraal | 52.231.39.142</br>52.231.36.209 | 433 | Inkomend |
    | &nbsp; | Korea - zuid | 52.231.203.16</br>52.231.205.214 | 443 | Inkomend
    | Verenigd Koninkrijk | Verenigd Koninkrijk West | 51.141.13.110</br>51.141.7.20 | 443 | Inkomend |
    | &nbsp; | Verenigd Koninkrijk Zuid | 51.140.47.39</br>51.140.52.16 | 443 | Inkomend |
    | Verenigde Staten | VS - midden | 13.67.223.215</br>40.86.83.253 | 443 | Inkomend |
    | &nbsp; | Noord-centraal VS | 157.56.8.38</br>157.55.213.99 | 443 | Inkomend |
    | &nbsp; | West-centraal VS | 52.161.23.15</br>52.161.10.167 | 443 | Inkomend |
    | &nbsp; | VS - west 2 | 52.175.211.210</br>52.175.222.222 | 443 | Inkomend |

    Zie voor informatie over het Hallo-IP toouse voor Azure Government adressen, Hallo [Azure Government Intelligence en analyse](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.

3. Als u een aangepaste DNS-server met het virtuele netwerk gebruikt, moet u ook toegang vanaf toestaan __168.63.129.16__. Dit adres is van de Azure recursieve naamomzetting. Zie voor meer informatie, Hallo [naamomzetting voor VM's en rol exemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.

Zie voor meer informatie, Hallo [netwerkverkeer beheren](#networktraffic) sectie.

## <a id="hdinsight-ports"></a>Vereiste poorten

Als u van plan bent met een netwerk **virtueel apparaat firewall** toosecure Hallo virtueel netwerk, moet u uitgaand verkeer toestaan op Hallo poorten te volgen:

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

Zie voor een lijst met poorten voor specifieke services, Hallo [poorten die worden gebruikt door de services van Hadoop op HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.

Zie voor meer informatie over firewallregels voor virtuele apparaten Hallo [virtueel apparaat scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.

## <a id="hdinsight-nsg"></a>Voorbeeld: netwerkbeveiligingsgroepen met HDInsight

Hallo-voorbeelden in deze sectie laten zien hoe de netwerkbeveiligingsgroep toocreate regels die HDInsight toocommunicate Hello Azure management-services toestaan. Voordat u Hallo voorbeelden, aanpassen Hallo IP-adressen toomatch Hallo waarden voor hello Azure-regio u gebruikt. U vindt deze informatie in Hallo [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.

### <a name="azure-resource-management-template"></a>Azure Resource Management-sjabloon

Hallo maakt volgende Resource Management-sjabloon een virtueel netwerk dat binnenkomend verkeer wordt beperkt, maar wordt verkeer van Hallo IP-adressen vereist voor HDInsight. Deze sjabloon maakt ook een HDInsight-cluster in Hallo virtueel netwerk.

* [Een beveiligde virtuele Azure-netwerk en een HDInsight Hadoop-cluster implementeren](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> Hallo IP-adressen in dit voorbeeld toomatch hello Azure-regio u wijzigen. U vindt deze informatie in Hallo [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.

### <a name="azure-powershell"></a>Azure PowerShell

Hallo volgende PowerShell-script toocreate een virtueel netwerk dat binnenkomend verkeer beperkt en kunt verkeer van Hallo IP-adressen voor de regio Noord-Europa hello gebruiken.

> [!IMPORTANT]
> Hallo IP-adressen in dit voorbeeld toomatch hello Azure-regio u wijzigen. U vindt deze informatie in Hallo [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> In dit voorbeeld laat zien hoe tooadd regels tooallow binnenkomend verkeer op Hallo vereist IP-adressen. Het bevat geen een toorestrict regel binnenkomende toegang uit andere bronnen.
>
> Hallo volgende voorbeeld laat zien hoe tooenable SSH vanaf Hallo Internet toegang tot:
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>Azure CLI

Hallo te volgen stappen toocreate een virtueel netwerk dat binnenkomend verkeer wordt beperkt, maar verkeer van Hallo IP-adressen vereist voor HDInsight kunt gebruiken.

1. Gebruik Hallo na de opdracht toocreate een nieuwe netwerkbeveiligingsgroep met de naam `hdisecure`. Vervang **RESOURCEGROUPNAME** met de resourcegroep Hallo met hello Azure Virtual Network. Vervang **locatie** met Hallo locatie (regio) in die groep Hallo is gemaakt.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    Zodra het Hallo-groep is gemaakt, krijgt u informatie over de nieuwe groep Hallo.

2. Hallo na tooadd regels toohello nieuwe netwerkbeveiligingsgroep waarmee binnenkomende communicatie op poort 443 van hello Azure HDInsight-status en management-service gebruiken. Vervang **RESOURCEGROUPNAME** met Hallo-naam van resourcegroep Hallo met hello Azure Virtual Network.

    > [!IMPORTANT]
    > Hallo IP-adressen in dit voorbeeld toomatch hello Azure-regio u wijzigen. U vindt deze informatie in Hallo [HDInsight met netwerkbeveiligingsgroepen en de gebruiker gedefinieerde routes](#hdinsight-ip) sectie.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve unieke id voor deze netwerkbeveiligingsgroep hello, Hallo volgende opdracht gebruiken:

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    Met deze opdracht retourneert een waarde van een vergelijkbare toohello volgende tekst:

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Gebruik dubbele aanhalingstekens rond id in Hallo opdracht als u geen Hallo verwacht resultaten krijgt.

4. Gebruik hello opdracht tooapply Hallo beveiliging groep tooa netwerksubnet te volgen. Vervang Hallo __GUID__ en __RESOURCEGROUPNAME__ waarden Hello die zijn geretourneerd door de vorige stap Hallo. Vervang __VNETNAME__ en __SUBNETNAME__ met virtuele-netwerknaam Hallo en subnetnaam die u toocreate wilt.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    Zodra deze opdracht is voltooid, kunt u HDInsight kunt installeren in Hallo virtueel netwerk.

> [!IMPORTANT]
> Deze stappen alleen openen access toohello HDInsight status en de management-service op Hallo Azure-cloud. Alle andere toegang toohello HDInsight-cluster van externe Hallo virtueel netwerk is geblokkeerd. tooenable toegang van buiten Hallo virtueel netwerk, moet u extra regels van de Netwerkbeveiligingsgroep toevoegen.
>
> Hallo volgende voorbeeld laat zien hoe tooenable SSH vanaf Hallo Internet toegang tot:
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a>Voorbeeld: DNS-configuratie

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>Naamomzetting tussen een virtueel netwerk en een netwerk verbonden on-premises

In dit voorbeeld maakt Hallo veronderstellingen te volgen:

* U hebt een Azure-netwerk dat is verbonden tooan on-premises netwerk via een VPN-gateway.

* aangepaste DNS-server in het virtuele netwerk Hallo Hallo wordt Linux of Unix als Hallo besturingssysteem uitgevoerd.

* [BIND](https://www.isc.org/downloads/bind/) op Hallo aangepaste DNS-server is geïnstalleerd.

Op Hallo aangepaste DNS-server in het virtuele netwerk Hallo:

1. Azure PowerShell of Azure CLI toofind Hallo DNS-achtervoegsel van het virtuele netwerk hello gebruiken:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Gebruik op Hallo aangepaste DNS-server voor het virtuele netwerk hello, na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.local` bestand:

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Vervang Hallo `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` waarde met de Hallo DNS-achtervoegsel van het virtuele netwerk.

    Deze configuratie alle DNS-aanvragen voor Hallo DNS-achtervoegsel van Hallo virtueel netwerk toohello Azure recursieve resolver gestuurd.

2. Gebruik op Hallo aangepaste DNS-server voor het virtuele netwerk hello, na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.options` bestand:

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Vervang Hallo `10.0.0.0/16` waarde met de Hallo IP-adresbereik van het virtuele netwerk. Deze vermelding kan name resolution aanvragen adressen binnen dit bereik.

    * Hallo IP-adresbereik van Hallo lokale netwerk toohello `acl goodclients { ... }` sectie.  vermelding kan aanvragen voor naamomzetting van resources in Hallo on-premises netwerk.
    
    * Vervang de waarde Hallo `192.168.0.1` met Hallo IP-adres van uw lokale DNS-server. Deze vermelding routeert alle andere DNS-aanvragen toohello lokale DNS-server.

3. configuratie van toouse hello, binding opnieuw opstarten. Bijvoorbeeld `sudo service bind9 restart`.

4. Een voorwaardelijke doorstuurserver toohello lokale DNS-server toevoegen. Hallo voorwaardelijke doorstuurserver toosend aanvragen voor Hallo DNS-achtervoegsel van stap 1 toohello aangepaste DNS-server configureren.

    > [!NOTE]
    > Raadpleeg Hallo documentatie bij uw DNS-software voor specifieke informatie over het tooadd een voorwaardelijke doorstuurserver.

Na het voltooien van deze stappen kunt u tooresources in een netwerk met behulp van de volledig gekwalificeerde domeinnamen (FQDN). U kunt nu HDInsight installeren in Hallo virtueel netwerk.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>Naamomzetting tussen de twee verbonden virtuele netwerken

In dit voorbeeld maakt Hallo veronderstellingen te volgen:

* U hebt twee virtuele netwerken van Azure die zijn verbonden via een VPN-gateway of -peering.

* Hallo aangepaste DNS-server in beide netwerken wordt Linux of Unix als Hallo besturingssysteem uitgevoerd.

* [BIND](https://www.isc.org/downloads/bind/) op Hallo aangepaste DNS-servers is geïnstalleerd.

1. Gebruik Azure PowerShell of Azure CLI toofind Hallo DNS-achtervoegsel van beide virtuele netwerken:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Gebruik Hallo na de tekst hello inhoud Hallo `/etc/bind/named.config.local` -bestand op Hallo aangepaste DNS-server. Deze wijziging hebt aangebracht op Hallo aangepaste DNS-server in beide virtuele netwerken.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Vervang Hallo `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` waarde met de DNS-achtervoegsel Hallo Hallo __andere__ virtueel netwerk. Deze vermelding aanvragen voor Hallo DNS-achtervoegsel van Hallo extern netwerk toohello gestuurd aangepaste DNS-server in dat netwerk.

3. Gebruik op Hallo aangepaste DNS-servers in beide virtuele netwerken, na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.options` bestand:

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Vervang Hallo `10.0.0.0/16` en `10.1.0.0/16` waarden met Hallo IP-adresbereiken van uw virtuele netwerken. Deze vermelding kan resources in elke netwerk toomake aanvragen van Hallo DNS-servers.

    Alle aanvragen die niet voor DNS-achtervoegsels Hallo Hallo virtuele netwerken (bijvoorbeeld microsoft.com) wordt uitgevoerd door hello Azure recursieve resolver.

4. configuratie van toouse hello, binding opnieuw opstarten. Bijvoorbeeld: `sudo service bind9 restart` op beide DNS-servers.

Na het voltooien van deze stappen kunt u tooresources in Hallo virtueel netwerk met behulp van de volledig gekwalificeerde domeinnamen (FQDN). U kunt nu HDInsight installeren in Hallo virtueel netwerk.

## <a name="next-steps"></a>Volgende stappen

* Zie voor een voorbeeld van de end-to-end van de configuratie van HDInsight tooconnect tooan on-premises netwerk, [verbinding maken met HDInsight tooan on-premises netwerk](./connect-on-premises-network.md).

* Zie voor meer informatie over virtuele netwerken van Azure Hallo [Azure Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).

* Zie voor meer informatie over netwerkbeveiligingsgroepen [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).

* Zie voor meer informatie over de gebruiker gedefinieerde routes, [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md).