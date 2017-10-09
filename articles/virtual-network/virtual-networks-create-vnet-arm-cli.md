---
title: een virtueel netwerk - Azure CLI 2.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk met Azure CLI 2.0 Hallo.
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
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="2c7bf-103">Een virtueel netwerk maken met hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2c7bf-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="2c7bf-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2c7bf-105">Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="2c7bf-106">Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2c7bf-107">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="2c7bf-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="2c7bf-108">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="2c7bf-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen</span><span class="sxs-lookup"><span data-stu-id="2c7bf-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="2c7bf-110">[Azure CLI 2.0](#create-a-virtual-network) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)'</span><span class="sxs-lookup"><span data-stu-id="2c7bf-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="2c7bf-111">Ook kunt u een VNet via Resource Manager, met andere hulpprogramma's maken of maak een VNet via de klassieke implementatiemodel Hallo door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c7bf-112">Portal</span><span class="sxs-lookup"><span data-stu-id="2c7bf-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="2c7bf-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c7bf-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="2c7bf-114">CLI</span><span class="sxs-lookup"><span data-stu-id="2c7bf-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="2c7bf-115">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="2c7bf-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="2c7bf-116">Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="2c7bf-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="2c7bf-117">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="2c7bf-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="2c7bf-118">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="2c7bf-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="2c7bf-119">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="2c7bf-119">Create a virtual network</span></span>

<span data-ttu-id="2c7bf-120">een virtueel netwerk met toocreate hello Azure CLI 2.0, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="2c7bf-121">Installeer en configureer Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2c7bf-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="2c7bf-122">Een resourcegroep maken voor uw VNet met Hallo [az groep maken](/cli/azure/group#create) opdracht Hello `--name` en `--location` argumenten:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="2c7bf-123">Een VNet en een subnet maken:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="2c7bf-124">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-124">Expected output:</span></span>
    
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

    <span data-ttu-id="2c7bf-125">Gebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-125">Parameters used:</span></span>

    - <span data-ttu-id="2c7bf-126">`--name TestVNet`: De naam van Hallo VNet toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="2c7bf-127">`--resource-group TestRG`: # Hallo Resourcegroepnaam die Hallo resource bepaalt.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="2c7bf-128">`--location centralus`: locatie naar welke toodeploy Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="2c7bf-129">`--address-prefix 192.168.0.0/16`: Hallo adresvoorvoegsel en blokkeren.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="2c7bf-130">`--subnet-name FrontEnd`: Hallo-naam van het Hallo-subnet.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="2c7bf-131">`--subnet-prefix 192.168.1.0/24`: Hallo adresvoorvoegsel en blokkeren.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="2c7bf-132">toolist hello basisinformatie toouse in Hallo naast uitvoert, en u kunt een query Hallo VNet met behulp van een [queryfilter](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="2c7bf-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="2c7bf-133">Hallo na uitvoer, die wordt gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="2c7bf-134">Een subnet maken:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="2c7bf-135">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-135">Expected output:</span></span>

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

    <span data-ttu-id="2c7bf-136">Gebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-136">Parameters used:</span></span>

    - <span data-ttu-id="2c7bf-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="2c7bf-138">`--name BackEnd`: De naam van nieuw subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="2c7bf-139">`--resource-group TestRG`: Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="2c7bf-140">`--vnet-name TestVNet`: naam Hallo Hallo die eigenaar is van VNet.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="2c7bf-141">Query Hallo eigenschappen van nieuwe VNet Hallo:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="2c7bf-142">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="2c7bf-143">Eigenschappen van de query Hallo van Hallo subnetten:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="2c7bf-144">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="2c7bf-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c7bf-145">Next steps</span></span>

<span data-ttu-id="2c7bf-146">Meer informatie over hoe tooconnect:</span><span class="sxs-lookup"><span data-stu-id="2c7bf-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="2c7bf-147">Een virtueel netwerk van virtuele machine (VM) tooa door te lezen Hallo [maken van een Linux-VM](../virtual-machines/linux/quick-create-cli.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="2c7bf-148">In plaats van een VNet en een subnet maken in stappen van Hallo artikelen hello, kunt u een bestaande VNet en een subnet tooconnect een virtuele machine aan.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="2c7bf-149">virtueel netwerk tooother virtuele netwerken door te lezen Hallo Hallo [VNets verbinden](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="2c7bf-150">Hallo virtueel netwerk tooan on-premises netwerk met een site-naar-site virtueel particulier netwerk (VPN) of het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="2c7bf-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="2c7bf-151">Meer informatie over hoe u door te lezen Hallo [verbinding maken met een VNet tooan on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [koppelen van een VNet tooan ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2c7bf-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
