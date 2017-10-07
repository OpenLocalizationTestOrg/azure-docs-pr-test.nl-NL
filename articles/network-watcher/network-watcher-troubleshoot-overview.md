---
title: aaaIntroduction tooresource probleemoplossing in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van de mogelijkheden van Hallo netwerk-Watcher resource voor probleemoplossing
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="c7992-103">Inleiding tooresource probleemoplossing in Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="c7992-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="c7992-104">Virtuele netwerkgateways bieden connectiviteit tussen lokale bronnen en andere virtuele netwerken in Azure.</span><span class="sxs-lookup"><span data-stu-id="c7992-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="c7992-105">Bewaking van deze gateways en hun verbindingen is essentieel tooensuring communicatie is niet verbroken.</span><span class="sxs-lookup"><span data-stu-id="c7992-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="c7992-106">Netwerk-Watcher Hallo mogelijkheid tootroubleshoot biedt virtuele netwerkgateways en verbindingen.</span><span class="sxs-lookup"><span data-stu-id="c7992-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="c7992-107">Dit kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="c7992-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="c7992-108">Als deze wordt aangeroepen, diagnoses netwerk-Watcher Hallo status van de virtuele netwerkgateway Hallo of verbinding en return Hallo juiste resultaten.</span><span class="sxs-lookup"><span data-stu-id="c7992-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="c7992-109">Deze aanvraag is een langdurige transactie, worden Hallo resultaten geretourneerd wanneer Hallo diagnose voltooid is.</span><span class="sxs-lookup"><span data-stu-id="c7992-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="c7992-111">Resultaten</span><span class="sxs-lookup"><span data-stu-id="c7992-111">Results</span></span>

<span data-ttu-id="c7992-112">Hallo voorlopige resultaten geretourneerd geven een overzicht van Hallo-status van het Hallo-resource.</span><span class="sxs-lookup"><span data-stu-id="c7992-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="c7992-113">Meer gedetailleerde informatie kan worden opgegeven voor resources, zoals wordt weergegeven in de volgende sectie Hallo:</span><span class="sxs-lookup"><span data-stu-id="c7992-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="c7992-114">Hallo volgende lijst bevat Hallo waarden geretourneerd met de Hallo API oplossen:</span><span class="sxs-lookup"><span data-stu-id="c7992-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="c7992-115">**startTime** -deze waarde is Hallo tijd Hallo oplossen API-aanroep is gestart.</span><span class="sxs-lookup"><span data-stu-id="c7992-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="c7992-116">**endTime** -deze waarde is Hallo tijd waarop het oplossen van Hallo is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="c7992-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="c7992-117">**code** -deze waarde is niet in orde, als er een fout één diagnose.</span><span class="sxs-lookup"><span data-stu-id="c7992-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="c7992-118">**resultaten** -resultaten is een verzameling van resultaten op Hallo verbinding of Hallo virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="c7992-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="c7992-119">**id** -deze waarde is het fouttype Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7992-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="c7992-120">**Samenvatting** -deze waarde is een overzicht van Hallo veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="c7992-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="c7992-121">**gedetailleerde** -deze waarde bevat een gedetailleerde beschrijving van het Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="c7992-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="c7992-122">**recommendedActions** -deze eigenschap is een verzameling aanbevolen acties tootake.</span><span class="sxs-lookup"><span data-stu-id="c7992-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="c7992-123">**actionText** -deze waarde bevat Hallo beschrijvende tekst voor welke tootake in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="c7992-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="c7992-124">**actionUri** -Hallo URI toodocumentation vindt u deze waarde voor het tooact.</span><span class="sxs-lookup"><span data-stu-id="c7992-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="c7992-125">**actionUriText** -deze waarde is een korte beschrijving van Hallo actietekst.</span><span class="sxs-lookup"><span data-stu-id="c7992-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="c7992-126">Hallo volgende tabellen tonen Hallo verschillende domeinen met fouten typen (id onder de resultaten van de voorgaande lijst Hallo) die beschikbaar zijn en als Hallo veroorzaakt Logboeken maakt.</span><span class="sxs-lookup"><span data-stu-id="c7992-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="c7992-127">Gateway</span><span class="sxs-lookup"><span data-stu-id="c7992-127">Gateway</span></span>

