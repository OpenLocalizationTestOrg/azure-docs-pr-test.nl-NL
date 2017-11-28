---
title: "aaaAzure voorbeeldscript CLI - momentopname exporteren/kopiëren als VHD tooa storage-account in andere regio | Microsoft Docs"
description: "Azure CLI-voorbeeldscript - momentopname exporteren/kopiëren als VHD tooa opslagaccount in dezelfde of een ander abonnement"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="1da10-103">Export/exemplaar beheerde momentopnamen als VHD tooa storage-account in andere regio met CLI</span><span class="sxs-lookup"><span data-stu-id="1da10-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="1da10-104">Dit script exporteert u een beheerde momentopname tooa storage-account in andere regio.</span><span class="sxs-lookup"><span data-stu-id="1da10-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="1da10-105">Deze genereert eerst Hallo SAS-URI van de momentopname Hallo en gebruikt vervolgens toocopy het tooa storage-account in andere regio.</span><span class="sxs-lookup"><span data-stu-id="1da10-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="1da10-106">Gebruik deze back-up toomaintain script beheerde schijven in andere regio voor herstel na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="1da10-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1da10-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="1da10-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="1da10-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="1da10-108">Script explanation</span></span>

<span data-ttu-id="1da10-109">Dit script maakt gebruik van opdrachten toogenerate na SAS-URI voor een beheerde momentopnamen en kopieën op Hallo momentopname tooa storage-account met behulp van SAS-URI.</span><span class="sxs-lookup"><span data-stu-id="1da10-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="1da10-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="1da10-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1da10-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="1da10-111">Command</span></span> | <span data-ttu-id="1da10-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1da10-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1da10-113">AZ momentopname toegang verlenen</span><span class="sxs-lookup"><span data-stu-id="1da10-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="1da10-114">Genereert alleen-lezen SA's dat is gebruikt toocopy onderliggende VHD-bestand tooa storage-account of download deze tooon-premises</span><span class="sxs-lookup"><span data-stu-id="1da10-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="1da10-115">start AZ storage-blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="1da10-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="1da10-116">Een blob asynchroon opgehaald uit één storage account tooanother</span><span class="sxs-lookup"><span data-stu-id="1da10-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1da10-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1da10-117">Next steps</span></span>

[<span data-ttu-id="1da10-118">Een beheerde schijf vanaf een VHD maken</span><span class="sxs-lookup"><span data-stu-id="1da10-118">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="1da10-119">Een virtuele machine maken van een beheerde schijf</span><span class="sxs-lookup"><span data-stu-id="1da10-119">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="1da10-120">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1da10-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1da10-121">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1da10-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
