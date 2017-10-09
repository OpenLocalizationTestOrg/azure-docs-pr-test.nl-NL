---
title: 'ExpressRoute- en site-naar-site-VPN-verbindingen configureren die naast elkaar kunnen worden gebruikt: klassiek: Azure | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van ExpressRoute en Site-naar-Site VPN-verbindingen die naast elkaar kan bestaan voor het klassieke implementatiemodel Hallo.
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>Gelijktijdige ExpressRoute- en site-to-site-verbindingen configureren (klassiek)
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Klassiek](expressroute-howto-coexist-classic.md)
> 
> 

Hallo mogelijkheid tooconfigure Site-naar-Site VPN en ExpressRoute heeft verschillende voordelen. U kunt Site-naar-Site-VPN configureren als een beveiligd failoverpad voor ExressRoute of Site-naar-Site VPN-verbindingen tooconnect toosites die niet zijn verbonden via ExpressRoute. Wordt ingegaan op het Hallo stappen tooconfigure beide scenario's in dit artikel. In dit artikel is van toepassing toohello klassieke implementatiemodel. Deze configuratie is niet beschikbaar in Hallo-portal.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Over Azure-implementatiemodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> ExpressRoute-circuits moeten vooraf worden geconfigureerd voordat u Hallo onderstaande instructies volgt. Zorg ervoor dat u Hallo handleidingen te hebt gevolgd[maken van een ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en [routering configureren](expressroute-howto-routing-classic.md) voordat u Hallo hieronder stappen.
> 
> 

