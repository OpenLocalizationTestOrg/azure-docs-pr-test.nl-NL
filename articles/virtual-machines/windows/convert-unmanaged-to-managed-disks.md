---
title: aaaConvert virtuele Windows-machine uit niet-beheerde schijven toomanaged schijven - beheerde Azure-schijven | Microsoft Docs
description: Hoe een Windows-VM uit niet-beheerde schijven toomanaged tooconvert schijven met behulp van PowerShell in Hallo Resource Manager-implementatiemodel
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Een virtuele Windows-machine converteren van niet-beheerde schijven toomanaged schijven

Als u een bestaande Windows virtuele machines (VM's) die gebruikmaken van niet-beheerde schijven hebt, Hallo VMs toouse beheerd schijven via hello, kunnen worden geconverteerd [Azure beheerd schijven](managed-disks-overview.md) service. Dit proces converteert Hallo OS-schijven en schijven bijgesloten gegevens.

Dit artikel ziet u hoe tooconvert virtuele machines met behulp van Azure PowerShell. Als u tooinstall moet of een upgrade uitvoeren, Zie [installeren en configureren van Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Voordat u begint


* Bekijk [Hallo-migratie plannen tooManaged schijven](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Single instance VMs converteren
Deze sectie bevat informatie over hoe tooconvert single instance Azure virtuele machines van niet-beheerde schijven toomanaged schijven. (Als uw virtuele machines zich in een beschikbaarheidsset, Zie de volgende sectie Hallo.) 

1. Hallo VM ongedaan met behulp van Hallo [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet. Hallo volgende voorbeeld deallocates Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Hallo VM toomanaged schijven worden geconverteerd met behulp van Hallo [ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet. Hallo proces converteert na Hallo vorige VM, met inbegrip van Hallo OS-schijf en eventuele gegevensschijven:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Hallo VM starten na Hallo conversie toomanaged schijven met behulp van [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm). Hallo voorbeeld opnieuw wordt opgestart na Hallo vorige VM:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Converteren van virtuele machines in een beschikbaarheidsset

Als Hallo VM's die u wilt dat tooconvert toomanaged schijven zich bevinden in een beschikbaarheidsset, u eerst tooconvert Hallo beschikbaarheid set tooa beheerd moet beschikbaarheidsset.

1. Hallo beschikbaarheid instellen met behulp van Hallo converteren [Update AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet. Hallo volgt updates Hallo beschikbaarheidsset benoemde `myAvailabilitySet` in Hallo resourcegroep met de naam `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Als Hallo regio waar uw beschikbaarheidsset zich bevindt slechts 2 beheerde foutdomeinen maar Hallo aantal niet-beheerde foutdomeinen 3, wordt deze opdracht wordt een fout ongeveer dezelfde te 'hello opgegeven aantal foutdomeinen 3 moet vallen in Hallo bereik van 1 too2." tooresolve Hallo fout, update Hallo veroorzaakt domein too2 en update `Sku` te`Aligned` als volgt:

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Toewijzing ongedaan maken en Hallo virtuele machines in de beschikbaarheidsset Hallo converteren. Hallo volgende script deallocates elke virtuele machine met behulp van Hallo [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converteert u deze met behulp van [ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), en start deze opnieuw met behulp van [Start-AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>Problemen oplossen

Als er een fout optreedt tijdens de conversie, of als een virtuele machine bevindt zich in een foutstatus vanwege problemen in een vorige conversie, Voer Hallo `ConvertTo-AzureRmVMManagedDisk` cmdlet opnieuw. Een eenvoudige opnieuw blokkering meestal opgeheven Hallo situatie.


## <a name="next-steps"></a>Volgende stappen

[Beheerde standaardschijven toopremium converteren](convert-disk-storage.md)

Een alleen-lezen kopie van een virtuele machine uitvoeren met behulp van [momentopnamen](snapshot-copy-managed-disk.md).

