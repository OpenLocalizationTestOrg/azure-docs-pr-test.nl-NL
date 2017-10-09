---
title: aaaIntroducing hello Service Fabric-Cluster Resource Manager | Microsoft Docs
description: Een inleiding toohello Service Fabric-Cluster Resource Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>Inleiding tot Hallo Service Fabric-cluster resourcemanager
Traditioneel beheren van IT-systemen of onlineservices bedoeld dat specifieke fysieke of virtuele machines toothose van bepaalde services of systemen. Services zijn ontworpen als lagen. Zou er een laag met 'web' of 'data' of 'opslag'. Toepassingen, zou een messaging-laag waar aanvragen gestroomd en afmelden, evenals een aantal machines toegewezen toocaching hebben. Elke fase of type werkbelasting had toegewezen tooit specifieke machines: Hallo database hebt u een aantal machines toegewezen tooit Hallo webservers enkele. Als een bepaald type werkbelasting Hallo-machines die op te hot toorun werd veroorzaakt, klikt u meer machines met die dezelfde configuratie toothat laag toegevoegd. Echter niet alle werkbelastingen kunnen heel eenvoudig worden uitgebreid - met name met Hallo gegevenslaag zou u meestal machines met een grotere machines vervangen. Eenvoudig. Als een machine is mislukt, dat deel van de algemene toepassing hello uitgevoerd op een lagere capaciteit totdat Hallo machine kan worden hersteld. Nog steeds redelijk eenvoudig (indien niet per se leuk).

Hallo wereld van de service nu echter en softwarearchitectuur is gewijzigd. Het is gebruikelijk dat toepassingen een scale-out-ontwerp hebt vastgesteld. Het is gebruikelijk voor het bouwen van toepassingen met containers of microservices (of beide). Terwijl u nog steeds alleen enkele machines hebt, zijn ze nu niet slechts één exemplaar van een werkbelasting uitgevoerd. Er worden meerdere verschillende werkbelastingen zelfs uitgevoerd op Hallo hetzelfde moment. U hebt nu tientallen verschillende soorten services (geen resources aan een volledige machine verbruikt), mogelijk honderden verschillende exemplaren van deze services. Elk benoemd exemplaar heeft een of meer exemplaren of replica's voor hoge beschikbaarheid (HA). Afhankelijk van de grootte van de Hallo van deze werkbelastingen en hoe bezet zijn en zult u zien met honderden of duizenden computers. 

Plotseling beheren van uw omgeving is niet zo eenvoudig als het enkele machines toegewezen toosingle typen werkbelastingen beheren. Uw servers virtueel zijn en niet langer namen hebben (u hebt gekozen mindsets van [huisdieren toocattle](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) nadat alle). Configuratie is minder over Hallo-machines en meer informatie over Hallo services zelf. Hardware die is toegewezen tooa één exemplaar van een werkbelasting is grotendeels een ding Hallo is afgelopen. Services zelf geworden kleine gedistribueerde systemen die meerdere kleinere delen van basishardware omvatten.

Omdat uw app niet langer een reeks monolieten verdeeld over meerdere lagen is, hebt u nu veel meer combinaties toodeal met. Die bepaalt wat typen werkbelastingen kunnen uitvoeren op welke hardware, of hoeveel? Welke workloads werken goed bij Hallo dezelfde hardware- en die strijdig zijn? U weet wat er op deze machine is uitgevoerd wanneer een machine gaat omlaag hoe doen? Wie is verantwoordelijk om ervoor te zorgen dat de werkbelasting wordt gestart opnieuw uit te voeren? Moet u wachten hello (virtueel)? machine toocome terug of uw werkbelastingen automatisch een failover tooother machines en uitvoering? Menselijke tussenkomst vereist is? Hoe zit het upgrades in deze omgeving?

Als ontwikkelaars en operators in deze omgeving omgaan, gaan we toowant help deze complexiteit te beheren. Een binge verhuur en probeer het toohide Hallo complexiteit met mensen is waarschijnlijk niet de juiste antwoord hello, dus wat we doen?

## <a name="introducing-orchestrators"></a>Inleiding tot orchestrators
Een "Orchestrator" is Hallo algemene term voor een stukje software waarmee beheerders kunnen deze soorten omgevingen beheren. Orchestrators zijn Hallo-onderdelen die in aanvragen nemen zoals "Ik wil graag vijf exemplaren van deze service wordt uitgevoerd op mijn omgeving." Proberen ze toomake Hallo omgeving overeen Hallo gewenst staat, ongeacht wat er gebeurt.

Orchestrators (geen mensen) zijn wat actie ondernemen als een computer uitvalt of een werkbelasting voor een bepaalde reden onverwacht beëindigd. De meeste orchestrators dan alleen te maken met de fout. Andere functies die ze hebben beheert nieuwe implementaties, upgrades verwerking en omgaan met brongebruik en beheeracties. Alle orchestrators zijn fundamenteel over het beheren van sommige gewenste status van de configuratie in Hallo-omgeving. Gewenste toobe kunnen tootell een orchestrator wat u wilt en deze Hallo zware werk. Aurora boven op Mesos, Docker-Datacenter/Docker Swarm Kubernetes en Service Fabric zijn alle voorbeelden van orchestrators. Deze orchestrators worden actief ontwikkelde toomeet Hallo behoeften van de echte werkbelastingen in productieomgevingen. 

