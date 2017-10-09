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
# <a name="use-powershell-toomanage-event-hubs-resources"></a>Gebruik PowerShell toomanage Event Hubs bronnen

Microsoft Azure PowerShell is een scriptomgeving toocontrol gebruiken en Hallo-implementatie en beheer van Azure services automatiseren. Dit artikel wordt beschreven hoe toouse hello [Event Hubs Resource Manager PowerShell-module](/powershell/module/azurerm.eventhub) tooprovision en Event Hubs-entiteiten (naamruimten, afzonderlijke event hubs en consumergroepen) beheren met behulp van een lokale Azure PowerShell-console of script.

U kunt ook Event Hubs-resources met behulp van Azure Resource Manager-sjablonen beheren. Zie voor meer informatie artikel Hallo [maken van een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub.md).

## <a name="prerequisites"></a>Vereisten

Voordat u begint, moet u de volgende Hallo:

* Een Azure-abonnement. Zie voor meer informatie over het verkrijgen van een abonnement [aanschafopties][purchase options], [lid biedt][member offers], of [gratis account][free account].
* Een computer met Azure PowerShell. Zie voor instructies [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps).
* Een algemeen begrip van de PowerShell-scripts, NuGet-pakketten en Hallo .NET Framework.

## <a name="get-started"></a>Aan de slag

de eerste stap Hallo is toouse PowerShell toolog in tooyour Azure-account en de Azure-abonnement. Volg de instructies in Hallo [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure-account, klikt u vervolgens toegang te krijgen tot Hallo bronnen in uw Azure-abonnement.

## <a name="provision-an-event-hubs-namespace"></a>Inrichten van een naamruimte Event Hubs

Als u werkt met Event Hubs-naamruimten, kunt u Hallo [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [nieuw AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [verwijderen AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , en [Set AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.

Dit voorbeeld wordt een paar lokale variabelen in Hallo script; `$Namespace` en `$Location`.

* `$Namespace`Hallo-naam van Hallo Event Hubs naamruimte waarmee we willen dat toowork is.
* `$Location`identificeert Hallo Datacenter waarin we Hallo naamruimte inricht.
* `$CurrentNamespace`slaat Hallo verwijzing naamruimte die we ophalen (of maak).

In een werkelijke script `$Namespace` en `$Location` kunnen worden doorgegeven als parameters.

Dit deel van het Hallo-script Hallo te volgen:

1. Pogingen tooretrieve een Event Hubs-naamruimte met Hallo opgegeven naam.
2. Als het Hallo-naamruimte wordt gevonden, meldt deze wat is gevonden.
3. Als het Hallo-naamruimte niet wordt gevonden, Hallo naamruimte maakt en vervolgens haalt Hallo zojuist-naamruimte gemaakt.

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

## <a name="create-an-event-hub"></a>Een Event Hub maken

toocreate een event hub, een naamruimte-controle met Hallo script in de vorige sectie Hallo uitvoeren. Gebruik vervolgens Hallo [nieuw AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate Hallo event hub:

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

### <a name="create-a-consumer-group"></a>Een consumergroep maken

toocreate een consumergroep binnen een event hub, Hallo-naamruimte en event hub controles uitvoeren met behulp van Hallo-scripts in de vorige sectie Hallo. Gebruik vervolgens Hallo [nieuw AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumergroep binnen Hallo event hub. Bijvoorbeeld:

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

#### <a name="set-user-metadata"></a>Metagegevens van de gebruiker instellen

Na het uitvoeren van scripts Hallo in de voorgaande secties hello, kunt u Hallo [Set AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate Hallo eigenschappen van een consumergroep, zoals in het volgende voorbeeld Hallo:

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>Verwijderen van de event hub

tooremove hello event hubs u hebt gemaakt, kunt u Hallo `Remove-*` cmdlets, zoals in het volgende voorbeeld Hallo:

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>Volgende stappen

- Zie Hallo volledige Event Hubs Resource Manager PowerShell-module documentatie [hier](/powershell/module/azurerm.eventhub). Deze pagina worden alle beschikbare cmdlets.
- Zie voor informatie over het gebruik van Azure Resource Manager-sjablonen Hallo artikel [maken van een naamruimte Event Hubs met event hub- en groep met een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub.md).
- Informatie over [Event Hubs .NET managementbibliotheken](event-hubs-management-libraries.md).

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
