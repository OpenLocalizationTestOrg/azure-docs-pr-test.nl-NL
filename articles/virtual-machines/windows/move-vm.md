---
title: een virtuele machine van Windows-resource in Azure aaaMove | Microsoft Docs
description: Een tooanother van de virtuele machine van Windows Azure-abonnement of resourcegroep verplaatsen Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Een tooanother van de virtuele machine van Windows Azure-abonnement of resourcegroep verplaatsen
In dit artikel leert u hoe u een Windows-VM tussen resourcegroepen of abonnementen toomove. Verplaatsen tussen abonnementen kan handig zijn als u een virtuele machine hebt gemaakt in een persoonlijke abonnement en nu wilt toomove deze van het bedrijf tooyour abonnement toocontinue uw werk.

> [!IMPORTANT]
>U kunt beheerde schijven op dit moment niet verplaatsen. 
>
>Nieuwe resource-id's worden gemaakt als onderdeel van Hallo verplaatsen. Als hello VM is verplaatst, moet u tooupdate de hulpprogramma's en scripts toouse Hallo nieuwe resource-id. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>Gebruik Powershell toomove een virtuele machine
een resourcegroep van de virtuele machine tooanother toomove, moet u ervoor dat u ook Verplaats alle afhankelijke resources Hallo toomake. toouse hello verplaatsen AzureRMResource cmdlet, moet u Hallo resourcenaam en Hallo type resource. U kunt zowel vanuit Hallo zoeken AzureRMResource cmdlet ophalen.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


toomove een virtuele machine moet toomove meerdere resources. We kunnen alleen afzonderlijke variabelen voor elke resource maken en deze vervolgens te vermelden. In dit voorbeeld bevat de meest Hallo basic resources voor een virtuele machine, maar u kunt meer behoefte toevoegen.

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

toomove Hallo resources toodifferent abonnement, omvatten Hallo **- DestinationSubscriptionId** parameter. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



U wordt gevraagd dat u wilt dat toomove hello tooconfirm opgegeven resources. Type **Y** tooconfirm dat u wilt dat toomove Hallo resources.

## <a name="next-steps"></a>Volgende stappen
U kunt verschillende soorten resources verplaatsen tussen resourcegroepen en abonnementen. Zie voor meer informatie [verplaatsen van resources toonew resourcegroep of abonnement](../../resource-group-move-resources.md).    

