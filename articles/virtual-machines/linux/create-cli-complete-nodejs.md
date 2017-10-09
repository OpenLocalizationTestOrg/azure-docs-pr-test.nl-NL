---
title: een volledige Linux-omgeving Hello Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Opslag, een Linux-VM, een virtueel netwerk en subnet, een load balancer, een NIC, een openbare IP-adres en een netwerkbeveiligingsgroep maken via Hallo gemalen met behulp van hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a><span data-ttu-id="e03c8-103">Een volledige Linux-omgeving maken met Azure CLI 1.0 Hallo</span><span class="sxs-lookup"><span data-stu-id="e03c8-103">Create a complete Linux environment with hello Azure CLI 1.0</span></span>
<span data-ttu-id="e03c8-104">In dit artikel verder gaan we met een eenvoudig netwerk met een combinatie van virtuele machines die gebruikt voor ontwikkeling en eenvoudige computing worden en een load balancer.</span><span class="sxs-lookup"><span data-stu-id="e03c8-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="e03c8-105">We doorlopen Hallo proces door de opdracht, totdat u twee hebt, beveiligde virtuele Linux-machines toowhich die u verbinding van een willekeurige plaats op Hallo Internet maken kunt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-105">We walk through hello process command by command, until you have two working, secure Linux VMs toowhich you can connect from anywhere on hello Internet.</span></span> <span data-ttu-id="e03c8-106">Vervolgens kunt u op toomore complexe netwerken en omgevingen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-106">Then you can move on toomore complex networks and environments.</span></span>

<span data-ttu-id="e03c8-107">Langs Hallo manier u meer informatie over Hallo afhankelijkheidshiërarchie dat Hallo Resource Manager-implementatiemodel u biedt, en over hoeveel power biedt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-107">Along hello way, you learn about hello dependency hierarchy that hello Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="e03c8-108">Nadat u hoe Hallo systeem is gemaakt ziet, kunt u opnieuw bouwen het veel sneller met behulp van [Azure Resource Manager-sjablonen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e03c8-108">After you see how hello system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e03c8-109">Ook, nadat u leert hoe onderdelen van uw omgeving Hallo bij elkaar passen, sjablonen tooautomate maken ze eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="e03c8-109">Also, after you learn how hello parts of your environment fit together, creating templates tooautomate them becomes easier.</span></span>

<span data-ttu-id="e03c8-110">Hallo-omgeving bevat:</span><span class="sxs-lookup"><span data-stu-id="e03c8-110">hello environment contains:</span></span>

* <span data-ttu-id="e03c8-111">Twee virtuele machines in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="e03c8-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="e03c8-112">Een load balancer met een regel voor load balancing op poort 80.</span><span class="sxs-lookup"><span data-stu-id="e03c8-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="e03c8-113">Netwerkbeveiligingsgroep (NSG) regels tooprotect tegen ongewenste verkeer van de VM.</span><span class="sxs-lookup"><span data-stu-id="e03c8-113">Network security group (NSG) rules tooprotect your VM from unwanted traffic.</span></span>

