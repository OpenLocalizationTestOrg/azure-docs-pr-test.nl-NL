---
title: Grootte van een Windows-VM in Azure met PowerShell | Microsoft Docs
description: Het formaat van een virtuele Windows-computer in het Resource Manager-implementatiemodel, met Azure Powershell hebt gemaakt.
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
ms.openlocfilehash: 742efd1496de9ce76b1e5636297ef30f546bd108
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="62fa1-103">Een Windows VM vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="62fa1-103">Resize a Windows VM</span></span>
<span data-ttu-id="62fa1-104">In dit artikel leest u hoe het formaat van een virtuele machine van Windows, in het Resource Manager-implementatiemodel met Azure Powershell hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="62fa1-104">This article shows you how to resize a Windows VM, created in the Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="62fa1-105">Nadat u een virtuele machine (VM) gemaakt, u kunt de virtuele machine omhoog of omlaag schalen door het wijzigen van de VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="62fa1-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span></span> <span data-ttu-id="62fa1-106">In sommige gevallen moet u eerst de VM ongedaan.</span><span class="sxs-lookup"><span data-stu-id="62fa1-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="62fa1-107">Dit kan gebeuren als de nieuwe grootte is niet beschikbaar op de hardware-cluster waarop de virtuele machine wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="62fa1-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="62fa1-108">Een Windows-VM niet in een beschikbaarheidsset vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="62fa1-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="62fa1-109">Lijst van de VM-grootten die beschikbaar zijn op de hardware-cluster waarop de virtuele machine wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="62fa1-109">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="62fa1-110">Als de gewenste grootte wordt weergegeven, voer de volgende opdrachten om het formaat van de virtuele machine aan.</span><span class="sxs-lookup"><span data-stu-id="62fa1-110">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="62fa1-111">Als de gewenste grootte niet wordt weergegeven, gaat u naar stap 3.</span><span class="sxs-lookup"><span data-stu-id="62fa1-111">If the desired size is not listed, go on to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="62fa1-112">Als de gewenste grootte niet wordt weergegeven, voer de volgende opdrachten toewijzing van de virtuele machine, het formaat en opnieuw opstarten van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="62fa1-112">If the desired size is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span></span>
   
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
> <span data-ttu-id="62fa1-113">Toewijzing van de virtuele machine versies dynamische IP-adressen toegewezen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="62fa1-113">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="62fa1-114">Het besturingssysteem en de gegevensschijven worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="62fa1-114">The OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="62fa1-115">Een virtuele machine van Windows in een beschikbaarheidsset vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="62fa1-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="62fa1-116">Als de nieuwe grootte voor een virtuele machine in een beschikbaarheidsset niet beschikbaar is op de hardware-cluster momenteel de virtuele machine host is, moet alle VM's in de beschikbaarheidsset aan om de grootte van de virtuele machine te ongedaan.</span><span class="sxs-lookup"><span data-stu-id="62fa1-116">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span></span> <span data-ttu-id="62fa1-117">Ook is het mogelijk om bij te werken van de grootte van andere virtuele machines in de beschikbaarheidsset nadat er één virtuele machine is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="62fa1-117">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span></span> <span data-ttu-id="62fa1-118">Als u een virtuele machine in een beschikbaarheidsset, moet u de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="62fa1-118">To resize a VM in an availability set, perform the following steps.</span></span>

1. <span data-ttu-id="62fa1-119">Lijst van de VM-grootten die beschikbaar zijn op de hardware-cluster waarop de virtuele machine wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="62fa1-119">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="62fa1-120">Als de gewenste grootte wordt weergegeven, voer de volgende opdrachten om het formaat van de virtuele machine aan.</span><span class="sxs-lookup"><span data-stu-id="62fa1-120">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="62fa1-121">Als deze niet wordt weergegeven, gaat u naar stap 3.</span><span class="sxs-lookup"><span data-stu-id="62fa1-121">If it is not listed, go to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="62fa1-122">Als de gewenste grootte niet wordt weergegeven, gaat u verder met de volgende stappen uit op alle VM's in de beschikbaarheidsset ongedaan vergroten of verkleinen van virtuele machines en het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="62fa1-122">If the desired size is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="62fa1-123">Stop alle VM's in de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="62fa1-123">Stop all VMs in the availability set.</span></span>
   
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
5. <span data-ttu-id="62fa1-124">De grootte wijzigen en opnieuw opstarten van de virtuele machines in de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="62fa1-124">Resize and restart the VMs in the availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="62fa1-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62fa1-125">Next steps</span></span>
* <span data-ttu-id="62fa1-126">Voor extra schaalbaarheid, meerdere exemplaren van de VM uitvoeren en uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="62fa1-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="62fa1-127">Zie voor meer informatie [automatisch schalen van Windows-machines in een virtuele-Machineschaalset](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="62fa1-127">For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

