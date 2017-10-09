---
title: aaaUse PowerShell toomanage Azure Service Bus-resources | Microsoft Docs
description: Gebruik PowerShell-module toocreate en Service Bus-resources beheren
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="e16b3-103">Gebruik PowerShell toomanage Service Bus-resources</span><span class="sxs-lookup"><span data-stu-id="e16b3-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="e16b3-104">Microsoft Azure PowerShell is een scriptomgeving toocontrol gebruiken en Hallo-implementatie en beheer van Azure services automatiseren.</span><span class="sxs-lookup"><span data-stu-id="e16b3-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="e16b3-105">Dit artikel wordt beschreven hoe toouse hello [Service Bus-Resource Manager PowerShell-module](/powershell/module/azurerm.servicebus) tooprovision en Service Bus-entiteiten (naamruimten, wachtrijen, onderwerpen en abonnementen) beheren met behulp van een lokale Azure PowerShell-console of script.</span><span class="sxs-lookup"><span data-stu-id="e16b3-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="e16b3-106">U kunt ook beheren met behulp van Azure Resource Manager-sjablonen van Service Bus-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="e16b3-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="e16b3-107">Zie voor meer informatie artikel Hallo [maken van Service Bus-resources met behulp van Azure Resource Manager-sjablonen](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e16b3-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e16b3-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e16b3-108">Prerequisites</span></span>

<span data-ttu-id="e16b3-109">Voordat u begint, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e16b3-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="e16b3-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e16b3-110">An Azure subscription.</span></span> <span data-ttu-id="e16b3-111">Zie voor meer informatie over het verkrijgen van een abonnement [aanschafopties][purchase options], [lid biedt][member offers], of [gratis account][free account].</span><span class="sxs-lookup"><span data-stu-id="e16b3-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="e16b3-112">Een computer met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e16b3-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="e16b3-113">Zie voor instructies [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="e16b3-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="e16b3-114">Een algemeen begrip van de PowerShell-scripts, NuGet-pakketten en Hallo .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e16b3-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="e16b3-115">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="e16b3-115">Get started</span></span>

<span data-ttu-id="e16b3-116">de eerste stap Hallo is toouse PowerShell toolog in tooyour Azure-account en de Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e16b3-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="e16b3-117">Volg de instructies in Hallo [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure-account en ophalen en toegang Hallo resources in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e16b3-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="e16b3-118">Inrichten van een Service Bus-naamruimte</span><span class="sxs-lookup"><span data-stu-id="e16b3-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="e16b3-119">Als u werkt met Service Bus-naamruimten, kunt u Hallo [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [nieuw AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), en [Set AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e16b3-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="e16b3-120">Dit voorbeeld wordt een paar lokale variabelen in Hallo script; `$Namespace` en `$Location`.</span><span class="sxs-lookup"><span data-stu-id="e16b3-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="e16b3-121">`$Namespace`Hallo-naam van Service Bus-naamruimte Hallo waarmee we willen dat toowork is.</span><span class="sxs-lookup"><span data-stu-id="e16b3-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="e16b3-122">`$Location`identificeert Hallo Datacenter waarin we Hallo naamruimte inricht.</span><span class="sxs-lookup"><span data-stu-id="e16b3-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="e16b3-123">`$CurrentNamespace`slaat Hallo verwijzing naamruimte die we ophalen (of maak).</span><span class="sxs-lookup"><span data-stu-id="e16b3-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="e16b3-124">In een werkelijke script `$Namespace` en `$Location` kunnen worden doorgegeven als parameters.</span><span class="sxs-lookup"><span data-stu-id="e16b3-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="e16b3-125">Dit deel van het Hallo-script Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="e16b3-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="e16b3-126">Pogingen tooretrieve een Service Bus-naamruimte met Hallo opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="e16b3-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="e16b3-127">Als het Hallo-naamruimte wordt gevonden, meldt deze wat is gevonden.</span><span class="sxs-lookup"><span data-stu-id="e16b3-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="e16b3-128">Als het Hallo-naamruimte niet wordt gevonden, Hallo naamruimte maakt en vervolgens haalt Hallo zojuist-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e16b3-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="e16b3-129">Een autorisatieregel naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="e16b3-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="e16b3-130">Hallo volgende voorbeeld laat zien hoe toomanage autorisatieregels voor naamruimte met behulp van Hallo [nieuw AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), en [verwijderen AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="e16b3-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="e16b3-131">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="e16b3-131">Create a queue</span></span>

<span data-ttu-id="e16b3-132">toocreate een wachtrij of onderwerp, moet u de controle van een naamruimte met Hallo script in de vorige sectie Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e16b3-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="e16b3-133">Maak vervolgens een Hallo wachtrij:</span><span class="sxs-lookup"><span data-stu-id="e16b3-133">Then, create hello queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="e16b3-134">De wachtrijeigenschappen van de wijzigen</span><span class="sxs-lookup"><span data-stu-id="e16b3-134">Modify queue properties</span></span>

<span data-ttu-id="e16b3-135">Na het uitvoeren van script Hallo in de voorgaande sectie hello, kunt u Hallo [Set AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate Hallo eigenschappen van een wachtrij, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="e16b3-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="e16b3-136">Inrichting van andere Service Bus-entiteiten</span><span class="sxs-lookup"><span data-stu-id="e16b3-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="e16b3-137">U kunt Hallo [Service Bus PowerShell-module](/powershell/module/azurerm.servicebus) tooprovision andere entiteiten, zoals onderwerpen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="e16b3-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="e16b3-138">Deze cmdlets zijn syntaxis vergelijkbaar toohello wachtrij maken cmdlets in de vorige sectie Hallo uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="e16b3-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e16b3-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e16b3-139">Next steps</span></span>

- <span data-ttu-id="e16b3-140">Zie Hallo volledige Service Bus-Resource Manager PowerShell-module documentatie [hier](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="e16b3-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="e16b3-141">Deze pagina worden alle beschikbare cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e16b3-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="e16b3-142">Zie voor informatie over het gebruik van Azure Resource Manager-sjablonen Hallo artikel [maken van Service Bus-resources met behulp van Azure Resource Manager-sjablonen](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e16b3-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="e16b3-143">Informatie over [management-Service Bus .NET-bibliotheken](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="e16b3-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="e16b3-144">Er zijn enkele manieren alternatieve toomanage Service Bus-entiteiten, zoals beschreven in deze blogberichten:</span><span class="sxs-lookup"><span data-stu-id="e16b3-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="e16b3-145">Hoe toocreate Service Bus-wachtrijen, onderwerpen en abonnementen op basis van een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="e16b3-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="e16b3-146">Hoe toocreate een Service Bus Namespace en een Event Hub met een PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="e16b3-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="e16b3-147">Service Bus PowerShell-Scripts</span><span class="sxs-lookup"><span data-stu-id="e16b3-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