<span data-ttu-id="e03c8-114">toocreate deze aangepaste omgeving, moet u Hallo nieuwste [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in de modus Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="e03c8-114">toocreate this custom environment, you need hello latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="e03c8-115">U moet ook een JSON hulpprogramma parseren.</span><span class="sxs-lookup"><span data-stu-id="e03c8-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="e03c8-116">In dit voorbeeld wordt [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="e03c8-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e03c8-117">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="e03c8-117">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e03c8-118">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e03c8-118">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e03c8-119">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="e03c8-119">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e03c8-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="e03c8-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="e03c8-121">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="e03c8-121">Quick commands</span></span>
<span data-ttu-id="e03c8-122">Als u moet tooquickly Hallo taak, na de sectie details Hallo Hallo baseren opdrachten tooupload een tooAzure VM.</span><span class="sxs-lookup"><span data-stu-id="e03c8-122">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="e03c8-123">Meer gedetailleerde informatie en context voor elke stap vindt u in de rest Hallo van Hallo document, te beginnen [hier](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="e03c8-123">More detailed information and context for each step can be found in hello rest of hello document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="e03c8-124">Zorg ervoor dat u hebt [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="e03c8-124">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e03c8-125">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="e03c8-125">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e03c8-126">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="e03c8-127">Hallo resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-127">Create hello resource group.</span></span> <span data-ttu-id="e03c8-128">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` locatie:</span><span class="sxs-lookup"><span data-stu-id="e03c8-128">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="e03c8-129">Hallo resourcegroep controleren met behulp van Hallo JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="e03c8-129">Verify hello resource group by using hello JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="e03c8-130">Hallo-opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-130">Create hello storage account.</span></span> <span data-ttu-id="e03c8-131">Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-131">hello following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="e03c8-132">(Hallo opslagaccountnaam moet uniek zijn, zodat uw eigen unieke naam opgeven.)</span><span class="sxs-lookup"><span data-stu-id="e03c8-132">(hello storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="e03c8-133">Hallo storage-account met behulp van de JSON-parser Hallo controleren:</span><span class="sxs-lookup"><span data-stu-id="e03c8-133">Verify hello storage account by using hello JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="e03c8-134">Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-134">Create hello virtual network.</span></span> <span data-ttu-id="e03c8-135">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-135">hello following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="e03c8-136">Een subnet maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-136">Create a subnet.</span></span> <span data-ttu-id="e03c8-137">Hallo volgende voorbeeld wordt een subnet met de naam `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-137">hello following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="e03c8-138">Hallo virtueel netwerk en subnet controleren met behulp van Hallo JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="e03c8-138">Verify hello virtual network and subnet by using hello JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="e03c8-139">Maak een openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="e03c8-139">Create a public IP.</span></span> <span data-ttu-id="e03c8-140">Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam `myPublicIP` met Hallo DNS-naam van `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-140">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="e03c8-141">(Hallo DNS-naam moet uniek zijn, zodat uw eigen unieke naam opgeven.)</span><span class="sxs-lookup"><span data-stu-id="e03c8-141">(hello DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="e03c8-142">Hallo load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-142">Create hello load balancer.</span></span> <span data-ttu-id="e03c8-143">Hallo volgende voorbeeld maakt u een load balancer met de naam `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-143">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="e03c8-144">Maak een front-end-IP-adresgroep voor Hallo load balancer, en koppel Hallo openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="e03c8-144">Create a front-end IP pool for hello load balancer, and associate hello public IP.</span></span> <span data-ttu-id="e03c8-145">Hallo volgende voorbeeld wordt een front-end-IP-adresgroep met de naam `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-145">hello following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="e03c8-146">Hallo backend-IP-adresgroep voor Hallo load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-146">Create hello back-end IP pool for hello load balancer.</span></span> <span data-ttu-id="e03c8-147">Hallo volgende voorbeeld wordt een back-end-IP-adresgroep met de naam `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-147">hello following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="e03c8-148">SSH inkomende netwerk address translation (NAT) regels voor Hallo load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-148">Create SSH inbound network address translation (NAT) rules for hello load balancer.</span></span> <span data-ttu-id="e03c8-149">Hallo volgende voorbeeld maakt u twee regels van load balancer, `myLoadBalancerRuleSSH1` en `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-149">hello following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="e03c8-150">Maken van webinhoud Hallo inkomende NAT-regels voor Hallo de load balancer.</span><span class="sxs-lookup"><span data-stu-id="e03c8-150">Create hello web inbound NAT rules for hello load balancer.</span></span> <span data-ttu-id="e03c8-151">Hallo volgende voorbeeld maakt u een regel voor load balancer met de naam `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-151">hello following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="e03c8-152">Hallo health load balancer-test maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-152">Create hello load balancer health probe.</span></span> <span data-ttu-id="e03c8-153">Hallo volgende voorbeeld wordt een TCP-test met de naam `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-153">hello following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="e03c8-154">Hallo load balancer, IP-adresgroepen en NAT-regels controleren met behulp van Hallo JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="e03c8-154">Verify hello load balancer, IP pools, and NAT rules by using hello JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="e03c8-155">Hallo eerste netwerkinterfacekaart (NIC) maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-155">Create hello first network interface card (NIC).</span></span> <span data-ttu-id="e03c8-156">Vervang Hallo `#####-###-###` secties met uw eigen Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="e03c8-156">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="e03c8-157">Uw abonnement ID wordt vermeld in de uitvoer van Hallo **jq** wanneer u bekijkt hello resources die u maakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-157">Your subscription ID is noted in hello output of **jq** when you examine hello resources you are creating.</span></span> <span data-ttu-id="e03c8-158">U kunt ook uw abonnements-ID met weergeven `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="e03c8-159">Hallo volgende voorbeeld wordt een NIC met de naam `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-159">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="e03c8-160">De tweede NIC Hallo maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-160">Create hello second NIC.</span></span> <span data-ttu-id="e03c8-161">Hallo volgende voorbeeld wordt een NIC met de naam `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-161">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="e03c8-162">Controleer of u Hallo twee NIC's met behulp van de JSON-parser Hallo:</span><span class="sxs-lookup"><span data-stu-id="e03c8-162">Verify hello two NICs by using hello JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="e03c8-163">Hallo netwerkbeveiligingsgroep maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-163">Create hello network security group.</span></span> <span data-ttu-id="e03c8-164">Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-164">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="e03c8-165">Twee regels voor binnenkomende verbindingen voor Hallo netwerkbeveiligingsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-165">Add two inbound rules for hello network security group.</span></span> <span data-ttu-id="e03c8-166">Hallo volgende voorbeeld maakt u twee regels `myNetworkSecurityGroupRuleSSH` en `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-166">hello following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="e03c8-167">Controleer of u Hallo netwerkbeveiligingsgroep en regels voor binnenkomende verbindingen met behulp van de JSON-parser Hallo:</span><span class="sxs-lookup"><span data-stu-id="e03c8-167">Verify hello network security group and inbound rules by using hello JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="e03c8-168">Hallo netwerkbeveiliging binden groep toohello twee NIC's:</span><span class="sxs-lookup"><span data-stu-id="e03c8-168">Bind hello network security group toohello two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="e03c8-169">Hallo beschikbaarheidsset maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-169">Create hello availability set.</span></span> <span data-ttu-id="e03c8-170">Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-170">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="e03c8-171">Maak Hallo eerste Linux VM.</span><span class="sxs-lookup"><span data-stu-id="e03c8-171">Create hello first Linux VM.</span></span> <span data-ttu-id="e03c8-172">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-172">hello following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="e03c8-173">Hallo maken tweede Linux VM.</span><span class="sxs-lookup"><span data-stu-id="e03c8-173">Create hello second Linux VM.</span></span> <span data-ttu-id="e03c8-174">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-174">hello following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="e03c8-175">Hallo JSON-parser tooverify gebruiken die alles die is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="e03c8-175">Use hello JSON parser tooverify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="e03c8-176">Uw nieuwe omgeving tooa sjabloon tooquickly opnieuw maken nieuwe exemplaren exporteren:</span><span class="sxs-lookup"><span data-stu-id="e03c8-176">Export your new environment tooa template tooquickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e03c8-177">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="e03c8-177">Detailed walkthrough</span></span>
<span data-ttu-id="e03c8-178">Hallo gedetailleerde stappen volgen wordt uitgelegd wat elke opdracht doet tijdens het samenstellen van buiten uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="e03c8-178">hello detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="e03c8-179">Deze begrippen zijn handig als u uw eigen aangepaste omgevingen voor ontwikkeling of productie bouwen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="e03c8-180">Zorg ervoor dat u hebt [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="e03c8-180">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e03c8-181">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="e03c8-181">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e03c8-182">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="e03c8-183">Maken van resourcegroepen en locaties implementatie kiezen</span><span class="sxs-lookup"><span data-stu-id="e03c8-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="e03c8-184">Azure-resourcegroepen zijn logische implementatie entiteiten met gegevens en metagegevens tooenable Hallo logische beheer van de configuratie van de resource-implementaties.</span><span class="sxs-lookup"><span data-stu-id="e03c8-184">Azure resource groups are logical deployment entities that contain configuration information and metadata tooenable hello logical management of resource deployments.</span></span> <span data-ttu-id="e03c8-185">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` locatie:</span><span class="sxs-lookup"><span data-stu-id="e03c8-185">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="e03c8-186">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="e03c8-187">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-187">Create a storage account</span></span>
<span data-ttu-id="e03c8-188">U moet de storage-accounts voor de VM-schijven en eventuele extra gegevensschijven die u tooadd wilt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-188">You need storage accounts for your VM disks and for any additional data disks that you want tooadd.</span></span> <span data-ttu-id="e03c8-189">U kunt storage-accounts maken bijna onmiddellijk na het maken van resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="e03c8-190">Hier gebruiken we Hallo `azure storage account create` opdracht, en Hallo type opslagondersteuning gewenste Hallo-locatie van de resourcegroep Hallo Hallo account die wordt doorgegeven bepaalt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-190">Here we use hello `azure storage account create` command, passing hello location of hello account, hello resource group that controls it, and hello type of storage support you want.</span></span> <span data-ttu-id="e03c8-191">Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-191">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="e03c8-192">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="e03c8-193">onze resourcegroep via Hallo tooexamine `azure group show` opdracht, gebruiken we Hallo [jq](https://stedolan.github.io/jq/) hulpprogramma samen met de Hallo `--json` Azure CLI-optie.</span><span class="sxs-lookup"><span data-stu-id="e03c8-193">tooexamine our resource group by using hello `azure group show` command, let's use hello [jq](https://stedolan.github.io/jq/) tool along with hello `--json` Azure CLI option.</span></span> <span data-ttu-id="e03c8-194">(U kunt **jsawk** of enkele taal bibliotheek u liever tooparse Hallo JSON.)</span><span class="sxs-lookup"><span data-stu-id="e03c8-194">(You can use **jsawk** or any language library you prefer tooparse hello JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="e03c8-195">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="e03c8-196">tooinvestigate hello storage-account met behulp van Hallo CLI, moet u eerst tooset Hallo accountnamen en sleutels.</span><span class="sxs-lookup"><span data-stu-id="e03c8-196">tooinvestigate hello storage account by using hello CLI, you first need tooset hello account names and keys.</span></span> <span data-ttu-id="e03c8-197">Hallo-naam van de storage-account in het volgende voorbeeld met een naam die u kiest Hallo Hallo vervangen:</span><span class="sxs-lookup"><span data-stu-id="e03c8-197">Replace hello name of hello storage account in hello following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="e03c8-198">U kunt vervolgens uw storage-gegevens eenvoudig bekijken:</span><span class="sxs-lookup"><span data-stu-id="e03c8-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="e03c8-199">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="e03c8-200">Een virtueel netwerk en subnet maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="e03c8-201">Vervolgens gaat u tooneed toocreate een virtueel netwerk in Azure en een subnet van uw virtuele machines maken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e03c8-201">Next you're going tooneed toocreate a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="e03c8-202">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet` Hello `192.168.0.0/16` adresvoorvoegsel:</span><span class="sxs-lookup"><span data-stu-id="e03c8-202">hello following example creates a virtual network named `myVnet` with hello `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="e03c8-203">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="e03c8-204">We gebruiken opnieuw Hallo--json-optie van `azure group show` en `jq` toosee hoe we onze bronnen bouwen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-204">Again, let's use hello --json option of `azure group show` and `jq` toosee how we're building our resources.</span></span> <span data-ttu-id="e03c8-205">Nu een `storageAccounts` resource en een `virtualNetworks` resource.</span><span class="sxs-lookup"><span data-stu-id="e03c8-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="e03c8-206">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="e03c8-207">Nu gaan we een subnet maken in Hallo `myVnet` virtueel netwerk in welke Hallo virtuele machines zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e03c8-207">Now let's create a subnet in hello `myVnet` virtual network into which hello VMs are deployed.</span></span> <span data-ttu-id="e03c8-208">We gebruiken Hallo `azure network vnet subnet create` opdracht samen met de Hallo resources we al hebt gemaakt: Hallo `myResourceGroup` resourcegroep en Hallo `myVnet` virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="e03c8-208">We use hello `azure network vnet subnet create` command, along with hello resources we've already created: hello `myResourceGroup` resource group and hello `myVnet` virtual network.</span></span> <span data-ttu-id="e03c8-209">In de Hallo voorbeeld te volgen, we Hallo subnet met de naam toevoegen `mySubnet` met Hallo subnet adresvoorvoegsel van `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-209">In hello following example, we add hello subnet named `mySubnet` with hello subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="e03c8-210">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="e03c8-211">Omdat Hallo subnet logisch in het virtuele netwerk hello, zoekt we Hallo subnet met een iets andere opdracht.</span><span class="sxs-lookup"><span data-stu-id="e03c8-211">Because hello subnet is logically inside hello virtual network, we look for hello subnet information with a slightly different command.</span></span> <span data-ttu-id="e03c8-212">Hallo-opdracht we gebruiken is `azure network vnet show`, maar we verder tooexamine Hallo JSON-uitvoer met behulp van `jq`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-212">hello command we use is `azure network vnet show`, but we continue tooexamine hello JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="e03c8-213">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="e03c8-214">Een openbaar IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-214">Create a public IP address</span></span>
<span data-ttu-id="e03c8-215">Nu gaan we maken Hallo openbaar IP-adres (PIP) dat we tooyour load balancer toewijzen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-215">Now let's create hello public IP address (PIP) that we assign tooyour load balancer.</span></span> <span data-ttu-id="e03c8-216">Hiermee kunt u tooconnect tooyour VM's van Hallo Internet met behulp van Hallo `azure network public-ip create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e03c8-216">It enables you tooconnect tooyour VMs from hello Internet by using hello `azure network public-ip create` command.</span></span> <span data-ttu-id="e03c8-217">Omdat Hallo standaardadres dynamisch is, maken we een benoemde DNS-vermelding in Hallo **cloudapp.azure.com** domein met behulp van Hallo `--domain-name-label` optie.</span><span class="sxs-lookup"><span data-stu-id="e03c8-217">Because hello default address is dynamic, we create a named DNS entry in hello **cloudapp.azure.com** domain by using hello `--domain-name-label` option.</span></span> <span data-ttu-id="e03c8-218">Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam `myPublicIP` met Hallo DNS-naam van `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-218">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="e03c8-219">Aangezien Hallo DNS-naam uniek zijn moet, kunt u uw eigen unieke DNS-naam opgeven:</span><span class="sxs-lookup"><span data-stu-id="e03c8-219">Because hello DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="e03c8-220">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="e03c8-221">Hallo openbaar IP-adres is ook een bron op het hoogste niveau, zodat u deze met ziet `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-221">hello public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="e03c8-222">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="e03c8-223">U kunt meer informatie over resource, zoals Hallo volledig gekwalificeerde domeinnaam (FQDN) van subdomein hello, met behulp van de volledige Hallo onderzoeken `azure network public-ip show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e03c8-223">You can investigate more resource details, including hello fully qualified domain name (FQDN) of hello subdomain, by using hello complete `azure network public-ip show` command.</span></span> <span data-ttu-id="e03c8-224">Hallo openbare IP-adres resource logisch is toegewezen, maar een specifiek adres nog niet is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-224">hello public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="e03c8-225">een IP-adres tooobtain, gaat u tooneed een load balancer die we nog geen hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-225">tooobtain an IP address, you're going tooneed a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="e03c8-226">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="e03c8-227">Een load balancer en IP-adresgroepen maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="e03c8-228">Wanneer u een load balancer maakt, kunt u toodistribute verkeer over meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e03c8-228">When you create a load balancer, it enables you toodistribute traffic across multiple VMs.</span></span> <span data-ttu-id="e03c8-229">Het bevat ook redundantie tooyour toepassing door het uitvoeren van meerdere virtuele machines die toouser aanvragen in Hallo-gebeurtenis van onderhoud of zware belasting reageren.</span><span class="sxs-lookup"><span data-stu-id="e03c8-229">It also provides redundancy tooyour application by running multiple VMs that respond toouser requests in hello event of maintenance or heavy loads.</span></span> <span data-ttu-id="e03c8-230">Hallo volgende voorbeeld maakt u een load balancer met de naam `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-230">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="e03c8-231">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="e03c8-232">De load balancer is redelijk leeg, dus gaan we een aantal IP-adresgroepen maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="e03c8-233">We willen toocreate twee IP-adresgroepen voor de load balancer, één voor Hallo-front-end en één voor de back-end Hallo.</span><span class="sxs-lookup"><span data-stu-id="e03c8-233">We want toocreate two IP pools for our load balancer, one for hello front end and one for hello back end.</span></span> <span data-ttu-id="e03c8-234">de front-end-IP-adresgroep Hallo is openbaar zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="e03c8-234">hello front-end IP pool is publicly visible.</span></span> <span data-ttu-id="e03c8-235">Het is ook Hallo locatie toowhich die we toewijzen Hallo PIP die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-235">It's also hello location toowhich we assign hello PIP that we created earlier.</span></span> <span data-ttu-id="e03c8-236">Vervolgens gebruiken we Hallo back-end-pool als locatie voor onze tooconnect VM's aan.</span><span class="sxs-lookup"><span data-stu-id="e03c8-236">Then we use hello back-end pool as a location for our VMs tooconnect to.</span></span> <span data-ttu-id="e03c8-237">Op die manier Hallo-verkeer door Hallo load balancer toohello VMs kan stromen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-237">That way, hello traffic can flow through hello load balancer toohello VMs.</span></span>

<span data-ttu-id="e03c8-238">Eerst laten we onze front-end-IP-adresgroep maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="e03c8-239">Hallo volgende voorbeeld wordt een front-groep met de naam `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-239">hello following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="e03c8-240">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="e03c8-241">Houd er rekening mee hoe we Hallo gebruikt `--public-ip-name` toopass in Hallo switch `myPublicIP` die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-241">Note how we used hello `--public-ip-name` switch toopass in hello `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="e03c8-242">Toewijzen van Hallo openbare IP-adres toohello load balancer kunt u tooreach uw virtuele machines via Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="e03c8-242">Assigning hello public IP address toohello load balancer allows you tooreach your VMs across hello Internet.</span></span>

<span data-ttu-id="e03c8-243">Vervolgens maken we onze tweede IP-adresgroep voor de back-end-verkeer.</span><span class="sxs-lookup"><span data-stu-id="e03c8-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="e03c8-244">Hallo volgende voorbeeld wordt een back-end-pool met de naam `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-244">hello following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="e03c8-245">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="e03c8-246">We zien hoe u onze load balancer doet door te zoeken met `azure network lb show` en onderzoeken Hallo JSON-uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining hello JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="e03c8-247">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="e03c8-248">NAT-regels van load balancer maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="e03c8-249">tooget verkeer via de load balancer moeten we toocreate netwerk address translation (NAT) regels die binnenkomend of uitgaand acties specificeren.</span><span class="sxs-lookup"><span data-stu-id="e03c8-249">tooget traffic flowing through our load balancer, we need toocreate network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="e03c8-250">U kunt opgeven Hallo protocol toouse vervolgens externe poorten toointernal poorten naar wens worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-250">You can specify hello protocol toouse, then map external ports toointernal ports as desired.</span></span> <span data-ttu-id="e03c8-251">Voor onze omgeving gaan we een aantal regels maken die SSH toestaan via onze load balancer tooour virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e03c8-251">For our environment, let's create some rules that allow SSH through our load balancer tooour VMs.</span></span> <span data-ttu-id="e03c8-252">We instellen TCP-poorten 4222 en 4223 toodirect tooTCP poort 22 op de virtuele machines (die we later maken).</span><span class="sxs-lookup"><span data-stu-id="e03c8-252">We set up TCP ports 4222 and 4223 toodirect tooTCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="e03c8-253">Hallo volgende voorbeeld maakt u een regel met naam `myLoadBalancerRuleSSH1` 4222 tooport 22 toomap TCP-poort:</span><span class="sxs-lookup"><span data-stu-id="e03c8-253">hello following example creates a rule named `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="e03c8-254">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="e03c8-255">Herhaal Hallo procedure voor de tweede NAT-regel voor SSH.</span><span class="sxs-lookup"><span data-stu-id="e03c8-255">Repeat hello procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="e03c8-256">Hallo volgende voorbeeld maakt u een regel met naam `myLoadBalancerRuleSSH2` 4223 tooport 22 toomap TCP-poort:</span><span class="sxs-lookup"><span data-stu-id="e03c8-256">hello following example creates a rule named `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="e03c8-257">We gaan ook opwekken en maak een NAT-regel voor TCP-poort 80 voor internetverkeer, Hallo regel aansluiting up tooour IP-adresgroepen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking hello rule up tooour IP pools.</span></span> <span data-ttu-id="e03c8-258">Als we IP-adresgroep, in plaats van een afzonderlijk, up Hallo regel tooour VMs aansluiting aansluiten Hallo regel tooan kunnen we toevoegen of verwijderen van virtuele machines van Hallo IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="e03c8-258">If we hook up hello rule tooan IP pool, instead of hooking up hello rule tooour VMs individually, we can add or remove VMs from hello IP pool.</span></span> <span data-ttu-id="e03c8-259">Hallo load balancer automatisch aangepast Hallo verkeersstroom.</span><span class="sxs-lookup"><span data-stu-id="e03c8-259">hello load balancer automatically adjusts hello flow of traffic.</span></span> <span data-ttu-id="e03c8-260">Hallo volgende voorbeeld maakt u een regel met naam `myLoadBalancerRuleWeb` toomap TCP-poort 80 tooport 80:</span><span class="sxs-lookup"><span data-stu-id="e03c8-260">hello following example creates a rule named `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="e03c8-261">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="e03c8-262">Een load balancer health test maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-262">Create a load balancer health probe</span></span>
<span data-ttu-id="e03c8-263">Een health test regelmatig controles op Hallo van virtuele machines die zich achter onze load balancer-toomake ervoor dat ze zijn het functioneren en toorequests reageert, zoals is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e03c8-263">A health probe periodically checks on hello VMs that are behind our load balancer toomake sure they're operating and responding toorequests as defined.</span></span> <span data-ttu-id="e03c8-264">Als u niet, ze verwijderd uit omgeleid bewerking tooensure dat gebruikers worden niet wordt toothem.</span><span class="sxs-lookup"><span data-stu-id="e03c8-264">If not, they're removed from operation tooensure that users aren't being directed toothem.</span></span> <span data-ttu-id="e03c8-265">U kunt aangepaste controles voor de Hallo health test, samen met intervallen en time-outwaarden definiëren.</span><span class="sxs-lookup"><span data-stu-id="e03c8-265">You can define custom checks for hello health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="e03c8-266">Zie voor meer informatie over statuscontroles [Load Balancer-tests](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e03c8-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e03c8-267">Hallo volgende voorbeeld wordt een TCP health aangeduid met de naam `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-267">hello following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="e03c8-268">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="e03c8-269">Hier wordt een interval van 15 seconden voor onze statuscontroles opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e03c8-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="e03c8-270">We kunnen maximaal vier tests (één minuut) voordat Hallo load balancer overweegt dat die host Hallo werkt niet meer over het hoofd ziet.</span><span class="sxs-lookup"><span data-stu-id="e03c8-270">We can miss a maximum of four probes (one minute) before hello load balancer considers that hello host is no longer functioning.</span></span>

## <a name="verify-hello-load-balancer"></a><span data-ttu-id="e03c8-271">Controleer of Hallo load balancer</span><span class="sxs-lookup"><span data-stu-id="e03c8-271">Verify hello load balancer</span></span>
<span data-ttu-id="e03c8-272">Nu wordt Hallo load balancer-configuratie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e03c8-272">Now hello load balancer configuration is done.</span></span> <span data-ttu-id="e03c8-273">Hier volgen Hallo manier te werk:</span><span class="sxs-lookup"><span data-stu-id="e03c8-273">Here are hello steps you took:</span></span>

1. <span data-ttu-id="e03c8-274">U hebt gemaakt voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="e03c8-274">You created a load balancer.</span></span>
2. <span data-ttu-id="e03c8-275">U een front-end-IP-adresgroep gemaakt en een openbare IP-tooit toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-275">You created a front-end IP pool and assigned a public IP tooit.</span></span>
3. <span data-ttu-id="e03c8-276">U een back-end-IP-adresgroep die virtuele machines verbinding met maken kunnen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="e03c8-277">U NAT-regels waarmee SSH toohello VM's voor beheer, samen met een regel waarmee u TCP-poort 80 voor de web-app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-277">You created NAT rules that allow SSH toohello VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="e03c8-278">U hebt een health test tooperiodically selectievakje Hallo VM's toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e03c8-278">You added a health probe tooperiodically check hello VMs.</span></span> <span data-ttu-id="e03c8-279">Deze test health zorgt ervoor dat gebruikers een virtuele machine die niet meer werkt of inhoud tooaccess niet proberen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-279">This health probe ensures that users don't try tooaccess a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="e03c8-280">We bekijken wat de load balancer er nu uit:</span><span class="sxs-lookup"><span data-stu-id="e03c8-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="e03c8-281">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a><span data-ttu-id="e03c8-282">Maken van een NIC toouse Hello Linux VM</span><span class="sxs-lookup"><span data-stu-id="e03c8-282">Create an NIC toouse with hello Linux VM</span></span>
<span data-ttu-id="e03c8-283">NIC's zijn programmatisch beschikbaar, omdat u regels tootheir gebruik kunt toepassen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-283">NICs are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="e03c8-284">U kunt ook meer dan één hebben.</span><span class="sxs-lookup"><span data-stu-id="e03c8-284">You can also have more than one.</span></span> <span data-ttu-id="e03c8-285">In de volgende Hallo `azure network nic create` opdracht u aansluiten Hallo NIC toohello load back-end-IP-adresgroep en deze koppelen aan Hallo NAT-regel toopermit SSH-verkeer.</span><span class="sxs-lookup"><span data-stu-id="e03c8-285">In hello following `azure network nic create` command, you hook up hello NIC toohello load back-end IP pool and associate it with hello NAT rule toopermit SSH traffic.</span></span>

<span data-ttu-id="e03c8-286">Vervang Hallo `#####-###-###` secties met uw eigen Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="e03c8-286">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="e03c8-287">Uw abonnement ID wordt vermeld in de uitvoer van Hallo `jq` wanneer u bekijkt hello resources die u maakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-287">Your subscription ID is noted in hello output of `jq` when you examine hello resources you are creating.</span></span> <span data-ttu-id="e03c8-288">U kunt ook uw abonnements-ID met weergeven `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="e03c8-289">Hallo volgende voorbeeld wordt een NIC met de naam `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-289">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="e03c8-290">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="e03c8-291">Hallo details kunt u zien door Hallo resource rechtstreeks in.</span><span class="sxs-lookup"><span data-stu-id="e03c8-291">You can see hello details by examining hello resource directly.</span></span> <span data-ttu-id="e03c8-292">U Hallo resource bestuderen met behulp van Hallo `azure network nic show` opdracht:</span><span class="sxs-lookup"><span data-stu-id="e03c8-292">You examine hello resource by using hello `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="e03c8-293">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="e03c8-294">Nu we maken Hallo tweede NIC, opnieuw koppelen in tooour backend-IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="e03c8-294">Now we create hello second NIC, hooking in tooour back-end IP pool again.</span></span> <span data-ttu-id="e03c8-295">Deze tijd Hallo tweede NAT-regel toestaat SSH verkeer.</span><span class="sxs-lookup"><span data-stu-id="e03c8-295">This time hello second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="e03c8-296">Hallo volgende voorbeeld wordt een NIC met de naam `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-296">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="e03c8-297">Een netwerkbeveiligingsgroep en regels maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-297">Create a network security group and rules</span></span>
<span data-ttu-id="e03c8-298">Nu een netwerkbeveiligingsgroep maken en regels voor binnenkomende verbindingen die van toepassing hello toegang krijgen tot toohello NIC.</span><span class="sxs-lookup"><span data-stu-id="e03c8-298">Now we create a network security group and hello inbound rules that govern access toohello NIC.</span></span> <span data-ttu-id="e03c8-299">Een netwerkbeveiligingsgroep kan worden toegepast tooa NIC of subnet.</span><span class="sxs-lookup"><span data-stu-id="e03c8-299">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="e03c8-300">U definiëren regels toocontrol Hallo verkeersstroom in uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e03c8-300">You define rules toocontrol hello flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="e03c8-301">Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-301">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="e03c8-302">We voegen inkomende hello-regel voor Hallo NSG tooallow binnenkomende verbindingen op poort 22 (toosupport SSH).</span><span class="sxs-lookup"><span data-stu-id="e03c8-302">Let's add hello inbound rule for hello NSG tooallow inbound connections on port 22 (toosupport SSH).</span></span> <span data-ttu-id="e03c8-303">Hallo volgende voorbeeld maakt u een regel met naam `myNetworkSecurityGroupRuleSSH` tooallow TCP op poort 22:</span><span class="sxs-lookup"><span data-stu-id="e03c8-303">hello following example creates a rule named `myNetworkSecurityGroupRuleSSH` tooallow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="e03c8-304">Nu gaan we voegen inkomende hello-regel voor Hallo NSG tooallow binnenkomende verbindingen op poort 80 (webverkeer toosupport).</span><span class="sxs-lookup"><span data-stu-id="e03c8-304">Now let's add hello inbound rule for hello NSG tooallow inbound connections on port 80 (toosupport web traffic).</span></span> <span data-ttu-id="e03c8-305">Hallo volgende voorbeeld maakt u een regel met naam `myNetworkSecurityGroupRuleHTTP` tooallow TCP op poort 80:</span><span class="sxs-lookup"><span data-stu-id="e03c8-305">hello following example creates a rule named `myNetworkSecurityGroupRuleHTTP` tooallow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="e03c8-306">inkomende Hello-regel is een filter naar binnenkomende netwerkverbindingen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-306">hello inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="e03c8-307">In dit voorbeeld binden we Hallo NSG toohello VMs virtuele NIC, wat betekent dat elke aanvraag tooport 22 wordt doorgegeven via toohello NIC op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e03c8-307">In this example, we bind hello NSG toohello VMs virtual NIC, which means that any request tooport 22 is passed through toohello NIC on our VM.</span></span> <span data-ttu-id="e03c8-308">Deze regel binnenkomende over een netwerkverbinding is en niet over een eindpunt met dit is wat het normaal zou zijn over in klassieke implementaties.</span><span class="sxs-lookup"><span data-stu-id="e03c8-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="e03c8-309">tooopen een poort, moet u Hallo laten `--source-port-range` instellen te '\*' (standaardwaarde Hallo) tooaccept inkomende aanvragen van **eventuele** poort aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-309">tooopen a port, you must leave hello `--source-port-range` set too'\*' (hello default value) tooaccept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="e03c8-310">Poorten zijn meestal dynamisch zijn.</span><span class="sxs-lookup"><span data-stu-id="e03c8-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-toohello-nic"></a><span data-ttu-id="e03c8-311">BIND toohello NIC</span><span class="sxs-lookup"><span data-stu-id="e03c8-311">Bind toohello NIC</span></span>
<span data-ttu-id="e03c8-312">Hallo NSG toohello NIC's worden gebonden.</span><span class="sxs-lookup"><span data-stu-id="e03c8-312">Bind hello NSG toohello NICs.</span></span> <span data-ttu-id="e03c8-313">We moeten tooconnect onze NIC's met onze netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="e03c8-313">We need tooconnect our NICs with our network security group.</span></span> <span data-ttu-id="e03c8-314">Voer beide opdrachten, toohook van beide onze NIC's:</span><span class="sxs-lookup"><span data-stu-id="e03c8-314">Run both commands, toohook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="e03c8-315">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-315">Create an availability set</span></span>
<span data-ttu-id="e03c8-316">Beschikbaarheidssets help verspreiding uw virtuele machines in domeinen met fouten en upgradedomeinen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="e03c8-317">Laten we de beschikbaarheidsset voor uw virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="e03c8-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="e03c8-318">Hallo volgende voorbeeld maakt u een beschikbaarheidsset benoemde `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="e03c8-318">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="e03c8-319">Domeinen met fouten definiëren een groepering van virtuele machines die een gemeenschappelijk power-bron- en switch delen.</span><span class="sxs-lookup"><span data-stu-id="e03c8-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="e03c8-320">Standaard zijn Hallo virtuele machines die zijn geconfigureerd in de beschikbaarheidsset gescheiden in up toothree domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="e03c8-320">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="e03c8-321">Hallo idee is een hardwareprobleem in een van deze domeinen met fouten heeft geen invloed op elke virtuele machine die uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e03c8-321">hello idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="e03c8-322">Virtuele machines verdeelt Azure automatisch over Hallo foutdomeinen wanneer ze worden geplaatst in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="e03c8-322">Azure automatically distributes VMs across hello fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="e03c8-323">Upgradedomeinen groepen van virtuele machines en de onderliggende fysieke hardware die kan worden opgestart op Hallo duiden op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="e03c8-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="e03c8-324">Hallo volgorde waarin upgradedomeinen worden opgestart mogelijk geen opeenvolgende tijdens gepland onderhoud, maar slechts één upgrade opnieuw wordt opgestart tegelijk.</span><span class="sxs-lookup"><span data-stu-id="e03c8-324">hello order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="e03c8-325">Opnieuw verdeelt Azure automatisch uw virtuele machines over upgradedomeinen wanneer ze worden geplaatst in een site beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="e03c8-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="e03c8-326">Lees meer over [Hallo beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e03c8-326">Read more about [managing hello availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-hello-linux-vms"></a><span data-ttu-id="e03c8-327">Hallo Linux virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="e03c8-327">Create hello Linux VMs</span></span>
<span data-ttu-id="e03c8-328">U hebt Hallo-opslag- en netwerkbronnen toosupport Internet toegankelijke VM's gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-328">You've created hello storage and network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="e03c8-329">Nu gaan we die virtuele machines maken en ze zijn beveiligd met een SSH-sleutel die geen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e03c8-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="e03c8-330">In dit geval gaan we een Ubuntu VM op basis van Hallo toocreate meest recente TNS.</span><span class="sxs-lookup"><span data-stu-id="e03c8-330">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="e03c8-331">We vinden die informatie van de installatiekopie met behulp van `azure vm image list`, zoals beschreven in [Azure VM-installatiekopieën vinden](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e03c8-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e03c8-332">We een installatiekopie van een geselecteerd met de opdracht Hallo `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-332">We selected an image by using hello command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="e03c8-333">In dit geval gebruiken we `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="e03c8-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="e03c8-334">Voor het laatste veld hello, geven we `latest` zodat in de toekomst Hallo we altijd de meest recente build Hallo gaan.</span><span class="sxs-lookup"><span data-stu-id="e03c8-334">For hello last field, we pass `latest` so that in hello future we always get hello most recent build.</span></span> <span data-ttu-id="e03c8-335">(we gebruiken Hallo-tekenreeks is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="e03c8-335">(hello string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="e03c8-336">Deze stap is bekend tooanyone die al is gemaakt door een ssh rsa openbare en persoonlijke sleutel koppelen op Linux- of Mac via **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="e03c8-336">This next step is familiar tooanyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="e03c8-337">Als u nog geen sleutelparen die een certificaat uw `~/.ssh` directory, kunt u deze maken:</span><span class="sxs-lookup"><span data-stu-id="e03c8-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="e03c8-338">Automatisch via Hallo `azure vm create --generate-ssh-keys` optie.</span><span class="sxs-lookup"><span data-stu-id="e03c8-338">Automatically, by using hello `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="e03c8-339">Handmatig met behulp van [Hallo instructies toocreate ze zelf](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e03c8-339">Manually, by using [hello instructions toocreate them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e03c8-340">U kunt ook hello gebruiken `--admin-password` methode tooauthenticate uw SSH-verbindingen na Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-340">Alternatively, you can use hello `--admin-password` method tooauthenticate your SSH connections after hello VM is created.</span></span> <span data-ttu-id="e03c8-341">Deze methode is meestal minder goed beveiligd.</span><span class="sxs-lookup"><span data-stu-id="e03c8-341">This method is typically less secure.</span></span>

<span data-ttu-id="e03c8-342">We Hallo VM maken door onze bronnen en informatie samen met de Hallo brengen `azure vm create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="e03c8-342">We create hello VM by bringing all our resources and information together with hello `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="e03c8-343">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="e03c8-344">U kunt tooyour VM direct verbinding maken met behulp van uw standaard SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="e03c8-344">You can connect tooyour VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="e03c8-345">Zorg ervoor dat u de juiste poort Hallo opgeeft omdat we via Hallo load balancer geven.</span><span class="sxs-lookup"><span data-stu-id="e03c8-345">Make sure that you specify hello appropriate port since we're passing through hello load balancer.</span></span> <span data-ttu-id="e03c8-346">(Voor onze eerste VM we ingesteld Hallo NAT regel tooforward poort 4222 tooour VM.)</span><span class="sxs-lookup"><span data-stu-id="e03c8-346">(For our first VM, we set up hello NAT rule tooforward port 4222 tooour VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="e03c8-347">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-347">Output:</span></span>

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="e03c8-348">Maak uw tweede VM in Hallo dezelfde manier:</span><span class="sxs-lookup"><span data-stu-id="e03c8-348">Go ahead and create your second VM in hello same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="e03c8-349">En u kunt nu Hallo `azure vm show myResourceGroup myVM1` opdracht tooexamine wat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-349">And you can now use hello `azure vm show myResourceGroup myVM1` command tooexamine what you've created.</span></span> <span data-ttu-id="e03c8-350">U uitvoert op dit moment uw Ubuntu VM's achter een load balancer in Azure die u aanmelden kunt bij alleen met uw SSH-sleutelpaar (omdat wachtwoorden zijn uitgeschakeld).</span><span class="sxs-lookup"><span data-stu-id="e03c8-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="e03c8-351">U kunt installeren nginx of httpd, een web-app implementeren en Zie Hallo verkeer verloopt via Hallo load balancer tooboth Hallo VM's.</span><span class="sxs-lookup"><span data-stu-id="e03c8-351">You can install nginx or httpd, deploy a web app, and see hello traffic flow through hello load balancer tooboth of hello VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="e03c8-352">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e03c8-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a><span data-ttu-id="e03c8-353">Hallo-omgeving exporteren als een sjabloon</span><span class="sxs-lookup"><span data-stu-id="e03c8-353">Export hello environment as a template</span></span>
<span data-ttu-id="e03c8-354">Nu dat u hebt gemaakt om een extra development environment Hello uit deze omgeving, wat gebeurt er als u wilt dat toocreate dezelfde parameters of een productie-omgeving die overeenkomt met het?</span><span class="sxs-lookup"><span data-stu-id="e03c8-354">Now that you have built out this environment, what if you want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="e03c8-355">Resource Manager JSON-sjablonen die alle Hallo parameters voor uw omgeving definiëren gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e03c8-355">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="e03c8-356">U maken uit de volledige omgeving door te verwijzen naar deze JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e03c8-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="e03c8-357">U kunt [handmatig JSON-sjablonen samenstellen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of een bestaande omgeving toocreate Hallo JSON-sjabloon voor u te exporteren:</span><span class="sxs-lookup"><span data-stu-id="e03c8-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="e03c8-358">Deze opdracht maakt u Hallo `myResourceGroup.json` bestand in de huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="e03c8-358">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="e03c8-359">Wanneer u een omgeving met deze sjabloon maakt, wordt u gevraagd alle Hallo resourcenamen, inclusief Hallo namen voor Hallo load balancer, netwerkinterfaces of virtuele machines op te geven.</span><span class="sxs-lookup"><span data-stu-id="e03c8-359">When you create an environment from this template, you are prompted for all hello resource names, including hello names for hello load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="e03c8-360">U kunt deze namen in uw sjabloonbestand vullen door toe te voegen Hallo `-p` of `--includeParameterDefaultValue` parameter toohello `azure group export` opdracht die eerder is aangegeven.</span><span class="sxs-lookup"><span data-stu-id="e03c8-360">You can populate these names in your template file by adding hello `-p` or `--includeParameterDefaultValue` parameter toohello `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="e03c8-361">Uw JSON-sjabloon toospecify Hallo resourcenamen, bewerken of [maken van een bestand parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) die Hallo resourcenamen aangeeft.</span><span class="sxs-lookup"><span data-stu-id="e03c8-361">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="e03c8-362">een omgeving met de sjabloon toocreate:</span><span class="sxs-lookup"><span data-stu-id="e03c8-362">toocreate an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="e03c8-363">U kunt tooread [meer over hoe u toodeploy van sjablonen](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e03c8-363">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e03c8-364">Meer informatie over hoe tooincrementally update omgevingen, parameterbestand hello gebruiken en sjablonen gebruiken vanaf een enkele opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="e03c8-364">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e03c8-365">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e03c8-365">Next steps</span></span>
<span data-ttu-id="e03c8-366">U bent nu klaar toobegin werken met meerdere netwerkonderdelen en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e03c8-366">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="e03c8-367">Kunt u dit voorbeeld omgeving toobuild out van uw toepassing met behulp van Hallo kernonderdelen geïntroduceerd hier.</span><span class="sxs-lookup"><span data-stu-id="e03c8-367">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
