---
title: 'Azure CLI-Script voorbeeld: Maak een Docker-host | Microsoft Docs'
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
ms.openlocfilehash: e8704824dec66d724f2d30dab4d6bdf019c6b206
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="31cb5-103">Een virtuele machine maken met Docker</span><span class="sxs-lookup"><span data-stu-id="31cb5-103">Create a VM with Docker</span></span>

<span data-ttu-id="31cb5-104">Dit script maakt een virtuele machine met Docker ingeschakeld en begint met een Docker-container NGINX uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="31cb5-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="31cb5-105">Nadat het script is uitgevoerd, kunt u het NGINX-webserver openen via de FQDN van de virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="31cb5-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="31cb5-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="31cb5-106">Sample script</span></span>

<span data-ttu-id="31cb5-107">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker-Host")]</span><span class="sxs-lookup"><span data-stu-id="31cb5-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="31cb5-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="31cb5-108">Clean up deployment</span></span> 

<span data-ttu-id="31cb5-109">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="31cb5-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="31cb5-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="31cb5-110">Script explanation</span></span>

<span data-ttu-id="31cb5-111">Dit script maakt gebruik van de volgende opdrachten om de implementatie te maken.</span><span class="sxs-lookup"><span data-stu-id="31cb5-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="31cb5-112">Elk item in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="31cb5-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="31cb5-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="31cb5-113">Command</span></span> | <span data-ttu-id="31cb5-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="31cb5-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="31cb5-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="31cb5-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="31cb5-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="31cb5-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="31cb5-117">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="31cb5-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="31cb5-118">De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en netwerkbeveiligingsgroep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="31cb5-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="31cb5-119">Met deze opdracht geeft ook de afbeelding van de virtuele machine moet worden gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="31cb5-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="31cb5-120">AZ vm open-poort</span><span class="sxs-lookup"><span data-stu-id="31cb5-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="31cb5-121">Maakt een groep van de netwerkbeveiligingsregel dat binnenkomend verkeer toegestaan.</span><span class="sxs-lookup"><span data-stu-id="31cb5-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="31cb5-122">In dit voorbeeld wordt is poort 80 geopend voor HTTP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="31cb5-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="31cb5-123">Azure vm-extensie instellen</span><span class="sxs-lookup"><span data-stu-id="31cb5-123">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="31cb5-124">Wordt toegevoegd en wordt de extensie van een virtuele machine naar een virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="31cb5-124">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="31cb5-125">In dit voorbeeld wordt de Docker-VM-extensie gebruikt voor het configureren van een Docker-host.</span><span class="sxs-lookup"><span data-stu-id="31cb5-125">In this sample, the Docker VM extension is used to configure a Docker host.</span></span>|
| [<span data-ttu-id="31cb5-126">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="31cb5-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="31cb5-127">Hiermee verwijdert u een resourcegroep, met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="31cb5-127">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="31cb5-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31cb5-128">Next steps</span></span>

<span data-ttu-id="31cb5-129">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="31cb5-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="31cb5-130">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31cb5-130">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
