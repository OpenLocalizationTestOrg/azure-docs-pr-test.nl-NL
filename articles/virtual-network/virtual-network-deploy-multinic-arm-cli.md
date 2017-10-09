---
title: een virtuele machine met meerdere NIC's - Azure CLI 2.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate met meerdere NIC's met behulp van een virtuele machine hello Azure CLI 2.0.
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
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="ec344-103">Een virtuele machine maken met meerdere NIC's met behulp van hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ec344-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ec344-104">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ec344-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ec344-105">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ec344-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="ec344-106"><a name="create"></a>Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="ec344-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="ec344-107">U kunt deze taak uitvoeren met hello Azure CLI 2.0 (in dit artikel) of Hallo [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ec344-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="ec344-108">waarden in Hallo ' ' voor Hallo variabelen in Hallo stappen volgen resources met de instellingen van Hallo scenario maken.</span><span class="sxs-lookup"><span data-stu-id="ec344-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="ec344-109">Hallo-waarden waar nodig voor uw omgeving te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ec344-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="ec344-110">Hallo installeren [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ec344-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="ec344-111">De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via Hallo stappen in Hallo [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ec344-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="ec344-112">Vanuit een opdrachtshell, meld u aan met de opdracht Hallo `az login`.</span><span class="sxs-lookup"><span data-stu-id="ec344-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="ec344-113">Hallo VM maken door het Hallo-script dat op een Linux- of Mac-computer volgt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ec344-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="ec344-114">Hallo script maakt een resourcegroep of een virtueel netwerk (VNet) met twee subnetten, twee NIC's en een virtuele machine met Hallo twee NIC's gekoppeld tooit.</span><span class="sxs-lookup"><span data-stu-id="ec344-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="ec344-115">Een van de Hallo NIC's verbonden tooone subnet en een statische openbare en particuliere IP-adres is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ec344-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="ec344-116">Hallo andere NIC is verbonden toohello andere subnet en een statisch privé IP-adres en geen openbare IP-adres is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ec344-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="ec344-117">Hallo NIC, openbare IP-adres, virtuele netwerken en VM netwerkbronnen moeten al bestaan in Hallo dezelfde locatie en het abonnement.</span><span class="sxs-lookup"><span data-stu-id="ec344-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="ec344-118">Hoewel Hallo resources niet allemaal tooexist in Hallo hebben dezelfde resourcegroep in Hallo na script ze doen.</span><span class="sxs-lookup"><span data-stu-id="ec344-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

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

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

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

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

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

<span data-ttu-id="ec344-119">Bovendien toocreating met twee NIC's een virtuele machine, Hallo script maakt:</span><span class="sxs-lookup"><span data-stu-id="ec344-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="ec344-120">Een enkele premium schijf standaard beheerd, maar hebben van andere opties voor het Hallo-schijftype die u kunt maken.</span><span class="sxs-lookup"><span data-stu-id="ec344-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="ec344-121">Lees Hallo [maken van een Linux-VM met hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec344-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="ec344-122">Een virtueel netwerk met twee subnetten en één openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ec344-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="ec344-123">U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="ec344-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="ec344-124">toolearn hoe toouse bestaande netwerkbronnen in plaats van invoeren voor het maken van aanvullende bronnen `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="ec344-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="ec344-125"><a name = "validate"></a>Maken van VM's en NIC's valideren</span><span class="sxs-lookup"><span data-stu-id="ec344-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="ec344-126">Voer de opdracht Hallo `az resource list --resouce-group Multi-NIC-VM --output table` toosee een lijst met Hallo-resources die zijn gemaakt door Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="ec344-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="ec344-127">Moet er zes resources in Hallo uitvoer geretourneerd: twee NIC's, één schijf, een openbare IP-adres, een virtueel netwerk en een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ec344-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="ec344-128">Voer de opdracht Hallo `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="ec344-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="ec344-129">In Hallo uitvoer geretourneerd, bekijkt hello waarde **IpAddress** en die waarde Hallo van **PublicIpAllocationMethod** is *statische*.</span><span class="sxs-lookup"><span data-stu-id="ec344-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="ec344-130">Verwijder, voordat Hallo volgende opdracht wordt uitgevoerd, Hallo <>, vervangen door *gebruikersnaam* met Hallo-naam die u voor Hallo gebruikt **gebruikersnaam** variabele in het Hallo-script en vervang *ipAddress* Hello **ipAddress** uit de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec344-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="ec344-131">Voer Hallo volgende opdracht tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="ec344-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="ec344-132">Uitvoeren zodra toohello VM is verbonden, Hallo `sudo ifconfig` opdracht toosee *eth0* en *eth1* interfaces.</span><span class="sxs-lookup"><span data-stu-id="ec344-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="ec344-133">Elke NIC is Hallo statisch privé IP-adressen opgegeven in Hallo script door hello Azure DHCP-servers toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ec344-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="ec344-134">Hallo wijzigen IP- en MAC-adressen toegewezen toohello NIC's niet totdat Hallo die virtuele machine is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ec344-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="ec344-135">U wordt aangeraden dat u niet IP-adressen binnen een besturingssysteem, wijzigt zoals connectiviteit toohello computer uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="ec344-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="ec344-136">Openbare IP-adressen worden niet weergegeven in het besturingssysteem hello, omdat ze netwerk adres vertaald tooand van Hallo privé IP-adres door hello Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="ec344-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="ec344-137"><a name= "clean-up"></a>Hallo VM en gekoppelde resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="ec344-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="ec344-138">Het raadzaam dat u Hallo resources in deze oefening hebt gemaakt verwijdert als u deze niet in productie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ec344-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="ec344-139">Virtuele machine, openbare IP-adres en schijfbronnen worden kosten in rekening, zolang deze zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="ec344-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="ec344-140">tooremove hello resources gemaakt tijdens deze oefening voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec344-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="ec344-141">tooview hello resources in de resourcegroep hello, Voer Hallo `az resource list --resource-group Multi-NIC-VM` opdracht.</span><span class="sxs-lookup"><span data-stu-id="ec344-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="ec344-142">Bevestig er zijn geen resources in de resourcegroep Hallo dan Hallo-resources die zijn gemaakt door Hallo script in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ec344-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="ec344-143">alle resources die zijn gemaakt in deze oefening uitvoeren Hallo toodelete `az group delete --name Multi-NIC-VM` opdracht.</span><span class="sxs-lookup"><span data-stu-id="ec344-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="ec344-144">Hallo opdracht verwijdert u Hallo-resourcegroep en alle Hallo resources bevat.</span><span class="sxs-lookup"><span data-stu-id="ec344-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec344-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec344-145">Next steps</span></span>

<span data-ttu-id="ec344-146">Netwerkverkeer kan tooand van virtuele machine in dit artikel gemaakt Hallo stromen.</span><span class="sxs-lookup"><span data-stu-id="ec344-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="ec344-147">Binnenkomende en uitgaande regels binnen een NSG die Hallo-verkeer dat tooand van elke netwerkinterface of elk subnet kan stromen te beperken, kunt u definiëren.</span><span class="sxs-lookup"><span data-stu-id="ec344-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="ec344-148">meer informatie over nsg's, Hallo lezen toolearn [NSG overzicht](virtual-networks-nsg.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ec344-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
