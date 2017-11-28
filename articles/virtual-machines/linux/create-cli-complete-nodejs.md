---
title: Een volledige Linux-omgeving maken met de Azure CLI 1.0 | Microsoft Docs
description: Maken van opslag, een Linux-VM, een virtueel netwerk en subnet, een load balancer, een NIC, een openbare IP-adres en een netwerkbeveiligingsgroep via een compleet nieuwe met behulp van de Azure CLI 1.0.
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
ms.openlocfilehash: 201ccd523e49d638ace50fbc0ffdceb705b35473
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="08a65-103">Een volledige Linux-omgeving maken met de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="08a65-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="08a65-104">In dit artikel verder gaan we met een eenvoudig netwerk met een combinatie van virtuele machines die gebruikt voor ontwikkeling en eenvoudige computing worden en een load balancer.</span><span class="sxs-lookup"><span data-stu-id="08a65-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="08a65-105">We doorlopen het proces door opdracht totdat u twee werkt, beveiligde virtuele Linux-machines waarmee u verbinding hebt van een willekeurige plaats op het Internet maken kunt.</span><span class="sxs-lookup"><span data-stu-id="08a65-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="08a65-106">Vervolgens kunt u op verplaatsen naar complexe netwerken en omgevingen.</span><span class="sxs-lookup"><span data-stu-id="08a65-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="08a65-107">Langs de manier u meer informatie over de afhankelijkheidshiërarchie of het implementatiemodel van Resource Manager u biedt en over hoeveel inschakelen biedt.</span><span class="sxs-lookup"><span data-stu-id="08a65-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="08a65-108">Nadat u hoe het systeem is gemaakt ziet, kunt u opnieuw bouwen het veel sneller met behulp van [Azure Resource Manager-sjablonen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08a65-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="08a65-109">Nadat u meer wilt hoe de onderdelen van uw omgeving bij elkaar passen weten, maken van sjablonen voor het automatiseren van hen wordt ook eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="08a65-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="08a65-110">De omgeving bevat:</span><span class="sxs-lookup"><span data-stu-id="08a65-110">The environment contains:</span></span>

* <span data-ttu-id="08a65-111">Twee virtuele machines in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="08a65-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="08a65-112">Een load balancer met een regel voor load balancing op poort 80.</span><span class="sxs-lookup"><span data-stu-id="08a65-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="08a65-113">(NSG) netwerkbeveiligingsgroepen uw virtuele machine te beveiligen tegen ongewenste verkeer.</span><span class="sxs-lookup"><span data-stu-id="08a65-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

