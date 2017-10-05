---
title: 'Een VPN-Gateway configureren: klassieke portal: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij het configureren van het virtuele netwerk VPN-gateway en het wijzigen van een gateway routering VPN-type. Deze stappen van toepassing op het klassieke implementatiemodel en de klassieke portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 2ea4e6bb86b1ba6f7b501b193d0713d3901457af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-vpn-gateway-in-the-classic-portal"></a>Een VPN-gateway in de klassieke portal configureren 
Als u maken van een beveiligde cross-premises-verbinding tussen Azure en uw on-premises locatie wilt, moet u de gateway van een virtueel netwerk maken. Een VPN-gateway is een specifieke type van de virtuele netwerkgateway. In het klassieke implementatiemodel, een VPN-gateway worden twee soorten VPN-routering: statisch of dynamisch. Het VPN-type dat u kiest, is afhankelijk van uw ontwerpplan netwerk en de on-premises VPN-apparaat dat u wilt gebruiken. Zie voor meer informatie over VPN-apparaten [over VPN-apparaten](vpn-gateway-about-vpn-devices.md).

**Over Azure-implementatiemodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Configuratie-overzicht
De volgende stappen doorlopen voor het configureren van uw VPN-gateway in de klassieke portal. Deze stappen van toepassing op gateways voor virtuele netwerken die zijn gemaakt met het klassieke implementatiemodel. Niet alle configuratie-instellingen voor gateways zijn momenteel beschikbaar in de Azure-portal. Wanneer ze zijn, wordt er een nieuwe reeks instructies die betrekking hebben op de Azure portal maken.

### <a name="before-you-begin"></a>Voordat u begint
Voordat u uw gateway configureert, moet u eerst het virtuele netwerk maken. Zie voor stappen voor het maken van een virtueel netwerk voor cross-premises connectiviteit [een virtueel netwerk configureren met een site-naar-site VPN-verbinding](vpn-gateway-site-to-site-create.md), of [een virtueel netwerk configureren met een punt-naar-site VPN-verbinding](vpn-gateway-point-to-site-create.md). Vervolgens gebruikt u de volgende stappen uit voor het configureren van de VPN-gateway en verzamelen van informatie die u nodig hebt om uw VPN-apparaat te configureren. 

