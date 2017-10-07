---
title: aaaSCOM integratie met Application Insights | Microsoft Docs
description: Als u een SCOM-gebruiker bent, prestaties bewaken en onderzoeken van problemen met Application Insights. Uitgebreide dashboards, slimme waarschuwingen, krachtige diagnostische hulpprogramma's en analyse query's.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="12571-104">Toepassingsprestaties bewaken met Application Insights voor SCOM</span><span class="sxs-lookup"><span data-stu-id="12571-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="12571-105">Als u System Center Operations Manager (SCOM) toomanage uw servers, kunt u bewaking van prestaties en prestatieproblemen met behulp van Hallo [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="12571-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="12571-106">Application Insights wordt uw webtoepassing inkomende aanvragen en uitgaande REST en SQL-aanroepen, uitzonderingen en logboektraceringen bewaakt.</span><span class="sxs-lookup"><span data-stu-id="12571-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="12571-107">Het biedt dashboards metrische grafieken en slimme waarschuwingen, evenals krachtige diagnostische gegevens doorzoeken en analytische query's via deze telemetrie.</span><span class="sxs-lookup"><span data-stu-id="12571-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="12571-108">U kunt overschakelen op de bewaking van Application Insights met behulp van een SCOM management pack.</span><span class="sxs-lookup"><span data-stu-id="12571-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="12571-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="12571-109">Before you start</span></span>
<span data-ttu-id="12571-110">We gaan ervan uit:</span><span class="sxs-lookup"><span data-stu-id="12571-110">We assume:</span></span>