| <span data-ttu-id="c7992-128">Fouttype</span><span class="sxs-lookup"><span data-stu-id="c7992-128">Fault Type</span></span> | <span data-ttu-id="c7992-129">Reden</span><span class="sxs-lookup"><span data-stu-id="c7992-129">Reason</span></span> | <span data-ttu-id="c7992-130">Logboek</span><span class="sxs-lookup"><span data-stu-id="c7992-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="c7992-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="c7992-131">NoFault</span></span> | <span data-ttu-id="c7992-132">Wanneer er geen fout wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="c7992-132">When no error is detected.</span></span> |<span data-ttu-id="c7992-133">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-133">Yes</span></span>|
| <span data-ttu-id="c7992-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="c7992-134">GatewayNotFound</span></span> | <span data-ttu-id="c7992-135">Kan de Gateway of Gateway niet is ingericht niet vinden.</span><span class="sxs-lookup"><span data-stu-id="c7992-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="c7992-136">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-136">No</span></span>|
| <span data-ttu-id="c7992-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="c7992-137">PlannedMaintenance</span></span> |  <span data-ttu-id="c7992-138">Gateway-instantie is in onderhoud.</span><span class="sxs-lookup"><span data-stu-id="c7992-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="c7992-139">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-139">No</span></span>|
| <span data-ttu-id="c7992-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="c7992-140">UserDrivenUpdate</span></span> | <span data-ttu-id="c7992-141">Wanneer een gebruiker wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c7992-141">When a user update is in progress.</span></span> <span data-ttu-id="c7992-142">Dit wordt mogelijk een bewerking formaat wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c7992-142">This could be a resize operation.</span></span> | <span data-ttu-id="c7992-143">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-143">No</span></span> |
| <span data-ttu-id="c7992-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="c7992-144">VipUnResponsive</span></span> | <span data-ttu-id="c7992-145">Kan de primaire instantie Hallo Hallo Gateway niet bereiken.</span><span class="sxs-lookup"><span data-stu-id="c7992-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="c7992-146">Dit gebeurt wanneer Hallo health test is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c7992-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="c7992-147">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-147">No</span></span> |
| <span data-ttu-id="c7992-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="c7992-148">PlatformInActive</span></span> | <span data-ttu-id="c7992-149">Er is een probleem met het Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="c7992-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="c7992-150">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-150">No</span></span>|
| <span data-ttu-id="c7992-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="c7992-151">ServiceNotRunning</span></span> | <span data-ttu-id="c7992-152">Hallo onderliggende service is niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c7992-152">hello underlying service is not running.</span></span> | <span data-ttu-id="c7992-153">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-153">No</span></span>|
| <span data-ttu-id="c7992-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="c7992-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="c7992-155">Er bestaat geen verbindingen op Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="c7992-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="c7992-156">Dit is alleen een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="c7992-156">This is only a warning.</span></span>| <span data-ttu-id="c7992-157">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-157">No</span></span>|
| <span data-ttu-id="c7992-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="c7992-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="c7992-159">Verbindingen zijn niet verbonden.</span><span class="sxs-lookup"><span data-stu-id="c7992-159">Connections are not connected.</span></span> <span data-ttu-id="c7992-160">Dit is alleen een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="c7992-160">This is only a warning.</span></span>| <span data-ttu-id="c7992-161">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-161">Yes</span></span>|
| <span data-ttu-id="c7992-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="c7992-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="c7992-163">de huidige Gateway CPU-gebruik Hallo is > 95%.</span><span class="sxs-lookup"><span data-stu-id="c7992-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="c7992-164">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="c7992-165">Verbinding</span><span class="sxs-lookup"><span data-stu-id="c7992-165">Connection</span></span>

