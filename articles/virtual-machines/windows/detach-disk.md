---
title: een gegevensschijf van een VM van Windows - Azure aaaDetach | Microsoft Docs
description: Meer informatie over toodetach een gegevensschijf van een virtuele machine in Azure met behulp van Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a>Hoe toodetach een schijf van een virtuele machine van Windows
Wanneer u een gegevensschijf die is aangesloten tooa virtuele machine niet meer nodig hebt, kunt u deze eenvoudig loskoppelen. Deze taak verwijdert Hallo schijf uit de Hallo virtuele machine, maar niet verwijderd uit de opslag.

> [!WARNING]
> Als u een schijf die wordt niet automatisch verwijderd loskoppelen. Als u tooPremium opslag hebt geabonneerd, blijft u tooincur opslagkosten voor Hallo schijf. Voor meer informatie raadpleegt u te[prijzen en facturering wanneer u Premium-opslag](../../storage/common/storage-premium-storage.md#pricing-and-billing).
>
>

Als u toouse Hallo bestaande gegevens op Hallo schijf opnieuw wilt, u kunt opnieuw het toohello dezelfde virtuele machine of een andere naam.

## <a name="detach-a-data-disk-using-hello-portal"></a>Een gegevensschijf met Hallo portal loskoppelen
1. Selecteer in de portal hub hello, **virtuele Machines**.
2. Selecteer Hallo virtuele machine met Hallo gegevensschijf toodetach en klik op **stoppen** toodeallocate Hallo VM.
3. Selecteer in de blade van de virtuele machine hello, **schijven**.
4. Hallo boven aan het Hallo **schijven** blade Selecteer **bewerken**.
5. In Hallo **schijven** blade toohello uiterst rechts in Hallo gegevensschijf dat u toodetach wilt, klikt u op Hallo ![Detach knopafbeelding](./media/detach-disk/detach.png) knop loskoppelen.
5. Nadat het Hallo-schijf is verwijderd, klikt u op opslaan op Hallo Hallo blade bovenaan.
6. In de blade van de virtuele machine hello, klikt u op **overzicht** en klik vervolgens op Hallo **Start** knop bovenaan Hallo Hallo blade toorestart Hallo VM.



Hallo schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.

## <a name="detach-a-data-disk-using-powershell"></a>Een gegevensschijf met behulp van PowerShell loskoppelen
In dit voorbeeld Hallo eerste opdracht opgehaald Hallo virtuele machine met de naam **MyVM07** in Hallo **RG11** resourcegroep met de cmdlet Get-AzureRmVM Hallo. opdracht slaat virtuele machine in Hallo HALLO hallo **$VirtualMachine** variabele.

de tweede opdracht Hallo verwijdert Hallo gegevensschijf DataDisk3 met de naam van de Hallo virtuele machine.

de laatste opdracht Hallo Hallo status van Hallo toocomplete Hallo proces voor virtuele machines van het verwijderen van de gegevensschijf Hallo-updates.

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

Zie voor meer informatie [verwijderen AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).

## <a name="next-steps"></a>Volgende stappen
Als u tooreuse Hallo gegevensschijf wilt, kunt u zojuist hebt [tooanother VM koppelen](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

