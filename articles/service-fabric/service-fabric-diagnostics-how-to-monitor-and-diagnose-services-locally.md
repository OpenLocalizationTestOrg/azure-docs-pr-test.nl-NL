---
title: aaaDebug Azure microservices in Windows | Microsoft Docs
description: Meer informatie over hoe toomonitor en onderzoeken van uw services die zijn geschreven met behulp van Microsoft Azure Service Fabric op een lokale ontwikkelcomputer.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Controle en diagnose van services in de instellingen voor een lokale computer-ontwikkeling
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

Wacht tot services toocontinue met minimale onderbrekingen toohello gebruikerservaring bewaking, detecteren, onderzoeken en het oplossen van problemen. Controle en diagnostische gegevens zijn essentieel belang is in een werkelijke geïmplementeerde productie-omgeving, afhankelijk Hallo efficiëntie van een vergelijkbaar model overstap tijdens de ontwikkeling van services tooensure die ze werken wanneer u tooa echte setup verplaatst. Service Fabric eenvoudig service ontwikkelaars tooimplement diagnostics dat naadloos voor zowel lokale ontwikkeling één machine-instellingen als de echte productie cluster instellingen werkt.

## <a name="event-tracing-for-windows"></a>Gebeurtenistracering voor Windows
[Event Tracing voor Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) is een technologie voor tracering van berichten in Service Fabric aanbevolen Hallo. Er zijn enkele voordelen van het gebruik van ETW:

* **ETW is snel.** Het is ontwikkeld als een tracering technologie met minimale gevolgen voor een uitvoeringstijden code.
* **ETW-tracering werkt naadloos samen in lokale ontwikkelomgevingen en ook instellingen echte cluster.** Dit betekent dat u hebt geen toorewrite uw tracering code wanneer u bent klaar toodeploy uw code tooa echte cluster.
* **Service Fabric systeemcode gebruikt ook ETW voor interne tracering.** Hiermee kunt u uw toepassingstraceringen interleaved met Service Fabric system traceringen tooview. Het helpt tevens toomore u gemakkelijk Hallo reeksen en relaties tussen uw toepassingscode en gebeurtenissen in de onderliggende systeem Hallo begrijpen.
* **Er is ondersteuning voor ingebouwde in Service Fabric Visual Studio tools tooview ETW-gebeurtenissen.** ETW-gebeurtenissen worden weergegeven in Hallo weergave van diagnostische gebeurtenissen van Visual Studio als Visual Studio correct is geconfigureerd met Service Fabric. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Service Fabric-systeemgebeurtenissen bekijken in Visual Studio
Service Fabric verzendt ETW-gebeurtenissen toohelp toepassingsontwikkelaars begrijpen wat er gebeurt in Hallo-platform. Als u dit nog niet hebt gedaan, gaat u verder gaan en Hallo stappen in [maken van uw eerste toepassing in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md). Deze informatie kunt u een toepassing krijgt actief en werkend met Hallo diagnostische gegevens van de gebeurtenisviewer Hallo traceringsberichten weergegeven.

1. Als Hallo diagnostische gebeurtenissen venster wordt niet automatisch wordt weergegeven, gaat u toohello **weergave** tabblad in Visual Studio, kiest u **overige vensters** en vervolgens **diagnostische logboeken**.
2. Elke gebeurtenis heeft vertelt u Hallo knooppunt, toepassing en service Hallo gebeurtenis afkomstig is van informatie over standard metagegevens. U kunt ook Hallo lijst met gebeurtenissen filteren met behulp van Hallo **gebeurtenissen filteren** vak bovenaan Hallo Hallo gebeurtenissen venster. Bijvoorbeeld, u kunt filteren op **knooppuntnaam** of **servicenaam.** En wanneer u de details van gebeurtenis kijkt, kunt u ook onderbreken met behulp van Hallo **onderbreken** knop bovenaan Hallo Hallo gebeurtenissen venster en later hervatten zonder verlies van gebeurtenissen.
   
   ![Visual Studio diagnostische gegevens van de Gebeurtenissenviewer](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Uw eigen aangepaste traceringen toohello toepassingscode toevoegen
Hallo Service Fabric Visual Studio-projectsjablonen bevatten voorbeeldcode. Hallo code laat zien hoe aangepaste toepassingscode tooadd ETW waarvoor traceert omhoog in Visual Studio ETW-viewer Hallo naast system traces van Service Fabric. Hallo voordeel van deze methode is dat metagegevens, wordt automatisch toegevoegd tootraces en Hallo Visual Studio diagnostische logboeken al is geconfigureerd toodisplay ze.

Voor projecten gemaakt op basis van Hallo **servicesjablonen** (stateless of stateful) alleen zoeken naar Hallo `RunAsync` implementatie:

1. Hallo aanroep te`ServiceEventSource.Current.ServiceMessage` in Hallo `RunAsync` methode toont een voorbeeld van een aangepaste ETW-tracering van Hallo-toepassingscode.
2. In Hallo **ServiceEventSource.cs** -bestand, vindt u een overbelasting voor Hallo `ServiceEventSource.ServiceMessage` methode die moet worden gebruikt voor hoge frequentie gebeurtenissen vanwege tooperformance redenen.

Voor projecten gemaakt op basis van Hallo **actor sjablonen** (stateless of stateful):

1. Open Hallo **'ProjectName'.cs** waar het bestand *ProjectName* Hallo-naam die u hebt gekozen voor Visual Studio-project.  
2. Hallo code zoeken `ActorEventSource.Current.ActorMessage(this, "Doing Work");` in Hallo *DoWorkAsync* methode.  Dit is een voorbeeld van een aangepaste ETW-tracering van toepassingscode geschreven.  
3. In het bestand **ActorEventSource.cs**, vindt u een overbelasting voor Hallo `ActorEventSource.ActorMessage` methode die moet worden gebruikt voor hoge frequentie gebeurtenissen vanwege tooperformance redenen.

Na het toevoegen van aangepaste ETW tooyour servicecode tracering kunt u bouwen, implementeren en toepassing hello uitvoeren opnieuw toosee uw gebeurtenis(sen) in Hallo diagnostische logboeken. Als u fouten opsporen in de toepassing hello met **F5**, Hallo diagnostische Gebeurtenissenviewer wordt automatisch geopend.

## <a name="next-steps"></a>Volgende stappen
Hallo werken dezelfde tracering-code die u hebt toegevoegd tooyour toepassing hierboven voor lokale diagnostische gegevens met hulpprogramma's waarmee u tooview kunt deze gebeurtenissen wanneer uw toepassing wordt uitgevoerd op een Azure-cluster. Bekijk deze artikelen die Hallo verschillende opties voor Hallo-hulpprogramma's worden behandeld en wordt beschreven hoe u kunt deze instellen.

* [Hoe toocollect logboeken met diagnostische Azure-gegevens](service-fabric-diagnostics-how-to-setup-wad.md)
* [Gebeurtenis-aggregatie en verzameling op basis van EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)

