---
title: een beheerde schijf aaaAzure voorbeeldscript CLI - maken van een VHD-bestand in een opslagaccount in Hallo hetzelfde abonnement | Microsoft Docs
description: Azure CLI-Script steekproef - maken van een beheerde schijf van een VHD-bestand in een opslagaccount in Hallo hetzelfde abonnement
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="c9938-103">Maak een beheerde schijf van een VHD-bestand in een opslagaccount in Hallo hetzelfde abonnement met CLI</span><span class="sxs-lookup"><span data-stu-id="c9938-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="c9938-104">Dit script maakt een beheerde schijf van een VHD-bestand in een opslagaccount in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="c9938-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="c9938-105">Gebruik dit script tooimport een gespecialiseerde (geen gegeneraliseerde/Sysprep voorbereide) VHD toomanaged OS schijf toocreate een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c9938-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="c9938-106">Of tooimport een gegevensschijf VHD toomanaged gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c9938-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c9938-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c9938-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="c9938-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c9938-108">Script explanation</span></span>

<span data-ttu-id="c9938-109">Dit script gebruikt na opdrachten toocreate een beheerde schijf vanaf een VHD.</span><span class="sxs-lookup"><span data-stu-id="c9938-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="c9938-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="c9938-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c9938-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c9938-111">Command</span></span> | <span data-ttu-id="c9938-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c9938-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9938-113">AZ schijf maken</span><span class="sxs-lookup"><span data-stu-id="c9938-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="c9938-114">Maakt een beheerde schijf met de URI van een VHD in een opslagaccount in Hallo hetzelfde abonnement</span><span class="sxs-lookup"><span data-stu-id="c9938-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9938-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9938-115">Next steps</span></span>

[<span data-ttu-id="c9938-116">Een virtuele machine maken door het koppelen van een beheerde schijf als besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="c9938-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="c9938-117">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9938-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c9938-118">Extra virtuele machine en beheerd schijven CLI scriptvoorbeelden vindt u in Hallo [Azure Linux VM documentatie](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9938-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
