---
title: aaaUse PowerShell tooresize een Windows-VM in Azure | Microsoft Docs
description: Het formaat van een virtuele Windows-machine gemaakt in Hallo Resource Manager-implementatiemodel, met Azure Powershell.
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a>Een Windows VM vergroten of verkleinen
Dit artikel laat zien hoe tooresize een Windows-VM gemaakt in Hallo Resource Manager-implementatiemodel met Azure Powershell.

Nadat u een virtuele machine (VM) gemaakt, kunt u Hallo VM schalen omhoog of omlaag door Hallo VM-grootte wijzigen. In sommige gevallen moet u eerst Hallo VM ongedaan. Dit kan gebeuren als de nieuwe grootte Hallo is niet beschikbaar op Hallo hardware cluster dat momenteel fungeert als Hallo VM host.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Een Windows-VM niet in een beschikbaarheidsset vergroten of verkleinen
1. Lijst met Hallo VM-grootten die beschikbaar zijn op Hallo hardware cluster waar Hallo VM wordt gehost. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. Als Hallo grootte wordt vermeld gewenst, voert u Hallo opdrachten tooresize Hallo VM te volgen. Desgewenst Hallo formaat niet wordt vermeld, gaat u toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Als Hallo formaat niet wordt vermeld gewenst, voert u Hallo opdrachten toodeallocate Hallo VM, het formaat en Hallo VM starten na.
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> Toewijzing Hallo VM versies dynamische IP-adressen toegewezen toohello VM. Hello OS- en gegevensschijven worden niet getroffen. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Een virtuele machine van Windows in een beschikbaarheidsset vergroten of verkleinen
Als hello nieuwe grootte voor een virtuele machine in een beschikbaarheidsset niet beschikbaar op Hallo hardware cluster is moet momenteel host Hallo VM en vervolgens alle VM's in de beschikbaarheidsset Hallo toobe tooresize Hallo VM ongedaan. U moet wellicht ook tooupdate Hallo grootte van andere virtuele machines in Hallo beschikbaarheid instellen nadat er één virtuele machine is gewijzigd. een virtuele machine in een beschikbaarheidsset tooresize uitvoeren Hallo stappen te volgen.

1. Lijst met Hallo VM-grootten die beschikbaar zijn op Hallo hardware cluster waar Hallo VM wordt gehost.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. Als Hallo grootte wordt vermeld gewenst, voert u Hallo opdrachten tooresize Hallo VM te volgen. Als deze niet wordt weergegeven, gaat u toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Desgewenst Hallo formaat niet wordt vermeld, doorgaan met de Hallo toodeallocate stappen te volgen alle VM's in de beschikbaarheidsset hello, vergroten of verkleinen van virtuele machines en deze opnieuw opstarten.
4. Alle virtuele machines in de beschikbaarheidsset Hallo stoppen.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. Vergroten of verkleinen en Hallo virtuele machines in de beschikbaarheidsset Hallo opnieuw.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a>Volgende stappen
* Voor extra schaalbaarheid, meerdere exemplaren van de VM uitvoeren en uitbreiden. Zie voor meer informatie [automatisch schalen van Windows-machines in een virtuele-Machineschaalset](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

