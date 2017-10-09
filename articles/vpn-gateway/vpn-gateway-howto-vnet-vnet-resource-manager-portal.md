---
title: 'Verbinding maken met een virtuele Azure-netwerk tooanother VNet: Portal | Microsoft Docs'
description: Maken van een VPN-gatewayverbinding tussen VNets met Resource Manager en hello Azure-portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>Een VNet-naar-VNet-VPN-gatewayverbinding configureren met hello Azure-portal

Dit artikel ziet u hoe toocreate een VPN-gatewayverbinding tussen virtuele netwerken. Hallo virtuele netwerken kunnen zich in dezelfde of verschillende regio's Hallo en Hallo van dezelfde of verschillende abonnementen behoren. Bij het maken van verbinding VNets uit verschillende abonnementen behoren, Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant. 

Hallo stappen in dit artikel toepassen toohello Resource Manager-implementatiemodel en hello Azure-portal gebruiken. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure-CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Verbinding maken tussen verschillende implementatiemodellen - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Verbinding maken tussen verschillende implementatiemodellen - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![v2v-diagram](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

Verbinding maken met een virtueel netwerk tooanother virtueel netwerk (VNet-naar-VNet) is vergelijkbaar tooconnecting een VNet tooan on-premises-locatie. Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE. Als uw vnet's in Hallo zijn dezelfde regio, kunt u tooconsider deze met behulp van VNet-Peering te verbinden. Bij VNet-peering wordt geen VPN-gateway gebruikt. Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie.

VNet-naar-VNet-communicatie kan worden gecombineerd met configuraties voor meerdere locaties. Hiermee kunt u netwerktopologieën maken waarin cross-premises-connectiviteit met connectiviteit tussen virtuele netwerken, zoals wordt weergegeven in het volgende diagram Hallo:

![Over verbindingen](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "Over verbindingen")

### <a name="why-connect-virtual-networks"></a>Waarom virtuele netwerken koppelen?

U kunt virtuele netwerken tooconnect voor Hallo volgende redenen:

* **Geografische redundantie en aanwezigheid tussen regio's**
  
  * U kunt uw eigen geo-replicatie of synchronisatie met beveiligde connectiviteit instellen zonder gebruik te maken van internetgerichte eindpunten.
  * Met Azure Traffic Manager en Load Balancer kunt u workloads met maximale beschikbaarheid instellen met behulp van geografische redundantie over meerdere Azure-regio's. Een belangrijk voorbeeld hiervan is tooset van SQL Always On met beschikbaarheidsgroepen verspreid over meerdere Azure-regio's.
* **Regionale toepassingen met meerdere lagen met isolatie- of beheergrenzen**
  
  * Hallo binnen dezelfde regio, kunt u toepassingen met meerdere lagen instellen met meerdere virtuele netwerken met elkaar verbonden vervaldatum tooisolation of beheervereisten.

Zie voor meer informatie over VNet-naar-VNet-verbindingen Hallo [Veelgestelde vragen over VNet-naar-VNet](#faq) aan Hallo einde van dit artikel. Houd er rekening mee dat als uw vnet's zich in verschillende abonnementen behoren, u Hallo verbinding in Hallo-portal maken kan. Gebruik in plaats daarvan [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) of de [CLI](vpn-gateway-howto-vnet-vnet-cli.md).

### <a name="values"></a>Voorbeeldinstellingen

Wanneer u deze stappen wijze van oefening maakt, kunt u instellingen voor Hallo voorbeeldwaarden. Als voorbeeld gebruiken we meerdere adresruimten voor elke VNet. Voor VNet-naar-VNet-configuraties zijn meerdere adresruimten echter niet vereist.

**Waarden voor TestVNet1:**

* VNet-naam: TestVNet1
* Adresruimte: 10.11.0.0/16
  * Subnetnaam: FrontEnd
  * Subnetadresbereik: 10.11.0.0/24
* Resourcegroep: TestRG1
* Locatie: VS - oost
* Adresruimte: 10.12.0.0/16
  * Subnetnaam: BackEnd
  * Subnetadresbereik: 10.12.0.0/24
* De naam van de gateway-Subnet: GatewaySubnet (dit wordt automatisch doorvoeren in Hallo-portal)
  * Adresbereik gatewaysubnet: 10.11.255.0/27
* DNS-Server: Hallo IP-adres van uw DNS-Server gebruiken
* Gatewaynaam van het virtuele netwerk: TestVNet1GW
* Gatewaytype: VPN
* VPN-type: op route gebaseerd
* SKU: Selecteer Hallo gewenste toouse Gateway-SKU
* Naam van openbare IP-adres: TestVNet1GWIP
* Verbindingswaarden:
  * Naam: TestVNet1toTestVNet4
  * Gedeelde sleutel: U kunt de gedeelde sleutel Hallo zelf maken. In dit voorbeeld gebruiken we abc123. Hallo-belangrijkste is dat bij het maken van verbinding tussen VNets Hallo HALLO hallo-waarde moet overeenkomen.

**Waarden voor TestVNet4:**

* VNet-naam: TestVNet4
* Adresruimte: 10.41.0.0/16
  * Subnetnaam: FrontEnd
  * Subnetadresbereik: 10.41.0.0/24
* Resourcegroep: TestRG1
* Locatie: VS - west
* Adresruimte: 10.42.0.0/16
  * Subnetnaam: BackEnd
  * Subnetadresbereik: 10.42.0.0/24
* De naam GatewaySubnet: GatewaySubnet (dit wordt automatisch doorvoeren in Hallo-portal)
  * Adresbereik GatewaySubnet: 10.41.255.0/27
* DNS-Server: Hallo IP-adres van uw DNS-Server gebruiken
* Gatewaynaam van het virtuele netwerk: TestVNet4GW
* Gatewaytype: VPN
* VPN-type: op route gebaseerd
* SKU: Selecteer Hallo gewenste toouse Gateway-SKU
* Naam van openbare IP-adres: TestVNet4GWIP
* Verbindingswaarden:
  * Naam: TestVNet4toTestVNet1
  * Gedeelde sleutel: U kunt de gedeelde sleutel Hallo zelf maken. In dit voorbeeld gebruiken we abc123. Hallo-belangrijkste is dat bij het maken van verbinding tussen VNets Hallo HALLO hallo-waarde moet overeenkomen.

## <a name="CreatVNet"></a>1. TestVNet1 maken en configureren
Als u al een VNet hebt, controleert u of Hallo instellingen compatibel zijn met uw VPN-gateway-ontwerp. Wat aandachtiger tooany subnetten die met andere netwerken overlappen. Als u overlappende subnetten hebt, werkt de verbinding mogelijk niet goed. Als uw VNet is geconfigureerd met de juiste instellingen hello, kunt u beginnen met Hallo stappen in Hallo [een DNS-server opgeven](#dns) sectie.

### <a name="toocreate-a-virtual-network"></a>toocreate een virtueel netwerk
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. Extra adresruimte toevoegen en subnetten maken
Wanneer het VNet is gemaakt, kunt u er extra adresruimte en subnetten aan toevoegen.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. Een gatewaysubnet maken
Voordat u verbinding maakt met uw virtuele netwerkgateway tooa, moet u eerst toocreate hello gatewaysubnet Hallo virtueel netwerk toowhich u tooconnect wilt. Indien mogelijk is het beste toocreate een gatewaysubnet met een CIDR-blok van/28 of /27 in volgorde tooprovide voldoende IP-adressen tooaccommodate aanvullende toekomstige configuratievereisten.

Als u deze configuratie bij wijze van oefening maakt, raadpleeg dan toothese [voorbeeldinstellingen](#values) bij het maken van het gatewaysubnet.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>een gatewaysubnet toocreate
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. Een DNS-server opgeven (optioneel)
DNS is niet vereist voor VNet-VNet-verbindingen. Als u naamomzetting toohave voor resources die geïmplementeerd tooyour virtueel netwerk zijn wilt, moet u een DNS-server opgeven. Deze instelling kunt u opgeven Hallo DNS-server wilt u toouse voor naamomzetting voor dit virtuele netwerk. Hierdoor wordt geen DNS-server aangemaakt.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. De gateway van een virtueel netwerk maken
In deze stap maakt u de virtuele netwerkgateway Hallo voor uw VNet. Maken van een gateway kunt vaak 45 minuten of langer duren, afhankelijk van de geselecteerde Hallo-gateway SKU. Als u deze configuratie bij wijze van oefening maakt, kunt u verwijzen toohello [voorbeeldinstellingen](#values).

### <a name="toocreate-a-virtual-network-gateway"></a>een virtuele netwerkgateway toocreate
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. TestVNet4 maken en configureren
Wanneer u TestVNet1 hebt geconfigureerd, kunt u de TestVNet4 maken door Hallo vorige stappen, waarbij Hallo waarden vervangt door die van TestVNet4 te herhalen. U hoeft niet toowait tot Hallo virtuele netwerkgateway voor TestVNet1 maken voordat u configureert TestVNet4 is voltooid. Als u uw eigen waarden gebruikt, ervoor zorgen dat Hallo adresruimten elkaar niet overlappen met een van de Hallo VNets die u wilt dat tooconnect aan.

## <a name="TestVNet1Connection"></a>7. Hallo TestVNet1 verbinding configureren
Wanneer de virtuele netwerkgateways Hallo voor TestVNet1 en TestVNet4 hebt voltooid, kunt u het virtuele netwerk gatewayverbindingen. In deze sectie maakt u een verbinding van VNet1 tooVNet4. Deze procedure werkt alleen voor VNets in Hallo hetzelfde abonnement. Als uw vnet's zich in verschillende abonnementen behoren, moet u PowerShell toomake Hallo verbinding gebruiken. Zie Hallo [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) artikel.

1. In **alle resources**, gaat u de virtuele netwerkgateway toohello voor uw VNet. Bijvoorbeeld **TestVNet1GW**. Klik op **TestVNet1GW** tooopen Hallo virtueel netwerk gateway blade.
   
    ![Blade Verbindingen](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Blade Verbindingen")
2. Klik op **+ toevoegen** tooopen hello **verbinding toevoegen** blade.
3. Op Hallo **verbinding toevoegen** blade in het veld Naam hello, typ een naam voor de verbinding. Bijvoorbeeld **TestVNet1toTestVNet4**.
   
    ![Verbindingsnaam](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Verbindingsnaam")
4. Voor **Verbindingstype** Selecteer **VNet-naar-VNet** uit Hallo vervolgkeuzelijst.
5. Hallo **eerste virtuele netwerkgateway** veldwaarde wordt automatisch ingevuld omdat u deze verbinding vanuit Hallo virtuele netwerkgateway opgegeven maakt.
6. Hallo **tweede virtuele netwerkgateway** veld is de virtuele netwerkgateway Hallo Hallo VNet dat u toocreate een verbinding wilt. Klik op **een andere virtuele netwerkgateway kiezen** tooopen hello **de virtuele netwerkgateway kiezen** blade.
   
    ![Verbinding toevoegen](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Een verbinding toevoegen")
7. Weergave Hallo virtuele netwerkgateways die op deze blade worden weergegeven. U ziet dat er alleen virtuele netwerkgateways worden vermeld die binnen uw abonnement vallen. Als u tooconnect tooa virtuele netwerkgateway die zich niet in uw abonnement wilt, gebruik Hallo [PowerShell artikel](vpn-gateway-vnet-vnet-rm-ps.md). 
8. Klik op Hallo virtuele netwerkgateway die u wilt dat tooconnect aan.
9. In Hallo **gedeelde sleutel** veld, typt u een gedeelde sleutel voor de verbinding. U kunt deze sleutel ook zelf maken of genereren. In een site-naar-site-verbinding, zou Hallo-sleutel die u worden exact Hallo hetzelfde zijn voor uw on-premises-apparaat en de verbinding van uw virtuele netwerk-gateway. Hallo concept is vergelijkbaar hier, behalve dat in plaats van te maken van verbinding tooa VPN-apparaat, u verbinding maakt tooanother virtuele netwerkgateway.
   
    ![Gedeelde sleutel](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Gedeelde sleutel")
10. Klik op **OK** op Hallo onderaan Hallo blade toosave worden uw wijzigingen.

## <a name="TestVNet4Connection"></a>8. Hallo TestVNet4-verbinding configureren
Maak vervolgens een verbinding van TestVNet4 tooTestVNet1. Gebruik Hallo dezelfde methode die u hebt toocreate Hallo verbinding van TestVNet1 tooTestVNet4 gebruikt. Zorg ervoor dat u Hallo dezelfde gedeelde sleutel.

## <a name="VerifyConnection"></a>9. De verbinding controleren
Hallo-verbinding controleren. Voor elke virtuele netwerkgateway Hallo te volgen:

1. Hallo-blade voor de virtuele netwerkgateway Hallo vinden. Bijvoorbeeld **TestVNet4GW**. 
2. Klik op de blade van Hallo virtueel netwerk gateway **verbindingen** tooview Hallo verbindingen blade voor de virtuele netwerkgateway Hallo.

Hallo verbindingen bekijken en Hallo status controleren. Nadat het Hallo-verbinding wordt gemaakt, ziet u **geslaagd** en **verbonden** zoals Hallo statuswaarden.

![Geslaagd](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Geslaagd")

U kunt dubbelklikken op elke verbinding afzonderlijk tooview meer informatie over Hallo-verbinding.

![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")

## <a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet
Hallo Veelgestelde vragen over de details voor meer informatie over VNet-naar-VNet-verbindingen weergeven.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Volgende stappen
Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie Hallo [documentatie Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.
