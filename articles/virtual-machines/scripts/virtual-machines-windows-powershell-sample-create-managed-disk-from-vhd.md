---
title: Azure PowerShell-Script steekproef - maken van een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of verschillende abonnement | Microsoft Docs
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
ms.openlocfilehash: 728def40a3eb132537decbd099fa71f4544c6b87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="9c093-103">Maak een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of verschillende abonnement met PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c093-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="9c093-104">Dit script maakt een beheerde schijf van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="9c093-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="9c093-105">Dit script gebruiken voor het importeren van een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD naar beheerde OS-schijf voor het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9c093-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="9c093-106">Deze ook gebruiken voor het importeren van een VHD-gegevens naar beheerde gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="9c093-106">Also, use it to import a data VHD to managed data disk.</span></span> 

<span data-ttu-id="9c093-107">Maak meerdere identieke beheerde schijven van een VHD-bestand in een kleine hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="9c093-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="9c093-108">Als u wilt maken beheerde schijven van een vhd-bestand, blob-momentopname van het vhd-bestand wordt gemaakt en wordt vervolgens gebruikt om beheerde schijven te maken.</span><span class="sxs-lookup"><span data-stu-id="9c093-108">To create managed disks from a vhd file, blob snapshot of the vhd file is created and then it is used to create managed disks.</span></span> <span data-ttu-id="9c093-109">Slechts één blob momentopname kan worden gemaakt in een minuut dat ervoor zorgt het maken van schijffouten vanwege een beperking dat.</span><span class="sxs-lookup"><span data-stu-id="9c093-109">Only one blob snapshot can be created in a minute that causes disk creation failures due to throttling.</span></span> <span data-ttu-id="9c093-110">Om te voorkomen dat deze beperking, maakt u een [beheerde momentopname van het vhd-bestand](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) en gebruik beheerd voor de beheerde momentopname maken van meerdere schijven vervolgens in korte tijd.</span><span class="sxs-lookup"><span data-stu-id="9c093-110">To avoid this throttling, create a [managed snapshot from the vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use the managed snapshot to create multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9c093-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9c093-111">Sample script</span></span>

<span data-ttu-id="9c093-112">[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "-beheerde schijven van VHD maken")]</span><span class="sxs-lookup"><span data-stu-id="9c093-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="9c093-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9c093-113">Script explanation</span></span>

<span data-ttu-id="9c093-114">Dit script gebruikt na de opdrachten voor het maken van een beheerde schijf vanaf een VHD in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="9c093-114">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="9c093-115">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="9c093-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9c093-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9c093-116">Command</span></span> | <span data-ttu-id="9c093-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9c093-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9c093-118">Nieuwe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="9c093-118">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="9c093-119">Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf.</span><span class="sxs-lookup"><span data-stu-id="9c093-119">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="9c093-120">Dit omvat opslagtype, locatie, resource-Id van het opslagaccount waarin de bovenliggende VHD is opgeslagen, VHD-URI van de bovenliggende VHD.</span><span class="sxs-lookup"><span data-stu-id="9c093-120">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="9c093-121">Nieuwe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="9c093-121">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="9c093-122">Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="9c093-122">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c093-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c093-123">Next steps</span></span>

[<span data-ttu-id="9c093-124">Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="9c093-124">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="9c093-125">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9c093-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9c093-126">Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c093-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>