---
title: aaaUse interne DNS voor de virtuele machine naamomzetting Hello Azure CLI 2.0 | Microsoft Docs
description: Hoe het virtuele netwerk toocreate netwerkinterfacekaarten en interne DNS gebruiken voor VM-naamomzetting in Azure met Azure CLI 2.0 Hallo
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="b5381-103">Maken van virtuele netwerkinterfacekaarten en interne DNS gebruiken voor naamomzetting van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="b5381-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="b5381-104">Dit artikel laat zien hoe tooset statische interne DNS-namen voor virtuele Linux-machines met virtual network netwerkinterfacekaarten (vNics) en DNS-labelnamen Hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b5381-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="b5381-105">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5381-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b5381-106">Statische DNS-namen worden gebruikt voor permanente infrastructuurservices zoals een Jenkins build-server, die wordt gebruikt voor dit document of een Git-server.</span><span class="sxs-lookup"><span data-stu-id="b5381-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="b5381-107">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="b5381-107">hello requirements are:</span></span>

* [<span data-ttu-id="b5381-108">een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="b5381-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="b5381-109">bestanden voor openbare en persoonlijke SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="b5381-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="b5381-110">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="b5381-110">Quick commands</span></span>
<span data-ttu-id="b5381-111">Als u moet tooquickly Hallo taak, Hallo sectie volgen details Hallo opdrachten die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="b5381-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="b5381-112">Meer gedetailleerde informatie en context voor elke stap u in de rest Hallo van Hallo document vindt [vanaf hier](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b5381-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="b5381-113">tooperform deze stappen, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b5381-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b5381-114">Randvoorwaarden voor: Resourcegroep, virtueel netwerk en subnet, Netwerkbeveiligingsgroep met SSH voor binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="b5381-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="b5381-115">Maken van een virtuele netwerkadapter met een statische interne DNS-naam</span><span class="sxs-lookup"><span data-stu-id="b5381-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="b5381-116">Maken van Hallo vNic met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b5381-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="b5381-117">Hallo `--internal-dns-name` CLI-vlag is voor instelling Hallo DNS-label, waardoor Hallo statische DNS-naam voor Hallo virtuele netwerkinterfacekaart (vNic).</span><span class="sxs-lookup"><span data-stu-id="b5381-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="b5381-118">Hallo volgende voorbeeld wordt een vNic met de naam `myNic`, verbonden toohello `myVnet` virtueel netwerk, en maakt een interne DNS-naam-record genoemd `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="b5381-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="b5381-119">Een virtuele machine implementeert en verbinden van Hallo vNic</span><span class="sxs-lookup"><span data-stu-id="b5381-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="b5381-120">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b5381-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b5381-121">Hallo `--nics` vlag Hallo vNic toohello VM tijdens Hallo implementatie tooAzure verbindt.</span><span class="sxs-lookup"><span data-stu-id="b5381-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="b5381-122">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` met Azure beheerd schijven en wordt Hallo vNic met de naam `myNic` van Hallo vóór stap:</span><span class="sxs-lookup"><span data-stu-id="b5381-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b5381-123">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="b5381-123">Detailed walkthrough</span></span>

<span data-ttu-id="b5381-124">Een volledige continue integratie en continue implementatie (CiCd) infrastructuur in Azure bepaalde servers toobe statisch of lange levensduur hebben servers vereist.</span><span class="sxs-lookup"><span data-stu-id="b5381-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="b5381-125">Het verdient aanbeveling dat Azure activa zoals Hallo virtuele netwerken en Netwerkbeveiligingsgroepen statisch zijn en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.</span><span class="sxs-lookup"><span data-stu-id="b5381-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="b5381-126">Zodra een virtueel netwerk is geïmplementeerd, kan opnieuw door nieuwe implementaties zonder een nadelige invloed toohello infrastructuur worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b5381-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="b5381-127">U kunt later een Git-opslagplaatsserver toevoegen of een automatiseringsserver Jenkins biedt CiCd toothis virtueel netwerk voor uw ontwikkel- of testomgevingen.</span><span class="sxs-lookup"><span data-stu-id="b5381-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="b5381-128">Interne DNS-namen zijn alleen omgezet in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="b5381-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="b5381-129">Omdat Hallo DNS-namen interne zijn, zijn ze niet worden omgezet toohello buiten internet, zodat u extra beveiliging toohello infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="b5381-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="b5381-130">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="b5381-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b5381-131">De namen van de voorbeeld-parameter `myResourceGroup`, `myNic`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="b5381-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="b5381-132">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="b5381-132">Create hello resource group</span></span>
<span data-ttu-id="b5381-133">Maak eerst de resourcegroep Hallo met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b5381-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b5381-134">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westus` locatie:</span><span class="sxs-lookup"><span data-stu-id="b5381-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="b5381-135">Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="b5381-135">Create hello virtual network</span></span>

<span data-ttu-id="b5381-136">de volgende stap Hallo is toobuild een virtueel netwerk toolaunch Hallo VM's in.</span><span class="sxs-lookup"><span data-stu-id="b5381-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="b5381-137">Hallo virtueel netwerk bevat één subnet voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="b5381-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="b5381-138">Zie voor meer informatie over virtuele netwerken van Azure [een virtueel netwerk maken met behulp van Azure CLI Hallo](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5381-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="b5381-139">Virtueel netwerk met Hallo maken [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="b5381-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="b5381-140">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet` en subnet met de naam `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="b5381-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="b5381-141">Hallo Netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="b5381-141">Create hello Network Security Group</span></span>
<span data-ttu-id="b5381-142">Beveiligingsgroepen voor Azure-netwerk zijn equivalent tooa firewall op Hallo netwerklaag.</span><span class="sxs-lookup"><span data-stu-id="b5381-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="b5381-143">Zie voor meer informatie over Netwerkbeveiligingsgroepen [hoe toocreate nsg's in Azure CLI Hallo](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5381-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="b5381-144">Maken van de netwerkbeveiligingsgroep met Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="b5381-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="b5381-145">Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="b5381-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="b5381-146">Een inkomende regel tooallow SSH toevoegen</span><span class="sxs-lookup"><span data-stu-id="b5381-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="b5381-147">Toevoegen van een inkomende regel voor de netwerkbeveiligingsgroep Hallo met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="b5381-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="b5381-148">Hallo volgende voorbeeld maakt u een regel met naam `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="b5381-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="b5381-149">Hallo subnet koppelen aan Hallo Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="b5381-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="b5381-150">tooassociate hello subnet Hello Netwerkbeveiligingsgroep, gebruiken [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="b5381-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="b5381-151">Hallo volgende voorbeeld wordt de subnetnaam hello `mySubnet` Hello Netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="b5381-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="b5381-152">Hallo virtuele netwerkinterfacekaart en statische DNS-namen maken</span><span class="sxs-lookup"><span data-stu-id="b5381-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="b5381-153">Azure is zeer flexibel, maar toouse DNS-namen voor naamomzetting van de virtuele machine, moet u toocreate virtuele netwerkinterfacekaarten (vNics) met een DNS-label.</span><span class="sxs-lookup"><span data-stu-id="b5381-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="b5381-154">vNics zijn belangrijk omdat u deze hergebruiken kunt door deze te verbinden toodifferent VM's via Hallo infrastructuur levenscyclus.</span><span class="sxs-lookup"><span data-stu-id="b5381-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="b5381-155">Deze aanpak houdt Hallo vNic als statische resource Hallo VMs tijdelijke kan zijn.</span><span class="sxs-lookup"><span data-stu-id="b5381-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="b5381-156">Met behulp van DNS op Hallo vNic labels, zijn we kunnen tooenable eenvoudige naamomzetting van andere virtuele machines in Hallo VNet.</span><span class="sxs-lookup"><span data-stu-id="b5381-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="b5381-157">Andere virtuele machines tooaccess Hallo-automatiseringsserver met Hallo DNS-naam met omgezette namen kan `Jenkins` of Hallo Git-server als `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="b5381-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="b5381-158">Maken van Hallo vNic met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b5381-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="b5381-159">Hallo volgende voorbeeld wordt een vNic met de naam `myNic`, verbonden toohello `myVnet` virtueel netwerk met de naam `myVnet`, en maakt een interne DNS-naam-record genoemd `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="b5381-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="b5381-160">Hallo VM in Hallo virtuele netwerkinfrastructuur implementeren</span><span class="sxs-lookup"><span data-stu-id="b5381-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="b5381-161">We hebben nu een virtueel netwerk en subnet, een Netwerkbeveiligingsgroep fungeert als een firewall tooprotect onze subnet door alle binnenkomend verkeer behalve poort 22 voor SSH en een vNic blokkeren.</span><span class="sxs-lookup"><span data-stu-id="b5381-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="b5381-162">U kunt nu een virtuele machine binnen deze bestaande netwerkinfrastructuur implementeren.</span><span class="sxs-lookup"><span data-stu-id="b5381-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="b5381-163">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b5381-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b5381-164">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` met Azure beheerd schijven en wordt Hallo vNic met de naam `myNic` van Hallo vóór stap:</span><span class="sxs-lookup"><span data-stu-id="b5381-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="b5381-165">Met behulp van Hallo vlaggen CLI toocall uit bestaande resources we Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo instrueren.</span><span class="sxs-lookup"><span data-stu-id="b5381-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="b5381-166">tooreiterate, zodra een VNet en een subnet is geïmplementeerd, kunnen ze worden gelaten als statisch of permanente resources binnen uw Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="b5381-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b5381-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5381-167">Next steps</span></span>
* [<span data-ttu-id="b5381-168">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="b5381-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5381-169">Linux-VM in Azure met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="b5381-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
