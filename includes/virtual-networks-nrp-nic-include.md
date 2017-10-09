## <a name="nic"></a>NIC
Een network interface (netwerkinterfacekaart)-bron biedt connectiviteit tooan bestaande netwerksubnet in een VNet-resource. Hoewel u een NIC als zelfstandige object maken kunt, moet u tooassociate deze tooanother object tooactually connectiviteit bieden. Een NIC kan worden gebruikt tooconnect tooa VM-subnet, een openbare IP-adres of een load balancer.  

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **virtuele machine** |VM Hallo NIC is gekoppeld. |/Subscriptions/{GUID}/../Microsoft.COMPUTE/virtualMachines/vm1 |
| **MAC-adres** |MAC-adres voor Hallo NIC |een waarde tussen 4 en 30 in |
| **networkSecurityGroup** |NSG die is gekoppeld toohello NIC |/Subscriptions/{GUID}/../Microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |DNS-instellingen voor Hallo NIC |Zie [PIP](#Public-IP-address) |

Een Network Interface Card of NIC, vertegenwoordigt een netwerkinterface die gekoppeld tooa virtuele machine (VM worden kan). Een virtuele machine kan een of meer NIC's hebben.

![NIC's op een enkele virtuele machine](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>IP-configuraties
NIC's hebben een onderliggend object met de naam **ipConfigurations** met Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **subnet** |Subnet Hallo NIC is onnected aan. |/Subscriptions/{GUID}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1 |
| **privateIPAddress** |IP-adres voor Hallo NIC in Hallo subnet |10.0.0.8 |
| **privateIPAllocationMethod** |IP-toewijzingsmethode |Dynamische of statische |
| **enableIPForwarding** |Hiermee wordt aangegeven of Hallo NIC kan worden gebruikt voor routering |waar of ONWAAR |
| **primaire** |Of NIC Hallo Hallo primaire NIC voor Hallo VM |waar of ONWAAR |
| **publicIPAddress** |PIP Hallo NIC gekoppeld |Zie [DNS-instellingen](#DNS-settings) |
| **loadbalancerbackendaddresspools gebruikt** |Back-end adres pools Hallo die NIC is gekoppeld aan | |
| **loadBalancerInboundNatRules** |Inkomende load balancer NAT-regels Hallo die NIC is gekoppeld aan | |

Voorbeeld openbare IP-adres in JSON-indeling:

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>Aanvullende bronnen
* Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163579.aspx) voor NIC's.

