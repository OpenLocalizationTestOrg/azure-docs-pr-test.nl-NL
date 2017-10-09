---
title: aaaAdvanced configuratie voor Windows universele Apps Engagement SDK
description: Geavanceerde configuratieopties voor Azure Mobile Engagement met universele Windows-Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Geavanceerde configuratie voor Windows universele Apps Engagement SDK
> [!div class="op_single_selector"]
> * [Universeel Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

Deze procedure wordt beschreven hoe tooconfigure verschillende configuratieopties voor Azure Mobile Engagement Android-apps.

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>Geavanceerde configuratie
### <a name="disable-automatic-crash-reporting"></a>Automatische crashrapporten uitschakelen
U kunt automatische Hallo-crash rapportagefunctie van Engagement uitschakelen. Klik, wanneer er een niet-verwerkte uitzondering optreedt, Engagement, gebeurt er niets.

> [!WARNING]
> Als u deze functie uitschakelen en vervolgens als een niet-verwerkte-crash in uw app plaatsvindt, Engagement geen Hallo crash verzendt **en** Hallo-sessie en taken niet gesloten.
> 
> 

de automatische crash toodisable rapportage, uw configuratie, afhankelijk van Hallo manier waarop u het gedeclareerd aanpassen:

#### <a name="from-engagementconfigurationxml-file"></a>Van `EngagementConfiguration.xml` bestand
Rapport vastlopen te ingesteld`false` tussen `<reportCrash>` en `</reportCrash>` labels.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Van `EngagementConfiguration` object tijdens runtime
Rapport crash toofalse met behulp van het object EngagementConfiguration ingesteld.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>Uitschakelen van realtime rapportage
Standaard Hallo Engagement servicerapporten Logboeken in realtime. Als uw toepassing wordt vaak logboeken rapporteert, is het beter toobuffer Hallo logboeken en tooreport ze in één keer op regelmatige basis. Dit heet 'burst modus'.

toodo worden dus Hallo-methode aanroept:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hallo-argument is een waarde in **milliseconden**. Aanroepen Hallo methode geen parameters of met de waarde 0 Hallo gewenst tooreactivate Hallo realtime logboekregistratie.

Burst-modus enigszins verhoogt de batterij Hallo maar heeft een invloed op Hallo Engagement-Monitor: alle sessies en taken duur zijn afgerond toohello burst drempelwaarde (dus sessies en korter zijn dan Hallo burst drempelwaarde is mogelijk niet zichtbaar taken). U kunt het beste een ' burst ' drempelwaarde niet langer dan 30000 (30s) gebruikt. Opgeslagen logboeken zijn beperkt too300 items. Als het verzenden te lang is, kunt u sommige logboeken gaan verloren.

> [!WARNING]
> Hallo burst drempelwaarde mag niet geconfigureerde tooa periode kleiner is dan een seconde. Als u doet dit, ziet u een tracering met Hallo fout hello SDK- en automatisch teruggezet op toohello standaardwaarde nul seconden. Deze triggers Hallo SDK tooreport Hallo logboeken realtime.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
