---
title: Realtime statistieken in Azure CDN | Microsoft Docs
description: Realtime statistieken biedt realtime-gegevens over de prestaties van Azure CDN wanneer het leveren van inhoud aan uw clients.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="af3aa-103">Realtime statistieken in Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="af3aa-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="af3aa-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="af3aa-104">Overview</span></span>
<span data-ttu-id="af3aa-105">Dit document wordt uitgelegd realtime statistieken in Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="af3aa-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="af3aa-106">Deze functionaliteit biedt realtime gegevens, zoals bandbreedte, cache statussen en gelijktijdige verbindingen met uw CDN-profiel wanneer het leveren van inhoud aan uw clients.</span><span class="sxs-lookup"><span data-stu-id="af3aa-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="af3aa-107">Hierdoor kan de doorlopende bewaking van de status van uw service op elk gewenst moment, waaronder Ga live gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="af3aa-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="af3aa-108">De volgende grafieken zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="af3aa-108">The following graphs are available:</span></span>

* [<span data-ttu-id="af3aa-109">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="af3aa-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="af3aa-110">Statuscodes</span><span class="sxs-lookup"><span data-stu-id="af3aa-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="af3aa-111">Cache-statussen</span><span class="sxs-lookup"><span data-stu-id="af3aa-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="af3aa-112">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="af3aa-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="af3aa-113">Toegang tot realtime statistieken</span><span class="sxs-lookup"><span data-stu-id="af3aa-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="af3aa-114">In de [Azure Portal](https://portal.azure.com), blader naar uw CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="af3aa-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Blade CDN-profiel](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="af3aa-116">Klik in de blade CDN-profiel op de **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="af3aa-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="af3aa-118">Hiermee opent u de CDN-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="af3aa-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="af3aa-119">Beweeg de muisaanwijzer over de **Analytics** tabblad en klik vervolgens Beweeg de muisaanwijzer over de **realtime statistieken** doel.</span><span class="sxs-lookup"><span data-stu-id="af3aa-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="af3aa-120">Klik op **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="af3aa-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN-beheerportal](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="af3aa-122">De grafieken realtime statistieken worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="af3aa-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="af3aa-123">Elk van de grafieken realtime geeft statistieken weer voor de geselecteerde tijdsspanne gestart wanneer de pagina wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="af3aa-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="af3aa-124">De grafieken worden automatisch bijgewerkt om de paar seconden.</span><span class="sxs-lookup"><span data-stu-id="af3aa-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="af3aa-125">De **grafiek vernieuwen** knop, indien aanwezig, wordt gewist de grafiek, waarna deze alleen de geselecteerde gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="af3aa-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="af3aa-126">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="af3aa-126">Bandwidth</span></span>
![Bandbreedte-grafiek](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="af3aa-128">De **bandbreedte** diagram toont de hoeveelheid bandbreedte die wordt gebruikt voor het huidige platform via de geselecteerde tijdsperiode.</span><span class="sxs-lookup"><span data-stu-id="af3aa-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="af3aa-129">Het gearceerde gedeelte van de grafiek geeft bandbreedtegebruik.</span><span class="sxs-lookup"><span data-stu-id="af3aa-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="af3aa-130">De exacte hoeveelheid bandbreedte die momenteel wordt gebruikt, wordt direct onder de lijngrafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="af3aa-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="af3aa-131">Statuscodes</span><span class="sxs-lookup"><span data-stu-id="af3aa-131">Status Codes</span></span>
![Status code grafiek](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="af3aa-133">De **statuscodes** grafiek geeft aan hoe vaak bepaalde HTTP-antwoordcodes via de geselecteerde tijdsspanne plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="af3aa-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="af3aa-134">Zie voor een beschrijving van elke optie voor HTTP-status code [Azure CDN HTTP-statuscodes](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="af3aa-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="af3aa-135">Een lijst met HTTP-statuscodes wordt direct boven de grafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="af3aa-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="af3aa-136">Deze lijst geeft aan dat elke statuscode die kan worden opgenomen in de lijngrafiek en het huidige aantal exemplaren per seconde voor deze statuscode.</span><span class="sxs-lookup"><span data-stu-id="af3aa-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="af3aa-137">Een regel wordt standaard weergegeven voor elk van deze statuscodes in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="af3aa-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="af3aa-138">U kunt echter alleen de statuscodes waarvoor speciale betekenis voor uw CDN-configuratie te controleren.</span><span class="sxs-lookup"><span data-stu-id="af3aa-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="af3aa-139">U doet dit door de gewenste statuscodes controleren en wissen van alle andere opties en klik vervolgens op **grafiek vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="af3aa-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="af3aa-140">U kunt tijdelijk logboekgegevens voor een bepaalde statuscode verbergen.</span><span class="sxs-lookup"><span data-stu-id="af3aa-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="af3aa-141">Klik op de statuscode die u wilt verbergen in de legenda direct onder de grafiek.</span><span class="sxs-lookup"><span data-stu-id="af3aa-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="af3aa-142">De statuscode wordt onmiddellijk worden verborgen in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="af3aa-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="af3aa-143">Die statuscode opnieuw te klikken, wordt deze optie moet opnieuw worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="af3aa-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="af3aa-144">Cache-statussen</span><span class="sxs-lookup"><span data-stu-id="af3aa-144">Cache Statuses</span></span>
![Cache statussen grafiek](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="af3aa-146">De **Cache statussen** grafiek geeft aan hoe vaak bepaalde typen statussen van de cache via de geselecteerde tijdsspanne plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="af3aa-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="af3aa-147">Zie voor een beschrijving van elke optie cache status code [Azure CDN Cache statuscodes](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="af3aa-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="af3aa-148">Een lijst met de statuscodes cache wordt direct boven de grafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="af3aa-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="af3aa-149">Deze lijst geeft aan dat elke statuscode die kan worden opgenomen in de lijngrafiek en het huidige aantal exemplaren per seconde voor deze statuscode.</span><span class="sxs-lookup"><span data-stu-id="af3aa-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="af3aa-150">Een regel wordt standaard weergegeven voor elk van deze statuscodes in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="af3aa-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="af3aa-151">U kunt echter alleen de statuscodes waarvoor speciale betekenis voor uw CDN-configuratie te controleren.</span><span class="sxs-lookup"><span data-stu-id="af3aa-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="af3aa-152">U doet dit door de gewenste statuscodes controleren en wissen van alle andere opties en klik vervolgens op **grafiek vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="af3aa-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="af3aa-153">U kunt tijdelijk logboekgegevens voor een bepaalde statuscode verbergen.</span><span class="sxs-lookup"><span data-stu-id="af3aa-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="af3aa-154">Klik op de statuscode die u wilt verbergen in de legenda direct onder de grafiek.</span><span class="sxs-lookup"><span data-stu-id="af3aa-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="af3aa-155">De statuscode wordt onmiddellijk worden verborgen in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="af3aa-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="af3aa-156">Die statuscode opnieuw te klikken, wordt deze optie moet opnieuw worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="af3aa-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="af3aa-157">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="af3aa-157">Connections</span></span>
![Verbindingen grafiek](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="af3aa-159">Deze grafiek geeft aan hoeveel verbindingen zijn gemaakt aan de randservers.</span><span class="sxs-lookup"><span data-stu-id="af3aa-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="af3aa-160">Elke aanvraag voor een asset die wordt doorgegeven via onze CDN resulteert in een verbinding.</span><span class="sxs-lookup"><span data-stu-id="af3aa-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af3aa-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af3aa-161">Next Steps</span></span>
* <span data-ttu-id="af3aa-162">Blijf op de hoogte met [realtime waarschuwingen in Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="af3aa-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="af3aa-163">Meer gedetailleerde met dig [geavanceerde HTTP-rapporten](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="af3aa-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="af3aa-164">Analyseren [gebruikspatronen](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="af3aa-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

