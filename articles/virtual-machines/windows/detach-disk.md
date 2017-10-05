---
title: Een gegevensschijf loskoppelen van een virtuele machine van Windows - Azure | Microsoft Docs
description: Meer informatie naar een gegevensschijf loskoppelen van een virtuele machine in Azure met behulp van het Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 97aa69745d200ee76f9f859eb3a8b0ad2f202bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="1e65b-103">Hoe u een gegevensschijf loskoppelen van een virtuele Windows-computer</span><span class="sxs-lookup"><span data-stu-id="1e65b-103">How to detach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="1e65b-104">Wanneer u een gegevensschijf die is gekoppeld aan een virtuele machine niet meer nodig hebt, kunt u deze eenvoudig loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="1e65b-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="1e65b-105">Hiermee verwijdert u de schijf van de virtuele machine, maar niet verwijderd uit de opslag.</span><span class="sxs-lookup"><span data-stu-id="1e65b-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="1e65b-106">Als u een schijf die wordt niet automatisch verwijderd loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="1e65b-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="1e65b-107">Als u bent geabonneerd op Premium-opslag, moet u blijft kosten voor opslag voor de schijf.</span><span class="sxs-lookup"><span data-stu-id="1e65b-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="1e65b-108">Raadpleeg voor meer informatie [prijzen en facturering wanneer u Premium-opslag](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="1e65b-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="1e65b-109">Als u de bestaande gegevens op de schijf opnieuw wilt gebruiken, kunt u de schijf opnieuw koppelen aan dezelfde of een andere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1e65b-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="1e65b-110">Een gegevensschijf ontkoppelen via de portal</span><span class="sxs-lookup"><span data-stu-id="1e65b-110">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="1e65b-111">Selecteer in de portal hub **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="1e65b-111">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="1e65b-112">Selecteer de virtuele machine met de gegevensschijf die u wilt loskoppelen en klik op **stoppen** toewijzing van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1e65b-112">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="1e65b-113">Selecteer in de virtuele machineblade **schijven**.</span><span class="sxs-lookup"><span data-stu-id="1e65b-113">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="1e65b-114">Aan de bovenkant van de **schijven** blade Selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1e65b-114">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="1e65b-115">In de **schijven** blade, aan de rechterkant van de gegevensschijf die u wilt loskoppelen, klikt u op de ![Detach knopafbeelding](./media/detach-disk/detach.png) knop loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="1e65b-115">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="1e65b-116">Nadat de schijf is verwijderd, klikt u op opslaan boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="1e65b-116">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="1e65b-117">Klik op de blade virtuele machine **overzicht** en klik vervolgens op de **Start** knop aan de bovenkant van de blade opnieuw opstarten van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1e65b-117">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>



<span data-ttu-id="1e65b-118">De schijf blijft in de opslag, maar is niet meer gekoppeld aan een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1e65b-118">The disk remains in storage but is no longer attached to a virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="1e65b-119">Een gegevensschijf met behulp van PowerShell loskoppelen</span><span class="sxs-lookup"><span data-stu-id="1e65b-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="1e65b-120">In dit voorbeeld wordt de eerste opdracht wordt de virtuele machine met de naam opgehaald **MyVM07** in de **RG11** resourcegroep met de cmdlet Get-AzureRmVM.</span><span class="sxs-lookup"><span data-stu-id="1e65b-120">In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="1e65b-121">De opdracht slaat de virtuele machine in de **$VirtualMachine** variabele.</span><span class="sxs-lookup"><span data-stu-id="1e65b-121">The command stores the virtual machine in the **$VirtualMachine** variable.</span></span>

<span data-ttu-id="1e65b-122">De tweede opdracht verwijdert u de gegevensschijf DataDisk3 met de naam van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1e65b-122">The second command removes the data disk named DataDisk3 from the virtual machine.</span></span>

<span data-ttu-id="1e65b-123">De laatste opdracht werkt de status van de virtuele machine om het proces van het verwijderen van de gegevensschijf te voltooien.</span><span class="sxs-lookup"><span data-stu-id="1e65b-123">The final command updates the state of the virtual machine to complete the process of removing the data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="1e65b-124">Zie voor meer informatie [verwijderen AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="1e65b-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e65b-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e65b-125">Next steps</span></span>
<span data-ttu-id="1e65b-126">Als u de gegevensschijf gebruiken wilt, kunt u zojuist hebt [koppelen aan een andere virtuele machine](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1e65b-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

