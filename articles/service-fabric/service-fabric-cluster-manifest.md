---
title: Configureren van uw Azure Service Fabric-cluster zelfstandige | Microsoft Docs
description: Informatie over het configureren van uw zelfstandige of persoonlijke Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Configuratie-instellingen voor zelfstandige Windows-cluster
In dit artikel wordt beschreven hoe u een zelfstandige Service Fabric cluster met de ***ClusterConfig.JSON*** bestand. U kunt dit bestand informatie zoals de Service Fabric-knooppunten en de IP-adressen, de verschillende soorten knooppunten op het cluster, de beveiligingsconfiguraties, evenals de netwerktopologie in termen van fouttolerantie/upgrade-domeinen voor uw zelfstandige cluster opgeven.

Wanneer u [download het zelfstandige Service Fabric-pakket](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), een paar voorbeelden van het bestand ClusterConfig.JSON worden gedownload met uw werk-machine. De voorbeelden die *DevCluster* in hun naam helpt u bij het maken van een cluster met alle drie knooppunten op dezelfde computer, zoals logische knooppunten. Buiten deze, moet ten minste één knooppunt worden gemarkeerd als een primaire knooppunt. Dit cluster is handig voor een omgeving met ontwikkeling of tests en wordt niet ondersteund als een productiecluster. De voorbeelden die *MultiMachine* in hun naam helpt u bij het maken van een productiecluster kwaliteit met elk knooppunt op een afzonderlijke computer.

