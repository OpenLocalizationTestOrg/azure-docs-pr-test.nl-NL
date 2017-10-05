---
title: Azure CLI-Script steekproef - maken van een virtuele machine van Windows Server 2016 met IIS gebruik van DSC | Microsoft Docs
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
ms.openlocfilehash: 1f605c0260fcaea29851d76c90ba0b287bec5ae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="188af-103">Een virtuele machine maken met gebruik van DSC IIS</span><span class="sxs-lookup"><span data-stu-id="188af-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="188af-104">Dit script wordt een virtuele machine gemaakt en gebruikt de Azure virtuele Machine DSC-extensie voor aangepaste scripts voor IIS installeren en configureren.</span><span class="sxs-lookup"><span data-stu-id="188af-104">This script creates a virtual machine, and uses the Azure Virtual Machine DSC custom script extension to install and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="188af-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="188af-105">Sample script</span></span>

<span data-ttu-id="188af-106">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "snelle VM maken")]</span><span class="sxs-lookup"><span data-stu-id="188af-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="188af-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="188af-107">Clean up deployment</span></span> 

<span data-ttu-id="188af-108">Voer de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="188af-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="188af-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="188af-109">Script explanation</span></span>

<span data-ttu-id="188af-110">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, virtuele machine en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="188af-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="188af-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="188af-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="188af-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="188af-112">Command</span></span> | <span data-ttu-id="188af-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="188af-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="188af-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="188af-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="188af-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="188af-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="188af-116">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="188af-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="188af-117">De virtuele machine maakt en met de netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="188af-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="188af-118">Met deze opdracht geeft ook de afbeelding van de virtuele machine moet worden gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="188af-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="188af-119">AZ vm-extensie instellen</span><span class="sxs-lookup"><span data-stu-id="188af-119">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="188af-120">De aangepaste Scriptextensie toevoegen aan de virtuele machine die wordt aangeroepen een script om IIS te installeren.</span><span class="sxs-lookup"><span data-stu-id="188af-120">Add the Custom Script Extension to the virtual machine which invokes a script to install IIS.</span></span> |
| [<span data-ttu-id="188af-121">AZ vm open-poort</span><span class="sxs-lookup"><span data-stu-id="188af-121">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="188af-122">Maakt een groep van de netwerkbeveiligingsregel dat binnenkomend verkeer toegestaan.</span><span class="sxs-lookup"><span data-stu-id="188af-122">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="188af-123">In dit voorbeeld wordt is poort 80 geopend voor HTTP-verkeer.</span><span class="sxs-lookup"><span data-stu-id="188af-123">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="188af-124">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="188af-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="188af-125">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="188af-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="188af-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="188af-126">Next steps</span></span>

<span data-ttu-id="188af-127">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="188af-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="188af-128">Extra virtuele machine CLI scriptvoorbeelden vindt u in de [virtuele machine van Windows Azure-documentatie](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="188af-128">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
