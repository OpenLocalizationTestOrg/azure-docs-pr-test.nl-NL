---
title: aaaAzure voorbeeldscript CLI - Maak een virtuele machine van Windows Server 2016 met IIS gebruik van DSC | Microsoft Docs
description: Azure CLI-Script steekproef - maken van een virtuele machine van Windows Server 2016 met IIS gebruik van DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="0f60a-103">Een virtuele machine maken met gebruik van DSC IIS</span><span class="sxs-lookup"><span data-stu-id="0f60a-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="0f60a-104">Dit script wordt een virtuele machine gemaakt en gebruikt hello Azure virtuele Machine DSC aangepast script extensie tooinstall en IIS te configureren.</span><span class="sxs-lookup"><span data-stu-id="0f60a-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0f60a-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="0f60a-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0f60a-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="0f60a-106">Clean up deployment</span></span> 

<span data-ttu-id="0f60a-107">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0f60a-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="0f60a-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="0f60a-108">Script explanation</span></span>

<span data-ttu-id="0f60a-109">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="0f60a-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="0f60a-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="0f60a-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0f60a-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="0f60a-111">Command</span></span> | <span data-ttu-id="0f60a-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0f60a-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0f60a-113">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="0f60a-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0f60a-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0f60a-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0f60a-115">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="0f60a-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="0f60a-116">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="0f60a-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="0f60a-117">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="0f60a-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="0f60a-118">AZ vm-extensie instellen</span><span class="sxs-lookup"><span data-stu-id="0f60a-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="0f60a-119">Hallo aangepaste Scriptextensie toohello virtuele machine die een script tooinstall IIS roept toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0f60a-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="0f60a-120">AZ vm open-poort</span><span class="sxs-lookup"><span data-stu-id="0f60a-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="0f60a-121">Hiermee maakt u een netwerk beveiliging groep regel tooallow binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="0f60a-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="0f60a-122">In dit voorbeeld wordt is poort 80 geopend voor HTTP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="0f60a-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="0f60a-123">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="0f60a-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="0f60a-124">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="0f60a-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0f60a-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0f60a-125">Next steps</span></span>

<span data-ttu-id="0f60a-126">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0f60a-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0f60a-127">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f60a-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
