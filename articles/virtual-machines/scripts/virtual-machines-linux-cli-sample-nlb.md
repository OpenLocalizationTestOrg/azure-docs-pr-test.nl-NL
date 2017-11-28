---
title: aaaAzure voorbeeldscript CLI - Maak een Linux-VM met NLB | Microsoft Docs
description: Azure CLI Script voorbeeld - een virtuele Linux-machine maken met NLB
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
ms.openlocfilehash: 79b245c1268734fead313b34c120f74ab2330d4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-highly-available-vm"></a><span data-ttu-id="b129d-103">Een maximaal beschikbare virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="b129d-103">Create a highly available VM</span></span>

<span data-ttu-id="b129d-104">Dit voorbeeldscript wordt gemaakt van alles wat u nodig toorun verschillende Ubuntu virtuele machines geconfigureerd in een maximaal beschikbare en load balanced configuratie.</span><span class="sxs-lookup"><span data-stu-id="b129d-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="b129d-105">Nadat het Hallo-script wordt uitgevoerd, hebt u drie virtuele machines, gekoppelde tooan Beschikbaarheidsset Azure en zijn toegankelijk via een Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="b129d-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b129d-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="b129d-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b129d-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="b129d-107">Clean up deployment</span></span> 

<span data-ttu-id="b129d-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b129d-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b129d-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="b129d-109">Script explanation</span></span>

<span data-ttu-id="b129d-110">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="b129d-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="b129d-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="b129d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b129d-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="b129d-112">Command</span></span> | <span data-ttu-id="b129d-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b129d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b129d-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="b129d-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b129d-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b129d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b129d-116">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="b129d-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="b129d-117">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="b129d-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="b129d-118">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="b129d-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="b129d-119">Hiermee maakt een openbaar IP-adres met een statisch IP-adres en een bijbehorende DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="b129d-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="b129d-120">AZ network Load Balancer maken</span><span class="sxs-lookup"><span data-stu-id="b129d-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="b129d-121">Hiermee maakt u een Azure-netwerk Load Balancer (NLB).</span><span class="sxs-lookup"><span data-stu-id="b129d-121">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="b129d-122">AZ network Load Balancer-test maken</span><span class="sxs-lookup"><span data-stu-id="b129d-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="b129d-123">Maakt een NLB-test.</span><span class="sxs-lookup"><span data-stu-id="b129d-123">Creates an NLB probe.</span></span> <span data-ttu-id="b129d-124">Een NLB-test gebruikte toomonitor elke virtuele machine in Hallo NLB set is.</span><span class="sxs-lookup"><span data-stu-id="b129d-124">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="b129d-125">Als een virtuele machine niet meer toegankelijk is, wordt verkeer is geen gerouteerde toohello VM.</span><span class="sxs-lookup"><span data-stu-id="b129d-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="b129d-126">AZ network Load Balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="b129d-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="b129d-127">Maakt een regel voor NLB.</span><span class="sxs-lookup"><span data-stu-id="b129d-127">Creates an NLB rule.</span></span> <span data-ttu-id="b129d-128">In dit voorbeeld wordt een regel gemaakt voor poort 80.</span><span class="sxs-lookup"><span data-stu-id="b129d-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="b129d-129">Zoals HTTP-verkeer bij Hallo NLB aankomt, is het gerouteerde tooport 80 een Hallo VM's in Hallo NLB set.</span><span class="sxs-lookup"><span data-stu-id="b129d-129">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="b129d-130">AZ netwerk lb-nat-regel voor binnenkomende verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="b129d-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="b129d-131">Maakt een regel voor NLB Network Address Translation (NAT).</span><span class="sxs-lookup"><span data-stu-id="b129d-131">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="b129d-132">NAT-regels toewijzen een poort Hallo NLB tooa poort op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b129d-132">NAT rules map a port of hello NLB tooa port on a VM.</span></span> <span data-ttu-id="b129d-133">In dit voorbeeld wordt een NAT-regel gemaakt voor SSH-verkeer tooeach VM in Hallo NLB set.</span><span class="sxs-lookup"><span data-stu-id="b129d-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello NLB set.</span></span>  |
| [<span data-ttu-id="b129d-134">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="b129d-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="b129d-135">Maakt een netwerkbeveiligingsgroep (NSG), die een beveiligingsgrens tussen Hallo internet en Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b129d-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="b129d-136">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="b129d-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="b129d-137">Hiermee maakt u een NSG regel tooallow binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="b129d-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="b129d-138">In dit voorbeeld wordt poort 22 voor SSH-verkeer geopend.</span><span class="sxs-lookup"><span data-stu-id="b129d-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="b129d-139">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="b129d-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="b129d-140">Maakt een virtueel netwerkkaart en toohello virtueel netwerk, subnet en NSG gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="b129d-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="b129d-141">AZ vm beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="b129d-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="b129d-142">Hiermee maakt een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="b129d-142">Creates an availability set.</span></span> <span data-ttu-id="b129d-143">Beschikbaarheidssets waarborgen uptime van toepassingen via Hallo virtuele machines verspreid over fysieke resources zo dat als fout optreedt, wordt de hele set Hallo niet gedaan.</span><span class="sxs-lookup"><span data-stu-id="b129d-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="b129d-144">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="b129d-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="b129d-145">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="b129d-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="b129d-146">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="b129d-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="b129d-147">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="b129d-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b129d-148">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="b129d-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b129d-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b129d-149">Next steps</span></span>

<span data-ttu-id="b129d-150">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b129d-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b129d-151">Extra virtuele machine CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure Linux VM documentatie](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b129d-151">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
