---
title: aaaOpen poorten tooa Linux-VM met Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over hoe een poort tooopen / maken van een eindpunt tooyour Linux-VM met hello Azure resource manager deployment model en hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="8462e-103">Openen van poorten en eindpunten tooa Linux VM Hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8462e-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="8462e-104">U een poort openen of maken van een eindpunt tooa virtuele machine (VM) in Azure door het maken van een netwerk-filter op een subnet of een VM-netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="8462e-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="8462e-105">U plaatsen deze filters die binnenkomend en uitgaand verkeer worden beheerd, van een Netwerkbeveiligingsgroep gekoppeld toohello resource die Hallo verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="8462e-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="8462e-106">We gebruiken een voorbeeld van webverkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="8462e-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="8462e-107">Dit artikel ziet u hoe tooopen een poort tooa VM Hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="8462e-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="8462e-108">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8462e-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="8462e-109">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="8462e-109">Quick commands</span></span>
<span data-ttu-id="8462e-110">toocreate een netwerkbeveiliging en regels u moet recente Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8462e-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="8462e-111">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="8462e-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8462e-112">De namen van de voorbeeld-parameter *myResourceGroup*, *myNetworkSecurityGroup*, en *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="8462e-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="8462e-113">Maken van de netwerkbeveiligingsgroep met Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="8462e-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="8462e-114">Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="8462e-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="8462e-115">Toevoegen van een regel met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) tooallow HTTP verkeer tooyour webserver (of aanpassen voor uw eigen scenario, zoals SSH-toegang of database connectivity).</span><span class="sxs-lookup"><span data-stu-id="8462e-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="8462e-116">Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRule* tooallow TCP-verkeer op poort 80:</span><span class="sxs-lookup"><span data-stu-id="8462e-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="8462e-117">Hallo Netwerkbeveiligingsgroep koppelen aan uw VM-netwerkinterface (NIC) met [az netwerk nic update](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="8462e-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="8462e-118">Hallo volgende voorbeeld wordt gekoppeld aan een bestaande NIC met de naam *myNic* Hello Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8462e-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="8462e-119">U kunt ook uw Netwerkbeveiligingsgroep koppelen aan een virtueel netwerksubnet met [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) in plaats van alleen toohello netwerkinterface op een enkele virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8462e-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="8462e-120">Hallo volgende voorbeeld wordt een bestaand subnet met de naam *mySubnet* in Hallo *myVnet* virtueel netwerk met Hallo Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8462e-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8462e-121">Meer informatie over Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="8462e-121">More information on Network Security Groups</span></span>
<span data-ttu-id="8462e-122">Hallo-hier snelle opdrachten kunt u tooget up en wordt uitgevoerd met verkeer stromende tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="8462e-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="8462e-123">Netwerkbeveiligingsgroepen bieden veel handige functies en verfijning voor het beheren van toegang tot tooyour bronnen.</span><span class="sxs-lookup"><span data-stu-id="8462e-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="8462e-124">U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="8462e-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="8462e-125">Voor maximaal beschikbare webtoepassingen, moet u uw virtuele machines achter een Load Balancer van Azure plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8462e-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="8462e-126">Hallo-taakverdeling verkeer tooVMs, met een Netwerkbeveiligingsgroep waarmee wordt verkeer gefilterd.</span><span class="sxs-lookup"><span data-stu-id="8462e-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="8462e-127">Zie voor meer informatie [hoe tooload saldo Linux virtuele machines in Azure toocreate een maximaal beschikbare toepassing](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8462e-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8462e-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8462e-128">Next steps</span></span>
<span data-ttu-id="8462e-129">In dit voorbeeld moet u een eenvoudige regel tooallow HTTP-verkeer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8462e-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="8462e-130">Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8462e-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="8462e-131">Overzicht van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8462e-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8462e-132">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="8462e-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
