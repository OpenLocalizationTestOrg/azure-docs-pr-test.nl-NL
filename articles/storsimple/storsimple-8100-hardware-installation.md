---
title: aaaInstall Microsoft Azure StorSimple 8100-apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe toounpack, rek monteren en bekabelen uw StorSimple 8100-apparaat voordat u implementeert en Hallo software configureert.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6098a01e-c031-488a-a8d7-0b607ce665e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 76b94e57318b6c25dc3333ae73edc9e4752b7d1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8100-device"></a>Unpack, rack koppelen, en uw StorSimple 8100-apparaat bekabelen
## <a name="overview"></a>Overzicht
Uw Microsoft Azure StorSimple 8100 is een enkel behuizing rek apparaat. Deze zelfstudie wordt uitgelegd hoe toounpack, rek monteren en bekabelen Hallo StorSimple 8100-apparaat hardware voordat u configureert en Hallo StorSimple-apparaat implementeren.

## <a name="unpack-your-storsimple-8100-device"></a>Uw StorSimple 8100-apparaat uitpakken
Hallo volgende stappen bevatten wissen, gedetailleerde instructies over het toounpack uw StorSimple 8100-opslagapparaat. Dit apparaat wordt geleverd in één vak.

### <a name="prepare-toounpack-your-device"></a>Uw apparaat toounpack voorbereiden
Voordat u uw apparaat uitpakken, controleert u Hallo informatie te volgen.

![Waarschuwingspictogram](./media/storsimple-safety/IC740879.png)![zware gewicht pictogram](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png) **waarschuwing!**

1. Zorg ervoor dat u hebt twee personen beschikbaar toomanage Hallo gewicht van Hallo behuizing als u deze handmatig worden verwerkt. Een volledig geconfigureerde behuizing wegen up too32 kg (70 lbs.).
2. Hallo vak op een plat niveau vlak plaatsen.

Vervolgens voltooien Hallo toounpack stappen te volgen van uw apparaat.

#### <a name="toounpack-your-device"></a>toounpack uw apparaat
1. Hallo vak en Hallo verpakking schuimrubber voor crushes, delen, water schade of andere duidelijk schade te controleren. Open Hallo vak niet als Hallo box of verpakking ernstig is beschadigd. Neem [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) toohelp u te beoordelen of apparaten Hallo in goede staat.
2. Hallo vak uitpakken. Hallo volgende afbeelding toont Hallo uitgepakt weergave van uw StorSimple-apparaat.
   
     ![Uitpakken van uw opslagapparaat](./media/storsimple-8100-hardware-installation/HCSUnpackyour2Udevice.png)
   
    **Uitgepakte weergave van uw opslagapparaat**
   
   | Label | Beschrijving |
   | --- | --- |
   |   1 |Verpakking vak |
   |   2 |Onder schuim |
   |   3 |Apparaat |
   |   4 |Bovenste schuim |
   |   5 |Accessoires vak |
3. Na het Hallo-vak uitpakken, zorg ervoor dat u hebt:
   
   * 1 apparaat met één behuizing
   * 2 stroomkabels
   * 1 crossover Ethernet-kabel
   * 2 seriële console kabels
   * 1 seriële USB converter voor de seriële toegang
   * 1 fraudebestendig T10 draai
   * 4 QSFP-naar-SFP + adapters voor gebruik met 10 GbE-netwerkinterfaces
   * 1 met het rek monteren kit (2 side rails met koppelen van de hardware)
   * Getting Started-documentatie
     
     Als u een van bovenstaande, Hallo-items niet ontvangen [contact op met Microsoft Support](storsimple-contact-microsoft-support.md).

de volgende stap Hallo toorack koppelen is uw apparaat.

## <a name="rack-mount-your-storsimple-8100-device"></a>Uw StorSimple 8100-apparaat rack koppelen
Volg de volgende stappen tooinstall Hallo uw StorSimple 8100-opslagapparaat in een standaard 19-inch rack met vooraan en achteraan advertenties. Hallo StorSimple 8100-apparaat heeft één primaire behuizing.

Hallo-installatie bestaat uit meerdere stappen, die wordt besproken in Hallo procedures te volgen.

> [!IMPORTANT]
> StorSimple-apparaten moet rek wordt gemonteerd voor een juiste werking.
> 
> 

