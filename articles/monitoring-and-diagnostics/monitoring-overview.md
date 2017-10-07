---
title: aaaMonitoring in Microsoft Azure | Microsoft Docs
description: Opties als u toomonitor alles in Microsoft Azure wilt. Monitor voor Azure, Application Insights Log Analytics
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Overzicht van de bewaking in Microsoft Azure
Dit artikel bevat een overzicht van hulpprogramma's die beschikbaar zijn voor het bewaken van Microsoft Azure. Toepassing te
- bewaking van toepassingen die worden uitgevoerd in Microsoft Azure 
- services of hulpprogramma's die worden uitgevoerd buiten Azure waarop objecten in Azure, kunt bewaken. 

Wordt besproken Hallo verschillende producten en services die beschikbaar zijn en hoe ze samenwerken. Dit kan u helpen toodetermine welke programma's zijn het meest geschikt is voor u in welke gevallen.  

## <a name="why-use-monitoring-and-diagnostics"></a>Waarom controle en diagnostische gegevens gebruiken?

Prestatieproblemen in uw cloud-app kunnen invloed hebben op uw bedrijf. Degradations kan met meerdere onderdelen onderling verbonden en releases vaak gebeuren op elk gewenst moment. En als u een app ontwikkelt, uw gebruikers problemen die u hebt niet vinden in het testen van meestal te detecteren. U moet weten over deze problemen direct en hulpprogramma's voor het opsporen en oplossen van problemen Hallo hebben. Microsoft Azure is een reeks hulpmiddelen om deze problemen te identificeren.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>Hoe bewaak ik mijn Azure-cloud-apps?

Er is een reeks hulpmiddelen voor het bewaken van Azure-toepassingen en services. Enkele van hun functies overlappen. Dit is gedeeltelijk omwille van de historische en deels vanwege toohello zorgt voor een vervaging tussen ontwikkeling en de werking van een toepassing. 

Hier volgen Hallo principal hulpprogramma's:

-   **Monitor voor Azure** is basic hulpprogramma voor het bewaken van services die worden uitgevoerd op Azure. Dit biedt u niveau van de infrastructuur gegevens over de doorvoer van een service en de omgeving rondom Hallo Hallo. Als u uw apps in Azure beheert, moet u bepalen of tooscale omhoog of omlaag bronnen, Azure Monitor u krijgt dan wat u toostart.

-   **Application Insights** kunnen worden gebruikt voor ontwikkeling en als een productie-bewakingsoplossing. Deze werkt met een pakket in uw app installeert en biedt dus een meer interne weergave van wat er gebeurt. De gegevens omvatten reactietijden van afhankelijkheden, uitzondering traceringen, foutopsporing van momentopnamen, profielen kan worden uitgevoerd. Het biedt krachtige smart tools voor het analyseren van alle telemetrie deze beide toohelp u fouten opsporen in een app en u begrijpt wat gebruikers doen met het toohelp. U kunt zien of een piek in de reactietijden vervalt toosomething in een app, of een bepaalde externe resourcing probleem. Als u Visual Studio gebruiken en het Hallo-app beschadigd is, kunt u geleid rechts toohello probleem regel (s) van code zodat u deze kunt oplossen.  

-   **Meld u Analytics** voor degenen die tootune prestaties en plan onderhoud van toepassingen die worden uitgevoerd in de productieomgeving nodig is. In Azure is gebaseerd. Deze verzamelt en gegevens uit diverse bronnen al met een vertraging van 10 too15 minuten worden verzameld. Dit biedt een holistische oplossing voor IT-beheer voor Azure, on-premises en cloud-gebaseerde infrastructuur hebben van derden (zoals Amazon Web Services). Het biedt uitgebreidere extra tooanalyze gegevens over meer bronnen, kunt u complexe query's via alle logboeken en proactief kan waarschuwing bij de opgegeven voorwaarden.  U kunt ook aangepaste gegevens verzamelen in de centrale opslagplaats zodat kunnen opvragen en visualiseren van deze. 

-   **System Center Operations Manager (SCOM)** is voor het beheren en controleren van grote cloud-installaties. U mogelijk al bekend bent met het beheerprogramma voor on-premises Windows Server en op basis van Hyper-V-clouds, maar het kan ook integreren met en beheren van apps van Azure. Onder andere kan Application Insights worden geïnstalleerd op bestaande live apps.  Als een app uitgeschakeld wordt, krijgt u in seconden. Houd er rekening mee dat Log Analytics SCOM niet vervangen. Dit werkt goed in combinatie met deze.  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>Toegang tot de bewaking in hello Azure-portal
Alle Azure-bewaking services zijn nu beschikbaar in één UI deelvenster. Voor meer informatie over het tooaccess dit gebied Zie [aan de slag met Azure Monitor](monitoring-get-started.md). 

U kunt bewaking functies voor specifieke resources ook openen door te selecteren die bronnen en inzoomen op hun controle-opties. 

## <a name="examples-of-when-toouse-which-tool"></a>Voorbeelden van wanneer toouse die hulpprogramma 

