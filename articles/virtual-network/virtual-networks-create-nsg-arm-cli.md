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
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a>Netwerk met behulp van Azure CLI 2.0 Hallo beveiligingsgroepen maken

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak 

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren: 

- [Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen 
- [Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Hallo voorbeeld Azure CLI 2.0 opdrachten volgende verwacht een eenvoudige omgeving al gemaakt op basis van de voorgaande Hallo-scenario. 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a>Hallo NSG voor Hallo maken `FrontEnd` subnet

een NSG met de naam toocreate *NSG-FrontEnd* op basis van de voorgaande Hallo-scenario, volgt u Hallo stappen hieronder.

1. Als u dit nog niet hebt nog installeren en configureren van Hallo meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login). 

2. Maken van een NSG met Hallo [az netwerk nsg maken](/cli/azure/network/nsg#create) opdracht. 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    Parameters:
   
   * `--resource-group`: De naam van resourcegroep Hallo waar Hallo NSG wordt gemaakt. In ons scenario *TestRG*.
   * `--location`: De azure-regio waar hello nieuwe NSG gemaakt. In ons scenario *westus*.
   * `--name`: Naam voor Hallo nieuwe NSG. In ons scenario *NSG-FrontEnd*.

    Hallo verwachte uitvoer is erg een stukje informatie, waaronder een lijst met alle Hallo standaardregels. Hallo volgende voorbeeld ziet u Hallo standaardregels met een filter van de query JMESPATH Hello `table` uitvoerindeling:

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   Uitvoer:

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Maak een regel waarmee toegang tooport 3389 (RDP) van Hallo Internet Hello [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) opdracht.

    > [!NOTE]
    > Afhankelijk van het Hallo-shell u gebruikt, moet u mogelijk toomodify hello `*` teken Hallo argumenten na dat het geen tooexpand Hallo argument voordat wordt uitgevoerd.
   
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
   
    Verwachte uitvoer:
   
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

    Parameters:

    * `--resource-group testrg`: Hallo resource groep toouse. Houd er rekening mee dat het is niet hoofdlettergevoelig.
    * `--nsg-name NSG-FrontEnd`: De naam van Hallo NSG in welke Hallo regel is gemaakt.
    * `--name rdp-rule`: De naam voor de nieuwe regel Hallo.
    * `--access Allow`: Toegangsniveau voor Hallo regel (weigeren of toestaan).
    * `--protocol Tcp`: Protocol (Tcp, Udp of *).
    * `--direction Inbound`: De richting van het Hallo-verbinding (inkomend of uitgaand).
    * `--priority 100`: De prioriteit voor Hallo regel.
    * `--source-address-prefix Internet`: Bron-adresvoorvoegsel in CIDR- of met standaardlabels.
    * `--source-port-range "*"`: Poort of poortbereik van bron. De poort die Hallo verbinding geopend.
    * `--destination-address-prefix "*"`: Voorvoegsel voor doeladres in CIDR- of met standaardlabels.
    * `--destination-port-range 3389`: Bestemming poort of poortbereik. De poort die Hallo verbindingsaanvraag ontvangt.



4. Maak een regel waarmee toegang tooport 80 (HTTP) vanaf Internet Hallo **az netwerk nsg regel maken** opdracht.
   
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
   
    Verwachte putput:
   
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

5. Hallo NSG toohello binden **FrontEnd** subnet met Hallo [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) opdracht.
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    Verwachte uitvoer:
   
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

## <a name="create-hello-nsg-for-hello-backend-subnet"></a>Hallo NSG voor Hallo maken `BackEnd` subnet
een NSG met de naam toocreate *NSG-back-end* op basis van de voorgaande Hallo-scenario, volgt u Hallo stappen hieronder.

1. Hallo maken `NSG-BackEnd` NSG met **az netwerk nsg maken**.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    Zoals in stap 2, voorgaande, verwacht Hallo uitvoer is erg groot is, met inbegrip van standaardregels.
   
2. Maak een regel waarmee toegang tooport 1433 (SQL) van Hallo `FrontEnd` subnet met Hallo **az netwerk nsg regel maken** opdracht.
   
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
   
    Verwachte uitvoer:

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

3. Een regel maken waarmee toegang toohello Internet via weigert Hallo **az netwerk nsg regel maken** opdracht.
   
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
   
    Verwachte putput:
   
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

4. Hallo NSG toohello binden `BackEnd` subnet met Hallo **az network vnet subnet set** opdracht.
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    Verwachte uitvoer:
   
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