### <a name="prepare-hello-site"></a>Hallo site voorbereiden
Hallo-apparaat moet worden geïnstalleerd in een standaard 19-inch rack die front- en achterste advertenties. Hallo te volgen procedure tooprepare voor rackinstallatie gebruiken.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>tooprepare hello site voor de rackinstallatie van
1. Zorg ervoor dat het Hallo-apparaat veilig is gebaseerd op een platte, stabiele en niveau werk water (of vergelijkbaar).
2. Controleer of Hallo site waar u van plan tooset up bent standaard netstroom is van een onafhankelijke bron of een rack power distribution Units (PDU) met uninterruptible power supply (UPS).
3. Zorg ervoor dat één 2U sleuf is beschikbaar op Hallo rek waarin u van plan toomount Hallo apparaat bent.

![Waarschuwingspictogram](./media/storsimple-safety/IC740879.png)![zware gewicht pictogram](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png) **waarschuwing!**

Zorg ervoor dat u hebt twee personen beschikbaar toomanage Hallo gewicht als u de Apparaatinstelling Hallo handmatig verwerkt. Een volledig geconfigureerde behuizing wegen up too32 kg (70 lbs.).

### <a name="rack-prerequisites"></a>Rack-vereisten
Hallo 8100 behuizing is ontworpen voor installatie in een standaard 19-inch rack cab met:

* Minimale diepte van 27.84 inches van rek boeken toopost.
* Maximale gewicht van 32 kg voor Hallo-apparaat
* Maximale back druk van 5 Pascal (0,5 mm water meter).

### <a name="rack-mounting-rail-kit"></a>Rek-montage spoor kit
Een set rails koppelen is beschikbaar voor gebruik met Hallo 19-inch rack CAB-bestand. Hallo rails zijn getest toohandle Hallo maximale behuizing gewicht. Deze rails wordt ook installatie van meerdere insluitingen zonder verlies van ruimte binnen Hallo rack toestaan.

#### <a name="tooinstall-hello-device-on-hello-rails"></a>tooinstall hello apparaat op Hallo rails
1. Deze stap alleen uitvoeren als interne rails zijn niet geïnstalleerd op uw apparaat. Normaal gesproken zijn op Hallo factory Hallo binnenste rails geïnstalleerd. Als rails niet zijn geïnstalleerd, installeert u Hallo links-spoor en rechts spoor dia toohello zijden van Hallo behuizing chassis. Ze koppelen met behulp van zes metrische schroeven voor elke zijde. toohelp met afdrukstand Hallo spoor dia's zijn gemarkeerd **LH – voorzijde** en **RH – voorzijde**, en het Hallo-end die is aangebracht vanaf Hallo achterzijde van Hallo behuizing heeft een Tapse end.<br/>
   
    ![Koppelen spoor dia tooenclosure chassis](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)

    **Koppelen van interne spoor dia toohello zijden van Hallo behuizing**
   
    Label | Beschrijving
    ----- | -----------
    1     | M 3 x 4 knop head schroeven
    2     | Chassis dia

