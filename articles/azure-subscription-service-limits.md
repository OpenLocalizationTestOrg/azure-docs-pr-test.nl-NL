---
title: aaaAzure abonnement limieten en quota | Microsoft Docs
description: Geeft een lijst van algemene Azure-abonnement en Servicelimieten, quota's en beperkingen. Dit omvat informatie over hoe tooincrease samen met maximale waarden beperkt.
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="b0e8b-104">Azure-abonnement en servicelimieten, quota's en beperkingen</span><span class="sxs-lookup"><span data-stu-id="b0e8b-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="b0e8b-105">Dit document vindt u enkele van Hallo meest voorkomende Microsoft Azure-limieten, quota's soms ook wel genoemd.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="b0e8b-106">Dit document betrekking niet op dit moment op alle Azure-services.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="b0e8b-107">Na verloop van tijd Hallo lijst zal worden uitgebreid en bijgewerkt toocover meer Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="b0e8b-108">Ga naar [overzicht van Azure prijzen](https://azure.microsoft.com/pricing/) toolearn meer informatie over prijzen voor Azure.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="b0e8b-109">Daar kunt u uw kosten Hallo met schatten [Prijscalculator](https://azure.microsoft.com/pricing/calculator/) of via Hallo prijzen detailpagina voor een service (bijvoorbeeld [VM's van Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="b0e8b-110">Uw kosten voor tips toohelp beheren, Zie [te voorkomen dat onverwachte kosten met Azure-facturering en kostenbeheer](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b0e8b-111">Als u tooraise Hallo limiet of quotum hierboven Hallo wilt **standaard limiet**, [opent u een ondersteuningsaanvraag online klant kosteloos](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="b0e8b-112">Hallo limieten kunnen niet worden verhoogd hierboven Hallo **maximumlimiet** waarde in het Hallo-tabellen te volgen.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="b0e8b-113">Als er geen **maximumlimiet** kolom, klikt u vervolgens Hallo-resource heeft geen instelbare limieten.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="b0e8b-114">Gratis proefversie van abonnementen zijn niet in aanmerking komen voor limiet of quotum vergroot.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="b0e8b-115">Als u een gratis proefversie hebt, kunt u upgraden tooa [betalen naar gebruik](https://azure.microsoft.com/offers/ms-azr-0003p/) abonnement.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="b0e8b-116">Zie voor meer informatie [Upgrade gratis proefversie van Azure tooPay-als-u-Go](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="b0e8b-117">Limieten en hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b0e8b-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="b0e8b-118">Het is nu mogelijk toocombine meerdere Azure-resources in tooa één Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="b0e8b-119">Bij gebruik van resourcegroepen limieten die eenmaal globale zijn beheerd op een regionaal niveau Hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="b0e8b-120">Zie voor meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b0e8b-121">Hallo limieten onder een nieuwe tabel is toegevoegd tooreflect eventuele verschillen in limieten bij gebruik van hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="b0e8b-122">Er is bijvoorbeeld een **abonnementen** tabel en een **abonnementen - Azure Resource Manager** tabel.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="b0e8b-123">Wanneer een limiet van toepassing tooboth scenario's is, is het alleen weergegeven in de eerste tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="b0e8b-124">Tenzij anders vermeld, gelden limieten in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="b0e8b-125">Belangrijke tooemphasize dat quota's voor resources in Azure-resourcegroepen per regio toegankelijk zijn voor uw abonnement zijn, en niet per abonnement is Hallo service management quota zijn.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="b0e8b-126">Laten we core quota gebruiken als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="b0e8b-127">Als u een quotum verhogen met ondersteuning voor kernen toorequest nodig hebt, moet u toodecide hoe veel kernen die u wilt toouse in welke regio's en vervolgens een specifieke aanvraag maken voor Azure-resourcegroep core quota's voor Hallo bedragen en regio's die u wilt.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="b0e8b-128">Dus als u nodig hebt toouse 30 cores in West-Europa toorun uw toepassing. specifiek moet u 30 kernen in West-Europa aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="b0e8b-129">Maar u geen een quotum voor kernen verhogen in elke andere regio--alleen West-Europa Hallo 30-kerngeheugenquotum hebben.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="b0e8b-130">Als gevolg hiervan soms is het nuttig tooconsider beslist wat uw Azure-resourcegroep quota's moeten toobe voor uw workload één regio is, en aanvragen die in elke regio waarin u implementatie overweegt bedrag.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="b0e8b-131">Zie [implementatieproblemen oplossen](resource-manager-common-deployment-errors.md) voor meer informatie voor het detecteren van uw huidige quota's voor specifieke regio's.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="b0e8b-132">Servicespecifieke limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-132">Service-specific limits</span></span>
* [<span data-ttu-id="b0e8b-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0e8b-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="b0e8b-134">API Management</span><span class="sxs-lookup"><span data-stu-id="b0e8b-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="b0e8b-135">App Service</span><span class="sxs-lookup"><span data-stu-id="b0e8b-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="b0e8b-136">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="b0e8b-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="b0e8b-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="b0e8b-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="b0e8b-138">Automatisering</span><span class="sxs-lookup"><span data-stu-id="b0e8b-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="b0e8b-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b0e8b-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="b0e8b-140">Azure Event raster</span><span class="sxs-lookup"><span data-stu-id="b0e8b-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="b0e8b-141">Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="b0e8b-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="b0e8b-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b0e8b-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="b0e8b-143">Een back-up maken</span><span class="sxs-lookup"><span data-stu-id="b0e8b-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="b0e8b-144">Batch</span><span class="sxs-lookup"><span data-stu-id="b0e8b-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="b0e8b-145">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="b0e8b-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="b0e8b-146">CDN</span><span class="sxs-lookup"><span data-stu-id="b0e8b-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="b0e8b-147">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b0e8b-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="b0e8b-148">Container Instances</span><span class="sxs-lookup"><span data-stu-id="b0e8b-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="b0e8b-149">Data Factory</span><span class="sxs-lookup"><span data-stu-id="b0e8b-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="b0e8b-150">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b0e8b-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="b0e8b-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b0e8b-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="b0e8b-152">DNS</span><span class="sxs-lookup"><span data-stu-id="b0e8b-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="b0e8b-153">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b0e8b-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="b0e8b-154">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b0e8b-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="b0e8b-155">Key Vault</span><span class="sxs-lookup"><span data-stu-id="b0e8b-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="b0e8b-156">Meld u Analytics / Operational Insights</span><span class="sxs-lookup"><span data-stu-id="b0e8b-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="b0e8b-157">Media Services</span><span class="sxs-lookup"><span data-stu-id="b0e8b-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="b0e8b-158">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b0e8b-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="b0e8b-159">Mobile Services</span><span class="sxs-lookup"><span data-stu-id="b0e8b-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="b0e8b-160">Controle</span><span class="sxs-lookup"><span data-stu-id="b0e8b-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="b0e8b-161">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="b0e8b-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="b0e8b-162">Netwerken</span><span class="sxs-lookup"><span data-stu-id="b0e8b-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="b0e8b-163">Netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="b0e8b-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="b0e8b-164">Notification Hub-Service</span><span class="sxs-lookup"><span data-stu-id="b0e8b-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="b0e8b-165">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="b0e8b-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="b0e8b-166">Scheduler</span><span class="sxs-lookup"><span data-stu-id="b0e8b-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="b0e8b-167">Zoeken</span><span class="sxs-lookup"><span data-stu-id="b0e8b-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="b0e8b-168">Service Bus</span><span class="sxs-lookup"><span data-stu-id="b0e8b-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="b0e8b-169">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b0e8b-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="b0e8b-170">SQL Database</span><span class="sxs-lookup"><span data-stu-id="b0e8b-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="b0e8b-171">Storage</span><span class="sxs-lookup"><span data-stu-id="b0e8b-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="b0e8b-172">StorSimple-systeem</span><span class="sxs-lookup"><span data-stu-id="b0e8b-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="b0e8b-173">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b0e8b-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="b0e8b-174">Abonnement</span><span class="sxs-lookup"><span data-stu-id="b0e8b-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="b0e8b-175">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b0e8b-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="b0e8b-176">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b0e8b-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="b0e8b-177">Virtuele-Machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="b0e8b-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="b0e8b-178">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="b0e8b-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="b0e8b-179">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="b0e8b-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="b0e8b-180">Abonnement - limieten voor Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b0e8b-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="b0e8b-181">Hallo volgende limieten van toepassing wanneer u hello Azure Resource Manager en Azure-resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="b0e8b-182">Limieten die niet zijn gewijzigd met hello Azure Resource Manager worden hieronder niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="b0e8b-183">Raadpleeg de vorige tabel toohello voor deze limieten.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="b0e8b-184">Zie voor meer informatie over het verwerken van limieten voor Resource Manager-verzoeken [beperking Resource Manager-aanvragen](resource-manager-request-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="b0e8b-185">Limieten voor resourcegroep</span><span class="sxs-lookup"><span data-stu-id="b0e8b-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="b0e8b-186">Limieten voor virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="b0e8b-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="b0e8b-187">Limieten voor de virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="b0e8b-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="b0e8b-188">Limieten voor virtuele Machines - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b0e8b-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="b0e8b-189">Hallo volgende limieten van toepassing wanneer u hello Azure Resource Manager en Azure-resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="b0e8b-190">Limieten die niet zijn gewijzigd met hello Azure Resource Manager worden hieronder niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="b0e8b-191">Raadpleeg de vorige tabel toohello voor deze limieten.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="b0e8b-192">Limieten voor virtuele-Machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="b0e8b-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="b0e8b-193">Container exemplaren limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="b0e8b-194">Netwerklimieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="b0e8b-195">Netwerklimieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="b0e8b-196">Toepassingsgateway beperkt</span><span class="sxs-lookup"><span data-stu-id="b0e8b-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="b0e8b-197">Grenzen van netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="b0e8b-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="b0e8b-198">Traffic Manager-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="b0e8b-199">DNS-beperkingen</span><span class="sxs-lookup"><span data-stu-id="b0e8b-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="b0e8b-200">Opslaglimieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-200">Storage limits</span></span>
<span data-ttu-id="b0e8b-201">Zie voor meer informatie over opslagaccountlimieten [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="b0e8b-202">Service opslaglimieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="b0e8b-203">Schijfruimtelimiet van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b0e8b-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="b0e8b-204">Zie [grootten van virtuele machines](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="b0e8b-205">Beheerde virtuele-machineschijven</span><span class="sxs-lookup"><span data-stu-id="b0e8b-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="b0e8b-206">Niet-beheerde virtuele-machineschijven</span><span class="sxs-lookup"><span data-stu-id="b0e8b-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="b0e8b-207">Resource Provider opslaglimieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="b0e8b-208">Limieten voor cloud-Services</span><span class="sxs-lookup"><span data-stu-id="b0e8b-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="b0e8b-209">App Service-beperkingen</span><span class="sxs-lookup"><span data-stu-id="b0e8b-209">App Service limits</span></span>
<span data-ttu-id="b0e8b-210">Hallo volgende die App Service-beperkingen zijn limieten voor Web-Apps, Mobile Apps, API-Apps en Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="b0e8b-211">Scheduler-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="b0e8b-212">Batch-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="b0e8b-213">Limieten voor BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="b0e8b-213">BizTalk Services limits</span></span>
<span data-ttu-id="b0e8b-214">Hallo volgende tabel toont Hallo limieten voor Azure Biztalk Services.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="b0e8b-215">Azure DB Cosmos-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="b0e8b-216">Azure Cosmos-database is een wereldwijde schaal-database in welke doorvoer en de opslag kan worden geschaald toohandle wat uw toepassing vereist.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="b0e8b-217">Als u vragen over Hallo scale Azure Cosmos DB biedt hebt, stuur e-mail tooaskcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="b0e8b-218">Mobile Engagement-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="b0e8b-219">Limieten voor zoeken</span><span class="sxs-lookup"><span data-stu-id="b0e8b-219">Search limits</span></span>
<span data-ttu-id="b0e8b-220">Prijscategorieën bepalen Hallo capaciteit en de grenzen van uw zoekservice.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="b0e8b-221">Lagen zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="b0e8b-221">Tiers include:</span></span>

* <span data-ttu-id="b0e8b-222">*Gratis* multitenant-service, gedeeld met andere Azure-abonnees die zijn bestemd voor evaluatie en klein ontwikkeling projecten.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="b0e8b-223">*Basic* biedt speciale computerbronnen voor productieworkloads op kleinere schaal omhoog toothree replica's voor query maximaal beschikbare werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="b0e8b-224">*Standard (S1, S2, S3, S3 high-density)* voor productieworkloads groter wordt.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="b0e8b-225">Meerdere niveaus bestaan binnen Hallo standaardcategorie, zodat u kunt de configuratie van een bron die het meest geschikt is voor uw profiel werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="b0e8b-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="b0e8b-226">**Limieten per abonnement**</span><span class="sxs-lookup"><span data-stu-id="b0e8b-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="b0e8b-227">**Limieten per zoekservice**</span><span class="sxs-lookup"><span data-stu-id="b0e8b-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="b0e8b-228">toolearn meer informatie over limieten voor een meer gedetailleerd niveau, zoals de documentgrootte van het, query's per seconde, sleutels, aanvragen en antwoorden, Zie [Servicelimieten in Azure Search](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="b0e8b-229">Media Services-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="b0e8b-230">CDN-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="b0e8b-231">Limieten voor Mobile Services</span><span class="sxs-lookup"><span data-stu-id="b0e8b-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="b0e8b-232">Monitor limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="b0e8b-233">Notification Hub Servicelimieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="b0e8b-234">Limieten voor Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b0e8b-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="b0e8b-235">Service Bus-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="b0e8b-236">IoT Hub-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="b0e8b-237">Hiermee beperkt u Data Factory</span><span class="sxs-lookup"><span data-stu-id="b0e8b-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="b0e8b-238">Data Lake Analytics-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="b0e8b-239">Data Lake Store-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="b0e8b-240">Stream Analytics-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="b0e8b-241">Active Directory-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="b0e8b-242">Azure Event raster limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="b0e8b-243">Azure RemoteApp-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="b0e8b-244">Beperkt StorSimple-systeem</span><span class="sxs-lookup"><span data-stu-id="b0e8b-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="b0e8b-245">Log Analytics beperkt</span><span class="sxs-lookup"><span data-stu-id="b0e8b-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="b0e8b-246">Back-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="b0e8b-247">Site Recovery-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="b0e8b-248">Application Insights-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="b0e8b-249">Limieten voor API Management</span><span class="sxs-lookup"><span data-stu-id="b0e8b-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="b0e8b-250">Azure Redis-Cache-limieten</span><span class="sxs-lookup"><span data-stu-id="b0e8b-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="b0e8b-251">Limieten voor Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="b0e8b-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="b0e8b-252">Meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="b0e8b-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="b0e8b-253">Limieten voor Automation</span><span class="sxs-lookup"><span data-stu-id="b0e8b-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="b0e8b-254">Limieten voor SQL-Database</span><span class="sxs-lookup"><span data-stu-id="b0e8b-254">SQL Database limits</span></span>
<span data-ttu-id="b0e8b-255">Zie voor SQL-Database-limieten, [limieten voor SQL Database](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b0e8b-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b0e8b-256">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b0e8b-256">See also</span></span>
[<span data-ttu-id="b0e8b-257">Inzicht in de Azure-limieten en toeneemt</span><span class="sxs-lookup"><span data-stu-id="b0e8b-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="b0e8b-258">Virtual Machine and Cloud Service Sizes for Azure</span><span class="sxs-lookup"><span data-stu-id="b0e8b-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b0e8b-259">Grootten voor Cloudservices</span><span class="sxs-lookup"><span data-stu-id="b0e8b-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

