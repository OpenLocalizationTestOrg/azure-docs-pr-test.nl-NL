---
title: Azure CLI Script voorbeeld - een virtuele machine maken met een VHD | Microsoft Docs
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
ms.openlocfilehash: fab65296a552c1839522c5254a868a3dc96227f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="07207-103">Een virtuele machine met een virtuele harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="07207-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="07207-104">In dit voorbeeld maakt een VHD met een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07207-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="07207-105">Het maakt een resourcegroep, een opslagaccount en een container en een virtuele machine wordt gemaakt door het uploaden van de VHD naar de container.</span><span class="sxs-lookup"><span data-stu-id="07207-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span></span>
<span data-ttu-id="07207-106">Vervangt de ssh openbare sleutel met de openbare sleutel zodat u toegang hebt tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07207-106">It replaces the ssh public key with your public key so that you have access to the VM.</span></span>

<span data-ttu-id="07207-107">U moet een opstartbare VHD.</span><span class="sxs-lookup"><span data-stu-id="07207-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="07207-108">U kunt downloaden van de VHD die wordt gebruikt vanuit https://azclisamples.blob.core.windows.net/vhds/sample.vhd of uw eigen VHD gebruiken.</span><span class="sxs-lookup"><span data-stu-id="07207-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="07207-109">Het script wordt gezocht naar `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="07207-109">The script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="07207-110">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="07207-110">Sample script</span></span>

<span data-ttu-id="07207-111">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "virtuele machine met behulp van een VHD maken")]</span><span class="sxs-lookup"><span data-stu-id="07207-111">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="07207-112">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="07207-112">Clean up deployment</span></span> 

<span data-ttu-id="07207-113">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="07207-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="07207-114">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="07207-114">Script explanation</span></span>

<span data-ttu-id="07207-115">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="07207-115">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="07207-116">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="07207-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="07207-117">Opdracht</span><span class="sxs-lookup"><span data-stu-id="07207-117">Command</span></span> | <span data-ttu-id="07207-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="07207-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="07207-119">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="07207-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="07207-120">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="07207-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="07207-121">lijst met opslagaccounts AZ</span><span class="sxs-lookup"><span data-stu-id="07207-121">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="07207-122">Een lijst met storage-accounts</span><span class="sxs-lookup"><span data-stu-id="07207-122">Lists storage accounts</span></span> |
| [<span data-ttu-id="07207-123">AZ opslag Controleer accountnaam</span><span class="sxs-lookup"><span data-stu-id="07207-123">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="07207-124">Controleert of de naam van een account geldig is en nog niet bestaat</span><span class="sxs-lookup"><span data-stu-id="07207-124">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="07207-125">lijst met opslagaccounts die sleutels AZ</span><span class="sxs-lookup"><span data-stu-id="07207-125">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="07207-126">Een lijst met sleutels voor de storage-accounts</span><span class="sxs-lookup"><span data-stu-id="07207-126">Lists keys for the storage accounts</span></span> |
| [<span data-ttu-id="07207-127">AZ storage-blob bestaat</span><span class="sxs-lookup"><span data-stu-id="07207-127">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="07207-128">Controleert of de blob bestaat</span><span class="sxs-lookup"><span data-stu-id="07207-128">Checks whether the blob exists</span></span> |
| [<span data-ttu-id="07207-129">AZ storage-container maken</span><span class="sxs-lookup"><span data-stu-id="07207-129">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="07207-130">Maakt een container in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="07207-130">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="07207-131">uploaden van blob storage AZ</span><span class="sxs-lookup"><span data-stu-id="07207-131">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="07207-132">Maakt een blob in de container door de VHD te uploaden.</span><span class="sxs-lookup"><span data-stu-id="07207-132">Creates a blob in the container by uploading the VHD.</span></span> |
| [<span data-ttu-id="07207-133">AZ vm lijst</span><span class="sxs-lookup"><span data-stu-id="07207-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="07207-134">Gebruikt met `--query` controleren of de naam van de VM in gebruik is.</span><span class="sxs-lookup"><span data-stu-id="07207-134">Used with `--query` check whether the VM name is in use.</span></span> | 
| [<span data-ttu-id="07207-135">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="07207-135">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="07207-136">Maakt de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="07207-136">Creates the virtual machines.</span></span> |
| [<span data-ttu-id="07207-137">AZ vm toegang set-linux-gebruikers</span><span class="sxs-lookup"><span data-stu-id="07207-137">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="07207-138">Hiermee stelt u de SSH-sleutel in de huidige om gebruikerstoegang te verlenen aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07207-138">Resets the SSH key to give the current user access to the VM.</span></span> |
| [<span data-ttu-id="07207-139">AZ vm lijst-ip-adressen</span><span class="sxs-lookup"><span data-stu-id="07207-139">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="07207-140">Hiermee haalt u het IP-adres van de virtuele machine die is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="07207-140">Gets the IP address of the VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="07207-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07207-141">Next steps</span></span>

<span data-ttu-id="07207-142">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07207-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="07207-143">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="07207-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
