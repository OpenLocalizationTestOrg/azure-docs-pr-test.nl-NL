---
title: een beheerde schijf van een VHD in Azure aaaCreate | Microsoft Docs
description: Een beheerde schijf maken vanaf een VHD die momenteel is in een Azure storage-account met Hallo Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="c3fc3-103">Beheerde schijven van niet-beheerde schijven in een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="c3fc3-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="c3fc3-104">Een beheerde schijf kan worden gemaakt vanuit een bestaande gegevensschijf of een besturingssysteemschijf die zich in een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="c3fc3-105">U kunt ook een lege schijf die kan worden gebruikt als een nieuwe gegevensschijf voor een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="c3fc3-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c3fc3-106">Before you begin</span></span>
<span data-ttu-id="c3fc3-107">Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="c3fc3-108">Voer Hallo na de opdracht tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="c3fc3-109">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c3fc3-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="c3fc3-110">Een beheerde schijf vanaf een VHD in Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="c3fc3-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="c3fc3-111">In voorbeeld Hallo we een schijf van een VHD als beheerde schijf maken en toewijzen toohello parameter **diskette $1** toouse later.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="c3fc3-112">Hallo beheerde schijf wordt gemaakt in Hallo **West VS** locatie in een resourcegroep met de naam **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="c3fc3-113">Hallo schijf worden benoemd **myDisk** en deze wordt gemaakt van een VHD-bestand met de naam **myDisk.vhd** we eerder tooa opslagaccount met de naam geüpload **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="c3fc3-114">Hallo-beheerde schijven wordt gemaakt in premium lokaal redundante opslag (LRS).</span><span class="sxs-lookup"><span data-stu-id="c3fc3-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="c3fc3-115">StandardLRS en PremiumLRS zijn alleen Hallo **- AccountType** beschikbare opties voor schijven die worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="c3fc3-116">Sommige parameters instellen</span><span class="sxs-lookup"><span data-stu-id="c3fc3-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="c3fc3-117">Hallo gegevensschijf maken.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="c3fc3-118">Een lege gegevensschijf als een beheerde schijf maken</span><span class="sxs-lookup"><span data-stu-id="c3fc3-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="c3fc3-119">In voorbeeld Hallo we een lege gegevensschijf als beheerde schijf maken en toewijzen toohello parameter **$dataDisk2** toouse later.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="c3fc3-120">Een lege gegevensschijf moet toobe geïnitialiseerd toohello VM aanmelden en het gebruik van diskmgmt.msc of [op afstand met WinRM en een script](attach-disk-ps.md#initialize-the-disk), wanneer het bijgevoegde tooa VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="c3fc3-121">Hallo lege gegevensschijf worden aangemaakt in Hallo **West-Centraal VS** locatie in een resourcegroep met de naam **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="c3fc3-122">Hallo schijf worden benoemd **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="c3fc3-123">Hallo lege schijf wordt gemaakt in premium lokaal redundante opslag (LRS).</span><span class="sxs-lookup"><span data-stu-id="c3fc3-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="c3fc3-124">StandardLRS en PremiumLRS zijn alleen Hallo **- AccountType** beschikbare opties voor schijven die worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="c3fc3-125">Hallo-schijfgrootte in dit voorbeeld is 128GB, maar moet u een grootte die voldoet aan de behoeften Hallo van alle toepassingen die op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="c3fc3-126">Sommige parameters instellen</span><span class="sxs-lookup"><span data-stu-id="c3fc3-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="c3fc3-127">Hallo gegevensschijf maken.</span><span class="sxs-lookup"><span data-stu-id="c3fc3-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="c3fc3-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3fc3-128">Next Steps</span></span>   
- <span data-ttu-id="c3fc3-129">Als u al een virtuele machine hebt, kunt u [een gegevensschijf koppelen](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c3fc3-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