| <span data-ttu-id="c7992-166">Fouttype</span><span class="sxs-lookup"><span data-stu-id="c7992-166">Fault Type</span></span> | <span data-ttu-id="c7992-167">Reden</span><span class="sxs-lookup"><span data-stu-id="c7992-167">Reason</span></span> | <span data-ttu-id="c7992-168">Logboek</span><span class="sxs-lookup"><span data-stu-id="c7992-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="c7992-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="c7992-169">NoFault</span></span> | <span data-ttu-id="c7992-170">Wanneer er geen fout wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="c7992-170">When no error is detected.</span></span> |<span data-ttu-id="c7992-171">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-171">Yes</span></span>|
| <span data-ttu-id="c7992-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="c7992-172">GatewayNotFound</span></span> | <span data-ttu-id="c7992-173">Kan de Gateway of Gateway niet is ingericht niet vinden.</span><span class="sxs-lookup"><span data-stu-id="c7992-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="c7992-174">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-174">No</span></span>|
| <span data-ttu-id="c7992-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="c7992-175">PlannedMaintenance</span></span> | <span data-ttu-id="c7992-176">Gateway-instantie is in onderhoud.</span><span class="sxs-lookup"><span data-stu-id="c7992-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="c7992-177">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-177">No</span></span>|
| <span data-ttu-id="c7992-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="c7992-178">UserDrivenUpdate</span></span> | <span data-ttu-id="c7992-179">Wanneer een gebruiker wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c7992-179">When a user update is in progress.</span></span> <span data-ttu-id="c7992-180">Dit wordt mogelijk een bewerking formaat wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c7992-180">This could be a resize operation.</span></span>  | <span data-ttu-id="c7992-181">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-181">No</span></span> |
| <span data-ttu-id="c7992-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="c7992-182">VipUnResponsive</span></span> | <span data-ttu-id="c7992-183">Kan de primaire instantie Hallo Hallo Gateway niet bereiken.</span><span class="sxs-lookup"><span data-stu-id="c7992-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="c7992-184">Dit gebeurt als Hallo health test is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c7992-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="c7992-185">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-185">No</span></span> |
| <span data-ttu-id="c7992-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="c7992-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="c7992-187">Verbindingsconfiguratie ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="c7992-187">Connection configuration is missing.</span></span> | <span data-ttu-id="c7992-188">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-188">No</span></span> |
| <span data-ttu-id="c7992-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="c7992-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="c7992-190">Hallo verbinding is gemarkeerd als 'verbinding verbroken'.</span><span class="sxs-lookup"><span data-stu-id="c7992-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="c7992-191">Nee</span><span class="sxs-lookup"><span data-stu-id="c7992-191">No</span></span>|
| <span data-ttu-id="c7992-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="c7992-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="c7992-193">onderliggende Hallo-service heeft geen Hallo-verbinding geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c7992-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="c7992-194">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-194">Yes</span></span> |
| <span data-ttu-id="c7992-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="c7992-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="c7992-196">Hallo onderliggende service is gemarkeerd als stand-by.</span><span class="sxs-lookup"><span data-stu-id="c7992-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="c7992-197">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-197">Yes</span></span>|
| <span data-ttu-id="c7992-198">Authentication</span><span class="sxs-lookup"><span data-stu-id="c7992-198">Authentication</span></span> | <span data-ttu-id="c7992-199">Vooraf gedeelde sleutel komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="c7992-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="c7992-200">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-200">Yes</span></span>|
| <span data-ttu-id="c7992-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="c7992-201">PeerReachability</span></span> | <span data-ttu-id="c7992-202">Hallo peer gateway is niet bereikbaar.</span><span class="sxs-lookup"><span data-stu-id="c7992-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="c7992-203">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-203">Yes</span></span>|
| <span data-ttu-id="c7992-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="c7992-204">IkePolicyMismatch</span></span> | <span data-ttu-id="c7992-205">Hallo peer gateway heeft IKE-beleidsregels die worden niet ondersteund door Azure.</span><span class="sxs-lookup"><span data-stu-id="c7992-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="c7992-206">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-206">Yes</span></span>|
| <span data-ttu-id="c7992-207">WfpParse fout</span><span class="sxs-lookup"><span data-stu-id="c7992-207">WfpParse Error</span></span> | <span data-ttu-id="c7992-208">Er is een fout opgetreden bij het parseren Hallo WFP-logboek.</span><span class="sxs-lookup"><span data-stu-id="c7992-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="c7992-209">Ja</span><span class="sxs-lookup"><span data-stu-id="c7992-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="c7992-210">Ondersteunde gatewaytypen</span><span class="sxs-lookup"><span data-stu-id="c7992-210">Supported Gateway types</span></span>

