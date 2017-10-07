---
title: "privé IP-adressen voor virtuele machines - Azure CLI 2.0 aaaConfigure | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé IP-adressen voor virtuele machines met hello Azure-opdrachtregelinterface (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Privé IP-adressen voor een virtuele machine met behulp van Azure CLI 2.0 Hallo configureren

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak 

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren: 

- [Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen 
- [Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel. U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel Hallo beheren](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> Hello Azure CLI 2.0 Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt. Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Bij het maken van een virtuele machine een statisch privé IP-adres opgeven

een virtuele machine met de naam toocreate *DNS01* in Hallo *FrontEnd* subnet van een VNet met de naam *TestVNet* met een statisch privé IP-adres van *192.168.1.101*, Volg onderstaande stappen voor Hallo:

1. Als u dit nog niet hebt nog installeren en configureren van Hallo meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login). 

2. Maken van een openbaar IP-adres voor Hallo VM Hello [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create) opdracht. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.

    > [!NOTE]
    > Mogelijk moet of wilt u verschillende waarden voor uw argumenten in deze toouse en daaropvolgende stappen, afhankelijk van uw omgeving.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Verwachte uitvoer:
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Naam van de resourcegroep Hallo in welke toocreate Hallo openbare IP-adres.
   * `--name`: De naam van Hallo openbare IP-adres.
   * `--location`: De azure-regio in welke toocreate Hallo openbare IP-adres.

3. Voer Hallo [az netwerk nic maken](/cli/azure/network/nic#create) opdracht toocreate een NIC met een statisch privé IP-adres. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Verwachte uitvoer:
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Parameters:

    * `--private-ip-address`: Statische privé IP-adres voor Hallo NIC.
    * `--vnet-name`: De naam van Hallo VNet in welke toocreate Hallo NIC.
    * `--subnet`: De naam van Hallo subnet in welke toocreate Hallo NIC.

4. Voer Hallo [azure vm maken](/cli/azure/vm/nic#create) opdracht toocreate Hallo VM die gebruikmaakt van Hallo openbare IP-adres en NIC die eerder is gemaakt. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Verwachte uitvoer:
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   Andere parameters dan Hallo basic [az vm maken](/cli/azure/vm#create) parameters.

   * `--nics`: De naam van Hallo NIC toowhich Hallo VM is gekoppeld.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Statische persoonlijke IP-adresgegevens voor een virtuele machine ophalen

tooview hello statisch privé IP-adres dat u hebt gemaakt, Hallo na Azure CLI-opdracht uitgevoerd en zien Hallo waarden voor *toewijzingseenheid particuliere IP-methode* en *particuliere IP-adres*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Verwachte uitvoer:

```json
"192.168.1.101"
```

toodisplay Hallo specifiek specifieke IP-informatie van Hallo NIC voor die VM, query Hallo NIC:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

Hallo uitvoer ziet er ongeveer als volgt:

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Een statisch privé IP-adres van een virtuele machine verwijderen

U kunt een statisch privé IP-adres niet verwijderen uit een NIC in Azure CLI voor implementaties van resource manager. U moet doen:
- Maak een nieuwe NIC die gebruikmaakt van een dynamische IP-adres
- Hallo NIC ingesteld op Hallo VM Hallo nieuw gemaakte NIC. 

toochange hello NIC voor VM die wordt gebruikt in Hallo opdrachten bovenstaande Hallo Hallo volgende stappen.

1. Voer Hallo **nic azure-netwerk maken** toocreate opdracht een nieuwe NIC met dynamische IP-toewijzing met een nieuw IP-adres. Houd er rekening mee dat omdat er geen IP-adres is opgegeven, Hallo toewijzingsmethode **dynamische**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Verwachte uitvoer:

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Voer Hallo **azure vm set** opdracht toochange Hallo NIC die wordt gebruikt door Hallo VM.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Verwachte uitvoer:
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Als Hallo VM groot genoeg toohave is meer dan één NIC, Voer Hallo **azure-netwerk nic verwijderen** opdracht toodelete Hallo oude NIC.
   
## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.
* Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.
* Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).

