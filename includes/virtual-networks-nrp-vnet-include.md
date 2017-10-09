## <a name="virtual-network"></a>Virtual Network
Virtuele netwerken (VNET) en subnetten bronnen het definiëren van een beveiligingsgrens voor werkbelastingen in Azure. Een VNet wordt gekenmerkt door een verzameling van adresruimten, gedefinieerd als CIDR-blokken. 

> [!NOTE]
> Netwerkbeheerders bent bekend met CIDR-notatie. Als u niet bekend met CIDR bent, [meer informatie over het](http://whatismyipaddress.com/cidr).
> 
> 

![VNet met meerdere subnetten](./media/resource-groups-networking/Figure4.png)

VNets bevatten hello volgende eigenschappen.

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **de addressSpace** |Verzameling van adresvoorvoegsels die gezamenlijk Hallo VNet in CIDR-notatie |192.168.0.0/16 |
| **subnetten** |Verzameling van subnetten die gezamenlijk Hallo VNet |Zie [subnetten](#Subnets) hieronder. |
| **IP-adres** |IP-adres toegewezen tooobject. Dit is een alleen-lezen eigenschap. |104.42.233.77 |

### <a name="subnets"></a>Subnetten
Een subnet is een onderliggende resource van een VNet en helpt bij het segmenten van adresruimten binnen een CIDR-blok met behulp van IP-adresvoorvoegsels definiëren. NIC's kunnen worden toegevoegd, toosubnets en verbonden tooVMs, tegelijk connectiviteit biedt voor verschillende werkbelastingen.

Subnetten bevatten Hallo volgende eigenschappen. 

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **addressPrefix** |Één adresvoorvoegsel die Hallo subnet in CIDR-notatie |192.168.1.0/24 |
| **networkSecurityGroup** |NSG die is toegepast toohello subnet |Zie [nsg's](#Network-Security-Group) |
| **Migratiestatus** |Routetabel toegepast toohello subnet |Zie [UDR](#Route-table) |
| **ipConfigurations** |Verzameling van IP-configruation objecten die worden gebruikt door de NIC's aangesloten toohello subnet |Zie [UDR](#Route-table) |

Voorbeeld VNet in JSON-indeling:

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a>Aanvullende bronnen
* Vindt u meer informatie over [VNet](../articles/virtual-network/virtual-networks-overview.md).
* Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163650.aspx) voor VNets.
* Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163618.aspx) voor subnetten.

