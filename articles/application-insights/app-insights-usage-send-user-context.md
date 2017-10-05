---
title: Verzenden gebruikerscontext gebruiksanalyse moet zijn ingeschakeld in Azure Application Insights optreedt | Microsoft Docs
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
ms.openlocfilehash: 9350029c775643be0dcc679b0f4bb9238b5f8aca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
#  <a name="sending-user-context-to-enable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="fa603-103">Verzenden gebruikerscontext ervaringen gebruik Azure Application Insights inschakelen</span><span class="sxs-lookup"><span data-stu-id="fa603-103">Sending user context to enable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="fa603-104">Gebruikers bijhouden</span><span class="sxs-lookup"><span data-stu-id="fa603-104">Tracking users</span></span>

<span data-ttu-id="fa603-105">Application Insights kunt u om te controleren en bijhouden van uw gebruikers via een set hulpprogramma's informatie over het gebruik van product:</span><span class="sxs-lookup"><span data-stu-id="fa603-105">Application Insights enables you to monitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="fa603-106">Gebruikers, sessies, gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="fa603-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="fa603-107">Trechters</span><span class="sxs-lookup"><span data-stu-id="fa603-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="fa603-108">Retentie</span><span class="sxs-lookup"><span data-stu-id="fa603-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="fa603-109">Cohorten</span><span class="sxs-lookup"><span data-stu-id="fa603-109">Cohorts</span></span>
* [<span data-ttu-id="fa603-110">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="fa603-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="fa603-111">Te houden wat een gebruiker gedurende een bepaalde periode doet, moet een Application Insights een ID voor elke gebruiker of de sessie.</span><span class="sxs-lookup"><span data-stu-id="fa603-111">In order to track what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="fa603-112">Deze id in elke aangepaste gebeurtenis- of -weergave wilt opnemen.</span><span class="sxs-lookup"><span data-stu-id="fa603-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="fa603-113">Gebruikers, schoorstenen, bewaren en cohorten: bevatten de gebruikers-ID.</span><span class="sxs-lookup"><span data-stu-id="fa603-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="fa603-114">Sessies: Omvatten sessie-ID.</span><span class="sxs-lookup"><span data-stu-id="fa603-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="fa603-115">Als uw app is geïntegreerd met de [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), gebruiker-ID automatisch wordt bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="fa603-115">If your app is integrated with the [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="fa603-116">Gebruikers-id's kiezen</span><span class="sxs-lookup"><span data-stu-id="fa603-116">Choosing user IDs</span></span>

<span data-ttu-id="fa603-117">Gebruikers-id's moeten blijven bewaard tussen gebruikerssessies bijhouden hoe gebruikers zich gedragen gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="fa603-117">User IDs should persist across user sessions to track how users behave over time.</span></span> <span data-ttu-id="fa603-118">Er zijn verschillende manieren voor het persistent maken van de-ID.</span><span class="sxs-lookup"><span data-stu-id="fa603-118">There are various approaches for persisting the ID.</span></span>
- <span data-ttu-id="fa603-119">Een definitie van een gebruiker die u al in uw service hebt.</span><span class="sxs-lookup"><span data-stu-id="fa603-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="fa603-120">Als de service toegang tot een browser heeft, kan deze de browser een cookie met een ID in het doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="fa603-120">If the service has access to a browser, it can pass the browser a cookie with an ID in it.</span></span> <span data-ttu-id="fa603-121">De ID bewaard voor, zolang de cookie in de browser van de gebruiker blijft.</span><span class="sxs-lookup"><span data-stu-id="fa603-121">The ID will persist for as long as the cookie remains in the user's browser.</span></span>
- <span data-ttu-id="fa603-122">Indien nodig, wordt kunt u een nieuwe ID elke sessie, maar de resultaten over gebruikers beperkt.</span><span class="sxs-lookup"><span data-stu-id="fa603-122">If necessary, you can use a new ID each session, but the results about users will be limited.</span></span> <span data-ttu-id="fa603-123">Bijvoorbeeld, u niet mogelijk om te zien hoe gedrag van een gebruiker verandert gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="fa603-123">For example, you won't be able to see how a user's behavior changes over time.</span></span>

<span data-ttu-id="fa603-124">De ID moet een Guid of een andere tekenreeks complex genoeg elke gebruiker uniek wordt geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="fa603-124">The ID should be a Guid or another string complex enough to identify each user uniquely.</span></span> <span data-ttu-id="fa603-125">Bijvoorbeeld, wordt een lange willekeurig getal.</span><span class="sxs-lookup"><span data-stu-id="fa603-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="fa603-126">Als de ID persoonlijke gegevens over de gebruiker bevat, is het niet de juiste waarde te verzenden naar Application Insights als een gebruikers-ID.</span><span class="sxs-lookup"><span data-stu-id="fa603-126">If the ID contains personally identifying information about the user, it is not an appropriate value to send to Application Insights as a user ID.</span></span> <span data-ttu-id="fa603-127">U kunt verzenden dergelijke ID als een [geverifieerde gebruikers-ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), maar deze voldoet niet aan de vereisten van de gebruiker-ID voor gebruiksscenario's.</span><span class="sxs-lookup"><span data-stu-id="fa603-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill the user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="fa603-128">ASP.NET-Apps: Gebruikerscontext in een ITelemetryInitializer instellen</span><span class="sxs-lookup"><span data-stu-id="fa603-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="fa603-129">Maak een initialisatiefunctie telemetrie zoals beschreven in detail [hier](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), en stel de Context.User.Id en de Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="fa603-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set the Context.User.Id and the Context.Session.Id.</span></span>

<span data-ttu-id="fa603-130">In het volgende voorbeeld wordt de gebruikers-ID op een id die na de sessie is verlopen.</span><span class="sxs-lookup"><span data-stu-id="fa603-130">This example sets the user ID to an identifier that expires after the session.</span></span> <span data-ttu-id="fa603-131">Gebruik zo mogelijk een gebruikers-ID dat behouden over de sessies blijft.</span><span class="sxs-lookup"><span data-stu-id="fa603-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="fa603-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="fa603-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets the user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on the HttpContext Session.
            // Set the user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set the user id on the Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set the session id on the Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="fa603-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fa603-133">Next steps</span></span>
- <span data-ttu-id="fa603-134">Om in te schakelen ervaringen gebruik, beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="fa603-134">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="fa603-135">Als u al aangepaste gebeurtenissen of paginaweergaven verzendt, gebruik de informatie over het gebruik hulpprogramma's voor meer informatie over hoe gebruikers gebruiken voor uw service.</span><span class="sxs-lookup"><span data-stu-id="fa603-135">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    * [<span data-ttu-id="fa603-136">Overzicht gebruik</span><span class="sxs-lookup"><span data-stu-id="fa603-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="fa603-137">Gebruikers, sessies en gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="fa603-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="fa603-138">Trechters</span><span class="sxs-lookup"><span data-stu-id="fa603-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="fa603-139">Retentie</span><span class="sxs-lookup"><span data-stu-id="fa603-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="fa603-140">Werkmappen</span><span class="sxs-lookup"><span data-stu-id="fa603-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