<span data-ttu-id="08a65-114">Als u wilt deze aangepaste omgeving maken, moet u de meest recente [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in de modus Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="08a65-114">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="08a65-115">U moet ook een JSON hulpprogramma parseren.</span><span class="sxs-lookup"><span data-stu-id="08a65-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="08a65-116">In dit voorbeeld wordt [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="08a65-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="08a65-117">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="08a65-117">CLI versions to complete the task</span></span>
<span data-ttu-id="08a65-118">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="08a65-118">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="08a65-119">[Azure CLI 1.0](#quick-commands) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="08a65-119">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="08a65-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="08a65-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="08a65-121">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="08a65-121">Quick commands</span></span>
<span data-ttu-id="08a65-122">Als u nodig hebt voor de taak, de volgende sectie details snel de base-opdrachten voor het uploaden van een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="08a65-122">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="08a65-123">Meer gedetailleerde informatie en context voor elke stap vindt u in de rest van het document, te beginnen [hier](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="08a65-123">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="08a65-124">Zorg ervoor dat u hebt [de Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="08a65-124">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="08a65-125">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="08a65-125">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="08a65-126">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="08a65-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="08a65-127">De resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-127">Create the resource group.</span></span> <span data-ttu-id="08a65-128">Het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` in de `westeurope` locatie:</span><span class="sxs-lookup"><span data-stu-id="08a65-128">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="08a65-129">Controleer of de resourcegroep met behulp van de JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="08a65-129">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="08a65-130">Het opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-130">Create the storage account.</span></span> <span data-ttu-id="08a65-131">Het volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="08a65-131">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="08a65-132">(Naam van het opslagaccount moet uniek zijn, zodat uw eigen unieke naam opgeven.)</span><span class="sxs-lookup"><span data-stu-id="08a65-132">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="08a65-133">Controleer of het opslagaccount met behulp van de JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="08a65-133">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="08a65-134">Maak het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="08a65-134">Create the virtual network.</span></span> <span data-ttu-id="08a65-135">Het volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="08a65-135">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="08a65-136">Een subnet maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-136">Create a subnet.</span></span> <span data-ttu-id="08a65-137">Het volgende voorbeeld wordt een subnet met de naam `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="08a65-137">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="08a65-138">Controleer of het virtuele netwerk en subnet met behulp van de JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="08a65-138">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="08a65-139">Maak een openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="08a65-139">Create a public IP.</span></span> <span data-ttu-id="08a65-140">Het volgende voorbeeld wordt een openbaar IP-adres met de naam `myPublicIP` met de DNS-naam van `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="08a65-140">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="08a65-141">(De DNS-naam moet uniek zijn, zodat uw eigen unieke naam opgeven.)</span><span class="sxs-lookup"><span data-stu-id="08a65-141">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="08a65-142">De load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-142">Create the load balancer.</span></span> <span data-ttu-id="08a65-143">Het volgende voorbeeld wordt een load balancer met de naam `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="08a65-143">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="08a65-144">Maak een front-end-IP-adresgroep voor de load balancer, en koppel het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="08a65-144">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="08a65-145">Het volgende voorbeeld wordt een front-end-IP-adresgroep met de naam `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="08a65-145">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="08a65-146">Maak de back-end-IP-adresgroep voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="08a65-146">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="08a65-147">Het volgende voorbeeld wordt een back-end-IP-adresgroep met de naam `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="08a65-147">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="08a65-148">SSH inkomende network address translation (NAT) regels voor de load balancer maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-148">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="08a65-149">Het volgende voorbeeld maakt u twee regels van load balancer, `myLoadBalancerRuleSSH1` en `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="08a65-149">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="08a65-150">Maken van het web inkomende NAT-regels voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="08a65-150">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="08a65-151">Het volgende voorbeeld wordt een regel voor load balancer met de naam `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="08a65-151">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="08a65-152">De load balancer-test health maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-152">Create the load balancer health probe.</span></span> <span data-ttu-id="08a65-153">Het volgende voorbeeld wordt een TCP-test met de naam `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="08a65-153">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="08a65-154">Controleer of de load balancer, IP-adresgroepen en NAT-regels met behulp van de JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="08a65-154">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="08a65-155">De eerste netwerkinterfacekaart (NIC) maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-155">Create the first network interface card (NIC).</span></span> <span data-ttu-id="08a65-156">Vervang de `#####-###-###` secties met uw eigen Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="08a65-156">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="08a65-157">Uw abonnement ID wordt vermeld in de uitvoer van **jq** wanneer u de resources die u maakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-157">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="08a65-158">U kunt ook uw abonnements-ID met weergeven `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="08a65-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="08a65-159">Het volgende voorbeeld wordt een NIC met de naam `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="08a65-159">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="08a65-160">Maken van de tweede netwerkadapter.</span><span class="sxs-lookup"><span data-stu-id="08a65-160">Create the second NIC.</span></span> <span data-ttu-id="08a65-161">Het volgende voorbeeld wordt een NIC met de naam `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="08a65-161">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="08a65-162">Controleer of de twee NIC's met behulp van de JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="08a65-162">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="08a65-163">De netwerkbeveiligingsgroep maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-163">Create the network security group.</span></span> <span data-ttu-id="08a65-164">Het volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="08a65-164">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="08a65-165">Twee regels voor binnenkomende verbindingen voor de netwerkbeveiligingsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="08a65-165">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="08a65-166">Het volgende voorbeeld maakt u twee regels `myNetworkSecurityGroupRuleSSH` en `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="08a65-166">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="08a65-167">Controleer of de netwerkbeveiligingsgroep en de regels voor binnenkomende verbindingen met behulp van de JSON-parser:</span><span class="sxs-lookup"><span data-stu-id="08a65-167">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="08a65-168">De netwerkbeveiligingsgroep binden aan de twee NIC's:</span><span class="sxs-lookup"><span data-stu-id="08a65-168">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="08a65-169">De beschikbaarheidsset maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-169">Create the availability set.</span></span> <span data-ttu-id="08a65-170">Het volgende voorbeeld wordt een benoemde beschikbaarheidsset `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="08a65-170">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="08a65-171">De eerste Linux VM maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-171">Create the first Linux VM.</span></span> <span data-ttu-id="08a65-172">Het volgende voorbeeld wordt een virtuele machine met de naam `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="08a65-172">The following example creates a VM named `myVM1`:</span></span>

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

<span data-ttu-id="08a65-173">De tweede Linux VM maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-173">Create the second Linux VM.</span></span> <span data-ttu-id="08a65-174">Het volgende voorbeeld wordt een virtuele machine met de naam `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="08a65-174">The following example creates a VM named `myVM2`:</span></span>

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

<span data-ttu-id="08a65-175">Gebruik de JSON-parser om te controleren of alles die is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="08a65-175">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="08a65-176">Uw nieuwe omgeving exporteren naar een sjabloon om snel nieuwe exemplaren opnieuw te maken:</span><span class="sxs-lookup"><span data-stu-id="08a65-176">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="08a65-177">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="08a65-177">Detailed walkthrough</span></span>
<span data-ttu-id="08a65-178">De gedetailleerde stappen volgen wordt uitgelegd wat elke opdracht doet tijdens het samenstellen van buiten uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="08a65-178">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="08a65-179">Deze begrippen zijn handig als u uw eigen aangepaste omgevingen voor ontwikkeling of productie bouwen.</span><span class="sxs-lookup"><span data-stu-id="08a65-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="08a65-180">Zorg ervoor dat u hebt [de Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="08a65-180">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="08a65-181">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="08a65-181">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="08a65-182">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="08a65-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="08a65-183">Maken van resourcegroepen en locaties implementatie kiezen</span><span class="sxs-lookup"><span data-stu-id="08a65-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="08a65-184">Azure-resourcegroepen zijn logische implementatie entiteiten die bevatten informatie over de configuratie en metagegevens inschakelen van de logische beheer van de resource-implementaties.</span><span class="sxs-lookup"><span data-stu-id="08a65-184">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="08a65-185">Het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` in de `westeurope` locatie:</span><span class="sxs-lookup"><span data-stu-id="08a65-185">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="08a65-186">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-186">Output:</span></span>

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

## <a name="create-a-storage-account"></a><span data-ttu-id="08a65-187">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="08a65-187">Create a storage account</span></span>
<span data-ttu-id="08a65-188">Storage-accounts moet u voor uw VM-schijven en voor eventuele extra gegevensschijven die u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="08a65-188">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="08a65-189">U kunt storage-accounts maken bijna onmiddellijk na het maken van resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="08a65-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="08a65-190">Hier gebruiken we de `azure storage account create` opdracht, en het type opslagondersteuning die u wilt dat de locatie van het account, de resourcegroep die wordt doorgegeven bepaalt.</span><span class="sxs-lookup"><span data-stu-id="08a65-190">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="08a65-191">Het volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="08a65-191">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="08a65-192">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="08a65-193">Onze resourcegroep controleren met behulp van de `azure group show` opdracht, gebruiken we de [jq](https://stedolan.github.io/jq/) hulpprogramma samen met de `--json` Azure CLI-optie.</span><span class="sxs-lookup"><span data-stu-id="08a65-193">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="08a65-194">(U kunt **jsawk** of elke gewenste parseren van de JSON taal-bibliotheek.)</span><span class="sxs-lookup"><span data-stu-id="08a65-194">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="08a65-195">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-195">Output:</span></span>

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

<span data-ttu-id="08a65-196">Voor het onderzoeken van het opslagaccount met behulp van de CLI, moet u eerst de accountnamen en sleutels ingesteld.</span><span class="sxs-lookup"><span data-stu-id="08a65-196">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="08a65-197">Vervang de naam van het opslagaccount in het volgende voorbeeld met een naam die u kiest:</span><span class="sxs-lookup"><span data-stu-id="08a65-197">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="08a65-198">U kunt vervolgens uw storage-gegevens eenvoudig bekijken:</span><span class="sxs-lookup"><span data-stu-id="08a65-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="08a65-199">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="08a65-200">Een virtueel netwerk en subnet maken</span><span class="sxs-lookup"><span data-stu-id="08a65-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="08a65-201">Vervolgens gaat u moet maken van een virtueel netwerk in Azure en een subnet van uw virtuele machines maken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="08a65-201">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="08a65-202">Het volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet` met de `192.168.0.0/16` adresvoorvoegsel:</span><span class="sxs-lookup"><span data-stu-id="08a65-202">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="08a65-203">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-203">Output:</span></span>

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

<span data-ttu-id="08a65-204">Opnieuw, Hiermee kunt u de optie--json gebruiken `azure group show` en `jq` om te zien hoe we onze bronnen bouwen.</span><span class="sxs-lookup"><span data-stu-id="08a65-204">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="08a65-205">Nu een `storageAccounts` resource en een `virtualNetworks` resource.</span><span class="sxs-lookup"><span data-stu-id="08a65-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="08a65-206">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-206">Output:</span></span>

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

<span data-ttu-id="08a65-207">Nu gaan we maken een subnet in de `myVnet` virtueel netwerk waarin de virtuele machines zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="08a65-207">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="08a65-208">We gebruiken de `azure network vnet subnet create` opdracht samen met de resources die we al hebt gemaakt: de `myResourceGroup` resourcegroep en de `myVnet` virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="08a65-208">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="08a65-209">In het volgende voorbeeld voegen we het subnet met de naam `mySubnet` met het adres subnetvoorvoegsel van `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="08a65-209">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="08a65-210">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="08a65-211">Omdat het subnet logisch binnen het virtuele netwerk, zoeken we de informatie over het subnet met een iets andere opdracht.</span><span class="sxs-lookup"><span data-stu-id="08a65-211">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="08a65-212">De opdracht we gebruiken is `azure network vnet show`, maar we verder te onderzoeken van de JSON-uitvoer met behulp van `jq`.</span><span class="sxs-lookup"><span data-stu-id="08a65-212">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="08a65-213">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-213">Output:</span></span>

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

## <a name="create-a-public-ip-address"></a><span data-ttu-id="08a65-214">Een openbaar IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="08a65-214">Create a public IP address</span></span>
<span data-ttu-id="08a65-215">Nu gaan we het openbare IP-adres (PIP) die we aan de load balancer toewijzen maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-215">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="08a65-216">Hiermee kunt u verbinding maken met uw virtuele machines van het Internet met behulp van de `azure network public-ip create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="08a65-216">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="08a65-217">Omdat het standaardadres dynamisch is, maken we een benoemde DNS-vermelding in de **cloudapp.azure.com** domein met behulp van de `--domain-name-label` optie.</span><span class="sxs-lookup"><span data-stu-id="08a65-217">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="08a65-218">Het volgende voorbeeld wordt een openbaar IP-adres met de naam `myPublicIP` met de DNS-naam van `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="08a65-218">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="08a65-219">Omdat de DNS-naam moet uniek zijn, kunt u uw eigen unieke DNS-naam opgeven:</span><span class="sxs-lookup"><span data-stu-id="08a65-219">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="08a65-220">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
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

<span data-ttu-id="08a65-221">Het openbare IP-adres is ook een bron op het hoogste niveau, zodat u deze met ziet `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="08a65-221">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="08a65-222">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-222">Output:</span></span>

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

<span data-ttu-id="08a65-223">U kunt meer informatie over resource, zoals de volledig gekwalificeerde domeinnaam (FQDN) van het subdomein, met behulp van de volledige onderzoeken `azure network public-ip show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="08a65-223">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="08a65-224">Het openbare IP-adres resource logisch is toegewezen, maar een specifiek adres nog niet is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="08a65-224">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="08a65-225">Als u een IP-adres, gaat u moet een load balancer die we nog geen hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-225">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="08a65-226">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-226">Output:</span></span>

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

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="08a65-227">Een load balancer en IP-adresgroepen maken</span><span class="sxs-lookup"><span data-stu-id="08a65-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="08a65-228">Wanneer u een load balancer maakt, kunt u verkeer verdelen over meerdere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="08a65-228">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="08a65-229">Het biedt redundantie voor uw toepassingen ook door het uitvoeren van meerdere virtuele machines die op aanvragen van gebruikers in het geval van onderhoud of zware belasting reageren.</span><span class="sxs-lookup"><span data-stu-id="08a65-229">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="08a65-230">Het volgende voorbeeld wordt een load balancer met de naam `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="08a65-230">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="08a65-231">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="08a65-232">De load balancer is redelijk leeg, dus gaan we een aantal IP-adresgroepen maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="08a65-233">We willen maken van twee IP-adresgroepen voor de load balancer, één voor de front-end en één voor de back-end.</span><span class="sxs-lookup"><span data-stu-id="08a65-233">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="08a65-234">De front-end-IP-adresgroep is openbaar zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="08a65-234">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="08a65-235">Het is ook de locatie waarop we de PIP die we eerder hebben gemaakt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="08a65-235">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="08a65-236">Vervolgens gebruiken we de back-end-pool als locatie voor de virtuele machines verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="08a65-236">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="08a65-237">Op die manier het verkeer door de load balancer naar de virtuele machines kan stromen.</span><span class="sxs-lookup"><span data-stu-id="08a65-237">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="08a65-238">Eerst laten we onze front-end-IP-adresgroep maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="08a65-239">Het volgende voorbeeld wordt een front-groep met de naam `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="08a65-239">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="08a65-240">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="08a65-241">Houd er rekening mee hoe we gebruikt de `--public-ip-name` switch door te geven de `myPublicIP` die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-241">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="08a65-242">Het openbare IP-adres toewijzen aan de load balancer, kunt u uw virtuele machines worden bereikt via Internet.</span><span class="sxs-lookup"><span data-stu-id="08a65-242">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="08a65-243">Vervolgens maken we onze tweede IP-adresgroep voor de back-end-verkeer.</span><span class="sxs-lookup"><span data-stu-id="08a65-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="08a65-244">Het volgende voorbeeld wordt een back-end-pool met de naam `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="08a65-244">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="08a65-245">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="08a65-246">We zien hoe u onze load balancer doet door te zoeken met `azure network lb show` en onderzoeken van de JSON-uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="08a65-247">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-247">Output:</span></span>

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

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="08a65-248">NAT-regels van load balancer maken</span><span class="sxs-lookup"><span data-stu-id="08a65-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="08a65-249">Als u verkeer via de load balancer, moeten we network address translation (NAT) regels maken die binnenkomend of uitgaand acties opgeven.</span><span class="sxs-lookup"><span data-stu-id="08a65-249">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="08a65-250">U kunt het te gebruiken protocol opgeven en vervolgens externe poorten naar interne poorten desgewenst toewijzen.</span><span class="sxs-lookup"><span data-stu-id="08a65-250">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="08a65-251">Voor onze omgeving gaan we een aantal regels maken die SSH toestaan via onze load balancer naar de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="08a65-251">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="08a65-252">We instellen TCP-poorten 4222 en 4223 om om te leiden TCP-poort 22 op onze virtuele machines (die we later maken).</span><span class="sxs-lookup"><span data-stu-id="08a65-252">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="08a65-253">Het volgende voorbeeld wordt een regel met naam `myLoadBalancerRuleSSH1` TCP-poort 4222 toewijzen aan poort 22:</span><span class="sxs-lookup"><span data-stu-id="08a65-253">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="08a65-254">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
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

<span data-ttu-id="08a65-255">Herhaal de procedure voor de tweede NAT-regel voor SSH.</span><span class="sxs-lookup"><span data-stu-id="08a65-255">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="08a65-256">Het volgende voorbeeld wordt een regel met naam `myLoadBalancerRuleSSH2` TCP-poort 4223 toewijzen aan poort 22:</span><span class="sxs-lookup"><span data-stu-id="08a65-256">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="08a65-257">We gaan ook opwekken en maak een NAT-regel voor TCP-poort 80 voor internetverkeer, de regel aansluiting tot onze IP-adresgroepen.</span><span class="sxs-lookup"><span data-stu-id="08a65-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="08a65-258">Als we de regel moet een IP-adresgroep, in plaats van een afzonderlijk, een regel aan onze VMs aansluiting aansluiten kunt we toevoegen of verwijderen van virtuele machines van de IP-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="08a65-258">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="08a65-259">De load balancer wordt automatisch de verkeersstroom aangepast.</span><span class="sxs-lookup"><span data-stu-id="08a65-259">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="08a65-260">Het volgende voorbeeld wordt een regel met naam `myLoadBalancerRuleWeb` TCP-poort 80 om toe te wijzen poort 80:</span><span class="sxs-lookup"><span data-stu-id="08a65-260">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="08a65-261">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
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

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="08a65-262">Een load balancer health test maken</span><span class="sxs-lookup"><span data-stu-id="08a65-262">Create a load balancer health probe</span></span>
<span data-ttu-id="08a65-263">Een health test regelmatig controles op de virtuele machines die zich achter de load balancer om te controleren of ze zijn het functioneren en reageren op aanvragen, zoals is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="08a65-263">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="08a65-264">Als dat niet het geval is, moet u ze zijn verwijderd uit de bewerking om ervoor te zorgen dat gebruikers worden niet omgeleid naar deze.</span><span class="sxs-lookup"><span data-stu-id="08a65-264">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="08a65-265">U kunt aangepaste controles voor de health-test, samen met intervallen en time-outwaarden definiëren.</span><span class="sxs-lookup"><span data-stu-id="08a65-265">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="08a65-266">Zie voor meer informatie over statuscontroles [Load Balancer-tests](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08a65-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="08a65-267">Het volgende voorbeeld wordt een TCP health aangeduid met de naam `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="08a65-267">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="08a65-268">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="08a65-269">Hier wordt een interval van 15 seconden voor onze statuscontroles opgegeven.</span><span class="sxs-lookup"><span data-stu-id="08a65-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="08a65-270">We kunnen maximaal vier tests (één minuut) voordat de load balancer van oordeel is dat de host niet meer werkt over het hoofd ziet.</span><span class="sxs-lookup"><span data-stu-id="08a65-270">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="08a65-271">Controleer of de load balancer</span><span class="sxs-lookup"><span data-stu-id="08a65-271">Verify the load balancer</span></span>
<span data-ttu-id="08a65-272">Nu wordt de load balancer-configuratie gedaan.</span><span class="sxs-lookup"><span data-stu-id="08a65-272">Now the load balancer configuration is done.</span></span> <span data-ttu-id="08a65-273">Hier volgen de stappen die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="08a65-273">Here are the steps you took:</span></span>

1. <span data-ttu-id="08a65-274">U hebt gemaakt voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="08a65-274">You created a load balancer.</span></span>
2. <span data-ttu-id="08a65-275">U een front-end-IP-adresgroep gemaakt en een openbare IP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="08a65-275">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="08a65-276">U een back-end-IP-adresgroep die virtuele machines verbinding met maken kunnen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="08a65-277">U NAT-regels waarmee SSH kunt uitvoeren naar de virtuele machines voor beheer, samen met een regel waarmee u TCP-poort 80 voor de web-app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-277">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="08a65-278">U hebt een health test geregeld wordt gecontroleerd of de virtuele machines toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="08a65-278">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="08a65-279">Deze test health zorgt ervoor dat gebruikers niet probeert te krijgen tot een virtuele machine die niet meer werkt of inhoud.</span><span class="sxs-lookup"><span data-stu-id="08a65-279">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="08a65-280">We bekijken wat de load balancer er nu uit:</span><span class="sxs-lookup"><span data-stu-id="08a65-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="08a65-281">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-281">Output:</span></span>

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

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="08a65-282">Maken van een NIC voor gebruik met de Linux-VM</span><span class="sxs-lookup"><span data-stu-id="08a65-282">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="08a65-283">NIC's zijn programmatisch beschikbaar omdat u regels toepassen op het gebruik ervan kunt.</span><span class="sxs-lookup"><span data-stu-id="08a65-283">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="08a65-284">U kunt ook meer dan één hebben.</span><span class="sxs-lookup"><span data-stu-id="08a65-284">You can also have more than one.</span></span> <span data-ttu-id="08a65-285">In de volgende `azure network nic create` opdracht u aansluiten op de NIC de belasting backend-IP-adresgroep en deze koppelen aan de NAT-regel SSH-verkeer toestaan.</span><span class="sxs-lookup"><span data-stu-id="08a65-285">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="08a65-286">Vervang de `#####-###-###` secties met uw eigen Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="08a65-286">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="08a65-287">Uw abonnement ID wordt vermeld in de uitvoer van `jq` wanneer u de resources die u maakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-287">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="08a65-288">U kunt ook uw abonnements-ID met weergeven `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="08a65-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="08a65-289">Het volgende voorbeeld wordt een NIC met de naam `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="08a65-289">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="08a65-290">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
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

<span data-ttu-id="08a65-291">U ziet de details vindt u rechtstreeks van de resource.</span><span class="sxs-lookup"><span data-stu-id="08a65-291">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="08a65-292">Bestuderen van de resource met behulp van de `azure network nic show` opdracht:</span><span class="sxs-lookup"><span data-stu-id="08a65-292">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="08a65-293">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-293">Output:</span></span>

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

<span data-ttu-id="08a65-294">Nu maken we de tweede Netwerkinterfacekaart, in aansluiting bij onze backend-IP-adresgroep opnieuw.</span><span class="sxs-lookup"><span data-stu-id="08a65-294">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="08a65-295">Deze tijd de tweede NAT-regel toestaat SSH verkeer.</span><span class="sxs-lookup"><span data-stu-id="08a65-295">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="08a65-296">Het volgende voorbeeld wordt een NIC met de naam `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="08a65-296">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="08a65-297">Een netwerkbeveiligingsgroep en regels maken</span><span class="sxs-lookup"><span data-stu-id="08a65-297">Create a network security group and rules</span></span>
<span data-ttu-id="08a65-298">We maken nu een netwerkbeveiligingsgroep en de regels voor binnenkomende verbindingen die voor de toegang tot de NIC.</span><span class="sxs-lookup"><span data-stu-id="08a65-298">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="08a65-299">Een netwerkbeveiligingsgroep kan worden toegepast op een NIC of een subnet.</span><span class="sxs-lookup"><span data-stu-id="08a65-299">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="08a65-300">Definieert u regels voor het beheren van de stroom van verkeer van en naar uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="08a65-300">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="08a65-301">Het volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="08a65-301">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="08a65-302">Laten we de inkomende regel voor het NSG aan het toestaan van binnenkomende verbindingen op poort 22 (voor ondersteuning van SSH) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="08a65-302">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="08a65-303">Het volgende voorbeeld wordt een regel met naam `myNetworkSecurityGroupRuleSSH` om TCP op poort 22 te staan:</span><span class="sxs-lookup"><span data-stu-id="08a65-303">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="08a65-304">Nu gaan we de binnenkomende regel voor het NSG aan het toestaan van binnenkomende verbindingen op poort 80 (voor ondersteuning webverkeer) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="08a65-304">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="08a65-305">Het volgende voorbeeld wordt een regel met naam `myNetworkSecurityGroupRuleHTTP` om TCP op poort 80 te staan:</span><span class="sxs-lookup"><span data-stu-id="08a65-305">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="08a65-306">De binnenkomende regel is een filter naar binnenkomende netwerkverbindingen.</span><span class="sxs-lookup"><span data-stu-id="08a65-306">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="08a65-307">In dit voorbeeld binden we het NSG aan de virtuele NIC van virtuele machines, wat betekent dat elk verzoek poort 22 wordt doorgegeven aan de NIC op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="08a65-307">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="08a65-308">Deze regel binnenkomende over een netwerkverbinding is en niet over een eindpunt met dit is wat het normaal zou zijn over in klassieke implementaties.</span><span class="sxs-lookup"><span data-stu-id="08a65-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="08a65-309">Als u wilt een poort opent, moet u laat de `--source-port-range` ingesteld op '\*' (de standaardwaarde) te accepteren van binnenkomende aanvragen van **eventuele** poort aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="08a65-309">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="08a65-310">Poorten zijn meestal dynamisch zijn.</span><span class="sxs-lookup"><span data-stu-id="08a65-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="08a65-311">Verbinding maken met de NIC</span><span class="sxs-lookup"><span data-stu-id="08a65-311">Bind to the NIC</span></span>
<span data-ttu-id="08a65-312">Het NSG binden aan de NIC's.</span><span class="sxs-lookup"><span data-stu-id="08a65-312">Bind the NSG to the NICs.</span></span> <span data-ttu-id="08a65-313">Moeten we onze NIC's een verbinding maakt met onze netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="08a65-313">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="08a65-314">Voer beide opdrachten, koppelt u beide onze NIC's:</span><span class="sxs-lookup"><span data-stu-id="08a65-314">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="08a65-315">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="08a65-315">Create an availability set</span></span>
<span data-ttu-id="08a65-316">Beschikbaarheidssets help verspreiding uw virtuele machines in domeinen met fouten en upgradedomeinen.</span><span class="sxs-lookup"><span data-stu-id="08a65-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="08a65-317">Laten we de beschikbaarheidsset voor uw virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="08a65-318">Het volgende voorbeeld wordt een benoemde beschikbaarheidsset `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="08a65-318">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="08a65-319">Domeinen met fouten definiëren een groepering van virtuele machines die een gemeenschappelijk power-bron- en switch delen.</span><span class="sxs-lookup"><span data-stu-id="08a65-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="08a65-320">Standaard worden de virtuele machines die worden geconfigureerd in de beschikbaarheidsset gescheiden over maximaal drie domeinen met fouten.</span><span class="sxs-lookup"><span data-stu-id="08a65-320">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="08a65-321">Het idee is een hardwareprobleem in een van deze domeinen met fouten heeft geen invloed op elke virtuele machine die uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="08a65-321">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="08a65-322">Virtuele machines verdeelt Azure automatisch over de domeinen met fouten wanneer ze worden geplaatst in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="08a65-322">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="08a65-323">Upgradedomeinen duiden op groepen van virtuele machines en de onderliggende fysieke hardware die op hetzelfde moment kan worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="08a65-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="08a65-324">De volgorde waarin upgradedomeinen worden opgestart mogelijk geen opeenvolgende tijdens gepland onderhoud, maar slechts één upgrade opnieuw wordt opgestart tegelijk.</span><span class="sxs-lookup"><span data-stu-id="08a65-324">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="08a65-325">Opnieuw verdeelt Azure automatisch uw virtuele machines over upgradedomeinen wanneer ze worden geplaatst in een site beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="08a65-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="08a65-326">Lees meer over [het beheren van de beschikbaarheid van virtuele machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08a65-326">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="08a65-327">De virtuele Linux-machines maken</span><span class="sxs-lookup"><span data-stu-id="08a65-327">Create the Linux VMs</span></span>
<span data-ttu-id="08a65-328">U kunt de opslag- en netwerkbronnen ter ondersteuning van Internet toegankelijke VM's hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-328">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="08a65-329">Nu gaan we die virtuele machines maken en ze zijn beveiligd met een SSH-sleutel die geen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="08a65-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="08a65-330">In dit geval gaan we een Ubuntu VM op basis van de meest recente TNS maken.</span><span class="sxs-lookup"><span data-stu-id="08a65-330">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="08a65-331">We vinden die informatie van de installatiekopie met behulp van `azure vm image list`, zoals beschreven in [Azure VM-installatiekopieën vinden](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08a65-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="08a65-332">We een installatiekopie van een geselecteerd met de opdracht `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="08a65-332">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="08a65-333">In dit geval gebruiken we `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="08a65-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="08a65-334">Voor het laatste veld, geven we `latest` zodat in de toekomst kunnen we de meest recente build altijd beschikken.</span><span class="sxs-lookup"><span data-stu-id="08a65-334">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="08a65-335">(De tekenreeks we gebruiken `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="08a65-335">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="08a65-336">Deze stap is vertrouwd voor iedereen die al is gemaakt door een ssh rsa openbare en persoonlijke sleutel koppelen op Linux- of Mac via **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="08a65-336">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="08a65-337">Als u nog geen sleutelparen die een certificaat uw `~/.ssh` directory, kunt u deze maken:</span><span class="sxs-lookup"><span data-stu-id="08a65-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="08a65-338">Automatisch, met behulp van de `azure vm create --generate-ssh-keys` optie.</span><span class="sxs-lookup"><span data-stu-id="08a65-338">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="08a65-339">Handmatig met behulp van [de instructies voor het zelf maken](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08a65-339">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="08a65-340">U kunt ook de `--admin-password` methode voor het verifiëren van uw SSH-verbindingen nadat de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-340">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="08a65-341">Deze methode is meestal minder goed beveiligd.</span><span class="sxs-lookup"><span data-stu-id="08a65-341">This method is typically less secure.</span></span>

<span data-ttu-id="08a65-342">We de virtuele machine maken door brengen onze bronnen en informatie samen met de `azure vm create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="08a65-342">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

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

<span data-ttu-id="08a65-343">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="08a65-344">U kunt verbinding maken met uw virtuele machine onmiddellijk met behulp van uw standaard SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="08a65-344">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="08a65-345">Zorg ervoor dat u de juiste poort opgeeft omdat we via de load balancer geven.</span><span class="sxs-lookup"><span data-stu-id="08a65-345">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="08a65-346">(Voor onze eerste VM we instellen de NAT-regel voor het doorsturen van poort 4222 voor onze VM.)</span><span class="sxs-lookup"><span data-stu-id="08a65-346">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="08a65-347">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-347">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="08a65-348">Opwekken en maak uw tweede virtuele machine op dezelfde manier:</span><span class="sxs-lookup"><span data-stu-id="08a65-348">Go ahead and create your second VM in the same manner:</span></span>

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

<span data-ttu-id="08a65-349">En u kunt nu de `azure vm show myResourceGroup myVM1` opdracht om te onderzoeken wat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08a65-349">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="08a65-350">U uitvoert op dit moment uw Ubuntu VM's achter een load balancer in Azure die u aanmelden kunt bij alleen met uw SSH-sleutelpaar (omdat wachtwoorden zijn uitgeschakeld).</span><span class="sxs-lookup"><span data-stu-id="08a65-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="08a65-351">U kunt nginx of httpd installeren, een web-app implementeren en het verkeer verloopt via de load balancer op beide van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="08a65-351">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="08a65-352">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="08a65-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
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


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="08a65-353">De omgeving exporteren als een sjabloon</span><span class="sxs-lookup"><span data-stu-id="08a65-353">Export the environment as a template</span></span>
<span data-ttu-id="08a65-354">Nu dat u hebt gemaakt uit deze omgeving, wat gebeurt er als u wilt maken van een extra development environment met dezelfde parameters of een productie-omgeving die overeenkomt met het?</span><span class="sxs-lookup"><span data-stu-id="08a65-354">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="08a65-355">Resource Manager gebruikt de JSON-sjablonen op dat de parameters voor uw omgeving definiëren.</span><span class="sxs-lookup"><span data-stu-id="08a65-355">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="08a65-356">U maken uit de volledige omgeving door te verwijzen naar deze JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="08a65-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="08a65-357">U kunt [handmatig JSON-sjablonen samenstellen](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of een bestaande omgeving voor het maken van het JSON-sjabloon voor u te exporteren:</span><span class="sxs-lookup"><span data-stu-id="08a65-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="08a65-358">Deze opdracht maakt u de `myResourceGroup.json` bestand in de huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="08a65-358">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="08a65-359">Wanneer u een omgeving met deze sjabloon maakt, wordt u gevraagd alle de resourcenamen, met inbegrip van de namen voor de load balancer, netwerkinterfaces of virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="08a65-359">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="08a65-360">U kunt deze namen in uw sjabloonbestand vullen door toe te voegen de `-p` of `--includeParameterDefaultValue` -parameter voor de `azure group export` opdracht die eerder is aangegeven.</span><span class="sxs-lookup"><span data-stu-id="08a65-360">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="08a65-361">Bewerk uw JSON-sjabloon om op te geven van de resourcenamen van de of [maken van een bestand parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) die Hiermee worden de resourcenamen.</span><span class="sxs-lookup"><span data-stu-id="08a65-361">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="08a65-362">Een omgeving maken van uw sjabloon:</span><span class="sxs-lookup"><span data-stu-id="08a65-362">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="08a65-363">U wilt lezen [meer over het implementeren van sjablonen](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08a65-363">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="08a65-364">Meer informatie over hoe u stapsgewijs omgevingen bijwerken, gebruikt u het parameterbestand en toegang tot sjablonen vanaf één locatie.</span><span class="sxs-lookup"><span data-stu-id="08a65-364">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08a65-365">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08a65-365">Next steps</span></span>
<span data-ttu-id="08a65-366">U nu kunt aan de slag met meerdere netwerkonderdelen en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="08a65-366">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="08a65-367">Voor het bouwen van uw toepassing met behulp van de belangrijkste onderdelen die zijn geïntroduceerd hier kunt u deze Voorbeeldomgeving.</span><span class="sxs-lookup"><span data-stu-id="08a65-367">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
