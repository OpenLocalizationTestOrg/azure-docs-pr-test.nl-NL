---
title: Inleiding tot het oplossen van problemen in de Azure-netwerk-Watcher resource | Microsoft Docs
description: Deze pagina bevat een overzicht van de mogelijkheden van resource-voor probleemoplossing voor de netwerk-Watcher
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
ms.openlocfilehash: 0d5091b682d1b25c47b224394bcc2c46366eeb2a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="e0789-103">Inleiding tot het oplossen van problemen in de Azure-netwerk-Watcher resource</span><span class="sxs-lookup"><span data-stu-id="e0789-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="e0789-104">Virtuele netwerkgateways bieden connectiviteit tussen lokale bronnen en andere virtuele netwerken in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0789-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="e0789-105">Bewaking van deze gateways en hun verbindingen essentieel is voor communicatie is niet verbroken.</span><span class="sxs-lookup"><span data-stu-id="e0789-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span></span> <span data-ttu-id="e0789-106">Netwerk-Watcher biedt de mogelijkheid om op te lossen virtuele netwerkgateways en verbindingen.</span><span class="sxs-lookup"><span data-stu-id="e0789-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="e0789-107">Dit kan via de portal, PowerShell, CLI of REST-API worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e0789-107">This can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="e0789-108">Aangeroepen, netwerk-Watcher diagnose stelt de status van de gateway van virtueel netwerk of de verbinding als de juiste resultaten retourneren.</span><span class="sxs-lookup"><span data-stu-id="e0789-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span></span> <span data-ttu-id="e0789-109">Deze aanvraag is een langdurige transactie, worden de resultaten geretourneerd nadat de diagnose voltooid is.</span><span class="sxs-lookup"><span data-stu-id="e0789-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="e0789-111">Resultaten</span><span class="sxs-lookup"><span data-stu-id="e0789-111">Results</span></span>

<span data-ttu-id="e0789-112">De voorlopige resultaten geven een overzicht van de status van de resource.</span><span class="sxs-lookup"><span data-stu-id="e0789-112">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="e0789-113">Meer gedetailleerde informatie kan worden opgegeven voor resources, zoals wordt weergegeven in de volgende sectie:</span><span class="sxs-lookup"><span data-stu-id="e0789-113">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="e0789-114">De volgende lijst bevat de waarden geretourneerd met de problemen met API:</span><span class="sxs-lookup"><span data-stu-id="e0789-114">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="e0789-115">**startTime** -deze waarde is de tijd die de problemen met API-aanroep is gestart.</span><span class="sxs-lookup"><span data-stu-id="e0789-115">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="e0789-116">**endTime** -deze waarde is de tijd waarop de probleemoplossing is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="e0789-116">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="e0789-117">**code** -deze waarde is niet in orde, als er een fout één diagnose.</span><span class="sxs-lookup"><span data-stu-id="e0789-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="e0789-118">**resultaten** -resultaten is een verzameling met resultaten geretourneerd op de netwerkverbinding of de virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="e0789-118">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="e0789-119">**id** -deze waarde is het fouttype.</span><span class="sxs-lookup"><span data-stu-id="e0789-119">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="e0789-120">**Samenvatting** -deze waarde is een overzicht van de fout.</span><span class="sxs-lookup"><span data-stu-id="e0789-120">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="e0789-121">**gedetailleerde** -deze waarde bevat een gedetailleerde beschrijving van de fout.</span><span class="sxs-lookup"><span data-stu-id="e0789-121">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="e0789-122">**recommendedActions** -deze eigenschap is een verzameling aanbevolen acties te ondernemen.</span><span class="sxs-lookup"><span data-stu-id="e0789-122">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="e0789-123">**actionText** -deze waarde bevat de tekst beschrijven welke actie moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0789-123">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="e0789-124">**actionUri** -deze waarde bevat de URI-documentatie over het om te fungeren.</span><span class="sxs-lookup"><span data-stu-id="e0789-124">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="e0789-125">**actionUriText** -deze waarde is een korte beschrijving van de tekst in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="e0789-125">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="e0789-126">De volgende tabellen geven de typen met verschillende domeinen met fouten (id onder de resultaten van de voorgaande lijst) die beschikbaar zijn en als de fout Logboeken maakt.</span><span class="sxs-lookup"><span data-stu-id="e0789-126">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="e0789-127">Gateway</span><span class="sxs-lookup"><span data-stu-id="e0789-127">Gateway</span></span>

