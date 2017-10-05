---
title: Virtuele machine met meerdere IP-adressen in de Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over meerdere IP-adressen toewijzen aan een virtuele machine via de Azure CLI 2.0 | Resource Manager.
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 0e9b2ef89ca39a7988a7b2573496a605dfc604b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-cli-20"></a><span data-ttu-id="2fd1f-103">Meerdere IP-adressen toewijzen aan virtuele machines met behulp van de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2fd1f-103">Assign multiple IP addresses to virtual machines using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="2fd1f-104">Dit artikel wordt uitgelegd hoe u een virtuele machine (VM) maken via het Azure Resource Manager-implementatiemodel met behulp van de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 2.0.</span></span> <span data-ttu-id="2fd1f-105">Meerdere IP-adressen kunnen niet worden toegewezen aan resources die zijn gemaakt met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="2fd1f-106">Lees voor meer informatie over Azure-implementatiemodellen de [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="2fd1f-107"><a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen</span><span class="sxs-lookup"><span data-stu-id="2fd1f-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="2fd1f-108">U kunt deze taak uitvoeren met de Azure CLI 2.0 (in dit artikel) of de [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2fd1f-108">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="2fd1f-109">Wijzig de waarden, waar nodig, voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-109">Change the values, as appropriate, for your environment.</span></span> <span data-ttu-id="2fd1f-110">Welke stappen volgen wordt uitgelegd hoe een voorbeeld van de virtuele machine maken met meerdere IP-adressen, zoals beschreven in het scenario.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-110">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="2fd1f-111">Variabelewaarden wijzigen in ' ' en IP-adrestypen zoals vereist voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="2fd1f-112">Installeer de [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="2fd1f-113">De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via de stappen in de [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fd1f-113">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="2fd1f-114">Vanuit een opdrachtshell, meld u aan met de opdracht `az login` en selecteer het abonnement dat u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-114">From a command shell, login with the command `az login` and select the subscription you're using.</span></span>
4. <span data-ttu-id="2fd1f-115">De virtuele machine maken door het uitvoeren van het script dat op een Linux- of Mac-computer volgt.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-115">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="2fd1f-116">Het script maakt een resourcegroep, een virtueel netwerk (VNet), een NIC met drie IP-configuraties en een virtuele machine met de twee NIC's gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-116">The script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="2fd1f-117">De NIC, openbare IP-adres, virtuele netwerken en VM netwerkbronnen moeten al bestaan in dezelfde locatie en abonnement.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="2fd1f-118">Hoewel de bronnen, geen bestaan in dezelfde resourcegroep hebt, in het volgende script doen ze.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using the `--allocation-method Static` option. If you
# do not specify this option, the address is allocated dynamically. The address is assigned to the resource from a pool
# of IP adresses unique to each Azure region. Download and view the file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists the ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected to the subnet and associate the public IP address to it. Azure will create the
# first IP configuration with a static private IP address and will associate the public IP address resource to it.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it to the NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it to the NIC. This configuration has  static private IP address and   # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations
# to any NIC in a VM. To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach the NIC.

VmName="myVm"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. The script fails if the VM size
# is not supported in the location you select. Run the `azure vm sizes --location estcentralus` command to get a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace the value for the OsImage variable value with a value for *urn* from the utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file. If you're creating a Windows VM, remove the following
# line and you'll be prompted for the password you want to configure for the VM.

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
```

<span data-ttu-id="2fd1f-119">Naast het maken van een virtuele machine met een NIC met 3-IP-configuraties, maakt het script:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-119">In addition to creating a VM with a NIC with 3 IP configurations, the script creates:</span></span>

- <span data-ttu-id="2fd1f-120">Een enkele premium schijf standaard beheerd, maar er andere opties voor het schijftype die u kunt maken.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="2fd1f-121">Lees de [maken van een Linux-VM met de Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="2fd1f-122">Een virtueel netwerk met één subnet en twee openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="2fd1f-123">U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="2fd1f-124">Voor meer informatie over het gebruik van bestaande netwerkbronnen in plaats van met maken van aanvullende resources, voer `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="2fd1f-125">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="2fd1f-126">Lees meer informatie over prijzen voor IP-adres, de [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-126">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="2fd1f-127">Er is een limiet aan het aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-127">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="2fd1f-128">Lees voor meer informatie over de limieten het artikel [Azure-limieten](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="2fd1f-128">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="2fd1f-129">Nadat de virtuele machine is gemaakt, voert u de `az network nic show --name MyNic1 --resource-group myResourceGroup` opdracht de NIC-configuratie kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-129">After the VM is created, enter the `az network nic show --name MyNic1 --resource-group myResourceGroup` command to view the NIC configuration.</span></span> <span data-ttu-id="2fd1f-130">Voer de `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` voor een lijst van de IP-configuraties die zijn gekoppeld naar de NIC.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-130">Enter the `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` to view a list of the IP configurations associated to the NIC.</span></span>

<span data-ttu-id="2fd1f-131">De particuliere IP-adressen toevoegen aan het besturingssysteem van de virtuele machine via de stappen voor het besturingssysteem in de [toevoegen IP-adressen naar een VM-besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-131">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="2fd1f-132"><a name="add"></a>IP-adressen toevoegen aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="2fd1f-132"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="2fd1f-133">U kunt extra persoonlijke en openbare IP-adressen toevoegen aan een bestaande NIC via de stappen volgen.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-133">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="2fd1f-134">De voorbeelden bouwen voort op de [scenario](#Scenario) in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-134">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="2fd1f-135">Open een opdrachtshell en voer de overige stappen in deze sectie binnen één sessie.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-135">Open a command shell and complete the remaining steps in this section within a single session.</span></span> <span data-ttu-id="2fd1f-136">Als u nog geen Azure CLI geïnstalleerd en geconfigureerd hebt, voer de stappen in de [installatie van Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel en meld u aan bij uw Azure-account met de `az-login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-136">If you don't already have Azure CLI installed and configured, complete the steps in the [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login to your Azure account with the `az-login` command.</span></span>

2. <span data-ttu-id="2fd1f-137">Volg de stappen in een van de volgende secties, op basis van uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-137">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="2fd1f-138">**Een persoonlijke IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="2fd1f-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="2fd1f-139">Als u wilt een particulier IP-adres toevoegen aan een NIC, moet u een IP-configuratie met de volgende opdracht te maken.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-139">To add a private IP address to a NIC, you must create an IP configuration using the command that follows.</span></span> <span data-ttu-id="2fd1f-140">Het statische IP-adres moet een niet-gebruikte adres voor het subnet.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-140">The static IP address must be an unused address for the subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="2fd1f-141">Configuraties die u nodig hebt, gebruik van unieke namen en privé IP-adressen (voor configuraties met statische IP-adressen) maken.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="2fd1f-142">**Een openbaar IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="2fd1f-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="2fd1f-143">Een openbaar IP-adres is toegevoegd door deze te koppelen aan een nieuwe IP-configuratie of een bestaande IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-143">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="2fd1f-144">Voer de stappen in een van de secties die volgen, die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-144">Complete the steps in one of the sections that follow, as you require.</span></span>

    <span data-ttu-id="2fd1f-145">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="2fd1f-146">Lees meer informatie over prijzen voor IP-adres, de [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-146">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="2fd1f-147">Er is een limiet aan het aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-147">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="2fd1f-148">Lees voor meer informatie over de limieten het artikel [Azure-limieten](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="2fd1f-148">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="2fd1f-149">**Koppelen van de resource toe aan een nieuwe IP-configuratie**</span><span class="sxs-lookup"><span data-stu-id="2fd1f-149">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="2fd1f-150">Als u een openbaar IP-adres in een nieuw IP-configuratie toevoegt, moet u ook een privé IP-adres toevoegen, omdat alle IP-configuraties moeten een particulier IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="2fd1f-151">U kunt een bestaande resource voor openbare IP-adres toevoegen of u een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="2fd1f-152">Voer de volgende opdracht om een nieuwe maken:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-152">To create a new one, enter the following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="2fd1f-153">Een nieuwe IP-configuratie maken met een statisch privé IP-adres en de bijbehorende *myPublicIP3* openbaar IP adres resource, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-153">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="2fd1f-154">**Koppelen van de resource toe aan een bestaande IP-configuratie** een openbare IP-adres resource kan alleen worden gekoppeld aan een IP-configuratie die nog geen die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-154">**Associate the resource to an existing IP configuration** A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="2fd1f-155">U kunt bepalen of een IP-configuratie een gekoppeld openbare IP-adres heeft met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-155">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="2fd1f-156">Geretourneerd uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="2fd1f-157">Aangezien de **PublicIpAddressId** kolom voor *IpConfig 3* is leeg in de uitvoer, geen openbare IP-adres-resource is momenteel gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-157">Since the **PublicIpAddressId** column for *IpConfig-3* is blank in the output, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="2fd1f-158">U kunt een bestaande resource voor openbare IP-adres toevoegen aan IpConfig 3 of Voer de volgende opdracht een te maken:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-158">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="2fd1f-159">Voer de volgende opdracht om te koppelen van het openbare IP-adres resource aan de bestaande IP-configuratie met de naam *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-159">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="2fd1f-160">Bekijk de privé IP-adressen en openbare IP-adres resource id's die zijn toegewezen aan de NIC met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-160">View the private IP addresses and the public IP address resource Ids assigned to the NIC by entering the following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="2fd1f-161">Geretourneerd uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2fd1f-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="2fd1f-162">Toevoegen van de privé IP-adressen die u hebt toegevoegd aan de NIC van het besturingssysteem van de virtuele machine door de instructies in de [toevoegen IP-adressen naar een VM-besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-162">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="2fd1f-163">Het openbare IP-adressen niet aan het besturingssysteem toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2fd1f-163">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
