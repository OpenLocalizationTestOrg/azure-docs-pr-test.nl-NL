---
title: PowerShell gebruiken om Azure Event Hubs-resources te beheren | Microsoft Docs
description: Gebruik PowerShell-module maken en beheren van Event Hubs
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
ms.openlocfilehash: 2b49c01153b1104612e6ebf9c88566fc40d1f635
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-manage-event-hubs-resources"></a><span data-ttu-id="e37c7-103">PowerShell gebruiken om Event Hubs-resources te beheren</span><span class="sxs-lookup"><span data-stu-id="e37c7-103">Use PowerShell to manage Event Hubs resources</span></span>

<span data-ttu-id="e37c7-104">Microsoft Azure PowerShell is een scriptomgeving op servers die u gebruiken kunt om te beheren en de implementatie en beheer van Azure services automatiseren.</span><span class="sxs-lookup"><span data-stu-id="e37c7-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="e37c7-105">In dit artikel wordt beschreven hoe u de [Event Hubs Resource Manager PowerShell-module](/powershell/module/azurerm.eventhub) inrichten en beheren van Event Hubs-entiteiten (naamruimten, afzonderlijke event hubs en consumergroepen) met behulp van een lokale Azure PowerShell-console of script.</span><span class="sxs-lookup"><span data-stu-id="e37c7-105">This article describes how to use the [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) to provision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="e37c7-106">U kunt ook Event Hubs-resources met behulp van Azure Resource Manager-sjablonen beheren.</span><span class="sxs-lookup"><span data-stu-id="e37c7-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="e37c7-107">Zie voor meer informatie het artikel [maken van een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e37c7-107">For more information, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e37c7-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e37c7-108">Prerequisites</span></span>

<span data-ttu-id="e37c7-109">Voordat u begint, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="e37c7-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="e37c7-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e37c7-110">An Azure subscription.</span></span> <span data-ttu-id="e37c7-111">Zie voor meer informatie over het verkrijgen van een abonnement [aanschafopties][purchase options], [lid biedt][member offers], of [gratis account][free account].</span><span class="sxs-lookup"><span data-stu-id="e37c7-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="e37c7-112">Een computer met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e37c7-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="e37c7-113">Zie voor instructies [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="e37c7-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="e37c7-114">Een algemeen begrip van de PowerShell-scripts, NuGet-pakketten en .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e37c7-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="e37c7-115">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="e37c7-115">Get started</span></span>

<span data-ttu-id="e37c7-116">De eerste stap is het gebruik van PowerShell zich aanmelden bij uw Azure-account en de Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e37c7-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="e37c7-117">Volg de instructies in [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps) voor het aanmelden bij uw Azure-account, klikt u vervolgens toegang te krijgen tot de resources in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e37c7-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, then retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="e37c7-118">Inrichten van een naamruimte Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e37c7-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="e37c7-119">Als u werkt met Event Hubs-naamruimten, kunt u de [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [nieuw AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [verwijderen AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), en [Set AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e37c7-119">When working with Event Hubs namespaces, you can use the [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="e37c7-120">In dit voorbeeld maakt een paar lokale variabelen in het script; `$Namespace` en `$Location`.</span><span class="sxs-lookup"><span data-stu-id="e37c7-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="e37c7-121">`$Namespace`is de naam van de Event Hubs-naamruimte die we wilt werken.</span><span class="sxs-lookup"><span data-stu-id="e37c7-121">`$Namespace` is the name of the Event Hubs namespace with which we want to work.</span></span>
* <span data-ttu-id="e37c7-122">`$Location`identificeert het datacenter waarin we de naamruimte inricht.</span><span class="sxs-lookup"><span data-stu-id="e37c7-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="e37c7-123">`$CurrentNamespace`slaat de referentie-naamruimte die we ophalen (of maak).</span><span class="sxs-lookup"><span data-stu-id="e37c7-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="e37c7-124">In een werkelijke script `$Namespace` en `$Location` kunnen worden doorgegeven als parameters.</span><span class="sxs-lookup"><span data-stu-id="e37c7-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="e37c7-125">Dit deel van het script doet het volgende:</span><span class="sxs-lookup"><span data-stu-id="e37c7-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="e37c7-126">Probeert op te halen van een naamruimte Event Hubs met de opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="e37c7-126">Attempts to retrieve an Event Hubs namespace with the specified name.</span></span>
2. <span data-ttu-id="e37c7-127">Als de naamruimte wordt gevonden, rapporteert wat is gevonden.</span><span class="sxs-lookup"><span data-stu-id="e37c7-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="e37c7-128">Als de naamruimte niet wordt gevonden, maakt u de naamruimte en vervolgens haalt de zojuist gemaakte naamruimte.</span><span class="sxs-lookup"><span data-stu-id="e37c7-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>

    ```powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="e37c7-129">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="e37c7-129">Create an event hub</span></span>

<span data-ttu-id="e37c7-130">Voer een naamruimte-controle met het script in de vorige sectie voor het maken van een event hub.</span><span class="sxs-lookup"><span data-stu-id="e37c7-130">To create an event hub, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="e37c7-131">Gebruik vervolgens de [nieuw AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet voor het maken van de event hub:</span><span class="sxs-lookup"><span data-stu-id="e37c7-131">Then, use the [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet to create the event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "The event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $EventHubName event hub does not exist."
    Write-Host "Creating the $EventHubName event hub in the $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $EventHubName event hub in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="e37c7-132">Een consumergroep maken</span><span class="sxs-lookup"><span data-stu-id="e37c7-132">Create a consumer group</span></span>

<span data-ttu-id="e37c7-133">Een consumergroep binnen een event hub maken, voert u de naamruimte en event hub wordt gecontroleerd met behulp van de scripts in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="e37c7-133">To create a consumer group within an event hub, perform the namespace and event hub checks using the scripts in the previous section.</span></span> <span data-ttu-id="e37c7-134">Gebruik vervolgens de [nieuw AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet om de consumergroep binnen event hub te maken.</span><span class="sxs-lookup"><span data-stu-id="e37c7-134">Then, use the [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet to create the consumer group within the event hub.</span></span> <span data-ttu-id="e37c7-135">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e37c7-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "The consumer group $ConsumerGroupName in event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating the $ConsumerGroupName consumer group in the $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="e37c7-136">Metagegevens van de gebruiker instellen</span><span class="sxs-lookup"><span data-stu-id="e37c7-136">Set user metadata</span></span>

<span data-ttu-id="e37c7-137">Na het uitvoeren van de scripts in de vorige secties, kunt u de [Set AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet bij te werken van de eigenschappen van een consumergroep, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e37c7-137">After executing the scripts in the preceding sections, you can use the [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet to update the properties of a consumer group, as in the following example:</span></span>

```powershell
# Set some user metadata on the CG
Write-Host "Setting the UserMetadata field to 'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="e37c7-138">Verwijderen van de event hub</span><span class="sxs-lookup"><span data-stu-id="e37c7-138">Remove event hub</span></span>

<span data-ttu-id="e37c7-139">Als u wilt verwijderen van de event-hubs die u hebt gemaakt, kunt u de `Remove-*` cmdlets, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e37c7-139">To remove the event hubs you created, you can use the `Remove-*` cmdlets, as in the following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="e37c7-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e37c7-140">Next steps</span></span>

- <span data-ttu-id="e37c7-141">Raadpleeg de documentatie voor volledige Event Hubs Resource Manager PowerShell-module bij [hier](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="e37c7-141">See the complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="e37c7-142">Deze pagina worden alle beschikbare cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e37c7-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="e37c7-143">Zie het artikel voor informatie over het gebruik van Azure Resource Manager-sjablonen [maken van een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e37c7-143">For information about using Azure Resource Manager templates, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="e37c7-144">Informatie over [Event Hubs .NET managementbibliotheken](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="e37c7-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
