---
title: 'Een VPN-Gateway configureren: klassieke portal: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij het configureren van het virtuele netwerk VPN-gateway en het wijzigen van een gateway routering VPN-type. Deze stappen gelden toohello classic deployment model en Hallo klassieke portal.
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
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>Een VPN-gateway configureren in de klassieke portal Hallo 
Als u een beveiligde cross-premises-verbinding tussen Azure en uw on-premises locatie toocreate wilt, moet u een virtuele netwerkgateway toocreate. Een VPN-gateway is een specifieke type van de virtuele netwerkgateway. In het klassieke implementatiemodel hello, een VPN-gateway worden twee soorten VPN-routering: statisch of dynamisch. Hallo VPN-type u kiest, is afhankelijk van uw ontwerpplan voor netwerk, zowel Hallo on-premises VPN-apparaat u wilt dat toouse. Zie voor meer informatie over VPN-apparaten [over VPN-apparaten](vpn-gateway-about-vpn-devices.md).

**Over Azure-implementatiemodellen**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Configuratie-overzicht
Hallo volgende stappen maakt u uw VPN-gateway configureren in de klassieke portal Hallo. Deze stappen gelden toogateways voor virtuele netwerken die zijn gemaakt met het klassieke implementatiemodel Hallo. Niet alle configuratie-instellingen voor gateways Hallo zijn momenteel leverbaar in hello Azure-portal. Wanneer ze zijn, maakt er een nieuwe reeks instructies die van toepassing toohello Azure-portal.

### <a name="before-you-begin"></a>Voordat u begint
Voordat u uw gateway configureert, moet u eerst toocreate het virtuele netwerk. Zie voor stappen toocreate een virtueel netwerk voor cross-premises connectiviteit, [een virtueel netwerk configureren met een site-naar-site VPN-verbinding](vpn-gateway-site-to-site-create.md), of [een virtueel netwerk configureren met een punt-naar-site VPN-verbinding](vpn-gateway-point-to-site-create.md). Vervolgens gebruiken hello te volgen stappen tooconfigure Hallo VPN-gateway en Hallo Verzamel u tooconfigure moet uw VPN-apparaat. 

