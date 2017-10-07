---
title: aaaConfigure uw Azure Service Fabric zelfstandige cluster | Microsoft Docs
description: Meer informatie over hoe tooconfigure uw zelfstandige of persoonlijke Service Fabric-cluster.
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
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Configuratie-instellingen voor zelfstandige Windows-cluster
Dit artikel wordt beschreven hoe een zelfstandige Service Fabric cluster met tooconfigure Hallo ***ClusterConfig.JSON*** bestand. U kunt dit bestand toospecify informatie zoals Hallo Service Fabric-knooppunten en hun IP-adressen, verschillende soorten knooppunten op Hallo-cluster, beveiligingsconfiguraties hello, evenals Hallo netwerktopologie in termen van fouttolerantie/upgrade-domeinen, gebruiken voor uw zelfstandige cluster.

Wanneer u [Hallo zelfstandige Service Fabric-pakket te downloaden](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), een paar voorbeelden van Hallo ClusterConfig.JSON bestand gedownloade tooyour werk machine zijn. Hallo-voorbeelden met *DevCluster* in hun naam helpt u bij het maken van een cluster met alle drie knooppunten op dezelfde computer, zoals logische knooppunten Hallo. Buiten deze, moet ten minste één knooppunt worden gemarkeerd als een primaire knooppunt. Dit cluster is handig voor een omgeving met ontwikkeling of tests en wordt niet ondersteund als een productiecluster. Hallo-voorbeelden met *MultiMachine* in hun naam helpt u bij het maken van een productiecluster kwaliteit met elk knooppunt op een afzonderlijke computer.

