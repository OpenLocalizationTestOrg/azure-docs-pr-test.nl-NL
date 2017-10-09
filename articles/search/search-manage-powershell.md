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
# <a name="manage-your-azure-search-service-with-powershell"></a>Uw Azure Search-service met PowerShell beheren
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

Dit onderwerp beschrijft Hallo PowerShell-opdrachten tooperform veel Hallo beheertaken voor Azure Search-services. U kunt zien bij het maken van een service voor zoeken, schalen en het beheren van de API-sleutels.
Deze opdrachten parallel Hallo management beschikbare opties in Hallo [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Vereisten
* U moet Azure PowerShell 1.0 of hoger hebben. Zie voor instructies [installeren en configureren van Azure PowerShell](/powershell/azure/overview).
* U moet zijn aangemeld tooyour Azure-abonnement in PowerShell zoals hieronder wordt beschreven.

Eerst moet u aanmelding tooAzure met deze opdracht:

    Login-AzureRmAccount

Geef Hallo e-mailadres van uw Azure-account en het bijbehorende wachtwoord in Hallo Microsoft Azure-aanmeldingsdialoogvenster.

U kunt ook [Meld u aan niet-interactief met een service-principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Als u meerdere Azure-abonnementen hebt, moet u tooset uw Azure-abonnement. een lijst met uw huidige abonnementen toosee deze opdracht uitvoeren.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello abonnement, Hallo volgende opdracht uitvoeren. In de Hallo voorbeeld te volgen, is de naam van Hallo abonnement `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Opdrachten toohelp die u aan de slag
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

## <a name="next-steps"></a>Volgende stappen
Nu dat uw service hebt gemaakt, kunt u de volgende stappen Hallo ondernemen: bouwen een [index](search-what-is-an-index.md), [query uitvoeren in een index](search-query-overview.md), en ten slotte maken en beheren van uw eigen-zoektoepassing die gebruikmaakt van Azure Search.

* [Een Azure Search-index in hello Azure-portal maken](search-create-index-portal.md)
* [Query uitvoeren op een Azure Search-index met behulp van de Search Explorer in hello Azure-portal](search-explorer.md)
* [Een indexeerfunctie tooload gegevens van andere services instellen](search-indexer-overview.md)
* [Hoe toouse Azure zoeken in .NET](search-howto-dotnet-sdk.md)
* [Analyseer het verkeer van uw Azure Search](search-traffic-analytics.md)

