---
title: Open poorten voor een Linux-VM met Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over het openen van een poort / maken van een eindpunt voor uw Linux-VM met behulp van het implementatiemodel van Azure resource manager en de Azure CLI 1.0
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
ms.openlocfilehash: 847bc76c37ed929851712ba1c12463a01032e267
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="opening-ports-and-endpoints-to-a-linux-vm-in-azure-using-the-azure-cli-10"></a><span data-ttu-id="43b8a-103">Openen van poorten en eindpunten voor een Linux-VM in Azure met behulp van de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="43b8a-103">Opening ports and endpoints to a Linux VM in Azure using the Azure CLI 1.0</span></span>
<span data-ttu-id="43b8a-104">U opent een poort of een eindpunt met een virtuele machine (VM) in Azure maken met het maken van een netwerk-filter op een subnet of een VM-netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="43b8a-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="43b8a-105">U kunt deze filters die binnenkomend en uitgaand verkeer worden beheerd, plaatsen op een Netwerkbeveiligingsgroep gekoppeld aan de resource die het verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="43b8a-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="43b8a-106">We gebruiken een voorbeeld van webverkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="43b8a-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="43b8a-107">In dit artikel leest u hoe een poort voor een virtuele machine moet worden geopend met behulp van de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="43b8a-107">This article shows you how to open a port to a VM using the Azure CLI 1.0.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="43b8a-108">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="43b8a-108">CLI versions to complete the task</span></span>
<span data-ttu-id="43b8a-109">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="43b8a-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="43b8a-110">[Azure CLI 1.0](#quick-commands) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="43b8a-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="43b8a-111">[Azure CLI 2.0](nsg-quickstart.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="43b8a-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="43b8a-112">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="43b8a-112">Quick commands</span></span>
<span data-ttu-id="43b8a-113">Maken van een Netwerkbeveiligingsgroep en regels u moet [de Azure CLI 1.0](../../cli-install-nodejs.md) geïnstalleerd en met Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="43b8a-113">To create a Network Security Group and rules you need [the Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="43b8a-114">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="43b8a-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="43b8a-115">Voorbeeld parameternamen opgenomen *myResourceGroup*, *myNetworkSecurityGroup*, en *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="43b8a-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="43b8a-116">Maak de beveiligingsgroep van uw netwerk, invoeren van uw eigen namen en de locatie op de juiste wijze.</span><span class="sxs-lookup"><span data-stu-id="43b8a-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="43b8a-117">Het volgende voorbeeld wordt een Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup* in de *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="43b8a-117">The following example creates a Network Security Group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="43b8a-118">Een regel voor het toestaan van HTTP-verkeer naar uw webserver (of aanpassen voor uw eigen scenario, zoals SSH-toegang of database connectivity) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="43b8a-118">Add a rule to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="43b8a-119">Het volgende voorbeeld wordt een regel met naam *myNetworkSecurityGroupRule* TCP-verkeer op poort 80 toestaan:</span><span class="sxs-lookup"><span data-stu-id="43b8a-119">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

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

<span data-ttu-id="43b8a-120">De Netwerkbeveiligingsgroep koppelen aan uw VM-netwerkinterface (NIC).</span><span class="sxs-lookup"><span data-stu-id="43b8a-120">Associate the Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="43b8a-121">Het volgende voorbeeld wordt gekoppeld aan een bestaande NIC met de naam *myNic* met de netwerk-beveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="43b8a-121">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="43b8a-122">U kunt ook uw Netwerkbeveiligingsgroep koppelen met een virtueel netwerksubnet in plaats van alleen aan de netwerkinterface op een enkele virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="43b8a-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="43b8a-123">Het volgende voorbeeld wordt een bestaand subnet met de naam *mySubnet* in de *myVnet* virtueel netwerk met de Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="43b8a-123">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="43b8a-124">Meer informatie over Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="43b8a-124">More information on Network Security Groups</span></span>
<span data-ttu-id="43b8a-125">De snelle opdrachten hier kunt u aan de slag te kunnen met verkeer naar uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="43b8a-125">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="43b8a-126">Netwerkbeveiligingsgroepen bieden veel handige functies en granulatie voor het beheren van toegang tot uw resources.</span><span class="sxs-lookup"><span data-stu-id="43b8a-126">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="43b8a-127">U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="43b8a-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="43b8a-128">U kunt Netwerkbeveiligingsgroepen en ACL-regels definiëren als onderdeel van Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="43b8a-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="43b8a-129">Lees meer over [Netwerkbeveiligingsgroepen maken met behulp van sjablonen](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="43b8a-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="43b8a-130">Als u gebruiken poort-doorsturen wilt naar een unieke externe poort toewijzen aan een interne poort op de virtuele machine, gebruikt u een load balancer en Network Address Translation (NAT)-regels.</span><span class="sxs-lookup"><span data-stu-id="43b8a-130">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="43b8a-131">U wilt bijvoorbeeld TCP-poort 8080 extern beschikbaar en hebt verkeer op TCP-poort 80 op een virtuele machine wordt gestuurd.</span><span class="sxs-lookup"><span data-stu-id="43b8a-131">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="43b8a-132">U kunt meer informatie over [maken van een Internet gerichte load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="43b8a-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43b8a-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43b8a-133">Next steps</span></span>
<span data-ttu-id="43b8a-134">In dit voorbeeld moet u een eenvoudige regel zodat HTTP-verkeer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="43b8a-134">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="43b8a-135">Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="43b8a-135">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="43b8a-136">Overzicht van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="43b8a-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="43b8a-137">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="43b8a-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="43b8a-138">Overzicht van Azure Resource Manager voor Load Balancers</span><span class="sxs-lookup"><span data-stu-id="43b8a-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

