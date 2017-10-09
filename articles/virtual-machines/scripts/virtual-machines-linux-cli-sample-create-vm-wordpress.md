---
title: aaaAzure voorbeeldscript CLI - Maak een Linux-VM met WordPress | Microsoft Docs
description: Azure CLI Script voorbeeld - een virtuele Linux-machine maken met WordPress
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
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="fbff2-103">Een virtuele machine maken met WordPress</span><span class="sxs-lookup"><span data-stu-id="fbff2-103">Create a VM with WordPress</span></span>

<span data-ttu-id="fbff2-104">Dit script wordt een virtuele machine gemaakt en gebruikt vervolgens hello Azure virtuele Machine aangepast script extensie tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="fbff2-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="fbff2-105">Na het Hallo-script wordt uitgevoerd, u toegang hebt tot Hallo WordPress-site voor configuration op `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="fbff2-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fbff2-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="fbff2-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fbff2-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="fbff2-107">Clean up deployment</span></span> 

<span data-ttu-id="fbff2-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fbff2-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fbff2-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="fbff2-109">Script explanation</span></span>

<span data-ttu-id="fbff2-110">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="fbff2-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="fbff2-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="fbff2-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fbff2-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="fbff2-112">Command</span></span> | <span data-ttu-id="fbff2-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fbff2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fbff2-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="fbff2-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fbff2-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fbff2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fbff2-116">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="fbff2-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="fbff2-117">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="fbff2-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="fbff2-118">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="fbff2-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="fbff2-119">AZ vm open-poort</span><span class="sxs-lookup"><span data-stu-id="fbff2-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="fbff2-120">Hiermee maakt u een netwerk beveiliging groep regel tooallow binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="fbff2-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="fbff2-121">In dit voorbeeld wordt is poort 80 geopend voor HTTP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="fbff2-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="fbff2-122">AZ vm-extensie instellen</span><span class="sxs-lookup"><span data-stu-id="fbff2-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="fbff2-123">Hallo aangepaste Scriptextensie toohello virtuele machine, die een script tooinstall WordPress roept toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fbff2-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="fbff2-124">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="fbff2-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fbff2-125">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="fbff2-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fbff2-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fbff2-126">Next steps</span></span>

<span data-ttu-id="fbff2-127">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbff2-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fbff2-128">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbff2-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
