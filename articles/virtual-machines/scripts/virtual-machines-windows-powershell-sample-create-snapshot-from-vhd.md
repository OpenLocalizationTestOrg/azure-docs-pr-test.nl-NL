---
title: PowerShell-voorbeeldscript - aaaAzure een momentopname maken van een VHD-toocreate meerdere identieke beheerde schijven in een kleine hoeveelheid tijd | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een momentopname maken van een VHD-toocreate meerdere identieke beheerde schijven in een kleine hoeveelheid tijd'
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
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="50eee-103">Een momentopname maken van een VHD-toocreate meerdere identieke beheerde schijven in een kleine hoeveelheid tijd met PowerShell</span><span class="sxs-lookup"><span data-stu-id="50eee-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="50eee-104">Dit script maakt een momentopname van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="50eee-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="50eee-105">Gebruik dit script tooimport een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD tooa momentopname en gebruik vervolgens Hallo momentopname toocreate meerdere identieke beheerde schijven in een kleine hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="50eee-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="50eee-106">Gebruik tevens een momentopname van de VHD gegevens tooa tooimport en gebruik vervolgens Hallo momentopname toocreate meerdere beheerde schijven in een kleine hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="50eee-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="50eee-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="50eee-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="50eee-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="50eee-108">Script explanation</span></span>

<span data-ttu-id="50eee-109">Dit script gebruikt na opdrachten toocreate een beheerde schijf van een VHD in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="50eee-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="50eee-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="50eee-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="50eee-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="50eee-111">Command</span></span> | <span data-ttu-id="50eee-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="50eee-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="50eee-113">Nieuwe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="50eee-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="50eee-114">Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf.</span><span class="sxs-lookup"><span data-stu-id="50eee-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="50eee-115">Dit omvat opslagtype, locatie, resource-Id van het opslagaccount Hallo waar Hallo bovenliggende VHD wordt opgeslagen en VHD-URI van Hallo bovenliggende VHD.</span><span class="sxs-lookup"><span data-stu-id="50eee-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="50eee-116">Nieuwe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="50eee-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="50eee-117">Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="50eee-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50eee-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50eee-118">Next steps</span></span>

[<span data-ttu-id="50eee-119">Een beheerde schijf maken vanuit een momentopname.</span><span class="sxs-lookup"><span data-stu-id="50eee-119">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="50eee-120">Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="50eee-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="50eee-121">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="50eee-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="50eee-122">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50eee-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
