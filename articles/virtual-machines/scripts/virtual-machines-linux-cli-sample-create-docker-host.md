---
title: aaaAzure voorbeeldscript CLI - Docker host maken | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: Maak een Docker-host'
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="b33f9-103">Een virtuele machine maken met Docker</span><span class="sxs-lookup"><span data-stu-id="b33f9-103">Create a VM with Docker</span></span>

<span data-ttu-id="b33f9-104">Dit script maakt een virtuele machine met Docker ingeschakeld en begint met een Docker-container NGINX uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b33f9-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="b33f9-105">U kunt na het uitvoeren van script Hallo Hallo NGINX-webserver openen via Hallo FQDN-naam van de virtuele machine van Azure Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33f9-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b33f9-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="b33f9-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b33f9-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="b33f9-107">Clean up deployment</span></span> 

<span data-ttu-id="b33f9-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b33f9-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b33f9-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="b33f9-109">Script explanation</span></span>

<span data-ttu-id="b33f9-110">Dit script maakt gebruik van Hallo opdrachten toocreate Hallo implementatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="b33f9-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="b33f9-111">Elk item in de tabel Hallo koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="b33f9-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b33f9-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="b33f9-112">Command</span></span> | <span data-ttu-id="b33f9-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b33f9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b33f9-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="b33f9-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b33f9-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b33f9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b33f9-116">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="b33f9-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="b33f9-117">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en netwerkbeveiligingsgroep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="b33f9-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="b33f9-118">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="b33f9-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="b33f9-119">AZ vm open-poort</span><span class="sxs-lookup"><span data-stu-id="b33f9-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="b33f9-120">Hiermee maakt u een netwerk beveiliging groep regel tooallow binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="b33f9-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="b33f9-121">In dit voorbeeld wordt is poort 80 geopend voor HTTP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="b33f9-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="b33f9-122">Azure vm-extensie instellen</span><span class="sxs-lookup"><span data-stu-id="b33f9-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b33f9-123">Wordt toegevoegd en wordt een virtuele machine extensie tooa VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b33f9-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="b33f9-124">In dit voorbeeld is Hallo Docker VM-extensie gebruikte tooconfigure een Docker-host.</span><span class="sxs-lookup"><span data-stu-id="b33f9-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="b33f9-125">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="b33f9-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b33f9-126">Hiermee verwijdert u een resourcegroep, met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="b33f9-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b33f9-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b33f9-127">Next steps</span></span>

<span data-ttu-id="b33f9-128">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b33f9-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b33f9-129">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b33f9-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
