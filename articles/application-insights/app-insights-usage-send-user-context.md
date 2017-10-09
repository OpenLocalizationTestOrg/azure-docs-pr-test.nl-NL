---
title: aaaSending gebruiker context tooenable gebruik optreedt in Azure Application Insights | Microsoft Docs
description: Bijhouden hoe gebruikers verplaatsen door middel van uw service na het toewijzen van elk van deze een unieke, permanente ID-reeks in Application Insights.
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>Verzenden tooenable gebruik van de gebruiker context optreedt in Azure Application Insights

## <a name="tracking-users"></a>Gebruikers bijhouden

Application Insights kunt u toomonitor en bijhouden van uw gebruikers via een set hulpprogramma's informatie over het gebruik van product: 
* [Gebruikers, sessies, gebeurtenissen](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [Trechters](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [Retentie](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* Cohorten
* [Werkmappen](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

In de volgorde tootrack wat een gebruiker gedurende een bepaalde periode heeft, moet Application Insights een ID voor elke gebruiker of de sessie. Deze id in elke aangepaste gebeurtenis- of -weergave wilt opnemen.
- Gebruikers, schoorstenen, bewaren en cohorten: bevatten de gebruikers-ID.
- Sessies: Omvatten sessie-ID.

Als uw app is geïntegreerd met Hallo [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), gebruiker-ID automatisch wordt bijgehouden.

## <a name="choosing-user-ids"></a>Gebruikers-id's kiezen

Gebruikers-id's moeten persistent is voor gebruiker sessies tootrack hoe gebruikers zich gedragen gedurende een bepaalde periode. Er zijn verschillende manieren voor persistent maken Hallo-ID.
- Een definitie van een gebruiker die u al in uw service hebt.
- Als Hallo-service toegang tot tooa browser heeft, kunt het Hallo-browser een cookie met een ID in het doorgeven. zolang Hallo cookie in de browser van de gebruiker Hallo blijft bewaard Hallo-ID voor.
- Indien nodig, kunt u een nieuwe ID elke sessie Hallo resultaten over gebruikers worden echter beperkt. Bijvoorbeeld, niet kunnen toosee hoe gedrag van een gebruiker gedurende een bepaalde periode verandert.

Hallo-ID moet een Guid of een andere tekenreeks complex genoeg tooidentify elke gebruiker een unieke. Bijvoorbeeld, wordt een lange willekeurig getal.

Hallo-ID bevat persoonsgegevens identificatiegegevens over Hallo gebruiker, is het niet als een geschikte waarde toosend tooApplication Insights als een gebruikers-ID. U kunt verzenden dergelijke ID als een [geverifieerde gebruikers-ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), maar deze voldoet niet aan de Hallo gebruiker-ID vereiste voor gebruiksscenario's.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>ASP.NET-Apps: Gebruikerscontext in een ITelemetryInitializer instellen

Maak een initialisatiefunctie telemetrie zoals beschreven in detail [hier](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), en een set Hallo Context.User.Id en Context.Session.Id Hallo.

In het volgende voorbeeld wordt de Hallo gebruikers-ID tooan-id die na Hallo-sessie verloopt. Gebruik zo mogelijk een gebruikers-ID dat behouden over de sessies blijft.

*C#*

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a>Volgende stappen
- Gebruik tooenable optreedt, te beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Als u al aangepaste gebeurtenissen of paginaweergaven verkennen Hallo gebruik hulpprogramma's voor toolearn verzendt hoe gebruikers de service gebruiken.
    * [Overzicht gebruik](app-insights-usage-overview.md)
    * [Gebruikers, sessies en gebeurtenissen](app-insights-usage-segmentation.md)
    * [Trechters](usage-funnels.md)
    * [Retentie](app-insights-usage-retention.md)
    * [Werkmappen](app-insights-usage-workbooks.md)