Hallo uit te voeren ziet u enkele algemene scenario's en welke hulpprogramma's moeten samen worden gebruikt. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>Scenario 1: Fix fouten in een Azure-toepassing in ontwikkeling   

**de beste optie Hallo is toouse Application Insights, Azure bewaken en Visual Studio samen**

Azure biedt nu Hallo alle mogelijkheden van de foutopsporingsfunctie Hallo in Hallo cloud. Monitor voor Azure toosend telemetrie tooApplication Insights configureren. Visual Studio tooinclude Hallo Application Insights-SDK in uw toepassing inschakelen. Wanneer in Application Insights, kunt u Hallo toepassingstoewijzing toodiscover visueel zijn welke onderdelen van uw actieve toepassing slecht of niet. Voor de onderdelen die niet in orde, zijn fouten en uitzonderingen al beschikbaar voor onderzoek. U kunt verschillende analyses in Application Insights toogo diepere Hallo. Als u niet zeker weet over Hallo fout, kunt u Hallo Visual Studio foutopsporingsprogramma tootrace in code en pincode punt een probleem verder. 

Zie voor meer informatie [Web-Apps bewaken](../application-insights/app-insights-azure-web-apps.md) en Raadpleeg toohello inhoudsopgave op Hallo links voor instructies over de verschillende typen apps en talen.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>Scenario 2: fouten opsporen in een webtoepassing Azure .NET voor fouten die alleen in productie weergeven 

> [!NOTE]
> Deze functies zijn Preview-versie. 

**Hallo aanbevolen optie toouse Application Insights is en indien mogelijk Visual Studio voor Hallo volledige foutopsporingsgegevens ervaring.**

Hallo Application Insights momentopname foutopsporingsprogramma toodebug uw app gebruiken. Wanneer een bepaalde drempelwaarde voor fout met onderdelen van de productie optreedt, vastgelegd Hallo systeem automatisch telemetrie in windows van keer aangeroepen "momentopnamen." Hallo vastgelegd bedrag is veilig voor een productie-cloud omdat deze klein is genoeg niet tooaffect prestaties, maar genoeg aanzienlijke tooallow tracering.  Hallo-systeem kan meerdere momentopnamen vastleggen. U kunt zoeken op een punt in tijd in hello Azure-portal of Visual Studio gebruiken voor volledige Hallo-ervaring. Met Visual Studio kunnen ontwikkelaars doorlopen die momentopname alsof ze zijn foutopsporing in realtime. Lokale variabelen, parameters, geheugen en frames zijn allemaal beschikbaar. Ontwikkelaars moeten toegang toothis productiegegevens via een RBAC-rol worden toegekend.  

Zie voor meer informatie [foutopsporing in momentopname](../application-insights/app-insights-snapshot-debugger.md). 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>Scenario 3: fouten opsporen in een Azure-toepassing die gebruikmaakt van containers of microservices 

**Hetzelfde als scenario 1. Application Insights, Azure bewaken en Visual Studio samen gebruiken** Application Insights biedt ook ondersteuning voor verzamelen telemetrie uit de processen die worden uitgevoerd binnen de containers en microservices (Kubernetes, Docker, Azure Service Fabric). Voor meer informatie [deze video bekijken in het foutopsporingsprogramma containers en microservices](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>Scenario 4: prestaties van de oplossing problemen in uw Azure-toepassing

Hallo [Application Insights profiler](../application-insights/app-insights-profiler.md) is ontworpen toohelp oplossen van problemen. U kunt identificeren en oplossen van prestatieproblemen voor toepassingen die worden uitgevoerd in App Services (Web-Apps, Logic Apps, Mobile Apps, API-Apps) en andere compute-bronnen zoals virtuele Machines, virtuele machine-schaalsets (VMSS), Cloud Services en de Service Fabric. 

> [!NOTE]
> Mogelijkheid tooprofile virtuele Machines, virtuele-machineschaalsets (VMSS), Cloud Services en -Services Fabric is een Preview-versie.   

Bovendien u proactief een melding per e-mail over bepaalde soorten fouten, zoals laadtijden voor pagina langzaam, door Hallo Slimme detectie hulpprogramma.  U hoeft niet toodo configuratie over dit hulpprogramma. Zie voor meer informatie [Slimme detectie - afwijkingen](../application-insights/app-insights-proactive-performance-diagnostics.md) en [Slimme detectie - afwijkingen](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview).



## <a name="next-steps"></a>Volgende stappen
Meer informatie over

* [Azure Monitor in een video Ignite 2016](https://myignite.microsoft.com/videos/4977)
* [Aan de slag met Azure Monitor](monitoring-get-started.md)
* [Azure Diagnostics](../azure-diagnostics.md) als u toodiagnose problemen in uw Cloud-Service, de virtuele Machine probeert virtuele machine instellen of de Service Fabric-toepassing schalen.
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) als u toodiagnostic problemen in uw App Service-Web-app probeert.
* [Meld u Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) en Hallo [Operations Management Suite](https://www.microsoft.com/oms/) bewakingsoplossing productie