Als u al een VPN-gateway hebt en u wilt wijzigen van het VPN-routering type, Zie [het wijzigen van het VPN-routering type voor uw gateway](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>Een VPN-gateway maken
1. In de [klassieke Azure-portal](https://manage.windowsazure.com)op de **netwerken** pagina, Controleer of de statuskolom voor het virtuele netwerk **gemaakt**.
2. In de **naam** kolom, klikt u op de naam van het virtuele netwerk.
3. Op de **Dashboard** pagina, zoals u ziet dat dit VNet geen gateway nog geconfigureerd. U ziet deze status als u de stappen voor het configureren van uw gateway doorlopen.

![Gateway is niet gemaakt](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

Aan de onderkant van de pagina, klik dan op **Gateway maken**. U kunt een selecteren *statische routering* of *dynamische routering*. Het VPN-routering dat u selecteert, is afhankelijk van enkele factoren. Bijvoorbeeld, wat uw VPN-apparaat ondersteunt en of u moet punt-naar-site-verbindingen ondersteunen. Controleer [over VPN-apparaten voor verbinding met het virtuele netwerk](vpn-gateway-about-vpn-devices.md) om te controleren of de VPN-routering type die u nodig hebt. Zodra de gateway is gemaakt, kunt u niet wijzigen tussen VPN-routering gatewaytypen zonder te verwijderen en opnieuw maken van de gateway. Wanneer het systeem wordt u gevraagd te bevestigen dat u wilt dat de gateway is gemaakt, klikt u op **Ja**.

![Routeringstype van de VPN-gateway](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Als uw gateway maakt, ziet de afbeelding gateway op de pagina wordt gewijzigd in geel en geeft aan dat *Gateway maken*. Duurt 45 minuten duren voordat de gateway te maken. Wacht totdat de gateway voltooid is voordat u kunt verder gaan met andere configuratie-instellingen.

![Gateway maken](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Wanneer de gateway verandert in *verbinding maakt met*, kunt u de informatie die u nodig hebt voor uw VPN-apparaat verzamelen.

![Gateway verbinding](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Site-naar-site-verbindingen

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>Step 1. Informatie verzamelen voor de configuratie van uw VPN-apparaat
Als u een Site-naar-Site-verbinding maakt nadat de gateway is gemaakt, informatie verzamelen voor de configuratie van uw VPN-apparaat. Deze informatie bevindt zich op de **Dashboard** pagina voor het virtuele netwerk:

1. **IP-adres van gateway -** kunt u het IP-adres vinden op de **Dashboard** pagina. Het niet mogelijk om te zien tot nadat uw gateway maken is voltooid.
2. **Gedeelde sleutel -** klikt u op **sleutel beheren** aan de onderkant van het scherm. Klik op het pictogram naast de sleutel tot het naar het Klembord kopiëren en plakken en opslaan van de sleutel. Deze knop werkt alleen als er één S2S-VPN-tunnel. Als u meerdere S2S VPN-tunnels hebt, gebruikt u de *ophalen Virtual Network Gateway gedeelde sleutel* API of PowerShell-cmdlet.

![Sleutel beheren](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>Stap 2.  Uw VPN-apparaat configureren
Voor site-naar-site-verbindingen met een on-premises netwerk is een VPN-apparaat vereist. Hoewel we niet voor alle VPN-apparaten de configuratiestappen geven, kan de informatie van de volgende koppelingen toch nuttig zijn:

- Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten. 
- Zie [Gevalideerde VPN-apparaten](vpn-gateway-about-vpn-devices.md#devicetable) voor koppelingen naar configuratie-instellingen. Deze koppelingen worden op basis van 'best effort' aangeboden. Het is altijd verstandig om de actuele configuratie-informatie op te vragen bij de fabrikant van uw apparaat.
- Zie [Bewerkingsvoorbeelden](vpn-gateway-about-vpn-devices.md#editing) voor voorbeelden van het bewerken van de apparaatconfiguratie.
- Zie [Parameters](vpn-gateway-about-vpn-devices.md#ipsec) voor de IPsec/IKE-parameters.
- Controleer voordat u uw VPN-apparaat configureert of er [bekende compatibiliteitsproblemen](vpn-gateway-about-vpn-devices.md#known) zijn met het VPN-apparaat dat u wilt gebruiken.

Bij de configuratie van uw VPN-apparaat hebt u het volgende nodig:

- Het openbare IP-adres van de gateway van uw virtuele netwerk. U vindt dit adres op de blade **Overzicht** voor het virtuele netwerk.
- Een gedeelde sleutel. Dit is dezelfde gedeelde sleutel die u opgeeft wanneer u uw site-naar-site-VPN-verbinding maakt. In onze voorbeelden gebruiken we een zeer eenvoudige gedeelde sleutel. We raden u aan een complexere sleutel te gebruiken.

Nadat de VPN-apparaat is geconfigureerd, kunt u uw bijgewerkte verbindingsinformatie weergeven op de pagina Dashboard voor uw VNet.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>Stap 3. Controleer of uw lokale netwerkbereiken en IP-adres van VPN-gateway
#### <a name="verify-your-vpn-gateway-ip-address"></a>Controleer of het IP-adres van uw VPN-gateway
Voor de gateway verbinding, het IP-adres voor uw VPN-apparaat moet correct zijn geconfigureerd voor het lokale netwerk die u hebt opgegeven voor uw cross-premises-configuratie. Dit is normaal gesproken geconfigureerd tijdens het configuratieproces van site-naar-site. Als u deze lokale netwerk eerder met een ander apparaat gebruikt of het IP-adres voor deze lokale netwerk is gewijzigd, echter de instellingen voor het opgeven van de juiste IP-adres Gateway bewerken.

1. Om te controleren of het IP-adres van uw gateway, klikt u op **netwerken** op de portal linkerdeelvenster en selecteer vervolgens **lokale netwerken** boven aan de pagina. Hier ziet u het VPN-Gateway-adres voor elke lokale netwerk dat u hebt gemaakt. Het IP-adres bewerken, selecteert u het VNet en klikt u op **bewerken** aan de onderkant van de pagina.
2. Op de **Geef details op uw lokale netwerk** pagina, het IP-adres bewerken en klik op de pijl volgende aan de onderkant van de pagina.
3. Op de **opgeven van de adresruimte** pagina, klikt u op het vinkje in de rechterbenedenhoek uw instellingen op te slaan.

#### <a name="verify-the-address-ranges-for-your-local-networks"></a>Controleer of de adresbereiken voor uw lokale netwerken
Voor de juiste verkeer via de gateway van uw on-premises locatie, moet u controleren dat elk IP-adresbereik is opgegeven. Elk bereik moet worden vermeld in uw Azure **lokale netwerken** configuratie. Dit kan een taak erg groot zijn afhankelijk van de netwerkconfiguratie van uw on-premises locatie. Verkeer dat is gekoppeld aan een IP-adres dat is opgenomen in de vermelde bereiken worden verzonden via de VPN-gateway van virtueel netwerk. De bereiken die u opgeeft, hoeft te worden persoonlijke bereiken, hoewel u wilt controleren of dat uw on-premises configuratie het binnenkomende verkeer kan ontvangen.

Als u wilt toevoegen of bewerken van de bereiken voor een lokaal netwerk, gebruikt u de volgende stappen uit:

1. Als u wilt bewerken in de IP-adresbereiken voor een lokaal netwerk, klikt u op **netwerken** op de portal linkerdeelvenster en selecteer vervolgens **lokale netwerken** boven aan de pagina. In de portal de eenvoudigste manier om weer te geven van de bereiken die u hebt opgegeven is op de **bewerken** pagina. De bereiken, selecteert u het VNet en klikt u op **bewerken** aan de onderkant van de pagina.
2. Op de **Geef details op uw lokale netwerk** pagina, geen wijzigingen aanbrengt. Klik op de pijl volgende aan de onderkant van de pagina.
3. Op de **opgeven van de adresruimte** maken van de adresruimtewijziigingen voor uw netwerk. Klik vervolgens op het vinkje om de configuratie op te slaan.

## <a name="how-to-view-gateway-traffic"></a>Gateway-verkeer weergeven
U kunt de gateway en de gateway-verkeer van het virtuele netwerk weergeven **Dashboard** pagina.

Op de **Dashboard** pagina kunt u het volgende bekijken:

* De hoeveelheid gegevens die via de gateway, zowel gegevens in en uit stroomt.
* De namen van de DNS-servers die zijn opgegeven voor het virtuele netwerk.
* De verbinding tussen uw gateway en uw VPN-apparaat.
* De gedeelde sleutel die wordt gebruikt voor het configureren van de gatewayverbinding met uw VPN-apparaat.

## <a name="how-to-change-the-vpn-routing-type-for-your-gateway"></a>Het VPN-routeringstype voor uw gateway wijzigen
Omdat sommige configuraties connectiviteit alleen beschikbaar voor bepaalde routering gatewaytypen zijn, merkt u dat u wilt wijzigen van de gateway routering VPN-type van een bestaande VPN-gateway. U wilt bijvoorbeeld punt-naar-site-verbinding toevoegen aan een bestaande site-naar-site-verbinding met een statische gateway. Punt-naar-site-verbindingen nodig een dynamische gateway. Dit betekent dat een P2S-verbinding configureren, moet u uw gateway routering VPN-type van statisch naar dynamisch wijzigen.

Als u wijzigen van een routeringstype voor VPN-gateway wilt, moet u de bestaande gateway verwijdert en vervolgens een nieuwe gateway maken met het nieuwe type routering. U hoeft niet te verwijderen van het gehele virtuele netwerk als de gateway routering type wilt wijzigen.

Voordat u uw gateway routering VPN-type wijzigt, moet u controleren of uw VPN-apparaat ondersteunt de routeringstype die u wilt gebruiken. Voor het downloaden van nieuwe routering configuratie samples en controleren van vereisten voor VPN-apparaten, Zie [over VPN-apparaten voor verbinding met het virtuele netwerk](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Wanneer u een VPN-gateway van virtueel netwerk verwijdert, wordt het VIP van de gateway uitgebracht. Wanneer u de gateway opnieuw maken, is een nieuwe VIP-adres toegewezen.
> 
> 

1. **Verwijder de bestaande VPN-gateway.**
   
    Op de **Dashboard** pagina voor het virtuele netwerk, navigeer naar de onderkant van de pagina en klik op **Gateway verwijderen**. Wacht totdat de melding dat de gateway is verwijderd. Nadat u hebt ontvangen de melding op het scherm dat uw gateway is verwijderd, kunt u een nieuwe gateway.
2. **Maak een nieuwe VPN-gateway.**
   
    Gebruik de procedure bovenaan de pagina voor het maken van een nieuwe gateway: [maken van een VPN-gateway](#create-a-vpn-gateway).

## <a name="next-steps"></a>Volgende stappen
U kunt virtuele machines toevoegen aan het virtuele netwerk. Zie [How to create a custom virtual machine](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (Een aangepaste virtuele machine maken).

Als u een punt-naar-site VPN-verbinding configureren wilt, Zie [een punt-naar-site VPN-verbinding configureren](vpn-gateway-point-to-site-create.md).

