---
title: aaaManage netwerkbeveiligingsgroepen - Azure PowerShell | Microsoft Docs
description: Meer informatie over hoe toomanage netwerkbeveiligingsgroepen met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a>Netwerkbeveiligingsgroepen met behulp van PowerShell beheren

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md). In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>Informatie ophalen
U kunt uw bestaande nsg's weergeven, regels voor een bestaande NSG ophalen en weten welke resources een NSG is gekoppeld aan.

### <a name="view-existing-nsgs"></a>Bestaande nsg's weergeven
tooview alle bestaande nsg's in een abonnement uitvoeren Hallo `Get-AzureRmNetworkSecurityGroup` cmdlet.

Verwachte resultaat:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


tooview hello lijst met nsg's in een specifieke resourcegroep of Voer Hallo `Get-AzureRmNetworkSecurityGroup` cmdlet.

Verwachte uitvoer:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a>Lijst met alle regels voor een NSG
tooview hello regels van een NSG met de naam **NSG-FrontEnd**, Voer Hallo volgende opdracht:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

Verwachte uitvoer:

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> U kunt ook `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist Hallo standaardregels van Hallo **NSG-FrontEnd** NSG.
> 

### <a name="view-nsgs-associations"></a>Nsg's koppelingen weergeven
tooview welke resources Hallo **NSG-FrontEnd** NSG is met, voert hello van de volgende opdracht:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

Zoek naar Hallo **NetworkInterfaces** en **subnetten** eigenschappen zoals hieronder wordt weergegeven:

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

In het vorige voorbeeld Hallo is Hallo NSG niet gekoppeld tooany netwerkinterfaces (NIC's); het is gekoppeld tooa subnet met de naam **FrontEnd**.

## <a name="manage-rules"></a>Regels beheren
U kunt regels tooan bestaande NSG toevoegen, bestaande regels bewerken en regels te verwijderen.

### <a name="add-a-rule"></a>Een regel toevoegen
tooadd een regel waarmee **inkomende** verkeer tooport **443** van een machine toohello **NSG-FrontEnd** NSG, volledige Hallo stappen te volgen:

1. Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hallo opdracht tooadd na een regel toohello NSG uitvoeren:

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello wijzigingen aangebracht toohello NSG, Hallo volgende opdracht uitvoeren:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    Verwachte uitvoer alleen Hallo beveiligingsregels voor verbindingen met:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a>Een regel wijzigen
toochange hello regel bovenstaande tooallow binnenkomend verkeer van Hallo **Internet** alleen Hallo volgende stappen.

1. Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Voer Hallo opdracht met de nieuwe regelinstellingen Hallo te volgen:

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello wijzigingen aangebracht toohello NSG, Hallo volgende opdracht uitvoeren:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Verwachte uitvoer alleen Hallo beveiligingsregels voor verbindingen met:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a>Een regel verwijderen
1. Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hallo volgende opdracht tooremove Hallo regel uit Hallo NSG uitvoeren:

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. Hallo wijzigingen toohello NSG, door het uitvoeren van de volgende opdracht Hallo opslaan:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Verwachte uitvoer met alleen Hallo beveiligingsregels, kennisgeving Hallo **https-regel** wordt niet meer vermeld:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a>Koppelingen beheren
U kunt een NSG toosubnets en NIC's kunt koppelen. U kunt ook een NSG van elke bron die deze gekoppeld ontkoppelen.

### <a name="associate-an-nsg-tooa-nic"></a>Een NSG tooa NIC koppelen
Hallo tooassociate **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, volledige Hallo stappen te volgen:

1. Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hallo na de opdracht tooretrieve Hallo bestaande NIC uitvoeren en op te slaan in een variabele:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. Set Hallo **NetworkSecurityGroup** eigenschap Hallo **NIC** waarde van variabele toohello Hallo **NSG** variabele, door te voeren Hallo volgende opdracht:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. toosave hello wijzigingen aangebracht toohello NIC, Hallo volgende opdracht uitvoeren:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Verwachte uitvoer waarin alleen Hallo **NetworkSecurityGroup** eigenschap:
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>Een NSG van een NIC ontkoppelen
Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **TestNICWeb1** NIC, volledige Hallo stappen te volgen:

1. Hallo na de opdracht tooretrieve Hallo bestaande NIC uitvoeren en op te slaan in een variabele:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. Set Hallo **NetworkSecurityGroup** eigenschap Hallo **NIC** variabele te**$null** door het uitvoeren van de volgende opdracht Hallo:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. toosave hello wijzigingen aangebracht toohello NIC, Hallo volgende opdracht uitvoeren:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Verwachte uitvoer waarin alleen Hallo **NetworkSecurityGroup** eigenschap:
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>Een NSG van een subnet ontkoppelen
Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **FrontEnd** subnet, volledige Hallo stappen te volgen:

1. Voer Hallo opdracht tooretrieve Hallo bestaande VNet te volgen en opslaan in een variabele:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Voer hello na de opdracht tooretrieve hello **FrontEnd** subnet en op te slaan in een variabele:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Set Hallo **NetworkSecurityGroup** eigenschap Hallo **subnet** variabele te**$null** hiertoe Hallo volgende opdracht:

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. toosave hello wijzigingen aangebracht toohello subnet, Hallo volgende opdracht uitvoeren:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Verwachte uitvoer met alleen Hallo eigenschappen van Hallo **FrontEnd** subnet. U ziet dat er zich geen eigenschap voor **NetworkSecurityGroup**:
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a>Een NSG tooa subnet koppelen
Hallo tooassociate **NSG-FrontEnd** NSG toohello **FronEnd** opnieuw subnet, volledige Hallo stappen te volgen:

1. Voer Hallo opdracht tooretrieve Hallo bestaande VNet te volgen en opslaan in een variabele:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Voer hello na de opdracht tooretrieve hello **FrontEnd** subnet en op te slaan in een variabele:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. Set Hallo **NetworkSecurityGroup** eigenschap Hallo **subnet** variabele te**$null** door het uitvoeren van de volgende opdracht Hallo:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. toosave hello wijzigingen aangebracht toohello subnet, Hallo volgende opdracht uitvoeren:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Verwachte uitvoer waarin alleen Hallo **NetworkSecurityGroup** eigenschap Hallo **FrontEnd** subnet:
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>Een NSG verwijderen
U kunt een NSG alleen verwijderen als het tooany resource niet is gekoppeld. een NSG toodelete Hallo volgende stappen.

1. toocheck hello resources die zijn gekoppeld tooan NSG, Voer Hallo `azure network nsg show` zoals in [weergave nsg's koppelingen](#View-NSGs-associations).
2. Als Hallo NSG gekoppeld tooany NIC's is, voert u Hallo `azure network nic set` zoals in [ontkoppelen van een NSG van een NIC](#Dissociate-an-NSG-from-a-NIC) voor elke NIC. 
3. Als Hallo NSG gekoppeld tooany subnet is, voert u Hallo `azure network vnet subnet set` zoals in [een NSG van een subnet ontkoppelen](#Dissociate-an-NSG-from-a-subnet) voor elk subnet.
4. toodelete hello NSG, Hallo volgende opdracht uitvoeren:

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > Hallo `-Force` parameter zorgt ervoor dat u hoeft niet tooconfirm Hallo verwijderen.
   > 

## <a name="next-steps"></a>Volgende stappen
* [Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.

