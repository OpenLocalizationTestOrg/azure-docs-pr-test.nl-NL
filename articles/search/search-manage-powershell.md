---
title: Azure Search met behulp van Powershell-scripts beheren | Microsoft Docs
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
ms.openlocfilehash: aa51c846efef12461ec382274199bc049c42aaa3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="1d717-104">Uw Azure Search-service met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="1d717-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d717-105">Portal</span><span class="sxs-lookup"><span data-stu-id="1d717-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="1d717-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d717-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="1d717-107">Dit onderwerp beschrijft de PowerShell-opdrachten uit te voeren veel van de beheertaken voor Azure Search-services.</span><span class="sxs-lookup"><span data-stu-id="1d717-107">This topic describes the PowerShell commands to perform many of the management tasks for Azure Search services.</span></span> <span data-ttu-id="1d717-108">U kunt zien bij het maken van een service voor zoeken, schalen en het beheren van de API-sleutels.</span><span class="sxs-lookup"><span data-stu-id="1d717-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="1d717-109">Deze opdrachten parallel de beheeropties beschikbaar in de [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d717-109">These commands parallel the management options available in the [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d717-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1d717-110">Prerequisites</span></span>
* <span data-ttu-id="1d717-111">U moet Azure PowerShell 1.0 of hoger hebben.</span><span class="sxs-lookup"><span data-stu-id="1d717-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="1d717-112">Zie voor instructies [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1d717-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="1d717-113">U moet zijn aangemeld met uw Azure-abonnement in PowerShell zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="1d717-113">You must be logged in to your Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="1d717-114">Eerst moet u aanmelden bij Azure met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="1d717-114">First, you must login to Azure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="1d717-115">Geef het e-mailadres van uw Azure-account en het bijbehorende wachtwoord in het dialoogvenster voor Microsoft Azure-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1d717-115">Specify the email address of your Azure account and its password in the Microsoft Azure login dialog.</span></span>

<span data-ttu-id="1d717-116">U kunt ook [Meld u aan niet-interactief met een service-principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="1d717-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="1d717-117">Als u meerdere Azure-abonnementen hebt, moet u uw Azure-abonnement instellen.</span><span class="sxs-lookup"><span data-stu-id="1d717-117">If you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="1d717-118">Een lijst van uw huidige abonnementen wilt bekijken, moet u deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1d717-118">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="1d717-119">Geef het abonnement door de volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1d717-119">To specify the subscription, run the following command.</span></span> <span data-ttu-id="1d717-120">In het volgende voorbeeld wordt de naam van het abonnement is `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="1d717-120">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-to-help-you-get-started"></a><span data-ttu-id="1d717-121">Opdrachten om u te helpen aan de slag</span><span class="sxs-lookup"><span data-stu-id="1d717-121">Commands to help you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register the ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once the service is fully created
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

    # Get the primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate the secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access to your indexes
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
    # This command will not return until the operation is finished
    # It can take 15 minutes or more to provision the additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in the service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="1d717-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1d717-122">Next Steps</span></span>
<span data-ttu-id="1d717-123">Nu dat uw service hebt gemaakt, kunt u de volgende stappen uitvoeren: bouwen een [index](search-what-is-an-index.md), [query uitvoeren in een index](search-query-overview.md), en ten slotte maken en beheren van uw eigen-zoektoepassing die gebruikmaakt van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="1d717-123">Now that your service is created, you can take the next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="1d717-124">Een Azure Search-index maken in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="1d717-124">Create an Azure Search index in the Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="1d717-125">Query uitvoeren op een Azure Search-index met behulp van de Search Explorer in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="1d717-125">Query an Azure Search index using Search Explorer in the Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="1d717-126">Stel een indexeerfunctie om gegevens te laden van andere services</span><span class="sxs-lookup"><span data-stu-id="1d717-126">Setup an indexer to load data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="1d717-127">Het gebruik van Azure Search in .NET</span><span class="sxs-lookup"><span data-stu-id="1d717-127">How to use Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="1d717-128">Analyseer het verkeer van uw Azure Search</span><span class="sxs-lookup"><span data-stu-id="1d717-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