1. *ClusterConfig.Unsecure.DevCluster.JSON* en *ClusterConfig.Unsecure.MultiMachine.JSON* laten zien hoe u respectievelijk een onbeveiligde test- of -cluster maken. 
2. *ClusterConfig.Windows.DevCluster.JSON* en *ClusterConfig.Windows.MultiMachine.JSON* weergeven van het maken van de test- of -cluster beveiligd met [Windows-beveiliging](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* en *ClusterConfig.X509.MultiMachine.JSON* weergeven van het maken van de test- of -cluster beveiligd met [X509 beveiliging op basis van certificaat](service-fabric-windows-cluster-x509-security.md). 

Nu gaan we de verschillende secties van kijken een ***ClusterConfig.JSON*** bestand zoals hieronder.

## <a name="general-cluster-configurations"></a>Algemene clusterconfiguraties
Dit betreft brede cluster specifieke configuraties, zoals wordt weergegeven in het onderstaande JSON-codefragment.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

U kunt een beschrijvende naam geven tot uw Service Fabric-cluster door toe te wijzen aan de **naam** variabele. De **clusterConfigurationVersion** is het versienummer van het cluster, moet u deze verhogen telkens wanneer u een upgrade uitvoert van Service Fabric-cluster. Laat u echter de **apiVersion** op de standaardwaarde.

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a>Knooppunten op het cluster
U kunt de knooppunten configureren op uw Service Fabric-cluster met behulp van de **knooppunten** sectie als het volgende codefragment bevat.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Een Service Fabric-cluster moet ten minste 3 knooppunten bevatten. In deze sectie kunt u meer knooppunten toevoegen aan de hand van uw instellingen. De volgende tabel beschrijft de configuratie-instellingen voor elk knooppunt.

| **Knooppuntconfiguratie** | **Beschrijving** |
| --- | --- |
| nodeName |U kunt een beschrijvende naam geven tot het knooppunt. |
| IP-adres |Het IP-adres van uw knooppunt vinden door een opdrachtpromptvenster te openen en te typen `ipconfig`. Let op het IPV4-adres en wijst deze toe aan de **iPAddress** variabele. |
| nodeTypeRef |Elk knooppunt kan worden toegewezen als een ander knooppunt-type. De [knooppunttypen](#nodetypes) zijn gedefinieerd in de onderstaande sectie. |
| faultDomain |Domeinen met fouten inschakelen clusterbeheerders voor het definiëren van fysieke knooppunten die op hetzelfde moment als gevolg van gedeelde fysieke afhankelijkheden kunnen mislukken. |
| upgradeDomain |Upgradedomeinen beschrijven sets met knooppunten die Service Fabric-upgrades op rond dezelfde tijd worden afgesloten. U kunt welke knooppunten toewijzen aan welke upgradedomeinen als ze niet door de fysieke vereisten beperkt worden. |

## <a name="cluster-properties"></a>Eigenschappen van cluster
De **eigenschappen** sectie in het ClusterConfig.JSON wordt gebruikt voor het configureren van het cluster als volgt.

<a id="reliability"></a>

### <a name="reliability"></a>Betrouwbaarheid
Het concept van **reliabilityLevel** definieert het aantal replica's of exemplaren van de Service Fabric-systeemservices die kunnen worden uitgevoerd op de primaire knooppunten van het cluster. Het bepalen van de betrouwbaarheid van deze services en is daarom het cluster. De waarde is berekende door het systeem tijdens het cluster maken en de upgrade.

### <a name="diagnostics"></a>Diagnostiek
De **diagnosticsStore** sectie kunt u parameters wilt configureren om in te schakelen van diagnostische gegevens en het oplossen van problemen knooppunt of cluster fouten, zoals wordt weergegeven in het volgende fragment. 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

De **metagegevens** is een beschrijving van uw cluster diagnostische gegevens en conform de instelling voor de installatie kan worden ingesteld. Deze variabelen helpen bij het verzamelen van ETW traceerlogboeken, crashdumps, evenals prestatiemeteritems. Lees [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) en [ETW-tracering](https://msdn.microsoft.com/library/ms751538.aspx) traceerlogboeken voor meer informatie over ETW. Alle logboeken, met inbegrip van [dumpbestanden Crash](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) en [prestatiemeteritems](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) kunnen worden omgeleid naar de **connectionString** map op uw computer. U kunt ook *AzureStorage* voor het opslaan van diagnostische gegevens. Hieronder vindt u een voorbeeld-fragment.

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Beveiliging
De **beveiliging** sectie nodig is voor een veilige zelfstandige Service Fabric-cluster. Het volgende fragment toont een deel van deze sectie.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

De **metagegevens** is een beschrijving van uw beveiligde cluster en conform de instelling voor de installatie kan worden ingesteld. De **ClusterCredentialType** en **ServerCredentialType** , bepalen het type dat door het cluster en de knooppunten gaat implementeren. Ze kunnen worden ingesteld op *X509* voor een beveiliging op basis van certificaten of *Windows* voor een Azure Active Directory gebaseerde beveiliging. De rest van de **beveiliging** sectie wordt gebaseerd op het type van de beveiliging. Lees [beveiliging op basis van certificaten in een zelfstandige cluster](service-fabric-windows-cluster-x509-security.md) of [Windows-beveiliging in een zelfstandige cluster](service-fabric-windows-cluster-windows-security.md) voor informatie over het invullen van de rest van de **beveiliging** sectie.

<a id="nodetypes"></a>

### <a name="node-types"></a>Knooppunttypen
De **nodeTypes** sectie worden beschreven van het type van de knooppunten met uw cluster. Ten minste één knooppunttype moet worden opgegeven voor een cluster, zoals wordt weergegeven in het onderstaande codefragment. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

De **naam** is de beschrijvende naam voor dit knooppunttype. Wijs de beschrijvende naam op voor het maken van een knooppunt van dit knooppunttype de **nodeTypeRef** variabele voor dat knooppunt, zoals vermeld [hierboven](#clusternodes). Definieer de eindpunten van de verbinding die wordt gebruikt voor elk knooppunttype. U kunt een ander poortnummer op voor deze verbindingseindpunten, zolang ze niet met een andere eindpunten in dit cluster conflicteren. In een cluster met meerdere knooppunten zal er een of meer primaire knooppunten (dat wil zeggen **isPrimary** ingesteld op *true*), afhankelijk van de [ **reliabilityLevel** ](#reliability). Lees [Service Fabric-cluster overwegingen bij capaciteitsplanning](service-fabric-cluster-capacity.md) voor meer informatie over **nodeTypes** en **reliabilityLevel**, en om te weten wat zijn primaire en de typen van niet-primaire knooppunten. 

#### <a name="endpoints-used-to-configure-the-node-types"></a>Eindpunten die worden gebruikt voor het configureren van de knooppunttypen
* *clientConnectionEndpointPort* is de poort die wordt gebruikt door de client verbinding maken met het cluster bij gebruik van de client-API. 
* *clusterConnectionEndpointPort* is de poort die de knooppunten met elkaar communiceren.
* *leaseDriverEndpointPort* is de poort die wordt gebruikt door het stuurprogramma van de lease cluster om te controleren of de knooppunten nog steeds actief zijn. 
* *serviceConnectionEndpointPort* is de poort die wordt gebruikt door de toepassingen en services die zijn geïmplementeerd op een knooppunt, om te communiceren met de Service Fabric-client op dat specifieke knooppunt.
* *httpGatewayEndpointPort* is de poort die wordt gebruikt door de Service Fabric Explorer verbinding maken met het cluster.
* *ephemeralPorts* overschrijven de [dynamische poorten gebruikt door het besturingssysteem](https://support.microsoft.com/kb/929851). Service Fabric gebruikt een deel van deze poorten als toepassing poorten en de resterende beschikbaar zullen zijn voor het besturingssysteem. Dit wordt ook dit bereik toewijzen aan het bestaande bereik aanwezig is in het besturingssysteem, zodat u de adresbereiken die zijn opgegeven in de JSON-voorbeeldbestanden voor alle doeleinden gebruiken kunt. U moet ervoor zorgen dat het verschil tussen de begin- en end-poorten ten minste 255 is. U kunt uitvoeren in conflicten als dit verschil te laag, omdat dit bereik wordt gedeeld met het besturingssysteem. Zie het geconfigureerde dynamisch poortbereik door het uitvoeren van `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* zijn de poorten die worden gebruikt door de Service Fabric-toepassingen. Het poortbereik van toepassing moet groot genoeg is voor het eindpunt behoefte van uw toepassingen. Dit bereik moet exclusieve uit het bereik van de dynamische poort op de machine, dat wil zeggen de *ephemeralPorts* bereik zoals ingesteld in de configuratie.  Service Fabric Gebruik deze wanneer nieuwe poorten zijn vereist, evenals zorgt voor het openen van de firewall voor deze poorten. 
* *reverseProxyEndpointPort* is een optionele reverse proxy-eindpunt. Zie [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) voor meer informatie. 

### <a name="log-settings"></a>Logboekinstellingen
De **fabricSettings** sectie kunt u de hoofdmappen voor de Service Fabric-gegevens en logboekbestanden instellen. U kunt deze alleen tijdens het maken van het oorspronkelijke cluster. Hieronder vindt u een voorbeeld-fragment van deze sectie.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

Het is raadzaam om een niet-OS-station gebruiken als de FabricDataRoot en FabricLogRoot aangezien deze biedt dat meer betrouwbaarheid tegen OS is vastgelopen. Houd er rekening mee dat als u alleen de gegevenshoofdmap wilt aanpassen, klikt u vervolgens de hoofdmap van het logboek wordt geplaatst één niveau onder de gegevenshoofdmap.

### <a name="stateful-reliable-service-settings"></a>Stateful betrouwbare Service-instellingen
De **KtlLogger** sectie kunt u de globale configuratie-instellingen voor Reliable Services. Lees voor meer informatie over deze instellingen [stateful betrouwbare services configureren](service-fabric-reliable-services-configuration.md).
Het volgende voorbeeld ziet u het wijzigen van de het gedeelde transactielogboek die wilt maken van een betrouwbare verzamelingen voor stateful services wordt gemaakt.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Extra functies
Voor het configureren van extra functies van de apiVersion moet worden geconfigureerd als '-04-2017' of hoger en addonFeatures moet worden geconfigureerd:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Container-ondersteuning
De functie van de invoegtoepassing 'DnsService' moet worden ingeschakeld zodat de container-ondersteuning voor windows server-container en hyper-v-container voor zelfstandige clusters.


## <a name="next-steps"></a>Volgende stappen
Zodra u een volledig ClusterConfig.JSON-bestand dat is geconfigureerd volgens de instellingen van uw zelfstandige cluster hebt, kunt u uw cluster implementeren door het artikel [maken van een zelfstandige Service Fabric-cluster](service-fabric-cluster-creation-for-windows-server.md) en ga verder met [ uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

