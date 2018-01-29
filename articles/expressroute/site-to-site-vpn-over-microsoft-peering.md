---
title: Een site-naar-site-VPN configureren via Microsoft-peering voor Azure ExpressRoute | Microsoft Docs
description: IPsec/IKE-connectiviteit naar Azure via een peering Microsoft ExpressRoute-circuit met behulp van een site-naar-site VPN-gateway configureren.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2017
ms.author: cherylmc
ms.openlocfilehash: 64203e2cbac1206224f0e0ad8b7d364f19ad0332
ms.sourcegitcommit: 4ac89872f4c86c612a71eb7ec30b755e7df89722
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/07/2017
---
# <a name="configure-a-site-to-site-vpn-over-expressroute-microsoft-peering"></a>Een site-naar-site-VPN configureren via ExpressRoute-Microsoft-peering

In dit artikel helpt u beveiligde versleutelde verbindingen tussen uw on-premises netwerk en uw virtuele netwerken van Azure (vnet's) via een persoonlijke ExpressRoute-verbinding configureren. Configureren van een beveiligde tunnel via ExpressRoute kunnen gegevens uitwisselen met vertrouwelijkheid, antivirusprogramma replay echtheid en integriteit.

## <a name="architecture"></a>Architectuur

U kunt gebruikmaken van Microsoft-peering voor het opzetten van een site-naar-site VPN-IPsec/IKE-tunnel tussen de geselecteerde on-premises netwerken en Azure VNets.

  ![overzicht van de verbinding](./media/site-to-site-vpn-over-microsoft-peering/IPsecER_Overview.png)

>[!NOTE]
>Bij het instellen van site-naar-site VPN via Microsoft-peering, wordt u in rekening gebracht voor de VPN-gateway en de VPN-uitgaande. Zie voor meer informatie [prijzen voor VPN-Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway).
>
>

Voor hoge beschikbaarheid en redundantie, kunt u meerdere tunnels via de twee MSEE-PE-paar van een ExpressRoute-circuit configureren en inschakelen van taakverdeling tussen de tunnels.

  ![Opties voor hoge beschikbaarheid](./media/site-to-site-vpn-over-microsoft-peering/HighAvailability.png)

VPN-tunnels via het Microsoft-peering kunnen worden beëindigd met behulp van VPN-gateway of met behulp van een juiste netwerk virtuele toestel (NVA) beschikbaar is via Azure Marketplace. U kunt routes uitwisselen statisch of dynamisch via de tunnels versleutelde zonder dat de uitwisseling van de route naar de onderliggende Microsoft-peering. In de voorbeelden in dit artikel wordt BGP (anders dan de BGP-sessie die is gebruikt voor het maken van de Microsoft-peering) gebruikt voor het uitwisselen van voorvoegsels dynamisch via de versleutelde tunnels.

>[!IMPORTANT]
>Doorgaans voor het oppervlak lokale Microsoft-peering wordt beëindigd op het Perimeternetwerk en persoonlijke peering wordt beëindigd op de core network-zone. De twee zones zouden worden gescheiden met firewalls. Als u Microsoft-peering uitsluitend bedoeld is voor het inschakelen van beveiligde tunneling via ExpressRoute configureert, moet u voor het filteren van alleen het openbare IP-adressen die zijn opgehaald geadverteerd via Microsoft-peering.
>
>

## <a name="workflow"></a>Werkstroom

1. Configureer Microsoft-peering voor uw ExpressRoute-circuit.
2. Geselecteerde Azure regionale openbare voorvoegsels voor uw on-premises netwerk via het Microsoft-peering wordt geadverteerd.
3. Een VPN-gateway configureren en IPsec-tunnels tot stand brengen
4. Configureer de on-premises VPN-apparaat.
5. De site-naar-site IPsec/IKE-verbinding maken.
6. (Optioneel) Configureren van firewalls/filteren op de on-premises VPN-apparaat.
7. Testen en valideren van de IPsec-communicatie via de ExpressRoute-circuit.

## <a name="peering"></a>1. Configureer Microsoft-peering

Als u wilt configureren met een site-naar-site VPN-verbinding via ExpressRoute, moet u gebruikmaken van Microsoft voor ExpressRoute-peering.

* Start voor het configureren van nieuwe ExpressRoute-circuit met de [vereisten voor ExpressRoute](expressroute-prerequisites.md) artikel, en vervolgens [maken en een ExpressRoute-circuit wijzigen](expressroute-howto-circuit-arm.md).

* Als u al een ExpressRoute-circuit hebben, maar hebben geen Microsoft-peering geconfigureerd, configureert u Microsoft-peering met behulp van de [maken en wijzigen van de peering voor een ExpressRoute-circuit](expressroute-howto-routing-arm.md#msft) artikel.

Als u uw circuit en de Microsoft-peering hebt geconfigureerd, kunt u eenvoudig bekijken met behulp van de **overzicht** pagina in de Azure-portal.

![circuit](./media/site-to-site-vpn-over-microsoft-peering/ExpressRouteCkt.png)

## <a name="routefilter"></a>2. Routefilters configureren

Een routefilter kunt u identificeren services die u gebruiken wilt via Microsoft-peering voor uw ExpressRoute-circuit. Het is in wezen een whitelist van alle waarden van de BGP-community. 

![routefilter](./media/site-to-site-vpn-over-microsoft-peering/route-filter.png)

In dit voorbeeld wordt de implementatie is alleen in de *Azure West ons 2* regio. Een filterregel route wordt toegevoegd aan het toestaan van alleen de aankondiging van regionale voorvoegsels in de Azure West ons 2, met de BGP-communitywaarde *12076:51026*. Geef van de regionale voorvoegsels die u toestaan dat wilt door het selecteren van **beheren regel**.

In het routefilter moet u ook kiest u de ExpressRoute-circuits waarvoor het routefilter van toepassing is. U kunt de ExpressRoute-circuits kiezen door het selecteren van **circuit toevoegen**. Het routefilter is in de vorige afbeelding is gekoppeld aan het voorbeeld ExpressRoute-circuit.

### <a name="configfilter"></a>2.1 routefilter instellen

Configureer een routefilter. Zie voor stappen [routefilters configureren voor Microsoft-peering](how-to-routefilter-portal.md).

### <a name="verifybgp"></a>2.2 controleren BGP-routes

Zodra u hebt gemaakt van Microsoft-peering via uw ExpressRoute-circuit en die een routefilter is gekoppeld aan het circuit, kunt u de BGP-routes ontvangen van msee's op de PE-apparaten die zijn peering met de msee's kunt controleren. De opdracht controle varieert, afhankelijk van het besturingssysteem van uw apparaten PE.

#### <a name="cisco-examples"></a>Cisco-voorbeelden

In dit voorbeeld wordt een Cisco IOS-XE-opdracht. In het voorbeeld wordt wordt een virtuele Routering en doorsturen (VRF)-exemplaar gebruikt om de peering verkeer te isoleren.

```
show ip bgp vpnv4 vrf 10 summary
```

De volgende gedeeltelijke uitvoer laat zien dat 68 voorvoegsels zijn ontvangen van de neighbor *.243.229.34 met de ASN 12076 (MSEE):

```
...

Neighbor        V           AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
X.243.229.34    4        12076   17671   17650    25228    0    0 1w4d           68
```

Als de lijst met voorvoegsels ontvangen van de neighbor weergeven, gebruikt u het volgende voorbeeld:

```
sh ip bgp vpnv4 vrf 10 neighbors X.243.229.34 received-routes
```

Om te bevestigen dat u de juiste set voorvoegsels ontvangt, kunt u cross-controleren. De uitvoer van de volgende Azure PowerShell-opdracht worden de voorvoegsels die worden geadverteerd via Microsoft-peering voor elk van de services en voor elk van de Azure-regio:

```powershell
Get-AzureRmBgpServiceCommunity
```

## <a name="vpngateway"></a>3. Configureer de VPN-gateway en IPsec-tunnels

In deze sectie worden IPsec VPN-tunnels gemaakt tussen de Azure VPN-gateway en de on-premises VPN-apparaat. De voorbeelden gebruikt Cisco Cloud Service-Router (CSR1000) VPN-apparaten.

Het volgende diagram toont de IPsec VPN-tunnels tot stand gebracht tussen de on-premises VPN-apparaat 1 en het paar Azure VPN-gateway-exemplaar. De twee IPsec VPN-tunnels tot stand gebracht tussen de on-premises VPN-apparaat 2 en de combinatie van Azure VPN-gateway-exemplaar wordt niet weergegeven in het diagram en de configuratiegegevens niet worden weergegeven. Met extra VPN-tunnels verbetert echter hoge beschikbaarheid.

  ![VPN-tunnels](./media/site-to-site-vpn-over-microsoft-peering/EstablishTunnels.png)

Via het paar IPsec-tunnel een eBGP-sessie tot stand is gebracht voor het uitwisselen van routes particuliere netwerk. Het volgende diagram toont de eBGP-sessie tot stand gebracht via het IPSec-tunnel paar:

  ![via de tunnel paar eBGP-sessies](./media/site-to-site-vpn-over-microsoft-peering/TunnelBGP.png)

Het volgende diagram toont het kort overzicht van de voorbeeld-netwerk:

  ![voorbeeld-netwerk](./media/site-to-site-vpn-over-microsoft-peering/OverviewRef.png)

### <a name="about-the-azure-resource-manager-template-examples"></a>Over de Azure Resource Manager-sjabloon-voorbeelden

In de voorbeelden de VPN-gateway en de IPSec-tunnel afsluitingen worden geconfigureerd met een Azure Resource Manager-sjabloon. Als u niet bekend bent met Resource Manager-sjablonen of om de basisbeginselen Resource Manager-sjabloon te leren Zie [inzicht in de structuur en de syntaxis van Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md). De sjabloon in deze sectie maakt u een greenfield Azure-omgeving (VNet). Echter, als u een bestaande VNet hebt, u kunt verwijzen naar deze in de sjabloon. Als u niet bekend met IPsec/IKE-site-naar-site configuraties voor VPN-gateway bent, Zie [maken van een site-naar-site-verbinding](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).

>[!NOTE]
>U hoeft niet te gebruiken van Azure Resource Manager-sjablonen om te kunnen maken van deze configuratie. U kunt deze configuratie met de Azure-portal of PowerShell maken.
>
>

### <a name="variables3"></a>3.1 de variabelen declareren

In dit voorbeeld is de variabelendeclaraties komen overeen met het netwerk voorbeeld. Wanneer de variabelen declareren, wijzigen in deze sectie om uw omgeving weer te geven.

* De variabele **localAddressPrefix** is een matrix met lokale IP-adressen worden beëindigd of dat de IPsec-tunnels.
* De **gatewaySku** bepaalt de VPN-doorvoer. Zie voor meer informatie over gatewaySku en vpnType [configuratie-instellingen voor VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). Zie voor prijzen [prijzen voor VPN-Gateway](https://azure.microsoft.com/pricing/details/vpn-gateway).
* Stel de **vpnType** naar **RouteBased**.

```json
"variables": {
  "virtualNetworkName": "SecureVNet",       // Name of the Azure VNet
  "azureVNetAddressPrefix": "10.2.0.0/24",  // Address space assigned to the VNet
  "subnetName": "Tenant",                   // subnet name in which tenants exists
  "subnetPrefix": "10.2.0.0/25",            // address space of the tenant subnet
  "gatewaySubnetPrefix": "10.2.0.224/27",   // address space of the gateway subnet
  "localGatewayName": "localGW1",           // name of remote gateway (on-premises)
  "localGatewayIpAddress": "X.243.229.110", // public IP address of the on-premises VPN device
  "localAddressPrefix": [
    "172.16.0.1/32",                        // termination of IPsec tunnel-1 on-premises 
    "172.16.0.2/32"                         // termination of IPsec tunnel-2 on-premises 
  ],
  "gatewayPublicIPName1": "vpnGwVIP1",    // Public address name of the first VPN gateway instance
  "gatewayPublicIPName2": "vpnGwVIP2",    // Public address name of the second VPN gateway instance 
  "gatewayName": "vpnGw",                 // Name of the Azure VPN gateway
  "gatewaySku": "VpnGw1",                 // Azure VPN gateway SKU
  "vpnType": "RouteBased",                // type of VPN gateway
  "sharedKey": "string",                  // shared secret needs to match with on-premise configuration
  "asnVpnGateway": 65000,                 // BGP Autonomous System number assigned to the VPN Gateway 
  "asnRemote": 65010,                     // BGP Autonmous Syste number assigned to the on-premises device
  "bgpPeeringAddress": "172.16.0.3",      // IP address of the remote BGP peer on-premises
  "connectionName": "vpn2local1",
  "vnetID": "[resourceId('Microsoft.Network/virtualNetworks', variables('virtualNetworkName'))]",
  "gatewaySubnetRef": "[concat(variables('vnetID'),'/subnets/','GatewaySubnet')]",
  "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
  "api-version": "2017-06-01"
},
```

### <a name="vnet"></a>3.2 virtueel netwerk (VNet) maken

Als u een bestaande VNet aan de VPN-tunnels koppelt, kunt u deze stap overslaan.

```json
{
  "apiVersion": "[variables('api-version')]",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "[variables('azureVNetAddressPrefix')]"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "[variables('subnetPrefix')]"
        }
      },
      {
        "name": "GatewaySubnet",
        "properties": {
          "addressPrefix": "[variables('gatewaySubnetPrefix')]"
        }
      }
    ]
  },
  "comments": "Create a Virtual Network with Subnet1 and Gatewaysubnet"
},
```

### <a name="ip"></a>3.3 openbare IP-adressen toewijzen aan VPN-gateway-exemplaren
 
Toewijzen van een openbaar IP-adres voor elk exemplaar van een VPN-gateway.

```json
{
  "apiVersion": "[variables('api-version')]",
  "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('gatewayPublicIPName1')]",
    "location": "[resourceGroup().location]",
    "properties": {
      "publicIPAllocationMethod": "Dynamic"
    },
    "comments": "Public IP for the first instance of the VPN gateway"
  },
  {
    "apiVersion": "[variables('api-version')]",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('gatewayPublicIPName2')]",
    "location": "[resourceGroup().location]",
    "properties": {
      "publicIPAllocationMethod": "Dynamic"
    },
    "comments": "Public IP for the second instance of the VPN gateway"
  },
```

### <a name="termination"></a>3.4 Geef het lokale VPN-tunnel beëindiging (lokale netwerkgateway)

De on-premises VPN-apparaten worden aangeduid als de **lokale netwerkgateway**. De volgende json-fragment bevat ook externe BGP-peer-details:

```json
{
  "apiVersion": "[variables('api-version')]",
  "type": "Microsoft.Network/localNetworkGateways",
  "name": "[variables('localGatewayName')]",
  "location": "[resourceGroup().location]",
  "properties": {
    "localNetworkAddressSpace": {
      "addressPrefixes": "[variables('localAddressPrefix')]"
    },
    "gatewayIpAddress": "[variables('localGatewayIpAddress')]",
    "bgpSettings": {
      "asn": "[variables('asnRemote')]",
      "bgpPeeringAddress": "[variables('bgpPeeringAddress')]",
      "peerWeight": 0
    }
  },
  "comments": "Local Network Gateway (referred to your on-premises location) with IP address of remote tunnel peering and IP address of remote BGP peer"
},
```

### <a name="creategw"></a>3.5 de VPN-gateway maken

Deze sectie van de sjabloon configureert de VPN-gateway met de vereiste instellingen voor een actief / actief-configuratie. Houd rekening met de volgende vereisten:

* Maken van de VPN-gateway met een **'RouteBased'** VpnType. Deze instelling is verplicht als u wilt inschakelen op de BGP-routering tussen de VPN-gateway en de VPN-on-premises.
* Tot stand brengen van VPN-tunnels tussen de twee exemplaren van de VPN-gateway en een bepaalde on-premises-apparaat in de actieve-actieve modus, de **'activeActive'** parameter is ingesteld op **true** in de Resource Manager-sjabloon . Zie voor meer informatie over de maximaal beschikbare VPN-gateways, [maximaal beschikbare VPN-gatewayverbinding](../vpn-gateway/vpn-gateway-highlyavailable.md).
* Voor het configureren van eBGP-sessies tussen de VPN-tunnels, moet u twee verschillende ASN links of rechts. Is het raadzaam om persoonlijke ASN-nummers opgeven. Zie voor meer informatie [overzicht van BGP- en Azure VPN-gateways](../vpn-gateway/vpn-gateway-bgp-overview.md).

```json
{
"apiVersion": "[variables('api-version')]",
"type": "Microsoft.Network/virtualNetworkGateways",
"name": "[variables('gatewayName')]",
"location": "[resourceGroup().location]",
"dependsOn": [
  "[concat('Microsoft.Network/publicIPAddresses/', variables('gatewayPublicIPName1'))]",
  "[concat('Microsoft.Network/publicIPAddresses/', variables('gatewayPublicIPName2'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
],
"properties": {
  "ipConfigurations": [
    {
      "properties": {
        "privateIPAllocationMethod": "Dynamic",
        "subnet": {
          "id": "[variables('gatewaySubnetRef')]"
        },
        "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('gatewayPublicIPName1'))]"
        }
      },
      "name": "vnetGtwConfig1"
    },
    {
      "properties": {
        "privateIPAllocationMethod": "Dynamic",
        "subnet": {
          "id": "[variables('gatewaySubnetRef')]"
        },
        "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('gatewayPublicIPName2'))]"
        }
      },
          "name": "vnetGtwConfig2"
        }
      ],
      "sku": {
        "name": "[variables('gatewaySku')]",
        "tier": "[variables('gatewaySku')]"
      },
      "gatewayType": "Vpn",
      "vpnType": "[variables('vpnType')]",
      "enableBgp": true,
      "activeActive": true,
      "bgpSettings": {
        "asn": "[variables('asnVpnGateway')]"
      }
    },
    "comments": "VPN Gateway in active-active configuration with BGP support"
  },
```

### <a name="ipsectunnel"></a>3.6 tot stand brengen van de IPsec-tunnels

De laatste actie van het script wordt gemaakt van IPsec-tunnels tussen de Azure VPN-gateway en de on-premises VPN-apparaat.

```json
{
  "apiVersion": "[variables('api-version')]",
  "name": "[variables('connectionName')]",
  "type": "Microsoft.Network/connections",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworkGateways/', variables('gatewayName'))]",
    "[concat('Microsoft.Network/localNetworkGateways/', variables('localGatewayName'))]"
  ],
  "properties": {
    "virtualNetworkGateway1": {
      "id": "[resourceId('Microsoft.Network/virtualNetworkGateways', variables('gatewayName'))]"
    },
    "localNetworkGateway2": {
      "id": "[resourceId('Microsoft.Network/localNetworkGateways', variables('localGatewayName'))]"
    },
    "connectionType": "IPsec",
    "routingWeight": 0,
    "sharedKey": "[variables('sharedKey')]",
    "enableBGP": "true"
  },
  "comments": "Create a Connection type site-to-site (IPsec) between the Azure VPN Gateway and the VPN device on-premises"
  }
```

## <a name="device"></a>4. De on-premises VPN-apparaat configureren

De Azure VPN-gateway is compatibel met veel VPN-apparaten van verschillende leveranciers. Zie voor informatie over de configuratie en apparaten die zijn gevalideerd om te werken met VPN-gateway [over VPN-apparaten](../vpn-gateway/vpn-gateway-about-vpn-devices.md).

Bij het configureren van uw VPN-apparaat, moet u de volgende items:

* Een gedeelde sleutel. Dit is dezelfde gedeelde sleutel die u opgeeft bij het maken van uw site-naar-site VPN-verbinding. De voorbeelden gebruikt een gedeelde sleutel. We raden u aan een complexere sleutel te genereren.
* Het openbare IP-adres van uw VPN-gateway. U kunt het openbare IP-adres weergeven met behulp van Azure Portal, PowerShell of de CLI. Als u wilt zoeken naar het openbare IP-adres van uw VPN-gateway met de Azure portal, Ga naar gateways voor virtueel netwerk en klik op de naam van uw gateway.

Doorgaans zijn eBGP peers rechtstreeks verbonden (vaak via een WAN-verbinding). Wanneer u eBGP via IPsec VPN-tunnels configureert via ExpressRoute-Microsoft-peering, zijn er echter meerdere Routeringsdomeinen tussen de eBGP-peers. Gebruik de **ebgp multihop** opdracht tot stand brengen van de eBGP neighbor relatie tussen de twee niet-peers rechtstreeks wordt verbonden. Het gehele getal dat volgt op ebgp multihop-opdracht geeft de TTL-waarde in de BGP-pakketten. De opdracht **maximum paden eibgp 2** maakt taakverdeling van verkeer tussen de twee paden van BGP.

### <a name="cisco1"></a>Cisco CSR1000 voorbeeld

Het volgende voorbeeld ziet u de configuratie voor Cisco CSR1000 in een Hyper-V virtuele machine als de on-premises VPN-apparaat:

```
!
crypto ikev2 proposal az-PROPOSAL
 encryption aes-cbc-256 aes-cbc-128 3des
 integrity sha1
 group 2
!
crypto ikev2 policy az-POLICY
 proposal az-PROPOSAL
!
crypto ikev2 keyring key-peer1
 peer azvpn1
  address 52.175.253.112
  pre-shared-key secret*1234
 !
!
crypto ikev2 keyring key-peer2
 peer azvpn2
  address 52.175.250.191
  pre-shared-key secret*1234
 !
!
!
crypto ikev2 profile az-PROFILE1
 match address local interface GigabitEthernet1
 match identity remote address 52.175.253.112 255.255.255.255
 authentication remote pre-share
 authentication local pre-share
 keyring local key-peer1
!
crypto ikev2 profile az-PROFILE2
 match address local interface GigabitEthernet1
 match identity remote address 52.175.250.191 255.255.255.255
 authentication remote pre-share
 authentication local pre-share
 keyring local key-peer2
!
crypto ikev2 dpd 10 2 on-demand
!
!
crypto ipsec transform-set az-IPSEC-PROPOSAL-SET esp-aes 256 esp-sha-hmac
 mode tunnel
!
crypto ipsec profile az-VTI1
 set transform-set az-IPSEC-PROPOSAL-SET
 set ikev2-profile az-PROFILE1
!
crypto ipsec profile az-VTI2
 set transform-set az-IPSEC-PROPOSAL-SET
 set ikev2-profile az-PROFILE2
!
!
interface Loopback0
 ip address 172.16.0.3 255.255.255.255
!
interface Tunnel0
 ip address 172.16.0.1 255.255.255.255
 ip tcp adjust-mss 1350
 tunnel source GigabitEthernet1
 tunnel mode ipsec ipv4
 tunnel destination 52.175.253.112
 tunnel protection ipsec profile az-VTI1
!
interface Tunnel1
 ip address 172.16.0.2 255.255.255.255
 ip tcp adjust-mss 1350
 tunnel source GigabitEthernet1
 tunnel mode ipsec ipv4
 tunnel destination 52.175.250.191
 tunnel protection ipsec profile az-VTI2
!
interface GigabitEthernet1
 description External interface
 ip address x.243.229.110 255.255.255.252
 negotiation auto
 no mop enabled
 no mop sysid
!
interface GigabitEthernet2
 ip address 10.0.0.1 255.255.255.0
 negotiation auto
 no mop enabled
 no mop sysid
!
router bgp 65010
 bgp router-id interface Loopback0
 bgp log-neighbor-changes
 network 10.0.0.0 mask 255.255.255.0
 network 10.1.10.0 mask 255.255.255.128
 neighbor 10.2.0.228 remote-as 65000
 neighbor 10.2.0.228 ebgp-multihop 5
 neighbor 10.2.0.228 update-source Loopback0
 neighbor 10.2.0.228 soft-reconfiguration inbound
 neighbor 10.2.0.228 filter-list 10 out
 neighbor 10.2.0.229 remote-as 65000    
 neighbor 10.2.0.229 ebgp-multihop 5
 neighbor 10.2.0.229 update-source Loopback0
 neighbor 10.2.0.229 soft-reconfiguration inbound
 maximum-paths eibgp 2
!
ip route 0.0.0.0 0.0.0.0 10.1.10.1
ip route 10.2.0.228 255.255.255.255 Tunnel0
ip route 10.2.0.229 255.255.255.255 Tunnel1
!
```

## <a name="firewalls"></a>5. Configureren van VPN-apparaat filteren en firewalls (optioneel)

Configureer uw firewall en filteren volgens uw vereisten.

## <a name="testipsec"></a>6. Testen en valideren van de IPsec-tunnel

De status van IPsec-tunnels kan worden gecontroleerd op de Azure VPN-gateway door Powershell-opdrachten:

```powershell
Get-AzureRmVirtualNetworkGatewayConnection -Name vpn2local1 -ResourceGroupName myRG | Select-Object  ConnectionStatus,EgressBytesTransferred,IngressBytesTransferred | fl
```

Voorbeelduitvoer:

```powershell
ConnectionStatus        : Connected
EgressBytesTransferred  : 17734660
IngressBytesTransferred : 10538211
```

Gebruikt u de status van de tunnels voor de Azure VPN-gateway-exemplaren onafhankelijk controleren door het volgende voorbeeld:

```powershell
Get-AzureRmVirtualNetworkGatewayConnection -Name vpn2local1 -ResourceGroupName myRG | Select-Object -ExpandProperty TunnelConnectionStatus
```

Voorbeelduitvoer:

```powershell
Tunnel                           : vpn2local1_52.175.250.191
ConnectionStatus                 : Connected
IngressBytesTransferred          : 4877438
EgressBytesTransferred           : 8754071
LastConnectionEstablishedUtcTime : 11/04/2017 17:03:30

Tunnel                           : vpn2local1_52.175.253.112
ConnectionStatus                 : Connected
IngressBytesTransferred          : 5660773
EgressBytesTransferred           : 8980589
LastConnectionEstablishedUtcTime : 11/04/2017 17:03:13
```

U kunt ook de status van de tunnel controleren op uw on-premises VPN-apparaat.

Cisco CSR1000 voorbeeld:

```
show crypto session detail
show crypto ikev2 sa
show crypto ikev2 session detail
show crypto ipsec sa
```

Voorbeelduitvoer:

```
csr1#show crypto session detail

Crypto session current status

Code: C - IKE Configuration mode, D - Dead Peer Detection
K - Keepalives, N - NAT-traversal, T - cTCP encapsulation
X - IKE Extended Authentication, F - IKE Fragmentation
R - IKE Auto Reconnect

Interface: Tunnel1
Profile: az-PROFILE2
Uptime: 00:52:46
Session status: UP-ACTIVE
Peer: 52.175.250.191 port 4500 fvrf: (none) ivrf: (none)
      Phase1_id: 52.175.250.191
      Desc: (none)
  Session ID: 3
  IKEv2 SA: local 10.1.10.50/4500 remote 52.175.250.191/4500 Active
          Capabilities:DN connid:3 lifetime:23:07:14
  IPSEC FLOW: permit ip 0.0.0.0/0.0.0.0 0.0.0.0/0.0.0.0
        Active SAs: 2, origin: crypto map
        Inbound:  #pkts dec'ed 279 drop 0 life (KB/Sec) 4607976/433
        Outbound: #pkts enc'ed 164 drop 0 life (KB/Sec) 4607992/433

Interface: Tunnel0
Profile: az-PROFILE1
Uptime: 00:52:43
Session status: UP-ACTIVE
Peer: 52.175.253.112 port 4500 fvrf: (none) ivrf: (none)
      Phase1_id: 52.175.253.112
      Desc: (none)
  Session ID: 2
  IKEv2 SA: local 10.1.10.50/4500 remote 52.175.253.112/4500 Active
          Capabilities:DN connid:2 lifetime:23:07:17
  IPSEC FLOW: permit ip 0.0.0.0/0.0.0.0 0.0.0.0/0.0.0.0
        Active SAs: 2, origin: crypto map
        Inbound:  #pkts dec'ed 668 drop 0 life (KB/Sec) 4607926/437
        Outbound: #pkts enc'ed 477 drop 0 life (KB/Sec) 4607953/437
```

Het protocol regel op de virtuele Tunnel-Interface (VTI) wordt niet gewijzigd voor 'omhoog' totdat IKE fase 2 is voltooid. De volgende opdracht controleert of de beveiligingskoppeling:

```
csr1#show crypto ikev2 sa

IPv4 Crypto IKEv2  SA

Tunnel-id Local                 Remote                fvrf/ivrf            Status
2         10.1.10.50/4500       52.175.253.112/4500   none/none            READY
      Encr: AES-CBC, keysize: 256, PRF: SHA1, Hash: SHA96, DH Grp:2, Auth sign: PSK, Auth verify: PSK
      Life/Active Time: 86400/3277 sec

Tunnel-id Local                 Remote                fvrf/ivrf            Status
3         10.1.10.50/4500       52.175.250.191/4500   none/none            READY
      Encr: AES-CBC, keysize: 256, PRF: SHA1, Hash: SHA96, DH Grp:2, Auth sign: PSK, Auth verify: PSK
      Life/Active Time: 86400/3280 sec

IPv6 Crypto IKEv2  SA

csr1#show crypto ipsec sa | inc encaps|decaps
    #pkts encaps: 177, #pkts encrypt: 177, #pkts digest: 177
    #pkts decaps: 296, #pkts decrypt: 296, #pkts verify: 296
    #pkts encaps: 554, #pkts encrypt: 554, #pkts digest: 554
    #pkts decaps: 746, #pkts decrypt: 746, #pkts verify: 746
```

### <a name="verifye2e"></a>Controleren of de end-to-end-verbinding tussen de binnen on-premises en de Azure-VNet-netwerk

Als de IPsec-tunnels actief zijn en de statische routes correct zijn ingesteld, kunt u moet kunnen ping het IP-adres van de externe BGP-peer:

```
csr1#ping 10.2.0.228
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.2.0.228, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 5/5/5 ms

#ping 10.2.0.229
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.2.0.229, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 4/5/6 ms
```

### <a name="verifybgp"></a>Controleer of de BGP-sessies via IPsec

Controleer de status van de BGP-peer op de Azure VPN-gateway:

```powershell
Get-AzureRmVirtualNetworkGatewayBGPPeerStatus -VirtualNetworkGatewayName vpnGtw -ResourceGroupName SEA-C1-VPN-ER | ft
```

Voorbeelduitvoer:

```powershell
  Asn ConnectedDuration LocalAddress MessagesReceived MessagesSent Neighbor    RoutesReceived State    
  --- ----------------- ------------ ---------------- ------------ --------    -------------- -----    
65010 00:57:19.9003584  10.2.0.228               68           72   172.16.0.10              2 Connected
65000                   10.2.0.228                0            0   10.2.0.228               0 Unknown  
65000 07:13:51.0109601  10.2.0.228              507          500   10.2.0.229               6 Connected
```

Om te controleren of de lijst met ontvangen via eBGP van de VPN-concentrator on-premises netwerkvoorvoegsels, kunt u filteren op kenmerk 'Origin':

```powershell
Get-AzureRmVirtualNetworkGatewayLearnedRoute -VirtualNetworkGatewayName vpnGtw -ResourceGroupName myRG  | Where-Object Origin -eq "EBgp" |ft
```

In het voorbeeld van uitvoer is de ASN-65010 de autonoom systeemnummer BGP in de VPN-on-premises.

```powershell
AsPath LocalAddress Network      NextHop     Origin SourcePeer  Weight
------ ------------ -------      -------     ------ ----------  ------
65010  10.2.0.228   10.1.10.0/25 172.16.0.10 EBgp   172.16.0.10  32768
65010  10.2.0.228   10.0.0.0/24  172.16.0.10 EBgp   172.16.0.10  32768
```

Voor een overzicht van aangekondigde routes:

```powershell
Get-AzureRmVirtualNetworkGatewayAdvertisedRoute -VirtualNetworkGatewayName vpnGtw -ResourceGroupName myRG -Peer 10.2.0.228 | ft
```

Voorbeelduitvoer:

```powershell
AsPath LocalAddress Network        NextHop    Origin SourcePeer Weight
------ ------------ -------        -------    ------ ---------- ------
       10.2.0.229   10.2.0.0/24    10.2.0.229 Igp                  0
       10.2.0.229   172.16.0.10/32 10.2.0.229 Igp                  0
       10.2.0.229   172.16.0.5/32  10.2.0.229 Igp                  0
       10.2.0.229   172.16.0.1/32  10.2.0.229 Igp                  0
65010  10.2.0.229   10.1.10.0/25   10.2.0.229 Igp                  0
65010  10.2.0.229   10.0.0.0/24    10.2.0.229 Igp                  0
```

Voorbeeld voor de on-premises Cisco CSR1000:

```
csr1#show ip bgp neighbors 10.2.0.228 routes
BGP table version is 7, local router ID is 172.16.0.10
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
              t secondary path,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *>   10.2.0.0/24      10.2.0.228                             0 65000 i
 r>   172.16.0.1/32    10.2.0.228                             0 65000 i
 r>   172.16.0.2/32    10.2.0.228                             0 65000 i
 r>   172.16.0.3/32   10.2.0.228                             0 65000 i

Total number of prefixes 4
```

De lijst met netwerken die worden geadverteerd vanuit de lokale Cisco CSR1000 naar de Azure VPN-gateway kan worden weergegeven met de volgende opdracht:

```powershell
csr1#show ip bgp neighbors 10.2.0.228 advertised-routes
BGP table version is 7, local router ID is 172.16.0.10
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
              t secondary path,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *>   10.0.0.0/24      0.0.0.0                  0         32768 i
 *>   10.1.10.0/25     0.0.0.0                  0         32768 i

Total number of prefixes 2
```

## <a name="next-steps"></a>Volgende stappen

* [Netwerkprestatiemeter configureren voor ExpressRoute](how-to-npm.md)

* [Een site-naar-site-verbinding toevoegen aan een VNet met een bestaande VPN-gateway-verbinding](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)