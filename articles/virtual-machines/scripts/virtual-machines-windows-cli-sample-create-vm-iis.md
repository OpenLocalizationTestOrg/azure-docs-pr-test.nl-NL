---
title: Azure CLI-voorbeeldscript - Installeer IIS | Microsoft Docs
description: Azure CLI-voorbeeldscript - Installeer IIS
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 426418c01b23845372443af5b8f4e826fb321f7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="01fa1-103">Snel een virtuele machine maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="01fa1-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="01fa1-104">Dit script maakt een Azure-virtuele Machine met Windows Server 2016 en de aangepaste Scriptextensie voor Azure virtuele Machine gebruikt voor het installeren van IIS.</span><span class="sxs-lookup"><span data-stu-id="01fa1-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses the Azure Virtual Machine Custom Script Extension to install IIS.</span></span> <span data-ttu-id="01fa1-105">Nadat het script is uitgevoerd, kunt u toegang tot de standaardwebsite van IIS op het openbare IP-adres van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="01fa1-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="01fa1-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="01fa1-106">Sample script</span></span>

<span data-ttu-id="01fa1-107">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "snelle VM maken")]</span><span class="sxs-lookup"><span data-stu-id="01fa1-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="01fa1-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="01fa1-108">Clean up deployment</span></span> 

<span data-ttu-id="01fa1-109">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="01fa1-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="01fa1-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="01fa1-110">Script explanation</span></span>

<span data-ttu-id="01fa1-111">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="01fa1-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="01fa1-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="01fa1-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="01fa1-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="01fa1-113">Command</span></span> | <span data-ttu-id="01fa1-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="01fa1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01fa1-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="01fa1-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="01fa1-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="01fa1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01fa1-117">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="01fa1-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="01fa1-118">De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en netwerkbeveiligingsgroep is verbonden.</span><span class="sxs-lookup"><span data-stu-id="01fa1-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="01fa1-119">Deze opdracht geeft ook aan de installatiekopie van de virtuele machine om te worden gebruikt en administratieve referenties.</span><span class="sxs-lookup"><span data-stu-id="01fa1-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="01fa1-120">AZ vm open-poort</span><span class="sxs-lookup"><span data-stu-id="01fa1-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="01fa1-121">Maakt een groep van de netwerkbeveiligingsregel dat binnenkomend verkeer toegestaan.</span><span class="sxs-lookup"><span data-stu-id="01fa1-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="01fa1-122">In dit voorbeeld wordt is poort 80 geopend voor HTTP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="01fa1-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="01fa1-123">Azure vm-extensie instellen</span><span class="sxs-lookup"><span data-stu-id="01fa1-123">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="01fa1-124">Wordt toegevoegd en wordt de extensie van een virtuele machine naar een virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="01fa1-124">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="01fa1-125">In dit voorbeeld wordt de extensie voor aangepaste scripts worden gebruikt om IIS te installeren.</span><span class="sxs-lookup"><span data-stu-id="01fa1-125">In this sample, the custom script extension is used to install IIS.</span></span>|
| [<span data-ttu-id="01fa1-126">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="01fa1-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="01fa1-127">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="01fa1-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="01fa1-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01fa1-128">Next steps</span></span>

<span data-ttu-id="01fa1-129">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01fa1-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="01fa1-130">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01fa1-130">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
