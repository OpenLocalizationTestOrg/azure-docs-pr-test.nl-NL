---
title: een virtuele machine met een statische openbare IP-adres - Azure CLI 2.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate met een statische openbare IP-adres met een virtuele machine hello Azure-opdrachtregelinterface (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="6b52b-103">Een virtuele machine maken met een statische openbare IP-adres met hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6b52b-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b52b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6b52b-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="6b52b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b52b-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="6b52b-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6b52b-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="6b52b-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6b52b-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="6b52b-108">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="6b52b-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="6b52b-109">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="6b52b-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="6b52b-110">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b52b-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="6b52b-111">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b52b-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="6b52b-112"><a name = "create"></a>Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="6b52b-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="6b52b-113">U kunt deze taak uitvoeren met hello Azure CLI 2.0 (in dit artikel) of Hallo [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6b52b-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="6b52b-114">waarden in Hallo ' ' voor Hallo variabelen in Hallo stappen volgen resources met de instellingen van Hallo scenario maken.</span><span class="sxs-lookup"><span data-stu-id="6b52b-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="6b52b-115">Hallo-waarden waar nodig voor uw omgeving te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6b52b-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="6b52b-116">Hallo installeren [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6b52b-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="6b52b-117">De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via Hallo stappen in Hallo [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b52b-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="6b52b-118">Vanuit een opdrachtshell, meld u aan met de opdracht Hallo `az login`.</span><span class="sxs-lookup"><span data-stu-id="6b52b-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="6b52b-119">Hallo VM maken door het Hallo-script dat op een Linux- of Mac-computer volgt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6b52b-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="6b52b-120">Hallo Azure openbaar IP-adres, het virtuele netwerk, netwerkinterface en VM netwerkbronnen moeten al bestaan in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="6b52b-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="6b52b-121">Hoewel Hallo resources niet allemaal tooexist in Hallo hebben dezelfde resourcegroep in Hallo na script ze doen.</span><span class="sxs-lookup"><span data-stu-id="6b52b-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

<span data-ttu-id="6b52b-122">Bovendien toocreating een virtuele machine, Hallo script maakt:</span><span class="sxs-lookup"><span data-stu-id="6b52b-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="6b52b-123">Een enkele premium schijf standaard beheerd, maar hebben van andere opties voor het Hallo-schijftype die u kunt maken.</span><span class="sxs-lookup"><span data-stu-id="6b52b-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="6b52b-124">Lees Hallo [maken van een Linux-VM met hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6b52b-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="6b52b-125">Virtueel netwerk, subnet, NIC en openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="6b52b-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="6b52b-126">U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="6b52b-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="6b52b-127">toolearn hoe toouse bestaande netwerkbronnen in plaats van invoeren voor het maken van aanvullende bronnen `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="6b52b-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="6b52b-128"><a name = "validate"></a>Maken van VM- en openbare IP-adres valideren</span><span class="sxs-lookup"><span data-stu-id="6b52b-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="6b52b-129">Voer de opdracht Hallo `az resource list --resouce-group IaaSStory --output table` toosee een lijst met Hallo-resources die zijn gemaakt door Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="6b52b-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="6b52b-130">Moet er vijf resources in Hallo uitvoer geretourneerd: network interface, schijf, openbare IP-adres, virtuele netwerk en een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6b52b-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="6b52b-131">Voer de opdracht Hallo `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="6b52b-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="6b52b-132">In Hallo uitvoer geretourneerd, bekijkt hello waarde **IpAddress** en die waarde Hallo van **PublicIpAllocationMethod** is *statische*.</span><span class="sxs-lookup"><span data-stu-id="6b52b-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="6b52b-133">Verwijder, voordat u Hallo na de opdracht uitvoert, Hallo <>, vervangen door *gebruikersnaam* met Hallo-naam die u voor Hallo gebruikt **gebruikersnaam** variabele in het Hallo-script en vervang *ipAddress* Hello **ipAddress** uit de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b52b-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="6b52b-134">Voer Hallo volgende opdracht tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="6b52b-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="6b52b-135"><a name= "clean-up"></a>Hallo VM en gekoppelde resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="6b52b-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="6b52b-136">Het raadzaam dat u Hallo resources in deze oefening hebt gemaakt verwijdert als u deze niet in productie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6b52b-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="6b52b-137">Virtuele machine, openbare IP-adres en schijfbronnen worden kosten in rekening, zolang deze zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="6b52b-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="6b52b-138">tooremove hello resources gemaakt tijdens deze oefening voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b52b-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="6b52b-139">tooview hello resources in de resourcegroep hello, Voer Hallo `az resource list --resource-group IaaSStory` opdracht.</span><span class="sxs-lookup"><span data-stu-id="6b52b-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="6b52b-140">Bevestig er zijn geen resources in de resourcegroep Hallo dan Hallo-resources die zijn gemaakt door Hallo script in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6b52b-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="6b52b-141">alle resources die zijn gemaakt in deze oefening uitvoeren Hallo toodelete `az group delete -n IaaSStory` opdracht.</span><span class="sxs-lookup"><span data-stu-id="6b52b-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="6b52b-142">Hallo opdracht verwijdert u Hallo-resourcegroep en alle Hallo resources bevat.</span><span class="sxs-lookup"><span data-stu-id="6b52b-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b52b-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b52b-143">Next steps</span></span>

<span data-ttu-id="6b52b-144">Netwerkverkeer kan tooand van virtuele machine in dit artikel gemaakt Hallo stromen.</span><span class="sxs-lookup"><span data-stu-id="6b52b-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="6b52b-145">Binnenkomende en uitgaande regels binnen een NSG die Hallo-verkeer dat tooand van netwerkinterface hello, Hallo subnet of beide kan stromen te beperken, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="6b52b-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="6b52b-146">meer informatie over nsg's, Hallo lezen toolearn [NSG overzicht](virtual-networks-nsg.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="6b52b-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
