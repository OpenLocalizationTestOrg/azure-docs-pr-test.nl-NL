---
title: 'Verbinding maken met uw lokale netwerk tooan virtuele Azure-netwerk: Site-naar-Site VPN: Portal | Microsoft Docs'
description: Stappen toocreate een IPsec-verbinding van uw on-premises netwerk tooan virtuele Azure-netwerk via openbaar Internet Hallo. Deze stappen kunt u een cross-premises Site-naar-Site VPN-gatewayverbinding maken met de Hallo-portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Een Site-naar-Site-verbinding maken in hello Azure-portal

Dit artikel laat zien hoe toouse hello Azure portal toocreate een Site-naar-Site VPN-gatewayverbinding vanuit uw lokale netwerk toohello VNet. Hallo stappen in dit artikel van toepassing toohello Resource Manager-implementatiemodel. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel. Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit. Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.

![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Voordat u begint

Controleer of dat u Hallo criteria volgen voordat u begint met de configuratie hebt voldaan:

* Zorg ervoor dat u hebt een compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze. Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.
* Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt. Dit IP-adres kan zich niet achter een NAT bevinden.
* Als u niet bekend bent met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie, moet u toocoordinate met iemand die deze details voor u verstrekken kan. Wanneer u deze configuratie maakt, moet u Hallo IP-bereik adresvoorvoegsels Azure routeert tooyour on-premises locatie. Geen van de subnetten Hallo van uw on-premises netwerk kunnen via lap met Hallo virtueel netwerksubnetten die u wilt dat tooconnect om te. 

### <a name="values"></a>Voorbeeldwaarden

Hallo-voorbeelden in dit artikel gebruiken Hallo waarden te volgen. U kunt deze waarden toocreate een testomgeving gebruiken of toothem verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel.

* **VNet-naam:** TestVNet1
* **Adresruimte:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (optioneel voor deze oefening)
* **Subnetten:**
  * FrontEnd: 10.11.0.0/24
  * Back-end: 10.12.0.0/24 (optioneel voor deze oefening)
* **Gatewaysubnet**: 10.11.255.0/27
* **Resourcegroep:** TestRG1
* **Locatie:** VS - oost
* **DNS-server:** optioneel. Hallo IP-adres van uw DNS-server.
* **Gatewaynaam van het virtuele netwerk:** VNet1GW
* **Openbare IP:** VNet1GWIP
* **VPN-type:** Op route gebaseerd
* **Verbindingstype:** site-naar-site (IPsec)
* **Gatewaytype:** VPN
* **Naam van lokale netwerkgateway:** Site2
* **Verbindingsnaam:** VNet1toSite2

## <a name="CreatVNet"></a>1. Een virtueel netwerk maken

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Een DNS-server opgeven

DNS is niet vereist toocreate een Site-naar-Site-verbinding. Als u naamomzetting toohave voor resources die geïmplementeerd tooyour virtueel netwerk zijn wilt, moet u een DNS-server opgeven. Deze instelling kunt u opgeven Hallo DNS-server wilt u toouse voor naamomzetting voor dit virtuele netwerk. Hierdoor wordt geen DNS-server aangemaakt. Zie [Naamomzetting voor VM's en rolinstanties](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) voor meer informatie over naamomzetting.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Hallo gatewaysubnet maken

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Hallo VPN-gateway maken

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Hallo lokale netwerkgateway maken

Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie. U geeft Hallo site een naam waarmee Azure kunt tooit verwijzen, geeft u vervolgens Hallo IP-adres van Hallo lokale VPN-apparaat toowhich maakt u een verbinding. U wordt ook Hallo IP-adresvoorvoegsels worden doorgestuurd via Hallo VPN-gateway toohello VPN-apparaat. Hallo-adresvoorvoegsels die u opgeeft voorvoegsels Hallo zich op uw on-premises netwerk. Als uw lokale netwerkwijzigingen of u toochange Hallo openbaar IP-adres voor Hallo VPN-apparaat moet, kunt u eenvoudig hello waarden later bijwerken.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Uw VPN-apparaat configureren

Site-naar-Site-verbindingen tooan on-premises netwerk een VPN-apparaat vereist. In deze stap configureert u het VPN-apparaat. Bij het configureren van uw VPN-apparaat, moet u de volgende Hallo:

- Een gedeelde sleutel. Dit is Hallo dezelfde gedeelde sleutel die u opgeeft bij het maken van uw Site-naar-Site VPN-verbinding. In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel. Het is raadzaam dat u een complexere sleutel toouse genereert.
- Hallo openbare IP-adres van uw virtuele netwerkgateway. U kunt het openbare IP-adres Hallo weergeven met behulp van hello Azure-portal, PowerShell of CLI. toofind hello openbare IP-adres van uw VPN-gateway met behulp van hello Azure-portal te navigeren**gateways voor virtueel netwerk**, klikt u op Hallo-naam van uw gateway.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Hallo VPN-verbinding maken

Hallo Site-naar-Site VPN-verbinding tussen uw virtuele netwerkgateway en uw on-premises VPN-apparaat maken.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Hallo VPN-verbinding controleren

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa virtuele machine

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Hoe tooreset een VPN-gateway

Het opnieuw instellen van een Azure VPN-gateway is handig als u cross-premises VPN-connectiviteit verliest in een of meer Site-to-Site VPN-tunnels. In dit geval uw on-premises VPN-apparaten zijn alle naar behoren werkt, maar er kan geen tooestablish IPsec-tunnels met hello Azure VPN-gateways zijn. Zie [Een VPN-gateway opnieuw instellen](vpn-gateway-resetgw-classic.md) voor de stappen.

## <a name="resize"></a>Hoe toochange een gateway-SKU (formaat een gateway)

Voor Hallo toochange een gateway-SKU stappen, Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Zie [Informatie over geforceerde tunneling](vpn-gateway-forced-tunneling-rm.md) voor meer informatie over geforceerde tunneling.
* Zie [Maximaal beschikbare cross-premises en VNet-naar-VNet-connectiviteit](vpn-gateway-highlyavailable.md) voor meer informatie over maximaal beschikbare actieve verbindingen.
