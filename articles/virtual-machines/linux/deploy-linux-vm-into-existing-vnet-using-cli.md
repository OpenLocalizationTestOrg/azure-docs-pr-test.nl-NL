---
title: aaaDeploy virtuele Linux-machines in bestaande netwerk met Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over hoe een virtuele Linux-machine naar een bestaand virtueel netwerk met behulp van toodeploy hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="ebe4c-103">Hoe toodeploy virtuele Linux-machine in Azure een bestaand virtueel netwerk met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ebe4c-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="ebe4c-104">Dit artikel ziet u hoe toouse hello Azure CLI 2.0 toodeploy een virtuele machine (VM) in een bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="ebe4c-105">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="ebe4c-105">hello requirements are:</span></span>

- [<span data-ttu-id="ebe4c-106">een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="ebe4c-107">bestanden voor openbare en persoonlijke SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="ebe4c-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="ebe4c-108">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="ebe4c-109">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="ebe4c-109">Quick Commands</span></span>
<span data-ttu-id="ebe4c-110">Als u moet tooquickly Hallo taak, Hallo sectie volgen details Hallo opdrachten die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="ebe4c-111">Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="ebe4c-112">toocreate deze aangepaste omgeving, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ebe4c-113">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ebe4c-114">De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="ebe4c-115">**Randvoorwaarden voor:** Azure-resourcegroep, virtueel netwerk en subnet, inkomende netwerkbeveiligingsgroep met SSH, en een virtuele netwerkinterfacekaart.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="ebe4c-116">Hallo VM in Hallo virtuele netwerkinfrastructuur implementeren</span><span class="sxs-lookup"><span data-stu-id="ebe4c-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ebe4c-117">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="ebe4c-117">Detailed walkthrough</span></span>

<span data-ttu-id="ebe4c-118">Azure activa zoals virtuele netwerken en netwerkbeveiligingsgroepen moeten statisch en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="ebe4c-119">Zodra een virtueel netwerk is geïmplementeerd, kan opnieuw door nieuwe implementaties zonder een nadelige invloed toohello infrastructuur worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="ebe4c-120">Nadenken over een virtueel netwerk als een netwerkswitch traditionele hardware - u moet een geheel nieuwe hardware overschakelen met elke implementatie tooconfigure niet.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="ebe4c-121">Met een virtueel netwerk correct is geconfigureerd, kunt u blijven toodeploy nieuwe virtuele machines in dit virtuele netwerk met weinig steeds, eventuele wijzigingen vereist over Hallo levensduur van het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="ebe4c-122">toocreate deze aangepaste omgeving, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ebe4c-123">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ebe4c-124">De namen van de voorbeeld-parameter *myResourceGroup*, *myVnet*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="ebe4c-125">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="ebe4c-125">Create hello resource group</span></span>

<span data-ttu-id="ebe4c-126">Maak eerst een Azure resource group tooorganize alles wat die u in dit scenario maakt.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="ebe4c-127">Zie [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ebe4c-128">Maak Hallo resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ebe4c-129">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="ebe4c-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="ebe4c-130">Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="ebe4c-130">Create hello virtual network</span></span>

<span data-ttu-id="ebe4c-131">U kunt bouwen van een virtuele Azure-netwerk toolaunch Hallo VM's in.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="ebe4c-132">Zie voor meer informatie over virtuele netwerken [een virtueel netwerk maken met behulp van Azure CLI Hallo](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="ebe4c-133">Virtueel netwerk met Hallo maken [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="ebe4c-134">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* en subnet met de naam *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="ebe4c-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="ebe4c-135">Hallo netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="ebe4c-135">Create hello network security group</span></span>

<span data-ttu-id="ebe4c-136">Beveiligingsgroepen voor Azure-netwerk zijn equivalent tooa firewall op Hallo netwerklaag.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="ebe4c-137">Zie voor meer informatie over netwerkbeveiligingsgroepen [hoe toocreate netwerk beveiligingsgroepen in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="ebe4c-138">Maken van de netwerkbeveiligingsgroep met Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="ebe4c-139">Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="ebe4c-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="ebe4c-140">Regel voor geven van een binnenkomende SSH toevoegen</span><span class="sxs-lookup"><span data-stu-id="ebe4c-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="ebe4c-141">Hallo VM nodig toegang vanaf internet, zodat een regel voor het toestaan van binnenkomende poort 22 verkeer toobe Hallo netwerk tooport 22 op Hallo VM doorgegeven nodig Hallo.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="ebe4c-142">Toevoegen van een inkomende regel voor de netwerkbeveiligingsgroep Hallo met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="ebe4c-143">Hallo volgende voorbeeld maakt u een regel met naam *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="ebe4c-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="ebe4c-144">Hallo subnet toohello netwerkbeveiligingsgroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="ebe4c-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="ebe4c-145">Hallo netwerkbeveiligingsgroepen mag toegepaste tooa subnet of een specifieke virtuele netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="ebe4c-146">U kunt Hallo beveiliging groep tooour netwerksubnet koppelen.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="ebe4c-147">Koppel uw subnet toohello netwerkbeveiligingsgroep met [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="ebe4c-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="ebe4c-148">Een virtueel netwerk interface kaart toohello subnet toevoegen</span><span class="sxs-lookup"><span data-stu-id="ebe4c-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="ebe4c-149">Virtuele netwerkinterfacekaarten (VNics) zijn belangrijk omdat u ze hergebruiken kunt door deze toodifferent virtuele machines te verbinden.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="ebe4c-150">Deze opnieuw gebruiken kunt u tookeep hello VNic als statische resource Hallo VMs tijdelijke kan zijn.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="ebe4c-151">Een VNic maken en deze koppelen aan Hallo subnet met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="ebe4c-152">Hallo volgende voorbeeld wordt een VNic met de naam *myNic*:</span><span class="sxs-lookup"><span data-stu-id="ebe4c-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="ebe4c-153">Hallo VM in Hallo virtuele netwerkinfrastructuur implementeren</span><span class="sxs-lookup"><span data-stu-id="ebe4c-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="ebe4c-154">U hebt nu een virtueel netwerk en subnet en een security group tooprotect Hallo netwerksubnet door alle binnenkomend verkeer behalve poort 22 voor SSH blokkeren.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="ebe4c-155">Hallo VM kan nu worden geïmplementeerd in deze bestaande netwerkinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="ebe4c-156">Maken van uw virtuele machine met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ebe4c-157">Zie voor meer informatie over het Hallo toouse met hello Azure CLI 2.0 toodeploy een volledige virtuele machine vlaggen, [een volledige Linux-omgeving maken met behulp van Azure CLI Hallo](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="ebe4c-158">Hallo volgende voorbeeld maakt een VM die gebruikmaakt van Azure-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="ebe4c-159">Deze schijven worden afgehandeld door hello Azure-platform en hoeven niet alle toostore voorbereidings- of locatie ze.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="ebe4c-160">Zie voor meer informatie over beheerde schijven [overzicht Azure Managed Disks](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="ebe4c-161">Als u toouse zonder begeleiding schijven wenst, Zie Hallo aanvullende opmerking hieronder.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="ebe4c-162">Als u beheerde schijven gebruikt, moet u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="ebe4c-163">Als u toouse zonder begeleiding schijven wenst, moet u tooadd Hallo na extra parameters toohello procedure opdracht toocreate zonder begeleiding schijven in Hallo opslagaccount met de naam `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="ebe4c-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="ebe4c-164">Met behulp van Hallo vlaggen CLI toocall uit bestaande resources instrueren van Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="ebe4c-165">Zodra een virtueel netwerk en subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="ebe4c-166">In dit voorbeeld u niet maken en toewijzen van een openbare IP-adres toohello VNic, zodat deze virtuele machine niet openbaar toegankelijk via Hallo Internet is.</span><span class="sxs-lookup"><span data-stu-id="ebe4c-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="ebe4c-167">Zie voor meer informatie [een virtuele machine maken met een statische openbare IP-adres met behulp van Azure CLI Hallo](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ebe4c-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebe4c-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebe4c-168">Next steps</span></span>
<span data-ttu-id="ebe4c-169">Zie voor meer informatie over manieren toocreate virtuele machines in Azure Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="ebe4c-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="ebe4c-170">Een Azure Resource Manager-sjabloon toocreate een specifieke implementatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="ebe4c-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="ebe4c-171">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="ebe4c-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="ebe4c-172">Linux-VM in Azure met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="ebe4c-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
