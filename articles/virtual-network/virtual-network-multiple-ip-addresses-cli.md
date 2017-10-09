---
title: aaaVM met meerdere IP-adressen met behulp van Azure CLI 2.0 Hallo | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met Azure CLI 2.0 Hallo | Resource Manager.
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
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a><span data-ttu-id="37343-103">Toovirtual machines hello Azure CLI 2.0 gebruiken voor meerdere IP-adressen toewijzen</span><span class="sxs-lookup"><span data-stu-id="37343-103">Assign multiple IP addresses toovirtual machines using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="37343-104">Dit artikel wordt uitgelegd hoe een virtuele machine (VM) via hello Azure Resource Manager deployment model met behulp van toocreate hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="37343-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 2.0.</span></span> <span data-ttu-id="37343-105">Meerdere IP-adressen kunnen niet worden toegewezen als tooresources via de klassieke implementatiemodel Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="37343-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="37343-106">meer informatie over Azure-implementatiemodellen, Hallo lezen toolearn [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="37343-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="37343-107"><a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen</span><span class="sxs-lookup"><span data-stu-id="37343-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="37343-108">U kunt deze taak uitvoeren met hello Azure CLI 2.0 (in dit artikel) of Hallo [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="37343-108">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="37343-109">Hallo-waarden waar nodig voor uw omgeving te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="37343-109">Change hello values, as appropriate, for your environment.</span></span> <span data-ttu-id="37343-110">Hallo in de volgende procedure wordt uitgelegd hoe toocreate een voorbeeld van de virtuele machine met meerdere IP-adressen, zoals beschreven in Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="37343-110">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="37343-111">Variabelewaarden wijzigen in ' ' en IP-adrestypen zoals vereist voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="37343-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="37343-112">Hallo installeren [Azure CLI 2.0](/cli/azure/install-az-cli2) als u dit nog niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="37343-112">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="37343-113">De openbare en persoonlijke sleutelpaar voor een SSH maken voor Linux virtuele machines via Hallo stappen in Hallo [maken van een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="37343-113">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="37343-114">Vanuit een opdrachtshell, meld u aan met de opdracht Hallo `az login` en u Hallo-abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="37343-114">From a command shell, login with hello command `az login` and select hello subscription you're using.</span></span>
4. <span data-ttu-id="37343-115">Hallo VM maken door het Hallo-script dat op een Linux- of Mac-computer volgt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="37343-115">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="37343-116">Hallo script maakt een resourcegroep, een virtueel netwerk (VNet), een NIC met drie IP-configuraties en een virtuele machine met Hallo twee NIC's gekoppeld tooit.</span><span class="sxs-lookup"><span data-stu-id="37343-116">hello script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="37343-117">Hallo NIC, openbare IP-adres, virtuele netwerken en VM netwerkbronnen moeten al bestaan in Hallo dezelfde locatie en het abonnement.</span><span class="sxs-lookup"><span data-stu-id="37343-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="37343-118">Hoewel Hallo resources niet allemaal tooexist in Hallo hebben dezelfde resourcegroep in Hallo na script ze doen.</span><span class="sxs-lookup"><span data-stu-id="37343-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

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

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
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

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

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

<span data-ttu-id="37343-119">Bovendien toocreating een virtuele machine met een NIC met 3-IP-configuraties, Hallo script maakt:</span><span class="sxs-lookup"><span data-stu-id="37343-119">In addition toocreating a VM with a NIC with 3 IP configurations, hello script creates:</span></span>

- <span data-ttu-id="37343-120">Een enkele premium schijf standaard beheerd, maar hebben van andere opties voor het Hallo-schijftype die u kunt maken.</span><span class="sxs-lookup"><span data-stu-id="37343-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="37343-121">Lees Hallo [maken van een Linux-VM met hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="37343-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="37343-122">Een virtueel netwerk met één subnet en twee openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="37343-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="37343-123">U kunt ook gebruiken *bestaande* virtueel netwerk, subnet, NIC of openbare IP-adresbronnen.</span><span class="sxs-lookup"><span data-stu-id="37343-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="37343-124">toolearn hoe toouse bestaande netwerkbronnen in plaats van invoeren voor het maken van aanvullende bronnen `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="37343-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="37343-125">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="37343-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="37343-126">meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="37343-126">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="37343-127">Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="37343-127">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="37343-128">meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.</span><span class="sxs-lookup"><span data-stu-id="37343-128">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="37343-129">Nadat het Hallo VM is gemaakt, voert u Hallo `az network nic show --name MyNic1 --resource-group myResourceGroup` opdracht tooview Hallo NIC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="37343-129">After hello VM is created, enter hello `az network nic show --name MyNic1 --resource-group myResourceGroup` command tooview hello NIC configuration.</span></span> <span data-ttu-id="37343-130">Voer Hallo `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview een lijst met Hallo IP-configuraties die zijn gekoppeld toohello NIC.</span><span class="sxs-lookup"><span data-stu-id="37343-130">Enter hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview a list of hello IP configurations associated toohello NIC.</span></span>

<span data-ttu-id="37343-131">Toevoegen Hallo privé-IP-adressen toohello VM besturingssysteem via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="37343-131">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="37343-132"><a name="add"></a>IP-adressen tooa VM toevoegen</span><span class="sxs-lookup"><span data-stu-id="37343-132"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="37343-133">U kunt extra persoonlijke en openbare IP-adressen tooan NIC bestaande via Hallo stappen volgen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="37343-133">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="37343-134">Hallo voorbeelden bouwen voort op Hallo [scenario](#Scenario) in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="37343-134">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="37343-135">Open een opdrachtshell en volledige Hallo resterende stappen in deze sectie binnen één sessie.</span><span class="sxs-lookup"><span data-stu-id="37343-135">Open a command shell and complete hello remaining steps in this section within a single session.</span></span> <span data-ttu-id="37343-136">Als u nog geen Azure CLI geïnstalleerd en geconfigureerd, voltooid Hallo stappen voor het Hallo [installatie van Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour artikel en meld u aan Azure-account met Hallo `az-login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="37343-136">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login tooyour Azure account with hello `az-login` command.</span></span>

2. <span data-ttu-id="37343-137">Voer Hallo stappen in een Hallo uit te voeren, op basis van uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="37343-137">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="37343-138">**Een persoonlijke IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="37343-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="37343-139">een persoonlijke IP-adres tooa NIC tooadd, moet u een IP-configuratie met Hallo-opdracht die volgt maken.</span><span class="sxs-lookup"><span data-stu-id="37343-139">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command that follows.</span></span> <span data-ttu-id="37343-140">Hallo statisch IP-adres moet een niet-gebruikte adres voor het Hallo-subnet.</span><span class="sxs-lookup"><span data-stu-id="37343-140">hello static IP address must be an unused address for hello subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="37343-141">Configuraties die u nodig hebt, gebruik van unieke namen en privé IP-adressen (voor configuraties met statische IP-adressen) maken.</span><span class="sxs-lookup"><span data-stu-id="37343-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="37343-142">**Een openbaar IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="37343-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="37343-143">Een openbaar IP-adres is toegevoegd door deze te koppelen tooeither een nieuwe IP-configuratie of een bestaande IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="37343-143">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="37343-144">Stappen Hallo in een van Hallo secties die volgen, die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="37343-144">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    <span data-ttu-id="37343-145">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="37343-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="37343-146">meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="37343-146">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="37343-147">Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="37343-147">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="37343-148">meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.</span><span class="sxs-lookup"><span data-stu-id="37343-148">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="37343-149">**Hallo resource tooa nieuwe IP-configuratie koppelen**</span><span class="sxs-lookup"><span data-stu-id="37343-149">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="37343-150">Als u een openbaar IP-adres in een nieuw IP-configuratie toevoegt, moet u ook een privé IP-adres toevoegen, omdat alle IP-configuraties moeten een particulier IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="37343-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="37343-151">U kunt een bestaande resource voor openbare IP-adres toevoegen of u een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="37343-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="37343-152">toocreate een nieuw wachtwoord invoeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="37343-152">toocreate a new one, enter hello following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="37343-153">toocreate een nieuwe IP-configuratie met een statisch privé IP-adres en het Hallo gekoppeld *myPublicIP3* openbare IP-adres adres resource, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="37343-153">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="37343-154">**Koppelen Hallo resource tooan bestaande IP-configuratie** een openbare IP-adres resource kan alleen worden gekoppeld tooan IP-configuratie die nog geen die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="37343-154">**Associate hello resource tooan existing IP configuration** A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="37343-155">U kunt bepalen of een IP-configuratie een gekoppeld openbare IP-adres heeft door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="37343-155">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="37343-156">Geretourneerd uitvoer:</span><span class="sxs-lookup"><span data-stu-id="37343-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="37343-157">Sinds Hallo **PublicIpAddressId** kolom voor *IpConfig 3* is leeg in Hallo uitvoer geen openbare IP-adres-resource is momenteel gekoppeld tooit.</span><span class="sxs-lookup"><span data-stu-id="37343-157">Since hello **PublicIpAddressId** column for *IpConfig-3* is blank in hello output, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="37343-158">U kunt een bestaand openbaar IP-adres resource tooIpConfig-3 toevoegen, of Voer Hallo opdracht toocreate een volgende:</span><span class="sxs-lookup"><span data-stu-id="37343-158">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="37343-159">Voer Hallo opdracht resource toohello bestaande IP-configuratie met de naam van tooassociate Hallo openbare IP-adressen te volgen *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="37343-159">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="37343-160">Weergave Hallo privé IP-adressen en Hallo openbare IP-adres resource-id toegewezen toohello NIC door te voeren Hallo de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="37343-160">View hello private IP addresses and hello public IP address resource Ids assigned toohello NIC by entering hello following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="37343-161">Geretourneerd uitvoer:</span><span class="sxs-lookup"><span data-stu-id="37343-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="37343-162">Hallo privé IP-adressen u toohello NIC toohello VM-besturingssysteem toegevoegd door de instructies te volgen Hallo in Hallo toevoegen [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="37343-162">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="37343-163">Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="37343-163">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
