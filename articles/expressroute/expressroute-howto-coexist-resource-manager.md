---
title: 'ExpressRoute- en site-naar-site-VPN-verbindingen configureren die naast elkaar kunnen worden gebruikt: klassiek: Resource Manager: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij het configureren van ExpressRoute- en site-naar-site-VPN-verbindingen die naast elkaar kunnen worden gebruikt in het Resource Manager-implementatiemodel.
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Gelijktijdige ExpressRoute- en site-to-site-verbindingen configureren
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Klassiek](expressroute-howto-coexist-classic.md)
> 
> 

Configuratie van gelijktijdige site-naar-site-VPN- en ExpressRoute-verbindingen heeft verschillende voordelen. U kunt een Site-naar-Site-VPN configureren als een beveiligd failoverpad voor ExressRoute of Site-naar-Site VPN-verbindingen tooconnect toosites die niet zijn verbonden via ExpressRoute. We hebben betrekking op Hallo stappen tooconfigure beide scenario's in dit artikel. In dit artikel is van toepassing toohello Resource Manager-implementatiemodel en PowerShell gebruikt. Deze configuratie is niet beschikbaar in hello Azure-portal.

> [!IMPORTANT]
> ExpressRoute-circuits moeten vooraf worden geconfigureerd voordat u Hallo onderstaande instructies volgt. Zorg ervoor dat u Hallo handleidingen te hebt gevolgd[maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en [routering configureren](expressroute-howto-routing-arm.md) voordat u doorgaat.
> 
> 

## <a name="limits-and-limitations"></a>Limieten en beperkingen
* **Transitroutering wordt niet ondersteund.** U kunt niet (via Azure) routeren tussen uw lokale netwerk dat is verbonden via site-naar-site-VPN en uw lokale netwerk dat is verbonden via ExpressRoute.
* **Basic SKU-gateway wordt niet ondersteund.** U moet een niet - basis-SKU-gateway gebruiken voor beide Hallo [ExpressRoute-gateway](expressroute-about-virtual-network-gateways.md) en Hallo [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Alleen een op route gebaseerde VPN-gateway wordt ondersteund.** U moet een op route gebaseerde [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) gebruiken.
* **Statische route moet worden geconfigureerd voor de VPN-gateway.** Als uw lokale netwerk verbonden tooboth ExpressRoute is en een Site-naar-Site VPN, u een statische route geconfigureerd in uw lokale netwerk tooroute Hallo Site-naar-Site VPN-verbinding toohello hebben moet openbare Internet.
* **ExpressRoute-gateway moet als eerste worden geconfigureerd en tooa circuit gekoppeld.** U moet Hallo ExpressRoute-gateway maken en een koppeling tooa circuit voordat u Hallo Site-naar-Site VPN-gateway toevoegt.

## <a name="configuration-designs"></a>Configuratie-ontwerpen
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Een site-naar-site-VPN configureren als een failoverpad voor ExpressRoute
U kunt een site-naar-site-VPN-verbinding configureren als een back-up voor ExpressRoute. Dit geldt alleen toovirtual netwerken gekoppelde toohello pad Azure-persoonlijke peering. Er is geen op VPN gebaseerde failoveroplossing voor services die toegankelijk zijn via openbare Azure- en Microsoft-peerings. Hallo ExpressRoute-circuit is altijd Hallo primaire koppeling. Gegevens loopt via de Site-naar-Site VPN-pad Hallo alleen als Hallo ExpressRoute-circuit is mislukt.

> [!NOTE]
> ExpressRoute-circuit is voorkeur via Site-naar-Site VPN wanneer beide routes worden dezelfde hello, gebruikt Azure Hallo langste voorvoegsel overeen toochoose Hallo route naar de bestemming hello-pakket.
> 
> 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Een Site-naar-Site VPN-tooconnect toosites niet is verbonden via ExpressRoute configureren
U kunt uw netwerk waarbij sommige sites verbinding rechtstreeks tooAzure via Site-naar-Site VPN en sommige sites verbinding maken via ExpressRoute. 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> U kunt een virtueel netwerk niet configureren als transitrouter.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Hallo stappen toouse selecteren
Er zijn twee sets met procedures toochoose uit. Hallo-configuratieprocedure u selecteert, is afhankelijk van of u een bestaand virtueel netwerk dat u tooconnect naar wilt, of u wilt dat toocreate een nieuw virtueel netwerk hebt.

* Ik heb geen VNet en moet er toocreate een.
  
    Als u nog geen virtueel netwerk hebt, begeleidt deze procedure u bij het maken van een nieuw virtueel netwerk met behulp van de Resource Manager-implementatie, en bij het maken van nieuwe ExpressRoute- en site-naar-site-VPN-verbindingen. een virtueel netwerk tooconfigure Hallo stappen in [toocreate een nieuw virtueel netwerk en naast elkaar bestaande verbindingen](#new).
* Ik heb al een VNet van het Resource Manager-implementatiemodel.
  
    Mogelijk hebt u al een virtueel netwerk met een bestaande site-naar-site-VPN-verbinding of ExpressRoute-verbinding. Hallo [tooconfigure naast elkaar bestaande verbindingen voor een bestaand VNet](#add) sectie leidt u door het verwijderen van Hallo-gateway en vervolgens nieuwe ExpressRoute- en Site-naar-Site VPN-verbindingen te maken. Hallo maken van nieuwe verbindingen, Hallo stappen moeten worden uitgevoerd in een bepaalde volgorde. Gebruik geen Hallo-instructies in de andere artikelen toocreate uw gateways en verbindingen.
  
    In deze procedure, maken verbindingen die naast elkaar kunnen bestaan vereist toodelete u uw gateway en vervolgens nieuwe gateways configureren. Hebt u uitvaltijd voor uw cross-premises verbindingen terwijl u verwijderen en opnieuw maken van uw gateway en verbindingen, maar u niet toomigrate hoeft van uw virtuele machines of services tooa nieuw virtueel netwerk. Uw virtuele machines en services nog steeds kunnen toocommunicate uit via Hallo load balancer terwijl u uw gateway configureren als ze geconfigureerde toodo dus zijn.

## <a name="new"></a>toocreate een nieuw virtueel netwerk en naast elkaar bestaande verbindingen
Deze procedure begeleidt u bij het maken van een VNet en van site-naar-site- en ExpressRoute-verbindingen die naast elkaar kunnen worden gebruikt.

1. Installeer de nieuwste versie Hallo Hallo Azure PowerShell-cmdlets. Zie voor meer informatie over het installeren van de cmdlets Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). Hallo-cmdlets die u voor deze configuratie gebruikt is mogelijk enigszins afwijken van wat u mogelijk bekend zijn. Ervoor toouse Hallo cmdlets worden opgegeven in deze instructies.
2. Meld u in tooyour-account en Hallo-omgeving instellen.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Maak een virtueel netwerk met een gatewaysubnet. Zie voor meer informatie over de configuratie van een virtueel netwerk Hallo [Azure Virtual Network-configuratie](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Hallo Gatewaysubnet moet/27 of een korter voorvoegsel (zoals/26 of /25).
   > 
   > 
   
    Maak een nieuw VNet.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Voeg subnetten toe.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Hallo-VNet-configuratie op te slaan.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>Maak een ExpressRoute-gateway. Zie voor meer informatie over ExpressRoute-gatewayconfiguratie Hallo [ExpressRoute-gatewayconfiguratie](expressroute-howto-add-gateway-resource-manager.md). Hallo GatewaySKU moet *standaard*, *HighPerformance*, of *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Koppeling Hallo ExpressRoute-gateway toohello ExpressRoute-circuit. Nadat deze stap is voltooid, Hallo-verbinding tussen uw on-premises netwerk en Azure via ExpressRoute, tot stand is gebracht. Zie voor meer informatie over de koppelingsbewerking Hallo [VNets koppelen tooExpressRoute](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>Maak vervolgens uw site-naar-site-VPN-gateway. Zie voor meer informatie over de configuratie van VPN-gateway Hallo [een VNet met een Site-naar-Site-verbinding configureren](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Hallo GatewaySKU moet *standaard*, *HighPerformance*, of *UltraPerformance*. Hallo VpnType moet *RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Azure VPN-gateway biedt ondersteuning voor BGP-routeringsprotocol. U kunt ASN (AS-nummer) opgeven voor dit virtuele netwerk door Hallo - Asn switch toe te voegen in de volgende opdracht Hallo. Deze parameter niet opgeeft wordt standaard tooAS nummer 65515.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    U kunt zoeken Hallo BGP-peer-IP en Hallo als getal die gebruikmaakt van Azure voor Hallo VPN-gateway in $azureVpn.BgpSettings.BgpPeeringAddress en $azureVpn.BgpSettings.Asn. Zie [BGP configureren](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) voor Azure VPN-gateway voor meer informatie.
7. Maak een lokaal exemplaar van de VPN-gateway van uw site. Deze opdracht wordt niet gebruikt om uw on-premises VPN-gateway te configureren. In plaats daarvan kunt u Hiermee tooprovide Hallo lokale gateway-instellingen, zoals Hallo openbare IP-adres en hello op premises-adresruimte, zodat hello Azure VPN-gateway verbinding tooit maken kan.
   
    Als uw lokale VPN-apparaat alleen statische routering ondersteunt, kunt u Hallo statische routes in de volgende manieren Hallo configureren:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Als uw lokale VPN-apparaat Hallo BGP ondersteunt en u wilt dat dynamische routering tooenable, moet u tooknow Hallo BGP peering IP-adres en Hallo als number die uw lokale VPN-apparaat gebruikt.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Configureer uw lokale VPN-apparaat tooconnect toohello nieuwe Azure VPN-gateway. Zie [VPN-apparaatconfiguratie](../vpn-gateway/vpn-gateway-about-vpn-devices.md) voor meer informatie over het configureren van een VPN-apparaat. 
9. Koppeling Hallo Site-naar-Site VPN-gateway op de lokale gateway Azure toohello.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>naast elkaar bestaande verbindingen tooconfigure voor een bestaand VNet
Als u een bestaand virtueel netwerk hebt, controleert u Hallo gateway subnetgrootte. Als Hallo gatewaysubnet/28 of slechts/29 is, moet u Hallo virtuele netwerkgateway verwijderen en vergroot Hallo gateway-subnet. Hallo stappen in deze sectie laten zien hoe u toodo die.

Als Hallo gatewaysubnet/27 of groter en Hallo virtueel netwerk is verbonden via ExpressRoute, kunt u Hallo onderstaande stappen overslaan en doorgaan te['Stap 6: een Site-naar-Site VPN-gateway maken'](#vpngw) in de vorige sectie Hallo. 

> [!NOTE]
> Wanneer u Hallo bestaande gateway verwijdert, wordt uw lokale site Hallo verbinding tooyour virtuele netwerk verbroken terwijl u bezig bent met deze configuratie. 
> 
> 

1. U moet tooinstall Hallo meest recente versie van hello Azure PowerShell-cmdlets. Zie voor meer informatie over het installeren van cmdlets [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). Hallo-cmdlets die u voor deze configuratie gebruikt is mogelijk enigszins afwijken van wat u mogelijk bekend zijn. Ervoor toouse Hallo cmdlets worden opgegeven in deze instructies. 
2. Verwijder de bestaande ExpressRoute of Site-naar-Site VPN-gateway Hallo.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Verwijder het gatewaysubnet.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Voeg een gatewaysubnet toe van /27 of hoger.
   
   > [!NOTE]
   > Als u geen voldoende IP-adressen in uw virtuele netwerk tooincrease Hallo gateway subnetgrootte gelaten, moet u tooadd meer IP-adresruimte.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Hallo-VNet-configuratie op te slaan.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. U hebt op dit moment een VNet zonder gateways. toocreate nieuwe gateways en uw verbindingen is voltooid, kunt u doorgaan met [stap 4 - een ExpressRoute-gateway maken](#gw)vindt u in de voorgaande reeks stappen Hallo.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>tooadd punt-naar-site-configuratie toohello VPN-gateway
U kunt stappen Hallo hieronder tooadd punt-naar-Site configuratie tooyour VPN-gateway in de instellingen voor een naast elkaar bestaan.

1. Voeg een VPN-clientadresgroep toe.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Upload Hallo VPN-hoofdmap certificaat tooAzure voor uw VPN-gateway. In dit voorbeeld wordt ervan uitgegaan dat Hallo-basiscertificaat is opgeslagen in de lokale computer Hallo waarin Hallo volgende PowerShell-cmdlets worden uitgevoerd.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Zie [Een punt-naar-site-verbinding configureren](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) voor meer informatie over punt-naar-site-VPN.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).
