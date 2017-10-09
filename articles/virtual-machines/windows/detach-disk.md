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
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="836f6-103">Hoe toodetach een schijf van een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="836f6-103">How toodetach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="836f6-104">Wanneer u een gegevensschijf die is aangesloten tooa virtuele machine niet meer nodig hebt, kunt u deze eenvoudig loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="836f6-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="836f6-105">Deze taak verwijdert Hallo schijf uit de Hallo virtuele machine, maar niet verwijderd uit de opslag.</span><span class="sxs-lookup"><span data-stu-id="836f6-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="836f6-106">Als u een schijf die wordt niet automatisch verwijderd loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="836f6-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="836f6-107">Als u tooPremium opslag hebt geabonneerd, blijft u tooincur opslagkosten voor Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="836f6-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="836f6-108">Voor meer informatie raadpleegt u te[prijzen en facturering wanneer u Premium-opslag](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="836f6-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="836f6-109">Als u toouse Hallo bestaande gegevens op Hallo schijf opnieuw wilt, u kunt opnieuw het toohello dezelfde virtuele machine of een andere naam.</span><span class="sxs-lookup"><span data-stu-id="836f6-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="836f6-110">Een gegevensschijf met Hallo portal loskoppelen</span><span class="sxs-lookup"><span data-stu-id="836f6-110">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="836f6-111">Selecteer in de portal hub hello, **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="836f6-111">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="836f6-112">Selecteer Hallo virtuele machine met Hallo gegevensschijf toodetach en klik op **stoppen** toodeallocate Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="836f6-112">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="836f6-113">Selecteer in de blade van de virtuele machine hello, **schijven**.</span><span class="sxs-lookup"><span data-stu-id="836f6-113">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="836f6-114">Hallo boven aan het Hallo **schijven** blade Selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="836f6-114">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="836f6-115">In Hallo **schijven** blade toohello uiterst rechts in Hallo gegevensschijf dat u toodetach wilt, klikt u op Hallo ![Detach knopafbeelding](./media/detach-disk/detach.png) knop loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="836f6-115">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="836f6-116">Nadat het Hallo-schijf is verwijderd, klikt u op opslaan op Hallo Hallo blade bovenaan.</span><span class="sxs-lookup"><span data-stu-id="836f6-116">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="836f6-117">In de blade van de virtuele machine hello, klikt u op **overzicht** en klik vervolgens op Hallo **Start** knop bovenaan Hallo Hallo blade toorestart Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="836f6-117">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>



<span data-ttu-id="836f6-118">Hallo schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="836f6-118">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="836f6-119">Een gegevensschijf met behulp van PowerShell loskoppelen</span><span class="sxs-lookup"><span data-stu-id="836f6-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="836f6-120">In dit voorbeeld Hallo eerste opdracht opgehaald Hallo virtuele machine met de naam **MyVM07** in Hallo **RG11** resourcegroep met de cmdlet Get-AzureRmVM Hallo.</span><span class="sxs-lookup"><span data-stu-id="836f6-120">In this example, hello first command gets hello virtual machine named **MyVM07** in hello **RG11** resource group using hello Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="836f6-121">opdracht slaat virtuele machine in Hallo HALLO hallo **$VirtualMachine** variabele.</span><span class="sxs-lookup"><span data-stu-id="836f6-121">hello command stores hello virtual machine in hello **$VirtualMachine** variable.</span></span>

<span data-ttu-id="836f6-122">de tweede opdracht Hallo verwijdert Hallo gegevensschijf DataDisk3 met de naam van de Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="836f6-122">hello second command removes hello data disk named DataDisk3 from hello virtual machine.</span></span>

<span data-ttu-id="836f6-123">de laatste opdracht Hallo Hallo status van Hallo toocomplete Hallo proces voor virtuele machines van het verwijderen van de gegevensschijf Hallo-updates.</span><span class="sxs-lookup"><span data-stu-id="836f6-123">hello final command updates hello state of hello virtual machine toocomplete hello process of removing hello data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="836f6-124">Zie voor meer informatie [verwijderen AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="836f6-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="836f6-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="836f6-125">Next steps</span></span>
<span data-ttu-id="836f6-126">Als u tooreuse Hallo gegevensschijf wilt, kunt u zojuist hebt [tooanother VM koppelen](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="836f6-126">If you want tooreuse hello data disk, you can just [attach it tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