Als u al een VPN-gateway hebt en u toochange Hallo VPN-routering type wilt, Zie [hoe toochange routering VPN-type voor uw gateway Hallo](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>Een VPN-gateway maken
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo **netwerken** pagina, controleer dan of die status Hallo kolom voor het virtuele netwerk is **gemaakt**.
2. In Hallo **naam** kolom, klik op Hallo-naam van het virtuele netwerk.
3. Op Hallo **Dashboard** pagina, zoals u ziet dat dit VNet geen gateway nog geconfigureerd. U ziet deze status terwijl u uw gateway Hallo stappen tooconfigure doorloopt.

![Gateway is niet gemaakt](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

Aan de onderkant van de Hallo van Hallo pagina, klik dan op **Gateway maken**. U kunt een selecteren *statische routering* of *dynamische routering*. Hallo VPN-routering dat u selecteert, is afhankelijk van enkele factoren. Bijvoorbeeld, wat uw VPN-apparaat ondersteunt en of u toosupport punt-naar-site-verbindingen nodig hebt. Controleer [over VPN-apparaten voor verbinding met het virtuele netwerk](vpn-gateway-about-vpn-devices.md) tooverify Hallo routering VPN-type die u nodig hebt. Zodra het Hallo-gateway is gemaakt, kunt u niet wijzigen tussen VPN-routering gatewaytypen zonder te verwijderen en opnieuw maken van Hallo-gateway. Wanneer hello wordt u gevraagd tooconfirm dat u wilt Hallo gateway is gemaakt, klikt u op **Ja**.

![Routeringstype van de VPN-gateway](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Als uw gateway maakt, merkt Hallo gateway afbeelding op pagina Hallo tooyellow verandert en geeft aan dat *Gateway maken*. Het kan Hallo-gateway toocreate too45 minuten duren. Wacht totdat het Hallo-gateway is voltooid voordat u kunt verder gaan met andere configuratie-instellingen.

![Gateway maken](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Wanneer de wijzigingen van de gateway te Hallo*verbinding maakt met*, kunt u Hallo-informatie die u nodig hebt voor uw VPN-apparaat verzamelen.

![Gateway verbinding](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Site-naar-site-verbindingen

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>Step 1. Informatie verzamelen voor de configuratie van uw VPN-apparaat
Als u een Site-naar-Site-verbinding maakt nadat Hallo gateway is gemaakt, informatie verzamelen voor de configuratie van uw VPN-apparaat. Deze informatie bevindt zich op Hallo **Dashboard** pagina voor het virtuele netwerk:

1. **IP-adres van gateway -** Hallo IP-adres kunt u vinden op Hallo **Dashboard** pagina. U kunt toosee deze pas na uw gateway is klaar met het maken niet.
2. **Gedeelde sleutel -** klikt u op **sleutel beheren** Hallo onder welkomstscherm aan. Hallo pictogram volgende toohello key toocopy klikt u op het Klembord tooyour, plakken en sla Hallo-sleutel. Deze knop werkt alleen als er één S2S-VPN-tunnel. Als u meerdere S2S VPN-tunnels hebt, gebruikt u Hallo *ophalen Virtual Network Gateway gedeelde sleutel* API of PowerShell-cmdlet.

![Sleutel beheren](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>Stap 2.  Uw VPN-apparaat configureren
Site-naar-Site-verbindingen tooan on-premises netwerk een VPN-apparaat vereist. Terwijl er geen configuratiestappen voor alle VPN-apparaten opgeeft, kunt u Hallo informatie vindt in Hallo volgen koppelingen die nuttig zijn:

- Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten. 
- Zie voor koppelingen toodevice configuratie-instellingen, [gevalideerde VPN-apparaten](vpn-gateway-about-vpn-devices.md#devicetable). Deze koppelingen worden op basis van 'best effort' aangeboden. Het is altijd best toocheck met de fabrikant van uw apparaat voor de meest recente configuratiegegevens Hallo.
- Zie [Bewerkingsvoorbeelden](vpn-gateway-about-vpn-devices.md#editing) voor voorbeelden van het bewerken van de apparaatconfiguratie.
- Zie [Parameters](vpn-gateway-about-vpn-devices.md#ipsec) voor de IPsec-/IKE-parameters.
- Voordat u uw VPN-apparaat configureert, controleren of er [bekende compatibiliteitsproblemen apparaat](vpn-gateway-about-vpn-devices.md#known) voor Hallo VPN-apparaat dat u wilt dat toouse.

Bij het configureren van uw VPN-apparaat, moet u Hallo volgende items:

- Hallo openbare IP-adres van uw virtuele netwerkgateway. U vindt dit door te gaan toohello **overzicht** blade voor het virtuele netwerk.
- Een gedeelde sleutel. Dit is Hallo dezelfde gedeelde sleutel die u opgeeft bij het maken van uw Site-naar-Site VPN-verbinding. In onze voorbeelden gebruiken we een zeer eenvoudige gedeelde sleutel. U moet een complexere sleutel toouse genereren.

Nadat het Hallo VPN-apparaat is geconfigureerd, kunt u uw bijgewerkte verbindingsinformatie weergeven op de dashboardpagina Hallo voor uw VNet.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>Stap 3. Controleer of uw lokale netwerkbereiken en IP-adres van VPN-gateway
#### <a name="verify-your-vpn-gateway-ip-address"></a>Controleer of het IP-adres van uw VPN-gateway
Voor de gateway tooconnect juist Hallo IP-adres voor uw VPN-apparaat moet correct zijn geconfigureerd voor Hallo lokale netwerk die u hebt opgegeven voor uw cross-premises-configuratie. Dit is normaal gesproken geconfigureerd tijdens Hallo site-naar-site-configuratie. Als u deze lokale netwerk eerder met een ander apparaat gebruikt of Hallo IP-adres voor deze lokale netwerk is gewijzigd, echter Hallo instellingen toospecify Hallo juiste Gateway IP-adres bewerken.

1. tooverify het IP-adres van uw gateway, klikt u op **netwerken** op Hallo portal linkerdeelvenster en selecteer vervolgens **lokale netwerken** bovenaan Hallo Hallo pagina. Hier ziet u Hallo VPN-Gateway-adres voor elke lokale netwerk dat u hebt gemaakt. tooedit hello IP-adres, selecteer Hallo VNet en klik op **bewerken** Hallo Hallo pagina onderaan in.
2. Op Hallo **Geef details op uw lokale netwerk** pagina en klik vervolgens op de volgende pijl Hallo HALLO hallo pagina onderaan in Hallo IP-adres bewerken.
3. Op Hallo **Geef Hallo-adresruimte** pagina, klikt u op Hallo vinkje Hallo lagere rechts toosave uw instellingen.

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>Hallo-adresbereiken voor uw lokale netwerken controleren
Hallo juist verkeer tooflow via Hallo gateway tooyour on-premises locatie moet u tooverify dat elk IP-adresbereik is opgegeven. Elk bereik moet worden vermeld in uw Azure **lokale netwerken** configuratie. Dit kan afhankelijk van de netwerkconfiguratie Hallo van uw on-premises locatie, een taak erg groot zijn. Verkeer dat is gekoppeld aan een IP-adres dat is opgenomen binnen Hallo vermeld bereiken worden verzonden via Hallo virtueel netwerk VPN-gateway. Hallo bereiken die u opgeeft niet toobe persoonlijke bereiken, hoewel u zult tooverify die uw on-premises-configuratie kan ontvangen Hallo binnenkomend verkeer.

bereik van de Hallo tooadd of bewerken voor een lokaal netwerk gebruik Hallo stappen te volgen:

1. tooedit hello IP-adresbereiken voor een lokale netwerk, klikt u op **netwerken** op Hallo portal linkerdeelvenster en selecteer vervolgens **lokale netwerken** bovenaan Hallo Hallo pagina. In de portal Hallo Hallo gemakkelijkste manier tooview Hallo bereiken die u hebt opgegeven is op Hallo **bewerken** pagina. toosee bereiken, selecteer Hallo VNet en klik op **bewerken** Hallo Hallo pagina onderaan in.
2. Op Hallo **Geef details op uw lokale netwerk** pagina, geen wijzigingen aanbrengt. Klik op volgende pijl Hallo HALLO hallo pagina onderaan in.
3. Op Hallo **Geef Hallo-adresruimte** maken van de adresruimtewijziigingen voor uw netwerk. Klik vervolgens op Hallo vinkje toosave uw configuratie.

## <a name="how-tooview-gateway-traffic"></a>Hoe tooview gateway verkeer
U kunt de gateway en de gateway-verkeer van het virtuele netwerk weergeven **Dashboard** pagina.

Op Hallo **Dashboard** pagina kunt u de volgende Hallo weergeven:

* Hallo hoeveelheid gegevens die via de gateway, zowel gegevens in en uit stroomt.
* Hallo-namen van Hallo DNS-servers die zijn opgegeven voor het virtuele netwerk.
* Hallo-verbinding tussen uw gateway en uw VPN-apparaat.
* Hallo gedeelde sleutel die is gebruikt tooconfigure uw gateway verbinding tooyour VPN-apparaat.

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>Hoe toochange Hallo routering VPN-type voor uw gateway
Omdat sommige configuraties connectiviteit alleen beschikbaar voor bepaalde routering gatewaytypen zijn, merkt u dat u nodig hebt toochange Hallo gateway VPN-routering type van een bestaande VPN-gateway. U kunt bijvoorbeeld tooadd punt-naar-site-connectiviteit tooan al een bestaande site-naar-site-verbinding met een statische gateway. Punt-naar-site-verbindingen nodig een dynamische gateway. Dit betekent tooconfigure een P2S-verbinding, moet u toochange uw gateway routering VPN-type van statische toodynamic.

Als u toochange routeringstype voor VPN-gateway moet, zult u Hallo bestaande gateway verwijdert en vervolgens een nieuwe gateway maken met de nieuwe routeringstype Hallo. U hoeft niet toodelete Hallo gehele virtuele netwerk toochange Hallo routering Gatewaytype.

Voordat u uw gateway routering VPN-type wijzigt, worden ervoor tooverify dat Hallo routeringstype dat u wilt dat toouse ondersteuning biedt voor uw VPN-apparaat. toodownload nieuwe routering configuratie samples en controle van VPN-apparaat, Zie [over VPN-apparaten voor verbinding met het virtuele netwerk](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Wanneer u een VPN-gateway van virtueel netwerk verwijdert, wordt Hallo VIP toegewezen toohello gateway uitgebracht. Wanneer u opnieuw Hallo gateway maakt, wordt een nieuwe VIP tooit toegewezen.
> 
> 

1. **Verwijder de bestaande VPN-gateway Hallo.**
   
    Op Hallo **Dashboard** pagina voor het virtuele netwerk, gaat u toohello onder aan Hallo pagina en klik op **Gateway verwijderen**. Wachttijd voor het Hallo-bericht dat Hallo gateway is verwijderd. Nadat u hebt ontvangen melding van de Hallo op het welkomstscherm dat uw gateway is verwijderd, kunt u een nieuwe gateway.
2. **Maak een nieuwe VPN-gateway.**
   
    Hallo procedure bovenaan Hallo Hallo pagina toocreate een nieuwe gateway gebruiken: [maken van een VPN-gateway](#create-a-vpn-gateway).

## <a name="next-steps"></a>Volgende stappen
U kunt virtuele machines tooyour virtueel netwerk kunt toevoegen. Zie [hoe een aangepaste virtuele machine toocreate](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Als u tooconfigure een punt-naar-site VPN-verbinding wilt, Zie [een punt-naar-site VPN-verbinding configureren](vpn-gateway-point-to-site-create.md).