1. *ClusterConfig.Unsecure.DevCluster.JSON* en *ClusterConfig.Unsecure.MultiMachine.JSON* laten zien hoe een onbeveiligde test toocreate productie van het cluster of respectievelijk. 
2. *ClusterConfig.Windows.DevCluster.JSON* en *ClusterConfig.Windows.MultiMachine.JSON* tonen hoe toocreate test- of -cluster beveiligd met [Windows-beveiliging](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* en *ClusterConfig.X509.MultiMachine.JSON* tonen hoe toocreate test- of -cluster beveiligd met [X509 beveiliging op basis van certificaat](service-fabric-windows-cluster-x509-security.md). 

Nu gaan we kijken Hallo verschillende secties van een ***ClusterConfig.JSON*** bestand zoals hieronder.

## <a name="general-cluster-configurations"></a>Algemene clusterconfiguraties
Dit heeft betrekking op Hallo brede cluster specifieke configuraties, zoals weergegeven in onderstaande Hallo JSON-codefragment.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

U kunt een beschrijvende naam tooyour Service Fabric-cluster geven door toe te wijzen toohello **naam** variabele. Hallo **clusterConfigurationVersion** Hallo versienummer van het cluster, moet u deze verhogen telkens wanneer u een upgrade uitvoert van Service Fabric-cluster. Laat u echter Hallo **apiVersion** toohello standaardwaarde.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Knooppunten op Hallo-cluster
U kunt Hallo knooppunten op uw Service Fabric-cluster configureren met behulp van Hallo **knooppunten** sectie als Hallo volgende codefragment bevat.

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

Een Service Fabric-cluster moet ten minste 3 knooppunten bevatten. U kunt meer knooppunten toothis sectie toevoegen aan de hand van uw instellingen. Hallo volgende tabel wordt uitgelegd Hallo configuratie-instellingen voor elk knooppunt.

| **Knooppuntconfiguratie** | **Beschrijving** |
| --- | --- |
| nodeName |U kunt een beschrijvende naam toohello knooppunt op te geven. |
| IP-adres |Hallo IP-adres van het knooppunt door een opdrachtpromptvenster te openen en te typen weten `ipconfig`. Houd er rekening mee Hallo IPV4-adres en toe te wijzen toohello **iPAddress** variabele. |
| nodeTypeRef |Elk knooppunt kan worden toegewezen als een ander knooppunt-type. Hallo [knooppunttypen](#nodetypes) zijn gedefinieerd in de onderstaande Hallo-sectie. |
| faultDomain |Fout met betrekking tot domeinen inschakelen beheerders toodefine Hallo fysieke clusterknooppunten die op Hallo mislukken dezelfde tijd vanwege tooshared fysieke afhankelijkheden. |
| upgradeDomain |Upgradedomeinen beschrijven sets met knooppunten die zijn uitgeschakeld voor Service Fabric wordt bijgewerkt op over Hallo dezelfde tijd. U kunt kiezen welke knooppunten tooassign toowhich upgradedomeinen, zoals ze niet door de fysieke vereisten beperkt worden. |

## <a name="cluster-properties"></a>Eigenschappen van cluster
Hallo **eigenschappen** sectie in Hallo ClusterConfig.JSON gebruikte tooconfigure Hallo cluster is als volgt.

<a id="reliability"></a>

### <a name="reliability"></a>Betrouwbaarheid
Hallo-concept van **reliabilityLevel** definieert Hallo aantal replica's of exemplaren van Hallo Service Fabric-systeemservices die kunnen worden uitgevoerd op de primaire knooppunten Hallo van Hallo-cluster. Het bepaalt Hallo betrouwbaarheid van deze services en daarom Hallo cluster. Hallo-waarde is berekende door Hallo systeem gelijktijdig cluster maken en de upgrade.

### <a name="diagnostics"></a>Diagnostiek
Hallo **diagnosticsStore** sectie kunt u tooconfigure parameters tooenable diagnostische gegevens en het oplossen van problemen knooppunt of cluster fouten, zoals wordt weergegeven in het volgende codefragment Hallo. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Hallo **metagegevens** is een beschrijving van uw cluster diagnostische gegevens en conform de instelling voor de installatie kan worden ingesteld. Deze variabelen helpen bij het verzamelen van ETW traceerlogboeken, crashdumps, evenals prestatiemeteritems. Lees [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) en [ETW-tracering](https://msdn.microsoft.com/library/ms751538.aspx) traceerlogboeken voor meer informatie over ETW. Alle logboeken, met inbegrip van [dumpbestanden Crash](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) en [prestatiemeteritems](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) mag gerichte toohello **connectionString** map op uw computer. U kunt ook *AzureStorage* voor het opslaan van diagnostische gegevens. Hieronder vindt u een voorbeeld-fragment.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Beveiliging
Hallo **beveiliging** sectie nodig is voor een veilige zelfstandige Service Fabric-cluster. Hallo volgende fragment toont een deel van deze sectie.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Hallo **metagegevens** is een beschrijving van uw beveiligde cluster en conform de instelling voor de installatie kan worden ingesteld. Hallo **ClusterCredentialType** en **ServerCredentialType** bepalen Hallo type beveiliging Hallo-cluster en Hallo knooppunten gaat implementeren. Ze kunnen worden ingesteld tooeither *X509* voor een beveiliging op basis van certificaten of *Windows* voor een Azure Active Directory gebaseerde beveiliging. Hallo rest Hallo **beveiliging** sectie wordt gebaseerd op Hallo type Hallo-beveiliging. Lees [beveiliging op basis van certificaten in een zelfstandige cluster](service-fabric-windows-cluster-x509-security.md) of [Windows-beveiliging in een zelfstandige cluster](service-fabric-windows-cluster-windows-security.md) voor meer informatie over hoe toofill uit Hallo rest van de Hallo **beveiliging**sectie.

<a id="nodetypes"></a>

### <a name="node-types"></a>Knooppunttypen
Hallo **nodeTypes** sectie wordt beschreven Hallo type Hallo knooppunten die fungeren als uw cluster heeft. Ten minste één knooppunttype moet worden opgegeven voor een cluster, zoals wordt weergegeven in onderstaande Hallo stukje. 

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

Hallo **naam** Hallo beschrijvende naam voor dit knooppunttype is. een knooppunt van dit knooppunttype toocreate toewijzen de beschrijvende naam toohello **nodeTypeRef** variabele voor dat knooppunt, zoals vermeld [hierboven](#clusternodes). Voor elk knooppunttype definiëren Hallo verbindingseindpunten die worden gebruikt. U kunt een ander poortnummer op voor deze verbindingseindpunten, zolang ze niet met een andere eindpunten in dit cluster conflicteren. In een cluster met meerdere knooppunten zal er een of meer primaire knooppunten (dat wil zeggen **isPrimary** instellen te*true*), afhankelijk van Hallo [ **reliabilityLevel** ](#reliability). Lees [Service Fabric-cluster overwegingen bij capaciteitsplanning](service-fabric-cluster-capacity.md) voor meer informatie over **nodeTypes** en **reliabilityLevel**, en tooknow wat zijn de primaire en Hallo typen van niet-primaire knooppunten. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>Eindpunten tooconfigure Hallo knooppunttypen gebruikt
* *clientConnectionEndpointPort* Hallo poort gebruikt door Hallo client tooconnect toohello cluster als u Hallo client-API's. 
* *clusterConnectionEndpointPort* Hallo poort waarop Hallo knooppunten met elkaar communiceren.
* *leaseDriverEndpointPort* Hallo poort wordt gebruikt door Hallo cluster lease stuurprogramma toofind uit als Hallo knooppunten nog steeds actief zijn is. 
* *serviceConnectionEndpointPort* Hallo-poort die wordt gebruikt door Hallo toepassingen en services die zijn geïmplementeerd op een knooppunt, toocommunicate met Hallo Service Fabric-client op dat bepaalde knooppunt is.
* *httpGatewayEndpointPort* Hallo-poort die wordt gebruikt door Hallo Service Fabric Explorer tooconnect toohello cluster is.
* *ephemeralPorts* overschrijven Hallo [dynamische poorten gebruikt door Hallo OS](https://support.microsoft.com/kb/929851). Service Fabric gebruikt een deel van deze poorten als toepassing poorten en Hallo resterende beschikbaar zullen zijn voor Hallo OS. Dit wordt ook deze bereik toohello bestaande bereik toegewezen aanwezig is in Hallo OS, zodat u Hallo bereiken opgegeven in de JSON voorbeeldbestanden Hallo voor alle doeleinden gebruiken kunt. U moet toomake Hallo verschil tussen het Hallo-begin- en end-poorten Hallo moet ten minste 255. U kunt uitvoeren in conflicten als dit verschil te laag, omdat dit bereik wordt gedeeld met Hallo-besturingssysteem. Zie het dynamisch poortbereik Hallo geconfigureerd door te voeren `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* Hallo-poorten die worden gebruikt door Hallo Service Fabric-toepassingen zijn. Hallo toepassingspoortbereik moet groot genoeg toocover Hallo eindpunt vereisten van uw toepassingen. Dit bereik moet exclusieve van Hallo dynamisch poortbereik op Hallo machine, dat wil zeggen Hallo *ephemeralPorts* bereik zoals ingesteld in Hallo-configuratie.  Service Fabric Gebruik deze wanneer nieuwe poorten zijn vereist, evenals behandelen Hallo firewall voor deze poorten te openen. 
* *reverseProxyEndpointPort* is een optionele reverse proxy-eindpunt. Zie [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) voor meer informatie. 

### <a name="log-settings"></a>Logboekinstellingen
Hallo **fabricSettings** sectie kunt u tooset Hallo hoofdmappen voor Hallo Service Fabric-gegevens en logboekbestanden. U kunt deze alleen tijdens het maken van het oorspronkelijke cluster Hallo aanpassen. Hieronder vindt u een voorbeeld-fragment van deze sectie.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

Het is raadzaam om met behulp van een niet-OS-station als Hallo FabricDataRoot en FabricLogRoot, aangezien deze meer betrouwbaarheid tegen OS crashes biedt. Houd er rekening mee dat als u alleen Hallo gegevenshoofdmap wilt aanpassen, klikt u vervolgens Hallo logboek hoofdmap worden geplaatst één niveau onder het Hallo-gegevenshoofdmap.

### <a name="stateful-reliable-service-settings"></a>Stateful betrouwbare Service-instellingen
Hallo **KtlLogger** sectie kunt u tooset Hallo globale configuratie-instellingen voor Reliable Services. Lees voor meer informatie over deze instellingen [stateful betrouwbare services configureren](service-fabric-reliable-services-configuration.md).
Hallo voorbeeld hieronder ziet u hoe toochange Hallo Hallo gedeelde transactielogboek die wordt gemaakt tooback worden betrouwbare verzamelingen voor stateful services.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Extra functies
Extra functies van tooconfigure hello apiVersion moet worden geconfigureerd als '-04-2017' of hoger en addonFeatures moet toobe geconfigureerd:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Container-ondersteuning
tooenable container ondersteuning voor windows server-container en hyper-v-container voor zelfstandige clusters, Hallo 'DnsService' invoegtoepassing functie moet toobe ingeschakeld.


## <a name="next-steps"></a>Volgende stappen
Zodra u een volledig ClusterConfig.JSON-bestand dat is geconfigureerd volgens de instellingen van uw zelfstandige cluster hebt, kunt u uw cluster door volgende Hallo artikel implementeren [maken van een zelfstandige Service Fabric-cluster](service-fabric-cluster-creation-for-windows-server.md) en ga vervolgens verder te[uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

