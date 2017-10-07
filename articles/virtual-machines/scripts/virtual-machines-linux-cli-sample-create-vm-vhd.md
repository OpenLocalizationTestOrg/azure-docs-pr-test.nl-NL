---
title: aaaAzure voorbeeldscript CLI - een virtuele machine maken met een VHD | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een virtuele machine maken met een virtuele harde schijf.'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="2359d-103">Een virtuele machine met een virtuele harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="2359d-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="2359d-104">In dit voorbeeld maakt een VHD met een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2359d-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="2359d-105">Het maakt een resourcegroep, een opslagaccount en een container en een virtuele machine wordt gemaakt door het uploaden van Hallo VHD toohello container.</span><span class="sxs-lookup"><span data-stu-id="2359d-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="2359d-106">Vervangt Hallo ssh openbare sleutel met de openbare sleutel, zodat u toegang toohello VM hebt.</span><span class="sxs-lookup"><span data-stu-id="2359d-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="2359d-107">U moet een opstartbare VHD.</span><span class="sxs-lookup"><span data-stu-id="2359d-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="2359d-108">U kunt downloaden Hallo VHD die wordt gebruikt vanuit https://azclisamples.blob.core.windows.net/vhds/sample.vhd of uw eigen VHD gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2359d-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="2359d-109">Hallo script zoekt `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="2359d-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2359d-110">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="2359d-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2359d-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="2359d-111">Clean up deployment</span></span> 

<span data-ttu-id="2359d-112">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2359d-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="2359d-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2359d-113">Script explanation</span></span>

<span data-ttu-id="2359d-114">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="2359d-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="2359d-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="2359d-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2359d-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2359d-116">Command</span></span> | <span data-ttu-id="2359d-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2359d-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2359d-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="2359d-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2359d-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2359d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2359d-120">lijst met opslagaccounts AZ</span><span class="sxs-lookup"><span data-stu-id="2359d-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="2359d-121">Een lijst met storage-accounts</span><span class="sxs-lookup"><span data-stu-id="2359d-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="2359d-122">AZ opslag Controleer accountnaam</span><span class="sxs-lookup"><span data-stu-id="2359d-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="2359d-123">Controleert of de naam van een account geldig is en nog niet bestaat</span><span class="sxs-lookup"><span data-stu-id="2359d-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="2359d-124">lijst met opslagaccounts die sleutels AZ</span><span class="sxs-lookup"><span data-stu-id="2359d-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="2359d-125">Een lijst met sleutels voor opslagaccounts Hallo</span><span class="sxs-lookup"><span data-stu-id="2359d-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="2359d-126">AZ storage-blob bestaat</span><span class="sxs-lookup"><span data-stu-id="2359d-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="2359d-127">Controleert of Hallo blob bestaat</span><span class="sxs-lookup"><span data-stu-id="2359d-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="2359d-128">AZ storage-container maken</span><span class="sxs-lookup"><span data-stu-id="2359d-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="2359d-129">Maakt een container in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2359d-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="2359d-130">uploaden van blob storage AZ</span><span class="sxs-lookup"><span data-stu-id="2359d-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="2359d-131">Hiermee maakt een blob in Hallo-container door uploaden Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="2359d-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="2359d-132">AZ vm lijst</span><span class="sxs-lookup"><span data-stu-id="2359d-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="2359d-133">Gebruikt met `--query` controleren of de naam van de VM Hallo in gebruik is.</span><span class="sxs-lookup"><span data-stu-id="2359d-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="2359d-134">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="2359d-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="2359d-135">Hallo virtuele machines maakt.</span><span class="sxs-lookup"><span data-stu-id="2359d-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="2359d-136">AZ vm toegang set-linux-gebruikers</span><span class="sxs-lookup"><span data-stu-id="2359d-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="2359d-137">Hiermee stelt u Hallo SSH sleutel toogive Hallo huidige gebruiker toegang toohello VM.</span><span class="sxs-lookup"><span data-stu-id="2359d-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="2359d-138">AZ vm lijst-ip-adressen</span><span class="sxs-lookup"><span data-stu-id="2359d-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="2359d-139">Hiermee haalt u Hallo IP-adres van Hallo VM die is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2359d-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2359d-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2359d-140">Next steps</span></span>

<span data-ttu-id="2359d-141">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2359d-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2359d-142">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2359d-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
