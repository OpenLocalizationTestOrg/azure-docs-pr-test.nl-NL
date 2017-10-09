---
title: aaaUse PowerShell toomanage Azure Event Hubs resources | Microsoft Docs
description: PowerShell-module toocreate gebruiken en beheren van Event Hubs
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="5b784-103">Gebruik PowerShell toomanage Event Hubs bronnen</span><span class="sxs-lookup"><span data-stu-id="5b784-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="5b784-104">Microsoft Azure PowerShell is een scriptomgeving toocontrol gebruiken en Hallo-implementatie en beheer van Azure services automatiseren.</span><span class="sxs-lookup"><span data-stu-id="5b784-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="5b784-105">Dit artikel wordt beschreven hoe toouse hello [Event Hubs Resource Manager PowerShell-module](/powershell/module/azurerm.eventhub) tooprovision en Event Hubs-entiteiten (naamruimten, afzonderlijke event hubs en consumergroepen) beheren met behulp van een lokale Azure PowerShell-console of script.</span><span class="sxs-lookup"><span data-stu-id="5b784-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="5b784-106">U kunt ook Event Hubs-resources met behulp van Azure Resource Manager-sjablonen beheren.</span><span class="sxs-lookup"><span data-stu-id="5b784-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="5b784-107">Zie voor meer informatie artikel Hallo [maken van een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5b784-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b784-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5b784-108">Prerequisites</span></span>

<span data-ttu-id="5b784-109">Voordat u begint, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5b784-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="5b784-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b784-110">An Azure subscription.</span></span> <span data-ttu-id="5b784-111">Zie voor meer informatie over het verkrijgen van een abonnement [aanschafopties][purchase options], [lid biedt][member offers], of [gratis account][free account].</span><span class="sxs-lookup"><span data-stu-id="5b784-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="5b784-112">Een computer met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b784-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="5b784-113">Zie voor instructies [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="5b784-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="5b784-114">Een algemeen begrip van de PowerShell-scripts, NuGet-pakketten en Hallo .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5b784-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="5b784-115">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="5b784-115">Get started</span></span>

<span data-ttu-id="5b784-116">de eerste stap Hallo is toouse PowerShell toolog in tooyour Azure-account en de Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b784-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="5b784-117">Volg de instructies in Hallo [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure-account, klikt u vervolgens toegang te krijgen tot Hallo bronnen in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b784-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="5b784-118">Inrichten van een naamruimte Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5b784-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="5b784-119">Als u werkt met Event Hubs-naamruimten, kunt u Hallo [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [nieuw AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [verwijderen AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , en [Set AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5b784-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="5b784-120">Dit voorbeeld wordt een paar lokale variabelen in Hallo script; `$Namespace` en `$Location`.</span><span class="sxs-lookup"><span data-stu-id="5b784-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="5b784-121">`$Namespace`Hallo-naam van Hallo Event Hubs naamruimte waarmee we willen dat toowork is.</span><span class="sxs-lookup"><span data-stu-id="5b784-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="5b784-122">`$Location`identificeert Hallo Datacenter waarin we Hallo naamruimte inricht.</span><span class="sxs-lookup"><span data-stu-id="5b784-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="5b784-123">`$CurrentNamespace`slaat Hallo verwijzing naamruimte die we ophalen (of maak).</span><span class="sxs-lookup"><span data-stu-id="5b784-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="5b784-124">In een werkelijke script `$Namespace` en `$Location` kunnen worden doorgegeven als parameters.</span><span class="sxs-lookup"><span data-stu-id="5b784-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="5b784-125">Dit deel van het Hallo-script Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5b784-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="5b784-126">Pogingen tooretrieve een Event Hubs-naamruimte met Hallo opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="5b784-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="5b784-127">Als het Hallo-naamruimte wordt gevonden, meldt deze wat is gevonden.</span><span class="sxs-lookup"><span data-stu-id="5b784-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="5b784-128">Als het Hallo-naamruimte niet wordt gevonden, Hallo naamruimte maakt en vervolgens haalt Hallo zojuist-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b784-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="5b784-129">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="5b784-129">Create an event hub</span></span>

<span data-ttu-id="5b784-130">toocreate een event hub, een naamruimte-controle met Hallo script in de vorige sectie Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5b784-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="5b784-131">Gebruik vervolgens Hallo [nieuw AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate Hallo event hub:</span><span class="sxs-lookup"><span data-stu-id="5b784-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="5b784-132">Een consumergroep maken</span><span class="sxs-lookup"><span data-stu-id="5b784-132">Create a consumer group</span></span>

<span data-ttu-id="5b784-133">toocreate een consumergroep binnen een event hub, Hallo-naamruimte en event hub controles uitvoeren met behulp van Hallo-scripts in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="5b784-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="5b784-134">Gebruik vervolgens Hallo [nieuw AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumergroep binnen Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="5b784-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="5b784-135">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5b784-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="5b784-136">Metagegevens van de gebruiker instellen</span><span class="sxs-lookup"><span data-stu-id="5b784-136">Set user metadata</span></span>

<span data-ttu-id="5b784-137">Na het uitvoeren van scripts Hallo in de voorgaande secties hello, kunt u Hallo [Set AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate Hallo eigenschappen van een consumergroep, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="5b784-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="5b784-138">Verwijderen van de event hub</span><span class="sxs-lookup"><span data-stu-id="5b784-138">Remove event hub</span></span>

<span data-ttu-id="5b784-139">tooremove hello event hubs u hebt gemaakt, kunt u Hallo `Remove-*` cmdlets, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="5b784-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="5b784-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b784-140">Next steps</span></span>

- <span data-ttu-id="5b784-141">Zie Hallo volledige Event Hubs Resource Manager PowerShell-module documentatie [hier](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="5b784-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="5b784-142">Deze pagina worden alle beschikbare cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5b784-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="5b784-143">Zie voor informatie over het gebruik van Azure Resource Manager-sjablonen Hallo artikel [maken van een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5b784-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="5b784-144">Informatie over [Event Hubs .NET managementbibliotheken](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="5b784-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
