---
title: aaaAzure virtuele netwerken en virtuele Linux-Machines | Microsoft Docs
description: Zelfstudie - beheert virtuele Azure-netwerken en virtuele Linux-Machines met hello Azure CLI
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="1247e-103">Azure virtuele netwerken en virtuele Linux-Machines beheren met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1247e-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="1247e-104">Azure netwerken virtuele Azure-machines gebruiken voor interne en externe communicatie.</span><span class="sxs-lookup"><span data-stu-id="1247e-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="1247e-105">Deze zelfstudie wordt begeleid twee virtuele machines implementeren en configureren van Azure netwerken voor deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1247e-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="1247e-106">Hallo-voorbeelden in deze zelfstudie wordt ervan uitgegaan dat Hallo virtuele machines als host voor een webtoepassing met een database back-end optreden, maar een toepassing niet is geïmplementeerd in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1247e-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="1247e-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="1247e-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1247e-108">Een virtueel netwerk implementeren</span><span class="sxs-lookup"><span data-stu-id="1247e-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="1247e-109">Een subnet binnen een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="1247e-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="1247e-110">Virtuele machines tooa subnet koppelen</span><span class="sxs-lookup"><span data-stu-id="1247e-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="1247e-111">Virtuele machine openbare IP-adressen beheren</span><span class="sxs-lookup"><span data-stu-id="1247e-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="1247e-112">Binnenkomend internetverkeer beveiligen</span><span class="sxs-lookup"><span data-stu-id="1247e-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="1247e-113">Beveiliging van verkeer van de VM-tooVM</span><span class="sxs-lookup"><span data-stu-id="1247e-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1247e-114">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="1247e-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1247e-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="1247e-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1247e-116">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1247e-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="1247e-117">Overzicht van VM-netwerken</span><span class="sxs-lookup"><span data-stu-id="1247e-117">VM networking overview</span></span>

<span data-ttu-id="1247e-118">Virtuele netwerken van Azure inschakelen van beveiligde netwerkverbindingen tussen virtuele machines, Hallo internet en andere Azure-services zoals Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="1247e-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="1247e-119">Virtuele netwerken zijn onderverdeeld in logische segmenten subnetten genoemd.</span><span class="sxs-lookup"><span data-stu-id="1247e-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="1247e-120">Subnetten gebruikt toocontrol netwerk flow, en als een beveiligingsgrens.</span><span class="sxs-lookup"><span data-stu-id="1247e-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="1247e-121">Bij het implementeren van een virtuele machine, omvat het doorgaans de virtuele netwerkinterface, gekoppelde tooa subnet.</span><span class="sxs-lookup"><span data-stu-id="1247e-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="1247e-122">Virtueel netwerk implementeren</span><span class="sxs-lookup"><span data-stu-id="1247e-122">Deploy virtual network</span></span>

<span data-ttu-id="1247e-123">Voor deze zelfstudie wordt één virtueel netwerk met twee subnetten gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1247e-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="1247e-124">Een front-end-subnet voor het hosten van een webtoepassing en een back-end-subnet voor het hosten van een database-server.</span><span class="sxs-lookup"><span data-stu-id="1247e-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="1247e-125">Voordat u een virtueel netwerk maken kunt, maakt u een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1247e-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1247e-126">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myRGNetwork* op Hallo eastus locatie.</span><span class="sxs-lookup"><span data-stu-id="1247e-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="1247e-127">Virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="1247e-127">Create virtual network</span></span>