| <span data-ttu-id="e0789-128">Fouttype</span><span class="sxs-lookup"><span data-stu-id="e0789-128">Fault Type</span></span> | <span data-ttu-id="e0789-129">Reden</span><span class="sxs-lookup"><span data-stu-id="e0789-129">Reason</span></span> | <span data-ttu-id="e0789-130">Logboek</span><span class="sxs-lookup"><span data-stu-id="e0789-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="e0789-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="e0789-131">NoFault</span></span> | <span data-ttu-id="e0789-132">Wanneer er geen fout wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="e0789-132">When no error is detected.</span></span> |<span data-ttu-id="e0789-133">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-133">Yes</span></span>|
| <span data-ttu-id="e0789-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="e0789-134">GatewayNotFound</span></span> | <span data-ttu-id="e0789-135">Kan de Gateway of Gateway niet is ingericht niet vinden.</span><span class="sxs-lookup"><span data-stu-id="e0789-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="e0789-136">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-136">No</span></span>|
| <span data-ttu-id="e0789-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="e0789-137">PlannedMaintenance</span></span> |  <span data-ttu-id="e0789-138">Gateway-instantie is in onderhoud.</span><span class="sxs-lookup"><span data-stu-id="e0789-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="e0789-139">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-139">No</span></span>|
| <span data-ttu-id="e0789-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="e0789-140">UserDrivenUpdate</span></span> | <span data-ttu-id="e0789-141">Wanneer een gebruiker wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e0789-141">When a user update is in progress.</span></span> <span data-ttu-id="e0789-142">Dit wordt mogelijk een bewerking formaat wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e0789-142">This could be a resize operation.</span></span> | <span data-ttu-id="e0789-143">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-143">No</span></span> |
| <span data-ttu-id="e0789-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="e0789-144">VipUnResponsive</span></span> | <span data-ttu-id="e0789-145">Kan het primaire exemplaar van de Gateway niet bereiken.</span><span class="sxs-lookup"><span data-stu-id="e0789-145">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="e0789-146">Dit gebeurt wanneer de health-test is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e0789-146">This happens when the health probe fails.</span></span> | <span data-ttu-id="e0789-147">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-147">No</span></span> |
| <span data-ttu-id="e0789-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="e0789-148">PlatformInActive</span></span> | <span data-ttu-id="e0789-149">Er is een probleem met het platform.</span><span class="sxs-lookup"><span data-stu-id="e0789-149">There is an issue with the platform.</span></span> | <span data-ttu-id="e0789-150">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-150">No</span></span>|
| <span data-ttu-id="e0789-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="e0789-151">ServiceNotRunning</span></span> | <span data-ttu-id="e0789-152">De onderliggende service is niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0789-152">The underlying service is not running.</span></span> | <span data-ttu-id="e0789-153">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-153">No</span></span>|
| <span data-ttu-id="e0789-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="e0789-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="e0789-155">Er bestaat geen verbindingen op de gateway.</span><span class="sxs-lookup"><span data-stu-id="e0789-155">No Connections exists on the gateway.</span></span> <span data-ttu-id="e0789-156">Dit is alleen een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="e0789-156">This is only a warning.</span></span>| <span data-ttu-id="e0789-157">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-157">No</span></span>|
| <span data-ttu-id="e0789-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="e0789-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="e0789-159">Verbindingen zijn niet verbonden.</span><span class="sxs-lookup"><span data-stu-id="e0789-159">Connections are not connected.</span></span> <span data-ttu-id="e0789-160">Dit is alleen een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="e0789-160">This is only a warning.</span></span>| <span data-ttu-id="e0789-161">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-161">Yes</span></span>|
| <span data-ttu-id="e0789-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="e0789-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="e0789-163">De huidige Gateway CPU-gebruik is > 95%.</span><span class="sxs-lookup"><span data-stu-id="e0789-163">The current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="e0789-164">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="e0789-165">Verbinding</span><span class="sxs-lookup"><span data-stu-id="e0789-165">Connection</span></span>

