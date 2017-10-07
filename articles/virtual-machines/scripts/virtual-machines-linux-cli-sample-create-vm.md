---
title: aaaAzure voorbeeldscript CLI - Maak een Linux-VM | Microsoft Docs
description: Azure CLI Script voorbeeld - een virtuele Linux-machine maken
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="dcae8-103">Een volledig geconfigureerde virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="dcae8-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="dcae8-104">Dit script maakt een virtuele Machine van Azure met een virtuele Ubuntu-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="dcae8-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="dcae8-105">Na het uitvoeren van script hello, kunt u toegang tot de Hallo virtuele machine via SSH.</span><span class="sxs-lookup"><span data-stu-id="dcae8-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dcae8-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="dcae8-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dcae8-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="dcae8-107">Clean up deployment</span></span> 

<span data-ttu-id="dcae8-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dcae8-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dcae8-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="dcae8-109">Script explanation</span></span>

<span data-ttu-id="dcae8-110">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="dcae8-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="dcae8-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="dcae8-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dcae8-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="dcae8-112">Command</span></span> | <span data-ttu-id="dcae8-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="dcae8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dcae8-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="dcae8-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dcae8-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="dcae8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dcae8-116">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="dcae8-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="dcae8-117">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="dcae8-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="dcae8-118">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="dcae8-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="dcae8-119">Hiermee maakt een openbaar IP-adres met een statisch IP-adres en een bijbehorende DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="dcae8-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="dcae8-120">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="dcae8-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="dcae8-121">Maakt een netwerkbeveiligingsgroep (NSG), die een beveiligingsgrens tussen Hallo internet en Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="dcae8-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="dcae8-122">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="dcae8-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="dcae8-123">Hiermee maakt u een NSG regel tooallow binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="dcae8-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="dcae8-124">In dit voorbeeld wordt poort 22 voor SSH-verkeer geopend.</span><span class="sxs-lookup"><span data-stu-id="dcae8-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="dcae8-125">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="dcae8-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="dcae8-126">Maakt een virtueel netwerkkaart en toohello virtueel netwerk, subnet en NSG gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="dcae8-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="dcae8-127">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="dcae8-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="dcae8-128">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="dcae8-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="dcae8-129">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="dcae8-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="dcae8-130">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="dcae8-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="dcae8-131">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="dcae8-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcae8-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dcae8-132">Next steps</span></span>

<span data-ttu-id="dcae8-133">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcae8-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dcae8-134">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dcae8-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