## <a name="limits-and-limitations"></a>Limieten en beperkingen
* **Transitroutering wordt niet ondersteund.** U kunt niet (via Azure) routeren tussen uw lokale netwerk dat is verbonden via site-naar-site-VPN en uw lokale netwerk dat is verbonden via ExpressRoute.
* **Punt-naar-site wordt niet ondersteund.** U kunt daar geen punt-naar-site VPN-verbindingen toohello hetzelfde VNet dat is verbonden tooExpressRoute. Punt-naar-site-VPN en ExpressRoute kunnen niet worden gecombineerd voor Hallo hetzelfde VNet.
* **Geforceerde tunneling kan niet worden ingeschakeld op Hallo Site-naar-Site VPN-gateway.** U kunt alleen 'forceren' alle Internet bestemd verkeer back tooyour on-premises netwerk via ExpressRoute.
* **Basic SKU-gateway wordt niet ondersteund.** U moet een niet - basis-SKU-gateway gebruiken voor beide Hallo [ExpressRoute-gateway](expressroute-about-virtual-network-gateways.md) en Hallo [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Alleen een op route gebaseerde VPN-gateway wordt ondersteund.** U moet een op route gebaseerde [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) gebruiken.
* **Statische route moet worden geconfigureerd voor de VPN-gateway.** Als uw lokale netwerk verbonden tooboth ExpressRoute is en een Site-naar-Site VPN, u een statische route geconfigureerd in uw lokale netwerk tooroute Hallo Site-naar-Site VPN-verbinding toohello hebben moet openbare Internet.
* **ExpressRoute gateway moet eerst worden geconfigureerd.** U moet eerst Hallo ExpressRoute-gateway maken voordat u Hallo Site-naar-Site VPN-gateway toevoegt.

## <a name="configuration-designs"></a>Configuratie-ontwerpen
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Een site-naar-site-VPN configureren als een failoverpad voor ExpressRoute
U kunt een site-naar-site-VPN-verbinding configureren als een back-up voor ExpressRoute. Dit geldt alleen toovirtual netwerken gekoppelde toohello pad Azure-persoonlijke peering. Er is geen op VPN gebaseerde failoveroplossing voor services die toegankelijk zijn via openbare Azure- en Microsoft-peerings. Hallo ExpressRoute-circuit is altijd Hallo primaire koppeling. Gegevens worden overgebracht via Site-naar-Site VPN-pad Hallo alleen als Hallo ExpressRoute-circuit is mislukt. 

> [!NOTE]
> ExpressRoute-circuit is voorkeur via Site-naar-Site VPN wanneer beide routes worden dezelfde hello, gebruikt Azure Hallo langste voorvoegsel overeen toochoose Hallo route naar de bestemming hello-pakket.
> 
> 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Een Site-naar-Site VPN-tooconnect toosites niet is verbonden via ExpressRoute configureren
U kunt uw netwerk waarbij sommige sites verbinding rechtstreeks tooAzure via Site-naar-Site VPN en sommige sites verbinding maken via ExpressRoute. 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> U kunt een virtueel netwerk niet configureren als transitrouter.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Hallo stappen toouse selecteren
Er zijn twee sets met procedures toochoose uit in de volgorde tooconfigure verbindingen die naast elkaar kunnen bestaan. Hallo-configuratieprocedure u selecteert afhankelijk van of u een bestaand virtueel netwerk dat u tooconnect naar wilt, of u wilt dat toocreate een nieuw virtueel netwerk hebt.

* Ik heb geen VNet en moet er toocreate een.
  
    Als u niet al een virtueel netwerk hebt, begeleidt deze procedure u stapsgewijs door het maken van een nieuw virtueel netwerk met behulp van het klassieke implementatiemodel Hallo en het maken van nieuwe ExpressRoute- en Site-naar-Site VPN-verbindingen. tooconfigure, Hallo Volg de stappen in de sectie artikel Hallo [toocreate een nieuw virtueel netwerk en naast elkaar bestaande verbindingen](#new).
* Ik heb al een VNet met het klassieke implementatiemodel.
  
    Mogelijk hebt u al een virtueel netwerk met een bestaande site-naar-site-VPN-verbinding of ExpressRoute-verbinding. sectie artikel Hallo [tooconfigure naast elkaar bestaande verbindingen voor een bestaand VNet](#add) begeleidt u bij het verwijderen van Hallo-gateway en vervolgens het maken van nieuwe ExpressRoute- en Site-naar-Site VPN-verbindingen. Houd er rekening mee dat wanneer u nieuwe verbindingen maakt hello, Hallo stappen moeten worden uitgevoerd in een specifieke volgorde. Gebruik geen Hallo-instructies in de andere artikelen toocreate uw gateways en verbindingen.
  
    In deze procedure, maken verbindingen die naast elkaar kunnen bestaan vereisen toodelete u uw gateway, en vervolgens nieuwe gateways configureren. Dit betekent dat u uitvaltijd voor uw cross-premises verbindingen terwijl u verwijderen en opnieuw maken van uw gateway en verbindingen, maar u niet toomigrate hoeft van uw virtuele machines of services tooa nieuw virtueel netwerk. Uw virtuele machines en services nog steeds kunnen toocommunicate uit via Hallo load balancer terwijl u uw gateway configureren als ze geconfigureerde toodo dus zijn.

## <a name="new"></a>toocreate een nieuw virtueel netwerk en naast elkaar bestaande verbindingen
Deze procedure helpt u bij het maken van een VNet en site-naar-site- en ExpressRoute-verbindingen die naast elkaar kunnen worden gebruikt.

1. U moet tooinstall Hallo meest recente versie van hello Azure PowerShell-cmdlets. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets. Houd er rekening mee dat Hallo-cmdlets die u voor deze configuratie mogelijk enigszins afwijken van wat u mogelijk bekend zijn met. Ervoor toouse Hallo cmdlets worden opgegeven in deze instructies. 
2. Maak een schema voor het virtuele netwerk. Zie voor meer informatie over het configuratieschema Hallo [Azure Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   
    Wanneer u uw schema maakt, moet dat u Hallo volgende waarden gebruiken:
   
   * Hallo gatewaysubnet voor het virtuele netwerk Hallo moet/27 of een korter voorvoegsel (zoals/26 of /25).
   * gateway-verbindingstype Hallo 'speciale' is.
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. Na het maken en configureren van uw XML-schemabestanden, Hallo-bestand te uploaden. Hiermee maakt u het virtuele netwerk.
   
    Hallo cmdlet tooupload na het bestand en vervang Hallo waarde door uw eigen gebruiken.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>Maak een ExpressRoute-gateway. Ervoor toospecify worden Hallo GatewaySKU *standaard*, *HighPerformance*, of *UltraPerformance* en GatewayType Hallo *DynamicRouting*.
   
    Hallo voorbeeld te volgen, vervangen door Hallo waarden voor uw eigen gebruik.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Koppeling Hallo ExpressRoute-gateway toohello ExpressRoute-circuit. Nadat deze stap is voltooid, Hallo-verbinding tussen uw on-premises netwerk en Azure via ExpressRoute, tot stand is gebracht.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>Maak vervolgens uw site-naar-site-VPN-gateway. Hallo GatewaySKU moet *standaard*, *HighPerformance*, of *UltraPerformance* en hello GatewayType *DynamicRouting*.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    tooretrieve hello virtueel netwerk gatewayinstellingen, inclusief Hallo gateway-ID en Hallo openbare IP-adres gebruiken Hallo `Get-AzureVirtualNetworkGateway` cmdlet.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. Maak een lokaal exemplaar van de VPN-gateway van uw site. Deze opdracht wordt niet gebruikt om uw on-premises VPN-gateway te configureren. In plaats daarvan kunt u Hiermee tooprovide Hallo lokale gateway-instellingen, zoals Hallo openbare IP-adres en hello op premises-adresruimte, zodat hello Azure VPN-gateway verbinding tooit maken kan.
   
   > [!IMPORTANT]
   > Hallo lokale site voor Hallo Site-naar-Site VPN is niet gedefinieerd in Hallo netcfg. In plaats daarvan moet u deze cmdlet-parameters voor lokale site toospecify hello gebruiken. U kunt met behulp van de portal of Hallo netcfg-bestand niet definiëren.
   > 
   > 
   
    Hallo volgende voorbeeld, waarbij Hallo waarden vervangt door uw eigen gebruik.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > Als uw lokale netwerk meerdere routes heeft, kunt u ze doorgeven als een matrix.  $MyLocalNetworkAddress = @('10.1.2.0/24', '10.1.3.0/24', '10.2.1.0/24')  
   > 
   > 

    tooretrieve hello virtueel netwerk gatewayinstellingen, inclusief Hallo gateway-ID en Hallo openbare IP-adres gebruiken Hallo `Get-AzureVirtualNetworkGateway` cmdlet. Zie Hallo voorbeeld te volgen.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. Configureer uw lokale VPN-apparaat tooconnect toohello nieuwe gateway. Hallo-informatie die u hebt opgehaald in stap 6 bij het configureren van uw VPN-apparaat gebruiken. Zie [VPN-apparaatconfiguratie](../vpn-gateway/vpn-gateway-about-vpn-devices.md) voor meer informatie over het configureren van een VPN-apparaat. 
2. Koppeling Hallo Site-naar-Site VPN-gateway op de lokale gateway Azure toohello.
   
    In dit voorbeeld is connectedEntityId de lokale gateway-id. hello, kunt u vinden door te voeren `Get-AzureLocalNetworkGateway`. U kunt virtualnetworkgatewayid vinden met behulp van Hallo `Get-AzureVirtualNetworkGateway` cmdlet. Na deze stap Hallo verbinding tussen uw lokale netwerk en Azure via Hallo Site-naar-Site VPN-verbinding tot stand is gebracht.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>tooconfigure naast elkaar bestaande verbindingen voor een bestaand VNet
Als u een bestaand virtueel netwerk hebt, controleert u Hallo gateway subnetgrootte. Als Hallo gatewaysubnet/28 of slechts/29 is, moet u Hallo virtuele netwerkgateway verwijderen en vergroot Hallo gateway-subnet. Hallo stappen in deze sectie wordt uitgelegd hoe u toodo die.

Als Hallo gatewaysubnet/27 of groter en Hallo virtueel netwerk is verbonden via ExpressRoute, kunt u Hallo onderstaande stappen overslaan en doorgaan te['Stap 6: een Site-naar-Site VPN-gateway maken'](#vpngw) in de vorige sectie Hallo.

> [!NOTE]
> Wanneer u Hallo bestaande gateway verwijdert, wordt uw lokale site Hallo verbinding tooyour virtuele netwerk verbroken terwijl u bezig bent met deze configuratie.
> 
> 

1. U moet tooinstall Hallo meest recente versie van hello Azure Resource Manager PowerShell-cmdlets. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets. Houd er rekening mee dat Hallo-cmdlets die u voor deze configuratie mogelijk enigszins afwijken van wat u mogelijk bekend zijn met. Ervoor toouse Hallo cmdlets worden opgegeven in deze instructies. 
2. Verwijder de bestaande ExpressRoute of Site-naar-Site VPN-gateway Hallo. Hallo volgende cmdlet, waarbij Hallo waarden vervangt door uw eigen gebruik.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Hallo virtueel netwerk schema exporteren. Hallo volgende PowerShell-cmdlet, waarbij Hallo waarden vervangt door uw eigen gebruik.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Hallo network-configuratieschema bestand bewerken zodat Hallo gatewaysubnet/27 of een korter voorvoegsel (zoals/26 of /25). Zie Hallo voorbeeld te volgen. 
   
   > [!NOTE]
   > Als u geen voldoende IP-adressen in uw virtuele netwerk tooincrease Hallo gateway subnetgrootte gelaten, moet u tooadd meer IP-adresruimte. Zie voor meer informatie over het configuratieschema Hallo [Azure Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. Als uw vorige gateway een Site-naar-Site-VPN was, moet u ook wijzigen Hallo verbindingstype te**toegewezen**.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. U hebt op dit moment een VNet zonder gateways. toocreate nieuwe gateways en uw verbindingen is voltooid, kunt u doorgaan met [stap 4 - een ExpressRoute-gateway maken](#gw)vindt u in de voorgaande reeks stappen Hallo.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md)

