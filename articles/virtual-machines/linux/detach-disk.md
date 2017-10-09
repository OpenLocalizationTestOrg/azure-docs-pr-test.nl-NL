---
title: een gegevensschijf van een Linux-VM - Azure aaaDetach | Microsoft Docs
description: Meer informatie over toodetach een gegevensschijf van een virtuele machine in Azure met behulp van de CLI 2.0 of hello Azure-portal.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Hoe toodetach een schijf van een virtuele Linux-machine

Wanneer u een gegevensschijf die is aangesloten tooa virtuele machine niet meer nodig hebt, kunt u deze eenvoudig loskoppelen. Deze taak verwijdert Hallo schijf uit de Hallo virtuele machine, maar niet verwijderd uit de opslag. 

> [!WARNING]
> Als u een schijf die wordt niet automatisch verwijderd loskoppelen. Als u tooPremium opslag hebt geabonneerd, blijft u tooincur opslagkosten voor Hallo schijf. Voor meer informatie raadpleegt u te[prijzen en facturering wanneer u Premium-opslag](../../storage/common/storage-premium-storage.md#pricing-and-billing). 
> 
> 

Als u toouse Hallo bestaande gegevens op Hallo schijf opnieuw wilt, u kunt opnieuw het toohello dezelfde virtuele machine of een andere naam.  

## <a name="detach-a-data-disk-using-cli-20"></a>Een gegevensschijf met CLI 2.0 loskoppelen

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

Hallo schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.


## <a name="detach-a-data-disk-using-hello-portal"></a>Een gegevensschijf met Hallo portal loskoppelen
1. Selecteer in de portal hub hello, **virtuele Machines**.
2. Selecteer Hallo virtuele machine met Hallo gegevensschijf toodetach en klik op **stoppen** toodeallocate Hallo VM.
3. Selecteer in de blade van de virtuele machine hello, **schijven**.
4. Hallo boven aan het Hallo **schijven** blade Selecteer **bewerken**.
5. In Hallo **schijven** blade toohello uiterst rechts in Hallo gegevensschijf dat u toodetach wilt, klikt u op Hallo ![Detach knopafbeelding](./media/detach-disk/detach.png) knop loskoppelen.
5. Nadat het Hallo-schijf is verwijderd, klikt u op opslaan op Hallo Hallo blade bovenaan.
6. In de blade van de virtuele machine hello, klikt u op **overzicht** en klik vervolgens op Hallo **Start** knop bovenaan Hallo Hallo blade toorestart Hallo VM.

Hallo schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.








## <a name="next-steps"></a>Volgende stappen
Als u tooreuse Hallo gegevensschijf wilt, kunt u zojuist hebt [koppelt u dit tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

