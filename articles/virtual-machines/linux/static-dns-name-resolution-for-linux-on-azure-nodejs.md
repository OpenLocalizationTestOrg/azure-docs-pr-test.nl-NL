---
title: aaaUsing interne DNS voor de virtuele machine naamomzetting in Azure | Microsoft Docs
description: Interne DNS gebruiken voor naamomzetting van de virtuele machine in Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="53322-103">Met behulp van de interne DNS voor naamomzetting van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="53322-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="53322-104">Dit artikel laat zien hoe tooset statische interne DNS-namen voor virtuele Linux-machines met virtuele NIC kaarten (VNic) en DNS-labelnamen.</span><span class="sxs-lookup"><span data-stu-id="53322-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="53322-105">Statische DNS-namen worden gebruikt voor permanente infrastructuurservices zoals een Jenkins build-server, die wordt gebruikt voor dit document of een Git-server.</span><span class="sxs-lookup"><span data-stu-id="53322-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="53322-106">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="53322-106">hello requirements are:</span></span>

* [<span data-ttu-id="53322-107">een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="53322-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="53322-108">bestanden voor openbare en persoonlijke SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="53322-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="53322-109">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="53322-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="53322-110">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="53322-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="53322-111">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="53322-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="53322-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="53322-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="53322-113">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="53322-113">Quick commands</span></span>

<span data-ttu-id="53322-114">Als u moet tooquickly Hallo taak, Hallo sectie volgen details Hallo opdrachten die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="53322-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="53322-115">Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="53322-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="53322-116">Randvoorwaarden voor: Resourcegroep, VNet, NSG met SSH inkomende Subnet.</span><span class="sxs-lookup"><span data-stu-id="53322-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="53322-117">Een VNic maken met een statische interne DNS-naam</span><span class="sxs-lookup"><span data-stu-id="53322-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="53322-118">Hallo `-r` cli-vlag is voor instelling Hallo DNS-label, waardoor Hallo statische DNS-naam voor Hallo VNic.</span><span class="sxs-lookup"><span data-stu-id="53322-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="53322-119">Hallo VM in Hallo VNet, NSG en implementeert, verbinding maken met de Hallo VNic</span><span class="sxs-lookup"><span data-stu-id="53322-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="53322-120">Hallo `-N` hello VNic toohello verbindt nieuwe virtuele machine tijdens Hallo implementatie tooAzure.</span><span class="sxs-lookup"><span data-stu-id="53322-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="53322-121">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="53322-121">Detailed walkthrough</span></span>

<span data-ttu-id="53322-122">Een volledige continue integratie en continue implementatie (CiCd) infrastructuur in Azure bepaalde servers toobe statisch of lange levensduur hebben servers vereist.</span><span class="sxs-lookup"><span data-stu-id="53322-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="53322-123">Het verdient aanbeveling dat Azure activa zoals Hallo virtuele netwerken (vnet's) en Netwerkbeveiligingsgroepen (nsg's), mag niet statisch en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.</span><span class="sxs-lookup"><span data-stu-id="53322-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="53322-124">Zodra een VNet is geïmplementeerd, kan opnieuw door nieuwe implementaties zonder een nadelige invloed toohello infrastructuur worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="53322-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="53322-125">Toe te voegen toothis statische netwerk een Git biedt repository server en een Jenkins automation-server CiCd tooyour ontwikkel- of testomgevingen.</span><span class="sxs-lookup"><span data-stu-id="53322-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="53322-126">Interne DNS-namen zijn alleen omgezet in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="53322-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="53322-127">Omdat Hallo DNS-namen interne zijn, zijn ze niet worden omgezet toohello buiten internet, zodat u extra beveiliging toohello infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="53322-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="53322-128">_Vervang geen voorbeelden door uw eigen namen._</span><span class="sxs-lookup"><span data-stu-id="53322-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="53322-129">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="53322-129">Create hello Resource group</span></span>

<span data-ttu-id="53322-130">Een resourcegroep benodigde tooorganize is alles wat er in dit scenario worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="53322-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="53322-131">Zie voor meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="53322-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="53322-132">Hallo VNet maken</span><span class="sxs-lookup"><span data-stu-id="53322-132">Create hello VNet</span></span>

<span data-ttu-id="53322-133">de eerste stap Hallo is toobuild een VNet-toolaunch Hallo VM's in.</span><span class="sxs-lookup"><span data-stu-id="53322-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="53322-134">Hallo VNet bevat één subnet voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="53322-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="53322-135">Zie voor meer informatie over Azure VNets [een virtueel netwerk maken met behulp van hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="53322-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="53322-136">Hallo NSG maken</span><span class="sxs-lookup"><span data-stu-id="53322-136">Create hello NSG</span></span>

<span data-ttu-id="53322-137">Hallo Subnet is gebouwd achter een bestaande Netwerkbeveiligingsgroep zodat wij Hallo NSG voordat Hallo Subnet bouwen.</span><span class="sxs-lookup"><span data-stu-id="53322-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="53322-138">Azure nsg's zijn equivalent tooa firewall op Hallo netwerklaag.</span><span class="sxs-lookup"><span data-stu-id="53322-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="53322-139">Zie voor meer informatie over Azure nsg's [hoe toocreate nsg's in Azure CLI Hallo](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="53322-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="53322-140">Regel voor geven van een binnenkomende SSH toevoegen</span><span class="sxs-lookup"><span data-stu-id="53322-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="53322-141">Hallo Linux VM moet toegang vanaf Hallo internet zodat een regel voor het toestaan van binnenkomende poort 22 verkeer toobe Hallo netwerk tooport 22 op Hallo Linux VM doorgegeven nodig is.</span><span class="sxs-lookup"><span data-stu-id="53322-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="53322-142">Voeg een subnet toohello VNet</span><span class="sxs-lookup"><span data-stu-id="53322-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="53322-143">Virtuele machines binnen Hallo VNet moeten zich bevinden in een subnet.</span><span class="sxs-lookup"><span data-stu-id="53322-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="53322-144">Elke VNet kan meerdere subnetten hebben.</span><span class="sxs-lookup"><span data-stu-id="53322-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="53322-145">Hallo subnet maken en Hallo subnet koppelen aan Hallo NSG tooadd een firewall toohello subnet.</span><span class="sxs-lookup"><span data-stu-id="53322-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="53322-146">Hallo Subnet is nu toegevoegd in Hallo VNet en die zijn gekoppeld aan het NSG hello en Hallo NSG regel.</span><span class="sxs-lookup"><span data-stu-id="53322-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="53322-147">Statische DNS-namen maken</span><span class="sxs-lookup"><span data-stu-id="53322-147">Creating static DNS names</span></span>

<span data-ttu-id="53322-148">Azure is zeer flexibel, maar toouse DNS-namen voor de naamomzetting voor virtuele machines, moet u ze als virtuele (VNics netwerkkaarten) met behulp van DNS-labels toocreate.</span><span class="sxs-lookup"><span data-stu-id="53322-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="53322-149">VNics zijn belangrijk omdat u deze hergebruiken kunt door deze te verbinden toodifferent virtuele machines, blijft Hallo VNic als statische resource Hallo VMs tijdelijke kan zijn.</span><span class="sxs-lookup"><span data-stu-id="53322-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="53322-150">Met behulp van DNS op Hallo VNic labels, zijn we kunnen tooenable eenvoudige naamomzetting van andere virtuele machines in Hallo VNet.</span><span class="sxs-lookup"><span data-stu-id="53322-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="53322-151">Andere virtuele machines tooaccess Hallo-automatiseringsserver met Hallo DNS-naam met omgezette namen kan `Jenkins` of Hallo Git-server als `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="53322-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="53322-152">Een VNic maken en deze koppelen aan een Subnet wordt gemaakt in de vorige stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="53322-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="53322-153">Hallo VM in Hallo VNet en NSG implementeren</span><span class="sxs-lookup"><span data-stu-id="53322-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="53322-154">We hebben nu een VNet, een subnet in dit VNet en een NSG fungeert als een firewall tooprotect onze subnet door alle binnenkomend verkeer behalve poort 22 voor SSH blokkeren.</span><span class="sxs-lookup"><span data-stu-id="53322-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="53322-155">Hallo VM kan nu worden geïmplementeerd in deze bestaande netwerkinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="53322-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="53322-156">Met behulp van Azure CLI Hallo en Hallo `azure vm create` opdracht Hallo Linux VM geïmplementeerde toohello bestaande Azure-resourcegroep, VNet Subnet en VNic is.</span><span class="sxs-lookup"><span data-stu-id="53322-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="53322-157">Zie voor meer informatie over het gebruik van Hallo CLI toodeploy een volledige virtuele machine [een volledige Linux-omgeving maken met behulp van hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="53322-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="53322-158">Met behulp van Hallo vlaggen CLI toocall uit bestaande resources we Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo instrueren.</span><span class="sxs-lookup"><span data-stu-id="53322-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="53322-159">tooreiterate, zodra een VNet en een subnet is geïmplementeerd, kunnen ze worden gelaten als statisch of permanente resources binnen uw Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="53322-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="53322-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="53322-160">Next steps</span></span>
* [<span data-ttu-id="53322-161">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="53322-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="53322-162">Linux-VM in Azure met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="53322-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
