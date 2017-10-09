---
title: aaaAzure voorbeeldscript CLI - maakt een Windows Server 2016-VM met OMS bewaking | Microsoft Docs
description: Azure CLI-Script steekproef - maken van een virtuele machine van Windows Server 2016 met OMS bewaking
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
ms.openlocfilehash: 4f070430ccc5d5402ed4a80ead3b78eff25dcd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="9ef78-103">Monitor voor een virtuele machine bij Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="9ef78-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="9ef78-104">Dit script maakt een virtuele Machine van Azure, Hallo Operations Management Suite (OMS)-agent geïnstalleerd en schrijft Hallo-systeem met een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="9ef78-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="9ef78-105">Zodra het Hallo-script is uitgevoerd, is de optie Hallo virtuele machine zijn zichtbaar in Hallo OMS-console.</span><span class="sxs-lookup"><span data-stu-id="9ef78-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9ef78-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9ef78-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9ef78-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="9ef78-107">Clean up deployment</span></span> 

<span data-ttu-id="9ef78-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ef78-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9ef78-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9ef78-109">Script explanation</span></span>

<span data-ttu-id="9ef78-110">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep of virtuele machine te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="9ef78-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9ef78-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="9ef78-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9ef78-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9ef78-112">Command</span></span> | <span data-ttu-id="9ef78-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9ef78-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9ef78-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="9ef78-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9ef78-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9ef78-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9ef78-116">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="9ef78-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9ef78-117">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="9ef78-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="9ef78-118">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="9ef78-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9ef78-119">Azure vm-extensie instellen</span><span class="sxs-lookup"><span data-stu-id="9ef78-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9ef78-120">Een VM-extensie uitgevoerd op basis van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9ef78-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="9ef78-121">In dit geval Hallo Operations Management Suite-agentextensie gebruikte tooinstall Hallo OMS-agent is en inschrijven Hallo VM in een OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="9ef78-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="9ef78-122">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="9ef78-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9ef78-123">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="9ef78-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9ef78-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ef78-124">Next steps</span></span>

<span data-ttu-id="9ef78-125">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9ef78-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9ef78-126">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ef78-126">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