<span data-ttu-id="c7992-211">Hallo volgende lijst bevat Hallo ondersteuning ziet u welke gateways en verbindingen worden ondersteund bij het oplossen van netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="c7992-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="c7992-212">**Gatewaytypen**</span><span class="sxs-lookup"><span data-stu-id="c7992-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="c7992-213">VPN</span><span class="sxs-lookup"><span data-stu-id="c7992-213">VPN</span></span>      | <span data-ttu-id="c7992-214">Ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-214">Supported</span></span>        |
|<span data-ttu-id="c7992-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c7992-215">ExpressRoute</span></span> | <span data-ttu-id="c7992-216">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-216">Not Supported</span></span> |
|<span data-ttu-id="c7992-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="c7992-217">Hypernet</span></span> | <span data-ttu-id="c7992-218">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-218">Not Supported</span></span>|
|<span data-ttu-id="c7992-219">**VPN-typen**</span><span class="sxs-lookup"><span data-stu-id="c7992-219">**VPN types**</span></span> | |
|<span data-ttu-id="c7992-220">Route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="c7992-220">Route Based</span></span> | <span data-ttu-id="c7992-221">Ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-221">Supported</span></span>|
|<span data-ttu-id="c7992-222">Op basis van beleid</span><span class="sxs-lookup"><span data-stu-id="c7992-222">Policy Based</span></span> | <span data-ttu-id="c7992-223">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-223">Not Supported</span></span>|
|<span data-ttu-id="c7992-224">**Verbindingstypen**</span><span class="sxs-lookup"><span data-stu-id="c7992-224">**Connection types**</span></span>||
|<span data-ttu-id="c7992-225">IPSec</span><span class="sxs-lookup"><span data-stu-id="c7992-225">IPSec</span></span>| <span data-ttu-id="c7992-226">Ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-226">Supported</span></span>|
|<span data-ttu-id="c7992-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="c7992-227">VNet2Vnet</span></span>| <span data-ttu-id="c7992-228">Ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-228">Supported</span></span>|
|<span data-ttu-id="c7992-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c7992-229">ExpressRoute</span></span>| <span data-ttu-id="c7992-230">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-230">Not Supported</span></span>|
|<span data-ttu-id="c7992-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="c7992-231">Hypernet</span></span>| <span data-ttu-id="c7992-232">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-232">Not Supported</span></span>|
|<span data-ttu-id="c7992-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="c7992-233">VPNClient</span></span>| <span data-ttu-id="c7992-234">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="c7992-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="c7992-235">Logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="c7992-235">Log files</span></span>

<span data-ttu-id="c7992-236">Hallo resource voor probleemoplossing logboekbestanden worden opgeslagen in een opslagaccount nadat de resource probleemoplossing is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c7992-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="c7992-237">Hallo toont volgende afbeelding Hallo voorbeeld van de inhoud van een aanroep van dat heeft geresulteerd in een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="c7992-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![ZIP-bestand][1]

