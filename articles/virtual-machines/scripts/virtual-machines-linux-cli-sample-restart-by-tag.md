---
title: aaaAzure voorbeeldscript CLI - virtuele machines opnieuw opstarten | Microsoft Docs
description: Azure CLI-voorbeeldscript - virtuele machines opnieuw starten door de tag en -ID
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="32eb6-103">Opnieuw opstarten van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="32eb6-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="32eb6-104">Dit voorbeeld toont een aantal manieren tooget sommige virtuele machines en deze opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="32eb6-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="32eb6-105">Hallo eerst opnieuw wordt opgestart alle Hallo VM's in de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="32eb6-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="32eb6-106">Hallo tweede opgehaald Hallo gelabeld virtuele machines met `az resouce list` filtert toohello resources die virtuele machines en deze VMs opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="32eb6-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="32eb6-107">Dit voorbeeld werkt in een Bash-shell.</span><span class="sxs-lookup"><span data-stu-id="32eb6-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="32eb6-108">Zie voor opties op Azure CLI-scripts die worden uitgevoerd op Windows-client [hello Azure CLI uitvoeren in Windows](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="32eb6-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="32eb6-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="32eb6-109">Sample script</span></span>

<span data-ttu-id="32eb6-110">Hallo voorbeeld heeft drie scripts.</span><span class="sxs-lookup"><span data-stu-id="32eb6-110">hello sample has three scripts.</span></span>
<span data-ttu-id="32eb6-111">Hallo eerst een bepaalde Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="32eb6-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="32eb6-112">Hallo Nee-wait-optie wordt gebruikt zodat Hallo-opdracht geretourneerd zonder te wachten op elke virtuele machine toobe ingericht.</span><span class="sxs-lookup"><span data-stu-id="32eb6-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="32eb6-113">Hallo wacht tweede Hallo VMs toobe volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="32eb6-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="32eb6-114">Hallo derde script start opnieuw alle Hallo VM's die zijn ingericht en vervolgens alleen Hallo label voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="32eb6-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="32eb6-115">Hallo virtuele machines inrichten</span><span class="sxs-lookup"><span data-stu-id="32eb6-115">Provision hello VMs</span></span>

<span data-ttu-id="32eb6-116">Dit script maakt een resourcegroep en maakt vervolgens het toorestart van drie virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="32eb6-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="32eb6-117">Twee van deze zijn gelabeld.</span><span class="sxs-lookup"><span data-stu-id="32eb6-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="32eb6-118">Wait</span><span class="sxs-lookup"><span data-stu-id="32eb6-118">Wait</span></span>

<span data-ttu-id="32eb6-119">Dit script wordt gecontroleerd op Hallo Inrichtingsstatus elke 20 seconden totdat alle drie virtuele machines zijn ingericht, of een van beide tooprovision is mislukt.</span><span class="sxs-lookup"><span data-stu-id="32eb6-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="32eb6-120">Hallo virtuele machines opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="32eb6-120">Restart hello VMs</span></span>

<span data-ttu-id="32eb6-121">Dit script in de resourcegroep Hallo alle Hallo VM opnieuw wordt opgestart en het zojuist Hallo gelabeld virtuele machines opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="32eb6-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="32eb6-122">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="32eb6-122">Clean up deployment</span></span> 

<span data-ttu-id="32eb6-123">Na het uitvoeren van het voorbeeldscript Hallo mag Hallo opdracht volgende gebruikte tooremove Hallo resourcegroepen, virtuele machines en alle gerelateerde bronnen.</span><span class="sxs-lookup"><span data-stu-id="32eb6-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="32eb6-124">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="32eb6-124">Script explanation</span></span>

<span data-ttu-id="32eb6-125">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="32eb6-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="32eb6-126">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="32eb6-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="32eb6-127">Opdracht</span><span class="sxs-lookup"><span data-stu-id="32eb6-127">Command</span></span> | <span data-ttu-id="32eb6-128">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="32eb6-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="32eb6-129">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="32eb6-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="32eb6-130">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="32eb6-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="32eb6-131">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="32eb6-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="32eb6-132">Hallo virtuele machines maakt.</span><span class="sxs-lookup"><span data-stu-id="32eb6-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="32eb6-133">AZ vm lijst</span><span class="sxs-lookup"><span data-stu-id="32eb6-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="32eb6-134">Gebruikt met `--query` tooensure Hallo virtuele machines zijn ingericht voordat u ze opnieuw start en vervolgens tooget Hallo-id's van Hallo VMs toorestart ze.</span><span class="sxs-lookup"><span data-stu-id="32eb6-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="32eb6-135">lijst met resources AZ</span><span class="sxs-lookup"><span data-stu-id="32eb6-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="32eb6-136">Gebruikt met `--query` tooget Hallo-id's van Hallo virtuele machines met behulp van Hallo-tag.</span><span class="sxs-lookup"><span data-stu-id="32eb6-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="32eb6-137">AZ vm opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="32eb6-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="32eb6-138">Hallo virtuele machines opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="32eb6-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="32eb6-139">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="32eb6-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="32eb6-140">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="32eb6-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="32eb6-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32eb6-141">Next steps</span></span>

<span data-ttu-id="32eb6-142">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="32eb6-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="32eb6-143">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32eb6-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
