---
title: aaaMove een Linux VM in Azure | Microsoft Docs
description: Verplaatsen van een Linux-VM tooanother Azure-abonnement of resourcegroep in Hallo Resource Manager-implementatiemodel.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Een groep Linux VM tooanother abonnement of resourcegroep verplaatsen
In dit artikel leert u hoe u een Linux-VM tussen resourcegroepen of abonnementen toomove. Een virtuele machine verplaatsen tussen abonnementen kan handig zijn als u een virtuele machine in een persoonlijke abonnement hebt gemaakt en nu wilt toomove het tooyour bedrijfsabonnement.

> [!IMPORTANT]
>U kunt beheerde schijven op dit moment niet verplaatsen. 
>
>Nieuwe resource-id's worden gemaakt als onderdeel van Hallo verplaatsen. Als hello VM is verplaatst, moet u tooupdate de hulpprogramma's en scripts toouse Hallo nieuwe resource-id. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Hello Azure CLI toomove een virtuele machine gebruiken
toosuccessfully een virtuele machine verplaatsen, moet u toomove Hallo VM en de bijbehorende ondersteunende bronnen. Gebruik Hallo **azure-groep weergeven** opdracht toolist alle Hallo resources in een resourcegroep en de id's. Het helpt toopipe Hallo uitvoer van deze opdracht tooa-bestand zodat u kunt kopiëren en Hallo id's in latere opdrachten plakken.

    azure group show <resourceGroupName>

toomove een virtuele machine en de resourcegroep resources tooanother gebruiken Hallo **azure-resource verplaatsen** CLI-opdracht. Hallo volgende voorbeeld ziet u hoe toomove een virtuele machine en de meest voorkomende bronnen Hallo vereist. We gebruiken Hallo **-i** parameter en geeft u een door komma's gescheiden lijst (zonder spaties) met id's voor Hallo resources toomove.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Als u wilt dat toomove Hallo virtuele machine en bijbehorende resources tooa ander abonnement, het toevoegen van Hallo **--bestemming subscriptionId &#60; destinationSubscriptionID &#62;** parameter toospecify Hallo doelabonnement.

Als u op Hallo opdrachtprompt op een Windows-computer werkt, moet u tooadd een  **$**  voor variabelenamen Hallo wanneer u ze declareren. Dit is niet nodig in Linux.

U wordt gevraagd dat u wilt dat toomove hello tooconfirm van de opgegeven bron. Type **Y** tooconfirm dat u wilt dat toomove Hallo resources.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>Volgende stappen
U kunt verschillende soorten resources verplaatsen tussen resourcegroepen en abonnementen. Zie voor meer informatie [verplaatsen van resources toonew resourcegroep of abonnement](../../resource-group-move-resources.md).    

