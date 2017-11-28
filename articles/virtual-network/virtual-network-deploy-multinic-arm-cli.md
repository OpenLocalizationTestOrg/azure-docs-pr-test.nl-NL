---
title: Een virtuele machine maken met meerdere NIC's - Azure CLI 2.0 | Microsoft Docs
description: Informatie over het maken van een virtuele machine met meerdere NIC's met behulp van de Azure CLI 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 19b1757dd694e756cfd2d0d6cd67e64f43ccab7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-the-azure-cli-20"></a><span data-ttu-id="67311-103">Een virtuele machine maken met meerdere NIC's met behulp van de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="67311-103">Create a VM with multiple NICs using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="67311-104">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="67311-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="67311-105">Dit artikel bevat informatie over het Resource Manager-implementatiemodel, dat door Microsoft wordt aanbevolen voor de meeste nieuwe implementaties in plaats van het [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="67311-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="67311-106"><a name="create"></a>De virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="67311-106"><a name="create"></a>Create the VM</span></span>

<span data-ttu-id="67311-107">U kunt deze taak uitvoeren met de Azure CLI 2.0 (in dit artikel) of de [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="67311-107">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="67311-108">De waarden in ' ' voor de variabelen in de stappen volgen resources met de instellingen van het scenario maken.</span><span class="sxs-lookup"><span data-stu-id="67311-108">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="67311-109">Wijzig de waarden, waar nodig, voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="67311-109">Change the values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="67311-110">Installeer de [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="67311-110">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="67311-111">De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via de stappen in de [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67311-111">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="67311-112">Vanuit een opdrachtshell, meld u aan met de opdracht `az login`.</span><span class="sxs-lookup"><span data-stu-id="67311-112">From a command shell, login with the command `az login`.</span></span>
4. <span data-ttu-id="67311-113">De virtuele machine maken door het uitvoeren van het script dat op een Linux- of Mac-computer volgt.</span><span class="sxs-lookup"><span data-stu-id="67311-113">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="67311-114">Het script maakt een resourcegroep, een virtueel netwerk (VNet) met twee subnetten, twee NIC's en met de twee NIC's een virtuele machine is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="67311-114">The script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="67311-115">Een van de NIC's is verbonden met één subnet en een statische openbare en particuliere IP-adres is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="67311-115">One of the NICs is connected to one subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="67311-116">De andere NIC is verbonden met het andere subnet en een statisch privé IP-adres en geen openbare IP-adres is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="67311-116">The other NIC is connected to the other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="67311-117">De NIC, openbare IP-adres, virtuele netwerken en VM netwerkbronnen moeten al bestaan in dezelfde locatie en abonnement.</span><span class="sxs-lookup"><span data-stu-id="67311-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="67311-118">Hoewel de bronnen, geen bestaan in dezelfde resourcegroep hebt, in het volgende script doen ze.</span><span class="sxs-lookup"><span data-stu-id="67311-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# The address is assigned to the resource from a pool of IP adresses unique to each Azure region. 
# Download and view the file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# the ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within the VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected to one of the subnets. The NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses to each NIC. To learn more about IP addressing
# options for NICs, enter the az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it to the other subnet. Though multiple NICs attached to the same
# VM can be connected to different subnets, the subnets must all be within the same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach the two NICs.

VmName="WEB"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure to select a VM size that supports the number of NICs you want to attach to the VM.
# You must create the VM with at least two NICs if you want to add more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs to the VM after VM creation, regardless of how many NICs the VM supports.
# The VM size specified in the following variable supports two NICs.

VmSize="Standard_DS2"

# Replace the value for the OsImage variable value with a value for *urn* from the output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing the following command, add variable names of additional NICs you may have added to the script that
# you want to attach to the VM. If creating a Windows VM, remove the **ssh-key-value** line and you'll be prompted for
# the password you want to configure for the VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

<span data-ttu-id="67311-119">Naast het maken van een VM met twee NIC's, maakt het script:</span><span class="sxs-lookup"><span data-stu-id="67311-119">In addition to creating a VM with two NICs, the script creates:</span></span>
- <span data-ttu-id="67311-120">Een enkele premium schijf standaard beheerd, maar er andere opties voor het schijftype die u kunt maken.</span><span class="sxs-lookup"><span data-stu-id="67311-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="67311-121">Lees de [maken van een Linux-VM met de Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="67311-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="67311-122">Een virtueel netwerk met twee subnetten en één openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="67311-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="67311-123">U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="67311-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="67311-124">Voor meer informatie over het gebruik van bestaande netwerkbronnen in plaats van met maken van aanvullende resources, voer `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="67311-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="67311-125"><a name = "validate"></a>Maken van VM's en NIC's valideren</span><span class="sxs-lookup"><span data-stu-id="67311-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="67311-126">Voer de opdracht `az resource list --resouce-group Multi-NIC-VM --output table` voor een overzicht van de resources die zijn gemaakt door het script.</span><span class="sxs-lookup"><span data-stu-id="67311-126">Enter the command `az resource list --resouce-group Multi-NIC-VM --output table` to see a list of the resources created by the script.</span></span> <span data-ttu-id="67311-127">Moet er zes resources in de uitvoer van de geretourneerde: twee NIC's, één schijf, een openbare IP-adres, een virtueel netwerk en een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="67311-127">There should be six resources in the returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="67311-128">Voer de opdracht `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="67311-128">Enter the command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="67311-129">Noteer de waarde van in de uitvoer van de geretourneerde **IpAddress** en dat de waarde van **PublicIpAllocationMethod** is *statische*.</span><span class="sxs-lookup"><span data-stu-id="67311-129">In the returned output, note the value of **IpAddress** and that the value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="67311-130">Voordat u de volgende opdracht uitvoert, verwijdert u de <>, vervangen door *gebruikersnaam* met de naam die u gebruikt voor de **gebruikersnaam** variabele in het script en vervang *ipAddress* met de **IP-adres** van de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="67311-130">Before running the following command, remove the <>, replace *Username* with the name you used for the **Username** variable in the script, and replace *ipAddress* with the **ipAddress** from the previous step.</span></span> <span data-ttu-id="67311-131">Voer de volgende opdracht verbinding maken met de virtuele machine: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="67311-131">Run the following command to connect to the VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="67311-132">Eenmaal zijn verbonden met de virtuele machine, voer de `sudo ifconfig` opdracht om te zien *eth0* en *eth1* interfaces.</span><span class="sxs-lookup"><span data-stu-id="67311-132">Once connected to the VM, run the `sudo ifconfig` command to see *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="67311-133">Elke NIC is het statische privé IP-adressen in het script is opgegeven door de Azure-DHCP-servers toegewezen.</span><span class="sxs-lookup"><span data-stu-id="67311-133">Each NIC has been assigned the static private IP addresses specified in the script by the Azure DHCP servers.</span></span> <span data-ttu-id="67311-134">De IP- en MAC-adressen die zijn toegewezen aan de NIC's wijzigen niet totdat de virtuele machine wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="67311-134">The IP and MAC addresses assigned to the NICs do not change until the VM is deleted.</span></span> <span data-ttu-id="67311-135">U wordt aangeraden dat u niet IP-adressen binnen een besturingssysteem, wijzigt als deze verbinding met de computer kunt uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="67311-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity to the computer.</span></span> <span data-ttu-id="67311-136">Openbare IP-adressen worden niet weergegeven in het besturingssysteem, omdat ze netwerkadres vertaald naar en van de privé IP-adres door de Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="67311-136">Public IP addresses do not appear within the operating system, as they are network address translated to and from the private IP address by the Azure infrastructure.</span></span>

## <span data-ttu-id="67311-137"><a name= "clean-up"></a>Verwijder de virtuele machine en de bijbehorende bronnen</span><span class="sxs-lookup"><span data-stu-id="67311-137"><a name= "clean-up"></a>Remove the VM and associated resources</span></span>

<span data-ttu-id="67311-138">Het raadzaam dat u de resources in deze oefening hebt gemaakt verwijdert als u deze niet in productie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="67311-138">It's recommended that you delete the resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="67311-139">Virtuele machine, openbare IP-adres en schijfbronnen worden kosten in rekening, zolang deze zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="67311-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="67311-140">Als u wilt verwijderen van de resources die zijn gemaakt tijdens deze oefening, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="67311-140">To remove the resources created during this exercise, complete the following steps:</span></span>
1. <span data-ttu-id="67311-141">Uitvoeren als u wilt weergeven van de resources in de resourcegroep, de `az resource list --resource-group Multi-NIC-VM` opdracht.</span><span class="sxs-lookup"><span data-stu-id="67311-141">To view the resources in the resource group, run the `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="67311-142">Bevestig er zijn geen resources in de resourcegroep, behalve de resources die zijn gemaakt door het script in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="67311-142">Confirm there are no resources in the resource group, other than the resources created by the script in this article.</span></span> 
3. <span data-ttu-id="67311-143">Uitvoeren als u wilt verwijderen van alle resources in deze oefening hebt gemaakt, de `az group delete --name Multi-NIC-VM` opdracht.</span><span class="sxs-lookup"><span data-stu-id="67311-143">To delete all resources created in this exercise, run the `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="67311-144">De opdracht verwijdert u de resourcegroep en alle resources die deze bevat.</span><span class="sxs-lookup"><span data-stu-id="67311-144">The command deletes the resource group and all the resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67311-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67311-145">Next steps</span></span>

<span data-ttu-id="67311-146">Netwerkverkeer kan stromen naar en van de virtuele machine gemaakt in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="67311-146">Any network traffic can flow to and from the VM created in this article.</span></span> <span data-ttu-id="67311-147">Binnenkomende en uitgaande regels binnen een NSG die het verkeer van en naar elke netwerkinterface of elk subnet kan stromen te beperken, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="67311-147">You can define inbound and outbound rules within an NSG that limit the traffic that can flow to and from each network interface, each subnet, or both.</span></span> <span data-ttu-id="67311-148">Lees voor meer informatie over Nsg de [NSG overzicht](virtual-networks-nsg.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="67311-148">To learn more about NSGs, read the [NSG overview](virtual-networks-nsg.md) article.</span></span>