---
title: Azure-resources naar nieuwe abonnement of de resource-groep verplaatsen | Microsoft Docs
description: Azure Resource Manager gebruiken voor resources verplaatsen naar een nieuwe resourcegroep of abonnement.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="10ffd-103">Resources verplaatsen naar de nieuwe resourcegroep of abonnement</span><span class="sxs-lookup"><span data-stu-id="10ffd-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="10ffd-104">Dit onderwerp leest u hoe u resources verplaatsen naar een nieuw abonnement of een nieuwe resourcegroep in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="10ffd-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="10ffd-105">U kunt de portal, PowerShell, Azure CLI of de REST-API resource verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="10ffd-106">De verplaatsing bewerkingen in dit onderwerp voor u beschikbaar zijn zonder eventuele hulp van de ondersteuning van Azure.</span><span class="sxs-lookup"><span data-stu-id="10ffd-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="10ffd-107">Bij het verplaatsen van resources, worden zowel de bronnengroep als de doelgroep vergrendeld tijdens de bewerking.</span><span class="sxs-lookup"><span data-stu-id="10ffd-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="10ffd-108">Schrijven en verwijderen van bewerkingen op de brongroepen worden geblokkeerd totdat de verplaatsing is voltooid.</span><span class="sxs-lookup"><span data-stu-id="10ffd-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="10ffd-109">Deze vergrendeling betekent dat u niet kunt toevoegen, bijwerken of verwijderen van resources in de resourcegroepen, maar dit betekent niet dat de bronnen worden bevroren.</span><span class="sxs-lookup"><span data-stu-id="10ffd-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="10ffd-110">Als u een SQL-Server en de bijbehorende database naar een nieuwe resourcegroep verplaatst, ervaringen een toepassing die gebruikmaakt van de database zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="10ffd-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="10ffd-111">Dit kan nog steeds lezen en schrijven naar de database.</span><span class="sxs-lookup"><span data-stu-id="10ffd-111">It can still read and write to the database.</span></span>

