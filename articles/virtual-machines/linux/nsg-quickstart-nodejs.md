---
title: aaaOpen poorten tooa Linux-VM met Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe een poort tooopen / maken van een eindpunt tooyour Linux-VM met hello Azure resource manager deployment model en Azure CLI 1.0 Hallo
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="0c5a0-103">Openen poorten en eindpunten tooa Linux VM aan Azure met Azure CLI 1.0 Hallo</span><span class="sxs-lookup"><span data-stu-id="0c5a0-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="0c5a0-104">U een poort openen of maken van een eindpunt tooa virtuele machine (VM) in Azure door het maken van een netwerk-filter op een subnet of een VM-netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="0c5a0-105">U plaatsen deze filters die binnenkomend en uitgaand verkeer worden beheerd, van een Netwerkbeveiligingsgroep gekoppeld toohello resource die Hallo verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="0c5a0-106">We gebruiken een voorbeeld van webverkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="0c5a0-107">Dit artikel laat zien hoe een poort tooa VM met tooopen hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0c5a0-108">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="0c5a0-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="0c5a0-109">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0c5a0-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="0c5a0-110">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="0c5a0-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0c5a0-111">[Azure CLI 2.0](nsg-quickstart.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="0c5a0-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="0c5a0-112">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="0c5a0-112">Quick commands</span></span>
<span data-ttu-id="0c5a0-113">een Netwerkbeveiligingsgroep toocreate en regels moet u [hello Azure CLI 1.0](../../cli-install-nodejs.md) geïnstalleerd en met Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="0c5a0-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="0c5a0-114">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0c5a0-115">Voorbeeld parameternamen opgenomen *myResourceGroup*, *myNetworkSecurityGroup*, en *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="0c5a0-116">Maak de beveiligingsgroep van uw netwerk, invoeren van uw eigen namen en de locatie op de juiste wijze.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="0c5a0-117">Hallo volgende voorbeeld wordt een Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="0c5a0-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="0c5a0-118">Een regel tooallow HTTP-verkeer tooyour webserver toevoegen (of aanpassen voor uw eigen scenario, zoals SSH-toegang of database connectivity).</span><span class="sxs-lookup"><span data-stu-id="0c5a0-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="0c5a0-119">Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRule* tooallow TCP-verkeer op poort 80:</span><span class="sxs-lookup"><span data-stu-id="0c5a0-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="0c5a0-120">Hallo Netwerkbeveiligingsgroep koppelen aan uw VM-netwerkinterface (NIC).</span><span class="sxs-lookup"><span data-stu-id="0c5a0-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="0c5a0-121">Hallo volgende voorbeeld wordt gekoppeld aan een bestaande NIC met de naam *myNic* Hello Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="0c5a0-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="0c5a0-122">U kunt ook uw Netwerkbeveiligingsgroep koppelen aan een virtueel netwerksubnet in plaats van alleen toohello netwerkinterface op een enkele virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="0c5a0-123">Hallo volgende voorbeeld wordt een bestaand subnet met de naam *mySubnet* in Hallo *myVnet* virtueel netwerk met Hallo Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="0c5a0-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="0c5a0-124">Meer informatie over Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="0c5a0-124">More information on Network Security Groups</span></span>
<span data-ttu-id="0c5a0-125">Hallo-hier snelle opdrachten kunt u tooget up en wordt uitgevoerd met verkeer stromende tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="0c5a0-126">Netwerkbeveiligingsgroepen bieden veel handige functies en verfijning voor het beheren van toegang tot tooyour bronnen.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="0c5a0-127">U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0c5a0-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="0c5a0-128">U kunt Netwerkbeveiligingsgroepen en ACL-regels definiëren als onderdeel van Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="0c5a0-129">Lees meer over [Netwerkbeveiligingsgroepen maken met behulp van sjablonen](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="0c5a0-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="0c5a0-130">Als u toouse poort doorsturen toomap een unieke externe poort tooan interne poort op de virtuele machine moet, gebruikt u een load balancer en Network Address Translation (NAT)-regels.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="0c5a0-131">U kunt bijvoorbeeld tooexpose TCP-poort 8080 extern wilt en verkeer wordt gestuurd tooTCP poort 80 op een virtuele machine hebben.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="0c5a0-132">U kunt meer informatie over [maken van een Internet gerichte load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0c5a0-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c5a0-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c5a0-133">Next steps</span></span>
<span data-ttu-id="0c5a0-134">In dit voorbeeld moet u een eenvoudige regel tooallow HTTP-verkeer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0c5a0-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="0c5a0-135">Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0c5a0-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="0c5a0-136">Overzicht van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0c5a0-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="0c5a0-137">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="0c5a0-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="0c5a0-138">Overzicht van Azure Resource Manager voor Load Balancers</span><span class="sxs-lookup"><span data-stu-id="0c5a0-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