| <span data-ttu-id="e0789-166">Fouttype</span><span class="sxs-lookup"><span data-stu-id="e0789-166">Fault Type</span></span> | <span data-ttu-id="e0789-167">Reden</span><span class="sxs-lookup"><span data-stu-id="e0789-167">Reason</span></span> | <span data-ttu-id="e0789-168">Logboek</span><span class="sxs-lookup"><span data-stu-id="e0789-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="e0789-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="e0789-169">NoFault</span></span> | <span data-ttu-id="e0789-170">Wanneer er geen fout wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="e0789-170">When no error is detected.</span></span> |<span data-ttu-id="e0789-171">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-171">Yes</span></span>|
| <span data-ttu-id="e0789-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="e0789-172">GatewayNotFound</span></span> | <span data-ttu-id="e0789-173">Kan de Gateway of Gateway niet is ingericht niet vinden.</span><span class="sxs-lookup"><span data-stu-id="e0789-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="e0789-174">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-174">No</span></span>|
| <span data-ttu-id="e0789-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="e0789-175">PlannedMaintenance</span></span> | <span data-ttu-id="e0789-176">Gateway-instantie is in onderhoud.</span><span class="sxs-lookup"><span data-stu-id="e0789-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="e0789-177">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-177">No</span></span>|
| <span data-ttu-id="e0789-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="e0789-178">UserDrivenUpdate</span></span> | <span data-ttu-id="e0789-179">Wanneer een gebruiker wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e0789-179">When a user update is in progress.</span></span> <span data-ttu-id="e0789-180">Dit wordt mogelijk een bewerking formaat wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e0789-180">This could be a resize operation.</span></span>  | <span data-ttu-id="e0789-181">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-181">No</span></span> |
| <span data-ttu-id="e0789-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="e0789-182">VipUnResponsive</span></span> | <span data-ttu-id="e0789-183">Kan het primaire exemplaar van de Gateway niet bereiken.</span><span class="sxs-lookup"><span data-stu-id="e0789-183">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="e0789-184">Fout treedt op wanneer de health-test is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e0789-184">It happens when the health probe fails.</span></span> | <span data-ttu-id="e0789-185">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-185">No</span></span> |
| <span data-ttu-id="e0789-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="e0789-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="e0789-187">Verbindingsconfiguratie ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="e0789-187">Connection configuration is missing.</span></span> | <span data-ttu-id="e0789-188">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-188">No</span></span> |
| <span data-ttu-id="e0789-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="e0789-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="e0789-190">De verbinding is gemarkeerd als 'verbinding verbroken'.</span><span class="sxs-lookup"><span data-stu-id="e0789-190">The Connection is marked "disconnected".</span></span> |<span data-ttu-id="e0789-191">Nee</span><span class="sxs-lookup"><span data-stu-id="e0789-191">No</span></span>|
| <span data-ttu-id="e0789-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="e0789-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="e0789-193">De onderliggende service heeft niet de verbinding geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e0789-193">The underlying service does not have the Connection configured.</span></span> | <span data-ttu-id="e0789-194">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-194">Yes</span></span> |
| <span data-ttu-id="e0789-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="e0789-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="e0789-196">De onderliggende service is gemarkeerd als stand-by.</span><span class="sxs-lookup"><span data-stu-id="e0789-196">The underlying service is marked as standby.</span></span>| <span data-ttu-id="e0789-197">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-197">Yes</span></span>|
| <span data-ttu-id="e0789-198">Authentication</span><span class="sxs-lookup"><span data-stu-id="e0789-198">Authentication</span></span> | <span data-ttu-id="e0789-199">Vooraf gedeelde sleutel komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="e0789-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="e0789-200">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-200">Yes</span></span>|
| <span data-ttu-id="e0789-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="e0789-201">PeerReachability</span></span> | <span data-ttu-id="e0789-202">De peer-gateway is niet bereikbaar.</span><span class="sxs-lookup"><span data-stu-id="e0789-202">The peer gateway is not reachable.</span></span> | <span data-ttu-id="e0789-203">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-203">Yes</span></span>|
| <span data-ttu-id="e0789-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="e0789-204">IkePolicyMismatch</span></span> | <span data-ttu-id="e0789-205">De gateway van de peer heeft IKE-beleidsregels die worden niet ondersteund door Azure.</span><span class="sxs-lookup"><span data-stu-id="e0789-205">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="e0789-206">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-206">Yes</span></span>|
| <span data-ttu-id="e0789-207">WfpParse fout</span><span class="sxs-lookup"><span data-stu-id="e0789-207">WfpParse Error</span></span> | <span data-ttu-id="e0789-208">Er is een fout opgetreden bij het parseren van het WPF-logboek.</span><span class="sxs-lookup"><span data-stu-id="e0789-208">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="e0789-209">Ja</span><span class="sxs-lookup"><span data-stu-id="e0789-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="e0789-210">Ondersteunde gatewaytypen</span><span class="sxs-lookup"><span data-stu-id="e0789-210">Supported Gateway types</span></span>

