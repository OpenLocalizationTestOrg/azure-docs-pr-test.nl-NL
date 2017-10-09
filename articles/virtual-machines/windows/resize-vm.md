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
# <a name="resize-a-windows-vm"></a><span data-ttu-id="3d5e0-103">Een Windows VM vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="3d5e0-103">Resize a Windows VM</span></span>
<span data-ttu-id="3d5e0-104">Dit artikel laat zien hoe tooresize een Windows-VM gemaakt in Hallo Resource Manager-implementatiemodel met Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="3d5e0-105">Nadat u een virtuele machine (VM) gemaakt, kunt u Hallo VM schalen omhoog of omlaag door Hallo VM-grootte wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="3d5e0-106">In sommige gevallen moet u eerst Hallo VM ongedaan.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="3d5e0-107">Dit kan gebeuren als de nieuwe grootte Hallo is niet beschikbaar op Hallo hardware cluster dat momenteel fungeert als Hallo VM host.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="3d5e0-108">Een Windows-VM niet in een beschikbaarheidsset vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="3d5e0-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="3d5e0-109">Lijst met Hallo VM-grootten die beschikbaar zijn op Hallo hardware cluster waar Hallo VM wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="3d5e0-110">Als Hallo grootte wordt vermeld gewenst, voert u Hallo opdrachten tooresize Hallo VM te volgen.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="3d5e0-111">Desgewenst Hallo formaat niet wordt vermeld, gaat u toostep 3.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="3d5e0-112">Als Hallo formaat niet wordt vermeld gewenst, voert u Hallo opdrachten toodeallocate Hallo VM, het formaat en Hallo VM starten na.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
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
> <span data-ttu-id="3d5e0-113">Toewijzing Hallo VM versies dynamische IP-adressen toegewezen toohello VM.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="3d5e0-114">Hello OS- en gegevensschijven worden niet getroffen.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="3d5e0-115">Een virtuele machine van Windows in een beschikbaarheidsset vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="3d5e0-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="3d5e0-116">Als hello nieuwe grootte voor een virtuele machine in een beschikbaarheidsset niet beschikbaar op Hallo hardware cluster is moet momenteel host Hallo VM en vervolgens alle VM's in de beschikbaarheidsset Hallo toobe tooresize Hallo VM ongedaan.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="3d5e0-117">U moet wellicht ook tooupdate Hallo grootte van andere virtuele machines in Hallo beschikbaarheid instellen nadat er één virtuele machine is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="3d5e0-118">een virtuele machine in een beschikbaarheidsset tooresize uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="3d5e0-119">Lijst met Hallo VM-grootten die beschikbaar zijn op Hallo hardware cluster waar Hallo VM wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="3d5e0-120">Als Hallo grootte wordt vermeld gewenst, voert u Hallo opdrachten tooresize Hallo VM te volgen.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="3d5e0-121">Als deze niet wordt weergegeven, gaat u toostep 3.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="3d5e0-122">Desgewenst Hallo formaat niet wordt vermeld, doorgaan met de Hallo toodeallocate stappen te volgen alle VM's in de beschikbaarheidsset hello, vergroten of verkleinen van virtuele machines en deze opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="3d5e0-123">Alle virtuele machines in de beschikbaarheidsset Hallo stoppen.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-123">Stop all VMs in hello availability set.</span></span>
   
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
5. <span data-ttu-id="3d5e0-124">Vergroten of verkleinen en Hallo virtuele machines in de beschikbaarheidsset Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3d5e0-124">Resize and restart hello VMs in hello availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="3d5e0-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d5e0-125">Next steps</span></span>
* <span data-ttu-id="3d5e0-126">Voor extra schaalbaarheid, meerdere exemplaren van de VM uitvoeren en uitbreiden. Zie voor meer informatie [automatisch schalen van Windows-machines in een virtuele-Machineschaalset](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="3d5e0-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