2. Hallo buitenste links spoor en buitenste rechterkant assembly's toohello rack cab verticale leden koppelen. Hallo vierkante haken zijn gemarkeerd **LH**, **RH**, en **deze kant up** tooguide u via Hallo afdrukstand corrigeren.
3. Zoek Hallo spoor pincodes op Hallo voor en achter van Hallo spoor assembly. Hallo spoor toofit tussen Hallo rack posts uitbreiden en Hallo pincodes invoegen in Hallo voorzijde en achterzijde rack post verticale lid gaten. Zorg ervoor dat Hallo spoor assembly niveau is.
4. Gebruik van twee opgegeven Hallo metrische schroeven toosecure Hallo spoor assembly toohello rack verticale leden. Een installatie op Hallo vooraan en één op Hallo achterzijde gebruiken.
5. Herhaal deze stappen voor Hallo andere spoor-assembly.<br/>
   
     ![Cab dia toorack koppelen spoor](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Buitenste spoor assembly's toohello rack koppelen**
   
   | Label | Beschrijving |
   | --- | --- |
   |   1 |Installatie clamping |
   |   2 |Vierkante hole front rack na installatie |
   |   3 |Links spoor front locatie pincodes |
   |   4 |Installatie clamping |
   |   5 |Links spoor achterste locatie pincodes |

### <a name="mounting-hello-device-in-hello-rack"></a>Hallo-apparaat in Hallo rack koppelen
Gebruik Hallo rackrails die alleen zijn geïnstalleerd, uit te voeren Hallo stappen toomount Hallo apparaat in Hallo rek te volgen.

#### <a name="toomount-hello-device"></a>toomount hello apparaat
1. Met een helper lift-Hallo behuizing en met Hallo rackrails uitlijnen.
2. Hallo apparaat zorgvuldig in Hallo rails plaatsen en vervolgens push Hallo apparaat volledig in Hallo rack cab.<br/>
   
    ![Apparaat invoegen in Hallo rek](./media/storsimple-8100-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Hallo-apparaat in Hallo rack koppelen**
3. Hallo links en rechts front flens caps verwijderen met binnenhalen Hallo caps gratis. Hallo flens caps uitgelijnd gewoon op Hallo flenzen.
4. Hallo behuizing in Hallo rek door het installeren van een opgegeven kruiskopschroevendraaier head installatie via elke flens, linker- en beveiligen.
5. Hallo flens caps installeren door ze naar de gewenste positie en uitlijning ze aanwezig.<br/>
   
     ![Flens caps installeren](./media/storsimple-8100-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Hallo flens caps installeren**
   
   | Label | Beschrijving |
   | --- | --- |
   |   1 |Behuizing fixeerpunt installatie |

de volgende stap Hallo toocable is uw apparaat voor voeding, netwerk- en seriële toegang.

## <a name="cable-your-storsimple-8100-device"></a>Uw StorSimple 8100-apparaat bekabelen
Hallo volgende procedures wordt uitgelegd hoe toocable uw StorSimple 8100-apparaat voor voeding, netwerk- en seriële verbindingen.

### <a name="prerequisites"></a>Vereisten
Voordat u begint met het Hallo bekabeling van uw apparaat, moet u:

* Uw opslagapparaat, volledig uitgepakt en rack gekoppeld.
* 2 power kabels die bij uw apparaat
* Toegang too2 Power Distribution Units (aanbevolen).
* Netwerkkabels
* Seriële kabels opgegeven
* Seriële USB converter met de juiste stuurprogramma Hallo op uw PC geïnstalleerd (indien nodig)
* Opgegeven 4 QSFP-naar-SFP + adapters voor gebruik met 10 GbE-netwerkinterfaces
* [Ondersteunde hardware voor Hallo 10 GbE-netwerkinterfaces op uw StorSimple-apparaat](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="power-cabling"></a>Power bekabeling
Uw apparaat bevat redundante stroom en koeling Modules (PCMs). Zowel PCMs moet worden geïnstalleerd en verbonden toodifferent power bronnen tooensure hoge beschikbaarheid.

Volgende stappen toocable Hallo uw apparaat voor power uitvoeren.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

### <a name="network-cabling"></a>Netwerkkabels
Uw apparaat is een actief/stand-byconfiguratie: op elk gewenst één module van de domeincontroller actief is en andere controllermodule is verwerkingen alle schijven en het netwerk tijdens het Hallo op stand-by. Als een domeincontroller is mislukt, wordt de stand-by-controller Hallo onmiddellijk wordt geactiveerd en blijft van alle Hallo-bewerkingen voor schijf- en -netwerken.

toosupport deze failover redundante domeincontroller, moet u uw apparaat netwerk zoals beschreven in de volgende stappen uit Hallo toocable.

#### <a name="toocable-for-network-connection"></a>toocable voor netwerkverbinding
1. Uw apparaat heeft zes netwerkinterfaces op elke domeincontroller: vier 1 Gbps en twee 10 Gbps Ethernet-poorten. Hallo verschillende gegevens poorten op HALLO backplane van uw apparaat identificeren.
   
    ![Backplane van 8100-apparaat](./media/storsimple-8100-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Gegevenspoorten terug van Hallo-apparaat wordt weergegeven**
   
   | Label | Beschrijving |
   | --- | --- |
   |   0,1,4,5 |1 GbE-netwerkinterfaces |
   |   2,3 |10 GbE-netwerkinterfaces |
   |   6 |Seriële poorten |
2. Zie de volgende diagram voor netwerkkabels Hallo. (Hallo minimale configuratie wordt weergegeven door ononderbroken blauwe lijnen. Aanvullende configuratie vereist voor hoge beschikbaarheid en prestaties wordt weergegeven door de stippellijn.)

    ![Uw apparaat 2U voor netwerk bekabelen](./media/storsimple-8100-hardware-installation/HCSCableYour2UDeviceforNetwork.png)

    **Netwerk bekabeling voor uw apparaat**

   |Label | Beschrijving |
   |----- | ----------- |
   | A    | LAN met internettoegang |
   | B    | Controller 0 |
   | C    | PCM 0 |
   | D    | Controller 1 |
   | E    | PCM 1 |
   | F, G | Hosts |
   | 0-5  | Netwerkinterfaces |



Wanneer bekabeling Hallo-apparaat, wordt de minimale configuratie Hallo vereist:

* Ten minste twee netwerkinterfaces verbonden op elke domeincontroller met één voor toegang tot de cloud en één voor iSCSI. Hallo DATA 0 poort is automatisch ingeschakeld en geconfigureerd via de seriële console Hallo Hallo-apparaat. Naast de DATA 0 moet een andere gegevenspoort ook toobe geconfigureerd via Hallo klassieke Azure-portal. In dit geval verbinding maken met DATA 0-poort toohello primaire LAN (netwerk met internettoegang). Hallo andere gegevens poorten kunnen worden verbonden tooSAN/iSCSI-LAN (VLAN)-segment van Hallo netwerk, afhankelijk van de rol Hallo bedoeld.
* Identieke interfaces op elke domeincontroller verbonden toohello netwerk tooensure beschikbaarheid als een domeincontroller failover plaatsvindt. Als u tooconnect DATA 0 en 3 van de gegevens voor een Hallo domeincontrollers, u tooconnect Hallo DATA 0- en DATA 3 overeenkomt moet op Hallo bijvoorbeeld andere domeincontroller.

Houd er rekening mee voor hoge beschikbaarheid en prestaties:

* Indien mogelijk, configureert u een andere combinatie voor iSCSI (10 GbE aanbevolen) en een combinatie van netwerkinterface voor toegang tot de cloud (1 GbE) op elke domeincontroller.
* Indien mogelijk, sluit u netwerkinterfaces van elke domeincontroller tootwo verschillende switches tooensure beschikbaarheid op basis van een switch-fout. Hallo-afbeelding ziet u Hallo twee 10 GbE netwerkinterfaces DATA 2 en DATA 3 uit elke domeincontroller verbonden tootwo verschillende switches.

Raadpleeg voor meer informatie, toohello **netwerkinterfaces** onder Hallo [vereisten voor hoge beschikbaarheid voor uw StorSimple-apparaat](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Als u met uw 10 GbE-netwerkinterfaces SFP + infraroodzenders gebruikt, gebruik Hallo QSFP opgegeven-SFP + adapters. Voor meer informatie gaat te[ondersteunde hardware voor Hallo 10 GbE-netwerkinterfaces op uw StorSimple-apparaat](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Seriële poort bekabeling
Hallo toocable stappen na de seriële poort uitvoeren.

#### <a name="toocable-for-serial-connection"></a>toocable voor seriële verbinding
1. Uw apparaat heeft een seriële poort van elke domeincontroller die wordt geïdentificeerd door een moersleutelpictogram. Raadpleeg toohello illustratie in Hallo [netwerkkabels](#network-cabling) sectie toolocate Hallo seriële poorten op HALLO backplane van uw apparaat.
2. Identificeer de actieve controller Hallo op uw apparaat-backplane. Een knipperende blauw LED geeft aan dat Hallo domeincontroller actief is.
3. Hallo opgegeven seriële kabels (indien nodig, Hallo USB-seriële converter voor uw laptop), en koppel de console of de computer (met terminal emulatie toohello apparaat) toohello seriële poort van de actieve controller Hallo.
4. Hallo serieel-USB-stuurprogramma's (geleverd bij Hallo apparaat) op uw computer installeren.
5. Hallo seriële verbinding als volgt instellen: 115.200 baud, 8 gegevensbits, 1 stop bits, geen pariteit en datatransportbesturing tooNone ingesteld.
6. Controleren of verbinding Hallo werkt met ENTER op Hallo-console. Het menu van een seriële console moet worden weergegeven.

> [!NOTE]
> **Lights-Out Management**: wanneer Hallo-apparaat is geïnstalleerd in een externe datacenter of in een computerruimte met beperkte toegang, zorg ervoor dat Hallo seriële verbindingen tooboth domeincontrollers altijd verbonden tooa seriële consoleswitch of vergelijkbare apparatuur. Hierdoor kan de out-of-band beheer op afstand en bewerkingen van de ondersteuning als er netwerkonderbrekingen of onverwachte storingen.
> 
> 

Uw apparaat is nu bekabeld voor voeding, toegang tot het netwerk- en seriële verbinding. de volgende stap Hallo is tooconfigure Hallo software en -apparaat implementeren.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe te[implementeren en configureren van uw on-premises StorSimple-apparaat](storsimple-deployment-walkthrough-u2.md).

