---
title: Azure Networking Analytics-oplossing in Log Analytics | Microsoft Docs
description: U kunt de Azure-netwerken Analytics-oplossing in Log Analytics gebruiken om te controleren van de groep beveiligingslogboeken Azure-netwerk en Azure Application Gateway-Logboeken.
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
ms.openlocfilehash: 06b67322b3812a668a515ecc357171ede1d85441
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="0d0ab-103">Azure netwerken bewakingsoplossingen in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d0ab-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="0d0ab-104">Log Analytics biedt de volgende oplossingen voor het bewaken van uw netwerken:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-104">Log Analytics offers the following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="0d0ab-105">Netwerk Prestatiemeter (NPM)</span><span class="sxs-lookup"><span data-stu-id="0d0ab-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="0d0ab-106">De status van uw netwerk</span><span class="sxs-lookup"><span data-stu-id="0d0ab-106">Monitor the health of your network</span></span>
* <span data-ttu-id="0d0ab-107">Azure Application Gateway analytics om te controleren</span><span class="sxs-lookup"><span data-stu-id="0d0ab-107">Azure Application Gateway analytics to review</span></span>
 * <span data-ttu-id="0d0ab-108">Azure Application Gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="0d0ab-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="0d0ab-109">Azure Application Gateway metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="0d0ab-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="0d0ab-110">Netwerkbeveiligingsgroep Azure analytics om te controleren</span><span class="sxs-lookup"><span data-stu-id="0d0ab-110">Azure Network Security Group analytics to review</span></span>
 * <span data-ttu-id="0d0ab-111">De Netwerkbeveiligingsgroep voor Azure-Logboeken</span><span class="sxs-lookup"><span data-stu-id="0d0ab-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="0d0ab-112">Netwerk-Prestatiemeter (NPM)</span><span class="sxs-lookup"><span data-stu-id="0d0ab-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="0d0ab-113">De [netwerk Prestatiemeter](log-analytics-network-performance-monitor.md) management-oplossing is een netwerk bewakingsoplossing die de status, beschikbaarheid en bereikbaarheid van netwerken bewaakt.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span></span>  <span data-ttu-id="0d0ab-114">Het wordt gebruikt voor het bewaken van de verbinding tussen:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-114">It is used to monitor connectivity between:</span></span>

