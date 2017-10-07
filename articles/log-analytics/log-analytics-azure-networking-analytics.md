---
title: aaaAzure Networking Analytics-oplossing in Log Analytics | Microsoft Docs
description: U kunt hello Azure Networking Analytics-oplossing in Azure Application Gateway-logboeken en Log Analytics tooreview Azure-netwerk-beveiligingslogboeken groep gebruiken.
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="e0fba-103">Azure netwerken bewakingsoplossingen in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e0fba-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="e0fba-104">Log Analytics biedt Hallo oplossingen voor het bewaken van uw netwerken te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0fba-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="e0fba-105">Netwerk Prestatiemeter (NPM)</span><span class="sxs-lookup"><span data-stu-id="e0fba-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="e0fba-106">Controleprogramma Hallo de status van uw netwerk</span><span class="sxs-lookup"><span data-stu-id="e0fba-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="e0fba-107">Azure Application Gateway analytics tooreview</span><span class="sxs-lookup"><span data-stu-id="e0fba-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="e0fba-108">Azure Application Gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="e0fba-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="e0fba-109">Azure Application Gateway metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="e0fba-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="e0fba-110">Netwerkbeveiligingsgroep Azure analytics tooreview</span><span class="sxs-lookup"><span data-stu-id="e0fba-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="e0fba-111">De Netwerkbeveiligingsgroep voor Azure-Logboeken</span><span class="sxs-lookup"><span data-stu-id="e0fba-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="e0fba-112">Netwerk-Prestatiemeter (NPM)</span><span class="sxs-lookup"><span data-stu-id="e0fba-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="e0fba-113">Hallo [netwerk Prestatiemeter](log-analytics-network-performance-monitor.md) management-oplossing is een netwerk bewakingsoplossing die Hallo health, beschikbaarheid en bereikbaarheid van netwerken bewaakt.</span><span class="sxs-lookup"><span data-stu-id="e0fba-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="e0fba-114">Gebruikte toomonitor connectiviteit tussen is:</span><span class="sxs-lookup"><span data-stu-id="e0fba-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="e0fba-115">openbare cloud en on-premises</span><span class="sxs-lookup"><span data-stu-id="e0fba-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="e0fba-116">datacenters en gebruikerslocaties (filialen)</span><span class="sxs-lookup"><span data-stu-id="e0fba-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="e0fba-117">de subnetten die als host fungeert voor verschillende lagen van een toepassing met meerdere lagen.</span><span class="sxs-lookup"><span data-stu-id="e0fba-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="e0fba-118">Zie voor meer informatie [netwerk Prestatiemeter](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="e0fba-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="e0fba-119">Azure Application Gateway en de Netwerkbeveiligingsgroep analyses</span><span class="sxs-lookup"><span data-stu-id="e0fba-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="e0fba-120">toouse hello oplossingen:</span><span class="sxs-lookup"><span data-stu-id="e0fba-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="e0fba-121">Hallo management oplossing tooLog Analytics, toevoegen en</span><span class="sxs-lookup"><span data-stu-id="e0fba-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="e0fba-122">Diagnostische gegevens toodirect Hallo diagnostics tooa logboekanalyse workspace in te stellen.</span><span class="sxs-lookup"><span data-stu-id="e0fba-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="e0fba-123">Het is niet nodig toowrite Hallo logboeken tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="e0fba-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="e0fba-124">U kunt diagnostische gegevens en de bijbehorende oplossing Hallo inschakelen voor een of beide van de toepassingsgateway en beveiligingsgroepen netwerken.</span><span class="sxs-lookup"><span data-stu-id="e0fba-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="e0fba-125">Als u Diagnostische logboekregistratie voor een bepaald brontype niet is ingeschakeld, maar het Hallo-oplossing installeren, worden de Hallo dashboard blades voor die bron leeg zijn en een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e0fba-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="e0fba-126">In januari 2017 ondersteund Hallo manier van het verzenden van Logboeken vanaf Toepassingsgateways en Netwerkbeveiligingsgroepen tooLog die Analytics gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e0fba-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="e0fba-127">Als u Hallo ziet **Azure Networking Analytics (afgeschaft)** oplossing te verwijzen[migreren van de oude Networking Analytics-oplossing Hallo](#migrating-from-the-old-networking-analytics-solution) voor stappen die u moet toofollow.</span><span class="sxs-lookup"><span data-stu-id="e0fba-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="e0fba-128">Azure verzameling Gegevensdetails toegang controleren</span><span class="sxs-lookup"><span data-stu-id="e0fba-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="e0fba-129">Hello Azure Application Gateway analytics en Hallo Netwerkbeveiligingsgroep analyseoplossingen management verzamelen van diagnostische logboeken rechtstreeks vanuit Azure Toepassingsgateways en Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="e0fba-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="e0fba-130">Het is niet nodig toowrite Hallo logboeken tooAzure Blob-opslag en geen agent is vereist voor het verzamelen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="e0fba-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="e0fba-131">Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld voor Azure Application Gateway analytics en Hallo Netwerkbeveiligingsgroep analytics.</span><span class="sxs-lookup"><span data-stu-id="e0fba-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="e0fba-132">Platform</span><span class="sxs-lookup"><span data-stu-id="e0fba-132">Platform</span></span> | <span data-ttu-id="e0fba-133">Directe agent</span><span class="sxs-lookup"><span data-stu-id="e0fba-133">Direct agent</span></span> | <span data-ttu-id="e0fba-134">Systems Center Operations Manager-agent</span><span class="sxs-lookup"><span data-stu-id="e0fba-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="e0fba-135">Azure</span><span class="sxs-lookup"><span data-stu-id="e0fba-135">Azure</span></span> | <span data-ttu-id="e0fba-136">Operations Manager is vereist?</span><span class="sxs-lookup"><span data-stu-id="e0fba-136">Operations Manager required?</span></span> | <span data-ttu-id="e0fba-137">Operations Manager-agent gegevens verzonden via de beheergroep</span><span class="sxs-lookup"><span data-stu-id="e0fba-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="e0fba-138">Verzamelingsfrequentie</span><span class="sxs-lookup"><span data-stu-id="e0fba-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e0fba-139">Azure</span><span class="sxs-lookup"><span data-stu-id="e0fba-139">Azure</span></span> |  |  |<span data-ttu-id="e0fba-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e0fba-140">&#8226;</span></span> |  |  |<span data-ttu-id="e0fba-141">Wanneer het logboek geregistreerd</span><span class="sxs-lookup"><span data-stu-id="e0fba-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="e0fba-142">Azure Application Gateway analytics-oplossing in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e0fba-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Azure Application Gateway Analytics symbool](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="e0fba-144">Hallo logboeken te volgen worden voor Toepassingsgateways ondersteund:</span><span class="sxs-lookup"><span data-stu-id="e0fba-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="e0fba-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="e0fba-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="e0fba-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="e0fba-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="e0fba-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="e0fba-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="e0fba-148">Hallo volgende metrische gegevens worden voor Toepassingsgateways ondersteund:</span><span class="sxs-lookup"><span data-stu-id="e0fba-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="e0fba-149">doorvoer van 5 minuten</span><span class="sxs-lookup"><span data-stu-id="e0fba-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="e0fba-150">Installeer en configureer Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="e0fba-150">Install and configure hello solution</span></span>
<span data-ttu-id="e0fba-151">Gebruik Hallo tooinstall instructies te volgen en hello Azure Application Gateway analytics-oplossing te configureren:</span><span class="sxs-lookup"><span data-stu-id="e0fba-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="e0fba-152">Inschakelen van hello Azure Application Gateway analytics-oplossing van [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="e0fba-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="e0fba-153">Inschakelen van logboekregistratie van diagnostische gegevens voor Hallo [Toepassingsgateways](../application-gateway/application-gateway-diagnostics.md) gewenste toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e0fba-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="e0fba-154">Azure Application Gateway diagnostische gegevens in de portal Hallo inschakelen</span><span class="sxs-lookup"><span data-stu-id="e0fba-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="e0fba-155">Navigeer in hello Azure-portal, toohello Application Gateway resource toomonitor</span><span class="sxs-lookup"><span data-stu-id="e0fba-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="e0fba-156">Selecteer *diagnostische logboeken* tooopen Hallo na pagina</span><span class="sxs-lookup"><span data-stu-id="e0fba-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![afbeelding van Azure Application Gateway resource](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="e0fba-158">Klik op *diagnostische gegevens inschakelen* tooopen Hallo na pagina</span><span class="sxs-lookup"><span data-stu-id="e0fba-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![afbeelding van Azure Application Gateway resource](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="e0fba-160">tooturn diagnostische gegevens, klikt u op *op* onder *Status*</span><span class="sxs-lookup"><span data-stu-id="e0fba-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="e0fba-161">Klik op Hallo selectievakje voor *tooLog Analytics verzenden*</span><span class="sxs-lookup"><span data-stu-id="e0fba-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="e0fba-162">Selecteer een bestaande werkruimte voor logboekanalyse of een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="e0fba-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="e0fba-163">Klik op Hallo selectievakje onder **logboek** voor elk Hallo logboek typen toocollect</span><span class="sxs-lookup"><span data-stu-id="e0fba-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="e0fba-164">Klik op *opslaan* tooenable Hallo logboekregistratie van diagnostische gegevens tooLog Analytics</span><span class="sxs-lookup"><span data-stu-id="e0fba-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="e0fba-165">Schakel Azure netwerkdiagnose met PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0fba-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="e0fba-166">Hallo volgende PowerShell-script geeft een voorbeeld van hoe diagnostische logboekregistratie voor Toepassingsgateways tooenable.</span><span class="sxs-lookup"><span data-stu-id="e0fba-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="e0fba-167">Azure Application Gateway analytics gebruiken</span><span class="sxs-lookup"><span data-stu-id="e0fba-167">Use Azure Application Gateway analytics</span></span>
![afbeelding van Azure Application Gateway analytics tegel](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="e0fba-169">Nadat u op Hallo **Azure Application Gateway analytics** tegel op Hallo overzicht, kunt u samenvattingen van uw logboeken weergeven en ga vervolgens omlaag in toodetails voor Hallo volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="e0fba-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="e0fba-170">Toegang tot toepassingen Gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="e0fba-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="e0fba-171">Client en server-fouten voor Application Gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="e0fba-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="e0fba-172">Aanvragen per uur voor elke Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e0fba-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="e0fba-173">Mislukte aanvragen per uur voor elke Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e0fba-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="e0fba-174">Fouten door gebruikersagent voor Toepassingsgateways</span><span class="sxs-lookup"><span data-stu-id="e0fba-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="e0fba-175">Gateway-toepassingsprestaties</span><span class="sxs-lookup"><span data-stu-id="e0fba-175">Application Gateway performance</span></span>
  * <span data-ttu-id="e0fba-176">Status van de host voor Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e0fba-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="e0fba-177">Maximum- en 95e percentiel voor Application Gateway mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="e0fba-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![afbeelding van een dashboard met analytische Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![afbeelding van een dashboard met analytische Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="e0fba-180">Op Hallo **Azure Application Gateway analytics** dashboard samenvattingsinformatie in een van de blades Hallo Hallo controleren en klik op een tooview gedetailleerde informatie over de zoekpagina Hallo-logboek.</span><span class="sxs-lookup"><span data-stu-id="e0fba-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="e0fba-181">U kunt op een van de Hallo logboek zoekpagina's, resultaten weergeven door de tijd, gedetailleerde resultaten en uw Logboekgeschiedenis zoeken.</span><span class="sxs-lookup"><span data-stu-id="e0fba-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="e0fba-182">U kunt ook facetten toonarrow Hallo resultaten filteren.</span><span class="sxs-lookup"><span data-stu-id="e0fba-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="e0fba-183">Netwerkbeveiligingsgroep Azure analytics-oplossing in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e0fba-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Netwerkbeveiligingsgroep Azure Analytics symbool](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="e0fba-185">Hallo na logboeken worden ondersteund voor netwerkbeveiligingsgroepen:</span><span class="sxs-lookup"><span data-stu-id="e0fba-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="e0fba-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="e0fba-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="e0fba-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="e0fba-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="e0fba-188">Installeer en configureer Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="e0fba-188">Install and configure hello solution</span></span>
<span data-ttu-id="e0fba-189">Gebruik Hallo tooinstall instructies te volgen en hello Azure Networking Analytics-oplossing te configureren:</span><span class="sxs-lookup"><span data-stu-id="e0fba-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="e0fba-190">Inschakelen van hello Azure Netwerkbeveiligingsgroep analytics-oplossing van [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="e0fba-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="e0fba-191">Inschakelen van logboekregistratie van diagnostische gegevens voor Hallo [Netwerkbeveiligingsgroep](../virtual-network/virtual-network-nsg-manage-log.md) gewenste toomonitor resources.</span><span class="sxs-lookup"><span data-stu-id="e0fba-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="e0fba-192">Inschakelen van Azure security groep Netwerkdiagnose in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="e0fba-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="e0fba-193">Navigeer in hello Azure-portal, toohello Netwerkbeveiligingsgroep resource toomonitor</span><span class="sxs-lookup"><span data-stu-id="e0fba-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="e0fba-194">Selecteer *diagnostische logboeken* tooopen Hallo na pagina</span><span class="sxs-lookup"><span data-stu-id="e0fba-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![afbeelding van de Netwerkbeveiligingsgroep voor Azure resource](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="e0fba-196">Klik op *diagnostische gegevens inschakelen* tooopen Hallo na pagina</span><span class="sxs-lookup"><span data-stu-id="e0fba-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![afbeelding van de Netwerkbeveiligingsgroep voor Azure resource](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="e0fba-198">tooturn diagnostische gegevens, klikt u op *op* onder *Status*</span><span class="sxs-lookup"><span data-stu-id="e0fba-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="e0fba-199">Klik op Hallo selectievakje voor *tooLog Analytics verzenden*</span><span class="sxs-lookup"><span data-stu-id="e0fba-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="e0fba-200">Selecteer een bestaande werkruimte voor logboekanalyse of een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="e0fba-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="e0fba-201">Klik op Hallo selectievakje onder **logboek** voor elk Hallo logboek typen toocollect</span><span class="sxs-lookup"><span data-stu-id="e0fba-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="e0fba-202">Klik op *opslaan* tooenable Hallo logboekregistratie van diagnostische gegevens tooLog Analytics</span><span class="sxs-lookup"><span data-stu-id="e0fba-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="e0fba-203">Schakel Azure netwerkdiagnose met PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0fba-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="e0fba-204">Hallo volgende PowerShell-script geeft een voorbeeld van het tooenable Diagnostische logboekregistratie voor netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="e0fba-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="e0fba-205">Gebruik Azure Netwerkbeveiligingsgroep analytics</span><span class="sxs-lookup"><span data-stu-id="e0fba-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="e0fba-206">Nadat u op Hallo **Netwerkbeveiligingsgroep Azure analytics** tegel op Hallo overzicht, kunt u samenvattingen van uw logboeken weergeven en ga vervolgens omlaag in toodetails voor Hallo volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="e0fba-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="e0fba-207">Netwerkbeveiligingsgroep geblokkeerd stromen</span><span class="sxs-lookup"><span data-stu-id="e0fba-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="e0fba-208">Netwerkbeveiligingsgroepen met geblokkeerde stromen</span><span class="sxs-lookup"><span data-stu-id="e0fba-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="e0fba-209">MAC-adressen met geblokkeerde stromen</span><span class="sxs-lookup"><span data-stu-id="e0fba-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="e0fba-210">Netwerkbeveiligingsgroep stromen toegestaan</span><span class="sxs-lookup"><span data-stu-id="e0fba-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="e0fba-211">Netwerkbeveiligingsgroepen met toegestane stromen</span><span class="sxs-lookup"><span data-stu-id="e0fba-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="e0fba-212">MAC-adressen met toegestane stromen</span><span class="sxs-lookup"><span data-stu-id="e0fba-212">MAC addresses with allowed flows</span></span>

![afbeelding van een dashboard met analytische Azure Netwerkbeveiligingsgroep](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![afbeelding van een dashboard met analytische Azure Netwerkbeveiligingsgroep](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="e0fba-215">Op Hallo **Netwerkbeveiligingsgroep Azure analytics** dashboard samenvattingsinformatie in een van de blades Hallo Hallo controleren en klik op een tooview gedetailleerde informatie over de zoekpagina Hallo-logboek.</span><span class="sxs-lookup"><span data-stu-id="e0fba-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="e0fba-216">U kunt op een van de Hallo logboek zoekpagina's, resultaten weergeven door de tijd, gedetailleerde resultaten en uw Logboekgeschiedenis zoeken.</span><span class="sxs-lookup"><span data-stu-id="e0fba-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="e0fba-217">U kunt ook facetten toonarrow Hallo resultaten filteren.</span><span class="sxs-lookup"><span data-stu-id="e0fba-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="e0fba-218">Migreren van Hallo oude Networking Analytics-oplossing</span><span class="sxs-lookup"><span data-stu-id="e0fba-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="e0fba-219">In januari 2017 ondersteund Hallo manier van het verzenden van Logboeken vanaf Azure Toepassingsgateways en Azure Netwerkbeveiligingsgroepen tooLog die Analytics gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e0fba-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="e0fba-220">Deze wijzigingen bieden Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e0fba-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="e0fba-221">Logboeken worden rechtstreeks tooLog Analytics zonder Hallo toouse storage-account moet geschreven</span><span class="sxs-lookup"><span data-stu-id="e0fba-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="e0fba-222">Minder latentie van Hallo-tijd wanneer logboeken worden gegenereerd toothem beschikbaar worden gesteld in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e0fba-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="e0fba-223">Minder configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="e0fba-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="e0fba-224">Een algemene indeling voor alle typen Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="e0fba-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="e0fba-225">toouse hello bijgewerkt oplossingen:</span><span class="sxs-lookup"><span data-stu-id="e0fba-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="e0fba-226">Diagnostische gegevens toobe verzonden tooLog Analytics rechtstreeks vanuit Azure Toepassingsgateways configureren</span><span class="sxs-lookup"><span data-stu-id="e0fba-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="e0fba-227">Diagnostische gegevens toobe verzonden tooLog Analytics rechtstreeks uit Azure Network-beveiligingsgroepen configureren</span><span class="sxs-lookup"><span data-stu-id="e0fba-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="e0fba-228">Hallo inschakelen *Azure Application Gateway Analytics* en Hallo *Azure Network Security groep Analytics* oplossing met behulp van Hallo proces dat wordt beschreven in [oplossingen van logboekanalyse toevoegen Hallo galerie met oplossingen](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="e0fba-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="e0fba-229">Bijwerken van een opgeslagen query's, dashboards of waarschuwingen toouse Hallo nieuwe gegevenstype</span><span class="sxs-lookup"><span data-stu-id="e0fba-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="e0fba-230">Het type is tooAzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="e0fba-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="e0fba-231">U kunt Hallo ResourceType toofilter tooAzure netwerken Logboeken kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0fba-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="e0fba-232">In plaats van:</span><span class="sxs-lookup"><span data-stu-id="e0fba-232">Instead of:</span></span> | <span data-ttu-id="e0fba-233">Gebruik:</span><span class="sxs-lookup"><span data-stu-id="e0fba-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="e0fba-234">Voor elk veld dat een achtervoegsel van \_s, \_d, of \_g in Hallo naam Hallo eerste teken toolower hoofdlettergebruik</span><span class="sxs-lookup"><span data-stu-id="e0fba-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="e0fba-235">Voor elk veld dat een achtervoegsel van \_o in naam Hallo gegevens is opgesplitst in afzonderlijke velden op basis van de veldnamen Hallo genest.</span><span class="sxs-lookup"><span data-stu-id="e0fba-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="e0fba-236">Hallo verwijderen *Azure Networking Analytics (afgeschaft)* oplossing.</span><span class="sxs-lookup"><span data-stu-id="e0fba-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="e0fba-237">Als u met behulp van PowerShell, gebruikt u`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="e0fba-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="e0fba-238">Gegevens verzameld voordat Hallo wijziging niet zichtbaar in de nieuwe oplossing Hallo is.</span><span class="sxs-lookup"><span data-stu-id="e0fba-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="e0fba-239">U kunt tooquery blijven voor deze gegevens met Hallo oude Type en de veldnamen.</span><span class="sxs-lookup"><span data-stu-id="e0fba-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e0fba-240">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="e0fba-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="e0fba-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0fba-241">Next steps</span></span>
* <span data-ttu-id="e0fba-242">Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens van Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="e0fba-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
