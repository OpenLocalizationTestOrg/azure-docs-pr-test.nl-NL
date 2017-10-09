---
title: aaaManage Azure Search met behulp van Powershell-scripts | Microsoft Docs
description: Uw Azure Search-service met de PowerShell-scripts beheren. Maken of bijwerken van een Azure Search-service en Azure Search administratorsleutels beheren
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="d013a-104">Uw Azure Search-service met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="d013a-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d013a-105">Portal</span><span class="sxs-lookup"><span data-stu-id="d013a-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="d013a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d013a-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="d013a-107">Dit onderwerp beschrijft Hallo PowerShell-opdrachten tooperform veel Hallo beheertaken voor Azure Search-services.</span><span class="sxs-lookup"><span data-stu-id="d013a-107">This topic describes hello PowerShell commands tooperform many of hello management tasks for Azure Search services.</span></span> <span data-ttu-id="d013a-108">U kunt zien bij het maken van een service voor zoeken, schalen en het beheren van de API-sleutels.</span><span class="sxs-lookup"><span data-stu-id="d013a-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="d013a-109">Deze opdrachten parallel Hallo management beschikbare opties in Hallo [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="d013a-109">These commands parallel hello management options available in hello [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d013a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d013a-110">Prerequisites</span></span>
* <span data-ttu-id="d013a-111">U moet Azure PowerShell 1.0 of hoger hebben.</span><span class="sxs-lookup"><span data-stu-id="d013a-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="d013a-112">Zie voor instructies [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d013a-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d013a-113">U moet zijn aangemeld tooyour Azure-abonnement in PowerShell zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="d013a-113">You must be logged in tooyour Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="d013a-114">Eerst moet u aanmelding tooAzure met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="d013a-114">First, you must login tooAzure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="d013a-115">Geef Hallo e-mailadres van uw Azure-account en het bijbehorende wachtwoord in Hallo Microsoft Azure-aanmeldingsdialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d013a-115">Specify hello email address of your Azure account and its password in hello Microsoft Azure login dialog.</span></span>

<span data-ttu-id="d013a-116">U kunt ook [Meld u aan niet-interactief met een service-principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="d013a-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="d013a-117">Als u meerdere Azure-abonnementen hebt, moet u tooset uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d013a-117">If you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="d013a-118">een lijst met uw huidige abonnementen toosee deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d013a-118">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="d013a-119">toospecify hello abonnement, Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d013a-119">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="d013a-120">In de Hallo voorbeeld te volgen, is de naam van Hallo abonnement `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="d013a-120">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a><span data-ttu-id="d013a-121">Opdrachten toohelp die u aan de slag</span><span class="sxs-lookup"><span data-stu-id="d013a-121">Commands toohelp you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="d013a-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d013a-122">Next Steps</span></span>
<span data-ttu-id="d013a-123">Nu dat uw service hebt gemaakt, kunt u de volgende stappen Hallo ondernemen: bouwen een [index](search-what-is-an-index.md), [query uitvoeren in een index](search-query-overview.md), en ten slotte maken en beheren van uw eigen-zoektoepassing die gebruikmaakt van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d013a-123">Now that your service is created, you can take hello next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="d013a-124">Een Azure Search-index in hello Azure-portal maken</span><span class="sxs-lookup"><span data-stu-id="d013a-124">Create an Azure Search index in hello Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="d013a-125">Query uitvoeren op een Azure Search-index met behulp van de Search Explorer in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d013a-125">Query an Azure Search index using Search Explorer in hello Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="d013a-126">Een indexeerfunctie tooload gegevens van andere services instellen</span><span class="sxs-lookup"><span data-stu-id="d013a-126">Setup an indexer tooload data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="d013a-127">Hoe toouse Azure zoeken in .NET</span><span class="sxs-lookup"><span data-stu-id="d013a-127">How toouse Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="d013a-128">Analyseer het verkeer van uw Azure Search</span><span class="sxs-lookup"><span data-stu-id="d013a-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

