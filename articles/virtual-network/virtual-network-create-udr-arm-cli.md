---
title: aaaControl Routering en virtuele apparaten via Azure CLI 2.0 Hallo | Microsoft Docs
description: Meer informatie over hoe toocontrol Routering en virtuele apparaten via Azure CLI 2.0 Hallo.
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
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="a5b3b-103">Door de gebruiker gedefinieerde Routes (UDR) met behulp van Azure CLI 2.0 Hallo maken</span><span class="sxs-lookup"><span data-stu-id="a5b3b-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5b3b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5b3b-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="a5b3b-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a5b3b-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="a5b3b-106">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="a5b3b-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="a5b3b-107">PowerShell (klassieke implementatie)</span><span class="sxs-lookup"><span data-stu-id="a5b3b-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="a5b3b-108">CLI (klassieke implementatie)</span><span class="sxs-lookup"><span data-stu-id="a5b3b-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a5b3b-109">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="a5b3b-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="a5b3b-110">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="a5b3b-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen</span><span class="sxs-lookup"><span data-stu-id="a5b3b-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="a5b3b-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="a5b3b-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="a5b3b-113">Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="a5b3b-114">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, moet u eerst Hallo testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), klikt u op **tooAzure implementeren**, standaardparameterwaarden Hallo vervangen indien nodig, en volg de instructies in Hallo in Hallo portal.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="a5b3b-115">Hallo UDR voor Hallo front-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="a5b3b-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="a5b3b-116">toocreate hello routetabel en route die nodig zijn voor Hallo front-end-subnet op basis van Hallo scenario bovenstaande stappen Hallo hieronder.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="a5b3b-117">Een routetabel voor Hallo front-end-subnet maken met de Hallo [az netwerk routetabel maken](/cli/azure/network/route-table#create) opdracht:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="a5b3b-118">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-118">Output:</span></span>

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

2. <span data-ttu-id="a5b3b-119">Maken van een route die alle verkeer dat is bestemd toohello back-end-subnet (192.168.2.0/24) toohello verzendt **FW1** VM (192.168.0.4) met behulp van Hallo [az routetabel netwerkroute maken](/cli/azure/network/route-table/route#create) opdracht:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="a5b3b-120">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-120">Output:</span></span>

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
    <span data-ttu-id="a5b3b-121">Parameters:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-121">Parameters:</span></span>

    * <span data-ttu-id="a5b3b-122">**--route tabelnaam**.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-122">**--route-table-name**.</span></span> <span data-ttu-id="a5b3b-123">Naam van de routetabel Hallo waar Hallo route wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="a5b3b-124">In ons scenario *UDR FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="a5b3b-125">**--adresvoorvoegsel**.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-125">**--address-prefix**.</span></span> <span data-ttu-id="a5b3b-126">Het adresvoorvoegsel voor Hallo subnet waar pakketten zijn bestemd voor.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="a5b3b-127">In ons scenario *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="a5b3b-128">**--volgende hoptype**.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-128">**--next-hop-type**.</span></span> <span data-ttu-id="a5b3b-129">Type object verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="a5b3b-130">Mogelijke waarden zijn *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, of *geen*.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="a5b3b-131">**--volgende hop-ip-adressen**.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="a5b3b-132">IP-adres voor de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-132">IP address for next hop.</span></span> <span data-ttu-id="a5b3b-133">In ons scenario *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="a5b3b-134">Voer Hallo [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) opdracht tooassociate Hallo routetabel die eerder is gemaakt met de Hallo **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="a5b3b-135">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-135">Output:</span></span>

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

    <span data-ttu-id="a5b3b-136">Parameters:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-136">Parameters:</span></span>
    
    * <span data-ttu-id="a5b3b-137">**--vnet naam**.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-137">**--vnet-name**.</span></span> <span data-ttu-id="a5b3b-138">Naam van Hallo VNet waar Hallo subnet bevindt.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="a5b3b-139">In ons scenario *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="a5b3b-140">Hallo UDR voor Hallo back-end subnet maken</span><span class="sxs-lookup"><span data-stu-id="a5b3b-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="a5b3b-141">toocreate hello routetabel en te routeren die nodig zijn voor Hallo back-end-subnet op basis van Hallo scenario hierboven voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="a5b3b-142">Voer Hallo opdracht toocreate na een routetabel voor Hallo back-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="a5b3b-143">Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello front-end-subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="a5b3b-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="a5b3b-144">Voer hello na de opdracht tooassociate Hallo routetabel Hello **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="a5b3b-145">Doorsturen via IP op FW1 inschakelen</span><span class="sxs-lookup"><span data-stu-id="a5b3b-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="a5b3b-146">doorsturen via IP in Hallo NIC die wordt gebruikt door tooenable **FW1**, volledige Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="a5b3b-147">Voer Hallo [az netwerk nic weergeven](/cli/azure/network/nic#show) opdracht met een huidige van JMESPATH filter toodisplay hello **enable--doorsturen via ip** waarde voor **doorsturen via IP inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="a5b3b-148">Deze dient te worden ingesteld*false*.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="a5b3b-149">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-149">Output:</span></span>

        false

2. <span data-ttu-id="a5b3b-150">Voer Hallo doorsturen via IP van opdracht tooenable te volgen:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="a5b3b-151">Hallo uitvoer gestreamde toohello console controleren of alleen voor specifieke Hallo testen **enableIpForwarding** waarde:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="a5b3b-152">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-152">Output:</span></span>

        true

    <span data-ttu-id="a5b3b-153">Parameters:</span><span class="sxs-lookup"><span data-stu-id="a5b3b-153">Parameters:</span></span>

    <span data-ttu-id="a5b3b-154">**---doorsturen via ip**: *true* of *false*.</span><span class="sxs-lookup"><span data-stu-id="a5b3b-154">**--ip-forwarding**: *true* or *false*.</span></span>

