---
title: aaaCreate kopie maken van een Azure beheerd schijf voor back-up | Microsoft Docs
description: Meer informatie over hoe toocreate een kopie van een Azure-schijf beheerd toouse voor reserve of probleemoplossing schijf uitgeeft.
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="843c1-103">Maak een kopie van een VHD die is opgeslagen als een beheerde Azure-schijf met behulp van momentopnamen beheerd</span><span class="sxs-lookup"><span data-stu-id="843c1-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="843c1-104">Een momentopname van een schijf beheerd voor back-up of een schijf beheerd vanuit Hallo momentopname maken en deze te koppelen tooa test virtuele machine tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="843c1-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="843c1-105">Een momentopname van een beheerd is een volledige point-in-time-kopie van een schijf VM beheerd.</span><span class="sxs-lookup"><span data-stu-id="843c1-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="843c1-106">Deze maakt een alleen-lezen kopie van uw VHD en standaard opgeslagen als een standaard beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="843c1-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="843c1-107">Zie voor meer informatie over beheerde schijven [overzicht van beheerde Azure-schijven](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="843c1-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="843c1-108">Zie voor meer informatie over prijzen [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="843c1-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="843c1-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="843c1-109">Before you begin</span></span>
<span data-ttu-id="843c1-110">Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="843c1-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="843c1-111">Voer Hallo na de opdracht tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="843c1-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="843c1-112">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="843c1-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="843c1-113">Hallo VHD met een momentopname kopiëren</span><span class="sxs-lookup"><span data-stu-id="843c1-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="843c1-114">Hello Azure-portal of PowerShell tootake een momentopname van Hallo beheerd schijf gebruiken.</span><span class="sxs-lookup"><span data-stu-id="843c1-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="843c1-115">Azure portal tootake een momentopname gebruiken</span><span class="sxs-lookup"><span data-stu-id="843c1-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="843c1-116">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="843c1-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="843c1-117">Beginnen in de linkerbovenhoek hello, klikt u op **nieuw** en zoek naar **momentopname**.</span><span class="sxs-lookup"><span data-stu-id="843c1-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="843c1-118">Klik op Hallo momentopname blade **maken**.</span><span class="sxs-lookup"><span data-stu-id="843c1-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="843c1-119">Voer een **naam** voor Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="843c1-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="843c1-120">Selecteer een bestaande [resourcegroep](../../azure-resource-manager/resource-group-overview.md#resource-groups) of Hallo typenaam voor een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="843c1-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="843c1-121">Selecteer een Azure-datacenter locatie.</span><span class="sxs-lookup"><span data-stu-id="843c1-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="843c1-122">Voor **bronschijf**, selecteer Hallo toosnapshot schijf beheerd.</span><span class="sxs-lookup"><span data-stu-id="843c1-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="843c1-123">Selecteer Hallo **accounttype** toouse toostore Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="843c1-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="843c1-124">Het is raadzaam **Standard_LRS** tenzij u deze opgeslagen op een hoog presterende schijf nodig.</span><span class="sxs-lookup"><span data-stu-id="843c1-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="843c1-125">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="843c1-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="843c1-126">Gebruik PowerShell tootake een momentopname</span><span class="sxs-lookup"><span data-stu-id="843c1-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="843c1-127">Hallo volgende stappen ziet u hoe tooget Hallo VHD schijf toobe gekopieerd, maken Hallo momentopnameconfiguraties en een momentopname van het Hallo-schijf met behulp van de cmdlet New-AzureRmSnapshot hello<!--Add link toocmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="843c1-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="843c1-128">Sommige parameters instellen.</span><span class="sxs-lookup"><span data-stu-id="843c1-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="843c1-129">Vervang de parameterwaarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="843c1-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="843c1-130">"myResourceGroup" met de resourcegroep Hallo van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="843c1-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="843c1-131">'southeastasia' hello geografische locatie waar u uw beheerde momentopname opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="843c1-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="843c1-132">"ContosoMD_datadisk1" met de naam van de Hallo van Hallo VHD schijf die u toocopy wilt.</span><span class="sxs-lookup"><span data-stu-id="843c1-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="843c1-133">'ContosoMD_datadisk1_snapshot1' Hello servernaam die u hebt toouse voor nieuwe Hallo-momentopname wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="843c1-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="843c1-134">Hallo VHD schijf toobe gekopieerd ophalen.</span><span class="sxs-lookup"><span data-stu-id="843c1-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="843c1-135">Hallo momentopnameconfiguraties maken.</span><span class="sxs-lookup"><span data-stu-id="843c1-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="843c1-136">Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="843c1-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="843c1-137">Als u toouse Hallo momentopname toocreate van plan een schijf beheerd bent en koppelt u dit een virtuele machine die toobe hoge prestaties behoeften, gebruikt u Hallo parameter `-AccountType Premium_LRS` met Hallo nieuw AzureRmSnapshot-opdracht.</span><span class="sxs-lookup"><span data-stu-id="843c1-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="843c1-138">Hallo-parameter wordt Hallo momentopname gemaakt, zodat deze wordt opgeslagen als een schijf Premium beheerd.</span><span class="sxs-lookup"><span data-stu-id="843c1-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="843c1-139">Premium-schijven beheerd zijn duurder dan de standaard.</span><span class="sxs-lookup"><span data-stu-id="843c1-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="843c1-140">Daarom moet u dat wat u moet Premium voordat u deze parameter.</span><span class="sxs-lookup"><span data-stu-id="843c1-140">So be sure you really need Premium before using that parameter.</span></span>