<span data-ttu-id="e0789-211">De volgende lijst bevat de ondersteuning ziet u welke gateways en verbindingen worden ondersteund bij het oplossen van netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="e0789-211">The following list shows the support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="e0789-212">**Gatewaytypen**</span><span class="sxs-lookup"><span data-stu-id="e0789-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="e0789-213">VPN</span><span class="sxs-lookup"><span data-stu-id="e0789-213">VPN</span></span>      | <span data-ttu-id="e0789-214">Ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-214">Supported</span></span>        |
|<span data-ttu-id="e0789-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e0789-215">ExpressRoute</span></span> | <span data-ttu-id="e0789-216">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-216">Not Supported</span></span> |
|<span data-ttu-id="e0789-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="e0789-217">Hypernet</span></span> | <span data-ttu-id="e0789-218">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-218">Not Supported</span></span>|
|<span data-ttu-id="e0789-219">**VPN-typen**</span><span class="sxs-lookup"><span data-stu-id="e0789-219">**VPN types**</span></span> | |
|<span data-ttu-id="e0789-220">Route gebaseerd</span><span class="sxs-lookup"><span data-stu-id="e0789-220">Route Based</span></span> | <span data-ttu-id="e0789-221">Ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-221">Supported</span></span>|
|<span data-ttu-id="e0789-222">Op basis van beleid</span><span class="sxs-lookup"><span data-stu-id="e0789-222">Policy Based</span></span> | <span data-ttu-id="e0789-223">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-223">Not Supported</span></span>|
|<span data-ttu-id="e0789-224">**Verbindingstypen**</span><span class="sxs-lookup"><span data-stu-id="e0789-224">**Connection types**</span></span>||
|<span data-ttu-id="e0789-225">IPSec</span><span class="sxs-lookup"><span data-stu-id="e0789-225">IPSec</span></span>| <span data-ttu-id="e0789-226">Ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-226">Supported</span></span>|
|<span data-ttu-id="e0789-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="e0789-227">VNet2Vnet</span></span>| <span data-ttu-id="e0789-228">Ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-228">Supported</span></span>|
|<span data-ttu-id="e0789-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e0789-229">ExpressRoute</span></span>| <span data-ttu-id="e0789-230">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-230">Not Supported</span></span>|
|<span data-ttu-id="e0789-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="e0789-231">Hypernet</span></span>| <span data-ttu-id="e0789-232">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-232">Not Supported</span></span>|
|<span data-ttu-id="e0789-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="e0789-233">VPNClient</span></span>| <span data-ttu-id="e0789-234">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e0789-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="e0789-235">Logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="e0789-235">Log files</span></span>

<span data-ttu-id="e0789-236">De resource voor probleemoplossing logboekbestanden worden opgeslagen in een opslagaccount nadat de resource probleemoplossing is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e0789-236">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="e0789-237">De volgende afbeelding toont een voorbeeld van de inhoud van een aanroep van dat heeft geresulteerd in een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="e0789-237">The following image shows the example contents of a call that resulted in an error.</span></span>

