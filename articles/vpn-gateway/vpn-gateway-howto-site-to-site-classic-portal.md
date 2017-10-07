---
title: 'Verbinding maken met uw lokale netwerk tooan virtuele Azure-netwerk: Site-naar-Site-VPN (klassiek): Portal | Microsoft Docs'
description: Stappen toocreate een IPsec-verbinding van uw on-premises netwerk tooan virtuele Azure-netwerk via openbaar Internet Hallo. Deze stappen kunt u een cross-premises Site-naar-Site VPN-gatewayverbinding maken met de Hallo-portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Een Site-naar-Site verbinding maken met hello Azure-portal (klassiek)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Dit artikel laat zien hoe toouse hello Azure portal toocreate een Site-naar-Site VPN-gatewayverbinding vanuit uw lokale netwerk toohello VNet. Hallo stappen in dit artikel van toepassing toohello klassieke implementatiemodel. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel. Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit. Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.

![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Voordat u begint

Controleer of dat u criteria na voorhand Hallo hebt voldaan:

* Controleer of de gewenste toowork Hallo klassieke implementatiemodel. Als u toowork Hallo Resource Manager-implementatiemodel wilt, Zie [maken van een Site-naar-Site-verbinding (Resource Manager)](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Indien mogelijk wordt u aangeraden dat u Hallo Resource Manager-implementatiemodel.
* Zorg ervoor dat u hebt een compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze. Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.
* Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt. Dit IP-adres kan zich niet achter een NAT bevinden.
* Als u niet bekend bent met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie, moet u toocoordinate met iemand die deze details voor u verstrekken kan. Wanneer u deze configuratie maakt, moet u Hallo IP-bereik adresvoorvoegsels Azure routeert tooyour on-premises locatie. Geen van de subnetten Hallo van uw on-premises netwerk kunnen via lap met Hallo virtueel netwerksubnetten die u wilt dat tooconnect om te.
* Op dit moment PowerShell is vereist toospecify Hallo gedeelde sleutel en Hallo VPN-gatewayverbinding maken. Installeer de nieuwste versie Hallo Hallo Azure Service Management (SM) PowerShell-cmdlets. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). Als u werkt met PowerShell voor deze configuratie, zorg er dan voor dat u de bewerkingen uitvoert als beheerder. 

### <a name="values"></a>Voorbeeld van configuratiewaarden voor deze oefening

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
* **DNS-server:** 10.11.0.3 (optioneel voor deze oefening)
* **Lokale sitenaam:** Site2
* **Client-adresruimte:** Hallo-adresruimte die bevindt zich op uw on-premises site.

## <a name="CreatVNet"></a>1. Een virtueel netwerk maken

Wanneer u een virtueel netwerk toouse voor een S2S-verbinding maakt, moet u ervoor dat Hallo adresruimten die u opgeeft niet overlappen met een van de Hallo client adresruimten voor Hallo lokale sites die u wilt dat tooconnect naar toomake. Als u overlappende subnetten hebt, werkt de verbinding mogelijk niet goed.

* Als u al een VNet hebt, controleert u of Hallo instellingen compatibel zijn met uw VPN-gateway-ontwerp. Wat aandachtiger tooany subnetten die met andere netwerken overlappen. 

* Als u nog geen virtueel netwerk hebt, maakt u er een. De schermafbeeldingen dienen alleen als voorbeeld. Ervoor tooreplace Hallo waarden door uw eigen worden.

### <a name="toocreate-a-virtual-network"></a>toocreate een virtueel netwerk

1. Navigeer via een browser toohello [Azure-portal](http://portal.azure.com) en, indien nodig, meld u aan met uw Azure-account.
2. Klik op **+**. In Hallo **zoeken Hallo marketplace** veld, typt u 'Virtueel netwerk'. Zoek **virtueel netwerk** Hallo geretourneerde lijst en klik op tooopen hello **virtueel netwerk** pagina.

  ![Pagina voor zoeken van virtueel netwerk](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Aan de onderkant Hallo van Hallo virtueel netwerk pagina van Hallo **een implementatiemodel selecteren** vervolgkeuzelijst, selecteer **klassieke**, en klik vervolgens op **maken**.

  ![Een implementatiemodel selecteren](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. Op Hallo **maken van virtuele network(classic)** pagina, Hallo VNet-instellingen configureren. Voeg op deze pagina de eerste adresruimte en één adresbereik voor het subnet toe. Nadat u Hallo VNet maken, kunt u teruggaan en aanvullende subnets en adresruimten toevoegen.

  ![Pagina Virtueel netwerk maken](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Pagina Virtueel netwerk maken")
5. Controleer of deze Hallo **abonnement** Hallo correct is. U kunt abonnementen wijzigen met behulp van Hallo vervolgkeuzelijst.
6. Klik op **Resourcegroep** en selecteer een bestaande resourcegroep of maak een nieuwe resourcegroep door een naam in te voeren. Zie [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md#resource-groups) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.
7. Selecteer vervolgens Hallo **locatie** instellingen voor uw VNet. Hallo locatie bepaalt waar Hallo-resources die u toothis VNet implementeert blijven staan.
8. Als u uw VNet gemakkelijk op Hallo dashboard toobe kunnen toofind wilt, selecteer **pincode toodashboard**. Klik op **maken** toocreate uw VNet.

  ![Pincode toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "pincode toodashboard")
9. Wanneer u op 'Maken', verschijnt een tegel op Hallo dashboard die overeenkomt met Hallo voortgang van uw VNet. Hallo tegel wijzigingen als Hallo VNet wordt gemaakt.

  ![Tegel Virtueel netwerk maken](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Tegel Virtueel netwerk maken")

Nadat het virtuele netwerk is gemaakt, ziet u **gemaakt** vermeld onder **Status** op Hallo netwerken pagina in Hallo klassieke Azure-portal.

## <a name="additionaladdress"></a>2. Extra adresruimte toevoegen

Nadat u het virtuele netwerk hebt gemaakt, kunt u extra adresruimte toevoegen. Toevoegen van extra adresruimte is niet een vereist onderdeel van een S2S-configuratie, maar als u meerdere adresruimten vereist, gebruikt Hallo stappen te volgen:

1. Hallo virtuele netwerken niet vinden in het Hallo-portal.
2. Op de pagina voor het virtuele netwerk, onder Hallo Hallo **instellingen** sectie, klikt u op **adresruimte**.
3. Klik op de pagina van het Hallo Address space **+ toevoegen** en voert u extra adresruimte.

## <a name="dns"></a>3. Een DNS-server opgeven

DNS-instellingen zijn geen vereist onderdeel van een S2S-configuratie, maar een DNS is nodig voor naamomzetting. Het opgeven van een waarde betekent niet dat er een nieuwe DNS-server wordt gemaakt. Hallo moet DNS-server IP-adres dat u opgeeft een DNS-server die u kunt Hallo namen omzetten voor Hallo resources die u verbinding maakt. Voor instellingen van Hallo voorbeeld hebben we een particulier IP-adres gebruikt. Hallo IP-adres we gebruiken is waarschijnlijk niet Hallo IP-adres van uw DNS-server. Worden toouse ervoor dat uw eigen waarden.

Nadat u het virtuele netwerk hebt gemaakt, kunt u Hallo IP-adres van een DNS-server toohandle naamomzetting kunt toevoegen. Hallo-instellingen voor het virtuele netwerk te openen, klikt u op de DNS-servers en Hallo IP-adres van Hallo DNS-server dat u voor naamomzetting toouse wilt toevoegen.

1. Hallo virtuele netwerken niet vinden in het Hallo-portal.
2. Op de pagina voor het virtuele netwerk, onder Hallo Hallo **instellingen** sectie, klikt u op **DNS-servers**.
3. Voeg een DNS-server toe.
4. toosave uw instellingen, klikt u op **opslaan** bovenaan Hallo Hallo pagina.

## <a name="localsite"></a>4. Hallo lokale site configureren

de lokale site Hallo verwijst doorgaans tooyour on-premises locatie. Het bevat Hallo IP-adres van Hallo VPN-apparaat toowhich u maakt een verbinding en Hallo IP-adresbereiken die worden doorgestuurd via Hallo VPN-gateway toohello VPN-apparaat.

1. Navigeer in Hallo portal toohello virtueel netwerk waarvoor u een gateway toocreate wilt.
2. Op de pagina voor het virtuele netwerk, klikt u op Hallo Hallo **overzicht** pagina in de sectie voor Hallo VPN-verbindingen, klikt u op **Gateway** tooopen hello **nieuwe VPN-verbinding** pagina.

  ![Klik op instellingen van de gateway tooconfigure](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "klikt u op tooconfigure gateway-instellingen")
3. Op Hallo **nieuwe VPN-verbinding** pagina **Site-naar-site**.
4. Klik op **lokale site - Configureer de vereiste instellingen** tooopen hello **lokale site** pagina. Hallo-instellingen configureren en klik vervolgens op **OK** toosave Hallo instellingen.
  - **Naam:** maken een naam voor uw lokale site toomake gemakkelijk voor u tooidentify.
  - **IP-adres van VPN-gateway:** dit openbare IP-adres van Hallo VPN-apparaat voor uw on-premises netwerk Hallo is. Hallo VPN-apparaat vereist een openbaar IPv4-IP-adres. Geef een geldig openbaar IP-adres voor VPN-apparaat toowhich gewenste tooconnect Hallo. Het mag zich niet achter NAT en toobe die door Azure bereikbaar is. Als u niet weet Hallo IP-adres van uw VPN-apparaat, die u kunt altijd plaatsen in een tijdelijke aanduidingswaarde (mits het Hallo-indeling van een geldig openbaar IP-adres) en later wijzigen.
  - **Client-adresruimte:** lijst Hallo IP-adresbereiken die u wilt dat gerouteerd toohello lokale on-premises netwerk via deze gateway. U kunt meerdere adresruimtebereiken toevoegen. Zorg ervoor dat Hallo bereiken die u hier opgeeft niet overlappen met bereiken van andere uw virtuele netwerk maakt verbinding met netwerken of met Hallo-adresbereiken van het virtuele netwerk Hallo zelf.

  ![Lokale site](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Lokale site configureren")

## <a name="gatewaysubnet"></a>5. Hallo gatewaysubnet configureren

U moet een gatewaysubnet maken voor de VPN-gateway. gatewaysubnet Hallo bevat Hallo IP-adressen die gebruikmaken van Hallo VPN-gatewayservices.

1. Op Hallo **nieuwe VPN-verbinding** pagina, selecteer Hallo selectievakje **gateway onmiddellijk maken**. Hallo optionele gateway 'configuration' pagina wordt weergegeven. Als u geen Hallo selectievakje selecteert, ziet u geen Hallo pagina tooconfigure Hallo gateway-subnet.

  ![Gatewayconfiguratie - subnet, grootte, routingtype](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Gatewayconfiguratie - subnet, grootte, routingtype")
2. Hallo tooopen **gatewayconfiguratie** pagina, klikt u op **optionele gatewayconfiguratie - Subnet, grootte en routeringstype**.
3. Op Hallo **gatewayconfiguratie** pagina, klikt u op **Subnet - vereiste instellingen configureren** tooopen hello **subnet toevoegen** pagina.

  ![Gatewayconfiguratie - gatewaysubnet](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "gatewayconfiguratie - gatewaysubnet")
4. Op Hallo **subnet toevoegen** pagina, Hallo gatewaysubnet toevoegen. Hallo grootte van gatewaysubnet Hallo die u opgeeft, afhankelijk Hallo VPN-gateway-configuratie die u toocreate wilt. Het is mogelijk toocreate een gatewaysubnet van slechts/29, wordt u aangeraden/27 of /28 te gebruiken. U maakt dan een groter subnet dat meer adressen bevat. Met behulp van een groter gatewaysubnet kunt voldoende IP-adressen tooaccommodate mogelijke toekomstige configuraties.

  ![Gatewaysubnet toevoegen](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Gatewaysubnet toevoegen")

## <a name="sku"></a>6. Geef hello SKU- en VPN-type

1. Selecteer Hallo gateway **grootte**. Dit is Hallo gateway-SKU dat u toocreate uw virtuele netwerkgateway. In de portal Hallo Hallo 'Standaard SKU' = **Basic**. Klassieke VPN-gateways gebruiken Hallo oude (verouderde) gateway-SKU's. Zie voor meer informatie over Hallo verouderde gateway-SKU's [werken met virtuele netwerkgateway SKU's (oude SKU's)](vpn-gateway-about-skus-legacy.md).

  ![SKUL- en VPN-type selecteren](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "SKU- en VPN-type selecteren")
2. Selecteer Hallo **Type routering** voor uw gateway. Dit is ook bekend als Hallo VPN-type. Het is belangrijk tooselect Hallo juiste Gatewaytype omdat u Hallo-gateway kan niet van een type tooanother converteren. Uw VPN-apparaat moet compatibel zijn met Hallo routering dat die u selecteert. Zie [Over VPN-gatewayinstellingen](vpn-gateway-about-vpn-gateway-settings.md#vpntype) voor meer informatie over VPN-typen. Mogelijk ziet u artikelen too'RouteBased verwijst ' en 'PolicyBased' VPN typen. ' Dynamische 'komt overeen too'RouteBased', en 'Statische' komt overeen met 'PolicyBased'.
3. Klik op **OK** toosave Hallo instellingen.
4. Op Hallo **nieuwe VPN-verbinding** pagina, klikt u op **OK** onderaan Hallo Hallo pagina toobegin maken van uw virtuele netwerkgateway. Afhankelijk van Hallo SKU die u selecteert, kunnen er too45 minuten toocreate een virtuele netwerkgateway.

## <a name="vpndevice"></a>7. Uw VPN-apparaat configureren

Site-naar-Site-verbindingen tooan on-premises netwerk een VPN-apparaat vereist. In deze stap configureert u het VPN-apparaat. Bij het configureren van uw VPN-apparaat, moet u de volgende Hallo:

- Een gedeelde sleutel. Dit is Hallo dezelfde gedeelde sleutel die u opgeeft bij het maken van uw Site-naar-Site VPN-verbinding. In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel. Het is raadzaam dat u een complexere sleutel toouse genereert.
- Hallo openbare IP-adres van uw virtuele netwerkgateway. U kunt het openbare IP-adres Hallo weergeven met behulp van hello Azure-portal, PowerShell of CLI.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Hallo verbinding maken
In deze stap maakt u Hallo gedeelde sleutel instellen en Hallo verbinding maken. Hallo Hallo-sleutel die u instelt is moet dezelfde sleutel die is gebruikt in de configuratie van uw VPN-apparaat.

> [!NOTE]
> Deze stap is momenteel niet beschikbaar in hello Azure-portal. U moet Hallo Service Management (SM) versie van hello Azure PowerShell-cmdlets gebruiken.
>

### <a name="step-1-connect-tooyour-azure-account"></a>Step 1. Verbinding maken met tooyour Azure-account

1. Open de PowerShell-console met verhoogde rechten en tooyour-account koppelen. Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:

  ```powershell
  Add-AzureAccount
  ```
2. Controleer de abonnementen Hallo voor Hallo-account.

  ```powershell
  Get-AzureSubscription
  ```
3. Als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u wilt dat toouse.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>Stap 2. Hallo gedeelde sleutel instellen en Hallo verbinding maken

Als u werkt met PowerShell en Hallo klassieke implementatiemodel, zijn soms Hallo namen van bronnen in Hallo-portal niet Hallo namen hello Azure toosee verwacht wanneer u PowerShell. Hallo volgende stappen uit te exporteren Hallo netwerk bestand tooobtain Hallo exacte configuratiewaarden voor Hallo namen.

1. Maak een map op uw computer en vervolgens exporteren Hallo configuration file toohello netwerkmap. In dit voorbeeld is Hallo netwerk configuratiebestand geëxporteerde tooC:\AzureNet.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Hallo netwerk-configuratiebestand met een xml-editor te openen en controleer Hallo waarden voor 'name LocalNetworkSite' en 'VirtualNetworkSite name'. Wijzig Hallo voorbeeld tooreflect Hallo waarden die u nodig hebt. Bij het opgeven van een naam die spaties bevat, gebruikt u enkele aanhalingstekens rond het Hallo-waarde.

3. Hallo gedeelde sleutel instellen en Hallo verbinding maken. Hallo '-SharedKey' is een waarde die u genereren en opgeven. In voorbeeld Hallo we 'abc123' gebruikt, maar u kunt genereren (en moeten) gebruikmaken van iets meer complexe. Hallo belangrijke dingen die u hier opgeeft, Hallo-waarde is moet Hallo die dezelfde waarde die u hebt opgegeven bij het configureren van uw VPN-apparaat.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Wanneer Hallo verbinding wordt gemaakt, is het resultaat Hallo: **Status: geslaagd**.

## <a name="verify"></a>9. De verbinding controleren

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Als u verbindingsproblemen ondervindt, raadpleegt u Hallo **oplossen** sectie van Hallo inhoudsopgave in het linkerdeelvenster Hallo.

## <a name="reset"></a>Hoe tooreset een VPN-gateway

Het opnieuw instellen van een Azure VPN-gateway is handig als u cross-premises VPN-connectiviteit verliest in een of meer Site-to-Site VPN-tunnels. In dit geval uw on-premises VPN-apparaten zijn alle naar behoren werkt, maar er kan geen tooestablish IPsec-tunnels met hello Azure VPN-gateways zijn. Zie [Een VPN-gateway opnieuw instellen](vpn-gateway-resetgw-classic.md) voor de stappen.

## <a name="changesku"></a>Hoe toochange een gateway-SKU

Voor Hallo toochange een gateway-SKU stappen, Zie [vergroten of verkleinen van een gateway-SKU](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Volgende stappen

* Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.
* Zie [Informatie over geforceerde tunneling](vpn-gateway-about-forced-tunneling.md) voor meer informatie over geforceerde tunneling.