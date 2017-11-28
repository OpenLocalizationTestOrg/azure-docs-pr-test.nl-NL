---
title: aaaAzure voorbeeldscript CLI - Load balance verkeer tooVMs voor hoge beschikbaarheid | Microsoft Docs
description: Azure CLI-voorbeeldscript - Load balance verkeer tooVMs voor hoge beschikbaarheid
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a><span data-ttu-id="56b4b-103">Laden van saldo verkeer tooVMs voor hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="56b4b-103">Load balance traffic tooVMs for high availability</span></span>

<span data-ttu-id="56b4b-104">Dit voorbeeldscript wordt gemaakt van alles wat u nodig toorun verschillende Ubuntu virtuele machines geconfigureerd in een maximaal beschikbare en load balanced configuratie.</span><span class="sxs-lookup"><span data-stu-id="56b4b-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="56b4b-105">Nadat het Hallo-script wordt uitgevoerd, hebt u drie virtuele machines, gekoppelde tooan Beschikbaarheidsset Azure en zijn toegankelijk via een Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="56b4b-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="56b4b-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="56b4b-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="56b4b-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="56b4b-107">Clean up deployment</span></span> 

<span data-ttu-id="56b4b-108">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="56b4b-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="56b4b-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="56b4b-109">Script explanation</span></span>

<span data-ttu-id="56b4b-110">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, virtuele machine, beschikbaarheidsset, load balancer en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="56b4b-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="56b4b-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="56b4b-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="56b4b-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="56b4b-112">Command</span></span> | <span data-ttu-id="56b4b-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="56b4b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="56b4b-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="56b4b-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="56b4b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="56b4b-116">AZ network vnet maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="56b4b-117">Maakt een virtueel Azure-netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="56b4b-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="56b4b-118">AZ netwerk openbare ip-maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="56b4b-119">Hiermee maakt een openbaar IP-adres met een statisch IP-adres en een bijbehorende DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="56b4b-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="56b4b-120">AZ network Load Balancer maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="56b4b-121">Hiermee maakt u een Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="56b4b-121">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="56b4b-122">AZ network Load Balancer-test maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="56b4b-123">Hiermee maakt u een load balancer-test.</span><span class="sxs-lookup"><span data-stu-id="56b4b-123">Creates a load balancer probe.</span></span> <span data-ttu-id="56b4b-124">Een load balancer-test gebruikte toomonitor elke virtuele machine in Hallo load balancer-set is.</span><span class="sxs-lookup"><span data-stu-id="56b4b-124">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="56b4b-125">Als een virtuele machine niet meer toegankelijk is, wordt verkeer is geen gerouteerde toohello VM.</span><span class="sxs-lookup"><span data-stu-id="56b4b-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="56b4b-126">AZ network Load Balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="56b4b-127">Maakt een regel voor load balancer.</span><span class="sxs-lookup"><span data-stu-id="56b4b-127">Creates a load balancer rule.</span></span> <span data-ttu-id="56b4b-128">In dit voorbeeld wordt een regel gemaakt voor poort 80.</span><span class="sxs-lookup"><span data-stu-id="56b4b-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="56b4b-129">HTTP-verkeer ontvangt bij Hallo load balancer is gerouteerde tooport 80 een Hallo VM's in Hallo LB-set.</span><span class="sxs-lookup"><span data-stu-id="56b4b-129">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello LB set.</span></span> |
| [<span data-ttu-id="56b4b-130">AZ netwerk lb-nat-regel voor binnenkomende verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="56b4b-131">Regel voor load balancer Network Address Translation (NAT) maakt.</span><span class="sxs-lookup"><span data-stu-id="56b4b-131">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="56b4b-132">NAT-regels toewijzen een poort van Hallo load balancer tooa poort op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="56b4b-132">NAT rules map a port of hello load balancer tooa port on a VM.</span></span> <span data-ttu-id="56b4b-133">In dit voorbeeld wordt een NAT-regel gemaakt voor SSH-verkeer tooeach VM in Hallo load balancer-set.</span><span class="sxs-lookup"><span data-stu-id="56b4b-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello load balancer set.</span></span>  |
| [<span data-ttu-id="56b4b-134">nsg voor AZ netwerk maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="56b4b-135">Maakt een netwerkbeveiligingsgroep (NSG), die een beveiligingsgrens tussen Hallo internet en Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="56b4b-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="56b4b-136">AZ netwerk nsg regel maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="56b4b-137">Hiermee maakt u een NSG regel tooallow binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="56b4b-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="56b4b-138">In dit voorbeeld wordt poort 22 voor SSH-verkeer geopend.</span><span class="sxs-lookup"><span data-stu-id="56b4b-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="56b4b-139">AZ netwerk nic maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="56b4b-140">Maakt een virtueel netwerkkaart en toohello virtueel netwerk, subnet en NSG gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="56b4b-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="56b4b-141">AZ vm beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="56b4b-142">Hiermee maakt een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="56b4b-142">Creates an availability set.</span></span> <span data-ttu-id="56b4b-143">Beschikbaarheidssets waarborgen uptime van toepassingen via Hallo virtuele machines verspreid over fysieke resources zo dat als fout optreedt, wordt de hele set Hallo niet gedaan.</span><span class="sxs-lookup"><span data-stu-id="56b4b-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="56b4b-144">AZ vm maken</span><span class="sxs-lookup"><span data-stu-id="56b4b-144">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="56b4b-145">Hallo virtuele machine maakt en toohello netwerkkaart, virtueel netwerk, subnet en NSG is verbonden.</span><span class="sxs-lookup"><span data-stu-id="56b4b-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="56b4b-146">Met deze opdracht geeft ook Hallo virtuele machine installatiekopie toobe gebruikt en de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="56b4b-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="56b4b-147">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="56b4b-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="56b4b-148">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="56b4b-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56b4b-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="56b4b-149">Next steps</span></span>

<span data-ttu-id="56b4b-150">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="56b4b-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="56b4b-151">Aanvullende voorbeelden van Azure toegang CLI script kunnen u vinden in Hallo [documentatie Azure Networking](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="56b4b-151">Additional Azure Networking CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