![ZIP-bestand][1]

> [!NOTE]
> <span data-ttu-id="e0789-239">In sommige gevallen wordt alleen een subset van de logboekbestanden geschreven naar de opslag.</span><span class="sxs-lookup"><span data-stu-id="e0789-239">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="e0789-240">Zie voor instructies over het downloaden van bestanden van azure storage-accounts, [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="e0789-240">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="e0789-241">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="e0789-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="e0789-242">Meer informatie over Opslagverkenner vindt u hier op de volgende koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="e0789-242">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="e0789-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="e0789-243">ConnectionStats.txt</span></span>

<span data-ttu-id="e0789-244">De **ConnectionStats.txt** bestand bevat de algemene statistieken van de verbinding, met inbegrip van inkomende en uitgaande bytes, de status van de verbinding en de tijd dat de verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="e0789-244">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="e0789-245">Als de aanroep van de API voor probleemoplossing worden geretourneerd in orde, het enige wat geretourneerd in het zip-bestand is een **ConnectionStats.txt** bestand.</span><span class="sxs-lookup"><span data-stu-id="e0789-245">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="e0789-246">De inhoud van dit bestand zijn vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e0789-246">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="e0789-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="e0789-247">CPUStats.txt</span></span>

<span data-ttu-id="e0789-248">De **CPUStats.txt** -bestand bevat CPU-gebruik en geheugen beschikbaar op het moment van de testen.</span><span class="sxs-lookup"><span data-stu-id="e0789-248">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="e0789-249">De inhoud van dit bestand is vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e0789-249">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="e0789-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="e0789-250">IKEErrors.txt</span></span>

<span data-ttu-id="e0789-251">De **IKEErrors.txt** bestand bevat alle IKE-fouten die zijn gevonden tijdens de bewaking.</span><span class="sxs-lookup"><span data-stu-id="e0789-251">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="e0789-252">Het volgende voorbeeld ziet de inhoud van een bestand IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="e0789-252">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="e0789-253">Uw fouten kunnen afwijken, afhankelijk van het probleem.</span><span class="sxs-lookup"><span data-stu-id="e0789-253">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="e0789-254">Verwijderd wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="e0789-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="e0789-255">De **Scrubbed wfpdiag.txt** logboekbestand bevat het WPF-logboek.</span><span class="sxs-lookup"><span data-stu-id="e0789-255">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="e0789-256">Dit logboek bevat de logboekregistratie van het pakket verwijderen en IKE/AuthIP fouten.</span><span class="sxs-lookup"><span data-stu-id="e0789-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="e0789-257">Het volgende voorbeeld ziet de inhoud van het bestand Scrubbed wfpdiag.txt.</span><span class="sxs-lookup"><span data-stu-id="e0789-257">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="e0789-258">In dit voorbeeld wordt is de gedeelde sleutel van een verbinding niet juist kan worden afgeleid uit de 3e regel van de onderkant.</span><span class="sxs-lookup"><span data-stu-id="e0789-258">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span></span> <span data-ttu-id="e0789-259">Het volgende voorbeeld is alleen een fragment van het hele logboek, omdat het logboek langdurige, afhankelijk van het probleem kan zijn.</span><span class="sxs-lookup"><span data-stu-id="e0789-259">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from the high priority thread pool list
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

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="e0789-260">wfpdiag.txt.Sum</span><span class="sxs-lookup"><span data-stu-id="e0789-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="e0789-261">De **wfpdiag.txt.sum** bestand is een logboek weergegeven met de buffers en gebeurtenissen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e0789-261">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="e0789-262">Het volgende voorbeeld wordt de inhoud van een bestand wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="e0789-262">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="e0789-263">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0789-263">Next steps</span></span>

<span data-ttu-id="e0789-264">Meer informatie over het onderzoeken van VPN-Gateways en verbindingen via de portal in via [Gateway probleemoplossing - Azure-portal](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e0789-264">Learn how to diagnose VPN Gateways and Connections through the portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