* <span data-ttu-id="12571-111">U bekend bent met SCOM en dat u SCOM 2012 R2 of 2016 toomanage uw IIS-webservers.</span><span class="sxs-lookup"><span data-stu-id="12571-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="12571-112">U hebt al geïnstalleerd op de servers die een webtoepassing die u toomonitor met Application Insights wilt.</span><span class="sxs-lookup"><span data-stu-id="12571-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="12571-113">App-framework-versie is .NET 4.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="12571-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="12571-114">Hebt u toegang tooa abonnement in [Microsoft Azure](https://azure.com) en toohello kunt aanmelden [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12571-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="12571-115">Uw organisatie kan een abonnement hebt en uw Microsoft-account tooit kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="12571-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="12571-116">(ontwikkelteam Hallo Hallo mogelijk bouwen [Application Insights-SDK](app-insights-asp-net.md) in Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="12571-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="12571-117">Deze instrumentation build-tijd biedt deze meer flexibiliteit bij het schrijven van aangepaste telemetrie.</span><span class="sxs-lookup"><span data-stu-id="12571-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="12571-118">Echter, het maakt niet uit: u kunt stappen Hallo Hier wordt beschreven, met of zonder Hallo SDK ingebouwd.)</span><span class="sxs-lookup"><span data-stu-id="12571-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="12571-119">(Eenmaal) Application Insights management pack installeren</span><span class="sxs-lookup"><span data-stu-id="12571-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="12571-120">Op het Hallo-machine waarop u Operations Manager uitvoert:</span><span class="sxs-lookup"><span data-stu-id="12571-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="12571-121">Een oude versie van Hallo management pack verwijderen:</span><span class="sxs-lookup"><span data-stu-id="12571-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="12571-122">Open in Operations Manager, beheer-, Management Packs.</span><span class="sxs-lookup"><span data-stu-id="12571-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="12571-123">Verwijder de oude versie Hallo.</span><span class="sxs-lookup"><span data-stu-id="12571-123">Delete hello old version.</span></span>
2. <span data-ttu-id="12571-124">Download en installeer Hallo management pack uit Hallo-catalogus.</span><span class="sxs-lookup"><span data-stu-id="12571-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="12571-125">Start Operations Manager opnieuw.</span><span class="sxs-lookup"><span data-stu-id="12571-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="12571-126">Een management pack maken</span><span class="sxs-lookup"><span data-stu-id="12571-126">Create a management pack</span></span>
1. <span data-ttu-id="12571-127">Open in Operations Manager **ontwerpen**, **.NET... met Application Insights**, **Wizard bewaking toevoegen**, en kies opnieuw **.NET... met de toepassing Insights**.</span><span class="sxs-lookup"><span data-stu-id="12571-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="12571-128">Na uw app naam Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="12571-128">Name hello configuration after your app.</span></span> <span data-ttu-id="12571-129">(U hebt tooinstrument één app tegelijk.)</span><span class="sxs-lookup"><span data-stu-id="12571-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="12571-130">Hallo op dezelfde pagina van de wizard, maak een nieuw management pack of Selecteer een pakket dat u eerder voor Application Insights hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12571-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="12571-131">(Hallo Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is een sjabloon, waaruit u een exemplaar maken.</span><span class="sxs-lookup"><span data-stu-id="12571-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="12571-132">U kunt opnieuw gebruiken hetzelfde exemplaar later Hallo.)</span><span class="sxs-lookup"><span data-stu-id="12571-132">You can reuse hello same instance later.)</span></span>

    ![Typ in Hallo tabblad algemene eigenschappen, Hallo-naam van Hallo-app.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="12571-136">Kies een app die u toomonitor wilt.</span><span class="sxs-lookup"><span data-stu-id="12571-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="12571-137">Hallo zoekfunctie zoekt tussen apps die zijn geïnstalleerd op uw servers.</span><span class="sxs-lookup"><span data-stu-id="12571-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![Op welke tabblad tooMonitor klikt u op toevoegen, typt u deel van naam van de app hello, klik op zoeken, OK Hallo-app en klik vervolgens op toevoegen, kiest.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="12571-139">Hallo optioneel bewaking bereik veld mag gebruikte toospecify een subset van uw servers, als u niet dat in alle servers toomonitor Hallo-app wilt.</span><span class="sxs-lookup"><span data-stu-id="12571-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="12571-140">Op de volgende wizardpagina hello, moet u eerst uw referenties toosign in tooMicrosoft Azure opgeven.</span><span class="sxs-lookup"><span data-stu-id="12571-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="12571-141">Op deze pagina kunt kiezen u Hallo Application Insights-resource waar u Hallo telemetrie gegevens toobe geanalyseerd en weergegeven.</span><span class="sxs-lookup"><span data-stu-id="12571-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="12571-142">Als de toepassing hello is geconfigureerd voor Application Insights tijdens de ontwikkeling, selecteert u de bestaande resource.</span><span class="sxs-lookup"><span data-stu-id="12571-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="12571-143">Anders maakt u een nieuwe resource met de naam van het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="12571-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="12571-144">Als er andere apps die deel uitmaken van Hallo hetzelfde systeem, plaatst u deze in Hallo dezelfde resourcegroep bevinden, toomake toegang toohello telemetrie eenvoudiger toomanage.</span><span class="sxs-lookup"><span data-stu-id="12571-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="12571-145">U kunt deze instellingen later wijzigen.</span><span class="sxs-lookup"><span data-stu-id="12571-145">You can change these settings later.</span></span>
     
     ![Klik op 'aanmelden' op het tabblad voor Application Insights-instellingen en geef de referenties van uw Microsoft-account voor Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="12571-148">Hallo voltooid de wizard.</span><span class="sxs-lookup"><span data-stu-id="12571-148">Complete hello wizard.</span></span>
   
    ![Klik op Maken](./media/app-insights-scom/070.png)

<span data-ttu-id="12571-150">Herhaal deze procedure voor elke app die u toomonitor wilt.</span><span class="sxs-lookup"><span data-stu-id="12571-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="12571-151">Als u toochange instellingen later nodig, opnieuw Hallo eigenschappen van de monitor Hallo vanuit Hallo ontwerpen-venster te openen.</span><span class="sxs-lookup"><span data-stu-id="12571-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![In het ontwerp, selecteer .NET Application Performance Monitoring met Application Insights, selecteer de monitor en klikt u op Eigenschappen.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="12571-153">Controleer of de bewaking</span><span class="sxs-lookup"><span data-stu-id="12571-153">Verify monitoring</span></span>
<span data-ttu-id="12571-154">Hallo-monitor is dat u zoekt naar uw app hebt geïnstalleerd op elke server.</span><span class="sxs-lookup"><span data-stu-id="12571-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="12571-155">Waar het Hallo-app wordt gevonden configureert het Application Insights Status Monitor toomonitor Hallo app.</span><span class="sxs-lookup"><span data-stu-id="12571-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="12571-156">Indien nodig, worden eerst Status Monitor op Hallo server installeert.</span><span class="sxs-lookup"><span data-stu-id="12571-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="12571-157">U kunt controleren welke exemplaren van Hallo app dat is aangetroffen:</span><span class="sxs-lookup"><span data-stu-id="12571-157">You can verify which instances of hello app it has found:</span></span>

![Open in de bewaking, Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="12571-159">Weergave telemetrie in Application Insights</span><span class="sxs-lookup"><span data-stu-id="12571-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="12571-160">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello bron voor uw app.</span><span class="sxs-lookup"><span data-stu-id="12571-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="12571-161">U [grafieken weergegeven telemetrie](app-insights-dashboards.md) van uw app.</span><span class="sxs-lookup"><span data-stu-id="12571-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="12571-162">(Als dit nog niet wordt weergegeven om op de hoofdpagina Hallo nog, klikt u op livestream metrische gegevens.)</span><span class="sxs-lookup"><span data-stu-id="12571-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="12571-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12571-163">Next steps</span></span>
* <span data-ttu-id="12571-164">[Instellen van een dashboard](app-insights-dashboards.md) toobring samen Hallo belangrijkste grafieken bewaking van deze en andere apps.</span><span class="sxs-lookup"><span data-stu-id="12571-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="12571-165">Meer informatie over metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="12571-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="12571-166">Waarschuwingen instellen</span><span class="sxs-lookup"><span data-stu-id="12571-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="12571-167">Prestatieproblemen oplossen</span><span class="sxs-lookup"><span data-stu-id="12571-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="12571-168">Krachtige Analytics-query 's</span><span class="sxs-lookup"><span data-stu-id="12571-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="12571-169">Webtests voor beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="12571-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