<span data-ttu-id="1247e-128">Ons Hallo [az network vnet maken](/cli/azure/network/vnet#create) opdracht toocreate een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="1247e-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="1247e-129">In dit voorbeeld Hallo netwerk heet *mvVnet* en krijgt een adresvoorvoegsel van *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="1247e-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="1247e-130">Een subnet wordt ook gemaakt met de naam *mySubnetFrontEnd* en het voorvoegsel *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="1247e-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="1247e-131">Verderop in deze zelfstudie is een front-virtuele machine verbonden toothis subnet.</span><span class="sxs-lookup"><span data-stu-id="1247e-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="1247e-132">Subnet maken</span><span class="sxs-lookup"><span data-stu-id="1247e-132">Create subnet</span></span>

<span data-ttu-id="1247e-133">Een nieuw subnet is toegevoegd toohello virtueel netwerk met behulp van Hallo [az network vnet subnet maken](/cli/azure/network/vnet/subnet#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1247e-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="1247e-134">In dit voorbeeld Hallo subnet heet *mySubnetBackEnd* en krijgt een adresvoorvoegsel van *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="1247e-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="1247e-135">Dit subnet wordt gebruikt met alle back-end-services.</span><span class="sxs-lookup"><span data-stu-id="1247e-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="1247e-136">Op dit moment is een netwerk gemaakt en gesegmenteerde in twee subnetten, één voor de front-end-services en een andere voor back-end-services.</span><span class="sxs-lookup"><span data-stu-id="1247e-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="1247e-137">In de volgende sectie hello, virtuele machines worden gemaakt en verbonden toothese subnetten.</span><span class="sxs-lookup"><span data-stu-id="1247e-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="1247e-138">Openbaar IP-adres begrijpen</span><span class="sxs-lookup"><span data-stu-id="1247e-138">Understand public IP address</span></span>

<span data-ttu-id="1247e-139">Een openbaar IP-adres kan Azure-resources toobe toegankelijk is op Hallo van internet.</span><span class="sxs-lookup"><span data-stu-id="1247e-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="1247e-140">Een virtuele machine wordt in deze sectie van de zelfstudie Hallo toodemonstrate hoe toowork met openbare IP-adressen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1247e-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="1247e-141">Toewijzingsmethode</span><span class="sxs-lookup"><span data-stu-id="1247e-141">Allocation method</span></span>

<span data-ttu-id="1247e-142">Een openbaar IP-adres kan worden toegewezen als dynamische of statische.</span><span class="sxs-lookup"><span data-stu-id="1247e-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="1247e-143">Openbaar IP-adres is standaard dynamisch toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1247e-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="1247e-144">Dynamische IP-adressen worden vrijgegeven wanneer een virtuele machine toewijzing ongedaan wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1247e-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="1247e-145">Dit gedrag zorgt ervoor dat Hallo IP-adres toochange tijdens een bewerking met een VM toewijzing is opgeheven.</span><span class="sxs-lookup"><span data-stu-id="1247e-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="1247e-146">Hallo-toewijzingsmethode toostatic, kan worden ingesteld tooa virtuele machine, zelfs tijdens de status van een toewijzing ongedaan is gemaakt waardoor wordt gegarandeerd dat Hallo IP-adres blijven worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1247e-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="1247e-147">Wanneer u een statisch toegewezen IP-adres, kan niet Hallo IP-adres zelf worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1247e-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="1247e-148">Het wordt toegewezen uit een groep met beschikbare adressen.</span><span class="sxs-lookup"><span data-stu-id="1247e-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="1247e-149">Dynamische toewijzing</span><span class="sxs-lookup"><span data-stu-id="1247e-149">Dynamic allocation</span></span>

<span data-ttu-id="1247e-150">Bij het maken van een virtuele machine met Hallo [az vm maken](/cli/azure/vm#create) opdracht Hallo standaard openbare IP-adres toewijzingsmethode is dynamisch.</span><span class="sxs-lookup"><span data-stu-id="1247e-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="1247e-151">In Hallo voorbeeld te volgen, wordt een virtuele machine gemaakt met een dynamische IP-adres.</span><span class="sxs-lookup"><span data-stu-id="1247e-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="1247e-152">Statische toewijzing</span><span class="sxs-lookup"><span data-stu-id="1247e-152">Static allocation</span></span>

<span data-ttu-id="1247e-153">Bij het maken van een virtuele machine met Hallo [az vm maken](/cli/azure/vm#create) opdracht, opnemen Hallo `--public-ip-address-allocation static` argument tooassign statisch openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="1247e-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="1247e-154">Deze bewerking wordt niet gedemonstreerd in deze zelfstudie echter in Hallo volgende sectie een dynamisch toegewezen IP-adres wordt gewijzigd tooa statisch toegewezen adres.</span><span class="sxs-lookup"><span data-stu-id="1247e-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="1247e-155">Toewijzingsmethode wijzigen</span><span class="sxs-lookup"><span data-stu-id="1247e-155">Change allocation method</span></span>

<span data-ttu-id="1247e-156">Hallo IP-adres toewijzingsmethode kan worden gewijzigd met Hallo [az netwerk openbare ip-update](/cli/azure/network/public-ip#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1247e-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="1247e-157">Hallo methode voor de toewijzing van IP-adressen van Hallo front-VM wordt gewijzigd in dit voorbeeld toostatic.</span><span class="sxs-lookup"><span data-stu-id="1247e-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="1247e-158">Ten eerste toewijzing Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1247e-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="1247e-159">Gebruik Hallo [az netwerk openbare ip-update](/cli/azure/network/public-ip#update) opdracht tooupdate Hallo toewijzingsmethode.</span><span class="sxs-lookup"><span data-stu-id="1247e-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="1247e-160">In dit geval Hallo `--allocation-method` te wordt ingesteld*statische*.</span><span class="sxs-lookup"><span data-stu-id="1247e-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="1247e-161">Hallo VM start.</span><span class="sxs-lookup"><span data-stu-id="1247e-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="1247e-162">Er is geen openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="1247e-162">No public IP address</span></span>

<span data-ttu-id="1247e-163">Vaak een virtuele machine hoeft niet toobe toegankelijk zijn via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="1247e-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="1247e-164">een virtuele machine zonder een openbaar IP-adres, gebruik Hallo toocreate `--public-ip-address ""` argument met een lege set dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="1247e-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="1247e-165">Deze configuratie wordt later in deze zelfstudie gedemonstreerd</span><span class="sxs-lookup"><span data-stu-id="1247e-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="1247e-166">Netwerkverkeer beveiligen</span><span class="sxs-lookup"><span data-stu-id="1247e-166">Secure network traffic</span></span>

<span data-ttu-id="1247e-167">Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor toestaan of weigeren netwerkverkeer tooresources verbonden tooAzure virtuele netwerken (VNet).</span><span class="sxs-lookup"><span data-stu-id="1247e-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="1247e-168">Nsg's kunnen worden gekoppeld toosubnets of afzonderlijke netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="1247e-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="1247e-169">Wanneer u een NSG is gekoppeld aan een netwerkinterface, dit is alleen van toepassing hello VM die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1247e-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="1247e-170">Wanneer een NSG gekoppeld tooa subnet is, Hallo regels van toepassing tooall bronnen verbonden toohello subnet.</span><span class="sxs-lookup"><span data-stu-id="1247e-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="1247e-171">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="1247e-171">Network security group rules</span></span>

<span data-ttu-id="1247e-172">NSG-regels definiëren netwerken poorten waarover verkeer wordt toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="1247e-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="1247e-173">Hallo-regels kunnen bron en doel-IP-adresbereiken bevatten, zodat verkeer wordt geregeld tussen specifieke systemen of subnetten.</span><span class="sxs-lookup"><span data-stu-id="1247e-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="1247e-174">NSG-regels bevatten ook een prioriteit (tussen 1- en 4096).</span><span class="sxs-lookup"><span data-stu-id="1247e-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="1247e-175">Regels worden in volgorde van prioriteit Hallo geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="1247e-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="1247e-176">Een regel met een prioriteit van 100 wordt geëvalueerd voor een regel met prioriteit 200.</span><span class="sxs-lookup"><span data-stu-id="1247e-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="1247e-177">Alle NSG's bevatten een set met standaardregels.</span><span class="sxs-lookup"><span data-stu-id="1247e-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="1247e-178">Hallo-standaardregels kunnen niet worden verwijderd, maar omdat ze de laagste prioriteit Hallo zijn toegewezen, kunnen ze worden overschreven door het Hallo-regels die u maakt.</span><span class="sxs-lookup"><span data-stu-id="1247e-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="1247e-179">**Virtueel netwerk** - die afkomstig zijn van verkeer en eindigt in een virtueel netwerk is toegestaan beide kanten van binnenkomend en uitgaand.</span><span class="sxs-lookup"><span data-stu-id="1247e-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="1247e-180">**Internet** - uitgaand verkeer is toegestaan, maar dat binnenkomend verkeer wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="1247e-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="1247e-181">**De load balancer** -toestaan Azure load balancer tooprobe Hallo status van uw VM's en rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="1247e-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="1247e-182">Als u een set met gelijke taakverdeling niet gebruikt, kunt u deze regel onderdrukken.</span><span class="sxs-lookup"><span data-stu-id="1247e-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="1247e-183">Netwerk-beveiligingsgroepen maken</span><span class="sxs-lookup"><span data-stu-id="1247e-183">Create network security groups</span></span>

<span data-ttu-id="1247e-184">Een netwerkbeveiligingsgroep kan worden gemaakt op Hallo dezelfde tijd als een virtuele machine met behulp van Hallo [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1247e-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="1247e-185">Wanneer doet, Hallo NSG is gekoppeld aan de netwerkinterface Hallo-VM's en een NSG-regel is automatisch gemaakt tooallow verkeer op poort *22* van elke bron.</span><span class="sxs-lookup"><span data-stu-id="1247e-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="1247e-186">Eerder in deze zelfstudie Hallo Hallo front-NSG is automatisch gemaakt met de front-VM.</span><span class="sxs-lookup"><span data-stu-id="1247e-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="1247e-187">Een regel voor het NSG is ook automatisch gemaakt voor poort 22.</span><span class="sxs-lookup"><span data-stu-id="1247e-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="1247e-188">In sommige gevallen kan zijn handig toopre-een NSG, zoals wanneer SSH standaardregels mogen niet worden gemaakt of wanneer Hallo NSG gekoppelde tooa subnet moet maken.</span><span class="sxs-lookup"><span data-stu-id="1247e-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="1247e-189">Gebruik Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create) opdracht toocreate een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="1247e-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="1247e-190">In plaats van het koppelen van Hallo NSG tooa netwerkinterface is gekoppeld aan een subnet.</span><span class="sxs-lookup"><span data-stu-id="1247e-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="1247e-191">In deze configuratie worden overgenomen elke virtuele machine die is aangesloten toohello subnet Hallo NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="1247e-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="1247e-192">Bijwerken van bestaande Hallo-subnet met de naam *mySubnetBackEnd* met nieuwe NSG Hallo.</span><span class="sxs-lookup"><span data-stu-id="1247e-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="1247e-193">Maak nu een virtuele machine, die aangesloten toohello is *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="1247e-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="1247e-194">U ziet dat Hallo `--nsg` argument heeft de waarde leeg dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="1247e-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="1247e-195">Een NSG is niet gemaakt met de Hallo VM toobe nodig.</span><span class="sxs-lookup"><span data-stu-id="1247e-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="1247e-196">Hallo VM is aangesloten toohello back-end-subnet, waardoor Hello vooraf gemaakte back-end NSG wordt beveiligd.</span><span class="sxs-lookup"><span data-stu-id="1247e-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="1247e-197">Deze NSG geldt toohello VM.</span><span class="sxs-lookup"><span data-stu-id="1247e-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="1247e-198">Hier ziet ook dat Hallo `--public-ip-address` argument heeft de waarde leeg dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="1247e-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="1247e-199">Deze configuratie maakt u een virtuele machine zonder een openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="1247e-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="1247e-200">Binnenkomend verkeer beveiligen</span><span class="sxs-lookup"><span data-stu-id="1247e-200">Secure incoming traffic</span></span>

<span data-ttu-id="1247e-201">Wanneer hello front-virtuele machine is gemaakt, is een regel voor het NSG tooallow binnenkomend verkeer op poort 22 gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1247e-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="1247e-202">Deze regel kunnen de SSH-verbindingen toohello VM.</span><span class="sxs-lookup"><span data-stu-id="1247e-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="1247e-203">In dit voorbeeld moet ook verkeer op poort worden toegestaan *80*.</span><span class="sxs-lookup"><span data-stu-id="1247e-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="1247e-204">Deze configuratie kunt een web application toobe geopend op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1247e-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="1247e-205">Gebruik Hallo [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) opdracht toocreate een regel voor de poort *80*.</span><span class="sxs-lookup"><span data-stu-id="1247e-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="1247e-206">Hallo front-end VM nu alleen toegankelijk is op poort *22* en poort *80*.</span><span class="sxs-lookup"><span data-stu-id="1247e-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="1247e-207">Alle binnenkomend verkeer wordt geblokkeerd op Hallo netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="1247e-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="1247e-208">Het wellicht handig toovisualize hello NSG regel configuraties.</span><span class="sxs-lookup"><span data-stu-id="1247e-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="1247e-209">Retour Hallo NSG regelconfiguratie Hello [az netwerk Regellijst](/cli/azure/network/nsg/rule#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1247e-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="1247e-210">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1247e-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="1247e-211">Beveiliging van verkeer van de VM-tooVM</span><span class="sxs-lookup"><span data-stu-id="1247e-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="1247e-212">Netwerkbeveiligingsgroepen kunnen ook tussen VM's toepassen.</span><span class="sxs-lookup"><span data-stu-id="1247e-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="1247e-213">In dit voorbeeld Hallo Hallo front-end VM moet toocommunicate met back-end-VM op poort *22* en *3306*.</span><span class="sxs-lookup"><span data-stu-id="1247e-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="1247e-214">Met deze configuratie kan SSH-verbindingen van Hallo front-VM en ook toestaan dat een toepassing op Hallo toocommunicate met betrekking tot een front-VM met een back-end MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="1247e-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="1247e-215">Al het andere verkeer moet worden geblokkeerd tussen Hallo front-end en back-end virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1247e-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="1247e-216">Gebruik Hallo [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) opdracht toocreate een regel voor poort 22.</span><span class="sxs-lookup"><span data-stu-id="1247e-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="1247e-217">U ziet dat Hallo `--source-address-prefix` geeft een waarde van argument *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="1247e-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="1247e-218">Deze configuratie zorgt ervoor dat alleen verkeer van de front-end-subnet Hallo door Hallo NSG wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="1247e-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="1247e-219">Nu een regel voor MySQL-verkeer op poort 3306 toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1247e-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="1247e-220">Ten slotte omdat nsg's een standaard-regel waarmee hebben alle verkeer tussen virtuele machines in Hallo hetzelfde VNet, een regel kan worden gemaakt voor Hallo back-end nsg's tooblock al het verkeer.</span><span class="sxs-lookup"><span data-stu-id="1247e-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="1247e-221">U ziet hier dat Hallo `--priority` krijgt een waarde van *300*, die is lager dat beide Hallo NSG en MySQL-regels.</span><span class="sxs-lookup"><span data-stu-id="1247e-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="1247e-222">Deze configuratie zorgt ervoor dat verkeer van SSH en MySQL nog steeds door Hallo NSG wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="1247e-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="1247e-223">Hallo back-end VM nu alleen toegankelijk is op poort *22* en poort *3306* van Hallo front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="1247e-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="1247e-224">Alle binnenkomend verkeer wordt geblokkeerd op Hallo netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="1247e-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="1247e-225">Het wellicht handig toovisualize hello NSG regel configuraties.</span><span class="sxs-lookup"><span data-stu-id="1247e-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="1247e-226">Retour Hallo NSG regelconfiguratie Hello [az netwerk Regellijst](/cli/azure/network/nsg/rule#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1247e-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="1247e-227">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1247e-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="1247e-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1247e-228">Next steps</span></span>

<span data-ttu-id="1247e-229">In deze zelfstudie hebt gemaakt en Azure-netwerken als verwante toovirtual machines beveiligd.</span><span class="sxs-lookup"><span data-stu-id="1247e-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="1247e-230">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="1247e-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1247e-231">Een virtueel netwerk implementeren</span><span class="sxs-lookup"><span data-stu-id="1247e-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="1247e-232">Een subnet binnen een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="1247e-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="1247e-233">Virtuele machines tooa subnet koppelen</span><span class="sxs-lookup"><span data-stu-id="1247e-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="1247e-234">Virtuele machine openbare IP-adressen beheren</span><span class="sxs-lookup"><span data-stu-id="1247e-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="1247e-235">Binnenkomend internetverkeer beveiligen</span><span class="sxs-lookup"><span data-stu-id="1247e-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="1247e-236">Beveiliging van verkeer van de VM-tooVM</span><span class="sxs-lookup"><span data-stu-id="1247e-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="1247e-237">Ga toohello volgende zelfstudie toolearn over het beveiligen van gegevens op virtuele machines met Azure backup.</span><span class="sxs-lookup"><span data-stu-id="1247e-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1247e-238">Back-up van Linux virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="1247e-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
