## <a name="route-tables"></a>Routetabellen
Route tabel resources bevat routes gebruikt toodefine hoe verkeersstromen binnen uw Azure-infrastructuur. U kunt door de gebruiker gedefinieerde routes (UDR) toosend al het verkeer van een bepaald subnet tooa virtueel apparaat, zoals een firewall of inbraakdetectie detectie-systeem (id's) gebruiken. U kunt een route tabel toosubnets koppelen. 

Routetabellen bevatten Hallo volgende eigenschappen.

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **routes** |Verzameling van de gebruiker gedefinieerde routes in de routetabel Hallo |Zie [door de gebruiker gedefinieerde routes](#User-defined-routes) |
| **subnetten** |Verzameling van subnetten Hallo routetabel wordt te toegepast|Zie [subnetten](#Subnets) |

### <a name="user-defined-routes"></a>De gebruiker gedefinieerde routes
U kunt udr's toospecify waar verkeer moet worden gezonden, maken op basis van het doeladres. U kunt een route beschouwen als Hallo standaard gateway-definitie op basis van het doeladres Hallo van een netwerkpakket.

Udr's bevatten de volgende eigenschappen Hallo. 

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **addressPrefix** |Adresvoorvoegsel of volledige IP-adres voor de bestemming Hallo |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |Type apparaat Hallo verkeer worden te verzonden|Internet VirtualAppliance, VPN-Gateway |
| **nextHopIpAddress** |IP-adres voor de volgende hop Hallo |192.168.1.4 |

Voorbeeld routetabel in JSON-indeling:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Aanvullende bronnen
* Vindt u meer informatie over [udr's](../articles/virtual-network/virtual-networks-udr-overview.md).
* Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt502549.aspx) voor routetabellen.
* Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt502539.aspx) voor de gebruiker gedefinieerde routes (udr's).

