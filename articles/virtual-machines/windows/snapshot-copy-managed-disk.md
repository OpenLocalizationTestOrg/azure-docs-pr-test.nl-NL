---
title: Maak een kopie van een Azure beheerd schijf voor back up | Microsoft Docs
description: Informatie over het maken van een kopie van een Azure beheerd schijf moet worden gebruikt voor back up of het oplossen van problemen van de schijf.
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
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="579d4-103">Maak een kopie van een VHD die is opgeslagen als een beheerde Azure-schijf met behulp van momentopnamen beheerd</span><span class="sxs-lookup"><span data-stu-id="579d4-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="579d4-104">Een momentopname van een schijf beheerd voor back-up of een schijf beheerd vanaf de momentopname maken en koppelen aan een virtuele testmachine om op te lossen.</span><span class="sxs-lookup"><span data-stu-id="579d4-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="579d4-105">Een momentopname van een beheerd is een volledige point-in-time-kopie van een schijf VM beheerd.</span><span class="sxs-lookup"><span data-stu-id="579d4-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="579d4-106">Deze maakt een alleen-lezen kopie van uw VHD en standaard opgeslagen als een standaard beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="579d4-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="579d4-107">Zie voor meer informatie over beheerde schijven [overzicht van beheerde Azure-schijven](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="579d4-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="579d4-108">Zie voor meer informatie over prijzen [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="579d4-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="579d4-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="579d4-109">Before you begin</span></span>
<span data-ttu-id="579d4-110">Als u PowerShell gebruikt, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="579d4-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="579d4-111">Voer de volgende opdracht om deze te installeren.</span><span class="sxs-lookup"><span data-stu-id="579d4-111">Run the following command to install it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="579d4-112">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="579d4-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-the-vhd-with-a-snapshot"></a><span data-ttu-id="579d4-113">Kopieer de VHD met een momentopname</span><span class="sxs-lookup"><span data-stu-id="579d4-113">Copy the VHD with a snapshot</span></span>
<span data-ttu-id="579d4-114">Azure portal of PowerShell gebruiken om een momentopname van de schijf worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="579d4-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span></span>

### <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="579d4-115">Azure portal gebruiken om een momentopname</span><span class="sxs-lookup"><span data-stu-id="579d4-115">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="579d4-116">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="579d4-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="579d4-117">Beginnen in de linkerbovenhoek, klikt u op **nieuw** en zoek naar **momentopname**.</span><span class="sxs-lookup"><span data-stu-id="579d4-117">Starting in the upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="579d4-118">Klik op de blade momentopname **maken**.</span><span class="sxs-lookup"><span data-stu-id="579d4-118">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="579d4-119">Voer een **naam** voor de momentopname.</span><span class="sxs-lookup"><span data-stu-id="579d4-119">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="579d4-120">Selecteer een bestaande [Resourcegroep](../../azure-resource-manager/resource-group-overview.md#resource-groups) of typ de gewenste naam voor een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="579d4-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="579d4-121">Selecteer een Azure-datacenter locatie.</span><span class="sxs-lookup"><span data-stu-id="579d4-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="579d4-122">Voor **bronschijf**, selecteert u de schijf worden beheerd met de momentopname.</span><span class="sxs-lookup"><span data-stu-id="579d4-122">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="579d4-123">Selecteer de **accounttype** moet worden gebruikt voor het opslaan van de momentopname.</span><span class="sxs-lookup"><span data-stu-id="579d4-123">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="579d4-124">Het is raadzaam **Standard_LRS** tenzij u deze opgeslagen op een hoog presterende schijf nodig.</span><span class="sxs-lookup"><span data-stu-id="579d4-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="579d4-125">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="579d4-125">Click **Create**.</span></span>

### <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="579d4-126">PowerShell gebruiken om een momentopname</span><span class="sxs-lookup"><span data-stu-id="579d4-126">Use PowerShell to take a snapshot</span></span>
<span data-ttu-id="579d4-127">De volgende stappen ziet u hoe u de VHD-schijf moet worden gekopieerd, maken de momentopnameconfiguraties en een momentopname van de schijf met de cmdlet New-AzureRmSnapshot<!--Add link to cmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="579d4-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span></span> 

1. <span data-ttu-id="579d4-128">Sommige parameters instellen.</span><span class="sxs-lookup"><span data-stu-id="579d4-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="579d4-129">Vervang de parameterwaarden:</span><span class="sxs-lookup"><span data-stu-id="579d4-129">Replace the parameter values:</span></span>
  -  <span data-ttu-id="579d4-130">"myResourceGroup" met de resourcegroep van de VM.</span><span class="sxs-lookup"><span data-stu-id="579d4-130">"myResourceGroup" with the VM's resource group.</span></span>
  -  <span data-ttu-id="579d4-131">"southeastasia" met de geografische locatie waar u uw beheerde momentopname opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="579d4-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="579d4-132">"ContosoMD_datadisk1" met de naam van de VHD-schijf die u wilt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="579d4-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span></span>
  -  <span data-ttu-id="579d4-133">"ContosoMD_datadisk1_snapshot1" met de naam die u wilt gebruiken voor de nieuwe momentopname.</span><span class="sxs-lookup"><span data-stu-id="579d4-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span></span>

2. <span data-ttu-id="579d4-134">Ophalen van de VHD-schijf moet worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="579d4-134">Get the VHD disk to be copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="579d4-135">Maken van de momentopnameconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="579d4-135">Create the snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="579d4-136">De momentopname.</span><span class="sxs-lookup"><span data-stu-id="579d4-136">Take the snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="579d4-137">Als u van plan bent de momentopname gebruiken om te maken van een schijf beheerd en koppelt u dit een virtuele machine die moet worden hoge prestaties, gebruikt u de parameter `-AccountType Premium_LRS` met de opdracht New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="579d4-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="579d4-138">De parameter wordt de momentopname gemaakt zodat deze wordt opgeslagen als een schijf Premium beheerd.</span><span class="sxs-lookup"><span data-stu-id="579d4-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="579d4-139">Premium-schijven beheerd zijn duurder dan de standaard.</span><span class="sxs-lookup"><span data-stu-id="579d4-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="579d4-140">Daarom moet u dat wat u moet Premium voordat u deze parameter.</span><span class="sxs-lookup"><span data-stu-id="579d4-140">So be sure you really need Premium before using that parameter.</span></span>


