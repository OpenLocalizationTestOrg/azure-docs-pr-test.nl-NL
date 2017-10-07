---
title: aaaInstall Microsoft Azure StorSimple 8600-apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe toounpack, rek monteren en bekabelen uw StorSimple 8600-apparaat voordat u implementeert en Hallo software configureert.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>Unpack, rack koppelen, en uw StorSimple 8600-apparaat bekabelen
## <a name="overview"></a>Overzicht
Microsoft Azure StorSimple 8600 is een dubbele behuizing-apparaat en bestaat uit een primaire en een EBOD behuizing. Deze zelfstudie wordt uitgelegd hoe toounpack, rek monteren en bekabelen Hallo StorSimple 8600-apparaat hardware voordat u Hallo StorSimple software configureren.

## <a name="unpack-your-storsimple-8600-device"></a>Uw StorSimple 8600-apparaat uitpakken
Hallo volgende stappen bevatten wissen, gedetailleerde instructies voor het toounpack uw StorSimple 8600-opslagapparaat. Dit apparaat wordt geleverd in twee vakken, één voor de primaire behuizing Hallo en één voor Hallo EBOD behuizing. Deze twee vakken worden vervolgens in één vak geplaatst.

### <a name="prepare-toounpack-your-device"></a>Uw apparaat toounpack voorbereiden
Voordat u uw apparaat uitpakken, controleert u Hallo informatie te volgen.

