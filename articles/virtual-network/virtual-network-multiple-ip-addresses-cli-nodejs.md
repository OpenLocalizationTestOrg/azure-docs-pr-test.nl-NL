---
title: aaaVM met meerdere IP-adressen met behulp van Azure CLI 1.0 Hallo | Microsoft Docs
description: Meer informatie over hoe tooassign meerdere IP-adressen tooa virtuele machine met Azure CLI 1.0 Hallo | Resource Manager.
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
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="44ddf-103">Meerdere IP-adressen toewijzen toovirtual machines met behulp van Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="44ddf-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="44ddf-104">Dit artikel wordt uitgelegd hoe een virtuele machine (VM) via hello Azure Resource Manager deployment model met behulp van toocreate hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="44ddf-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="44ddf-105">Meerdere IP-adressen kunnen niet worden toegewezen als tooresources via de klassieke implementatiemodel Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44ddf-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="44ddf-106">meer informatie over Azure-implementatiemodellen, Hallo lezen toolearn [begrijpen implementatiemodellen](../resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="44ddf-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="44ddf-107"><a name = "create"></a>Een virtuele machine maken met meerdere IP-adressen</span><span class="sxs-lookup"><span data-stu-id="44ddf-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="44ddf-108">U kunt deze taak uitvoeren met hello Azure CLI 1.0 (in dit artikel) of Hallo [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="44ddf-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="44ddf-109">Hallo in de volgende procedure wordt uitgelegd hoe toocreate een voorbeeld van de virtuele machine met meerdere IP-adressen, zoals beschreven in Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="44ddf-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="44ddf-110">Namen van variabelen en typen van de IP-adres zoals vereist voor uw implementatie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="44ddf-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="44ddf-111">Installeren en configureren van Azure CLI 1.0 door de volgende Hallo stappen Hallo in Hallo [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel en meld u aan bij uw Azure-account met Hallo `azure-login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="44ddf-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="44ddf-112">Een resourcegroep maken:</span><span class="sxs-lookup"><span data-stu-id="44ddf-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="44ddf-113">Een virtueel netwerk maken:</span><span class="sxs-lookup"><span data-stu-id="44ddf-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="44ddf-114">Een subnet in het virtuele netwerk Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="44ddf-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="44ddf-115">Maak een opslagaccount voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="44ddf-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="44ddf-116">Voordat u Hallo volgende opdracht, vervangt u *mystorageaccount* met een unieke naam.</span><span class="sxs-lookup"><span data-stu-id="44ddf-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="44ddf-117">Hallo-naam moet uniek zijn in Azure:</span><span class="sxs-lookup"><span data-stu-id="44ddf-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="44ddf-118">Hallo IP-configuraties, een NIC maken en toewijzen Hallo IP-configuraties toohello NIC.</span><span class="sxs-lookup"><span data-stu-id="44ddf-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="44ddf-119">U kunt toevoegen, verwijderen of Hallo configuraties zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="44ddf-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="44ddf-120">Hallo volgende configuraties worden beschreven in Hallo scenario:</span><span class="sxs-lookup"><span data-stu-id="44ddf-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="44ddf-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="44ddf-121">**IPConfig-1**</span></span>

    <span data-ttu-id="44ddf-122">Voer Hallo-opdrachten die toocreate volgen:</span><span class="sxs-lookup"><span data-stu-id="44ddf-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="44ddf-123">Een openbaar IP-adres-resource met een statische openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="44ddf-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="44ddf-124">Een NIC Hallo openbaar IP-adres en een tooit statisch privé IP-adres toewijzen.</span><span class="sxs-lookup"><span data-stu-id="44ddf-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="44ddf-125">Vervang *mypublicdns* met een naam die uniek is binnen hello Azure-locatie.</span><span class="sxs-lookup"><span data-stu-id="44ddf-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="44ddf-126">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="44ddf-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="44ddf-127">meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="44ddf-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="44ddf-128">Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="44ddf-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="44ddf-129">meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.</span><span class="sxs-lookup"><span data-stu-id="44ddf-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="44ddf-130">**IPConfig 2**</span><span class="sxs-lookup"><span data-stu-id="44ddf-130">**IPConfig-2**</span></span>

     <span data-ttu-id="44ddf-131">Voer Hallo opdrachten toocreate na een nieuwe bron voor openbare IP-adres en een nieuwe IP-configuratie met een statische openbare IP-adres en een statisch privé IP-adres:</span><span class="sxs-lookup"><span data-stu-id="44ddf-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="44ddf-132">**IPConfig 3**</span><span class="sxs-lookup"><span data-stu-id="44ddf-132">**IPConfig-3**</span></span>

    <span data-ttu-id="44ddf-133">Voer Hallo opdrachten toocreate een IP-configuratie met een statisch privé IP-adres en geen openbare IP-adres te volgen:</span><span class="sxs-lookup"><span data-stu-id="44ddf-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="44ddf-134">Hoewel dit artikel wordt toegewezen voor alle IP-configuraties tooa één NIC, u kunt ook meerdere IP-configuraties tooany NIC op een virtuele machine toewijzen.</span><span class="sxs-lookup"><span data-stu-id="44ddf-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="44ddf-135">toolearn hoe toocreate met meerdere NIC's, een virtuele machine lezen Hallo maken van een virtuele machine met meerdere NIC's artikel.</span><span class="sxs-lookup"><span data-stu-id="44ddf-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="44ddf-136">Een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="44ddf-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="44ddf-137">toochange hello VM grootte tooStandard DS2 v2, bijvoorbeeld toe te voegen na eigenschap Hallo `--vm-size Standard_DS3_v2` toohello `azure vm create` opdracht in stap 6.</span><span class="sxs-lookup"><span data-stu-id="44ddf-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="44ddf-138">Voer Hallo opdracht tooview Hallo NIC te volgen en Hallo bijbehorende IP-configuraties:</span><span class="sxs-lookup"><span data-stu-id="44ddf-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="44ddf-139">Toevoegen Hallo privé-IP-adressen toohello VM besturingssysteem via Hallo stappen voor het besturingssysteem in Hallo [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="44ddf-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="44ddf-140"><a name="add"></a>IP-adressen tooa VM toevoegen</span><span class="sxs-lookup"><span data-stu-id="44ddf-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="44ddf-141">U kunt extra persoonlijke en openbare IP-adressen tooan NIC bestaande via Hallo stappen volgen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="44ddf-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="44ddf-142">Hallo voorbeelden bouwen voort op Hallo [scenario](#Scenario) in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="44ddf-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="44ddf-143">Open Azure CLI en volledige Hallo resterende stappen in deze sectie binnen één CLI-sessie.</span><span class="sxs-lookup"><span data-stu-id="44ddf-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="44ddf-144">Als u nog geen Azure CLI geïnstalleerd en geconfigureerd, voltooid Hallo stappen voor het Hallo [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel en meld u aan bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="44ddf-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="44ddf-145">Voer Hallo stappen in een Hallo uit te voeren, op basis van uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="44ddf-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="44ddf-146">**Een persoonlijke IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="44ddf-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="44ddf-147">een persoonlijke IP-adres tooa NIC tooadd, moet u een IP-configuratie met behulp van Hallo onderstaande opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="44ddf-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="44ddf-148">Hallo statisch adres moet een niet-gebruikte adres voor het Hallo-subnet.</span><span class="sxs-lookup"><span data-stu-id="44ddf-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="44ddf-149">Configuraties die u nodig hebt, gebruik van unieke namen en privé IP-adressen (voor configuraties met statische IP-adressen) maken.</span><span class="sxs-lookup"><span data-stu-id="44ddf-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="44ddf-150">**Een openbaar IP-adres toevoegen**</span><span class="sxs-lookup"><span data-stu-id="44ddf-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="44ddf-151">Een openbaar IP-adres is toegevoegd door deze te koppelen tooeither een nieuwe IP-configuratie of een bestaande IP-configuratie.</span><span class="sxs-lookup"><span data-stu-id="44ddf-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="44ddf-152">Stappen Hallo in een van Hallo secties die volgen, die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="44ddf-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="44ddf-153">Openbare IP-adressen hebben een nominaal kosten.</span><span class="sxs-lookup"><span data-stu-id="44ddf-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="44ddf-154">meer over IP-prijzen toolearn lezen Hallo [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="44ddf-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="44ddf-155">Er is een limiet toohello aantal openbare IP-adressen die kunnen worden gebruikt in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="44ddf-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="44ddf-156">meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.</span><span class="sxs-lookup"><span data-stu-id="44ddf-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="44ddf-157">**Hallo resource tooa nieuwe IP-configuratie koppelen**</span><span class="sxs-lookup"><span data-stu-id="44ddf-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="44ddf-158">Als u een openbaar IP-adres in een nieuw IP-configuratie toevoegt, moet u ook een privé IP-adres toevoegen, omdat alle IP-configuraties moeten een particulier IP-adres hebben.</span><span class="sxs-lookup"><span data-stu-id="44ddf-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="44ddf-159">U kunt een bestaande resource voor openbare IP-adres toevoegen of u een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="44ddf-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="44ddf-160">toocreate een nieuw wachtwoord invoeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44ddf-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="44ddf-161">toocreate een nieuwe IP-configuratie met een statisch privé IP-adres en het Hallo gekoppeld *myPublicIP3* openbare IP-adres adres resource, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44ddf-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="44ddf-162">**Hallo resource tooan bestaande IP-configuratie koppelen**</span><span class="sxs-lookup"><span data-stu-id="44ddf-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="44ddf-163">Een openbare IP-adres resource kan alleen worden gekoppeld tooan IP-configuratie die nog geen die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="44ddf-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="44ddf-164">U kunt bepalen of een IP-configuratie een gekoppeld openbare IP-adres heeft door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44ddf-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="44ddf-165">Zoek naar een regel vergelijkbaar toohello die voor IPConfig 3 in Hallo uitvoer geretourneerd volgt:</span><span class="sxs-lookup"><span data-stu-id="44ddf-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="44ddf-166">Sinds Hallo **openbare IP-adres** kolom voor *IpConfig 3* is leeg, geen openbare IP-adres-resource is momenteel gekoppeld tooit.</span><span class="sxs-lookup"><span data-stu-id="44ddf-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="44ddf-167">U kunt een bestaand openbaar IP-adres resource tooIpConfig-3 toevoegen, of Voer Hallo opdracht toocreate een volgende:</span><span class="sxs-lookup"><span data-stu-id="44ddf-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="44ddf-168">Voer Hallo opdracht resource toohello bestaande IP-configuratie met de naam van tooassociate Hallo openbare IP-adressen te volgen *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="44ddf-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="44ddf-169">Hallo privé IP-adressen weergeven en Hallo openbare IP-adres resources toegewezen toohello NIC door te voeren Hallo de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44ddf-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="44ddf-170">Hallo geretourneerd uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="44ddf-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="44ddf-171">Hallo privé IP-adressen u toohello NIC toohello VM-besturingssysteem toegevoegd door de instructies te volgen Hallo in Hallo toevoegen [toevoegen IP-adressen tooa VM besturingssysteem](#os-config) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="44ddf-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="44ddf-172">Voeg geen Hallo openbare IP-adressen toohello besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="44ddf-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
