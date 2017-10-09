---
title: Azure Redis-Cache met Azure PowerShell aaaManage | Microsoft Docs
description: Meer informatie over hoe tooperform beheertaken voor Azure Redis-Cache met Azure PowerShell.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="3f850-103">Azure Redis-Cache met Azure PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="3f850-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f850-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f850-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="3f850-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="3f850-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="3f850-106">Dit onderwerp leest u hoe tooperform algemene taken, zoals het maken, bijwerken en schalen van uw Azure Redis-Cache-exemplaren hoe tooregenerate toegangstoetsen, en hoe tooview informatie over uw caches.</span><span class="sxs-lookup"><span data-stu-id="3f850-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="3f850-107">Zie voor een volledige lijst met Azure Redis-Cache PowerShell-cmdlets, [cmdlets van Azure Redis-Cache](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f850-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="3f850-108">Zie voor meer informatie over het klassieke implementatiemodel Hallo [Azure Resource Manager versus klassieke implementatie: implementatiemodellen begrijpen en de status van uw resources Hallo](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="3f850-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f850-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3f850-109">Prerequisites</span></span>
<span data-ttu-id="3f850-110">Als u Azure PowerShell al hebt geïnstalleerd, moet u Azure PowerShell versie 1.0.0 hebben of hoger.</span><span class="sxs-lookup"><span data-stu-id="3f850-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="3f850-111">U kunt controleren Hallo-versie van Azure PowerShell die u hebt geïnstalleerd met deze opdracht op Hallo Azure PowerShell-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="3f850-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="3f850-112">U moet eerst tooAzure met deze opdracht aanmelden.</span><span class="sxs-lookup"><span data-stu-id="3f850-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="3f850-113">Hallo e-mailadres van uw Azure-account en het bijbehorende wachtwoord in het dialoogvenster Hallo Microsoft Azure-aanmeldingspagina opgeven.</span><span class="sxs-lookup"><span data-stu-id="3f850-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="3f850-114">Vervolgens als u meerdere Azure-abonnementen hebt, moet u tooset uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f850-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="3f850-115">een lijst met uw huidige abonnementen toosee deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3f850-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="3f850-116">toospecify hello abonnement, Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3f850-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="3f850-117">In de Hallo voorbeeld te volgen, is de naam van Hallo abonnement `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="3f850-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="3f850-118">Voordat u Windows PowerShell met Azure Resource Manager gebruiken kunt, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="3f850-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="3f850-119">Windows PowerShell versie 3.0 of 4.0.</span><span class="sxs-lookup"><span data-stu-id="3f850-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="3f850-120">toofind hello versie van Windows PowerShell, typ:`$PSVersionTable` en controleer of de waarde van Hallo `PSVersion` 3.0 of 4.0.</span><span class="sxs-lookup"><span data-stu-id="3f850-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="3f850-121">Zie een compatibele versie tooinstall [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) of [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="3f850-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="3f850-122">tooget gedetailleerde help voor een cmdlet die u in deze zelfstudie Hallo gebruik de cmdlet Get-Help ziet.</span><span class="sxs-lookup"><span data-stu-id="3f850-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="3f850-123">Bijvoorbeeld, tooget help voor Hallo `New-AzureRmRedisCache` cmdlet, type:</span><span class="sxs-lookup"><span data-stu-id="3f850-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="3f850-124">Hoe tooconnect tooother clouds</span><span class="sxs-lookup"><span data-stu-id="3f850-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="3f850-125">Door standaard hello Azure-omgeving is `AzureCloud`, welke vertegenwoordigt Hallo globale Azure cloud-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3f850-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="3f850-126">tooconnect tooa ander exemplaar, gebruik Hallo `Add-AzureRmAccount` opdracht Hello `-Environment` of -`EnvironmentName` opdrachtregelparameter met de gewenste omgeving Hallo of de omgevingsnaam van de.</span><span class="sxs-lookup"><span data-stu-id="3f850-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="3f850-127">toosee hello lijst met beschikbare omgevingen, Voer Hallo `Get-AzureRmEnvironment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="3f850-128">tooconnect toohello Azure Government Cloud</span><span class="sxs-lookup"><span data-stu-id="3f850-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="3f850-129">tooconnect toohello Azure Government Cloud, gebruik een van de volgende opdrachten Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f850-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="3f850-130">of</span><span class="sxs-lookup"><span data-stu-id="3f850-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="3f850-131">toocreate een cache in hello Azure Government Cloud, gebruik een van de volgende locaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f850-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="3f850-132">Amerikaanse overheid Virginia</span><span class="sxs-lookup"><span data-stu-id="3f850-132">USGov Virginia</span></span>
* <span data-ttu-id="3f850-133">Amerikaanse overheid Iowa</span><span class="sxs-lookup"><span data-stu-id="3f850-133">USGov Iowa</span></span>

<span data-ttu-id="3f850-134">Zie voor meer informatie over hello Azure Government Cloud [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) en [Ontwikkelaarshandleiding voor Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="3f850-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="3f850-135">tooconnect toohello Azure China Cloud</span><span class="sxs-lookup"><span data-stu-id="3f850-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="3f850-136">tooconnect toohello Azure China Cloud, gebruik een van de volgende opdrachten Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f850-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="3f850-137">of</span><span class="sxs-lookup"><span data-stu-id="3f850-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="3f850-138">toocreate een cache in hello Azure China Cloud, gebruik een van de volgende locaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f850-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="3f850-139">China - oost</span><span class="sxs-lookup"><span data-stu-id="3f850-139">China East</span></span>
* <span data-ttu-id="3f850-140">China - noord</span><span class="sxs-lookup"><span data-stu-id="3f850-140">China North</span></span>

<span data-ttu-id="3f850-141">Zie voor meer informatie over hello Azure China Cloud [AzureChinaCloud voor Azure wordt beheerd door 21Vianet in China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="3f850-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="3f850-142">tooconnect tooMicrosoft Duitse Azure</span><span class="sxs-lookup"><span data-stu-id="3f850-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="3f850-143">tooconnect tooMicrosoft Duitse Azure, gebruik een van de volgende opdrachten Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f850-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="3f850-144">of</span><span class="sxs-lookup"><span data-stu-id="3f850-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="3f850-145">toocreate een cache in Microsoft Azure Duitsland, gebruik een van de volgende locaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f850-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="3f850-146">Duitsland - centraal</span><span class="sxs-lookup"><span data-stu-id="3f850-146">Germany Central</span></span>
* <span data-ttu-id="3f850-147">Duitsland - noordoost</span><span class="sxs-lookup"><span data-stu-id="3f850-147">Germany Northeast</span></span>

<span data-ttu-id="3f850-148">Zie voor meer informatie over Microsoft Azure Duitsland [Microsoft Azure Duitsland](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="3f850-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="3f850-149">Eigenschappen die worden gebruikt voor Azure Redis-Cache PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f850-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="3f850-150">Hallo volgende tabel bevat de eigenschappen en beschrijvingen voor vaak gebruikte parameters bij het maken en beheren van uw Azure Redis-Cache-exemplaren die gebruikmaken van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f850-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="3f850-151">Parameter</span><span class="sxs-lookup"><span data-stu-id="3f850-151">Parameter</span></span> | <span data-ttu-id="3f850-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3f850-152">Description</span></span> | <span data-ttu-id="3f850-153">Standaard</span><span class="sxs-lookup"><span data-stu-id="3f850-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f850-154">Naam</span><span class="sxs-lookup"><span data-stu-id="3f850-154">Name</span></span> |<span data-ttu-id="3f850-155">Naam van het Hallo-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-155">Name of hello cache</span></span> | |
| <span data-ttu-id="3f850-156">Locatie</span><span class="sxs-lookup"><span data-stu-id="3f850-156">Location</span></span> |<span data-ttu-id="3f850-157">Locatie van het Hallo-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-157">Location of hello cache</span></span> | |
| <span data-ttu-id="3f850-158">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3f850-158">ResourceGroupName</span></span> |<span data-ttu-id="3f850-159">Naam van resourcegroep in welke toocreate Hallo-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="3f850-160">Grootte</span><span class="sxs-lookup"><span data-stu-id="3f850-160">Size</span></span> |<span data-ttu-id="3f850-161">Hallo-grootte van Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-161">hello size of hello cache.</span></span> <span data-ttu-id="3f850-162">Geldige waarden zijn: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB</span><span class="sxs-lookup"><span data-stu-id="3f850-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="3f850-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="3f850-163">1GB</span></span> |
| <span data-ttu-id="3f850-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="3f850-164">ShardCount</span></span> |<span data-ttu-id="3f850-165">Hallo aantal shards toocreate bij het maken van een premium-cache met clustering is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3f850-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="3f850-166">Geldige waarden zijn: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="3f850-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="3f850-167">SKU</span><span class="sxs-lookup"><span data-stu-id="3f850-167">SKU</span></span> |<span data-ttu-id="3f850-168">Hiermee geeft u Hallo SKU van Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="3f850-169">Geldige waarden zijn: Basic, Standard, Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="3f850-170">Standard</span><span class="sxs-lookup"><span data-stu-id="3f850-170">Standard</span></span> |
| <span data-ttu-id="3f850-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="3f850-171">RedisConfiguration</span></span> |<span data-ttu-id="3f850-172">Hiermee geeft u Redis-configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="3f850-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="3f850-173">Zie voor meer informatie over elke instelling Hallo volgende [RedisConfiguration eigenschappen](#redisconfiguration-properties) tabel.</span><span class="sxs-lookup"><span data-stu-id="3f850-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="3f850-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="3f850-174">EnableNonSslPort</span></span> |<span data-ttu-id="3f850-175">Hiermee wordt aangegeven of het Hallo-niet-SSL-poort is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3f850-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="3f850-176">False</span><span class="sxs-lookup"><span data-stu-id="3f850-176">False</span></span> |
| <span data-ttu-id="3f850-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="3f850-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="3f850-178">Deze parameter is afgeschaft - gebruik in plaats daarvan RedisConfiguration.</span><span class="sxs-lookup"><span data-stu-id="3f850-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="3f850-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="3f850-179">StaticIP</span></span> |<span data-ttu-id="3f850-180">Bij het hosten van uw cache in een VNET, geeft een uniek IP-adres in Hallo-subnet voor Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="3f850-181">Als niet wordt opgegeven, wordt een gekozen voor u van Hallo subnet.</span><span class="sxs-lookup"><span data-stu-id="3f850-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="3f850-182">Subnet</span><span class="sxs-lookup"><span data-stu-id="3f850-182">Subnet</span></span> |<span data-ttu-id="3f850-183">Bij het hosten van uw cache in een VNET, geeft Hallo-naam van Hallo subnet in welke toodeploy Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="3f850-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3f850-184">VirtualNetwork</span></span> |<span data-ttu-id="3f850-185">Bij het hosten van uw cache in een VNET Hallo bron-ID van Hallo dan VNET in welke toodeploy Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="3f850-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="3f850-186">KeyType</span></span> |<span data-ttu-id="3f850-187">Hiermee geeft u op welke toegangssleutel tooregenerate tijdens het vernieuwen van de toegangssleutels.</span><span class="sxs-lookup"><span data-stu-id="3f850-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="3f850-188">Geldige waarden zijn: primaire, secundaire</span><span class="sxs-lookup"><span data-stu-id="3f850-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="3f850-189">RedisConfiguration eigenschappen</span><span class="sxs-lookup"><span data-stu-id="3f850-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="3f850-190">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3f850-190">Property</span></span> | <span data-ttu-id="3f850-191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3f850-191">Description</span></span> | <span data-ttu-id="3f850-192">Prijscategorieën</span><span class="sxs-lookup"><span data-stu-id="3f850-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f850-193">RDB back-up is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="3f850-193">rdb-backup-enabled</span></span> |<span data-ttu-id="3f850-194">Of [Redis-gegevenspersistentie](cache-how-to-premium-persistence.md) is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="3f850-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="3f850-195">Alleen Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-195">Premium only</span></span> |
| <span data-ttu-id="3f850-196">RDB---verbindingsreeks voor opslag</span><span class="sxs-lookup"><span data-stu-id="3f850-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="3f850-197">Hallo tekenreeks toohello storage-account voor verbinding [Redis-gegevenspersistentie](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="3f850-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="3f850-198">Alleen Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-198">Premium only</span></span> |
| <span data-ttu-id="3f850-199">back-up RDB frequentie</span><span class="sxs-lookup"><span data-stu-id="3f850-199">rdb-backup-frequency</span></span> |<span data-ttu-id="3f850-200">back-upfrequentie voor Hallo [Redis-gegevenspersistentie](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="3f850-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="3f850-201">Alleen Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-201">Premium only</span></span> |
| <span data-ttu-id="3f850-202">maxmemory gereserveerd</span><span class="sxs-lookup"><span data-stu-id="3f850-202">maxmemory-reserved</span></span> |<span data-ttu-id="3f850-203">Hiermee configureert u Hallo [geheugen gereserveerd](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) voor niet-cache-processen</span><span class="sxs-lookup"><span data-stu-id="3f850-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="3f850-204">Standard en Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-204">Standard and Premium</span></span> |
| <span data-ttu-id="3f850-205">maxmemory-beleid</span><span class="sxs-lookup"><span data-stu-id="3f850-205">maxmemory-policy</span></span> |<span data-ttu-id="3f850-206">Hiermee configureert u Hallo [taakverwijdering beleid](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) voor Hallo-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="3f850-207">Alle Prijscategorieën</span><span class="sxs-lookup"><span data-stu-id="3f850-207">All pricing tiers</span></span> |
| <span data-ttu-id="3f850-208">melding-keyspace-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="3f850-208">notify-keyspace-events</span></span> |<span data-ttu-id="3f850-209">Hiermee configureert u [keyspace-kennisgevingen](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="3f850-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="3f850-210">Standard en Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-210">Standard and Premium</span></span> |
| <span data-ttu-id="3f850-211">hash-max-ziplist-vermeldingen</span><span class="sxs-lookup"><span data-stu-id="3f850-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="3f850-212">Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="3f850-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3f850-213">Standard en Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-213">Standard and Premium</span></span> |
| <span data-ttu-id="3f850-214">hash-max-ziplist-waarde</span><span class="sxs-lookup"><span data-stu-id="3f850-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="3f850-215">Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="3f850-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3f850-216">Standard en Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-216">Standard and Premium</span></span> |
| <span data-ttu-id="3f850-217">set-max-intset-vermeldingen</span><span class="sxs-lookup"><span data-stu-id="3f850-217">set-max-intset-entries</span></span> |<span data-ttu-id="3f850-218">Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="3f850-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3f850-219">Standard en Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-219">Standard and Premium</span></span> |
| <span data-ttu-id="3f850-220">zset max-ziplist vermeldingen</span><span class="sxs-lookup"><span data-stu-id="3f850-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="3f850-221">Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="3f850-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3f850-222">Standard en Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-222">Standard and Premium</span></span> |
| <span data-ttu-id="3f850-223">zset-max-ziplist-waarde</span><span class="sxs-lookup"><span data-stu-id="3f850-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="3f850-224">Hiermee configureert u [geheugenoptimalisatie](http://redis.io/topics/memory-optimization) voor kleine cumulatieve gegevenstypen</span><span class="sxs-lookup"><span data-stu-id="3f850-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3f850-225">Standard en Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-225">Standard and Premium</span></span> |
| <span data-ttu-id="3f850-226">databases</span><span class="sxs-lookup"><span data-stu-id="3f850-226">databases</span></span> |<span data-ttu-id="3f850-227">Hiermee configureert u het aantal databases Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f850-227">Configures hello number of databases.</span></span> <span data-ttu-id="3f850-228">Deze eigenschap kan alleen bij het maken van de cache worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3f850-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="3f850-229">Standard en Premium</span><span class="sxs-lookup"><span data-stu-id="3f850-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="3f850-230">toocreate een Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="3f850-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="3f850-231">Nieuwe exemplaren van Azure Redis-Cache zijn gemaakt met behulp van Hallo [nieuw AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f850-232">Hallo eerste keer dat u een Redis-cache maken in een abonnement met Azure-portal Hallo Hallo portal registreert Hallo `Microsoft.Cache` naamruimte voor dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f850-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="3f850-233">Als u probeert toocreate Hallo eerst Redis-cache in een abonnement met behulp van PowerShell, moet u eerst registreren die naamruimte met behulp van Hallo na de opdracht; anders cmdlets zoals `New-AzureRmRedisCache` en `Get-AzureRmRedisCache` mislukken.</span><span class="sxs-lookup"><span data-stu-id="3f850-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="3f850-234">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `New-AzureRmRedisCache`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3f850-235">toocreate een cache met standaardparameters Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3f850-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="3f850-236">`ResourceGroupName`, `Name`, en `Location` vereiste parameters zijn, maar Hallo rest zijn optioneel en standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="3f850-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="3f850-237">Hallo vorige opdracht uitvoert, maakt een standaard SKU Azure Redis-Cache-exemplaar met de opgegeven naam hello, locatie en resourcegroep die 1 GB aan de grootte van niet-SSL-poort Hallo uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3f850-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="3f850-238">toocreate een premium-cache een grootte van P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), geef P3 (26 GB - 260 GB), of P4 (53 GB tot 530 GB).</span><span class="sxs-lookup"><span data-stu-id="3f850-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="3f850-239">tooenable clustering, een shard aantal opgeven met behulp van Hallo `ShardCount` parameter.</span><span class="sxs-lookup"><span data-stu-id="3f850-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="3f850-240">Hallo volgende voorbeeld wordt een premium P1 cache met 3 shards.</span><span class="sxs-lookup"><span data-stu-id="3f850-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="3f850-241">Een cache van de premium P1 6 GB groot is en omdat we drie shards Hallo totale grootte opgegeven is 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="3f850-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="3f850-242">toospecify waarden voor Hallo `RedisConfiguration` parameter, moet u waarden binnen Hallo `{}` als sleutel/waarde-paren, zoals `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="3f850-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="3f850-243">Hallo volgende voorbeeld wordt een standaard 1 GB cache met `allkeys-random` maxmemory-beleid en keyspace meldingen geconfigureerd met `KEA`.</span><span class="sxs-lookup"><span data-stu-id="3f850-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="3f850-244">Zie voor meer informatie [Keyspace-kennisgevingen (geavanceerde instellingen)](cache-configure.md#keyspace-notifications-advanced-settings) en [geheugen beleid](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="3f850-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="3f850-245">tooconfigure hello databases instellen tijdens het maken van de cache</span><span class="sxs-lookup"><span data-stu-id="3f850-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="3f850-246">Hallo `databases` instelling kan alleen tijdens het maken van de cache worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3f850-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="3f850-247">Hallo volgende voorbeeld wordt een premium P3 (26 GB)-cache met 48-databases via Hallo [nieuw AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="3f850-248">Voor meer informatie over Hallo `databases` eigenschap, Zie [serverconfiguratie Azure Redis-Cache standaard](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="3f850-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="3f850-249">Voor meer informatie over het maken van een cache met behulp van Hallo [nieuw AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, Zie de vorige Hallo [toocreate een Redis-Cache](#to-create-a-redis-cache) sectie.</span><span class="sxs-lookup"><span data-stu-id="3f850-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="3f850-250">tooupdate een Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="3f850-251">Azure Redis-Cache-exemplaren zijn bijgewerkt met Hallo [Set AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="3f850-252">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Set-AzureRmRedisCache`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3f850-253">Hallo `Set-AzureRmRedisCache` cmdlet kan worden gebruikt tooupdate eigenschappen zoals `Size`, `Sku`, `EnableNonSslPort`, en Hallo `RedisConfiguration` waarden.</span><span class="sxs-lookup"><span data-stu-id="3f850-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="3f850-254">Hallo volgende opdracht updates Hallo maxmemory-beleid voor Hallo Redis-Cache met de naam myCache.</span><span class="sxs-lookup"><span data-stu-id="3f850-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="3f850-255">tooscale een Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-255">tooscale a Redis cache</span></span>
<span data-ttu-id="3f850-256">`Set-AzureRmRedisCache`gebruikte tooscale een Azure Redis-cache-exemplaar als hello kan worden `Size`, `Sku`, of `ShardCount` eigenschappen zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3f850-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="3f850-257">Schalen van een cache met behulp van PowerShell is onderwerp toohello grenzen en richtlijnen als u een cache van schalen hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3f850-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="3f850-258">U kunt andere prijscategorie Hello volgen beperkingen tooa schalen.</span><span class="sxs-lookup"><span data-stu-id="3f850-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="3f850-259">U kan niet uit een hogere prijscategorie laag tooa lagere prijscategorie schalen.</span><span class="sxs-lookup"><span data-stu-id="3f850-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="3f850-260">U kunt geen schalen van een **Premium** cache omlaag tooa **standaard** of een **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="3f850-261">U kunt geen schalen van een **standaard** cache omlaag tooa **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="3f850-262">U kunt opschalen van een **Basic** cache tooa **standaard** cache, maar niet wijzigen Hallo grootte op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="3f850-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="3f850-263">Als u een ander formaat nodig hebt, kunt u een daaropvolgende vergroten/verkleinen bewerking toohello gewenst grootte kunt doen.</span><span class="sxs-lookup"><span data-stu-id="3f850-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="3f850-264">U kunt geen schalen van een **Basic** cache rechtstreeks tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="3f850-265">U moet de schaal van **Basic** te**standaard** in één bewerking van de schaal en vervolgens van **standaard** te**Premium** bij een volgende schaal de bewerking.</span><span class="sxs-lookup"><span data-stu-id="3f850-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="3f850-266">Kan niet worden geschaald uit een groter formaat omlaag toohello **C0 (250 MB)** grootte.</span><span class="sxs-lookup"><span data-stu-id="3f850-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="3f850-267">Zie voor meer informatie [hoe tooScale Azure Redis-Cache](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="3f850-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="3f850-268">Hallo volgende voorbeeld laat zien hoe tooscale een cache met de naam `myCache` tooa 2,5 GB cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="3f850-269">Houd er rekening mee dat deze opdracht voor zowel een Basislidmaatschap of een standaard-cache werkt.</span><span class="sxs-lookup"><span data-stu-id="3f850-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="3f850-270">Nadat u deze opdracht wordt uitgevoerd, Hallo status van Hallo cache geretourneerd (vergelijkbaar toocalling `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="3f850-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="3f850-271">Houd er rekening mee dat Hallo `ProvisioningState` is `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="3f850-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="3f850-272">Wanneer Hallo schalen van de bewerking voltooid is, Hallo `ProvisioningState` wijzigingen te`Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3f850-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="3f850-273">Als u nodig hebt toomake volgende vergroten/verkleinen bewerking, zoals het wijzigen van Basic tooStandard en vervolgens wijzigen Hallo grootte, moet u wachten tot Hallo vorige bewerking voltooid is of dat u een foutbericht vergelijkbaar toohello volgende ontvangt.</span><span class="sxs-lookup"><span data-stu-id="3f850-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="3f850-274">tooget informatie over een Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="3f850-275">U kunt informatie ophalen over een cache met behulp van Hallo [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="3f850-276">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Get-AzureRmRedisCache`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3f850-277">tooreturn informatie over alle caches in het huidige abonnement hello, voeren `Get-AzureRmRedisCache` zonder parameters.</span><span class="sxs-lookup"><span data-stu-id="3f850-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="3f850-278">informatie over alle caches in een specifieke resourcegroep tooreturn uitvoeren `Get-AzureRmRedisCache` Hello `ResourceGroupName` parameter.</span><span class="sxs-lookup"><span data-stu-id="3f850-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="3f850-279">informatie over een specifieke cache tooreturn uitvoeren `Get-AzureRmRedisCache` Hello `Name` parameter met de naam Hallo van Hallo-cache en Hallo `ResourceGroupName` Hallo resourcegroep die cache met de parameter.</span><span class="sxs-lookup"><span data-stu-id="3f850-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="3f850-280">tooretrieve hello toegangstoetsen voor Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="3f850-281">tooretrieve hello toegangssleutels voor uw cache, kunt u Hallo [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="3f850-282">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Get-AzureRmRedisCacheKey`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3f850-283">Hallo tooretrieve sleutels voor uw cache, aanroep Hallo `Get-AzureRmRedisCacheKey` cmdlet en geeft u Hallo-naam van uw cache Hallo naam van resourcegroep Hallo met Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="3f850-284">tooregenerate toegangstoetsen voor Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="3f850-285">tooregenerate hello toegangssleutels voor uw cache, kunt u Hallo [nieuw AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="3f850-286">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `New-AzureRmRedisCacheKey`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3f850-287">tooregenerate hello primaire of secundaire sleutel voor uw cache, aanroep Hallo `New-AzureRmRedisCacheKey` cmdlet Hallo geeft u een naam, resourcegroep, en Geef ofwel `Primary` of `Secondary` voor Hallo `KeyType` parameter.</span><span class="sxs-lookup"><span data-stu-id="3f850-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="3f850-288">In de Hallo voorbeeld te volgen, wordt Hallo secundaire toegangssleutel voor een cache gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3f850-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="3f850-289">toodelete een Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-289">toodelete a Redis cache</span></span>
<span data-ttu-id="3f850-290">toodelete een Redis-cache gebruiken Hallo [verwijderen AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="3f850-291">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Remove-AzureRmRedisCache`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3f850-292">Hallo in Hallo voorbeeld te volgen, cache met de naam `myCache` wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3f850-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="3f850-293">tooimport een Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-293">tooimport a Redis cache</span></span>
<span data-ttu-id="3f850-294">U kunt gegevens importeren in een Azure Redis-Cache-exemplaar met behulp van Hallo `Import-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f850-295">Import/Export is alleen beschikbaar voor [premium-laag](cache-premium-tier-intro.md) in de cache opslaat.</span><span class="sxs-lookup"><span data-stu-id="3f850-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3f850-296">Zie voor meer informatie over het importeren/exporteren [importeren en exporteren van gegevens in Azure Redis-Cache](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="3f850-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="3f850-297">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Import-AzureRmRedisCache`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3f850-298">Hallo importeert volgende opdracht gegevens van Hallo blob in Azure Redis-Cache door Hallo SAS-uri is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3f850-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="3f850-299">tooexport een Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-299">tooexport a Redis cache</span></span>
<span data-ttu-id="3f850-300">U kunt gegevens exporteren van een Azure Redis-Cache-exemplaar met behulp van Hallo `Export-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f850-301">Import/Export is alleen beschikbaar voor [premium-laag](cache-premium-tier-intro.md) in de cache opslaat.</span><span class="sxs-lookup"><span data-stu-id="3f850-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3f850-302">Zie voor meer informatie over het importeren/exporteren [importeren en exporteren van gegevens in Azure Redis-Cache](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="3f850-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="3f850-303">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Export-AzureRmRedisCache`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3f850-304">Hallo volgende opdracht exporteert u de gegevens van een Azure Redis-Cache-exemplaar naar Hallo-container door Hallo SAS-uri opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3f850-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="3f850-305">tooreboot een Redis-cache</span><span class="sxs-lookup"><span data-stu-id="3f850-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="3f850-306">U kunt uw Azure Redis-Cache-exemplaar met behulp van Hallo opstarten `Reset-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f850-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f850-307">Opnieuw opstarten is alleen beschikbaar voor [premium-laag](cache-premium-tier-intro.md) in de cache opslaat.</span><span class="sxs-lookup"><span data-stu-id="3f850-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3f850-308">Zie voor meer informatie over het opnieuw opstarten van uw cache [beheer in de Cache - opnieuw opstarten](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="3f850-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="3f850-309">een lijst met beschikbare parameters en de bijbehorende beschrijvingen voor toosee `Reset-AzureRmRedisCache`, voert hello na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f850-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3f850-310">Hallo volgende opdracht wordt opnieuw opgestart beide knooppunten van de opgegeven Hallo cache.</span><span class="sxs-lookup"><span data-stu-id="3f850-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="3f850-311">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f850-311">Next steps</span></span>
<span data-ttu-id="3f850-312">toolearn meer informatie over Windows PowerShell gebruiken met Azure, Zie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f850-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="3f850-313">Azure Redis-Cache-cmdlet-documentatie op MSDN</span><span class="sxs-lookup"><span data-stu-id="3f850-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="3f850-314">[Azure Resource Manager-Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): informatie over toouse Hallo-cmdlets in hello Azure Resource Manager-module.</span><span class="sxs-lookup"><span data-stu-id="3f850-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="3f850-315">[Toomanage uw Azure-resources met behulp van de Resource groepen](../azure-resource-manager/resource-group-template-deploy-portal.md): meer informatie over hoe toocreate en resourcegroepen in hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="3f850-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="3f850-316">[Azure-blog](http://blogs.msdn.com/windowsazure): meer informatie over nieuwe functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f850-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="3f850-317">[Windows PowerShell-blog](http://blogs.msdn.com/powershell): meer informatie over nieuwe functies in Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f850-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="3f850-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): echte tips en trucs ophalen uit Hallo Windows PowerShell-community.</span><span class="sxs-lookup"><span data-stu-id="3f850-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

