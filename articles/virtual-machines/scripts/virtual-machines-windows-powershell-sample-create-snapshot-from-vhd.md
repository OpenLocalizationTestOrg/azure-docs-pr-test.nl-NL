---
title: 'Azure PowerShell-Script voorbeeld: een momentopname maken van een VHD voor het maken van meerdere identieke beheerde schijven in een kleine hoeveelheid tijd | Microsoft Docs'
description: 'Azure PowerShell-Script voorbeeld: een momentopname maken van een VHD voor het maken van meerdere identieke beheerde schijven in een kleine hoeveelheid tijd'
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
ms.openlocfilehash: 02a69abd6c17ce765996379309e22afad82c4e10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="a7790-103">Een momentopname maken van een VHD voor het maken van meerdere identieke beheerde schijven in een kleine hoeveelheid tijd met PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7790-103">Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="a7790-104">Dit script maakt een momentopname van een VHD-bestand in een opslagaccount in dezelfde of een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7790-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="a7790-105">Dit script gebruiken voor het importeren van een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD naar een momentopname en gebruik vervolgens de momentopname voor het maken van meerdere identieke schijven die worden beheerd in een kleine hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="a7790-105">Use this script to import a specialized (not generalized/sysprepped) VHD to a snapshot and then use the snapshot to create multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="a7790-106">Ook gebruikt om een VHD-gegevens importeren in een momentopname en gebruik vervolgens de momentopname maken van meerdere beheerde schijven in een kleine hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="a7790-106">Also, use it to import a data VHD to a snapshot and then use the snapshot to create multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a7790-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a7790-107">Sample script</span></span>

<span data-ttu-id="a7790-108">[!code-powershell[belangrijkste](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "momentopname maken van VHD")]</span><span class="sxs-lookup"><span data-stu-id="a7790-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="a7790-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a7790-109">Script explanation</span></span>

<span data-ttu-id="a7790-110">Dit script gebruikt na de opdrachten voor het maken van een beheerde schijf vanaf een VHD in een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7790-110">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="a7790-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="a7790-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a7790-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a7790-112">Command</span></span> | <span data-ttu-id="a7790-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a7790-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a7790-114">Nieuwe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="a7790-114">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="a7790-115">Maakt de configuratie van de schijf die wordt gebruikt voor het maken van de schijf.</span><span class="sxs-lookup"><span data-stu-id="a7790-115">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="a7790-116">Dit omvat opslagtype, locatie, resource-Id van het opslagaccount waarin de bovenliggende VHD wordt opgeslagen en VHD-URI van de bovenliggende VHD.</span><span class="sxs-lookup"><span data-stu-id="a7790-116">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, and VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="a7790-117">Nieuwe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a7790-117">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="a7790-118">Hiermee maakt u een schijf met de schijfconfiguratie, de naam van de en Resourcegroepnaam als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="a7790-118">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a7790-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7790-119">Next steps</span></span>

[<span data-ttu-id="a7790-120">Een beheerde schijf maken vanuit een momentopname.</span><span class="sxs-lookup"><span data-stu-id="a7790-120">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="a7790-121">Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="a7790-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a7790-122">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a7790-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a7790-123">Voorbeelden van extra virtuele machine PowerShell-script kunnen worden gevonden in de [virtuele machine van Windows Azure-documentatie](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7790-123">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>