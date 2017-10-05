---
title: SCOM-integratie met Application Insights | Microsoft Docs
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
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="97d16-104">Toepassingsprestaties bewaken met Application Insights voor SCOM</span><span class="sxs-lookup"><span data-stu-id="97d16-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="97d16-105">Als u System Center Operations Manager (SCOM) gebruikt voor het beheren van uw servers, kunt u prestaties bewaken en onderzoeken van prestatieproblemen met behulp van [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="97d16-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="97d16-106">Application Insights wordt uw webtoepassing inkomende aanvragen en uitgaande REST en SQL-aanroepen, uitzonderingen en logboektraceringen bewaakt.</span><span class="sxs-lookup"><span data-stu-id="97d16-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="97d16-107">Het biedt dashboards metrische grafieken en slimme waarschuwingen, evenals krachtige diagnostische gegevens doorzoeken en analytische query's via deze telemetrie.</span><span class="sxs-lookup"><span data-stu-id="97d16-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="97d16-108">U kunt overschakelen op de bewaking van Application Insights met behulp van een SCOM management pack.</span><span class="sxs-lookup"><span data-stu-id="97d16-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="97d16-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="97d16-109">Before you start</span></span>
<span data-ttu-id="97d16-110">We gaan ervan uit:</span><span class="sxs-lookup"><span data-stu-id="97d16-110">We assume:</span></span>

