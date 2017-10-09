---
title: Analyse van Service Fabric-gebeurtenis met OMS aaaAzure | Microsoft Docs
description: Meer informatie over het visualiseren en analyseren van gebeurtenissen met OMS voor controle en diagnostische gegevens van Azure Service Fabric-clusters.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>Analyse van gebeurtenis en visualisatie met OMS

Operations Management Suite (OMS) is een verzameling van de management-services die u bij de controle en diagnostische gegevens voor toepassingen helpen en services die worden gehost in Hallo cloud. lezen van een meer gedetailleerd overzicht van OMS en het biedt, tooget [wat OMS is?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>Meld u Analytics en Hallo OMS-werkruimte

Log Analytics verzamelt gegevens van beheerde bronnen, met inbegrip van de tabel van een Azure-opslag of een agent en onderhoudt dat bij een centrale opslagplaats. Hallo-gegevens kunnen vervolgens worden gebruikt voor analyse, waarschuwingen en visualisatie of meer geëxporteerd. Log Analytics ondersteunt gebeurtenissen, prestatiegegevens of andere aangepaste gegevens.

Wanneer OMS is geconfigureerd, hebt u toegang tooa specifieke *OMS-werkruimte*, uit waarbij gegevens kunnen worden opgevraagd of weergegeven in dashboards.

Nadat de gegevens worden ontvangen door logboekanalyse OMS heeft diverse *beheeroplossingen* die voorverpakte oplossingen toomonitor binnenkomende gegevens, aangepaste tooseveral scenario's zijn. Deze omvatten een *Service Fabric Analytics* oplossing en een *Containers* oplossing Hallo twee meest relevante resultaten toodiagnostics en bewaking bij gebruik van Service Fabric-clusters. Er zijn verschillende evenals met waard en OMS ook kan voor het maken van aangepaste oplossingen die u kunt meer lezen over Hallo [hier](../operations-management-suite/operations-management-suite-solutions.md). Elke oplossing toouse te kiezen voor een cluster worden geconfigureerd in Hallo dezelfde OMS-werkruimte, samen met logboekanalyse. Werkruimten kunnen u aangepaste dashboards en visualisatie van gegevens, en wijzigingen toohello gegevens die u wilt dat toocollect, verwerken en analyseren.

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>Instellen van een OMS-werkruimte Hello Service Fabric-oplossing

Het wordt aangeraden dat u Hallo Service Fabric-oplossing opnemen in de OMS-werkruimte, omdat het een handig dashboard biedt waarin Hallo verschillende binnenkomende logboekkanalen vanaf niveau voor het platform en toepassing van Hallo en Hallo kunnen tooquery Service Fabric specifieke de logboeken. Hier ziet u hoe een relatief eenvoudige oplossing voor Service Fabric uitziet, met één toepassing geïmplementeerd op Hallo-cluster:

![OMS SF-oplossing](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

Er zijn twee manieren tooprovision en configureren van een OMS-werkruimte, via een Resource Manager-sjabloon of rechtstreeks uit Azure Marketplace. Hallo voormalige gebruiken wanneer u een cluster implementeert en Hallo laatste als u al een cluster dat is geïmplementeerd met diagnostische gegevens hebt ingeschakeld.

### <a name="deploying-oms-using-a-resource-management-template"></a>OMS met een Resource Management-sjabloon implementeren

Dit gebeurt stadium Hallo cluster maken: wanneer u een cluster met behulp van een Resource Manager-sjabloon, het Hallo-sjabloon implementeren, kunt ook een nieuwe OMS-werkruimte maken, Hallo Service Fabric-oplossing tooit toevoegen en configureer deze tooread gegevens van de juiste opslag Hallo tabellen.

>[!NOTE]
>Voor deze toowork heeft diagnostische gegevens inschakelen om hello Azure storage-tabellen tooexist voor OMS toobe / Log Analytics tooread gegevens in uit.

[Hier](https://azure.microsoft.com/resources/templates/service-fabric-oms/) is een voorbeeldsjabloon die u kunt gebruiken en aanpassen aan de hand van behoefte die wordt uitgevoerd boven acties. In geval van Hallo dat u meer optionaliteit wilt, er enkele meer sjablonen waarmee u verschillende opties zijn, afhankelijk van waar in Hallo proces mogelijk voor het instellen van een OMS-werkruimte: kan worden gevonden op [Service Fabric en OMS sjablonen](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Implementatie met behulp van OMS via Azure Marketplace

Als u liever een OMS-werkruimte tooadd nadat u een cluster hebt geïmplementeerd, Ga tooAzure Marketplace en zoekt u *'Service Fabric Analytics'*. Er moet slechts één resource die wordt weergegeven, binnen Hallo 'Monitoring + Management' categorie hieronder wordt weergegeven:

![OMS SF analyses in de Marketplace](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

Te klikken op **maken** wordt u gevraagd een OMS-werkruimte. Klik op **Selecteer een werkruimte** en vervolgens **Maak een nieuwe werkruimte**. Hallo vereist vermeldingen invullen - Hallo hier enige vereiste is Hallo abonnement voor Service Fabric-cluster en Hallo OMS-werkruimte moet Hallo Hallo dezelfde. Zodra uw vermeldingen zijn geverifieerd, wordt de OMS-werkruimte implementeren in een paar minuten. Tijdens de implementatie is voltooid, wordt Hallo maken van Hallo Service Fabric-oplossing blade nog steeds geopend blijven. Zorg ervoor dat dezelfde werkruimte wordt onder Hallo *OMS-werkruimte* en treffers **maken** onderin Hallo Hallo tooadd Service Fabric-oplossing toohello werkruimte.

## <a name="using-hello-oms-agent"></a>Met behulp van Hallo OMS-Agent

Het verdient aanbeveling toouse EventFlow en af als aggregatieoplossingen omdat ze is toegestaan voor een meer modulaire benadering toodiagnostics en controleren. Bijvoorbeeld, als u de uitvoer van EventFlow toochange wilt, hiervoor geen wijziging tooyour Werkelijke instrumentation, alleen een eenvoudige wijziging tooyour config-bestand. Als u echter tooinvest besluit bij het gebruik van OMS en bereid bent toocontinue voor analyse van gebeurtenis (geen toobe Hallo alleen platform gebruiken in plaats dat deze worden echter ten minste één Hallo-platforms), het is raadzaam dat u kennis met instellen Hallo [</C0>OMS-agent<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md).</span> U moet ook Hallo OMS-agent gebruiken bij het implementeren van containers tooyour cluster, zoals hieronder beschreven.

Hallo-proces om dit te doen is betrekkelijk eenvoudig, omdat u zojuist tooadd Hallo agent hebt als een virtuele-machineschaalset extensie tooyour Resource Manager-sjabloon instellen waarbij u ervoor zorgt dat deze wordt geïnstalleerd op elk van de knooppunten. Een Resource Manager voorbeeldsjabloon Hallo OMS-werkruimte Hello Service Fabric-oplossing (Zie boven) implementeert en Hallo agent tooyour knooppunten toevoegen kan worden gevonden voor clusters met [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) of [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

Hallo voordelen hiervan zijn Hallo volgende:

* Rijkere gegevens op Hallo prestaties tellers en metrische gegevens aan clientzijde
* Eenvoudig tooconfigure gegevens worden verzameld van Hallo cluster en wijzigingen tooit te maken zonder dat uw toepassingen of Hallo cluster, omdat wijzigingen toohello instellingen van de agent Hallo kunnen worden gedaan vanuit Hallo OMS-werkruimte en alleen wordt opnieuw instellen van Hallo-agent automatisch. tooconfigure hello OMS-agent toopick van specifieke prestatiemeteritems, Ga toohello werkruimte **Start > Instellingen > gegevens > Windows-prestatiemeteritems** en kies Hallo gegevens die u toosee verzameld dat wilt
* Gegevens weergegeven sneller dan met toobe opgeslagen voordat deze wordt opgehaald door OMS / Log Analytics
* Bewaking van containers is veel eenvoudiger, omdat deze docker-Logboeken (stdout, stderror moet worden geplaatst) en statistieken (maatstaven voor prestaties op knooppunt en container niveaus ophalen kan)

Hallo-hier belangrijkste overweging is dat omdat deze een agent, wordt deze geïmplementeerd op het cluster naast alle toepassingen, zodat er wordt slechts minimale gevolgen toohello prestaties van uw toepassingen op Hallo-cluster.

## <a name="monitoring-containers"></a>Bewaking van Containers

Wanneer u containers tooa Service Fabric-cluster implementeert, verdient het Hallo cluster is ingesteld met Hallo OMS-agent en tooyour OMS werkruimte tooenable controle en diagnostische gegevens die Hallo Containers oplossing is toegevoegd. Hier ziet u welke oplossing ziet als in een werkruimte eruit Hallo-containers:

![Basic OMS-Dashboard](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

Hallo agent kunt Hallo verzamelen van verschillende container-specifieke-logboeken die kunnen worden opgevraagd in OMS of toovisualized prestatie-indicatoren gebruikt. Hallo logboek typen die zijn verzameld zijn:

* ContainerInventory: geeft informatie over de containerlocatie, naam en installatiekopieën
* ContainerImageInventory: informatie over geïmplementeerde installatiekopieën, met inbegrip van id's of grootten
* ContainerLog: specifieke foutenlogboeken, docker-Logboeken (stdout, enzovoort) en andere items
* ContainerServiceLog: docker-daemon opdrachten die zijn uitgevoerd
* Prestaties: prestatiemeteritems met inbegrip van container cpu, geheugen, netwerkverkeer, schijf-i/o en aangepaste metrische gegevens van Hallo machines hosten

In dit artikel bevat informatie over Hallo stappen vereist tooset up container bewaking voor uw cluster. meer informatie over de OMS-Containers oplossing toolearn uitchecken hun [documentatie](../log-analytics/log-analytics-containers.md).

tooset up Hallo Container oplossing in uw werkruimte, Controleer of er Hallo OMS-agent is geïnstalleerd op uw cluster knooppunten Hallo stappen hierboven vermeld. Zodra Hallo cluster gereed is, implementeert u een tooit container. Voorzien zijn er rekening mee dat de eerste keer een installatiekopie van een container Hallo geïmplementeerde tooa cluster is, duurt het enkele minuten toodownload Hallo afbeelding, afhankelijk van de grootte.

Zoeken in Azure Marketplace *Containers* en maak een resource Containers (onder controle + Management Hallo categorie).

![Containers oplossing toevoegen](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

In stap Hallo maken vraagt het een OMS-werkruimte. Selecteer Hallo die zijn met de bovenstaande Hallo-implementatie gemaakt. Deze stap voegt een oplossing Containers in de OMS-werkruimte en wordt automatisch gedetecteerd door Hallo OMS-agent is geïmplementeerd door Hallo-sjabloon. Hallo-agent wordt gestart met het verzamelen van gegevens op Hallo containers processen in het Hallo-cluster en minder dan 15 minuten of geval is, ziet u Hallo oplossing lichte up met gegevens, zoals in afbeelding Hallo van Hallo dashboard hierboven.


## <a name="next-steps"></a>Volgende stappen

Bekijk Hallo OMS-hulpprogramma's en opties toocustomize die een werkruimte tooyour moet volgen:

* OMS biedt een Gateway (http-doorsturen Proxy) die gebruikt toosend gegevens tooOMS worden kan voor lokale-clusters. Lees meer over die in [verbinden van computers zonder internettoegang tooOMS met Hallo OMS-Gateway](../log-analytics/log-analytics-oms-gateway.md)
* Configureren van OMS tooset up [geautomatiseerde waarschuwingen](../log-analytics/log-analytics-alerts.md) tooaid in detecteren en diagnostische gegevens
* Hello ophalen familiarized [zoeken en uitvoeren van query's in logboek registreren](../log-analytics/log-analytics-log-searches.md) functies die worden aangeboden als onderdeel van logboekanalyse
