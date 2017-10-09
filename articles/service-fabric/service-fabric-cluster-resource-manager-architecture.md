---
title: aaaResource Manager-architectuur | Microsoft Docs
description: Een overzicht van architectuur van Service Fabric Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>Overzicht van de cluster resource manager-architectuur
Hallo Service Fabric-Cluster Resource Manager is een centrale service die wordt uitgevoerd in Hallo-cluster. Hiermee worden beheerd Hallo gewenste status van Hallo-services in Hallo-cluster, met name met opzicht tooresource gebruiks- en regels voor de plaatsing. 

toomanage hello bronnen in het cluster, Hallo Service Fabric-Cluster Resource Manager moet beschikken over verschillende soorten informatie:

- Welke services bestaat
- Brongebruik door elke service is de huidige (of standaard) 
- Hallo resterende cluster capaciteit 
- Hallo-capaciteit van Hallo knooppunten in cluster Hallo 
- Hallo hoeveelheid resources verbruikt op elk knooppunt

Hallo brongebruik van een bepaalde service kunt wijzigen na verloop van tijd en meer dan één type resource services meestal interesseren. Alle andere services worden echt fysieke en fysieke resources wordt gemeten. Services kunnen fysieke metrische gegevens zoals verbruik van geheugen en schijfruimte bijhouden. Services kunnen vaker voorkomt, logische metrics - items zoals 'WorkQueueDepth' of 'TotalRequests' hechten. Logische en fysieke metrische gegevens kunnen worden gebruikt in Hallo hetzelfde cluster. Metrische gegevens kunnen worden gedeeld door veel services of specifieke tooa bepaalde service zijn.

## <a name="other-considerations"></a>Andere overwegingen
Hallo-eigenaren en operators van Hallo cluster kunnen afwijken van auteurs in service en toepassing hello of op een minimale weet Hallo dezelfde personen met verschillende rollen. Bij het ontwikkelen van uw toepassing weet u leest over wat is vereist. U hebt een schatting van Hallo resources dit verbruikt en hoe verschillende services moeten worden geïmplementeerd. Hallo weblaag moet toorun op knooppunten blootgesteld toohello Internet, bijvoorbeeld bij het Hallo-database-services niet. Hallo-webservices worden bijvoorbeeld waarschijnlijk beperkt door CPU en het netwerk tijdens het Hallo gegevens laag services voorzichtig meer informatie over het verbruik van geheugen en schijfruimte. Echter Hallo persoon afhandeling van een incident live-site voor de service in productie of die wordt beheerd door een upgrade toohello-service heeft een andere taak toodo en vereist verschillende hulpprogramma's. 

Zowel Hallo-cluster en services zijn dynamisch:

- het aantal knooppunten in cluster Hallo Hallo kunt vergroten of verkleinen
- Knooppunten van verschillende grootte en de typen kunnen worden geleverd en Ga
- Services kunnen worden gemaakt, verwijderd, en hun resourcetoewijzingen van de gewenste en de regels voor de plaatsing wijzigen
- Upgrades of andere beheerbewerkingen kunnen draaien via Hallo-cluster op Hallo-toepassing op infrastructuur niveaus
- Fouten kunnen optreden op elk gewenst moment.

## <a name="cluster-resource-manager-components-and-data-flow"></a>Cluster resource manager-onderdelen en gegevensstroom
Hallo Cluster Resource Manager heeft tootrack Hallo vereisten van elke service en Hallo verbruik van bronnen door elke serviceobject in deze services. Hallo Cluster Resource Manager bestaat uit twee delen van de conceptuele: agents die worden uitgevoerd op elk knooppunt en een fouttolerante-service. Hallo-agents op elk knooppunt bijhouden load rapporten van services, cumulatieve ze en deze regelmatig te melden. Hallo Cluster Resource Manager-service alle Hallo-informatie van de lokale agents Hallo samenvoegt en reageert op basis van de huidige configuratie.

Bekijk Hallo-diagram te volgen:

<center>
![Resource Balancer architectuur][Image1]
</center>

Er zijn veel wijzigingen die kunnen optreden tijdens runtime. Bijvoorbeeld, stel Hallo bedrag van resources voor sommige services wijzigingen, sommige mislukken services verbruiken en sommige knooppunten toevoegen en laat Hallo-cluster. Alle Hallo wijzigingen op een knooppunt zijn geaggregeerd en periodiek verzonden toohello Cluster Resource Manager-service (1,2) waarin ze zijn geaggregeerd opnieuw, geanalyseerd en opgeslagen. Om de paar seconden die service bekijkt hello wijzigingen en bepaalt of de acties die het nodig zijn (3). Het kan bijvoorbeeld merkt dat sommige leeg knooppunten toohello cluster zijn toegevoegd. Als gevolg hiervan besluit toomove sommige services toothose knooppunten. Hallo Cluster Resource Manager kan ziet ook dat een bepaald knooppunt is overbelast of dat bepaalde services is mislukt of verwijderd, resources elders vrijmaken.

Laten we bekijkt hello volgende diagram en kijk wat gebeurt er nu. Laten we bepaalt zeggen dat Hallo Cluster Resource Manager of er wijzigingen nodig zijn. Deze coördineert met andere services (bepaalde Hallo Failover Manager) toomake Hallo benodigde wijzigingen in het systeem. Worden de benodigde opdrachten Hallo toohello juiste knooppunten (4) verzonden. Stel bijvoorbeeld Hallo bronnenbeheerder gemerkt Knooppunt5 is overbelast en dus besloten toomove service B van Knooppunt5 tooNode4. Aan het einde van de Hallo van Hallo herconfiguratie (5) uitziet Hallo cluster:

<center>
![Resource Balancer architectuur][Image2]
</center>

## <a name="next-steps"></a>Volgende stappen
- Hallo Cluster Resource Manager heeft veel opties voor het beschrijven van Hallo-cluster. toofind voor meer informatie over deze Raadpleeg dit artikel op [met een beschrijving van een Service Fabric-cluster](./service-fabric-cluster-resource-manager-cluster-description.md)
- Hallo Cluster Resource Manager van primaire rechten zijn herverdeling Hallo-cluster en het afdwingen van regels voor de plaatsing. Zie voor meer informatie over het configureren van deze problemen [balancing Service Fabric-cluster](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