> [!NOTE]
> <span data-ttu-id="c7992-239">In sommige gevallen wordt alleen een subset van de logboekbestanden Hallo toostorage geschreven.</span><span class="sxs-lookup"><span data-stu-id="c7992-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="c7992-240">Voor instructies over het downloaden van bestanden van azure storage-accounts, Raadpleeg te[aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c7992-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c7992-241">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="c7992-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="c7992-242">Meer informatie over Opslagverkenner vindt u hier op Hallo koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="c7992-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="c7992-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="c7992-243">ConnectionStats.txt</span></span>

<span data-ttu-id="c7992-244">Hallo **ConnectionStats.txt** bestand bevat de algemene statistieken Hallo-verbinding, met inbegrip van inkomende en uitgaande bytes, de status van de verbinding en Hallo tijd Hallo verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="c7992-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="c7992-245">Als Hallo aanroep toohello probleemoplossing API in orde retourneert, Hallo geretourneerd in het zip-bestand Hallo heeft alleen een **ConnectionStats.txt** bestand.</span><span class="sxs-lookup"><span data-stu-id="c7992-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="c7992-246">Hallo-inhoud van dit bestand zijn vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7992-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="c7992-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="c7992-247">CPUStats.txt</span></span>

<span data-ttu-id="c7992-248">Hallo **CPUStats.txt** -bestand bevat CPU-gebruik en geheugen beschikbaar op Hallo tijdstip van de testen.</span><span class="sxs-lookup"><span data-stu-id="c7992-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="c7992-249">Hallo-inhoud van dit bestand is vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7992-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="c7992-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="c7992-250">IKEErrors.txt</span></span>

<span data-ttu-id="c7992-251">Hallo **IKEErrors.txt** bestand bevat alle IKE-fouten die zijn gevonden tijdens de bewaking.</span><span class="sxs-lookup"><span data-stu-id="c7992-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="c7992-252">Hallo ziet volgende voorbeeld Hallo inhoud van een bestand IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="c7992-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="c7992-253">Uw fouten kunnen afwijken, afhankelijk van Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="c7992-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="c7992-254">Verwijderd wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="c7992-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="c7992-255">Hallo **Scrubbed wfpdiag.txt** logboekbestand Hallo wfp-logboek bevat.</span><span class="sxs-lookup"><span data-stu-id="c7992-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="c7992-256">Dit logboek bevat de logboekregistratie van het pakket verwijderen en IKE/AuthIP fouten.</span><span class="sxs-lookup"><span data-stu-id="c7992-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="c7992-257">Hallo ziet volgende voorbeeld Hallo inhoud van Hallo Scrubbed wfpdiag.txt bestand.</span><span class="sxs-lookup"><span data-stu-id="c7992-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="c7992-258">In dit voorbeeld is Hallo gedeelde sleutel van een verbinding niet juist kan worden afgeleid uit 3e regel Hallo van Hallo onder.</span><span class="sxs-lookup"><span data-stu-id="c7992-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="c7992-259">Hallo volgende voorbeeld is alleen een fragment van de hele logboek Hallo, zoals Hallo logboek langdurige, afhankelijk van Hallo probleem kan worden.</span><span class="sxs-lookup"><span data-stu-id="c7992-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="c7992-260">wfpdiag.txt.Sum</span><span class="sxs-lookup"><span data-stu-id="c7992-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="c7992-261">Hallo **wfpdiag.txt.sum** bestand is een logboek met Hallo buffers en gebeurtenissen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c7992-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="c7992-262">Hallo is volgende voorbeeld Hallo inhoud van een bestand wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="c7992-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="c7992-263">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7992-263">Next steps</span></span>

<span data-ttu-id="c7992-264">Meer informatie over hoe toodiagnose VPN-Gateways en verbindingen via portal Hallo in via [Gateway probleemoplossing - Azure-portal](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7992-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
