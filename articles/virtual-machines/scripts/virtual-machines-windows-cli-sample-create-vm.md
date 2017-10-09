---
title: aaaAzure voorbeeldscript CLI - Maak een virtuele machine van Windows Server | Microsoft Docs
description: Azure CLI Script voorbeeld - een WindowsServer-machine maken
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="3dd9b-103">Een virtuele machine maken met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3dd9b-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="3dd9b-104">Dit script maakt een Azure-virtuele Machine met Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="3dd9b-105">Na het uitvoeren van script hello, kunt u Hallo virtuele machine via Extern bureaublad-verbinding openen.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3dd9b-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="3dd9b-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3dd9b-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="3dd9b-107">Clean up deployment</span></span> 

<span data-ttu-id="3dd9b-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3dd9b-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3dd9b-109">Script explanation</span></span>

<span data-ttu-id="3dd9b-110">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="3dd9b-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3dd9b-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3dd9b-112">Command</span></span> | <span data-ttu-id="3dd9b-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3dd9b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3dd9b-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="3dd9b-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3dd9b-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3dd9b-116">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="3dd9b-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="3dd9b-117">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="3dd9b-118">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="3dd9b-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="3dd9b-119">Hiermee maakt een openbaar IP-adres met een statisch IP-adres en een bijbehorende DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="3dd9b-120">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="3dd9b-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="3dd9b-121">Maakt een netwerkbeveiligingsgroep (NSG), die een beveiligingsgrens tussen Hallo internet en Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="3dd9b-122">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="3dd9b-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="3dd9b-123">Maakt een virtueel netwerkkaart en toohello virtueel netwerk, subnet en NSG gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="3dd9b-124">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="3dd9b-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="3dd9b-125">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="3dd9b-126">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="3dd9b-127">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="3dd9b-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3dd9b-128">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="3dd9b-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3dd9b-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3dd9b-129">Next steps</span></span>

<span data-ttu-id="3dd9b-130">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3dd9b-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3dd9b-131">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3dd9b-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
