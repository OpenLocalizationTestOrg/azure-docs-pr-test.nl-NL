---
title: aaaAzure voorbeeldscript CLI - Hallo licht Stack in een Load-Balanced Virtual Machin implementeren | Microsoft Docs
description: Gebruik een aangepast script extensie toodeploy Hallo licht Stack in de belasting = taakverdeling virtuele-machineschaalset ingesteld op Azure.
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="ace70-103">Hallo licht stack in een taakverdeling virtuele-machineschaalset implementeren</span><span class="sxs-lookup"><span data-stu-id="ace70-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="ace70-104">In dit voorbeeld maakt u een virtuele-machineschaalset en past een uitbreiding die een aangepast script toodeploy Hallo licht stack op elke virtuele machine in de schaalset hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ace70-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="ace70-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="ace70-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="ace70-106">Verbinding maken</span><span class="sxs-lookup"><span data-stu-id="ace70-106">Connect</span></span>

<span data-ttu-id="ace70-107">Gebruik deze code toosee hoe tooconnect tooyour VM's en schaal ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ace70-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ace70-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="ace70-108">Clean up deployment</span></span> 

<span data-ttu-id="ace70-109">Hallo na de opdracht tooremove Hallo-resourcegroep, Hallo schaalset en virtuele machines en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ace70-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ace70-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="ace70-110">Script explanation</span></span>

<span data-ttu-id="ace70-111">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="ace70-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="ace70-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="ace70-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ace70-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="ace70-113">Command</span></span> | <span data-ttu-id="ace70-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ace70-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ace70-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="ace70-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ace70-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ace70-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ace70-117">AZ vmss maken</span><span class="sxs-lookup"><span data-stu-id="ace70-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="ace70-118">Hiermee maakt u een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="ace70-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="ace70-119">AZ network Load Balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="ace70-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="ace70-120">Een eindpunt met gelijke taakverdeling toevoegen</span><span class="sxs-lookup"><span data-stu-id="ace70-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="ace70-121">AZ vmss extensie instellen</span><span class="sxs-lookup"><span data-stu-id="ace70-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="ace70-122">Hallo-extensie die Hallo aangepast script wordt uitgevoerd op de implementatie van een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="ace70-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="ace70-123">AZ vmss update-exemplaren</span><span class="sxs-lookup"><span data-stu-id="ace70-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="ace70-124">Hallo aangepast script uitvoeren op Hallo VM-exemplaren die zijn geïmplementeerd voordat het Hallo-uitbreiding is toegepast toohello schaalset.</span><span class="sxs-lookup"><span data-stu-id="ace70-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="ace70-125">AZ vmss schaal</span><span class="sxs-lookup"><span data-stu-id="ace70-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="ace70-126">Opschalen Hallo scale ingesteld door meer VM-exemplaren toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="ace70-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="ace70-127">Hallo aangepast script wordt uitgevoerd op deze wanneer ze zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ace70-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="ace70-128">lijst met AZ netwerken openbare-ip</span><span class="sxs-lookup"><span data-stu-id="ace70-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="ace70-129">Hallo IP-adressen van virtuele machines die zijn gemaakt door Hallo voorbeeld Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="ace70-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="ace70-130">AZ netwerk lb weergeven</span><span class="sxs-lookup"><span data-stu-id="ace70-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="ace70-131">Hallo frontend en backend poorten die worden gebruikt door Hallo load balancer ophalen.</span><span class="sxs-lookup"><span data-stu-id="ace70-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ace70-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ace70-132">Next steps</span></span>

<span data-ttu-id="ace70-133">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ace70-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ace70-134">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ace70-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