<span data-ttu-id="10ffd-112">U kunt de locatie van de resource niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="10ffd-113">Het verplaatsen van een resource alleen verplaatst naar een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10ffd-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="10ffd-114">De nieuwe resourcegroep mag een andere locatie hebben, maar die niet de locatie van de bron wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="10ffd-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="10ffd-115">Dit artikel wordt beschreven hoe u resources binnen een bestaande Azure-account aanbieden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="10ffd-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="10ffd-116">Als u daadwerkelijk wijzigen van uw Azure-account biedt (zoals een upgrade van betalen naar gebruik vooraf betalen wilt) maar blijft werken met uw bestaande bronnen, Zie [overschakelen van uw Azure-abonnement op een andere aanbieding](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="10ffd-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="10ffd-117">Controlelijst voor het verplaatsen van resources</span><span class="sxs-lookup"><span data-stu-id="10ffd-117">Checklist before moving resources</span></span>
<span data-ttu-id="10ffd-118">Voordat u een resource verplaatst, moeten er enkele belangrijke stappen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10ffd-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="10ffd-119">U kunt fouten voorkomen door te controleren of aan de volgende voorwaarden is voldaan.</span><span class="sxs-lookup"><span data-stu-id="10ffd-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="10ffd-120">De bron- en doelserver abonnementen moeten bestaan binnen dezelfde [Azure Active Directory-tenant](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="10ffd-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="10ffd-121">Om te controleren of beide abonnementen dezelfde tenant-ID hebben, gebruikt u Azure PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="10ffd-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="10ffd-122">Azure PowerShell gebruiken:</span><span class="sxs-lookup"><span data-stu-id="10ffd-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="10ffd-123">Voor Azure CLI 2.0 gebruiken:</span><span class="sxs-lookup"><span data-stu-id="10ffd-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="10ffd-124">Als de tenant-id's voor de bron- en doelserver abonnementen niet hetzelfde zijn zijn, kunt u proberen de map voor het abonnement wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="10ffd-125">Deze optie is echter alleen beschikbaar voor Service-beheerders die zijn aangemeld met een Microsoft-account (niet in een organisatie-account).</span><span class="sxs-lookup"><span data-stu-id="10ffd-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="10ffd-126">Om te proberen de map wordt gewijzigd, moet u zich aanmelden bij de [klassieke portal](https://manage.windowsazure.com/), en selecteer **instellingen**, en selecteer het abonnement.</span><span class="sxs-lookup"><span data-stu-id="10ffd-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="10ffd-127">Als de **Directory bewerken** pictogram beschikbaar is, selecteert u het wijzigen van de gekoppelde Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10ffd-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![directory bewerken](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="10ffd-129">Als dit pictogram niet beschikbaar is, moet u contact op met ondersteuning om de resources verplaatsen naar een nieuwe tenant.</span><span class="sxs-lookup"><span data-stu-id="10ffd-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="10ffd-130">De service moet de mogelijkheid activeren om resources te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="10ffd-131">Dit onderwerp vindt u welke services kunnen verplaatsen bronnen en welke services de zwevende resources niet inschakelt.</span><span class="sxs-lookup"><span data-stu-id="10ffd-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="10ffd-132">Het doelabonnement moet zijn geregistreerd voor de resourceprovider van de resource die wordt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="10ffd-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="10ffd-133">Als u niet het geval is, er een foutbericht met de mededeling dat de **abonnement is niet geregistreerd voor een brontype**.</span><span class="sxs-lookup"><span data-stu-id="10ffd-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="10ffd-134">U kunt dit probleem tegenkomen bij het verplaatsen van een resource naar een nieuw abonnement, terwijl dat abonnement nooit is gebruikt met dat type resource.</span><span class="sxs-lookup"><span data-stu-id="10ffd-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="10ffd-135">Raadpleeg [Resourceproviders en typen](resource-manager-supported-services.md) om te leren hoe u de registratiestatus controleert en resourceproviders registreert.</span><span class="sxs-lookup"><span data-stu-id="10ffd-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="10ffd-136">Het aanroepen van ondersteuning</span><span class="sxs-lookup"><span data-stu-id="10ffd-136">When to call support</span></span>
<span data-ttu-id="10ffd-137">U kunt de meeste resources via de selfservice bewerkingen die wordt weergegeven in dit onderwerp kunt verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="10ffd-138">De bewerkingen selfservice gebruiken:</span><span class="sxs-lookup"><span data-stu-id="10ffd-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="10ffd-139">Resource Manager-resources wilt verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="10ffd-140">Verplaatsen van klassieke resources volgens de [klassieke implementatie beperkingen](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="10ffd-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="10ffd-141">Wanneer u moet contact op met ondersteuning:</span><span class="sxs-lookup"><span data-stu-id="10ffd-141">Call support when you need to:</span></span>

* <span data-ttu-id="10ffd-142">Uw resources verplaatsen naar een nieuwe Azure-account (en Azure Active Directory-tenant).</span><span class="sxs-lookup"><span data-stu-id="10ffd-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="10ffd-143">Klassieke resources verplaatsen, maar hebben problemen met de beperkingen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="10ffd-144">Services waarmee verplaatsen</span><span class="sxs-lookup"><span data-stu-id="10ffd-144">Services that enable move</span></span>
<span data-ttu-id="10ffd-145">Op dit moment zijn de services die verplaatsen naar een nieuwe resourcegroep en een abonnement inschakelen:</span><span class="sxs-lookup"><span data-stu-id="10ffd-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="10ffd-146">API Management</span><span class="sxs-lookup"><span data-stu-id="10ffd-146">API Management</span></span>
* <span data-ttu-id="10ffd-147">App Service-apps (web-apps) - Zie [App Service-beperkingen](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="10ffd-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="10ffd-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="10ffd-148">Application Insights</span></span>
* <span data-ttu-id="10ffd-149">Automatisering</span><span class="sxs-lookup"><span data-stu-id="10ffd-149">Automation</span></span>
* <span data-ttu-id="10ffd-150">Batch</span><span class="sxs-lookup"><span data-stu-id="10ffd-150">Batch</span></span>
* <span data-ttu-id="10ffd-151">Bing-kaarten</span><span class="sxs-lookup"><span data-stu-id="10ffd-151">Bing Maps</span></span>
* <span data-ttu-id="10ffd-152">CDN</span><span class="sxs-lookup"><span data-stu-id="10ffd-152">CDN</span></span>
* <span data-ttu-id="10ffd-153">Cloud Services - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="10ffd-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="10ffd-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="10ffd-154">Cognitive Services</span></span>
* <span data-ttu-id="10ffd-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="10ffd-155">Content Moderator</span></span>
* <span data-ttu-id="10ffd-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="10ffd-156">Data Catalog</span></span>
* <span data-ttu-id="10ffd-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="10ffd-157">Data Factory</span></span>
* <span data-ttu-id="10ffd-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="10ffd-158">Data Lake Analytics</span></span>
* <span data-ttu-id="10ffd-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="10ffd-159">Data Lake Store</span></span>
* <span data-ttu-id="10ffd-160">DNS</span><span class="sxs-lookup"><span data-stu-id="10ffd-160">DNS</span></span>
* <span data-ttu-id="10ffd-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10ffd-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="10ffd-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="10ffd-162">Event Hubs</span></span>
* <span data-ttu-id="10ffd-163">HDInsight-clusters - Zie [HDInsight-beperkingen](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="10ffd-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="10ffd-164">IoT-Hubs</span><span class="sxs-lookup"><span data-stu-id="10ffd-164">IoT Hubs</span></span>
* <span data-ttu-id="10ffd-165">Key Vault</span><span class="sxs-lookup"><span data-stu-id="10ffd-165">Key Vault</span></span>
* <span data-ttu-id="10ffd-166">Taakverdelers</span><span class="sxs-lookup"><span data-stu-id="10ffd-166">Load Balancers</span></span>
* <span data-ttu-id="10ffd-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="10ffd-167">Logic Apps</span></span>
* <span data-ttu-id="10ffd-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="10ffd-168">Machine Learning</span></span>
* <span data-ttu-id="10ffd-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="10ffd-169">Media Services</span></span>
* <span data-ttu-id="10ffd-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="10ffd-170">Mobile Engagement</span></span>
* <span data-ttu-id="10ffd-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="10ffd-171">Notification Hubs</span></span>
* <span data-ttu-id="10ffd-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="10ffd-172">Operational Insights</span></span>
* <span data-ttu-id="10ffd-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="10ffd-173">Operations Management</span></span>
* <span data-ttu-id="10ffd-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="10ffd-174">Power BI</span></span>
* <span data-ttu-id="10ffd-175">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="10ffd-175">Redis Cache</span></span>
* <span data-ttu-id="10ffd-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="10ffd-176">Scheduler</span></span>
* <span data-ttu-id="10ffd-177">Search</span><span class="sxs-lookup"><span data-stu-id="10ffd-177">Search</span></span>
* <span data-ttu-id="10ffd-178">Server Management</span><span class="sxs-lookup"><span data-stu-id="10ffd-178">Server Management</span></span>
* <span data-ttu-id="10ffd-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="10ffd-179">Service Bus</span></span>
* <span data-ttu-id="10ffd-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="10ffd-180">Service Fabric</span></span>
* <span data-ttu-id="10ffd-181">Storage</span><span class="sxs-lookup"><span data-stu-id="10ffd-181">Storage</span></span>
* <span data-ttu-id="10ffd-182">Opslag (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="10ffd-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="10ffd-183">Stream Analytics - Stream Analytics-taken kunnen niet worden verplaatst, bij uitvoering in status.</span><span class="sxs-lookup"><span data-stu-id="10ffd-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="10ffd-184">SQL Database-server - database en server moet zich bevinden in dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10ffd-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="10ffd-185">Wanneer u een SQL-server hebt verplaatst, worden ook alle databases die zijn verplaatst.</span><span class="sxs-lookup"><span data-stu-id="10ffd-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="10ffd-186">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="10ffd-186">Traffic Manager</span></span>
* <span data-ttu-id="10ffd-187">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="10ffd-187">Virtual Machines</span></span>
* <span data-ttu-id="10ffd-188">Virtuele Machines met een certificaat wordt opgeslagen in de Sleutelkluis - verplaatsen naar de nieuwe resource groep in hetzelfde abonnement is ingeschakeld, maar het verplaatsen van cross-abonnement is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="10ffd-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="10ffd-189">Virtuele Machines (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="10ffd-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="10ffd-190">Schaalsets voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="10ffd-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="10ffd-191">Virtuele netwerken - momenteel, een peered virtueel netwerk kan niet worden verplaatst tot VNet-peering is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="10ffd-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="10ffd-192">Als uitgeschakeld, het virtuele netwerk kan worden verplaatst en de VNet-peering kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="10ffd-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="10ffd-193">Bovendien kan niet een virtueel netwerk worden verplaatst naar een ander abonnement, als het virtuele netwerk subnet met resourcenavigatiekoppelingen bevat.</span><span class="sxs-lookup"><span data-stu-id="10ffd-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="10ffd-194">Een virtueel netwerksubnet heeft bijvoorbeeld een resource navigatiekoppeling wanneer een bron van de redis Microsoft.Cache wordt geïmplementeerd in dit subnet.</span><span class="sxs-lookup"><span data-stu-id="10ffd-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="10ffd-195">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="10ffd-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="10ffd-196">Services die niet verplaatsen inschakelen</span><span class="sxs-lookup"><span data-stu-id="10ffd-196">Services that do not enable move</span></span>
<span data-ttu-id="10ffd-197">De services die op dit moment niet inschakelen voor het verplaatsen van een resource zijn:</span><span class="sxs-lookup"><span data-stu-id="10ffd-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="10ffd-198">AD-domeinservices</span><span class="sxs-lookup"><span data-stu-id="10ffd-198">AD Domain Services</span></span>
* <span data-ttu-id="10ffd-199">Hybride AD Health-Service</span><span class="sxs-lookup"><span data-stu-id="10ffd-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="10ffd-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="10ffd-200">Application Gateway</span></span>
* <span data-ttu-id="10ffd-201">Beschikbaarheidssets met virtuele Machines met schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="10ffd-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="10ffd-202">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="10ffd-202">BizTalk Services</span></span>
* <span data-ttu-id="10ffd-203">Container Service</span><span class="sxs-lookup"><span data-stu-id="10ffd-203">Container Service</span></span>
* <span data-ttu-id="10ffd-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="10ffd-204">Express Route</span></span>
* <span data-ttu-id="10ffd-205">DevTest Labs - te verplaatsen naar een nieuwe resourcegroep in hetzelfde abonnement is ingeschakeld, maar cross abonnement verplaatsen is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="10ffd-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="10ffd-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="10ffd-206">Dynamics LCS</span></span>
* <span data-ttu-id="10ffd-207">Installatiekopieën die zijn gemaakt op basis van schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="10ffd-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="10ffd-208">Beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="10ffd-208">Managed Disks</span></span>
* <span data-ttu-id="10ffd-209">Beheerde toepassingen</span><span class="sxs-lookup"><span data-stu-id="10ffd-209">Managed Applications</span></span>
* <span data-ttu-id="10ffd-210">Recovery Services-kluis - ook komen niet verplaatsen van de Compute, Network en Storage-resources die zijn gekoppeld aan de Recovery Services-kluis, Zie [Recovery Services-beperkingen](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="10ffd-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="10ffd-211">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="10ffd-211">Security</span></span>
* <span data-ttu-id="10ffd-212">Momentopnamen die zijn gemaakt op basis van schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="10ffd-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="10ffd-213">StorSimple-Apparaatbeheer</span><span class="sxs-lookup"><span data-stu-id="10ffd-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="10ffd-214">Virtuele Machines met beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="10ffd-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="10ffd-215">Virtuele netwerken (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="10ffd-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="10ffd-216">Virtuele Machines die zijn gemaakt op basis van bronnen van de Marketplace - kan niet worden verplaatst tussen abonnementen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="10ffd-217">Resource moet worden gemaakt in het huidige abonnement en opnieuw wordt geïmplementeerd in het nieuwe abonnement</span><span class="sxs-lookup"><span data-stu-id="10ffd-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="10ffd-218">App Service-beperkingen</span><span class="sxs-lookup"><span data-stu-id="10ffd-218">App Service limitations</span></span>
<span data-ttu-id="10ffd-219">Als u werkt met App Service-apps, kunt u alleen een App Service-abonnement niet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="10ffd-220">Uw opties zijn beschikbaar voor het verplaatsen van App Service-apps:</span><span class="sxs-lookup"><span data-stu-id="10ffd-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="10ffd-221">De App Service-abonnement en alle andere App Service-resources in die resourcegroep verplaatsen naar een nieuwe resourcegroep die geen App Service-resources.</span><span class="sxs-lookup"><span data-stu-id="10ffd-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="10ffd-222">Deze vereiste betekent dat u zelfs de App Service-resources die niet gekoppeld aan de App Service-abonnement zijn te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="10ffd-223">De apps naar een andere resourcegroep verplaatsen, maar blijven alle App Service-abonnementen in de oorspronkelijke resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10ffd-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="10ffd-224">De App Service-abonnement hoeft niet te bevinden zich in dezelfde resourcegroep als de app voor de app te laten functioneren.</span><span class="sxs-lookup"><span data-stu-id="10ffd-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="10ffd-225">Bijvoorbeeld, als uw resourcegroep bevat:</span><span class="sxs-lookup"><span data-stu-id="10ffd-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="10ffd-226">**Web-a** die is gekoppeld aan **plan een**</span><span class="sxs-lookup"><span data-stu-id="10ffd-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="10ffd-227">**Web-b** die is gekoppeld aan **plan b**</span><span class="sxs-lookup"><span data-stu-id="10ffd-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="10ffd-228">Uw opties zijn:</span><span class="sxs-lookup"><span data-stu-id="10ffd-228">Your options are:</span></span>

* <span data-ttu-id="10ffd-229">Verplaats **web-a**, **plan een**, **web-b**, en **plan b**</span><span class="sxs-lookup"><span data-stu-id="10ffd-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="10ffd-230">Verplaats **web-a** en **web-b**</span><span class="sxs-lookup"><span data-stu-id="10ffd-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="10ffd-231">Verplaats **web-a**</span><span class="sxs-lookup"><span data-stu-id="10ffd-231">Move **web-a**</span></span>
* <span data-ttu-id="10ffd-232">Verplaats **web-b**</span><span class="sxs-lookup"><span data-stu-id="10ffd-232">Move **web-b**</span></span>

<span data-ttu-id="10ffd-233">Alle andere combinaties hebben betrekking op verlaten achter een brontype dat bij het verplaatsen van een App Service-abonnement (type van de bron-App Service) kan niet worden achtergelaten.</span><span class="sxs-lookup"><span data-stu-id="10ffd-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="10ffd-234">Als uw web-app bevindt zich in een andere resourcegroep dan de App Service-abonnement, maar u wilt zowel voor een nieuwe resourcegroep te verplaatsen, moet u de verplaatsing in twee stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="10ffd-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="10ffd-235">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="10ffd-235">For example:</span></span>

* <span data-ttu-id="10ffd-236">**Web-a** bevindt zich in **web-groep**</span><span class="sxs-lookup"><span data-stu-id="10ffd-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="10ffd-237">**plan een** bevindt zich in **plan-groep**</span><span class="sxs-lookup"><span data-stu-id="10ffd-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="10ffd-238">Gewenste **web-a** en **plan een** zich bevinden **gecombineerd groep**</span><span class="sxs-lookup"><span data-stu-id="10ffd-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="10ffd-239">Voer hiertoe verplaatsing twee afzonderlijke migratiebewerkingen in de volgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="10ffd-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="10ffd-240">Verplaats de **web-a** naar **plan-groep**</span><span class="sxs-lookup"><span data-stu-id="10ffd-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="10ffd-241">Verplaats **web-a** en **plan een** naar **gecombineerd groep**.</span><span class="sxs-lookup"><span data-stu-id="10ffd-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="10ffd-242">U kunt een App Service-certificaat verplaatsen naar een nieuwe resourcegroep of abonnement zonder problemen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="10ffd-243">Als uw web-app een SSL-certificaat dat u hebt aangeschaft extern en geüpload naar de app bevat, moet u het certificaat verwijderen voordat u de web-app.</span><span class="sxs-lookup"><span data-stu-id="10ffd-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="10ffd-244">U kunt bijvoorbeeld de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="10ffd-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="10ffd-245">Het geüploade certificaat verwijderen van de web-app</span><span class="sxs-lookup"><span data-stu-id="10ffd-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="10ffd-246">Verplaatsen van de web-app</span><span class="sxs-lookup"><span data-stu-id="10ffd-246">Move the web app</span></span>
3. <span data-ttu-id="10ffd-247">Upload het certificaat naar de web-app</span><span class="sxs-lookup"><span data-stu-id="10ffd-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="10ffd-248">Recovery Services-beperkingen</span><span class="sxs-lookup"><span data-stu-id="10ffd-248">Recovery Services limitations</span></span>
<span data-ttu-id="10ffd-249">Verplaatsen is niet ingeschakeld voor de opslag, netwerk, of Compute-resources die worden gebruikt voor het instellen van herstel na noodgevallen met Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="10ffd-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="10ffd-250">Stel dat u de replicatie van uw lokale machines naar een opslagaccount (Storage1) hebt ingesteld en wilt dat de beveiligde machine actief na een failover naar Azure als een virtuele machine (VM1) gekoppeld aan een virtueel netwerk (Network1).</span><span class="sxs-lookup"><span data-stu-id="10ffd-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="10ffd-251">U kunt deze Azure-resources - Storage1, VM1 en Network1 - niet verplaatsen, tussen resourcegroepen binnen hetzelfde abonnement of tussen abonnementen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="10ffd-252">HDInsight-beperkingen</span><span class="sxs-lookup"><span data-stu-id="10ffd-252">HDInsight limitations</span></span>

<span data-ttu-id="10ffd-253">U kunt de HDInsight-clusters verplaatsen naar een nieuw abonnement of resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10ffd-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="10ffd-254">U kunt echter niet verplaatsen tussen abonnementen de netwerkresources die zijn gekoppeld aan het HDInsight-cluster (zoals het virtuele netwerk, een NIC of een load balancer).</span><span class="sxs-lookup"><span data-stu-id="10ffd-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="10ffd-255">Bovendien verplaatsen u niet naar een nieuwe resourcegroep een NIC die is gekoppeld aan een virtuele machine voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="10ffd-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="10ffd-256">Wanneer u een HDInsight-cluster naar een nieuw abonnement verplaatst, moet u eerst andere bronnen (zoals het storage-account) verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="10ffd-257">Verplaats het HDInsight-cluster op zichzelf.</span><span class="sxs-lookup"><span data-stu-id="10ffd-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="10ffd-258">Beperkingen voor klassieke implementatie</span><span class="sxs-lookup"><span data-stu-id="10ffd-258">Classic deployment limitations</span></span>
<span data-ttu-id="10ffd-259">De opties voor het verplaatsen van resources die zijn geïmplementeerd via het klassieke model verschillen op basis van of het verplaatsen van de resources binnen een abonnement of in een nieuw abonnement.</span><span class="sxs-lookup"><span data-stu-id="10ffd-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="10ffd-260">Hetzelfde abonnement</span><span class="sxs-lookup"><span data-stu-id="10ffd-260">Same subscription</span></span>
<span data-ttu-id="10ffd-261">Bij het verplaatsen van resources van een resourcegroep naar een andere resourcegroep binnen hetzelfde abonnement, gelden de volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="10ffd-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="10ffd-262">Virtuele netwerken (klassiek) kunnen niet worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="10ffd-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="10ffd-263">Virtuele machines (klassiek) moeten worden verplaatst met de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="10ffd-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="10ffd-264">Cloudservice kan alleen worden verplaatst, wanneer de verplaatsing alle virtuele machines bevat.</span><span class="sxs-lookup"><span data-stu-id="10ffd-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="10ffd-265">Slechts één cloudservice kan tegelijk worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="10ffd-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="10ffd-266">Slechts één opslagaccount (klassiek) kan tegelijk worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="10ffd-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="10ffd-267">Storage-account (klassiek) kan niet worden verplaatst in dezelfde bewerking met een virtuele machine of een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="10ffd-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="10ffd-268">Klassieke om resources te verplaatsen naar een nieuwe resourcegroep binnen hetzelfde abonnement, gebruiken de standaard migratiebewerkingen via de [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), of [REST-API](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="10ffd-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="10ffd-269">U dezelfde bewerkingen zoals u voor het verplaatsen van Resource Manager-resources.</span><span class="sxs-lookup"><span data-stu-id="10ffd-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="10ffd-270">Nieuw abonnement</span><span class="sxs-lookup"><span data-stu-id="10ffd-270">New subscription</span></span>
<span data-ttu-id="10ffd-271">Bij het verplaatsen van resources in een nieuw abonnement, gelden de volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="10ffd-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="10ffd-272">Alle klassieke resources in het abonnement moeten worden verplaatst in dezelfde bewerking.</span><span class="sxs-lookup"><span data-stu-id="10ffd-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="10ffd-273">Het doelabonnement mag geen andere klassieke resources bevatten.</span><span class="sxs-lookup"><span data-stu-id="10ffd-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="10ffd-274">De verplaatsing kan alleen worden aangevraagd via een afzonderlijke REST-API voor klassieke verplaatst.</span><span class="sxs-lookup"><span data-stu-id="10ffd-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="10ffd-275">De standaardopdrachten verplaatsen van Resource Manager werken niet bij het klassieke resources verplaatsen naar een nieuw abonnement.</span><span class="sxs-lookup"><span data-stu-id="10ffd-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="10ffd-276">Klassieke om resources te verplaatsen naar een nieuw abonnement, de REST-bewerkingen die specifiek voor klassieke resources zijn te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="10ffd-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="10ffd-277">Voor het gebruik van REST, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="10ffd-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="10ffd-278">Controleer als het bronabonnement deel uitmaken van een verplaatsing abonnementoverschrijdende.</span><span class="sxs-lookup"><span data-stu-id="10ffd-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="10ffd-279">Gebruik de volgende bewerking:</span><span class="sxs-lookup"><span data-stu-id="10ffd-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="10ffd-280">In de aanvraagtekst zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="10ffd-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="10ffd-281">De reactie voor de validatiebewerking is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="10ffd-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="10ffd-282">Controleer of het doelabonnement in een verplaatsing abonnementoverschrijdende deelnemen kan.</span><span class="sxs-lookup"><span data-stu-id="10ffd-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="10ffd-283">Gebruik de volgende bewerking:</span><span class="sxs-lookup"><span data-stu-id="10ffd-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="10ffd-284">In de aanvraagtekst zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="10ffd-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="10ffd-285">De reactie is in dezelfde indeling als de validatie van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="10ffd-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="10ffd-286">Verplaats alle klassieke resources uit één abonnement als beide abonnementen gevalideerd worden, een ander abonnement met de volgende bewerking:</span><span class="sxs-lookup"><span data-stu-id="10ffd-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="10ffd-287">In de aanvraagtekst zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="10ffd-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="10ffd-288">De bewerking kan enkele minuten uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10ffd-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="10ffd-289">De portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="10ffd-289">Use portal</span></span>
<span data-ttu-id="10ffd-290">Selecteer de resourcegroep met deze bronnen om resources te verplaatsen, en selecteer vervolgens de **verplaatsen** knop.</span><span class="sxs-lookup"><span data-stu-id="10ffd-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![Verplaatsen van resources](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="10ffd-292">Selecteer of u de resources naar een nieuwe resourcegroep of een nieuw abonnement verplaatsen wilt.</span><span class="sxs-lookup"><span data-stu-id="10ffd-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="10ffd-293">Selecteer de resources te verplaatsen en de resourcegroep voor de bestemming.</span><span class="sxs-lookup"><span data-stu-id="10ffd-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="10ffd-294">Bevestig dat u wilt bijwerken scripts voor deze bronnen, en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="10ffd-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="10ffd-295">Als u het pictogram van het abonnement bewerken in de vorige stap hebt geselecteerd, moet u ook het doelabonnement.</span><span class="sxs-lookup"><span data-stu-id="10ffd-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![Selecteer bestemming](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="10ffd-297">In **meldingen**, ziet u dat de move-bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10ffd-297">In **Notifications**, you see that the move operation is running.</span></span>

![verplaatsing status weergeven](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="10ffd-299">Wanneer deze is voltooid, wordt u gewaarschuwd van het resultaat.</span><span class="sxs-lookup"><span data-stu-id="10ffd-299">When it has completed, you are notified of the result.</span></span>

![resultaat van de verplaatsing weergeven](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="10ffd-301">PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="10ffd-301">Use PowerShell</span></span>
<span data-ttu-id="10ffd-302">U kunt bestaande resources verplaatsen naar een andere resourcegroep of abonnement met de `Move-AzureRmResource` opdracht.</span><span class="sxs-lookup"><span data-stu-id="10ffd-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="10ffd-303">Het eerste voorbeeld laat zien hoe één resource verplaatsen naar een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10ffd-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="10ffd-304">Het tweede voorbeeld laat zien hoe meerdere resources verplaatsen naar een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10ffd-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="10ffd-305">Als u wilt verplaatsen naar een nieuw abonnement, een waarde bevatten voor de `DestinationSubscriptionId` parameter.</span><span class="sxs-lookup"><span data-stu-id="10ffd-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="10ffd-306">U wordt gevraagd te bevestigen dat u wilt verplaatsen van de opgegeven resources.</span><span class="sxs-lookup"><span data-stu-id="10ffd-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="10ffd-307">Azure CLI 2.0 gebruiken</span><span class="sxs-lookup"><span data-stu-id="10ffd-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="10ffd-308">U kunt bestaande resources verplaatsen naar een andere resourcegroep of abonnement met de `az resource move` opdracht.</span><span class="sxs-lookup"><span data-stu-id="10ffd-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="10ffd-309">Geef de bron-id's van de resources te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="10ffd-310">U kunt krijgen resource-id's met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="10ffd-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="10ffd-311">Het volgende voorbeeld ziet hoe u een opslagaccount naar een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10ffd-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="10ffd-312">In de `--ids` parameter, Geef een door spaties gescheiden lijst van de resource-id's te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="10ffd-313">Als u wilt verplaatsen naar een nieuw abonnement, bieden de `--destination-subscription-id` parameter.</span><span class="sxs-lookup"><span data-stu-id="10ffd-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="10ffd-314">Azure CLI 1.0 gebruiken</span><span class="sxs-lookup"><span data-stu-id="10ffd-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="10ffd-315">U kunt bestaande resources verplaatsen naar een andere resourcegroep of abonnement met de `azure resource move` opdracht.</span><span class="sxs-lookup"><span data-stu-id="10ffd-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="10ffd-316">Geef de bron-id's van de resources te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="10ffd-317">U kunt krijgen resource-id's met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="10ffd-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="10ffd-318">Dit retourneert de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="10ffd-318">Which returns the following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="10ffd-319">Het volgende voorbeeld ziet hoe u een opslagaccount naar een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="10ffd-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="10ffd-320">In de `-i` parameter, voorzien in een door komma's gescheiden lijst van de resource-id's te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="10ffd-321">U wordt gevraagd te bevestigen dat u wilt verplaatsen van de opgegeven resource.</span><span class="sxs-lookup"><span data-stu-id="10ffd-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="10ffd-322">REST API gebruiken</span><span class="sxs-lookup"><span data-stu-id="10ffd-322">Use REST API</span></span>
<span data-ttu-id="10ffd-323">Bestaande om resources te verplaatsen naar een andere resourcegroep of abonnement, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="10ffd-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="10ffd-324">In de aanvraagtekst geeft u de doelresourcegroep en de resources te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10ffd-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="10ffd-325">Zie voor meer informatie over de REST-verplaatsbewerking [verplaatsen van resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="10ffd-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10ffd-326">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10ffd-326">Next steps</span></span>
* <span data-ttu-id="10ffd-327">Zie voor meer informatie over PowerShell-cmdlets voor het beheren van uw abonnement, [Azure PowerShell gebruiken met Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="10ffd-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="10ffd-328">Zie voor meer informatie over Azure CLI-opdrachten voor het beheren van uw abonnement, [met de Azure CLI met Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="10ffd-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="10ffd-329">Zie voor meer informatie over portal functies voor het beheren van uw abonnement, [om resources te beheren met behulp van de Azure-portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="10ffd-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="10ffd-330">Zie voor meer informatie over het toepassen van een logische organisatie op uw resources, [met labels om uw resources te organiseren](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="10ffd-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
