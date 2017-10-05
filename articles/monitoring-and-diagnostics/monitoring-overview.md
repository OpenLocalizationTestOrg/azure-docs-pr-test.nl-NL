---
title: Bewaking in Microsoft Azure | Microsoft Docs
description: Opties wanneer u wilt bewaken alles in Microsoft Azure. Monitor voor Azure, Application Insights Log Analytics
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
ms.openlocfilehash: d4a94a92585420cf92018084437422fd0c66fa2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Overzicht van de bewaking in Microsoft Azure
Dit artikel bevat een overzicht van hulpprogramma's die beschikbaar zijn voor het bewaken van Microsoft Azure. Van toepassing op 
- bewaking van toepassingen die worden uitgevoerd in Microsoft Azure 
- services of hulpprogramma's die worden uitgevoerd buiten Azure waarop objecten in Azure, kunt bewaken. 

Het behandelt de verschillende producten en services die beschikbaar zijn en hoe ze samenwerken. Dit kan helpen u om te bepalen welke programma's zijn het meest geschikt is voor u in welke gevallen.  

## <a name="why-use-monitoring-and-diagnostics"></a>Waarom controle en diagnostische gegevens gebruiken?

Prestatieproblemen in uw cloud-app kunnen invloed hebben op uw bedrijf. Degradations kan met meerdere onderdelen onderling verbonden en releases vaak gebeuren op elk gewenst moment. En als u een app ontwikkelt, uw gebruikers problemen die u hebt niet vinden in het testen van meestal te detecteren. U moet weten over deze problemen direct en hulpprogramma's voor het opsporen en oplossen van de problemen hebben. Microsoft Azure is een reeks hulpmiddelen om deze problemen te identificeren.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>Hoe bewaak ik mijn Azure-cloud-apps?

Er is een reeks hulpmiddelen voor het bewaken van Azure-toepassingen en services. Enkele van hun functies overlappen. Dit is gedeeltelijk omwille van de historische en deels vervaging tussen ontwikkeling en de werking van een toepassing. 

Hier volgen de principal-hulpprogramma's:

-   **Monitor voor Azure** is basic hulpprogramma voor het bewaken van services die worden uitgevoerd op Azure. Dit biedt u niveau van de infrastructuur gegevens over de doorvoer van een service en de omgeving. Als u uw apps in Azure beheert, krijgt bepalen of schaal omhoog of omlaag resources, Azure Monitor u dan gebruik om te starten.

-   **Application Insights** kunnen worden gebruikt voor ontwikkeling en als een productie-bewakingsoplossing. Deze werkt met een pakket in uw app installeert en biedt dus een meer interne weergave van wat er gebeurt. De gegevens omvatten reactietijden van afhankelijkheden, uitzondering traceringen, foutopsporing van momentopnamen, profielen kan worden uitgevoerd. Het biedt krachtige smart tools voor het analyseren van alle deze telemetrie kunt u fouten opsporen in een app, en ook om te begrijpen wat gebruikers doen met het. U kunt zien of een piek in de reactietijden veroorzaakt door iets in een app, of een bepaalde externe resourcing probleem wordt. Als u Visual Studio gebruiken en de app beschadigd is, kunt u geleid rechts op de regel (s) probleem van code zodat u deze kunt oplossen.  

-   **Meld u Analytics** is voor gebruikers die moeten afstemmen van de prestaties en onderhoud plannen van toepassingen die worden uitgevoerd in de productieomgeving. In Azure is gebaseerd. Deze verzamelt en gegevens uit diverse bronnen, maar met een vertraging van 10 tot 15 minuten worden verzameld. Dit biedt een holistische oplossing voor IT-beheer voor Azure, on-premises en cloud-gebaseerde infrastructuur hebben van derden (zoals Amazon Web Services). Het biedt uitgebreidere hulpprogramma's om gegevens te analyseren in meer bronnen, kunt u complexe query's via alle logboeken en proactief waarschuwt van de opgegeven voorwaarden.  U kunt ook aangepaste gegevens verzamelen in de centrale opslagplaats zodat kunnen opvragen en visualiseren van deze. 

-   **System Center Operations Manager (SCOM)** is voor het beheren en controleren van grote cloud-installaties. U mogelijk al bekend bent met het beheerprogramma voor on-premises Windows Server en op basis van Hyper-V-clouds, maar het kan ook integreren met en beheren van apps van Azure. Onder andere kan Application Insights worden geïnstalleerd op bestaande live apps.  Als een app uitgeschakeld wordt, krijgt u in seconden. Houd er rekening mee dat Log Analytics SCOM niet vervangen. Dit werkt goed in combinatie met deze.  


## <a name="accessing-monitoring-in-the-azure-portal"></a>Toegang tot de bewaking in de Azure portal
Alle Azure-bewaking services zijn nu beschikbaar in één UI deelvenster. Zie voor meer informatie over toegang krijgen tot dit gebied [aan de slag met Azure Monitor](monitoring-get-started.md). 

