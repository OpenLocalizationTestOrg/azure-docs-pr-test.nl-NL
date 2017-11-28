---
title: Beheren van Routering en virtuele apparaten met behulp van de Azure CLI 2.0 | Microsoft Docs
description: Informatie over het beheren van Routering en virtuele apparaten met behulp van de Azure CLI 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: e5d9519998346619093f443b740c8904283f76e8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-20"></a><span data-ttu-id="3a8f9-103">Door de gebruiker gedefinieerde Routes (UDR) met behulp van de Azure CLI 2.0 maken</span><span class="sxs-lookup"><span data-stu-id="3a8f9-103">Create User-Defined Routes (UDR) using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a8f9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a8f9-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="3a8f9-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3a8f9-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="3a8f9-106">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="3a8f9-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="3a8f9-107">PowerShell (klassieke implementatie)</span><span class="sxs-lookup"><span data-stu-id="3a8f9-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="3a8f9-108">CLI (klassieke implementatie)</span><span class="sxs-lookup"><span data-stu-id="3a8f9-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="3a8f9-109">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="3a8f9-109">CLI versions to complete the task</span></span> 

<span data-ttu-id="3a8f9-110">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-110">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="3a8f9-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="3a8f9-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="3a8f9-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -onze volgende generatie CLI voor de resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="3a8f9-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="3a8f9-113">De Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van het bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-113">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="3a8f9-114">Als u wilt de opdrachten uitvoeren zoals ze worden weergegeven in dit document, moet u eerst de testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), klikt u op **implementeren in Azure**, vervangt u de standaardwaarden voor parameters indien nodig en volg de instructies in de portal.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-114">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="3a8f9-115">De UDR voor de front-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="3a8f9-115">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="3a8f9-116">Volg de onderstaande stappen voor het maken van de routetabel en de route die nodig zijn voor de front-end-subnet op basis van de bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="3a8f9-117">Maken van een routetabel voor het front-end-subnet met de [az netwerk routetabel maken](/cli/azure/network/route-table#create) opdracht:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-117">Create a route table for the front-end subnet with the [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="3a8f9-118">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="3a8f9-119">Maken van een route dat al het verkeer naar de back-end-subnet (192.168.2.0/24) verzendt naar de **FW1** VM (192.168.0.4) met behulp van de [az routetabel netwerkroute maken](/cli/azure/network/route-table/route#create) opdracht:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-119">Create a route that sends all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4) using the [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="3a8f9-120">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="3a8f9-121">Parameters:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-121">Parameters:</span></span>

    * <span data-ttu-id="3a8f9-122">**--route tabelnaam**.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-122">**--route-table-name**.</span></span> <span data-ttu-id="3a8f9-123">Naam van de routetabel waar de route wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-123">Name of the route table where the route will be added.</span></span> <span data-ttu-id="3a8f9-124">In ons scenario *UDR FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="3a8f9-125">**--adresvoorvoegsel**.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-125">**--address-prefix**.</span></span> <span data-ttu-id="3a8f9-126">Het adresvoorvoegsel voor het subnet waarin pakketten naar.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-126">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="3a8f9-127">In ons scenario *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="3a8f9-128">**--volgende hoptype**.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-128">**--next-hop-type**.</span></span> <span data-ttu-id="3a8f9-129">Type object verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="3a8f9-130">Mogelijke waarden zijn *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, of *geen*.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="3a8f9-131">**--volgende hop-ip-adressen**.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="3a8f9-132">IP-adres voor de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-132">IP address for next hop.</span></span> <span data-ttu-id="3a8f9-133">In ons scenario *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="3a8f9-134">Voer de [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) opdracht voor het koppelen van de routetabel die eerder is gemaakt met de **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-134">Run the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="3a8f9-135">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="3a8f9-136">Parameters:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-136">Parameters:</span></span>
    
    * <span data-ttu-id="3a8f9-137">**--vnet naam**.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-137">**--vnet-name**.</span></span> <span data-ttu-id="3a8f9-138">De naam van de VNet waar het subnet bevindt.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-138">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="3a8f9-139">In ons scenario *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="3a8f9-140">De UDR voor de back-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="3a8f9-140">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="3a8f9-141">Voor het maken van de routetabel en de route die nodig zijn voor de back-end-subnet op basis van het bovenstaande scenario, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-141">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="3a8f9-142">Voer de volgende opdracht voor het maken van een routetabel voor de back-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-142">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="3a8f9-143">Voer de volgende opdracht voor het maken van een route in de routetabel alle verkeer dat is bestemd voor het front-end-subnet (192.168.1.0/24) te verzenden naar de **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="3a8f9-143">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="3a8f9-144">Voer de volgende opdracht om te koppelen van de routetabel met de **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-144">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="3a8f9-145">Doorsturen via IP op FW1 inschakelen</span><span class="sxs-lookup"><span data-stu-id="3a8f9-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="3a8f9-146">Om in te schakelen doorsturen via IP in de NIC die wordt gebruikt door **FW1**, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-146">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="3a8f9-147">Voer de [az netwerk nic weergeven](/cli/azure/network/nic#show) opdracht met een filter JMESPATH om weer te geven van de huidige **enable--doorsturen via ip** waarde voor **doorsturen via IP inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-147">Run the [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter to display the current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="3a8f9-148">Moet worden ingesteld op *false*.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-148">It should be set to *false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="3a8f9-149">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-149">Output:</span></span>

        false

2. <span data-ttu-id="3a8f9-150">Voer de volgende opdracht doorsturen via IP inschakelen:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-150">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="3a8f9-151">Bekijk de uitvoer naar de console gestreamd of alleen testen voor de specifieke **enableIpForwarding** waarde:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-151">You can examine the output streamed to the console, or just retest for the specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="3a8f9-152">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-152">Output:</span></span>

        true

    <span data-ttu-id="3a8f9-153">Parameters:</span><span class="sxs-lookup"><span data-stu-id="3a8f9-153">Parameters:</span></span>

    <span data-ttu-id="3a8f9-154">**---doorsturen via ip**: *true* of *false*.</span><span class="sxs-lookup"><span data-stu-id="3a8f9-154">**--ip-forwarding**: *true* or *false*.</span></span>