![Waarschuwingspictogram](./media/storsimple-safety/IC740879.png)![zware gewicht pictogram](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **waarschuwing!**

1. Zorg ervoor dat u hebt twee personen beschikbaar toomanage Hallo gewicht van Hallo-apparaat als u deze handmatig worden verwerkt. Een volledig geconfigureerde behuizing wegen up too32 kg (70 lbs.).
2. Hallo vak op een plat niveau vlak plaatsen.

Vervolgens voltooien Hallo toounpack stappen te volgen van uw apparaat.

#### <a name="toounpack-your-device"></a>toounpack uw apparaat
1. Hallo vak en Hallo verpakking schuimrubber voor crushes, delen, water schade of andere duidelijk schade te controleren. Open Hallo vak niet als Hallo box of verpakking ernstig is beschadigd. Neem [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) toohelp u te beoordelen of apparaten Hallo in goede staat.
2. Hallo buitenste het openen en los uit Hallo twee vakken tooprimary en EBOD behuizingen overeenkomt. U kunt nu Hallo primaire en behuizingen EBOD uitpakken. Hallo volgende afbeelding toont Hallo uitgepakt weergave van een Hallo insluitingen.
   
    ![Uitpakken van uw opslagapparaat](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **Uitgepakte weergave van uw opslagapparaat**
   
   | Label | Beschrijving |
   | --- | --- |
   |   1 |Verpakking vak |
   |   2 |SAS-kabels (in het systeemvak, accessoires en kabels) |
   |   3 |Onder schuim |
   |   4 |Apparaat |
   |   5 |Bovenste schuim |
   |   6 |Accessoires vak |
3. Na het Hallo twee vakken uitpakken, zorg ervoor dat u hebt:
   
   * 1 primaire behuizing (Hallo primaire enclosure en EBOD behuizing zijn in twee afzonderlijke vakken)
   * 1 EBOD behuizing
   * 4 stroomkabels, 2 in elk vak
   * 2 SAS-kabels (tooconnect Hallo primaire behuizing tooEBOD behuizing)
   * 1 crossover Ethernet-kabel
   * 2 seriële console kabels
   * 1 seriële USB converter voor de seriële toegang
   * 4 QSFP-naar-SFP + adapters voor gebruik met 10 GbE-netwerkinterfaces
   * 2 rack mount kits (4 side rails met koppelen van de hardware, 2 voor de primaire behuizing Hallo en EBOD behuizing), 1 in elk vak
   * Gestarte documentatie ophalen
     
     Als u een van bovenstaande, Hallo-items niet ontvangen [contact op met Microsoft Support](storsimple-contact-microsoft-support.md).  

de volgende stap Hallo toorack koppelen is uw apparaat.

## <a name="rack-mount-your-storsimple-8600-device"></a>Uw StorSimple 8600-apparaat rack koppelen
Volg de volgende stappen tooinstall Hallo uw StorSimple 8600-opslagapparaat in een standaard 19-inch rack met vooraan en achteraan advertenties. Dit apparaat wordt geleverd met twee behuizingen: een primaire-behuizing en een EBOD behuizing. Deze moeten toobe rek.

Hallo-installatie bestaat uit meerdere stappen, die wordt besproken in Hallo procedures te volgen.

> [!IMPORTANT]
> StorSimple-apparaten moet rek wordt gemonteerd voor een juiste werking.
> 
> 

### <a name="site-preparation"></a>Voorbereiding van de site
Hallo-behuizingen moeten worden geïnstalleerd in een standaard 19-inch rack die front- en achterste advertenties. Hallo te volgen procedure tooprepare voor rackinstallatie gebruiken.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>tooprepare hello site voor de rackinstallatie van
1. Zorg ervoor dat Hallo primaire en EBOD behuizingen zijn veilig op een platte, stabiele en niveau werkoppervlak verwerken (of vergelijkbaar).
2. Controleren die Hallo site waar u van plan bent tooset up heeft standaard AC macht van een onafhankelijke bron of een rek Power Distribution Unit (PDU) met een noodvoeding (UPS).
3. Zorg ervoor dat één 4U (2 X 2U) sleuf is beschikbaar op Hallo rek waarin u van plan toomount Hallo behuizingen bent.

![Waarschuwingspictogram](./media/storsimple-safety/IC740879.png)![zware gewicht pictogram](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **waarschuwing!**

 Zorg ervoor dat u hebt twee personen beschikbaar toomanage Hallo gewicht als u de Apparaatinstelling Hallo handmatig verwerkt. Een volledig geconfigureerde behuizing wegen up too32 kg (70 lbs.).

### <a name="rack-prerequisites"></a>Rack-vereisten
Hallo-behuizingen zijn ontworpen voor installatie in een standaard 19-inch rack cab met:

* Minimale diepte van 27.84 inches van rek boeken toopost
* Maximale gewicht van 32 kg voor Hallo-apparaat
* Maximale back druk van 5 Pascal (0,5 mm water meter)

### <a name="rack-mounting-rail-kit"></a>Rek-montage spoor kit
U krijgt een reeks rails koppelen voor gebruik met Hallo 19-inch rack CAB-bestand. Hallo rails zijn getest toohandle Hallo maximale behuizing gewicht. Deze rails wordt ook installatie van meerdere insluitingen zonder verlies van ruimte binnen Hallo rack toestaan. Installeer eerst Hallo EBOD behuizing.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>tooinstall hello EBOD behuizing op Hallo rails
1. Deze stap alleen uitvoeren als interne rails zijn niet geïnstalleerd op uw apparaat. Normaal gesproken zijn op Hallo factory Hallo binnenste rails geïnstalleerd. Als rails niet zijn geïnstalleerd, installeert u Hallo links-spoor en rechts spoor dia toohello zijden van Hallo behuizing chassis. Ze koppelen met behulp van zes metrische schroeven voor elke zijde. toohelp met afdrukstand Hallo spoor dia's zijn gemarkeerd **LH – voorzijde** en **RH – voorzijde**, en het Hallo-end die is aangebracht vanaf Hallo achterzijde van Hallo behuizing heeft een Tapse end.
   
    ![Koppelen spoor dia tooenclosure chassis](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **Koppelen spoor dia toohello zijden van Hallo behuizing**
   
   | Label | Beschrijving |
   | --- | --- |
   |  1 |M 3 x 4 knop head schroeven |
   |  2 |Chassis dia |
2. Hallo links spoor en rechterkant assembly's toohello rack cab verticale leden koppelen. Hallo vierkante haken zijn gemarkeerd **LH**, **RH**, en **deze kant up** tooguide u via de juiste richting.
3. Zoek Hallo spoor pincodes op Hallo voor en achter van Hallo spoor assembly. Hallo spoor toofit tussen Hallo rack posts uitbreiden en Hallo pincodes invoegen in Hallo voor- en achterzijde rack post verticale lid gaten. Zorg ervoor dat Hallo spoor assembly niveau is.
4. Beveilig Hallo spoor assembly toohello rack verticale leden met behulp van twee van de metrische schroeven Hallo opgegeven. Een installatie op Hallo vooraan en één op Hallo achterzijde gebruiken.
5. Herhaal deze stappen voor Hallo andere spoor-assembly.
   
     ![Cab dia toorack koppelen spoor](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Spoor assembly's toohello rack koppelen**
   
   | Label | Beschrijving |
   | --- | --- |
   |   1 |Installatie clamping |
   |   2 |Vierkante hole front rack na installatie |
   |   3 |Front-spoor locatie pincodes links |
   |   4 |Installatie clamping |
   |   5 |Links achterste spoor locatie pincodes |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Hallo EBOD behuizing in Hallo rek koppelen
Gebruik Hallo rackrails die alleen zijn geïnstalleerd, uit te voeren Hallo stappen toomount hello EBOD behuizing in Hallo rek te volgen.

#### <a name="toomount-hello-ebod-enclosure"></a>toomount hello EBOD behuizing
1. Met een helper lift-Hallo behuizing en met Hallo rackrails uitlijnen.
2. Hallo behuizing zorgvuldig in Hallo rails plaatsen en vervolgens dit doorgeven volledig in Hallo rack cab.
   
    ![Apparaat invoegen in Hallo rek](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Hallo behuizing in Hallo rek koppelen**
3. Hallo links en rechts front flens caps verwijderen met binnenhalen Hallo caps gratis. Hallo flens caps uitgelijnd gewoon op Hallo flenzen.
4. Hallo behuizing in Hallo rack beveiligen door het installeren van een opgegeven kruiskopschroevendraaier head installatie via elke flens, linker- en.
5. Hallo flens caps installeren door ze naar de gewenste positie en uitlijning ze naar de juiste plaats.
   
     ![Flens caps installeren](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Hallo flens caps installeren**
   
   | Label | Beschrijving |
   | --- | --- |
   |   1 |Behuizing fixeerpunt installatie |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Hallo primaire behuizing in Hallo rek koppelen
Nadat u klaar bent met het Hallo EBOD behuizing koppelen, moet u toomount Hallo primaire behuizing volgende Hallo dezelfde stappen.

> [!NOTE]
> * Het is mogelijk toohave enkele leeg sleuven in Hallo rack tussen de primaire behuizing Hallo en Hallo EBOD behuizing.
> * Hallo opgegeven 2m SAS-kabel tooconnect Hallo primaire behuizing toohello EBOD behuizing gebruiken.
> * Er zijn geen beperkingen op Hallo relatieve plaatsing van Hallo head eenheid toohello EBOD eenheid. Daarom Hallo primaire behuizing kan worden geplaatst in het bovenste sleuf Hallo en Hallo EBOD behuizing onderstaande — of vice versa.
> 
> 

de volgende stap Hallo toocable is uw apparaat voor voeding, netwerk- en seriële toegang.

## <a name="cable-your-storsimple-8600-device"></a>Uw StorSimple 8600-apparaat bekabelen
Hallo volgende procedures wordt uitgelegd hoe toocable uw StorSimple 8600-apparaat voor voeding, netwerk- en seriële verbindingen.

### <a name="prerequisites"></a>Vereisten
Voordat u uw apparaat met toocable begint, moet u:

* Uw primaire behuizing en Hallo EBOD behuizing, volledig uitgepakt
* 4 power kabels (2 elke voor primaire Hallo en Hallo EBOD behuizing) bij uw apparaat
* 2 SAS-kabels geleverd met Hallo apparaat tooconnect hello EBOD behuizing toohello primaire behuizing
* Toegang too2 Power Distribution Units (PDU's) (aanbevolen)
* Netwerkkabels
* Seriële kabels opgegeven
* Seriële USB converter met de juiste stuurprogramma Hallo op uw PC geïnstalleerd (indien nodig)
* Opgegeven 4 QSFP-naar-SFP + adapters voor gebruik met 10 GbE-netwerkinterfaces
* [Ondersteunde hardware voor Hallo 10 GbE-netwerkinterfaces op uw StorSimple-apparaat](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>SAS en Power bekabeling
Uw apparaat heeft zowel een primaire-behuizing en een EBOD behuizing. U moet hiervoor Hallo eenheden toobe bekabeld samen voor seriële gekoppelde SCSI (SAS)-verbinding en geen stroom.

Bij het instellen van dit apparaat voor Hallo eerst, Voer u Hallo stappen voor SAS eerst bekabeling en vervolgens voltooit Hallo stappen voor het power bekabeling.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>Netwerkkabels
Het apparaat zich in een actief/stand-byconfiguratie: op elk gewenst één module van de domeincontroller actief is en andere controllermodule is verwerkingen alle schijven en het netwerk tijdens het Hallo op stand-by. Als een domeincontroller-fout optreedt, wordt de stand-by-controller Hallo onmiddellijk wordt geactiveerd en blijft alle Hallo-bewerkingen voor schijf- en -netwerken.

toosupport deze failover redundante domeincontroller, moet u uw apparaat netwerk zoals weergegeven in de volgende stappen uit Hallo toocable.

#### <a name="toocable-for-network-connection"></a>toocable voor netwerkverbinding
1. Uw apparaat heeft zes netwerkinterfaces op elke domeincontroller: vier 1 Gbps en twee 10 Gbps Ethernet-poorten. Raadpleeg toohello afbeelding tooidentify Hallo gegevenspoorten op HALLO backplane van uw apparaat te volgen.
   
     ![Backplane van 8600-apparaat](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Terug van uw apparaat weergegeven Hallo gegevenspoorten**
   
   | Label | Beschrijving |
   | --- | --- |
   |   0,1,4,5 |1 GbE-netwerkinterfaces |
   |   2,3 |10 GbE-netwerkinterfaces |
   |   6 |Seriële poorten |
2. Zie de volgende diagram voor netwerkkabels Hallo. (Hallo minimale configuratie wordt weergegeven door ononderbroken blauwe lijnen. Voor hoge beschikbaarheid en prestaties aanvullende configuratie vereist weergegeven door de stippellijn.)

![Uw apparaat 4U voor netwerk bekabelen](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**Netwerk bekabeling voor uw apparaat**

| Label | Beschrijving |
| --- | --- |
| A |LAN met internettoegang |
| B |Controller 0 |
| C |PCM 0 |
| D |Controller 1 |
| E |PCM 1 |
| F |EBOD-controller 0 |
| G |EBOD controller 1 |
| H, IK |Hosts (bijvoorbeeld bestandsservers) |
| 0-5 |Netwerkinterfaces |
| 6 |Primaire behuizing |
| 7 |EBOD behuizing |

Wanneer bekabeling Hallo-apparaat, wordt de minimale configuratie Hallo vereist:

* Ten minste twee netwerkinterfaces verbonden op elke domeincontroller met één voor toegang tot de cloud en één voor iSCSI. Hallo DATA 0 poort is automatisch ingeschakeld en geconfigureerd via de seriële console Hallo Hallo-apparaat. Naast de DATA 0 moet een andere gegevenspoort ook toobe geconfigureerd via Hallo klassieke Azure-portal. In dit geval verbinding maken met DATA 0-poort toohello primaire LAN (netwerk met internettoegang). Hallo andere gegevens poorten kunnen worden verbonden tooSAN/iSCSI-LAN (VLAN)-segment van Hallo netwerk, afhankelijk van de rol Hallo bedoeld.
* Identieke interfaces op elke domeincontroller verbonden toohello netwerk tooensure beschikbaarheid als een domeincontroller failover plaatsvindt. Als u tooconnect DATA 0 en 3 van de gegevens voor een Hallo domeincontrollers, u tooconnect Hallo DATA 0- en DATA 3 overeenkomt moet op Hallo bijvoorbeeld andere domeincontroller.

Houd er rekening mee voor hoge beschikbaarheid en prestaties:

* Indien mogelijk, configureert u een andere combinatie voor iSCSI (10 GbE aanbevolen) en een combinatie van netwerkinterface voor toegang tot de cloud (1 GbE) op elke domeincontroller.
* Indien mogelijk, sluit u netwerkinterfaces van elke domeincontroller tootwo verschillende switches tooensure beschikbaarheid op basis van een switch-fout. Hallo-afbeelding ziet u Hallo twee 10 GbE netwerkinterfaces DATA 2 en DATA 3 uit elke domeincontroller verbonden tootwo verschillende switches. Raadpleeg voor meer informatie, toohello **netwerkinterfaces** onder Hallo [vereisten voor hoge beschikbaarheid voor uw StorSimple-apparaat](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Als u SFP + infraroodzenders met uw 10 GbE-netwerkinterfaces, gebruik Hallo QSFP opgegeven-SFP + adapters. Voor meer informatie gaat te[ondersteunde hardware voor Hallo 10 GbE-netwerkinterfaces op uw StorSimple-apparaat](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Seriële poort bekabeling
Hallo toocable stappen na de seriële poort uitvoeren.

#### <a name="toocable-for-serial-connection"></a>toocable voor seriële verbinding
1. Uw apparaat heeft een seriële poort van elke domeincontroller die wordt geïdentificeerd door een moersleutelpictogram. toolocate hello seriële poorten, Raadpleeg toohello-afbeelding die laat zien Hallo gegevenspoorten op Hallo achterzijde van het apparaat.
2. Identificeer de actieve controller Hallo op uw apparaat-backplane. Een knipperende blauw LED geeft aan dat Hallo domeincontroller actief is.
3. Hallo opgegeven in de seriële kabel (indien nodig, Hallo USB-seriële converter voor uw laptop), en koppel de console of de computer (met terminal emulatie toohello apparaat) toohello seriële poort van de actieve controller Hallo.
4. Hallo serieel-USB-stuurprogramma's (geleverd bij Hallo apparaat) op uw computer installeren.
5. Hallo seriële verbinding instellen als volgt:
   
   * 115.200 baud
   * 8 gegevensbits
   * 1 stop-bits
   * Geen pariteit
   * Datatransportbesturing instellen te**geen**
6. Controleren of verbinding Hallo werkt met ENTER op Hallo-console. Het menu van een seriële console moet worden weergegeven.

> [!NOTE]
> **Beheer van lights-Out:** wanneer Hallo-apparaat is geïnstalleerd in een externe datacenter of in een computerruimte met beperkte toegang, zorg ervoor dat Hallo seriële verbindingen tooboth domeincontrollers altijd verbonden tooa seriële consoleswitch of vergelijkbare apparatuur. Hierdoor kan out-of-band beheer op afstand en ondersteuning-bewerkingen in geval van een onderbreking van de netwerk- of onverwachte storingen.
> 
> 

U hebt uw apparaat voor voeding, toegang tot het netwerk, kabels en de volgende stap seriële connection.hello tooconfigure Hallo software op uw apparaat.

## <a name="next-steps"></a>Volgende stappen
U bent gereed te[implementeren en configureren van uw on-premises StorSimple-apparaat](storsimple-deployment-walkthrough-u2.md).