U kunt bewaking functies voor specifieke resources ook openen door te selecteren die bronnen en inzoomen op hun controle-opties. 

## <a name="examples-of-when-to-use-which-tool"></a>Voorbeelden van wanneer u welke hulpprogramma 

De volgende secties ziet u enkele algemene scenario's en welke hulpprogramma's moeten samen worden gebruikt. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>Scenario 1: Fix fouten in een Azure-toepassing in ontwikkeling   

**De beste oplossing is Application Insights, Azure bewaken en Visual Studio samen gebruiken**

Azure biedt nu de kracht van de Visual Studio-foutopsporing in de cloud. Azure-Monitor voor het verzenden van telemetrie naar Application Insights configureren. Visual Studio Application Insights-SDK opnemen in uw toepassing inschakelen. Eenmaal in Application Insights, kunt u de kaart toepassing visueel te ontdekken welke onderdelen van uw toepassing actief zijn beschadigd of niet. Voor de onderdelen die niet in orde, zijn fouten en uitzonderingen al beschikbaar voor onderzoek. U kunt de verschillende analytics in Application Insights dieper. Als u niet zeker weet over de fout, kunt u de foutopsporingsfunctie als u wilt traceren in code en de pincode van een probleem verder. 

Zie voor meer informatie [Web-Apps bewaken](../application-insights/app-insights-azure-web-apps.md) en verwijzen naar de inhoudsopgave links voor instructies over de verschillende typen apps en talen.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>Scenario 2: fouten opsporen in een webtoepassing Azure .NET voor fouten die alleen in productie weergeven 

> [!NOTE]
> Deze functies zijn Preview-versie. 

**De beste optie is het gebruik van Application Insights en als mogelijke Visual Studio voor de volledige foutopsporing optreden.**

Gebruik de Application Insights momentopname foutopsporing fouten opsporen in uw app. Wanneer een bepaalde drempelwaarde voor fout met productieonderdelen optreedt, het systeem automatisch wordt vastgelegd telemetrie in windows van keer aangeroepen "momentopnamen." De hoeveelheid vastgelegd is voor een productie-cloud veilig omdat deze niet te beïnvloeden klein genoeg maar aanzienlijke om toe te staan tracering.  Het systeem kan meerdere momentopnamen vastleggen. U kunt zoeken op een punt in tijd in de Azure portal of Visual Studio gebruiken voor de volledige functionaliteit. Met Visual Studio kunnen ontwikkelaars doorlopen die momentopname alsof ze zijn foutopsporing in realtime. Lokale variabelen, parameters, geheugen en frames zijn allemaal beschikbaar. Ontwikkelaars moeten toegang tot deze productiegegevens via een RBAC-rol worden toegekend.  

Zie voor meer informatie [foutopsporing in momentopname](../application-insights/app-insights-snapshot-debugger.md). 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>Scenario 3: fouten opsporen in een Azure-toepassing die gebruikmaakt van containers of microservices 

**Hetzelfde als scenario 1. Application Insights, Azure bewaken en Visual Studio samen gebruiken** Application Insights biedt ook ondersteuning voor verzamelen telemetrie uit de processen die worden uitgevoerd binnen de containers en microservices (Kubernetes, Docker, Azure Service Fabric). Voor meer informatie [deze video bekijken in het foutopsporingsprogramma containers en microservices](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>Scenario 4: prestaties van de oplossing problemen in uw Azure-toepassing

De [Application Insights profiler](../application-insights/app-insights-profiler.md) is ontworpen voor het oplossen van problemen. U kunt identificeren en oplossen van prestatieproblemen voor toepassingen die worden uitgevoerd in App Services (Web-Apps, Logic Apps, Mobile Apps, API-Apps) en andere compute-bronnen zoals virtuele Machines, virtuele machine-schaalsets (VMSS), Cloud Services en de Service Fabric. 

> [!NOTE]
> De mogelijkheid aan virtuele Machines, virtuele-machineschaalsets (VMSS), Cloud Services en -Services Fabric-profiel is een Preview-versie.   

Bovendien u proactief een melding per e-mail over bepaalde soorten fouten, zoals laadtijden voor pagina langzaam, door het hulpprogramma Slimme detectie.  U hoeft niet te geen instellingen op dit hulpprogramma. Zie voor meer informatie [Slimme detectie - afwijkingen](../application-insights/app-insights-proactive-performance-diagnostics.md) en [Slimme detectie - afwijkingen](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview).



## <a name="next-steps"></a>Volgende stappen
Meer informatie over

* [Azure Monitor in een video Ignite 2016](https://myignite.microsoft.com/videos/4977)
* [Aan de slag met Azure Monitor](monitoring-get-started.md)
* [Azure Diagnostics](../azure-diagnostics.md) als u probeert te analyseren van problemen in uw Cloud-Service, de virtuele Machine virtuele machine instellen of de Service Fabric-toepassing schalen.
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) als u te diagnostische problemen in uw App Service-Web-app probeert.
* [Meld u Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) en de [Operations Management Suite](https://www.microsoft.com/oms/) bewakingsoplossing productie