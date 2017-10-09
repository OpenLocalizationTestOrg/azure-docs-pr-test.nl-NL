---
title: statistieken aaaReal tijd in Azure CDN | Microsoft Docs
description: Realtime statistieken biedt realtime-gegevens over de prestaties van Azure CDN Hallo wanneer inhoud tooyour clients leveren.
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="c664f-103">Realtime statistieken in Microsoft Azure CDN</span><span class="sxs-lookup"><span data-stu-id="c664f-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="c664f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c664f-104">Overview</span></span>
<span data-ttu-id="c664f-105">Dit document wordt uitgelegd realtime statistieken in Microsoft Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="c664f-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="c664f-106">Deze functionaliteit biedt realtime gegevens, zoals bandbreedte, cache statussen en gelijktijdige verbindingen tooyour CDN-profiel voor het leveren van inhoud tooyour clients.</span><span class="sxs-lookup"><span data-stu-id="c664f-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="c664f-107">Hierdoor kan de doorlopende bewaking van Hallo status van uw service op elk gewenst moment, waaronder Ga live gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="c664f-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="c664f-108">Hallo na grafieken zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="c664f-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="c664f-109">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="c664f-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="c664f-110">Statuscodes</span><span class="sxs-lookup"><span data-stu-id="c664f-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="c664f-111">Cache-statussen</span><span class="sxs-lookup"><span data-stu-id="c664f-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="c664f-112">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="c664f-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="c664f-113">Toegang tot realtime statistieken</span><span class="sxs-lookup"><span data-stu-id="c664f-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="c664f-114">In Hallo [Azure Portal](https://portal.azure.com), bladeren tooyour CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="c664f-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Blade CDN-profiel](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="c664f-116">Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="c664f-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="c664f-118">Hallo CDN-beheerportal geopend.</span><span class="sxs-lookup"><span data-stu-id="c664f-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="c664f-119">Houd de muis boven Hallo **Analytics** tabblad en houd de muis boven Hallo **realtime statistieken** doel.</span><span class="sxs-lookup"><span data-stu-id="c664f-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="c664f-120">Klik op **HTTP Large Object**.</span><span class="sxs-lookup"><span data-stu-id="c664f-120">Click on **HTTP Large Object**.</span></span>
   
    ![CDN-beheerportal](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="c664f-122">Hallo realtime statistieken grafieken worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="c664f-123">Elk van de grafieken Hallo realtime geeft statistieken weer voor de tijdsspanne Hallo geselecteerd, wordt gestart wanneer het Hallo-pagina wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="c664f-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="c664f-124">Hallo grafieken automatisch bijgewerkt om de paar seconden.</span><span class="sxs-lookup"><span data-stu-id="c664f-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="c664f-125">Hallo **grafiek vernieuwen** knop, indien aanwezig, wordt gewist Hallo grafiek, waarna deze alleen Hallo geselecteerd gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="c664f-126">Bandbreedte</span><span class="sxs-lookup"><span data-stu-id="c664f-126">Bandwidth</span></span>
![Bandbreedte-grafiek](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="c664f-128">Hallo **bandbreedte** diagram toont de Hallo en de hoeveelheid bandbreedte die wordt gebruikt voor het huidige platform Hallo via tijdsspanne Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c664f-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="c664f-129">Hallo gearceerde gedeelte van de grafiek Hallo geeft bandbreedtegebruik.</span><span class="sxs-lookup"><span data-stu-id="c664f-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="c664f-130">Hallo exacte hoeveelheid bandbreedte die momenteel wordt gebruikt wordt direct onder Hallo lijndiagram weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="c664f-131">Statuscodes</span><span class="sxs-lookup"><span data-stu-id="c664f-131">Status Codes</span></span>
![Status code grafiek](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="c664f-133">Hallo **statuscodes** grafiek geeft aan hoe vaak bepaalde HTTP-antwoordcodes via Hallo geselecteerd tijdsspanne plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="c664f-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="c664f-134">Zie voor een beschrijving van elke optie voor HTTP-status code [Azure CDN HTTP-statuscodes](https://msdn.microsoft.com/library/mt759238.aspx).</span><span class="sxs-lookup"><span data-stu-id="c664f-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="c664f-135">Een lijst met HTTP-statuscodes wordt direct boven Hallo grafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="c664f-136">Deze lijst geeft aan dat elke statuscode die kan worden opgenomen in een lijndiagram Hallo en Hallo kunt u het huidige aantal exemplaren per seconde voor deze statuscode.</span><span class="sxs-lookup"><span data-stu-id="c664f-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="c664f-137">Standaard wordt een regel voor elk van deze statuscodes in Hallo grafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="c664f-138">U kunt echter tooonly monitor Hallo statuscodes waarvoor speciale betekenis voor uw CDN-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c664f-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="c664f-139">toodo dit gewenst Hallo statuscodes controleren en wis alle andere opties en klik vervolgens op **grafiek vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="c664f-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="c664f-140">U kunt tijdelijk logboekgegevens voor een bepaalde statuscode verbergen.</span><span class="sxs-lookup"><span data-stu-id="c664f-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="c664f-141">Klik Hallo statuscode gewenste toohide Hallo legenda direct onder het Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="c664f-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="c664f-142">Hallo grafiek verborgen onmiddellijk Hallo-statuscode.</span><span class="sxs-lookup"><span data-stu-id="c664f-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="c664f-143">Die statuscode opnieuw te klikken, wordt die optie toobe opnieuw weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="c664f-144">Cache-statussen</span><span class="sxs-lookup"><span data-stu-id="c664f-144">Cache Statuses</span></span>
![Cache statussen grafiek](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="c664f-146">Hallo **Cache statussen** grafiek geeft aan hoe vaak bepaalde typen statussen van de cache via Hallo geselecteerd tijdsspanne plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="c664f-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="c664f-147">Zie voor een beschrijving van elke optie cache status code [Azure CDN Cache statuscodes](https://msdn.microsoft.com/library/mt759237.aspx).</span><span class="sxs-lookup"><span data-stu-id="c664f-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="c664f-148">Een lijst met de statuscodes cache wordt direct boven Hallo grafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="c664f-149">Deze lijst geeft aan dat elke statuscode die kan worden opgenomen in een lijndiagram Hallo en Hallo kunt u het huidige aantal exemplaren per seconde voor deze statuscode.</span><span class="sxs-lookup"><span data-stu-id="c664f-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="c664f-150">Standaard wordt een regel voor elk van deze statuscodes in Hallo grafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="c664f-151">U kunt echter tooonly monitor Hallo statuscodes waarvoor speciale betekenis voor uw CDN-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c664f-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="c664f-152">toodo dit gewenst Hallo statuscodes controleren en wis alle andere opties en klik vervolgens op **grafiek vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="c664f-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="c664f-153">U kunt tijdelijk logboekgegevens voor een bepaalde statuscode verbergen.</span><span class="sxs-lookup"><span data-stu-id="c664f-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="c664f-154">Klik Hallo statuscode gewenste toohide Hallo legenda direct onder het Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="c664f-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="c664f-155">Hallo grafiek verborgen onmiddellijk Hallo-statuscode.</span><span class="sxs-lookup"><span data-stu-id="c664f-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="c664f-156">Die statuscode opnieuw te klikken, wordt die optie toobe opnieuw weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c664f-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="c664f-157">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="c664f-157">Connections</span></span>
![Verbindingen grafiek](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="c664f-159">Deze grafiek geeft aan hoeveel verbindingen tot stand gebrachte tooyour randservers zijn.</span><span class="sxs-lookup"><span data-stu-id="c664f-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="c664f-160">Elke aanvraag voor een asset die wordt doorgegeven via onze CDN resulteert in een verbinding.</span><span class="sxs-lookup"><span data-stu-id="c664f-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c664f-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c664f-161">Next Steps</span></span>
* <span data-ttu-id="c664f-162">Blijf op de hoogte met [realtime waarschuwingen in Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="c664f-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="c664f-163">Meer gedetailleerde met dig [geavanceerde HTTP-rapporten](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="c664f-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="c664f-164">Analyseren [gebruikspatronen](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="c664f-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

