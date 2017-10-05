---
title: Een beheerde schijf maken vanaf een VHD in Azure | Microsoft Docs
description: Een beheerde schijf maken vanaf een VHD die momenteel is in een Azure storage-account met het implementatiemodel van Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="5ed25-103">Beheerde schijven van niet-beheerde schijven in een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="5ed25-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="5ed25-104">Een beheerde schijf kan worden gemaakt vanuit een bestaande gegevensschijf of een besturingssysteemschijf die zich in een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="5ed25-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="5ed25-105">U kunt ook een lege schijf die kan worden gebruikt als een nieuwe gegevensschijf voor een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="5ed25-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="5ed25-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5ed25-106">Before you begin</span></span>
<span data-ttu-id="5ed25-107">Als u PowerShell gebruikt, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="5ed25-107">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5ed25-108">Voer de volgende opdracht om deze te installeren.</span><span class="sxs-lookup"><span data-stu-id="5ed25-108">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="5ed25-109">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5ed25-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="5ed25-110">Een beheerde schijf vanaf een VHD in Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="5ed25-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="5ed25-111">In het voorbeeld wordt een schijf maken vanaf een VHD als beheerde schijf en deze toewijzen aan de parameter **diskette $1** voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="5ed25-111">In the example we create a disk from a VHD as managed disk and assign it to the parameter **$disk1** to use later.</span></span> 

<span data-ttu-id="5ed25-112">De beheerde schijf wordt gemaakt in de **West VS** locatie in een resourcegroep met de naam **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5ed25-112">The managed disk will be created in the **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="5ed25-113">De schijf worden benoemd **myDisk** en deze wordt gemaakt van een VHD-bestand met de naam **myDisk.vhd** we eerder hebt geüpload naar een opslagaccount met de naam **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="5ed25-113">The disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded to a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="5ed25-114">De beheerde schijf wordt gemaakt in premium lokaal redundante opslag (LRS).</span><span class="sxs-lookup"><span data-stu-id="5ed25-114">The managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="5ed25-115">StandardLRS en PremiumLRS zijn de enige **- AccountType** beschikbare opties voor schijven die worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="5ed25-115">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="5ed25-116">Sommige parameters instellen</span><span class="sxs-lookup"><span data-stu-id="5ed25-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="5ed25-117">De gegevensschijf maken.</span><span class="sxs-lookup"><span data-stu-id="5ed25-117">Create the data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="5ed25-118">Een lege gegevensschijf als een beheerde schijf maken</span><span class="sxs-lookup"><span data-stu-id="5ed25-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="5ed25-119">In het voorbeeld wordt een lege gegevensschijf als beheerde schijf maken en toewijzen aan de parameter **$dataDisk2** voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="5ed25-119">In the example we create an empty data disk as managed disk and assign it to the parameter **$dataDisk2** to use later.</span></span> <span data-ttu-id="5ed25-120">Een lege gegevensschijf moet worden geïnitialiseerd aanmelden bij de virtuele machine en het gebruik van diskmgmt.msc of [op afstand met WinRM en een script](attach-disk-ps.md#initialize-the-disk), zodra deze is gekoppeld aan een actieve virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5ed25-120">An empty data disk will need to be initialized logging in to the VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached to a running VM.</span></span>

<span data-ttu-id="5ed25-121">De lege gegevensschijf wordt gemaakt in de **West-Centraal VS** locatie in een resourcegroep met de naam **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5ed25-121">The empty data disk will be created in the **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="5ed25-122">De schijf worden benoemd **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="5ed25-122">The disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="5ed25-123">De lege schijf wordt gemaakt in premium lokaal redundante opslag (LRS).</span><span class="sxs-lookup"><span data-stu-id="5ed25-123">The empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="5ed25-124">StandardLRS en PremiumLRS zijn de enige **- AccountType** beschikbare opties voor schijven die worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="5ed25-124">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="5ed25-125">De schijfgrootte in dit voorbeeld is 128GB, maar moet u een grootte die voldoet aan de behoeften van alle toepassingen die op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5ed25-125">The disk size in this example is 128GB, but you should choose a size that meets the needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="5ed25-126">Sommige parameters instellen</span><span class="sxs-lookup"><span data-stu-id="5ed25-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="5ed25-127">De gegevensschijf maken.</span><span class="sxs-lookup"><span data-stu-id="5ed25-127">Create the data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="5ed25-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ed25-128">Next Steps</span></span>   
- <span data-ttu-id="5ed25-129">Als u al een virtuele machine hebt, kunt u [een gegevensschijf koppelen](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5ed25-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
