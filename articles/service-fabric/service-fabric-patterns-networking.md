---
title: aaaNetworking patronen voor Azure Service Fabric | Microsoft Docs
description: Beschrijving van algemene patronen voor netwerken voor Service Fabric en hoe toocreate een cluster met behulp van Azure-netwerkfuncties.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Service Fabric netwerken patronen
U kunt uw Azure Service Fabric-cluster integreren met andere Azure-netwerkfuncties. In dit artikel zien we u hoe toocreate clusters die gebruik Hallo volgende kenmerken:

- [Bestaand virtueel netwerk of subnet](#existingvnet)
- [Statische openbare IP-adres](#staticpublicip)
- [Alleen voor interne load balancer](#internallb)
- [Interne en externe load balancer](#internalexternallb)

Service Fabric wordt uitgevoerd in een standaard virtuele-machineschaalset. Functionaliteit die u in een virtuele-machineschaalset gebruiken kunt, kunt u met een Service Fabric-cluster. Hallo netwerken secties met hello Azure Resource Manager-sjablonen voor virtuele-machineschaalsets en Service Fabric zijn identiek. Nadat u tooan bestaande virtuele netwerk implementeert, is het eenvoudig tooincorporate andere netwerkfuncties, zoals Azure ExpressRoute, Azure VPN-Gateway, een netwerkbeveiligingsgroep en virtueel netwerk peering.

Service Fabric is uniek in vergelijking met andere netwerkfuncties in één aspect. Hallo [Azure-portal](https://portal.azure.com) intern gebruikt Hallo Service Fabric resource provider toocall tooa cluster tooget informatie over de knooppunten en toepassingen. Hallo Service Fabric-resourceprovider vereist openbaar toegankelijk binnenkomende toegang toohello HTTP gateway poort (standaard poort 19080,) op Hallo management eindpunt. [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) gebruikt Hallo management eindpunt toomanage uw cluster. Hallo Service Fabric-resourceprovider gebruikt ook deze poort tooquery informatie over uw cluster, toodisplay in hello Azure-portal. 

Als poort 19080 is niet toegankelijk is vanaf Hallo Service Fabric-resourceprovider, een bericht zoals *knooppunten is niet gevonden* wordt weergegeven in de portal hello, en de lijst met knooppunt en de toepassing is leeg. Als u wilt dat toosee uw cluster in hello Azure-portal, de load balancer moet een openbaar IP-adres beschikbaar en uw netwerkbeveiligingsgroep moet de binnenkomende 19080-poortverkeer toestaan. Als uw installatie voldoet niet aan deze vereisten, weergegeven hello Azure-portal Hallo status van het cluster niet.

## <a name="templates"></a>Sjablonen

Alle Service Fabric-sjablonen zijn in [één gedownloade bestand](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip). U moet kunnen toodeploy Hallo sjablonen als-is via Hallo PowerShell-opdrachten te volgen. Als u implementeert Hallo bestaande Azure Virtual Network-sjabloon of Hallo statische openbare IP-sjabloon Hallo eerst lezen [initiële setup](#initialsetup) sectie van dit artikel.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>Eerste installatie

### <a name="existing-virtual-network"></a>Bestaand virtueel netwerk

In de Hallo voorbeeld te volgen, we beginnen met een bestaand virtueel netwerk met de naam ExistingRG-vnet in Hallo **ExistingRG** resourcegroep. naam van het Hallo-subnet is standaard. Deze standaardresources worden gemaakt wanneer u hello Azure portal toocreate een standaard virtuele machine (VM) gebruiken. U kan Hallo virtueel netwerk en subnet maken zonder Hallo VM maken, maar Hallo belangrijkste doel van het toevoegen van een cluster tooan bestaand virtueel netwerk is tooprovide network connectivity tooother virtuele machines. Maken Hallo VM biedt een goed voorbeeld van hoe een bestaand virtueel netwerk wordt meestal gebruikt. Als uw Service Fabric-cluster maakt gebruik van alleen een interne load balancer, zonder een openbaar IP-adres, kunt u virtuele machine en de openbare IP-adres als een veilige Hallo *springen vak*.

### <a name="static-public-ip-address"></a>Statische openbare IP-adres

Een statische openbare IP-adres is doorgaans een speciale resource die wordt afzonderlijk beheerd vanaf Hallo VM of deze toegewezen aan virtuele machines. Het ingericht in een specifieke netwerken resourcegroep (als tegengestelde tooin Hallo Service Fabric-clusterresourcegroep zelf). Maak een statische openbare IP-adres met de naam staticIP1 in Hallo dezelfde ExistingRG resourcegroep, in hello Azure-portal of met behulp van PowerShell:

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Service Fabric-sjabloon

In het Hallo-voorbeelden in dit artikel gebruiken we Hallo Service Fabric template.json. Voordat u een cluster maakt, kunt u Hallo portal wizard standaard toodownload Hallo sjabloon van Hallo-portal gebruiken. Ook kunt u een van de sjablonen Hallo in Hallo [sjablonengalerie](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), zoals Hallo [vijf knooppunten Service Fabric-cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>Bestaand virtueel netwerk of subnet

1. Hallo subnet parameter toohello naam van de bestaande subnet Hallo wijzigen en voeg vervolgens twee nieuwe parameters tooreference Hallo bestaand virtueel netwerk:

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. Wijziging Hallo `vnetID` variabele toopoint toohello bestaand virtueel netwerk:

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Verwijder `Microsoft.Network/virtualNetworks` van uw resources zo Azure geen maakt een nieuw virtueel netwerk:

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Commentaar Hallo virtueel netwerk uit Hallo `dependsOn` kenmerk van `Microsoft.Compute/virtualMachineScaleSets`, zodat u niet afhankelijk zijn van een nieuw virtueel netwerk maken:

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Hallo-sjabloon implementeren:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    Na de implementatie, het virtuele netwerk moet zijn opgenomen Hallo nieuwe schaal ingesteld virtuele machines. Hallo virtuele machine scale set-knooppunttype moet Hallo bestaand virtueel netwerk en subnetmasker worden weergegeven. Ook kunt u Remote Desktop Protocol (RDP) tooaccess Hallo VM die was al niet in het virtuele netwerk Hallo en tooping Hallo nieuwe schaal ingesteld virtuele machines:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

Zie voor een ander voorbeeld [een die niet specifiek tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>Statische openbare IP-adres

1. Voeg parameters voor de naam van de Hallo Hallo bestaande statische IP-resourcegroep, naam en volledig gekwalificeerde domeinnaam (FQDN):

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Hallo verwijderen `dnsName` parameter. (Hallo statisch IP-adres heeft al een.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. Een variabele tooreference Hallo bestaande statische IP-adres toevoegen:

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Verwijder `Microsoft.Network/publicIPAddresses` van uw resources zo Azure geen maakt een nieuw IP-adres:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Commentaar Hallo IP-adres uit Hallo `dependsOn` kenmerk van `Microsoft.Network/loadBalancers`, zodat u niet afhankelijk zijn van het maken van een nieuw IP-adres:

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. In Hallo `Microsoft.Network/loadBalancers` resource, wijziging Hallo `publicIPAddress` element van `frontendIPConfigurations` tooreference Hallo bestaande statisch IP-adres in plaats van een nieuwe:

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. In Hallo `Microsoft.ServiceFabric/clusters` resource wijzigen `managementEndpoint` toohello DNS FQDN Hallo statische IP-adres. Als u een beveiligde cluster gebruikt, controleert u of u kunt wijzigen *http://* te*https://*. (Houd er rekening mee dat deze stap alleen tooService Fabric-clusters geldt. Als u van een virtuele-machineschaalset gebruikmaakt, deze stap overslaan.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Hallo-sjabloon implementeren:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

Na de implementatie kunt u zien dat de load balancer gebonden toohello openbare statische IP-adres uit Hallo is andere resourcegroep. Hallo verbindingseindpunt Service Fabric-client en [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) eindpunt punt toohello DNS FQDN Hallo statische IP-adres.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>Alleen voor interne load balancer

Dit scenario vervangen Hallo externe load balancer in de Service Fabric standaardsjabloon Hallo door een interne load balancer. Zie Hallo voorgaande sectie voor gevolgen voor hello Azure-portal en Hallo Service Fabric-resourceprovider.

1. Hallo verwijderen `dnsName` parameter. (Dit niet nodig.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. Als u een statische toewijzingsmethode gebruikt, kunt u eventueel een parameter statische IP-adres toevoegen. Als u een dynamische toewijzingsmethode gebruikt, hoeft u niet toodo deze stap.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Verwijder `Microsoft.Network/publicIPAddresses` van uw resources zo Azure geen maakt een nieuw IP-adres:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Verwijder Hallo IP-adres `dependsOn` kenmerk van `Microsoft.Network/loadBalancers`, zodat u niet afhankelijk zijn van het maken van een nieuw IP-adres. Toevoegen van het virtuele netwerk Hallo `dependsOn` omdat Hallo subnet van het virtuele netwerk Hallo Hallo load balancer nu afhankelijk van het kenmerk:

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Hallo load balancer wijzigen `frontendIPConfigurations` instellen uit met behulp van een `publicIPAddress`, toousing een subnet en `privateIPAddress`. `privateIPAddress`een vooraf gedefinieerde statische interne IP-adres gebruikt. toouse een dynamisch IP-adres verwijderen Hallo `privateIPAddress` element en wijzig vervolgens `privateIPAllocationMethod` te**dynamische**.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. In Hallo `Microsoft.ServiceFabric/clusters` resource wijzigen `managementEndpoint` toopoint toohello interne load balancer-adres. Als u een beveiligde cluster gebruikt, controleert u of u kunt wijzigen *http://* te*https://*. (Houd er rekening mee dat deze stap alleen tooService Fabric-clusters geldt. Als u van een virtuele-machineschaalset gebruikmaakt, deze stap overslaan.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Hallo-sjabloon implementeren:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

Na de implementatie maakt gebruik van de load balancer Hallo persoonlijke 10.0.0.250 van statische IP-adres. Als u een andere computer die hetzelfde virtuele netwerk hebt, kunt u gaan toohello interne [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) eindpunt. Houd er rekening mee dat deze verbinding tooone Hallo knooppunten achter Hallo load balancer maakt.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>Interne en externe load balancer

In dit scenario u beginnen met Hallo bestaande één knooppunt type externe load balancer en toevoegen van een interne load balancer voor Hallo dezelfde knooppunttype. Een back-end-poort gekoppeld tooa back-end-adresgroep kan alleen tooa één load balancer worden toegewezen. Kies welke load balancer wordt de poorten van uw toepassing, en welke load balancer heeft uw eindpunten voor beheer (poorten 19000 en 19080). Als u Hallo-eindpunten voor beheer op Hallo interne load balancer plaatst, houd rekening Hallo Service Fabric-resource provider-beperkingen die eerder in Hallo artikel besproken. In Hallo voorbeeld we gebruiken blijven Hallo-eindpunten voor beheer op Hallo externe load balancer. U ook een poort 80 toepassing poort toevoegen en plaats het op Hallo interne load balancer.

In een cluster met twee knooppunttype is één knooppunttype op Hallo externe load balancer. Hallo is andere knooppunttype op Hallo interne load balancer. een cluster twee knooppunttype in Hallo portal gemaakt twee knooppunttype sjabloon (die wordt geleverd met twee netwerktaakverdelers) toouse overschakelen Hallo tweede load balancer tooan interne load balancer. Zie voor meer informatie, Hallo [alleen interne load balancer](#internallb) sectie.

1. Parameter van IP-adres van Hallo statische interne load balancer toevoegen. (Zie de vorige secties van dit artikel voor opmerkingen bij de gerelateerde toousing een dynamisch IP-adres,.)

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. Een parameter van de poort 80 toepassing toevoegen.

3. interne versies van bestaande Hallo tooadd networking variabelen, kopiëren en plakken en toevoegen '-Int ' toohello naam:

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. Als u met Hallo portal gegenereerde sjabloon die gebruikmaakt van toepassing poort 80 begint, portal standaardsjabloon Hallo AppPort1 toegevoegd (poort 80) op Hallo externe load balancer. In dit geval AppPort1 verwijderen uit Hallo externe load balancer `loadBalancingRules` en tests, zodat u toohello interne load balancer kunt toevoegen:

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. Toevoegen van een tweede `Microsoft.Network/loadBalancers` resource. Het lijkt erop vergelijkbare toohello interne load balancer gemaakt in Hallo [alleen interne load balancer](#internallb) sectie, maar gebruikt u Hallo '-Int "load balancer-variabelen en implementeert alleen Hallo toepassing poort 80. Hiermee worden `inboundNatPools`, tookeep RDP-eindpunten op Hallo openbare load balancer. Desgewenst kunt u RDP op Hallo interne load balancer verplaatsen `inboundNatPools` van Hallo externe load balancer toothis interne de load balancer:

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. In `networkProfile` voor Hallo `Microsoft.Compute/virtualMachineScaleSets` resource, Hallo interne back-end-adresgroep toevoegen:

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Hallo-sjabloon implementeren:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

Na de implementatie ziet u twee load balancers in de resourcegroep Hallo. Als u de netwerktaakverdelers Hallo bladert, ziet u Hallo openbaar IP-adres en management eindpunten (poorten 19000 en 19080) toegewezen toohello openbaar IP-adres. Ook ziet u Hallo statische interne IP-adres en de toepassing eindpunt (poort 80) toegewezen toohello interne load balancer. Beide load balancers gebruik hello dezelfde virtuele-machineschaalset back-end-pool.

## <a name="next-steps"></a>Volgende stappen
[Een cluster maken](service-fabric-cluster-creation-via-arm.md)