* <span data-ttu-id="0d0ab-115">openbare cloud en on-premises</span><span class="sxs-lookup"><span data-stu-id="0d0ab-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="0d0ab-116">datacenters en gebruikerslocaties (filialen)</span><span class="sxs-lookup"><span data-stu-id="0d0ab-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="0d0ab-117">de subnetten die als host fungeert voor verschillende lagen van een toepassing met meerdere lagen.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="0d0ab-118">Zie voor meer informatie [netwerk Prestatiemeter](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="0d0ab-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="0d0ab-119">Azure Application Gateway en de Netwerkbeveiligingsgroep analyses</span><span class="sxs-lookup"><span data-stu-id="0d0ab-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="0d0ab-120">De oplossingen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-120">To use the solutions:</span></span>
1. <span data-ttu-id="0d0ab-121">Toevoegen van de oplossing voor beheer met Log Analytics en</span><span class="sxs-lookup"><span data-stu-id="0d0ab-121">Add the management solution to Log Analytics, and</span></span>
2. <span data-ttu-id="0d0ab-122">Diagnostische gegevens om te leiden van de diagnostische gegevens naar een werkruimte voor logboekanalyse inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="0d0ab-123">Het is niet nodig zijn voor het schrijven van de logboeken naar Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-123">It is not necessary to write the logs to Azure Blob storage.</span></span>

<span data-ttu-id="0d0ab-124">U kunt diagnostische gegevens en de bijbehorende oplossing inschakelen voor een of beide van de toepassingsgateway en beveiligingsgroepen netwerken.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="0d0ab-125">Als u Diagnostische logboekregistratie voor een bepaald brontype niet is ingeschakeld, maar de oplossing te installeren, wordt de blades dashboard voor die bron leeg zijn en een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="0d0ab-126">In januari 2017, de ondersteunde manier van het verzenden van Logboeken vanaf Toepassingsgateways en Netwerkbeveiligingsgroepen met logboekanalyse gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="0d0ab-127">Als u ziet de **Azure Networking Analytics (afgeschaft)** oplossing Raadpleeg [migreren van de oude Networking Analytics-oplossing](#migrating-from-the-old-networking-analytics-solution) voor stappen die u moet volgen.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="0d0ab-128">Azure verzameling Gegevensdetails toegang controleren</span><span class="sxs-lookup"><span data-stu-id="0d0ab-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="0d0ab-129">De Azure Application Gateway-analyses en het beheer van Netwerkbeveiligingsgroep analyseoplossingen verzamelen van diagnostische gegevens logboeken rechtstreeks vanuit Azure Toepassingsgateways en Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="0d0ab-130">Het is niet nodig om te schrijven van de logboeken naar Azure Blob-opslag en geen agent is vereist voor het verzamelen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="0d0ab-131">De volgende tabel bevat gegevens verzameling methoden en andere informatie over hoe gegevens worden verzameld voor de analyse van Azure Application Gateway en de Netwerkbeveiligingsgroep analytics.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span></span>

| <span data-ttu-id="0d0ab-132">Platform</span><span class="sxs-lookup"><span data-stu-id="0d0ab-132">Platform</span></span> | <span data-ttu-id="0d0ab-133">Directe agent</span><span class="sxs-lookup"><span data-stu-id="0d0ab-133">Direct agent</span></span> | <span data-ttu-id="0d0ab-134">Systems Center Operations Manager-agent</span><span class="sxs-lookup"><span data-stu-id="0d0ab-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="0d0ab-135">Azure</span><span class="sxs-lookup"><span data-stu-id="0d0ab-135">Azure</span></span> | <span data-ttu-id="0d0ab-136">Operations Manager is vereist?</span><span class="sxs-lookup"><span data-stu-id="0d0ab-136">Operations Manager required?</span></span> | <span data-ttu-id="0d0ab-137">Operations Manager-agent gegevens verzonden via de beheergroep</span><span class="sxs-lookup"><span data-stu-id="0d0ab-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="0d0ab-138">Verzamelingsfrequentie</span><span class="sxs-lookup"><span data-stu-id="0d0ab-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0d0ab-139">Azure</span><span class="sxs-lookup"><span data-stu-id="0d0ab-139">Azure</span></span> |  |  |<span data-ttu-id="0d0ab-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="0d0ab-140">&#8226;</span></span> |  |  |<span data-ttu-id="0d0ab-141">Wanneer het logboek geregistreerd</span><span class="sxs-lookup"><span data-stu-id="0d0ab-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="0d0ab-142">Azure Application Gateway analytics-oplossing in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d0ab-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Azure Application Gateway Analytics symbool](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="0d0ab-144">De volgende logboeken worden ondersteund voor Toepassingsgateways:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-144">The following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="0d0ab-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="0d0ab-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="0d0ab-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="0d0ab-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="0d0ab-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="0d0ab-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="0d0ab-148">De volgende metrische gegevens worden voor Toepassingsgateways ondersteund:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-148">The following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="0d0ab-149">doorvoer van 5 minuten</span><span class="sxs-lookup"><span data-stu-id="0d0ab-149">5 minute throughput</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="0d0ab-150">Installeren en configureren van de oplossing</span><span class="sxs-lookup"><span data-stu-id="0d0ab-150">Install and configure the solution</span></span>
<span data-ttu-id="0d0ab-151">Gebruik de volgende instructies voor het installeren en configureren van de Azure Application Gateway analytics-oplossing:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-151">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="0d0ab-152">Inschakelen van de Azure Application Gateway analytics-oplossing van [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) of met behulp van de procedure beschreven in [toevoegen Log Analytics-oplossingen van de galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="0d0ab-152">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="0d0ab-153">Registratie voor diagnostische gegevens inschakelen de [Toepassingsgateways](../application-gateway/application-gateway-diagnostics.md) u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-153">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a><span data-ttu-id="0d0ab-154">Azure Application Gateway diagnostische gegevens in de portal inschakelen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-154">Enable Azure Application Gateway diagnostics in the portal</span></span>

1. <span data-ttu-id="0d0ab-155">Navigeer in de Azure-portal aan de toepassingsgateway resource bewaken</span><span class="sxs-lookup"><span data-stu-id="0d0ab-155">In the Azure portal, navigate to the Application Gateway resource to monitor</span></span>
2. <span data-ttu-id="0d0ab-156">Selecteer *diagnostische logboeken* om de volgende pagina te openen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-156">Select *Diagnostics logs* to open the following page</span></span>

   ![afbeelding van Azure Application Gateway resource](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="0d0ab-158">Klik op *diagnostische gegevens inschakelen* om de volgende pagina te openen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-158">Click *Turn on diagnostics* to open the following page</span></span>

   ![afbeelding van Azure Application Gateway resource](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="0d0ab-160">Om diagnostische gegevens inschakelen, klikt u op *op* onder *Status*</span><span class="sxs-lookup"><span data-stu-id="0d0ab-160">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="0d0ab-161">Klik op het selectievakje voor *verzenden met Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="0d0ab-161">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="0d0ab-162">Selecteer een bestaande werkruimte voor logboekanalyse of een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="0d0ab-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="0d0ab-163">Klik op het selectievakje onder **logboek** voor elk van de typen logboekbestanden te verzamelen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-163">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="0d0ab-164">Klik op *opslaan* waarmee de logboekregistratie van diagnostische gegevens met Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d0ab-164">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="0d0ab-165">Schakel Azure netwerkdiagnose met PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d0ab-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="0d0ab-166">De volgende PowerShell-script bevat een voorbeeld van hoe diagnostische logboekregistratie voor Toepassingsgateways inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-166">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="0d0ab-167">Azure Application Gateway analytics gebruiken</span><span class="sxs-lookup"><span data-stu-id="0d0ab-167">Use Azure Application Gateway analytics</span></span>
![afbeelding van Azure Application Gateway analytics tegel](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="0d0ab-169">Nadat u op de **Azure Application Gateway analytics** tegel in het overzicht kunt u samenvattingen van uw logboeken weergeven en ga vervolgens omlaag de gedetailleerde informatie voor de volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-169">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="0d0ab-170">Toegang tot toepassingen Gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="0d0ab-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="0d0ab-171">Client en server-fouten voor Application Gateway-Logboeken</span><span class="sxs-lookup"><span data-stu-id="0d0ab-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="0d0ab-172">Aanvragen per uur voor elke Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0d0ab-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="0d0ab-173">Mislukte aanvragen per uur voor elke Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0d0ab-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="0d0ab-174">Fouten door gebruikersagent voor Toepassingsgateways</span><span class="sxs-lookup"><span data-stu-id="0d0ab-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="0d0ab-175">Gateway-toepassingsprestaties</span><span class="sxs-lookup"><span data-stu-id="0d0ab-175">Application Gateway performance</span></span>
  * <span data-ttu-id="0d0ab-176">Status van de host voor Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0d0ab-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="0d0ab-177">Maximum- en 95e percentiel voor Application Gateway mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![afbeelding van een dashboard met analytische Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![afbeelding van een dashboard met analytische Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="0d0ab-180">Op de **Azure Application Gateway analytics** dashboard, Controleer de overzichtsgegevens in een van de blades en klik op eentje om gedetailleerde informatie weergeven over de zoekpagina logboek.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-180">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="0d0ab-181">U kunt op elk van de zoekpagina logboek kunt resultaten weergeven door de tijd, gedetailleerde resultaten en uw Logboekgeschiedenis zoeken.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-181">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="0d0ab-182">U kunt ook filteren op facetten om de resultaten te beperken.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-182">You can also filter by facets to narrow the results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="0d0ab-183">Netwerkbeveiligingsgroep Azure analytics-oplossing in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d0ab-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Netwerkbeveiligingsgroep Azure Analytics symbool](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="0d0ab-185">De volgende logboeken worden ondersteund voor netwerkbeveiligingsgroepen:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-185">The following logs are supported for network security groups:</span></span>

* <span data-ttu-id="0d0ab-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="0d0ab-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="0d0ab-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="0d0ab-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="0d0ab-188">Installeren en configureren van de oplossing</span><span class="sxs-lookup"><span data-stu-id="0d0ab-188">Install and configure the solution</span></span>
<span data-ttu-id="0d0ab-189">Gebruik de volgende instructies voor het installeren en configureren van de Azure-netwerken Analytics-oplossing:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-189">Use the following instructions to install and configure the Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="0d0ab-190">Inschakelen van de Netwerkbeveiligingsgroep Azure analytics-oplossing van [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) of met behulp van de procedure beschreven in [toevoegen Log Analytics-oplossingen van de galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="0d0ab-190">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="0d0ab-191">Registratie voor diagnostische gegevens inschakelen de [Netwerkbeveiligingsgroep](../virtual-network/virtual-network-nsg-manage-log.md) resources die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-191">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a><span data-ttu-id="0d0ab-192">Azure-netwerk beveiliging groep diagnostische gegevens in de portal inschakelen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-192">Enable Azure network security group diagnostics in the portal</span></span>

1. <span data-ttu-id="0d0ab-193">Navigeer in de Azure-portal naar de bron van de Netwerkbeveiligingsgroep voor het bewaken van</span><span class="sxs-lookup"><span data-stu-id="0d0ab-193">In the Azure portal, navigate to the Network Security Group resource to monitor</span></span>
2. <span data-ttu-id="0d0ab-194">Selecteer *diagnostische logboeken* om de volgende pagina te openen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-194">Select *Diagnostics logs* to open the following page</span></span>

   ![afbeelding van de Netwerkbeveiligingsgroep voor Azure resource](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="0d0ab-196">Klik op *diagnostische gegevens inschakelen* om de volgende pagina te openen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-196">Click *Turn on diagnostics* to open the following page</span></span>

   ![afbeelding van de Netwerkbeveiligingsgroep voor Azure resource](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="0d0ab-198">Om diagnostische gegevens inschakelen, klikt u op *op* onder *Status*</span><span class="sxs-lookup"><span data-stu-id="0d0ab-198">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="0d0ab-199">Klik op het selectievakje voor *verzenden met Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="0d0ab-199">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="0d0ab-200">Selecteer een bestaande werkruimte voor logboekanalyse of een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="0d0ab-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="0d0ab-201">Klik op het selectievakje onder **logboek** voor elk van de typen logboekbestanden te verzamelen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-201">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="0d0ab-202">Klik op *opslaan* waarmee de logboekregistratie van diagnostische gegevens met Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d0ab-202">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="0d0ab-203">Schakel Azure netwerkdiagnose met PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d0ab-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="0d0ab-204">De volgende PowerShell-script bevat een voorbeeld van het inschakelen van diagnostische logboekregistratie voor netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-204">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="0d0ab-205">Gebruik Azure Netwerkbeveiligingsgroep analytics</span><span class="sxs-lookup"><span data-stu-id="0d0ab-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="0d0ab-206">Nadat u op de **Netwerkbeveiligingsgroep Azure analytics** tegel in het overzicht kunt u samenvattingen van uw logboeken weergeven en ga vervolgens omlaag de gedetailleerde informatie voor de volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-206">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="0d0ab-207">Netwerkbeveiligingsgroep geblokkeerd stromen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="0d0ab-208">Netwerkbeveiligingsgroepen met geblokkeerde stromen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="0d0ab-209">MAC-adressen met geblokkeerde stromen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="0d0ab-210">Netwerkbeveiligingsgroep stromen toegestaan</span><span class="sxs-lookup"><span data-stu-id="0d0ab-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="0d0ab-211">Netwerkbeveiligingsgroepen met toegestane stromen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="0d0ab-212">MAC-adressen met toegestane stromen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-212">MAC addresses with allowed flows</span></span>

![afbeelding van een dashboard met analytische Azure Netwerkbeveiligingsgroep](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![afbeelding van een dashboard met analytische Azure Netwerkbeveiligingsgroep](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="0d0ab-215">Op de **Netwerkbeveiligingsgroep Azure analytics** dashboard, Controleer de overzichtsgegevens in een van de blades en klik op eentje om gedetailleerde informatie weergeven over de zoekpagina logboek.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-215">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="0d0ab-216">U kunt op elk van de zoekpagina logboek kunt resultaten weergeven door de tijd, gedetailleerde resultaten en uw Logboekgeschiedenis zoeken.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-216">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="0d0ab-217">U kunt ook filteren op facetten om de resultaten te beperken.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-217">You can also filter by facets to narrow the results.</span></span>

## <a name="migrating-from-the-old-networking-analytics-solution"></a><span data-ttu-id="0d0ab-218">Migreren van de oude Networking Analytics-oplossing</span><span class="sxs-lookup"><span data-stu-id="0d0ab-218">Migrating from the old Networking Analytics solution</span></span>
<span data-ttu-id="0d0ab-219">In januari 2017, de ondersteunde manier van het verzenden van Logboeken vanaf Azure Toepassingsgateways en beveiligingsgroepen voor Azure-netwerk met logboekanalyse gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-219">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="0d0ab-220">Deze wijzigingen bieden de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-220">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="0d0ab-221">Logboeken geschreven rechtstreeks met logboekanalyse zonder te hoeven gebruiken van een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="0d0ab-221">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="0d0ab-222">Minder latentie vanaf het moment wanneer logboeken worden gegenereerd voor hen beschikbaar worden gesteld in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d0ab-222">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="0d0ab-223">Minder configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="0d0ab-224">Een algemene indeling voor alle typen Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="0d0ab-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="0d0ab-225">De bijgewerkte oplossingen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-225">To use the updated solutions:</span></span>

1. [<span data-ttu-id="0d0ab-226">Diagnostische gegevens worden verzonden met logboekanalyse rechtstreeks vanuit Azure Toepassingsgateways configureren</span><span class="sxs-lookup"><span data-stu-id="0d0ab-226">Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="0d0ab-227">Diagnostische gegevens rechtstreeks met logboekanalyse worden verzonden vanuit Azure Network-beveiligingsgroepen configureren</span><span class="sxs-lookup"><span data-stu-id="0d0ab-227">Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="0d0ab-228">Schakel de *Azure Application Gateway Analytics* en de *Azure Network Security groep Analytics* oplossing met behulp van de procedure beschreven in [toevoegen Log Analytics-oplossingen van de Galerie met oplossingen](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="0d0ab-228">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="0d0ab-229">Bijwerken van een opgeslagen query's, dashboards of waarschuwingen te gebruiken van het nieuwe gegevenstype</span><span class="sxs-lookup"><span data-stu-id="0d0ab-229">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="0d0ab-230">Type is het AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-230">Type is to AzureDiagnostics.</span></span> <span data-ttu-id="0d0ab-231">Het ResourceType kunt u filteren op Azure VPN-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-231">You can use the ResourceType to filter to Azure networking logs.</span></span>

    | <span data-ttu-id="0d0ab-232">In plaats van:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-232">Instead of:</span></span> | <span data-ttu-id="0d0ab-233">Gebruik:</span><span class="sxs-lookup"><span data-stu-id="0d0ab-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="0d0ab-234">Voor elk veld dat een achtervoegsel van \_s, \_d, of \_g in de naam wijzigen van het eerste teken in kleine letters</span><span class="sxs-lookup"><span data-stu-id="0d0ab-234">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
   + <span data-ttu-id="0d0ab-235">Voor elk veld dat een achtervoegsel van \_o in naam van de gegevens is opgesplitst in afzonderlijke velden op basis van de geneste veldnamen.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-235">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span>
4. <span data-ttu-id="0d0ab-236">Verwijder de *Azure Networking Analytics (afgeschaft)* oplossing.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-236">Remove the *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="0d0ab-237">Als u met behulp van PowerShell, gebruikt u`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="0d0ab-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="0d0ab-238">Gegevens verzameld voordat de wijziging niet zichtbaar in de nieuwe oplossing is.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-238">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="0d0ab-239">U kunt blijven opvragen voor deze gegevens met behulp van de oude Type en de veldnamen.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-239">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0d0ab-240">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="0d0ab-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0d0ab-241">Next steps</span></span>
* <span data-ttu-id="0d0ab-242">Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) gedetailleerde Azure diagnostics-gegevens om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0d0ab-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span></span>
