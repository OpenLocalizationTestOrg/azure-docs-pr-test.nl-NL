---
title: Maak een virtueel netwerk - Azure CLI 2.0 | Microsoft Docs
description: Informatie over het maken van een virtueel netwerk met de Azure CLI 2.0.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c7d7b3543f488aedff1ea2c68a2b497e0ca744af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli-20"></a><span data-ttu-id="11ce1-103">Een virtueel netwerk maken met de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="11ce1-103">Create a virtual network using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="11ce1-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="11ce1-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="11ce1-105">Microsoft raadt aan resources te maken via het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="11ce1-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="11ce1-106">Lees het artikel [Azure-implementatiemodellen begrijpen](../azure-resource-manager/resource-manager-deployment-model.md) voor meer informatie over de verschillen tussen de twee modellen.</span><span class="sxs-lookup"><span data-stu-id="11ce1-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="11ce1-107">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="11ce1-107">CLI versions to complete the task</span></span>
<span data-ttu-id="11ce1-108">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="11ce1-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="11ce1-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="11ce1-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="11ce1-110">[Azure CLI 2.0](#create-a-virtual-network) -onze volgende generatie CLI voor de resource management-implementatiemodel (in dit artikel)'</span><span class="sxs-lookup"><span data-stu-id="11ce1-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="11ce1-111">U kunt via Resource Manager ook een VNet maken met andere hulpprogramma's. Bovendien kunt u een VNet maken via het klassieke implementatiemodel door in de volgende lijst een andere optie te selecteren:</span><span class="sxs-lookup"><span data-stu-id="11ce1-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="11ce1-112">Portal</span><span class="sxs-lookup"><span data-stu-id="11ce1-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="11ce1-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11ce1-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="11ce1-114">CLI</span><span class="sxs-lookup"><span data-stu-id="11ce1-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="11ce1-115">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="11ce1-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="11ce1-116">Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="11ce1-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="11ce1-117">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="11ce1-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="11ce1-118">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="11ce1-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="11ce1-119">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="11ce1-119">Create a virtual network</span></span>

<span data-ttu-id="11ce1-120">Voor het maken van een virtueel netwerk met de Azure CLI 2.0, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="11ce1-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span></span>

1. <span data-ttu-id="11ce1-121">Installeren en configureren van de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u aan op een Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="11ce1-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="11ce1-122">Maak een resourcegroep voor uw VNet met de [az groep maken](/cli/azure/group#create) opdracht met de `--name` en `--location` argumenten:</span><span class="sxs-lookup"><span data-stu-id="11ce1-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="11ce1-123">Een VNet en een subnet maken:</span><span class="sxs-lookup"><span data-stu-id="11ce1-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="11ce1-124">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="11ce1-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="11ce1-125">Gebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="11ce1-125">Parameters used:</span></span>

    - <span data-ttu-id="11ce1-126">`--name TestVNet`: De naam van het VNet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11ce1-126">`--name TestVNet`: Name of the VNet to be created.</span></span>
    - <span data-ttu-id="11ce1-127">`--resource-group TestRG`: # Naam van de resourcegroep die bepaalt van de resource.</span><span class="sxs-lookup"><span data-stu-id="11ce1-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span></span> 
    - <span data-ttu-id="11ce1-128">`--location centralus`: De locatie waarin te implementeren.</span><span class="sxs-lookup"><span data-stu-id="11ce1-128">`--location centralus`: The location into which to deploy.</span></span>
    - <span data-ttu-id="11ce1-129">`--address-prefix 192.168.0.0/16`: De adresvoorvoegsel en het blok.</span><span class="sxs-lookup"><span data-stu-id="11ce1-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span></span>  
    - <span data-ttu-id="11ce1-130">`--subnet-name FrontEnd`: De naam van het subnet.</span><span class="sxs-lookup"><span data-stu-id="11ce1-130">`--subnet-name FrontEnd`: The name of the subnet.</span></span>
    - <span data-ttu-id="11ce1-131">`--subnet-prefix 192.168.1.0/24`: De adresvoorvoegsel en het blok.</span><span class="sxs-lookup"><span data-stu-id="11ce1-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span></span>

    <span data-ttu-id="11ce1-132">Als u de basisinformatie moet worden gebruikt in de volgende opdracht, u kunt een query de VNet via een [queryfilter](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="11ce1-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="11ce1-133">Dit wordt de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="11ce1-133">Which produces the following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="11ce1-134">Een subnet maken:</span><span class="sxs-lookup"><span data-stu-id="11ce1-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="11ce1-135">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="11ce1-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="11ce1-136">Gebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="11ce1-136">Parameters used:</span></span>

    - <span data-ttu-id="11ce1-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="11ce1-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="11ce1-138">`--name BackEnd`: De naam van het nieuwe subnet.</span><span class="sxs-lookup"><span data-stu-id="11ce1-138">`--name BackEnd`: Name of the new subnet.</span></span>
    - <span data-ttu-id="11ce1-139">`--resource-group TestRG`: De resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="11ce1-139">`--resource-group TestRG`: The resource group.</span></span>
    - <span data-ttu-id="11ce1-140">`--vnet-name TestVNet`: De naam van de eigenaar VNet.</span><span class="sxs-lookup"><span data-stu-id="11ce1-140">`--vnet-name TestVNet`: The name of the owning VNet.</span></span>

5. <span data-ttu-id="11ce1-141">Opvragen van de eigenschappen van de nieuwe VNet:</span><span class="sxs-lookup"><span data-stu-id="11ce1-141">Query the properties of the new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="11ce1-142">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="11ce1-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="11ce1-143">Opvragen van de eigenschappen van de subnetten:</span><span class="sxs-lookup"><span data-stu-id="11ce1-143">Query the properties of the subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="11ce1-144">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="11ce1-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="11ce1-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11ce1-145">Next steps</span></span>

<span data-ttu-id="11ce1-146">Leer hoe u de volgende verbindingen maakt:</span><span class="sxs-lookup"><span data-stu-id="11ce1-146">Learn how to connect:</span></span>

- <span data-ttu-id="11ce1-147">Een virtuele machine (VM) met een virtueel netwerk door het lezen van de [maken van een Linux-VM](../virtual-machines/linux/quick-create-cli.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="11ce1-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="11ce1-148">In plaats van een VNet en subnet te maken via de stappen die in de artikelen worden beschreven, kunt u ook een bestaand VNet en subnet selecteren waarmee u een VM wilt verbinden.</span><span class="sxs-lookup"><span data-stu-id="11ce1-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="11ce1-149">Verbinding van het virtuele netwerk met andere virtuele netwerken: lees het artikel [VNets verbinden](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11ce1-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="11ce1-150">Verbinding van het virtuele netwerk met een on-premises netwerk via een site-naar-site virtueel particulier netwerk (VPN) of een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="11ce1-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="11ce1-151">Meer informatie over hoe door het lezen van de [verbinding van een VNet met een on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [een VNet koppelen aan een ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="11ce1-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>