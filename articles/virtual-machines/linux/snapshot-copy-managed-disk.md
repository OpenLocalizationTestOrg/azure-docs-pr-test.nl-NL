---
title: een beheerde Azure Disk voor Back up aaaCopy | Microsoft Docs
description: Meer informatie over hoe toocreate een kopie van een Azure-schijf beheerd toouse voor reserve of probleemoplossing schijf uitgeeft.
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Maak een kopie van een VHD die is opgeslagen als een beheerde Azure-schijf met behulp van momentopnamen beheerd
Een momentopname van een beheerde-schijf voor back-up of een schijf beheerd vanuit Hallo momentopname maken en deze te koppelen tooa test virtuele machine tootroubleshoot. Een momentopname van een beheerd is een volledige point-in-time-kopie van een schijf VM beheerd. Deze maakt een alleen-lezen kopie van uw VHD en standaard opgeslagen als een standaard beheerde schijf. 

Zie voor meer informatie over prijzen [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Beide hello Azure portal of hello Azure CLI 2.0 tootake een momentopname van Hallo beheerd schijf gebruiken.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Azure CLI 2.0 tootake een momentopname gebruiken

> [!NOTE] 
> Hallo moet volgende voorbeeld hello Azure CLI 2.0 geïnstalleerd en geregistreerd in uw Azure-account.

Hallo volgende stappen laten zien hoe tooobtain en maak een momentopname van een beheerde OS schijf met Hallo `az snapshot create` opdracht Hello `--source-disk` parameter. Hallo volgende voorbeeld wordt ervan uitgegaan dat er een virtuele machine aangeroepen `myVM` gemaakt met een beheerde besturingssysteemschijf in Hallo `myResourceGroup` resourcegroep.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

Hallo-uitvoer ziet er ongeveer als:

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Azure portal tootake een momentopname gebruiken 

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Beginnen in de linkerbovenhoek hello, klikt u op **nieuw** en zoek naar **momentopname**.
3. Klik op Hallo momentopname blade **maken**.
4. Voer een **naam** voor Hallo momentopname.
5. Selecteer een bestaande [resourcegroep](../../azure-resource-manager/resource-group-overview.md#resource-groups) of Hallo typenaam voor een nieuwe resourcegroep. 
6. Selecteer een Azure-datacenter locatie.  
7. Voor **bronschijf**, selecteer Hallo toosnapshot schijf beheerd.
8. Selecteer Hallo **accounttype** toouse toostore Hallo momentopname. Het is raadzaam **Standard_LRS** tenzij u deze opgeslagen op een hoog presterende schijf nodig.
9. Klik op **Create**.

Als u toouse Hallo momentopname toocreate van plan een schijf beheerd bent en koppelt u dit een virtuele machine die toobe hoge prestaties behoeften, gebruikt u Hallo parameter `--sku Premium_LRS` Hello `az snapshot create` opdracht. Hiermee maakt u Hallo momentopname zodanig dat deze wordt opgeslagen als een schijf Premium beheerd. Premium-schijven beheerd sneller omdat ze SSD-schijven (SSD's zijn), maar duurder dan standaardschijven (HDD's).


