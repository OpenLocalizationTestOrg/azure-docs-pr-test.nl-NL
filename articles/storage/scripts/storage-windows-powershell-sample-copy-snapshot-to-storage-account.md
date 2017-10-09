---
title: "PowerShell-voorbeeldscript - momentopname exporteren/kopiëren als VHD tooa storage-account in andere regio aaaAzure | Microsoft Docs"
description: "Azure PowerShell-Script voorbeeld - momentopname exporteren/kopiëren als VHD tooa opslagaccount in dezelfde andere regio"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="0a819-103">Export/exemplaar beheerde momentopnamen als VHD tooa storage-account in andere regio met PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a819-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="0a819-104">Dit script exporteert u een beheerde momentopname tooa storage-account in andere regio.</span><span class="sxs-lookup"><span data-stu-id="0a819-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="0a819-105">Deze genereert eerst Hallo SAS-URI van de momentopname Hallo en gebruikt vervolgens toocopy het tooa storage-account in andere regio.</span><span class="sxs-lookup"><span data-stu-id="0a819-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="0a819-106">Gebruik deze back-up toomaintain script beheerde schijven in andere regio voor herstel na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="0a819-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0a819-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="0a819-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="0a819-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="0a819-108">Script explanation</span></span>

<span data-ttu-id="0a819-109">Dit script maakt gebruik van opdrachten toogenerate na SAS-URI voor een beheerde momentopnamen en kopieën op Hallo momentopname tooa storage-account met behulp van SAS-URI.</span><span class="sxs-lookup"><span data-stu-id="0a819-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="0a819-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="0a819-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0a819-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="0a819-111">Command</span></span> | <span data-ttu-id="0a819-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0a819-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0a819-113">Verleen AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="0a819-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="0a819-114">De SAS-URI voor een momentopname die is gebruikt toocopy genereert het tooa storage-account.</span><span class="sxs-lookup"><span data-stu-id="0a819-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="0a819-115">Nieuwe AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="0a819-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="0a819-116">Maakt een storage account context Hallo-accountnaam en-sleutel.</span><span class="sxs-lookup"><span data-stu-id="0a819-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="0a819-117">Deze context kan worden gebruikt tooperform lezen/schrijven-bewerkingen op Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="0a819-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="0a819-118">Start AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="0a819-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="0a819-119">Kopieën Hallo onderliggende VHD van een momentopname tooa storage-account</span><span class="sxs-lookup"><span data-stu-id="0a819-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0a819-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a819-120">Next steps</span></span>

[<span data-ttu-id="0a819-121">Een beheerde schijf vanaf een VHD maken</span><span class="sxs-lookup"><span data-stu-id="0a819-121">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="0a819-122">Een virtuele machine maken van een beheerde schijf</span><span class="sxs-lookup"><span data-stu-id="0a819-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="0a819-123">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a819-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0a819-124">Voorbeelden van extra virtuele machine PowerShell-script kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0a819-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
