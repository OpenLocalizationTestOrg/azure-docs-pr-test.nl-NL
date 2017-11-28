---
title: Interne DNS gebruiken voor naamomzetting van de virtuele machine met de Azure CLI 2.0 | Microsoft Docs
description: Het maken van virtueel netwerk netwerkinterfacekaarten en interne DNS gebruiken voor naamomzetting van de virtuele machine in Azure met de Azure CLI 2.0
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
ms.openlocfilehash: 992920adb1ae3736d43cc5f0bbb2081a20a1674d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="03438-103">Maken van virtuele netwerkinterfacekaarten en interne DNS gebruiken voor naamomzetting van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="03438-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="03438-104">Dit artikel ziet u het instellen van statische interne DNS-namen voor virtuele Linux-machines met virtuele netwerkinterfacekaarten (vNics) en DNS-labelnamen met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="03438-104">This article shows you how to set static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with the Azure CLI 2.0.</span></span> <span data-ttu-id="03438-105">U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03438-105">You can also perform these steps with the [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="03438-106">Statische DNS-namen worden gebruikt voor permanente infrastructuurservices zoals een Jenkins build-server, die wordt gebruikt voor dit document of een Git-server.</span><span class="sxs-lookup"><span data-stu-id="03438-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="03438-107">De vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="03438-107">The requirements are:</span></span>

* [<span data-ttu-id="03438-108">een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="03438-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="03438-109">bestanden voor openbare en persoonlijke SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="03438-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="03438-110">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="03438-110">Quick commands</span></span>
<span data-ttu-id="03438-111">Als u de taak snel uitvoeren moet, wordt de volgende sectie de opdrachten die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="03438-111">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="03438-112">Meer gedetailleerde informatie en context voor elke stap u in de rest van het document vindt [vanaf hier](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="03438-112">More detailed information and context for each step can be found in the rest of the document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="03438-113">Als u wilt deze stappen uitvoert, moet u de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in het gebruik van een Azure-account [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="03438-113">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="03438-114">Randvoorwaarden voor: Resourcegroep, virtueel netwerk en subnet, Netwerkbeveiligingsgroep met SSH voor binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="03438-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="03438-115">Maken van een virtuele netwerkadapter met een statische interne DNS-naam</span><span class="sxs-lookup"><span data-stu-id="03438-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="03438-116">Maken van de vNic met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="03438-116">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="03438-117">De `--internal-dns-name` CLI-vlag is voor het instellen van de DNS-label, waardoor de statische DNS-naam voor de virtuele netwerkinterfacekaart (vNic).</span><span class="sxs-lookup"><span data-stu-id="03438-117">The `--internal-dns-name` CLI flag is for setting the DNS label, which provides the static DNS name for the virtual network interface card (vNic).</span></span> <span data-ttu-id="03438-118">Het volgende voorbeeld wordt een vNic met de naam `myNic`, verbonden aan de `myVnet` virtueel netwerk, en maakt een interne DNS-naam-record genoemd `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="03438-118">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-the-vnic"></a><span data-ttu-id="03438-119">Een virtuele machine implementeren en verbinding maken met de vnic van.</span><span class="sxs-lookup"><span data-stu-id="03438-119">Deploy a VM and connect the vNic</span></span>
<span data-ttu-id="03438-120">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="03438-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="03438-121">De `--nics` vlag de vNic verbindt met de virtuele machine tijdens de implementatie naar Azure.</span><span class="sxs-lookup"><span data-stu-id="03438-121">The `--nics` flag connects the vNic to the VM during the deployment to Azure.</span></span> <span data-ttu-id="03438-122">Het volgende voorbeeld wordt een virtuele machine met de naam `myVM` met Azure beheerd schijven en wordt de vNic met de naam `myNic` uit de vorige stap:</span><span class="sxs-lookup"><span data-stu-id="03438-122">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="03438-123">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="03438-123">Detailed walkthrough</span></span>

<span data-ttu-id="03438-124">Een volledige continue integratie en continue implementatie (CiCd) infrastructuur in Azure bepaalde servers statisch of lange levensduur hebben servers vereist.</span><span class="sxs-lookup"><span data-stu-id="03438-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span> <span data-ttu-id="03438-125">Het verdient aanbeveling dat Azure activa op de virtuele netwerken en Netwerkbeveiligingsgroepen statisch zijn en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.</span><span class="sxs-lookup"><span data-stu-id="03438-125">It is recommended that Azure assets like the virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="03438-126">Zodra een virtueel netwerk is geïmplementeerd, kan dit opnieuw gebruikt door nieuwe implementaties zonder een ongewenst is van invloed op de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="03438-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="03438-127">U kunt later een Git-opslagplaatsserver toevoegen of een automatiseringsserver Jenkins CiCd levert aan dit virtuele netwerk voor de ontwikkeling of testomgevingen.</span><span class="sxs-lookup"><span data-stu-id="03438-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd to this virtual network for your development or test environments.</span></span>  

<span data-ttu-id="03438-128">Interne DNS-namen zijn alleen omgezet in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="03438-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="03438-129">Omdat de DNS-namen interne zijn, zijn ze niet worden omgezet naar het internet, bieden van bijkomende beveiliging aan de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="03438-129">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="03438-130">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="03438-130">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="03438-131">De namen van de voorbeeld-parameter `myResourceGroup`, `myNic`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="03438-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="03438-132">De resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="03438-132">Create the resource group</span></span>
<span data-ttu-id="03438-133">Maak eerst de resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="03438-133">First, create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="03438-134">Het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` in de `westus` locatie:</span><span class="sxs-lookup"><span data-stu-id="03438-134">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="03438-135">Het virtuele netwerk maken</span><span class="sxs-lookup"><span data-stu-id="03438-135">Create the virtual network</span></span>

<span data-ttu-id="03438-136">De volgende stap is het bouwen van een virtueel netwerk voor het starten van de virtuele machines in.</span><span class="sxs-lookup"><span data-stu-id="03438-136">The next step is to build a virtual network to launch the VMs into.</span></span> <span data-ttu-id="03438-137">Het virtuele netwerk bevat één subnet voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="03438-137">The virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="03438-138">Zie voor meer informatie over virtuele netwerken van Azure [een virtueel netwerk maken met behulp van de Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03438-138">For more information on Azure virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="03438-139">Maken van het virtuele netwerk met [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="03438-139">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="03438-140">Het volgende voorbeeld wordt een virtueel netwerk met de naam `myVnet` en subnet met de naam `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="03438-140">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="03438-141">De Netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="03438-141">Create the Network Security Group</span></span>
<span data-ttu-id="03438-142">Beveiligingsgroepen voor Azure-netwerk zijn equivalent aan een firewall op de netwerklaag.</span><span class="sxs-lookup"><span data-stu-id="03438-142">Azure Network Security Groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="03438-143">Zie voor meer informatie over Netwerkbeveiligingsgroepen [het nsg's maken in de Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="03438-143">For more information about Network Security Groups, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="03438-144">Maken van de netwerkbeveiligingsgroep met [az netwerk nsg maken](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="03438-144">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="03438-145">Het volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="03438-145">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-to-allow-ssh"></a><span data-ttu-id="03438-146">Een inkomende regel om toe te staan SSH toevoegen</span><span class="sxs-lookup"><span data-stu-id="03438-146">Add an inbound rule to allow SSH</span></span>
<span data-ttu-id="03438-147">Toevoegen van een inkomende regel voor de netwerkbeveiligingsgroep met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="03438-147">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="03438-148">Het volgende voorbeeld wordt een regel met naam `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="03438-148">The following example creates a rule named `myRuleAllowSSH`:</span></span>

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

## <a name="associate-the-subnet-with-the-network-security-group"></a><span data-ttu-id="03438-149">Het subnet koppelen aan de Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="03438-149">Associate the subnet with the Network Security Group</span></span>
<span data-ttu-id="03438-150">Gebruiken om het subnet koppelen aan de Netwerkbeveiligingsgroep, [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="03438-150">To associate the subnet with the Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="03438-151">Het volgende voorbeeld wordt de subnetnaam `mySubnet` met de netwerk-beveiligingsgroep met de naam `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="03438-151">The following example associates the subnet name `mySubnet` with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-the-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="03438-152">De virtuele netwerkinterfacekaart en statische DNS-namen maken</span><span class="sxs-lookup"><span data-stu-id="03438-152">Create the virtual network interface card and static DNS names</span></span>
<span data-ttu-id="03438-153">Azure is zeer flexibel, maar voor het gebruik van DNS-namen voor naamomzetting van de virtuele machine, moet u netwerkinterfacekaarten (vNics) met een DNS-label voor virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="03438-153">Azure is very flexible, but to use DNS names for VM name resolution, you need to create virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="03438-154">vNics zijn belangrijk omdat u ze hergebruiken kunt door deze te verbinden met andere virtuele machines gedurende de levenscyclus van de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="03438-154">vNics are important as you can reuse them by connecting them to different VMs over the infrastructure lifecycle.</span></span> <span data-ttu-id="03438-155">Deze aanpak houdt de vNic als statische resource terwijl de virtuele machines kunnen tijdelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="03438-155">This approach keeps the vNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="03438-156">Met behulp van DNS labels op de vNic, kunnen we eenvoudig naamomzetting van andere VM's in het VNet inschakelen.</span><span class="sxs-lookup"><span data-stu-id="03438-156">By using DNS labeling on the vNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span> <span data-ttu-id="03438-157">Andere VM's toegang tot de automatiseringsserver door de DNS-naam met behulp van omgezette namen kan `Jenkins` of de Git-server als `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="03438-157">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  

<span data-ttu-id="03438-158">Maken van de vNic met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="03438-158">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="03438-159">Het volgende voorbeeld wordt een vNic met de naam `myNic`, verbonden aan de `myVnet` virtueel netwerk met de naam `myVnet`, en maakt een interne DNS-naam-record genoemd `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="03438-159">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="03438-160">Implementeer de virtuele machine in de infrastructuur van het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="03438-160">Deploy the VM into the virtual network infrastructure</span></span>
<span data-ttu-id="03438-161">We hebben nu een virtueel netwerk en subnet, een Netwerkbeveiligingsgroep fungeert als een firewall blokkeert al het binnenkomende verkeer behalve poort 22 voor SSH en een vNic voor het beveiligen van onze subnet.</span><span class="sxs-lookup"><span data-stu-id="03438-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="03438-162">U kunt nu een virtuele machine binnen deze bestaande netwerkinfrastructuur implementeren.</span><span class="sxs-lookup"><span data-stu-id="03438-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="03438-163">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="03438-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="03438-164">Het volgende voorbeeld wordt een virtuele machine met de naam `myVM` met Azure beheerd schijven en wordt de vNic met de naam `myNic` uit de vorige stap:</span><span class="sxs-lookup"><span data-stu-id="03438-164">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="03438-165">Met behulp van de vlaggen CLI aan te roepen bestaande bronnen, zodat we Azure voor het implementeren van de virtuele machine binnen de bestaande netwerk.</span><span class="sxs-lookup"><span data-stu-id="03438-165">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="03438-166">Om aan te wijzen er nogmaals zodra een VNet en het subnet zijn geïmplementeerd, kunnen ze blijven als statisch of permanente resources binnen uw Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="03438-166">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="03438-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="03438-167">Next steps</span></span>
* [<span data-ttu-id="03438-168">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="03438-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="03438-169">Linux-VM in Azure met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="03438-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
