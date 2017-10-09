---
title: aaaCreate netwerkbeveiligingsgroepen - Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over hoe toocreate en netwerkbeveiligingsgroepen hello Azure CLI 2.0 met implementeren.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="65a46-103">Netwerk met behulp van Azure CLI 2.0 Hallo beveiligingsgroepen maken</span><span class="sxs-lookup"><span data-stu-id="65a46-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="65a46-104">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="65a46-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="65a46-105">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="65a46-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="65a46-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen</span><span class="sxs-lookup"><span data-stu-id="65a46-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="65a46-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="65a46-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="65a46-108">Hallo voorbeeld Azure CLI 2.0 opdrachten volgende verwacht een eenvoudige omgeving al gemaakt op basis van de voorgaande Hallo-scenario.</span><span class="sxs-lookup"><span data-stu-id="65a46-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="65a46-109">Hallo NSG voor Hallo maken `FrontEnd` subnet</span><span class="sxs-lookup"><span data-stu-id="65a46-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="65a46-110">een NSG met de naam toocreate *NSG-FrontEnd* op basis van de voorgaande Hallo-scenario, volgt u Hallo stappen hieronder.</span><span class="sxs-lookup"><span data-stu-id="65a46-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="65a46-111">Als u dit nog niet hebt nog installeren en configureren van Hallo meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="65a46-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="65a46-112">Maken van een NSG met Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="65a46-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="65a46-113">Parameters:</span><span class="sxs-lookup"><span data-stu-id="65a46-113">Parameters:</span></span>
   
   * <span data-ttu-id="65a46-114">`--resource-group`: De naam van resourcegroep Hallo waar Hallo NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65a46-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="65a46-115">In ons scenario *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="65a46-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="65a46-116">`--location`: De azure-regio waar hello nieuwe NSG gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65a46-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="65a46-117">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="65a46-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="65a46-118">`--name`: Naam voor Hallo nieuwe NSG.</span><span class="sxs-lookup"><span data-stu-id="65a46-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="65a46-119">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="65a46-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="65a46-120">Hallo verwachte uitvoer is erg een stukje informatie, waaronder een lijst met alle Hallo standaardregels.</span><span class="sxs-lookup"><span data-stu-id="65a46-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="65a46-121">Hallo volgende voorbeeld ziet u Hallo standaardregels met een filter van de query JMESPATH Hello `table` uitvoerindeling:</span><span class="sxs-lookup"><span data-stu-id="65a46-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="65a46-122">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="65a46-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="65a46-123">Maak een regel waarmee toegang tooport 3389 (RDP) van Hallo Internet Hello [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="65a46-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="65a46-124">Afhankelijk van het Hallo-shell u gebruikt, moet u mogelijk toomodify hello `*` teken Hallo argumenten na dat het geen tooexpand Hallo argument voordat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65a46-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="65a46-125">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="65a46-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="65a46-126">Parameters:</span><span class="sxs-lookup"><span data-stu-id="65a46-126">Parameters:</span></span>

    * <span data-ttu-id="65a46-127">`--resource-group testrg`: Hallo resource groep toouse.</span><span class="sxs-lookup"><span data-stu-id="65a46-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="65a46-128">Houd er rekening mee dat het is niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="65a46-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="65a46-129">`--nsg-name NSG-FrontEnd`: De naam van Hallo NSG in welke Hallo regel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65a46-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="65a46-130">`--name rdp-rule`: De naam voor de nieuwe regel Hallo.</span><span class="sxs-lookup"><span data-stu-id="65a46-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="65a46-131">`--access Allow`: Toegangsniveau voor Hallo regel (weigeren of toestaan).</span><span class="sxs-lookup"><span data-stu-id="65a46-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="65a46-132">`--protocol Tcp`: Protocol (Tcp, Udp of *).</span><span class="sxs-lookup"><span data-stu-id="65a46-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="65a46-133">`--direction Inbound`: De richting van het Hallo-verbinding (inkomend of uitgaand).</span><span class="sxs-lookup"><span data-stu-id="65a46-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="65a46-134">`--priority 100`: De prioriteit voor Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="65a46-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="65a46-135">`--source-address-prefix Internet`: Bron-adresvoorvoegsel in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="65a46-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="65a46-136">`--source-port-range "*"`: Poort of poortbereik van bron.</span><span class="sxs-lookup"><span data-stu-id="65a46-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="65a46-137">De poort die Hallo verbinding geopend.</span><span class="sxs-lookup"><span data-stu-id="65a46-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="65a46-138">`--destination-address-prefix "*"`: Voorvoegsel voor doeladres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="65a46-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="65a46-139">`--destination-port-range 3389`: Bestemming poort of poortbereik.</span><span class="sxs-lookup"><span data-stu-id="65a46-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="65a46-140">De poort die Hallo verbindingsaanvraag ontvangt.</span><span class="sxs-lookup"><span data-stu-id="65a46-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="65a46-141">Maak een regel waarmee toegang tooport 80 (HTTP) vanaf Internet Hallo **az netwerk nsg regel maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="65a46-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="65a46-142">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="65a46-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="65a46-143">Hallo NSG toohello binden **FrontEnd** subnet met Hallo [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="65a46-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="65a46-144">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="65a46-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="65a46-145">Hallo NSG voor Hallo maken `BackEnd` subnet</span><span class="sxs-lookup"><span data-stu-id="65a46-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="65a46-146">een NSG met de naam toocreate *NSG-back-end* op basis van de voorgaande Hallo-scenario, volgt u Hallo stappen hieronder.</span><span class="sxs-lookup"><span data-stu-id="65a46-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="65a46-147">Hallo maken `NSG-BackEnd` NSG met **az netwerk nsg maken**.</span><span class="sxs-lookup"><span data-stu-id="65a46-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="65a46-148">Zoals in stap 2, voorgaande, verwacht Hallo uitvoer is erg groot is, met inbegrip van standaardregels.</span><span class="sxs-lookup"><span data-stu-id="65a46-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="65a46-149">Maak een regel waarmee toegang tooport 1433 (SQL) van Hallo `FrontEnd` subnet met Hallo **az netwerk nsg regel maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="65a46-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="65a46-150">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="65a46-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="65a46-151">Een regel maken waarmee toegang toohello Internet via weigert Hallo **az netwerk nsg regel maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="65a46-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="65a46-152">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="65a46-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="65a46-153">Hallo NSG toohello binden `BackEnd` subnet met Hallo **az network vnet subnet set** opdracht.</span><span class="sxs-lookup"><span data-stu-id="65a46-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="65a46-154">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="65a46-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