* <span data-ttu-id="97d16-111">U bekend bent met SCOM en SCOM 2012 R2 of 2016 te gebruiken voor het beheren van uw IIS-webservers.</span><span class="sxs-lookup"><span data-stu-id="97d16-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="97d16-112">U hebt al geïnstalleerd op de servers die een webtoepassing die u wilt bewaken met Application Insights.</span><span class="sxs-lookup"><span data-stu-id="97d16-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="97d16-113">App-framework-versie is .NET 4.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="97d16-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="97d16-114">U hebt toegang tot een abonnement in [Microsoft Azure](https://azure.com) en zich aanmelden bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97d16-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="97d16-115">Uw organisatie wellicht een abonnement en aan uw Microsoft-account kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="97d16-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="97d16-116">(Het ontwikkelingsteam kan maken de [Application Insights-SDK](app-insights-asp-net.md) in de web-app.</span><span class="sxs-lookup"><span data-stu-id="97d16-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="97d16-117">Deze instrumentation build-tijd biedt deze meer flexibiliteit bij het schrijven van aangepaste telemetrie.</span><span class="sxs-lookup"><span data-stu-id="97d16-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="97d16-118">Echter, het maakt niet uit: u kunt de stappen die hier worden beschreven, met of zonder de SDK al ingebouwd.)</span><span class="sxs-lookup"><span data-stu-id="97d16-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="97d16-119">(Eenmaal) Application Insights management pack installeren</span><span class="sxs-lookup"><span data-stu-id="97d16-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="97d16-120">Op de computer waarop u Operations Manager uitvoert:</span><span class="sxs-lookup"><span data-stu-id="97d16-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="97d16-121">Een oude versie van het management pack verwijderen:</span><span class="sxs-lookup"><span data-stu-id="97d16-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="97d16-122">Open in Operations Manager, beheer-, Management Packs.</span><span class="sxs-lookup"><span data-stu-id="97d16-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="97d16-123">Verwijder de oude versie.</span><span class="sxs-lookup"><span data-stu-id="97d16-123">Delete the old version.</span></span>
2. <span data-ttu-id="97d16-124">Download en installeer het management pack uit de catalogus.</span><span class="sxs-lookup"><span data-stu-id="97d16-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="97d16-125">Start Operations Manager opnieuw.</span><span class="sxs-lookup"><span data-stu-id="97d16-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="97d16-126">Een management pack maken</span><span class="sxs-lookup"><span data-stu-id="97d16-126">Create a management pack</span></span>
1. <span data-ttu-id="97d16-127">Open in Operations Manager **ontwerpen**, **.NET... met Application Insights**, **Wizard bewaking toevoegen**, en kies opnieuw **.NET... met de toepassing Insights**.</span><span class="sxs-lookup"><span data-stu-id="97d16-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="97d16-128">De naam van de configuratie na uw app.</span><span class="sxs-lookup"><span data-stu-id="97d16-128">Name the configuration after your app.</span></span> <span data-ttu-id="97d16-129">(Als u één app tegelijk softwareontwikkelaars hebben.)</span><span class="sxs-lookup"><span data-stu-id="97d16-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="97d16-130">Maak een nieuw management pack op dezelfde wizardpagina, of Selecteer een pakket dat u eerder voor Application Insights hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97d16-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="97d16-131">(De Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is een sjabloon, waaruit u een exemplaar maken.</span><span class="sxs-lookup"><span data-stu-id="97d16-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="97d16-132">U kunt later opnieuw gebruiken hetzelfde exemplaar.)</span><span class="sxs-lookup"><span data-stu-id="97d16-132">You can reuse the same instance later.)</span></span>

    ![Typ de naam van de app in het tabblad algemene eigenschappen.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="97d16-136">Kies een app die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="97d16-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="97d16-137">De zoekfunctie zoekt tussen apps die zijn geïnstalleerd op uw servers.</span><span class="sxs-lookup"><span data-stu-id="97d16-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![Over wat u moet het tabblad Monitor, klik op toevoegen, typt u deel van naam van de app, klik op zoeken, kies de app en vervolgens op toevoegen, OK.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="97d16-139">Het veld optionele bewaking scope kan worden gebruikt om op te geven van een subset van uw servers, als u niet wilt bewaken van de app in alle servers.</span><span class="sxs-lookup"><span data-stu-id="97d16-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="97d16-140">U moet uw referenties aan te melden bij Microsoft Azure opgeven op de volgende wizardpagina.</span><span class="sxs-lookup"><span data-stu-id="97d16-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="97d16-141">Op deze pagina kunt u de Application Insights-resource waar u de telemetriegegevens worden geanalyseerd en weergegeven.</span><span class="sxs-lookup"><span data-stu-id="97d16-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="97d16-142">Als de toepassing is geconfigureerd voor Application Insights tijdens de ontwikkeling, selecteert u de bestaande resource.</span><span class="sxs-lookup"><span data-stu-id="97d16-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="97d16-143">Anders maakt u een nieuwe resource met de naam van de app.</span><span class="sxs-lookup"><span data-stu-id="97d16-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="97d16-144">Als er andere apps die deel uitmaken van hetzelfde systeem, plaatst u deze in dezelfde resourcegroep, om toegang aan de telemetrie gemakkelijker te beheren.</span><span class="sxs-lookup"><span data-stu-id="97d16-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="97d16-145">U kunt deze instellingen later wijzigen.</span><span class="sxs-lookup"><span data-stu-id="97d16-145">You can change these settings later.</span></span>
     
     ![Klik op 'aanmelden' op het tabblad voor Application Insights-instellingen en geef de referenties van uw Microsoft-account voor Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="97d16-148">Voltooi de wizard.</span><span class="sxs-lookup"><span data-stu-id="97d16-148">Complete the wizard.</span></span>
   
    ![Klik op Maken](./media/app-insights-scom/070.png)

<span data-ttu-id="97d16-150">Herhaal deze procedure voor elke app die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="97d16-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="97d16-151">Als u deze instellingen later wijzigen moet, opent u de eigenschappen van de monitor van het ontwerpen-venster opnieuw op.</span><span class="sxs-lookup"><span data-stu-id="97d16-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![In het ontwerp, selecteer .NET Application Performance Monitoring met Application Insights, selecteer de monitor en klikt u op Eigenschappen.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="97d16-153">Controleer of de bewaking</span><span class="sxs-lookup"><span data-stu-id="97d16-153">Verify monitoring</span></span>
<span data-ttu-id="97d16-154">De monitor die u zoekt u naar uw app hebt geïnstalleerd op elke server.</span><span class="sxs-lookup"><span data-stu-id="97d16-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="97d16-155">Wanneer zij de app constateert configureert het Application Insights Status Monitor om de app te bewaken.</span><span class="sxs-lookup"><span data-stu-id="97d16-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="97d16-156">Indien nodig, worden eerst Status Monitor op de server installeert.</span><span class="sxs-lookup"><span data-stu-id="97d16-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="97d16-157">U kunt controleren welke exemplaren van de app heeft gevonden:</span><span class="sxs-lookup"><span data-stu-id="97d16-157">You can verify which instances of the app it has found:</span></span>

![Open in de bewaking, Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="97d16-159">Weergave telemetrie in Application Insights</span><span class="sxs-lookup"><span data-stu-id="97d16-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="97d16-160">In de [Azure-portal](https://portal.azure.com), blader naar de bron voor uw app.</span><span class="sxs-lookup"><span data-stu-id="97d16-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="97d16-161">U [grafieken weergegeven telemetrie](app-insights-dashboards.md) van uw app.</span><span class="sxs-lookup"><span data-stu-id="97d16-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="97d16-162">(Als dit nog niet wordt weergegeven om op de hoofdpagina nog, klikt u op livestream metrische gegevens.)</span><span class="sxs-lookup"><span data-stu-id="97d16-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="97d16-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97d16-163">Next steps</span></span>
* <span data-ttu-id="97d16-164">[Instellen van een dashboard](app-insights-dashboards.md) bij elkaar brengt de belangrijkste grafieken bewaking van deze en andere apps.</span><span class="sxs-lookup"><span data-stu-id="97d16-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="97d16-165">Meer informatie over metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="97d16-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="97d16-166">Waarschuwingen instellen</span><span class="sxs-lookup"><span data-stu-id="97d16-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="97d16-167">Prestatieproblemen oplossen</span><span class="sxs-lookup"><span data-stu-id="97d16-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="97d16-168">Krachtige Analytics-query 's</span><span class="sxs-lookup"><span data-stu-id="97d16-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="97d16-169">Webtests voor beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="97d16-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

