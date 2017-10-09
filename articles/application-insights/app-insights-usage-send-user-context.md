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
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="83702-103">Verzenden tooenable gebruik van de gebruiker context optreedt in Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="83702-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="83702-104">Gebruikers bijhouden</span><span class="sxs-lookup"><span data-stu-id="83702-104">Tracking users</span></span>

<span data-ttu-id="83702-105">Application Insights kunt u toomonitor en bijhouden van uw gebruikers via een set hulpprogramma's informatie over het gebruik van product:</span><span class="sxs-lookup"><span data-stu-id="83702-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="83702-106">Gebruikers, sessies, gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="83702-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="83702-107">Trechters</span><span class="sxs-lookup"><span data-stu-id="83702-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="83702-108">Retentie</span><span class="sxs-lookup"><span data-stu-id="83702-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="83702-109">Cohorten</span><span class="sxs-lookup"><span data-stu-id="83702-109">Cohorts</span></span>
* [<span data-ttu-id="83702-110">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="83702-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="83702-111">In de volgorde tootrack wat een gebruiker gedurende een bepaalde periode heeft, moet Application Insights een ID voor elke gebruiker of de sessie.</span><span class="sxs-lookup"><span data-stu-id="83702-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="83702-112">Deze id in elke aangepaste gebeurtenis- of -weergave wilt opnemen.</span><span class="sxs-lookup"><span data-stu-id="83702-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="83702-113">Gebruikers, schoorstenen, bewaren en cohorten: bevatten de gebruikers-ID.</span><span class="sxs-lookup"><span data-stu-id="83702-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="83702-114">Sessies: Omvatten sessie-ID.</span><span class="sxs-lookup"><span data-stu-id="83702-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="83702-115">Als uw app is geïntegreerd met Hallo [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), gebruiker-ID automatisch wordt bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="83702-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="83702-116">Gebruikers-id's kiezen</span><span class="sxs-lookup"><span data-stu-id="83702-116">Choosing user IDs</span></span>

<span data-ttu-id="83702-117">Gebruikers-id's moeten persistent is voor gebruiker sessies tootrack hoe gebruikers zich gedragen gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="83702-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="83702-118">Er zijn verschillende manieren voor persistent maken Hallo-ID.</span><span class="sxs-lookup"><span data-stu-id="83702-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="83702-119">Een definitie van een gebruiker die u al in uw service hebt.</span><span class="sxs-lookup"><span data-stu-id="83702-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="83702-120">Als Hallo-service toegang tot tooa browser heeft, kunt het Hallo-browser een cookie met een ID in het doorgeven.</span><span class="sxs-lookup"><span data-stu-id="83702-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="83702-121">zolang Hallo cookie in de browser van de gebruiker Hallo blijft bewaard Hallo-ID voor.</span><span class="sxs-lookup"><span data-stu-id="83702-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="83702-122">Indien nodig, kunt u een nieuwe ID elke sessie Hallo resultaten over gebruikers worden echter beperkt.</span><span class="sxs-lookup"><span data-stu-id="83702-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="83702-123">Bijvoorbeeld, niet kunnen toosee hoe gedrag van een gebruiker gedurende een bepaalde periode verandert.</span><span class="sxs-lookup"><span data-stu-id="83702-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="83702-124">Hallo-ID moet een Guid of een andere tekenreeks complex genoeg tooidentify elke gebruiker een unieke.</span><span class="sxs-lookup"><span data-stu-id="83702-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="83702-125">Bijvoorbeeld, wordt een lange willekeurig getal.</span><span class="sxs-lookup"><span data-stu-id="83702-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="83702-126">Hallo-ID bevat persoonsgegevens identificatiegegevens over Hallo gebruiker, is het niet als een geschikte waarde toosend tooApplication Insights als een gebruikers-ID.</span><span class="sxs-lookup"><span data-stu-id="83702-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="83702-127">U kunt verzenden dergelijke ID als een [geverifieerde gebruikers-ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), maar deze voldoet niet aan de Hallo gebruiker-ID vereiste voor gebruiksscenario's.</span><span class="sxs-lookup"><span data-stu-id="83702-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="83702-128">ASP.NET-Apps: Gebruikerscontext in een ITelemetryInitializer instellen</span><span class="sxs-lookup"><span data-stu-id="83702-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="83702-129">Maak een initialisatiefunctie telemetrie zoals beschreven in detail [hier](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), en een set Hallo Context.User.Id en Context.Session.Id Hallo.</span><span class="sxs-lookup"><span data-stu-id="83702-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="83702-130">In het volgende voorbeeld wordt de Hallo gebruikers-ID tooan-id die na Hallo-sessie verloopt.</span><span class="sxs-lookup"><span data-stu-id="83702-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="83702-131">Gebruik zo mogelijk een gebruikers-ID dat behouden over de sessies blijft.</span><span class="sxs-lookup"><span data-stu-id="83702-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="83702-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="83702-132">*C#*</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="83702-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="83702-133">Next steps</span></span>
- <span data-ttu-id="83702-134">Gebruik tooenable optreedt, te beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="83702-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="83702-135">Als u al aangepaste gebeurtenissen of paginaweergaven verkennen Hallo gebruik hulpprogramma's voor toolearn verzendt hoe gebruikers de service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="83702-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="83702-136">Overzicht gebruik</span><span class="sxs-lookup"><span data-stu-id="83702-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="83702-137">Gebruikers, sessies en gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="83702-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="83702-138">Trechters</span><span class="sxs-lookup"><span data-stu-id="83702-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="83702-139">Retentie</span><span class="sxs-lookup"><span data-stu-id="83702-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="83702-140">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="83702-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
