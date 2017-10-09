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
# <a name="use-powershell-toomanage-service-bus-resources"></a>Gebruik PowerShell toomanage Service Bus-resources

Microsoft Azure PowerShell is een scriptomgeving toocontrol gebruiken en Hallo-implementatie en beheer van Azure services automatiseren. Dit artikel wordt beschreven hoe toouse hello [Service Bus-Resource Manager PowerShell-module](/powershell/module/azurerm.servicebus) tooprovision en Service Bus-entiteiten (naamruimten, wachtrijen, onderwerpen en abonnementen) beheren met behulp van een lokale Azure PowerShell-console of script.

U kunt ook beheren met behulp van Azure Resource Manager-sjablonen van Service Bus-entiteiten. Zie voor meer informatie artikel Hallo [maken van Service Bus-resources met behulp van Azure Resource Manager-sjablonen](service-bus-resource-manager-overview.md).

## <a name="prerequisites"></a>Vereisten

Voordat u begint, moet u de volgende Hallo:

* Een Azure-abonnement. Zie voor meer informatie over het verkrijgen van een abonnement [aanschafopties][purchase options], [lid biedt][member offers], of [gratis account][free account].
* Een computer met Azure PowerShell. Zie voor instructies [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps).
* Een algemeen begrip van de PowerShell-scripts, NuGet-pakketten en Hallo .NET Framework.

## <a name="get-started"></a>Aan de slag

de eerste stap Hallo is toouse PowerShell toolog in tooyour Azure-account en de Azure-abonnement. Volg de instructies in Hallo [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure-account en ophalen en toegang Hallo resources in uw Azure-abonnement.

## <a name="provision-a-service-bus-namespace"></a>Inrichten van een Service Bus-naamruimte

Als u werkt met Service Bus-naamruimten, kunt u Hallo [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [nieuw AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), en [Set AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.

Dit voorbeeld wordt een paar lokale variabelen in Hallo script; `$Namespace` en `$Location`.

* `$Namespace`Hallo-naam van Service Bus-naamruimte Hallo waarmee we willen dat toowork is.
* `$Location`identificeert Hallo Datacenter waarin we Hallo naamruimte inricht.
* `$CurrentNamespace`slaat Hallo verwijzing naamruimte die we ophalen (of maak).

In een werkelijke script `$Namespace` en `$Location` kunnen worden doorgegeven als parameters.

Dit deel van het Hallo-script Hallo te volgen:

1. Pogingen tooretrieve een Service Bus-naamruimte met Hallo opgegeven naam.
2. Als het Hallo-naamruimte wordt gevonden, meldt deze wat is gevonden.
3. Als het Hallo-naamruimte niet wordt gevonden, Hallo naamruimte maakt en vervolgens haalt Hallo zojuist-naamruimte gemaakt.
   
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

### <a name="create-a-namespace-authorization-rule"></a>Een autorisatieregel naamruimte maken

Hallo volgende voorbeeld laat zien hoe toomanage autorisatieregels voor naamruimte met behulp van Hallo [nieuw AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), en [verwijderen AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).

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

## <a name="create-a-queue"></a>Een wachtrij maken

toocreate een wachtrij of onderwerp, moet u de controle van een naamruimte met Hallo script in de vorige sectie Hallo uitvoeren. Maak vervolgens een Hallo wachtrij:

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

### <a name="modify-queue-properties"></a>De wachtrijeigenschappen van de wijzigen

Na het uitvoeren van script Hallo in de voorgaande sectie hello, kunt u Hallo [Set AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate Hallo eigenschappen van een wachtrij, zoals in het volgende voorbeeld Hallo:

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>Inrichting van andere Service Bus-entiteiten

U kunt Hallo [Service Bus PowerShell-module](/powershell/module/azurerm.servicebus) tooprovision andere entiteiten, zoals onderwerpen en abonnementen. Deze cmdlets zijn syntaxis vergelijkbaar toohello wachtrij maken cmdlets in de vorige sectie Hallo uitgelegd.

## <a name="next-steps"></a>Volgende stappen

- Zie Hallo volledige Service Bus-Resource Manager PowerShell-module documentatie [hier](/powershell/module/azurerm.servicebus). Deze pagina worden alle beschikbare cmdlets.
- Zie voor informatie over het gebruik van Azure Resource Manager-sjablonen Hallo artikel [maken van Service Bus-resources met behulp van Azure Resource Manager-sjablonen](service-bus-resource-manager-overview.md).
- Informatie over [management-Service Bus .NET-bibliotheken](service-bus-management-libraries.md).

Er zijn enkele manieren alternatieve toomanage Service Bus-entiteiten, zoals beschreven in deze blogberichten:

* [Hoe toocreate Service Bus-wachtrijen, onderwerpen en abonnementen op basis van een PowerShell-script](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Hoe toocreate een Service Bus Namespace en een Event Hub met een PowerShell-script](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Service Bus PowerShell-Scripts](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
