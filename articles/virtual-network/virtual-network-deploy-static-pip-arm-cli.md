---
title: Een virtuele machine maken met statische openbare IP-adres - Azure CLI 2.0 | Microsoft Docs
description: Informatie over het maken van een virtuele machine met een statische openbare IP-adres met de Azure-opdrachtregelinterface (CLI) 2.0.
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
ms.openlocfilehash: a4c32694949880037f01bb2b6b9779d2cbb9809c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-cli-20"></a><span data-ttu-id="3800d-103">Een virtuele machine maken met een statische openbare IP-adres met de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3800d-103">Create a VM with a static public IP address using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3800d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3800d-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="3800d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3800d-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="3800d-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3800d-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="3800d-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3800d-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="3800d-108">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="3800d-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="3800d-109">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="3800d-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="3800d-110">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3800d-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="3800d-111">In dit artikel wordt behandeld met het implementatiemodel van Resource Manager, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel aanbeveelt.</span><span class="sxs-lookup"><span data-stu-id="3800d-111">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="3800d-112"><a name = "create"></a>De virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="3800d-112"><a name = "create"></a>Create the VM</span></span>

<span data-ttu-id="3800d-113">U kunt deze taak uitvoeren met de Azure CLI 2.0 (in dit artikel) of de [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3800d-113">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="3800d-114">De waarden in ' ' voor de variabelen in de stappen volgen resources met de instellingen van het scenario maken.</span><span class="sxs-lookup"><span data-stu-id="3800d-114">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="3800d-115">Wijzig de waarden, waar nodig, voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="3800d-115">Change the values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="3800d-116">Installeer de [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3800d-116">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="3800d-117">De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via de stappen in de [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3800d-117">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="3800d-118">Vanuit een opdrachtshell, meld u aan met de opdracht `az login`.</span><span class="sxs-lookup"><span data-stu-id="3800d-118">From a command shell, login with the command `az login`.</span></span>
4. <span data-ttu-id="3800d-119">De virtuele machine maken door het uitvoeren van het script dat op een Linux- of Mac-computer volgt.</span><span class="sxs-lookup"><span data-stu-id="3800d-119">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="3800d-120">De Azure openbaar IP-adres, virtuele netwerk, netwerkinterface en VM-resources moeten allemaal voorkomen op dezelfde locatie bevinden.</span><span class="sxs-lookup"><span data-stu-id="3800d-120">The Azure public IP address, virtual network, network interface, and VM resources must all exist in the same location.</span></span> <span data-ttu-id="3800d-121">Hoewel de bronnen, geen bestaan in dezelfde resourcegroep hebt, in het volgende script doen ze.</span><span class="sxs-lookup"><span data-stu-id="3800d-121">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using the --allocation-method Static option.
# If you do not specify this option, the address is allocated dynamically. The address is assigned to the
# resource from a pool of IP adresses unique to each Azure region. The DnsName must be unique within the
# Azure location it's created in. Download and view the file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists the ranges for each region.

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

# Create a network interface connected to the VNet with a static private IP address and associate the public IP address
# resource to the NIC.

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

# Create a new VM with the NIC

VmName="WEB1"

# Replace the value for the VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace the value for the OsImage variable with a value for *urn* from the output returned by entering
# the `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace the following value with the path to your public key file.
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
# If creating a Windows VM, remove the previous line and you'll be prompted for the password you want to configure for the VM.
```

<span data-ttu-id="3800d-122">Naast het maken van een virtuele machine, maakt het script:</span><span class="sxs-lookup"><span data-stu-id="3800d-122">In addition to creating a VM, the script creates:</span></span>
- <span data-ttu-id="3800d-123">Een enkele premium schijf standaard beheerd, maar er andere opties voor het schijftype die u kunt maken.</span><span class="sxs-lookup"><span data-stu-id="3800d-123">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="3800d-124">Lees de [maken van een Linux-VM met de Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3800d-124">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="3800d-125">Virtueel netwerk, subnet, NIC en openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="3800d-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="3800d-126">U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="3800d-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="3800d-127">Voor meer informatie over het gebruik van bestaande netwerkbronnen in plaats van met maken van aanvullende resources, voer `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="3800d-127">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="3800d-128"><a name = "validate"></a>Maken van VM- en openbare IP-adres valideren</span><span class="sxs-lookup"><span data-stu-id="3800d-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="3800d-129">Voer de opdracht `az resource list --resouce-group IaaSStory --output table` voor een overzicht van de resources die zijn gemaakt door het script.</span><span class="sxs-lookup"><span data-stu-id="3800d-129">Enter the command `az resource list --resouce-group IaaSStory --output table` to see a list of the resources created by the script.</span></span> <span data-ttu-id="3800d-130">Moet er vijf resources in de uitvoer van de geretourneerde: network interface, schijf, openbare IP-adres, virtuele netwerk en een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3800d-130">There should be five resources in the returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="3800d-131">Voer de opdracht `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="3800d-131">Enter the command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="3800d-132">Noteer de waarde van in de uitvoer van de geretourneerde **IpAddress** en dat de waarde van **PublicIpAllocationMethod** is *statische*.</span><span class="sxs-lookup"><span data-stu-id="3800d-132">In the returned output, note the value of **IpAddress** and that the value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="3800d-133">Verwijder, voordat u de volgende opdracht uitvoert, de <>, vervangen door *gebruikersnaam* met de naam die u gebruikt voor de **gebruikersnaam** variabele in het script en vervang *ipAddress*met de **ipAddress** uit de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="3800d-133">Before executing the following command, remove the <>, replace *Username* with the name you used for the **Username** variable in the script, and replace *ipAddress* with the **ipAddress** from the previous step.</span></span> <span data-ttu-id="3800d-134">Voer de volgende opdracht verbinding maken met de virtuele machine: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="3800d-134">Run the following command to connect to the VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="3800d-135"><a name= "clean-up"></a>Verwijder de virtuele machine en de bijbehorende bronnen</span><span class="sxs-lookup"><span data-stu-id="3800d-135"><a name= "clean-up"></a>Remove the VM and associated resources</span></span>

<span data-ttu-id="3800d-136">Het raadzaam dat u de resources in deze oefening hebt gemaakt verwijdert als u deze niet in productie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3800d-136">It's recommended that you delete the resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="3800d-137">Virtuele machine, openbare IP-adres en schijfbronnen worden kosten in rekening, zolang deze zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="3800d-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="3800d-138">Als u wilt verwijderen van de resources die zijn gemaakt tijdens deze oefening, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3800d-138">To remove the resources created during this exercise, complete the following steps:</span></span>

1. <span data-ttu-id="3800d-139">Uitvoeren als u wilt weergeven van de resources in de resourcegroep, de `az resource list --resource-group IaaSStory` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3800d-139">To view the resources in the resource group, run the `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="3800d-140">Bevestig er zijn geen resources in de resourcegroep, behalve de resources die zijn gemaakt door het script in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3800d-140">Confirm there are no resources in the resource group, other than the resources created by the script in this article.</span></span> 
3. <span data-ttu-id="3800d-141">Uitvoeren als u wilt verwijderen van alle resources in deze oefening hebt gemaakt, de `az group delete -n IaaSStory` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3800d-141">To delete all resources created in this exercise, run the `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="3800d-142">De opdracht verwijdert u de resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="3800d-142">The command deletes the resource group and all the resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3800d-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3800d-143">Next steps</span></span>

<span data-ttu-id="3800d-144">Netwerkverkeer kan stromen naar en van de virtuele machine gemaakt in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3800d-144">Any network traffic can flow to and from the VM created in this article.</span></span> <span data-ttu-id="3800d-145">Binnenkomende en uitgaande regels binnen een NSG die het verkeer dat naar en van de netwerkinterface, het subnet of beide stromen kan beperken, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="3800d-145">You can define inbound and outbound rules within an NSG that limit the traffic that can flow to and from the network interface, the subnet, or both.</span></span> <span data-ttu-id="3800d-146">Lees voor meer informatie over Nsg de [NSG overzicht](virtual-networks-nsg.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="3800d-146">To learn more about NSGs, read the [NSG overview](virtual-networks-nsg.md) article.</span></span>