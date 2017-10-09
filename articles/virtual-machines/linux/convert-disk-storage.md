---
title: aaaConvert Azure beheerd schijven opslag van standaard toopremium, en vice versa | Microsoft Docs
description: Hoe beheerd tooconvert Azure storage van de schijven van standaard toopremium en omgekeerd, met behulp van Azure CLI.
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Converteren van Azure storage schijven beheerd van standaard toopremium, en vice versa

Beheerde schijven biedt twee opties voor opslag: [Premium](../../storage/storage-premium-storage.md) (SSD-gebaseerde) en [standaard](../../storage/storage-standard-storage.md) (gebaseerd op harde schijf). Hiermee kunt u tooeasily schakelen tussen Hallo twee opties met minimale downtime op basis van uw prestatievereisten past. Deze mogelijkheid is niet beschikbaar voor niet-beheerde schijven. Maar u kunt eenvoudig [toomanaged schijven geconverteerd](convert-unmanaged-to-managed-disks.md) tooeasily schakelen tussen Hallo twee opties.

Dit artikel laat zien hoe tooconvert schijven die worden beheerd vanaf standaard toopremium, en vice versa met Azure CLI. Als u tooinstall moet of een upgrade uitvoeren, Zie [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli.md). 

## <a name="before-you-begin"></a>Voordat u begint

* Hallo conversie vereist Hallo VM opnieuw wordt opgestart, dus plannen Hallo-migratie van de opslag van uw schijven tijdens een vooraf bestaande onderhoudsvenster. 
* Als u niet-beheerde schijven eerst [toomanaged schijven geconverteerd](convert-unmanaged-to-managed-disks.md) toouse in dit artikel tooswitch tussen twee Hallo opslagopties. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Converteert alle Hallo beheerd schijven van een virtuele machine van de standaard toopremium, en vice versa

In de Hallo voorbeeld te volgen, laten we zien hoe tooswitch alle schijven van een virtuele machine uit de opslag van de standaard toopremium Hallo. premium toouse schijven die worden beheerd, uw virtuele machine moet gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag. In dit voorbeeld wordt ook tooa grootte die ondersteuning biedt voor premium-opslag.

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Een beheerde schijf converteren van standaard toopremium, en vice versa

Voor uw workload ontwikkelen en testen kunt u toohave combinatie van standard en premium-schijven tooreduce uw kosten. U kunt dit doen door het upgraden van toopremium opslag, alleen Hallo-schijven die betere prestaties zijn vereist. In de Hallo voorbeeld te volgen, laten we zien hoe tooswitch één schijf van een virtuele machine uit de standaard toopremium opslag, en vice versa. premium toouse schijven die worden beheerd, uw virtuele machine moet gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag. In dit voorbeeld wordt ook tooa grootte die ondersteuning biedt voor premium-opslag.

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a>Volgende stappen

Een alleen-lezen kopie van een virtuele machine uitvoeren met behulp van [momentopnamen](snapshot-copy-managed-disk.md).

