---
title: aaaMove Azure-resources toonew abonnement of resourcegroep groep | Microsoft Docs
description: Gebruik Azure Resource Manager toomove resources tooa nieuwe resourcegroep of abonnement.
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
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="31dfd-103">Verplaatsen van resources toonew resourcegroep of abonnement</span><span class="sxs-lookup"><span data-stu-id="31dfd-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="31dfd-104">Dit onderwerp leest u hoe toomove resources tooeither een nieuw abonnement of een nieuwe bron groeperen in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="31dfd-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="31dfd-105">U kunt Hallo-portal, PowerShell, Azure CLI of Hallo REST-API toomove resource gebruiken.</span><span class="sxs-lookup"><span data-stu-id="31dfd-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="31dfd-106">Hallo migratiebewerkingen in dit onderwerp zijn beschikbaar tooyou zonder eventuele hulp van de ondersteuning van Azure.</span><span class="sxs-lookup"><span data-stu-id="31dfd-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="31dfd-107">Bij het verplaatsen van resources, worden zowel Hallo brongroep en de doelgroep Hallo Hallo tijdens vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="31dfd-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="31dfd-108">Schrijf- en verwijderbewerkingen op Hallo resourcegroepen worden geblokkeerd totdat Hallo verplaatsen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="31dfd-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="31dfd-109">Deze vergrendeling betekent dat u niet kunt toevoegen, bijwerken of verwijderen van resources in resourcegroepen hello, maar dit betekent niet dat Hallo resources worden bevroren.</span><span class="sxs-lookup"><span data-stu-id="31dfd-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="31dfd-110">Als u een SQL-Server en de database tooa nieuwe resourcegroep hebt verplaatst, ervaringen een toepassing die gebruikmaakt van Hallo database zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="31dfd-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="31dfd-111">Dit kan nog steeds lezen en schrijven van toohello-database.</span><span class="sxs-lookup"><span data-stu-id="31dfd-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="31dfd-112">U kunt Hallo-locatie van Hallo-bron niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="31dfd-113">Door een resource alleen verplaatst u deze tooa nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="31dfd-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="31dfd-114">de nieuwe resourcegroep Hallo mag een andere locatie hebben, maar die verandert niet Hallo-locatie van het Hallo-resource.</span><span class="sxs-lookup"><span data-stu-id="31dfd-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="31dfd-115">Dit artikel wordt beschreven hoe toomove resources binnen een bestaande Azure-account aanbieden.</span><span class="sxs-lookup"><span data-stu-id="31dfd-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="31dfd-116">Als u daadwerkelijk wilt toochange uw Azure-account biedt (zoals een upgrade van betalen naar gebruik toopre betalen) terwijl u toowork met uw bestaande bronnen, Zie [overschakelen van uw Azure-abonnement tooanother aanbieding](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="31dfd-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="31dfd-117">Controlelijst voor het verplaatsen van resources</span><span class="sxs-lookup"><span data-stu-id="31dfd-117">Checklist before moving resources</span></span>
<span data-ttu-id="31dfd-118">Er zijn een aantal belangrijke stappen tooperform voordat u doorgaat een resource.</span><span class="sxs-lookup"><span data-stu-id="31dfd-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="31dfd-119">U kunt fouten voorkomen door te controleren of aan de volgende voorwaarden is voldaan.</span><span class="sxs-lookup"><span data-stu-id="31dfd-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="31dfd-120">Hallo bron- en doelserver abonnementen moeten bestaan binnen Hallo dezelfde [Azure Active Directory-tenant](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="31dfd-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="31dfd-121">beide abonnementen hebben dezelfde Hallo toocheck tenant-ID, gebruikt u Azure PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="31dfd-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="31dfd-122">Azure PowerShell gebruiken:</span><span class="sxs-lookup"><span data-stu-id="31dfd-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="31dfd-123">Voor Azure CLI 2.0 gebruiken:</span><span class="sxs-lookup"><span data-stu-id="31dfd-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="31dfd-124">Als Hallo tenant-id's voor zijn Hallo bron- en doelserver geen abonnementen Hallo dezelfde, kunt u proberen toochange Hallo directory voor Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="31dfd-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="31dfd-125">Deze optie is echter alleen beschikbaar tooService beheerders die zijn aangemeld met een Microsoft-account (niet in een organisatie-account).</span><span class="sxs-lookup"><span data-stu-id="31dfd-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="31dfd-126">Hallo-directory, aanmelden toohello wijzigen tooattempt [klassieke portal](https://manage.windowsazure.com/), en selecteer **instellingen**, en Hallo abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="31dfd-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="31dfd-127">Als hello **Directory bewerken** pictogram beschikbaar is, selecteert u deze toochange hello Azure Active Directory die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="31dfd-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![directory bewerken](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="31dfd-129">Als dit pictogram niet beschikbaar is, moet u contact op met de ondersteuning toomove Hallo resources tooa nieuwe tenant.</span><span class="sxs-lookup"><span data-stu-id="31dfd-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="31dfd-130">Hallo-service moet Hallo mogelijkheid toomove bronnen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="31dfd-131">Dit onderwerp vindt u welke services kunnen verplaatsen bronnen en welke services de zwevende resources niet inschakelt.</span><span class="sxs-lookup"><span data-stu-id="31dfd-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="31dfd-132">Hallo doelabonnement moet zijn geregistreerd voor de resourceprovider Hallo Hallo resource worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="31dfd-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="31dfd-133">Als niet zo is, u ontvangt een foutmelding weergegeven dat Hallo **abonnement is niet geregistreerd voor een brontype**.</span><span class="sxs-lookup"><span data-stu-id="31dfd-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="31dfd-134">U kunt dit probleem tegenkomen bij het verplaatsen van een nieuw abonnement van bron tooa, maar dat abonnement nog nooit is gebruikt met dat resourcetype.</span><span class="sxs-lookup"><span data-stu-id="31dfd-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="31dfd-135">toolearn hoe toocheck Hallo registratiestatus en registreren van de resourceproviders, Zie [resourceproviders en typen](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="31dfd-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="31dfd-136">Wanneer toocall ondersteunt</span><span class="sxs-lookup"><span data-stu-id="31dfd-136">When toocall support</span></span>
<span data-ttu-id="31dfd-137">U kunt de meeste bronnen via Hallo selfservice operations weergegeven in dit onderwerp kunt verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="31dfd-138">Hallo selfservice bewerkingen om te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="31dfd-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="31dfd-139">Resource Manager-resources wilt verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="31dfd-140">Klassieke resources op basis van toohello verplaatsen [klassieke implementatie beperkingen](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="31dfd-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="31dfd-141">Wanneer u moet contact op met ondersteuning:</span><span class="sxs-lookup"><span data-stu-id="31dfd-141">Call support when you need to:</span></span>

* <span data-ttu-id="31dfd-142">Verplaats uw resources tooa nieuwe Azure-account (en Azure Active Directory-tenant).</span><span class="sxs-lookup"><span data-stu-id="31dfd-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="31dfd-143">Klassieke resources verplaatsen, maar hebben problemen met Hallo beperkingen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="31dfd-144">Services waarmee verplaatsen</span><span class="sxs-lookup"><span data-stu-id="31dfd-144">Services that enable move</span></span>
<span data-ttu-id="31dfd-145">Op dit moment zijn Hallo-services die bewegende tooboth een nieuwe resourcegroep en abonnement inschakelen:</span><span class="sxs-lookup"><span data-stu-id="31dfd-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="31dfd-146">API Management</span><span class="sxs-lookup"><span data-stu-id="31dfd-146">API Management</span></span>
* <span data-ttu-id="31dfd-147">App Service-apps (web-apps) - Zie [App Service-beperkingen](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="31dfd-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="31dfd-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="31dfd-148">Application Insights</span></span>
* <span data-ttu-id="31dfd-149">Automatisering</span><span class="sxs-lookup"><span data-stu-id="31dfd-149">Automation</span></span>
* <span data-ttu-id="31dfd-150">Batch</span><span class="sxs-lookup"><span data-stu-id="31dfd-150">Batch</span></span>
* <span data-ttu-id="31dfd-151">Bing-kaarten</span><span class="sxs-lookup"><span data-stu-id="31dfd-151">Bing Maps</span></span>
* <span data-ttu-id="31dfd-152">CDN</span><span class="sxs-lookup"><span data-stu-id="31dfd-152">CDN</span></span>
* <span data-ttu-id="31dfd-153">Cloud Services - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="31dfd-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="31dfd-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="31dfd-154">Cognitive Services</span></span>
* <span data-ttu-id="31dfd-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="31dfd-155">Content Moderator</span></span>
* <span data-ttu-id="31dfd-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="31dfd-156">Data Catalog</span></span>
* <span data-ttu-id="31dfd-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="31dfd-157">Data Factory</span></span>
* <span data-ttu-id="31dfd-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="31dfd-158">Data Lake Analytics</span></span>
* <span data-ttu-id="31dfd-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="31dfd-159">Data Lake Store</span></span>
* <span data-ttu-id="31dfd-160">DNS</span><span class="sxs-lookup"><span data-stu-id="31dfd-160">DNS</span></span>
* <span data-ttu-id="31dfd-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="31dfd-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="31dfd-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="31dfd-162">Event Hubs</span></span>
* <span data-ttu-id="31dfd-163">HDInsight-clusters - Zie [HDInsight-beperkingen](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="31dfd-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="31dfd-164">IoT-Hubs</span><span class="sxs-lookup"><span data-stu-id="31dfd-164">IoT Hubs</span></span>
* <span data-ttu-id="31dfd-165">Key Vault</span><span class="sxs-lookup"><span data-stu-id="31dfd-165">Key Vault</span></span>
* <span data-ttu-id="31dfd-166">Taakverdelers</span><span class="sxs-lookup"><span data-stu-id="31dfd-166">Load Balancers</span></span>
* <span data-ttu-id="31dfd-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="31dfd-167">Logic Apps</span></span>
* <span data-ttu-id="31dfd-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="31dfd-168">Machine Learning</span></span>
* <span data-ttu-id="31dfd-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="31dfd-169">Media Services</span></span>
* <span data-ttu-id="31dfd-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="31dfd-170">Mobile Engagement</span></span>
* <span data-ttu-id="31dfd-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="31dfd-171">Notification Hubs</span></span>
* <span data-ttu-id="31dfd-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="31dfd-172">Operational Insights</span></span>
* <span data-ttu-id="31dfd-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="31dfd-173">Operations Management</span></span>
* <span data-ttu-id="31dfd-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="31dfd-174">Power BI</span></span>
* <span data-ttu-id="31dfd-175">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="31dfd-175">Redis Cache</span></span>
* <span data-ttu-id="31dfd-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="31dfd-176">Scheduler</span></span>
* <span data-ttu-id="31dfd-177">Search</span><span class="sxs-lookup"><span data-stu-id="31dfd-177">Search</span></span>
* <span data-ttu-id="31dfd-178">Server Management</span><span class="sxs-lookup"><span data-stu-id="31dfd-178">Server Management</span></span>
* <span data-ttu-id="31dfd-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="31dfd-179">Service Bus</span></span>
* <span data-ttu-id="31dfd-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="31dfd-180">Service Fabric</span></span>
* <span data-ttu-id="31dfd-181">Storage</span><span class="sxs-lookup"><span data-stu-id="31dfd-181">Storage</span></span>
* <span data-ttu-id="31dfd-182">Opslag (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="31dfd-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="31dfd-183">Stream Analytics - Stream Analytics-taken kunnen niet worden verplaatst, bij uitvoering in status.</span><span class="sxs-lookup"><span data-stu-id="31dfd-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="31dfd-184">SQL Database-server - hello database en de server moeten zich bevinden in Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="31dfd-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="31dfd-185">Wanneer u een SQL-server hebt verplaatst, worden ook alle databases die zijn verplaatst.</span><span class="sxs-lookup"><span data-stu-id="31dfd-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="31dfd-186">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="31dfd-186">Traffic Manager</span></span>
* <span data-ttu-id="31dfd-187">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="31dfd-187">Virtual Machines</span></span>
* <span data-ttu-id="31dfd-188">Virtuele Machines met een certificaat dat is opgeslagen in de Sleutelkluis - verplaatsen toonew resourcegroep in hetzelfde abonnement is ingeschakeld, maar cross abonnement verplaatsen is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="31dfd-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="31dfd-189">Virtuele Machines (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="31dfd-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="31dfd-190">Schaalsets voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="31dfd-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="31dfd-191">Virtuele netwerken - momenteel, een peered virtueel netwerk kan niet worden verplaatst tot VNet-peering is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="31dfd-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="31dfd-192">Als uitgeschakeld, Hallo virtueel netwerk kan worden verplaatst en Hallo VNet-peering kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="31dfd-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="31dfd-193">Bovendien kan een virtueel netwerk verplaatste tooa ander abonnement niet als Hallo virtueel netwerk subnet met resourcenavigatiekoppelingen bevat.</span><span class="sxs-lookup"><span data-stu-id="31dfd-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="31dfd-194">Een virtueel netwerksubnet heeft bijvoorbeeld een resource navigatiekoppeling wanneer een bron van de redis Microsoft.Cache wordt geïmplementeerd in dit subnet.</span><span class="sxs-lookup"><span data-stu-id="31dfd-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="31dfd-195">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="31dfd-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="31dfd-196">Services die niet verplaatsen inschakelen</span><span class="sxs-lookup"><span data-stu-id="31dfd-196">Services that do not enable move</span></span>
<span data-ttu-id="31dfd-197">Hallo-services die op dit moment niet inschakelen voor het verplaatsen van een resource zijn:</span><span class="sxs-lookup"><span data-stu-id="31dfd-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="31dfd-198">AD-domeinservices</span><span class="sxs-lookup"><span data-stu-id="31dfd-198">AD Domain Services</span></span>
* <span data-ttu-id="31dfd-199">Hybride AD Health-Service</span><span class="sxs-lookup"><span data-stu-id="31dfd-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="31dfd-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="31dfd-200">Application Gateway</span></span>
* <span data-ttu-id="31dfd-201">Beschikbaarheidssets met virtuele Machines met schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="31dfd-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="31dfd-202">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="31dfd-202">BizTalk Services</span></span>
* <span data-ttu-id="31dfd-203">Container Service</span><span class="sxs-lookup"><span data-stu-id="31dfd-203">Container Service</span></span>
* <span data-ttu-id="31dfd-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="31dfd-204">Express Route</span></span>
* <span data-ttu-id="31dfd-205">DevTest Labs - verplaatsen toonew resourcegroep in hetzelfde abonnement is ingeschakeld, maar cross-abonnement verplaatsen is niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="31dfd-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="31dfd-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="31dfd-206">Dynamics LCS</span></span>
* <span data-ttu-id="31dfd-207">Installatiekopieën die zijn gemaakt op basis van schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="31dfd-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="31dfd-208">Beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="31dfd-208">Managed Disks</span></span>
* <span data-ttu-id="31dfd-209">Beheerde toepassingen</span><span class="sxs-lookup"><span data-stu-id="31dfd-209">Managed Applications</span></span>
* <span data-ttu-id="31dfd-210">Recovery Services-kluis: ook doen door niet verplaatsen Hallo Compute, netwerk en opslag van de resources die zijn gekoppeld aan de Recovery Services Hallo-kluis, Zie [Recovery Services-beperkingen](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="31dfd-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="31dfd-211">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="31dfd-211">Security</span></span>
* <span data-ttu-id="31dfd-212">Momentopnamen die zijn gemaakt op basis van schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="31dfd-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="31dfd-213">StorSimple-Apparaatbeheer</span><span class="sxs-lookup"><span data-stu-id="31dfd-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="31dfd-214">Virtuele Machines met beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="31dfd-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="31dfd-215">Virtuele netwerken (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="31dfd-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="31dfd-216">Virtuele Machines die zijn gemaakt op basis van bronnen van de Marketplace - kan niet worden verplaatst tussen abonnementen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="31dfd-217">Resource moet toobe gemaakt in het huidige abonnement Hallo en opnieuw wordt geïmplementeerd in een nieuw abonnement Hallo</span><span class="sxs-lookup"><span data-stu-id="31dfd-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="31dfd-218">App Service-beperkingen</span><span class="sxs-lookup"><span data-stu-id="31dfd-218">App Service limitations</span></span>
<span data-ttu-id="31dfd-219">Als u werkt met App Service-apps, kunt u alleen een App Service-abonnement niet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="31dfd-220">toomove App Service-apps, uw opties zijn:</span><span class="sxs-lookup"><span data-stu-id="31dfd-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="31dfd-221">Hallo App Service-abonnement en alle andere App Service-resources in die groep tooa nieuwe resource resourcegroep die geen App Service-resources verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="31dfd-222">Deze vereiste manier die moet u zelfs verplaatsen Hallo App Service-resources die niet zijn gekoppeld aan Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="31dfd-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="31dfd-223">Hallo apps tooa andere resourcegroep verplaatsen, maar alle App Service-abonnementen in de oorspronkelijke resourcegroep Hallo houden.</span><span class="sxs-lookup"><span data-stu-id="31dfd-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="31dfd-224">Hallo Hallo App Service plan hoeft niet tooreside in dezelfde resourcegroep als Hallo-app voor Hallo app toofunction correct.</span><span class="sxs-lookup"><span data-stu-id="31dfd-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="31dfd-225">Bijvoorbeeld, als uw resourcegroep bevat:</span><span class="sxs-lookup"><span data-stu-id="31dfd-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="31dfd-226">**Web-a** die is gekoppeld aan **plan een**</span><span class="sxs-lookup"><span data-stu-id="31dfd-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="31dfd-227">**Web-b** die is gekoppeld aan **plan b**</span><span class="sxs-lookup"><span data-stu-id="31dfd-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="31dfd-228">Uw opties zijn:</span><span class="sxs-lookup"><span data-stu-id="31dfd-228">Your options are:</span></span>

* <span data-ttu-id="31dfd-229">Verplaats **web-a**, **plan een**, **web-b**, en **plan b**</span><span class="sxs-lookup"><span data-stu-id="31dfd-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="31dfd-230">Verplaats **web-a** en **web-b**</span><span class="sxs-lookup"><span data-stu-id="31dfd-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="31dfd-231">Verplaats **web-a**</span><span class="sxs-lookup"><span data-stu-id="31dfd-231">Move **web-a**</span></span>
* <span data-ttu-id="31dfd-232">Verplaats **web-b**</span><span class="sxs-lookup"><span data-stu-id="31dfd-232">Move **web-b**</span></span>

<span data-ttu-id="31dfd-233">Alle andere combinaties hebben betrekking op verlaten achter een brontype dat bij het verplaatsen van een App Service-abonnement (type van de bron-App Service) kan niet worden achtergelaten.</span><span class="sxs-lookup"><span data-stu-id="31dfd-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="31dfd-234">Als uw web-app bevindt zich in een andere resourcegroep dan de App Service-abonnement, maar u toomove beide tooa nieuwe resourcegroep wilt, moet u Hallo verplaatsen in twee stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="31dfd-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="31dfd-235">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="31dfd-235">For example:</span></span>

* <span data-ttu-id="31dfd-236">**Web-a** bevindt zich in **web-groep**</span><span class="sxs-lookup"><span data-stu-id="31dfd-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="31dfd-237">**plan een** bevindt zich in **plan-groep**</span><span class="sxs-lookup"><span data-stu-id="31dfd-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="31dfd-238">Gewenste **web-a** en **plan een** tooreside in **gecombineerd groep**</span><span class="sxs-lookup"><span data-stu-id="31dfd-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="31dfd-239">tooaccomplish dit verplaatst, twee afzonderlijke move-bewerkingen uitvoeren in Hallo volgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="31dfd-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="31dfd-240">Hallo verplaatsen **web-a** te**plan-groep**</span><span class="sxs-lookup"><span data-stu-id="31dfd-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="31dfd-241">Verplaats **web-a** en **plan een** te**gecombineerd groep**.</span><span class="sxs-lookup"><span data-stu-id="31dfd-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="31dfd-242">U kunt een nieuwe App Service-certificaat tooa-resourcegroep of abonnement zonder problemen verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="31dfd-243">Als uw web-app een SSL-certificaat bevat dat u hebt aangeschaft extern en toohello-app geüpload, moet u Hallo-certificaat voordat zwevend Hallo web-app verwijderen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="31dfd-244">U kunt bijvoorbeeld Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="31dfd-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="31dfd-245">Hallo geüpload certificaat verwijderen uit Hallo web-app</span><span class="sxs-lookup"><span data-stu-id="31dfd-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="31dfd-246">Hallo-web-app te verplaatsen</span><span class="sxs-lookup"><span data-stu-id="31dfd-246">Move hello web app</span></span>
3. <span data-ttu-id="31dfd-247">Hallo certificaat toohello web-app uploaden</span><span class="sxs-lookup"><span data-stu-id="31dfd-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="31dfd-248">Recovery Services-beperkingen</span><span class="sxs-lookup"><span data-stu-id="31dfd-248">Recovery Services limitations</span></span>
<span data-ttu-id="31dfd-249">Verplaatsing is niet ingeschakeld voor de opslag, netwerk, of rekenresources tooset van herstel na noodgevallen gebruikt met Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="31dfd-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="31dfd-250">Bijvoorbeeld, Stel dat u de replicatie van uw lokale machines tooa storage-account (Storage1) hebt ingesteld en Hallo beveiligd machine toocome-up wilt na failover tooAzure als een virtuele machine (VM1) tooa virtueel netwerk (Network1 gekoppelde).</span><span class="sxs-lookup"><span data-stu-id="31dfd-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="31dfd-251">U kunt een van deze Azure-resources - Storage1, VM1, niet verplaatsen en Network1 - via resource groepen binnen Hallo dezelfde abonnement of tussen abonnementen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="31dfd-252">HDInsight-beperkingen</span><span class="sxs-lookup"><span data-stu-id="31dfd-252">HDInsight limitations</span></span>

<span data-ttu-id="31dfd-253">U kunt de HDInsight-clusters tooa nieuw abonnement of resourcegroep verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="31dfd-254">U kunt echter niet verplaatsen tussen abonnementen Hallo networking resources toohello gekoppelde HDInsight-cluster (zoals Hallo virtueel netwerk, een NIC of een load balancer).</span><span class="sxs-lookup"><span data-stu-id="31dfd-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="31dfd-255">U kunt bovendien tooa nieuwe resourcegroep een NIC die is aangesloten tooa virtuele machine voor het Hallo-cluster niet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="31dfd-256">Wanneer u een nieuw abonnement voor HDInsight-cluster tooa verplaatst, moet u eerst andere bronnen (zoals Hallo storage-account) verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="31dfd-257">Verplaats Hallo HDInsight-cluster op zichzelf.</span><span class="sxs-lookup"><span data-stu-id="31dfd-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="31dfd-258">Beperkingen voor klassieke implementatie</span><span class="sxs-lookup"><span data-stu-id="31dfd-258">Classic deployment limitations</span></span>
<span data-ttu-id="31dfd-259">Hallo verschillen opties voor het verplaatsen van resources die zijn geïmplementeerd via het klassieke model Hallo op basis van of het verplaatsen van resources binnen een abonnement of een nieuw abonnement tooa Hallo.</span><span class="sxs-lookup"><span data-stu-id="31dfd-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="31dfd-260">Hetzelfde abonnement</span><span class="sxs-lookup"><span data-stu-id="31dfd-260">Same subscription</span></span>
<span data-ttu-id="31dfd-261">Wanneer u resources van één resource groep tooanother resourcegroep binnen hetzelfde abonnement behoren, Hallo volgen beperkingen van toepassing hello verplaatst:</span><span class="sxs-lookup"><span data-stu-id="31dfd-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="31dfd-262">Virtuele netwerken (klassiek) kunnen niet worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="31dfd-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="31dfd-263">Virtuele machines (klassiek) moeten worden verplaatst met Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="31dfd-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="31dfd-264">Cloudservice kan alleen worden verplaatst als Hallo verplaatsen alle virtuele machines bevat.</span><span class="sxs-lookup"><span data-stu-id="31dfd-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="31dfd-265">Slechts één cloudservice kan tegelijk worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="31dfd-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="31dfd-266">Slechts één opslagaccount (klassiek) kan tegelijk worden verplaatst.</span><span class="sxs-lookup"><span data-stu-id="31dfd-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="31dfd-267">Storage-account (klassiek) kan niet worden verplaatst in Hallo dezelfde bewerking met een virtuele machine of een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="31dfd-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="31dfd-268">toomove klassieke resources tooa nieuwe resourcegroep binnen hetzelfde abonnement hello, gebruikt u Hallo standaard migratiebewerkingen via Hallo [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), of [REST-API](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="31dfd-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="31dfd-269">U dezelfde bewerkingen Hallo terwijl u gebruikt voor het verplaatsen van Resource Manager-resources.</span><span class="sxs-lookup"><span data-stu-id="31dfd-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="31dfd-270">Nieuw abonnement</span><span class="sxs-lookup"><span data-stu-id="31dfd-270">New subscription</span></span>
<span data-ttu-id="31dfd-271">Bij het verplaatsen van resources tooa nieuw abonnement toepassing hello volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="31dfd-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="31dfd-272">Alle klassieke resources in het Hallo-abonnement moeten worden verplaatst in Hallo dezelfde bewerking.</span><span class="sxs-lookup"><span data-stu-id="31dfd-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="31dfd-273">Hallo doelabonnement mag geen andere klassieke resources bevatten.</span><span class="sxs-lookup"><span data-stu-id="31dfd-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="31dfd-274">Hallo verplaatsen kan alleen worden aangevraagd via een afzonderlijke REST-API voor klassieke verplaatst.</span><span class="sxs-lookup"><span data-stu-id="31dfd-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="31dfd-275">Hallo-opdrachten voor het verplaatsen van standaard Resource Manager werken niet bij het verplaatsen van klassieke resources tooa nieuw abonnement.</span><span class="sxs-lookup"><span data-stu-id="31dfd-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="31dfd-276">toomove klassieke resources tooa nieuw abonnement, gebruik Hallo REST-bewerkingen die specifieke tooclassic resources zijn.</span><span class="sxs-lookup"><span data-stu-id="31dfd-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="31dfd-277">toouse REST, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="31dfd-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="31dfd-278">Controleer als Hallo bronabonnement kan deelnemen in een abonnementoverschrijdende verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="31dfd-279">Volgende bewerking hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="31dfd-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="31dfd-280">In de aanvraagtekst hello, zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="31dfd-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="31dfd-281">Hallo-antwoord voor Hallo validatiebewerking heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="31dfd-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="31dfd-282">Controleer als Hallo doelabonnement kan deelnemen in een abonnementoverschrijdende verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="31dfd-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="31dfd-283">Volgende bewerking hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="31dfd-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="31dfd-284">In de aanvraagtekst hello, zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="31dfd-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="31dfd-285">Hallo-reactie is in dezelfde notatie als de validatie van abonnement Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="31dfd-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="31dfd-286">Verplaats alle klassieke resources uit één abonnement tooanother abonnement als beide abonnementen gevalideerd worden, met de volgende bewerking Hallo:</span><span class="sxs-lookup"><span data-stu-id="31dfd-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="31dfd-287">In de aanvraagtekst hello, zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="31dfd-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="31dfd-288">Hallo mogelijk voor enkele minuten uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="31dfd-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="31dfd-289">De portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="31dfd-289">Use portal</span></span>
<span data-ttu-id="31dfd-290">toomove resources, selecteer Hallo resourcegroep met deze bronnen, en selecteer vervolgens Hallo **verplaatsen** knop.</span><span class="sxs-lookup"><span data-stu-id="31dfd-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![Verplaatsen van resources](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="31dfd-292">Selecteer of u Hallo resources tooa nieuwe resourcegroep of een nieuw abonnement overstapt.</span><span class="sxs-lookup"><span data-stu-id="31dfd-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="31dfd-293">Selecteer Hallo resources toomove en Hallo bestemming resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="31dfd-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="31dfd-294">Bevestig dat u voor deze resources en selecteer tooupdate scripts moet **OK**.</span><span class="sxs-lookup"><span data-stu-id="31dfd-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="31dfd-295">Als u in de vorige stap Hallo Hallo abonnement bewerkingspictogram hebt geselecteerd, moet u ook het doelabonnement Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="31dfd-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![Selecteer bestemming](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="31dfd-297">In **meldingen**, ziet u dat Hallo verplaatsen bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="31dfd-297">In **Notifications**, you see that hello move operation is running.</span></span>

![verplaatsing status weergeven](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="31dfd-299">Wanneer deze is voltooid, wordt u gewaarschuwd van Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="31dfd-299">When it has completed, you are notified of hello result.</span></span>

![resultaat van de verplaatsing weergeven](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="31dfd-301">PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="31dfd-301">Use PowerShell</span></span>
<span data-ttu-id="31dfd-302">toomove bestaande resources tooanother resourcegroep of abonnement, gebruikt u Hallo `Move-AzureRmResource` opdracht.</span><span class="sxs-lookup"><span data-stu-id="31dfd-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="31dfd-303">Hallo eerste voorbeeld laat zien hoe toomove één resource tooa nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="31dfd-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="31dfd-304">Hallo tweede voorbeeld wordt getoond hoe toomove meerdere resources tooa nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="31dfd-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="31dfd-305">toomove tooa nieuw abonnement, een waarde bevatten voor Hallo `DestinationSubscriptionId` parameter.</span><span class="sxs-lookup"><span data-stu-id="31dfd-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="31dfd-306">U wordt gevraagd dat u wilt dat toomove hello tooconfirm opgegeven resources.</span><span class="sxs-lookup"><span data-stu-id="31dfd-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="31dfd-307">Azure CLI 2.0 gebruiken</span><span class="sxs-lookup"><span data-stu-id="31dfd-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="31dfd-308">toomove bestaande resources tooanother resourcegroep of abonnement, gebruikt u Hallo `az resource move` opdracht.</span><span class="sxs-lookup"><span data-stu-id="31dfd-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="31dfd-309">Hallo resource-id's van Hallo resources toomove bieden.</span><span class="sxs-lookup"><span data-stu-id="31dfd-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="31dfd-310">U kunt resource-id's met de volgende opdracht Hallo krijgen:</span><span class="sxs-lookup"><span data-stu-id="31dfd-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="31dfd-311">Hallo volgende voorbeeld ziet u hoe toomove een storage account tooa nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="31dfd-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="31dfd-312">In Hallo `--ids` parameter, Geef een door spaties gescheiden lijst met Hallo resource-id's toomove.</span><span class="sxs-lookup"><span data-stu-id="31dfd-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="31dfd-313">toomove tooa nieuw abonnement, bieden Hallo `--destination-subscription-id` parameter.</span><span class="sxs-lookup"><span data-stu-id="31dfd-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="31dfd-314">Azure CLI 1.0 gebruiken</span><span class="sxs-lookup"><span data-stu-id="31dfd-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="31dfd-315">toomove bestaande resources tooanother resourcegroep of abonnement, gebruikt u Hallo `azure resource move` opdracht.</span><span class="sxs-lookup"><span data-stu-id="31dfd-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="31dfd-316">Hallo resource-id's van Hallo resources toomove bieden.</span><span class="sxs-lookup"><span data-stu-id="31dfd-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="31dfd-317">U kunt resource-id's met de volgende opdracht Hallo krijgen:</span><span class="sxs-lookup"><span data-stu-id="31dfd-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="31dfd-318">Welke retourneert Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="31dfd-318">Which returns hello following format:</span></span>

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

<span data-ttu-id="31dfd-319">Hallo volgende voorbeeld ziet u hoe toomove een storage account tooa nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="31dfd-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="31dfd-320">In Hallo `-i` parameter, Geef een door komma's gescheiden lijst met Hallo resource-id's toomove.</span><span class="sxs-lookup"><span data-stu-id="31dfd-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="31dfd-321">U wordt gevraagd dat u wilt dat toomove hello tooconfirm van de opgegeven bron.</span><span class="sxs-lookup"><span data-stu-id="31dfd-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="31dfd-322">REST API gebruiken</span><span class="sxs-lookup"><span data-stu-id="31dfd-322">Use REST API</span></span>
<span data-ttu-id="31dfd-323">toomove bestaande resources tooanother resourcegroep of abonnement, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="31dfd-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="31dfd-324">In de aanvraagtekst hello geeft u de doelresourcegroep hello en Hallo resources toomove.</span><span class="sxs-lookup"><span data-stu-id="31dfd-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="31dfd-325">Zie voor meer informatie over Hallo move REST-bewerking [verplaatsen van resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="31dfd-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31dfd-326">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31dfd-326">Next steps</span></span>
* <span data-ttu-id="31dfd-327">toolearn over PowerShell-cmdlets voor het beheren van uw abonnement, Zie [Azure PowerShell gebruiken met Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="31dfd-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="31dfd-328">toolearn over Azure CLI-opdrachten voor het beheren van uw abonnement, Zie [Using hello Azure CLI met Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="31dfd-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="31dfd-329">toolearn over portal functies voor het beheren van uw abonnement, Zie [hello Azure portal toomanage bronnen](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="31dfd-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="31dfd-330">toolearn over het toepassen van een logische tooyour organisatiebronnen, Zie [Using tags tooorganize uw resources](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="31dfd-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
