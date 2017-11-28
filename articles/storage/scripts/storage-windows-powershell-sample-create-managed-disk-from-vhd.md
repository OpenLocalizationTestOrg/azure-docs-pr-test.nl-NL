---
title: een beheerde schijf aaaAzure PowerShell-voorbeeldscript - maken van een VHD-bestand in een opslagaccount in dezelfde of verschillende abonnement | Microsoft Docs
description: Azure PowerShell-Script steekproef - maken van een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="45a93-103">Maak een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of verschillende abonnement met PowerShell</span><span class="sxs-lookup"><span data-stu-id="45a93-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="45a93-104">Dit script maakt een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="45a93-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="45a93-105">Gebruik dit script tooimport een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD toomanaged OS schijf toocreate een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="45a93-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="45a93-106">Gebruik tevens het tooimport een gegevensschijf VHD toomanaged gegevens.</span><span class="sxs-lookup"><span data-stu-id="45a93-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="45a93-107">Maak meerdere identieke beheerde schijven van een VHD-bestand in een kleine hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="45a93-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="45a93-108">toocreate schijven die worden beheerd vanaf een vhd-bestand, blob-momentopname van Hallo vhd-bestand wordt gemaakt en wordt het gebruikte toocreate beheerd schijven.</span><span class="sxs-lookup"><span data-stu-id="45a93-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="45a93-109">Slechts één blob momentopname kan worden gemaakt in een minuut dat ervoor zorgt het maken van schijffouten dat vanwege toothrottling.</span><span class="sxs-lookup"><span data-stu-id="45a93-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="45a93-110">tooavoid deze beperking, maak een [beheerde momentopname van de vhd-bestand Hallo](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) en vervolgens gebruik Hallo beheerd momentopname toocreate meerdere beheerde schijven in korte tijd.</span><span class="sxs-lookup"><span data-stu-id="45a93-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="45a93-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="45a93-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="45a93-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="45a93-112">Script explanation</span></span>

<span data-ttu-id="45a93-113">Dit script gebruikt na opdrachten toocreate een beheerde schijf van een VHD in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="45a93-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="45a93-114">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="45a93-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="45a93-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="45a93-115">Command</span></span> | <span data-ttu-id="45a93-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="45a93-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45a93-117">Nieuwe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="45a93-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="45a93-118">Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf.</span><span class="sxs-lookup"><span data-stu-id="45a93-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="45a93-119">Dit omvat opslagtype, locatie, resource-Id van Hallo opslagaccount waar Hallo bovenliggende VHD wordt opgeslagen, VHD-URI van Hallo bovenliggende VHD.</span><span class="sxs-lookup"><span data-stu-id="45a93-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="45a93-120">Nieuwe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="45a93-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="45a93-121">Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="45a93-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45a93-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45a93-122">Next steps</span></span>

[<span data-ttu-id="45a93-123">Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="45a93-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="45a93-124">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45a93-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="45a93-125">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45a93-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