## <a name="orchestration-as-a-service"></a>Orchestration als een service
Hallo Cluster Resource Manager is onderdeel van Hallo die verantwoordelijk is voor orchestration in Service Fabric. Hallo Cluster Resource Manager de taak is onderverdeeld in drie delen:

1. Regels afdwingen
2. Uw omgeving te optimaliseren
3. Helpt met andere processen

toosee hoe Hallo Cluster Resource Manager werkt, bekijkt hello Microsoft Virtual Academy video te volgen:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>Het is niet
In traditionele N laag toepassingen is altijd een [Load Balancer](https://en.wikipedia.org/wiki/Load_balancing_(computing)). Dit is meestal een Network Load Balancer (NLB) of een toepassing Load Balancer (ALB), afhankelijk van waar het in de netwerkstack Hallo zat. Sommige netwerktaakverdelers hardwarematige zoals van F5 BigIP aanbieding, anderen zijn op basis van software zoals Microsoft NLB de. In andere omgevingen ziet u mogelijk iets zoals HAProxy, nginx, Istio of Envoy in deze rol. In deze architecturen Hallo-taak van taakverdeling is tooensure staatloze werkbelastingen ontvangen (ongeveer) Hallo dezelfde hoeveelheid werk. Strategieën voor netwerktaakverdeling uiteenlopende laden. Sommige balancers zou elke aanroep van verschillende tooa andere server verzenden. Anderen vastmaken/sessiepersistentie opgegeven. Meer geavanceerde balancers schatting van de daadwerkelijke laadbewerking of reporting tooroute op basis van een aanroep van de verwachte kosten en de huidige machine-werkbelasting gebruiken.

Netwerk balancers of bericht routers geprobeerd tooensure die web/worker laag Hallo bleef ongeveer taakverdeling. Strategieën voor netwerktaakverdeling Hallo gegevenslaag zijn verschillende en afhankelijke op opslagmechanisme Hallo-gegevens. Op gegevens sharding, caching, beheerde weergaven, opgeslagen procedures en andere mechanismen voor store-specifieke vertrouwen Balancing Hallo gegevenslaag.

Hoewel sommige van deze strategieën interessante, is Hallo Service Fabric-Cluster Resource Manager niet iets zoals een network load balancer of een cache. Een Network Load Balancer een compromis tussen de frontends door het verkeer verspreid over frontends. Hallo Service Fabric-Cluster Resource Manager heeft een andere strategie. Fundamenteel, Service Fabric verplaatst *services* toowhere indienen Hallo verstandig verkeer verwacht of toofollow worden geladen. Deze Verplaats bijvoorbeeld services toonodes die momenteel koude omdat Hallo-services die er zijn veel werk niet doen. Hallo knooppunten mogelijk koude omdat Hallo-services die aanwezig waren zijn verwijderd of verplaatst. Als een ander voorbeeld kan Hallo Cluster Resource Manager een service niet op een machine ook verplaatsen. Mogelijk Hallo machine is over toobe bijgewerkt of overbelast is vanwege tooa piek in de verbruik door Hallo-services uitgevoerd. Alernatively, resourcevereisten Hallo-service is mogelijk verhoogd. Als gevolg hiervan er zijn niet voldoende bronnen op deze machine toocontinue uitgevoerd. 

Omdat Hallo Cluster Resource Manager verantwoordelijk is voor het verplaatsen van services rond, bevat deze een andere functie set vergeleken toowhat die u in een network load balancer vinden wilt. Dit komt doordat de netwerktaakverdelers netwerk netwerkverkeer toowhere services al, leveren zijn zelfs als deze locatie niet ideaal is voor het uitvoeren van Hallo-service zelf. Hallo Service Fabric-Cluster Resource Manager veiligheidsmaatregelen fundamenteel verschillende strategieën om ervoor te zorgen dat de Hallo bronnen in Hallo cluster efficiënt worden gebruikt.

## <a name="next-steps"></a>Volgende stappen
- Bekijk voor informatie over het Hallo-architectuur en de informatiestroom binnen Hallo Cluster Resource Manager, [in dit artikel](service-fabric-cluster-resource-manager-architecture.md)
- Hallo Cluster Resource Manager heeft veel opties voor het beschrijven van Hallo-cluster. toofind voor meer informatie over metrische gegevens, Bekijk dit artikel op [met een beschrijving van een Service Fabric-cluster](service-fabric-cluster-resource-manager-cluster-description.md)
- Voor meer informatie over het configureren van services, [informatie over het configureren van Services](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Metrische gegevens zijn hoe Hallo Service Fabric-Cluster Resource Manager beheert gebruiks- en capaciteit in Hallo-cluster. meer informatie over metrische gegevens en hoe tooconfigure ze uitchecken toolearn [in dit artikel](service-fabric-cluster-resource-manager-metrics.md)
- Hallo Cluster Resource Manager werkt met de beheermogelijkheden van Service Fabric. toofind voor meer informatie over deze integratie lezen [in dit artikel](service-fabric-cluster-resource-manager-management-integration.md)
- toofind uit over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, bekijk Hallo artikel op [load balancing](service-fabric-cluster-resource-manager-balancing.md)
