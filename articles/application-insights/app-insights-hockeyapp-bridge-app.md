---
title: aaaExploring HockeyApp-gegevens in Azure Application Insights | Microsoft Docs
description: Analyseer gebruik en prestaties van uw app in Azure met Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a>HockeyApp-gegevens in Application Insights verkennen
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) wordt aanbevolen Hallo platform voor het bewaken van live desktop- en mobiele apps. Van HockeyApp, kunt u aangepaste verzenden en telemetrie toomonitor gebruik bijhouden en helpt bij de diagnose (in aanvulling toogetting crashgegevens). Deze stroom telemetrie kan worden opgevraagd met Hallo krachtige [Analytics](app-insights-analytics.md) functie van [Azure Application Insights](app-insights-overview.md). Bovendien kunt u [Hallo aangepaste en tracetelemetrie exporteren](app-insights-export-telemetry.md). Deze functies, tooenable brug waarlangs HockeyApp aangepaste gegevens tooApplication Insights doorstuurt instellen.

## <a name="hello-hockeyapp-bridge-app"></a>Hallo HockeyApp Bridge app
Hallo HockeyApp brug App is Hallo core functie waarmee u tooaccess uw aangepaste HockeyApp en tracering telemetrie in Application Insights via Hallo Analytics en functies voor continue Export. Aangepaste en tracering verzamelde gebeurtenissen per HockeyApp na het maken van Hallo HockeyApp Bridge App Hallo van deze functies toegankelijk zijn. Laten we zien hoe tooset slechts één van deze Apps Bridge.

Open in de HockeyApp, accountinstellingen, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens). Een nieuw token maken of een bestaande hergebruiken. Hallo minimale rechten vereist zijn 'alleen-lezen'. Een kopie van Hallo API token duren.

![Een API HockeyApp-token ophalen](./media/app-insights-hockeyapp-bridge-app/01.png)

Open Hallo Microsoft Azure-portal en [een Application Insights-resource maken](app-insights-create-new-resource.md). Type van de toepassing te instellen 'HockeyApp bridge application':

![Nieuwe Application Insights-resource](./media/app-insights-hockeyapp-bridge-app/02.png)

U hoeft niet tooset een naam - dit automatisch uit de naam van de HockeyApp Hallo worden ingesteld.

Hallo HockeyApp bridge velden worden weergegeven. 

![Geef de velden brug](./media/app-insights-hockeyapp-bridge-app/03.png)

Voer Hallo HockeyApp token die u eerder hebt genoteerd. Deze actie wordt gevuld Hallo 'HockeyApp Application' vervolgkeuzemenu met alle HockeyApp-toepassingen. Selecteer Hallo een gewenste toouse en volledige Hallo overige Hallo velden. 

Open de nieuwe resource Hallo. 

Houd er rekening mee dat Hallo gegevens duurt even voordat toostart stromende.

![Application Insights-resource wachten op gegevens](./media/app-insights-hockeyapp-bridge-app/04.png)

Dat is alles. Aangepaste en tracering verzamelde gegevens in uw app HockeyApp geïnstrumenteerd vanaf dit punt is nu ook beschikbaar tooyou in Hallo Analytics en continue Export functies van Application Insights.

Laten we kort Bekijk elk van deze functies nu beschikbaar tooyou.

## <a name="analytics"></a>Analytische gegevens
Analytics is een krachtig hulpmiddel voor ad-hoc query's naar uw gegevens, zodat u toodiagnose en analyseren van uw Telemetrie en snel hoofdoorzaken en patronen te detecteren.

![Analytische gegevens](./media/app-insights-hockeyapp-bridge-app/05.png)

* [Meer informatie over Analytics](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>Continue export
Continue Export kunt u tooexport uw gegevens in een Azure Blob Storage-container. Dit is erg handig als u tookeep uw gegevens langer dan de bewaarperiode Hallo die momenteel worden aangeboden door Application Insights hebt. U kunt bewaren Hallo gegevens in blob-opslag, verwerken in een SQL-Database of de oplossing van uw voorkeur gegevensopslag.

[Meer informatie over de continue Export](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Volgende stappen
* [Analytics tooyour gegevens toepassen](app-insights-analytics-tour.md)

