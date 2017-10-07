---
title: aaaStorSimple lokaal vastgemaakte volumes Veelgestelde vragen | Microsoft Docs
description: Biedt antwoorden toofrequently gevraagd vragen over StorSimple lokaal vastgemaakte volumes.
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 7a2f4b1a-4ac9-4ce1-9359-bd40a9cbbb5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/11/2017
ms.author: manuaery
ms.openlocfilehash: 6a0c742acea836c2b960cb604e4010bcb08c3169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>StorSimple lokaal vastgemaakte volumes: veelgestelde vragen (FAQ)
## <a name="overview"></a>Overzicht
Hallo volgen vragen en antwoorden er bij het maken van een lokaal vastgemaakt StorSimple-volume een gelaagd volume tooa lokaal vastgemaakt volume converteren (en omgekeerd) of back-up en herstellen van een lokaal vastgemaakt volume.

Vragen en antwoorden zijn gerangschikt in de volgende categorieën Hallo

* Een lokaal vastgemaakt volume maken
* Back-ups van een lokaal vastgemaakt
* Converteren van een gelaagd volume tooa lokaal vastgemaakt volume
* Herstellen van een lokaal vastgemaakt volume
* Mislukte via een lokaal vastgemaakt volume

## <a name="questions-about-creating-a-locally-pinned-volume"></a>Vragen over het maken van een lokaal vastgemaakt volume
**V:** Wat is de maximale grootte van een lokaal vastgemaakt volume dat ik op apparaten met 8000 serie Hallo maken kunt Hallo?

**Een** op apparaten met StorSimple 8000 Series Update 3.0 kunt u lokaal vastgemaakte volumes tot too8.5 TB en gelaagde volumes van too200 TB op Hallo 8100-apparaat kunt inrichten. U kunt lokaal vastgemaakte volumes tot too22.5 TB en gelaagde volumes van too500 TB inrichten op Hallo groter 8600-apparaat.    
Op apparaten waarop StorSimple 8000 serie Update 2.x, kunt u lokaal vastgemaakte volumes van too8 TB en gelaagde volumes van too200 TB op Hallo 8100-apparaat inrichten. U kunt lokaal vastgemaakte volumes van too20 TB en gelaagde volumes van too500 TB inrichten op Hallo groter 8600-apparaat.   

**V:** Ik mijn 8100-apparaat tooUpdate 2.0 kortgeleden is geüpgraded en wanneer ik probeer toocreate een lokaal vastgemaakt volume, Hallo maximumgrootte beschikbaar is alleen 6 TB en niet 8 TB. Waarom niet kan ik een volume van 8 TB maken?

**Een** als uw apparaat update 2.0 wordt uitgevoerd, kunt u lokaal vastgemaakte volumes van too8 TB inrichten of gelaagde volumes van too200 TB op Hallo 8100-apparaat. Als het apparaat reeds volumes gelaagde, zullen Hallo beschikbare schijfruimte voor het maken van een lokaal vastgemaakt volume proportioneel lager is dan de maximale limiet zijn. Bijvoorbeeld, als er 100 TB van gelaagde volumes al zijn ingericht op uw 8100-apparaat (dit is de helft van Hallo capaciteit gelaagd), wordt Hallo maximale grootte van een lokaal volume dat kan worden gemaakt op Hallo 8100-apparaat navenant verminderde too4 TB (ongeveer de helft van Hallo maximum lokaal vastgemaakt volumecapaciteit).

Aangezien lokale ruimte op Hallo apparaat gebruikte toohost Hallo werkset van gelaagde volumes, is Hallo beschikbare ruimte voor het maken van een lokaal vastgemaakt volume als Hallo apparaat volumes gelaagde verminderd. Maken van een lokaal vastgemaakt volume proportioneel vermindert daarentegen Hallo beschikbare ruimte voor gelaagde volumes. Hallo na tabellen bevat een overzicht van Hallo beschikbare gelaagde capaciteit op Hallo 8100 en 8600 apparaten tijdens het maken van lokaal vastgemaakte volumes.

####<a name="update-30"></a>3.0 bijwerken 
| Lokaal vastgemaakte volumes ingerichte capaciteit | Beschikbare capaciteit toobe ingericht voor gelaagde volumes - 8100 | Beschikbare capaciteit toobe ingericht voor gelaagde volumes - 8600 |
| --- | --- | --- |
| 0 |200 TB |500 TB |
| 1 TB |176,5 TB |477.8 TB |
| 4 TB |105.9 TB |411.1 TB |
| 8.5 TB |0 TB |311.1 TB |
| 10 TB |N.v.t. |277.8 TB |
| 15 TB |N.v.t. |166.7 TB |
| 22.5 TB |N.v.t. |0 TB |

####<a name="update-2x"></a>2.x bijwerken  
 | Lokaal vastgemaakte volumes ingerichte capaciteit | Beschikbare capaciteit toobe ingericht voor gelaagde volumes - 8100 | Beschikbare capaciteit toobe ingericht voor gelaagde volumes - 8600 |  
 | --- | --- | --- |  
 | 0 |200 TB |500 TB |  
 | 1 TB |25 TB |475 TB |  
 | 4 TB |100 TB |400 TB |  
 | 8 TB |0 TB |300 TB |  
 | 10 TB |N.v.t. |250 TB |  
 | 15 TB |N.v.t. |125 TB |  
 | 20 TB |N.v.t. |0 TB |   

**V:** Waarom is een langdurige bewerking lokaal vastgemaakt volume maken? 

**A:** Lokaal vastgemaakte volumes compact ingericht. toocreate ruimte op de lokale lagen van apparaat Hallo Hallo, sommige gegevens van bestaande gelaagde volumes mogelijk toohello cloud worden gepusht tijdens het inrichtingsproces Hallo. En omdat dit is afhankelijk van de grootte van Hallo volume wordt ingericht, Hallo bestaande gegevens op uw apparaat en Hallo beschikbare bandbreedte toohello cloud, Hallo Hallo tijd toocreate die een lokaal volume mogelijk enkele uren.

**V:** Hoe lang duurt toocreate een lokaal vastgemaakt volume?

**A:** Omdat lokaal vastgemaakte volumes compact ingericht zijn, kan bepaalde bestaande gegevens van gelaagde volumes mogelijk toohello cloud tijdens het inrichtingsproces Hallo worden gepusht. Daarom Hallo tijd toocreate een lokaal vastgemaakt volume is afhankelijk van meerdere factoren, onder andere de grootte Hallo van Hallo volume, Hallo gegevens op uw apparaat en de beschikbare bandbreedte Hallo. Op een geheel nieuw geïnstalleerde apparaat dat geen volumes heeft, is Hallo tijd toocreate een lokaal vastgemaakt volume ongeveer tien minuten per terabyte van gegevens. Maken van lokale volumes duurt echter enkele uren gebaseerd op Hallo factoren die hierboven worden uitgelegd op een apparaat dat wordt gebruikt.

**V:** Ik wil toocreate een lokaal vastgemaakt volume. Zijn er aanbevolen procedures die ik toobe op de hoogte van nodig?

**A:** Lokaal vastgemaakte volumes zijn geschikt voor werkbelastingen waarvoor lokale garanties van gegevens te allen tijde vereisen en worden gevoelige toocloud latenties. Tijdens het gebruik van lokale volumes voor een van de werkbelasting van uw overweegt, moet je erop letten van Hallo volgende:

* Lokaal vastgemaakte volumes zijn compact ingericht en maken van lokale volumes heeft impact op Hallo beschikbare ruimte voor gelaagde volumes. We raden daarom u beginnen met kleiner volumes en omhoog schalen als uw opslag vereiste toeneemt.
* Het inrichten van lokale volumes is een langdurige bewerking waarbij bestaande gegevens worden gepusht van gelaagde volumes toohello cloud mogelijk. Als gevolg hiervan kunnen optreden verminderde prestaties op deze volumes.
* Het inrichten van lokale volumes is een tijdrovende bewerking. Hallo werkelijke tijd die zijn betrokken, is afhankelijk van meerdere factoren: Hallo grootte van de Hallo volume wordt ingericht, gegevens op het apparaat en de beschikbare bandbreedte. Als u geen reservekopie uw bestaande volumes toohello cloud hebt gemaakt, zijn maken van volumes is langzamer. We raden dat u momentopnamen cloud van uw bestaande volumes voordat u een lokaal volume inricht.
* U kunt bestaande gelaagde volumes toolocally vastgemaakt volumes converteren en deze conversie omvat het inrichten van de ruimte op het Hallo-apparaat voor Hallo resulterende lokaal vastgemaakt volume (in aanvulling toobringing omlaag gelaagde gegevens [eventuele] vanuit de cloud Hallo). Dit is ook een langdurige bewerking die is afhankelijk van factoren besproken hierboven hebt. Het is raadzaam om de back-up van uw bestaande volumes voorafgaande tooconversion als Hallo proces nog langer duren als er bestaande volumes zijn niet een back-up. Uw apparaat tegenkomen verminderde prestaties tijdens dit proces ook.

Meer informatie over het te[een lokaal vastgemaakt volume maken](storsimple-manage-volumes-u2.md#add-a-volume)

**V:** Kan ik meerdere lokaal vastgemaakte volumes maken op Hallo hetzelfde moment?

**A:** Ja, maar geen lokaal vastgemaakt volume maken en uitbreiding van de taken worden opeenvolgend verwerkt.

Lokaal vastgemaakte volumes zijn compact ingericht en hiervoor is het maken van lokale ruimte op Hallo-apparaat (dit kan leiden tot bestaande gegevens van gelaagde volumes toobe toohello cloud gepusht tijdens het inrichtingsproces Hallo) vereist. Dus als een taak uitgevoerd wordt, andere taken voor het maken van lokaal volume wordt in de wachtrij gezet tot deze taak is voltooid.

Als een bestaand lokaal volume wordt uitgebreid of een gelaagd volume wordt omgezet tooa lokaal vastgemaakt volume vervolgens hello maken van een nieuw lokaal vastgemaakt volume zich in de wachtrij totdat de vorige taak Hallo is voltooid. Hallo-grootte van een lokaal vastgemaakt volume uitbreiden omvat het Hallo-uitbreiding van de bestaande lokale ruimte Hallo voor dat volume. Conversie van een gelaagde toolocally vastgemaakt volume omvat ook Hallo maken van lokale ruimte voor Hallo resulterende lokaal vastgemaakt volume. In beide deze bewerkingen, maken of uitbreiding van de lokale ruimte wordt een long uitgevoerd taak.

U kunt deze taken weergeven in Hallo **taken** pagina Hallo Azure StorSimple Manager-service. Hallo taak die actief wordt verwerkt wordt voortdurend bijgewerkt tooreflect Hallo voortgang van de schijfruimte wordt ingericht. Hallo resterende lokaal vastgemaakt volume taken zijn gemarkeerd als actief, maar hun progressie tot stilstand is gekomen en ze worden opgenomen in Hallo volgorde waarin dat ze zijn in de wachtrij.

**V:** Ik heb verwijderd een lokaal vastgemaakt volume. Waarom zie ik niet ruimte vrijgemaakt Hallo weerspiegeld in de beschikbare ruimte Hallo wanneer ik probeer toocreate een nieuw volume? 

**A:** Als u een lokaal vastgemaakt volume verwijdert, worden Hallo beschikbare schijfruimte voor het nieuwe volumes mogelijk niet meteen bijgewerkt. Hallo StorSimple Manager-Service-updates Hallo lokale ruimte beschikbaar ongeveer om het uur. We raden dat u wachten tot een uur voordat u toocreate Hallo nieuw volume probeert.

**V:** Worden lokaal vastgemaakte volumes op Hallo cloud toestel ondersteund?

**A:** Lokaal vastgemaakte volumes worden niet ondersteund op Hallo cloud toestel (8010 en 8020 apparaten voorheen waarnaar wordt verwezen tooas Hallo virtuele StorSimple-apparaat).

**V:** Kan ik hello Azure PowerShell-cmdlets toocreate gebruiken en beheren van lokaal vastgemaakte volumes? 

**A:** Nee, u lokaal vastgemaakte volumes via Azure PowerShell-cmdlets (alle volumes die u via Azure PowerShell maakt is gelaagd) niet maken. Ook het is raadzaam dat u niet hello Azure PowerShell-cmdlets toomodify alle eigenschappen van een lokaal vastgemaakt volume gebruiken als deze hebben Hallo ongewenst effect Hallo volume type tootiered wijzigen.

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>Vragen over het back-ups van een lokaal vastgemaakt volume
**V:** Zijn lokale momentopnamen van lokaal vastgemaakte volumes ondersteund?

**A:** Ja, u kunt momentopnamen lokale van uw lokaal vastgemaakte volumes. Echter ten zeerste het is raadzaam dat u regelmatig back-up van uw lokaal vastgemaakte volumes met cloud momentopnamen tooensure die wordt beveiligd in uw gegevens Hallo deze van een noodgeval.

**V:** Zijn er richtlijnen voor het beheren van lokale momentopnamen voor lokaal vastgemaakte volumes?

**A:** Regelmatige lokale momentopnamen samen met een hoge frequentie van gegevensverloop in Hallo lokaal vastgemaakt volume mogelijk ertoe leiden dat lokale ruimte op Hallo apparaat toobe snel verbruikt en leiden tot gegevens van gelaagde volumes toohello cloud wordt gepusht. We raden daarom minimaliseert u Hallo aantal lokale momentopnamen.

**V:** Ik krijg een waarschuwing met de mededeling dat mijn lokale momentopnamen van lokaal vastgemaakte volumes mogelijk ongeldig worden gemaakt. Wanneer kan dit gebeuren

**A:** Regelmatige lokale momentopnamen samen met een hoge frequentie van gegevensverloop in Hallo lokaal vastgemaakt volume ertoe leiden lokale ruimte op Hallo apparaat toobe snel verbruikt dat kan. Als u lokale lagen Hallo Hallo apparaat intensief gebruikt, een uitgebreide cloud storing kan leiden tot Hallo apparaat vol raken en binnenkomende schrijfbewerkingen toohello volume kan leiden tot ongeldig te maken van momentopnamen hello (zoals geen ruimte tooupdate Hallo momentopnamen toorefer bestaat toohello oudere blokken met gegevens die zijn overschreven). In dergelijke een situatie Hallo blijft schrijfbewerkingen toohello volume toobe geleverd, maar Hallo lokale momentopnamen is mogelijk ongeldig. Er is geen impact tooyour bestaande cloudmomentopnamen.

Hallo waarschuwing waarschuwing is toonotify kunt u dat een dergelijke situatie voordoen en zorg ervoor dat u Hallo dezelfde tijdig door ofwel het controleren van uw lokale momentopnamen plant u tootake minder frequente lokale momentopnamen of verwijderen oudere lokale momentopnamen die niet langer te houden Vereist.

Als de lokale momentopnamen Hallo ongeldig worden gemaakt, ontvangt u alarm informatie om u te informeren dat lokale momentopnamen voor de specifieke back-upbeleid Hallo Hallo zijn ongeldig gemaakt naast Hallo-lijst van tijdstempels van Hallo lokale momentopnamen die ongeldig zijn gemaakt. Deze momentopnamen worden automatisch verwijderd en kunt u niet meer kunnen tooview ze in Hallo **back-up catalogussen** pagina in Hallo klassieke Azure-portal.

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>Vragen over het converteren van een gelaagd volume tooa lokaal vastgemaakt volume
**V:** Ik ben sommige traagheid op Hallo apparaat geobserveerd tijdens het converteren van een gelaagd volume tooa lokaal vastgemaakt volume. Waarom is dit gebeurt? 

**A:** Hallo-conversieproces bestaat uit twee stappen: 

1. Het inrichten van ruimte op het Hallo-apparaat voor hello, snel-naar-worden-geconverteerd volume lokaal vastgemaakt.
2. Gelaagde gegevens downloaden vanaf Hallo cloud tooensure lokale gegarandeerd.

Beide stappen zijn lang met bewerkingen die afhankelijk van de grootte van de Hallo van Hallo-volume wordt geconverteerd zijn, gegevens op het Hallo-apparaat en de beschikbare bandbreedte. Als sommige gegevens van bestaande gelaagde volumes mogelijk toohello cloud worden gelekt als onderdeel van Hallo inrichtingsproces, kan uw apparaat verminderde prestaties tijdens deze periode optreden. Bovendien Hallo conversieproces duurt mogelijk als:

* Bestaande volumes zijn toohello cloud; geen back-ups zodat het is raadzaam om de dat back-up van uw eerdere tooinitiating een conversie van volumes.
* Bandbreedte, snelheidsbeperking beleidsregels zijn toegepast, kan die Hallo beschikbare bandbreedte toohello cloud; beperken Daarom raden we aan dat u hebt een speciale 40 Mbps of meer verbinding toohello cloud.
* Hallo kan conversie enkele uren duren vanwege toohello meerdere factoren uiteengezet; daarom het is raadzaam dat u deze bewerking niet pieken op tijdstippen of op een tooavoid weekend uitvoeren Hallo gevolgen voor de end-consumenten.

Meer informatie over het te[een gelaagd volume tooa lokaal vastgemaakt volume converteren](storsimple-manage-volumes-u2.md#change-the-volume-type)

**V:** Kan ik Hallo volume conversiebewerking annuleren?

**A:** Nee, kan niet u Hallo Hallo conversie annuleringsbewerking eenmaal is gestart. Zoals beschreven in de vorige vragen hello, zich van Hallo potentiële prestatieproblemen die u mogelijk bij het Hallo-proces stuit en volg de aanbevolen procedures Hallo die hierboven worden genoemd als u van plan uw conversie bent.

**V:** Wat gebeurt er toomy volume als Hallo conversiebewerking mislukt?

**A:** Volumeconversie kan mislukken vanwege problemen met de netwerkverbinding toocloud. Hallo-apparaat niet meer Hallo conversieproces uiteindelijk na een bepaald aantal mislukte pogingen toobring omlaag gelaagde gegevens uit Hallo cloud. In een dergelijk scenario Hallo volumetype toobe Hallo bron volume type voorafgaande tooconversion, wordt voortgezet en:

* Kritieke waarschuwing worden verhoogd toonotify u Hallo fout bij het converteren van het volume. Meer informatie over [gerelateerde toolocally vastgemaakt volumes waarschuwingen](storsimple-manage-alerts.md#locally-pinned-volume-alerts)
* Als u een gelaagde tooa lokaal vastgemaakt volume converteert, blijven Hallo volume tooexhibit eigenschappen van een gelaagd volume als gegevens mogelijk nog steeds op Hallo cloud staan. Het is raadzaam dat u problemen met Hallo en probeer vervolgens Hallo conversie opnieuw.
* Op dezelfde manier als de conversie van een lokaal vastgemaakt tooa gelaagd volume mislukt, hoewel Hallo volume wordt gemarkeerd als een lokaal vastgemaakt volume, werkt als een gelaagd volume (omdat de gegevens kan toohello cloud terechtgekomen). Deze blijven echter wel toooccupy ruimte op de lokale lagen Hallo Hallo-apparaat. Deze ruimte worden niet beschikbaar voor andere lokaal vastgemaakte volumes. Het is raadzaam dat u opnieuw proberen om deze bewerking tooensure dat Hallo volumeconversie voltooid is en Hallo lokale ruimte op Hallo apparaat kan worden vrijgemaakt.

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>Vragen over het herstellen van een lokaal vastgemaakt volume
**V:** Lokaal vastgemaakte volumes hersteld onmiddellijk?

**A:** Ja, lokaal vastgemaakte volumes zijn direct hersteld. Hallo-metagegevens voor Hallo volume is uit Hallo cloud opgehaald als onderdeel van de herstelbewerking hello, Hallo volume online is gebracht en zodra toegankelijk zijn voor het Hallo-host. Echter verlaagd lokale garanties met betrekking tot Hallo volume gegevens niet meer aanwezig totdat alle Hallo gegevens uit de cloud Hallo is gedownload en kunnen zich op de prestaties van deze volumes voor de duur van Hallo terugzetten Hallo.

**V:** Hoe lang duurt toorestore een lokaal vastgemaakt volume?

**A:** Lokaal vastgemaakte volumes zijn onmiddellijk teruggezet en online worden gebracht als u de informatie over de metagegevens van de Hallo volume wordt opgehaald uit Hallo cloud, terwijl de volumegegevens Hallo nog steeds toobe op Hallo achtergrond gedownload. Deze laatste gedeelte van het Hallo-herstelbewerking--om terug te zetten Hallo lokale garanties voor Hallo volumegegevens--is een langdurige bewerking en duurt enkele uren alle Hallo gegevens toobe lokale opnieuw gemaakt. Hallo tijd toocomplete hello dezelfde afhankelijk is van meerdere factoren, zoals het Hallo-grootte van het Hallo-volume wordt hersteld en Hallo beschikbare bandbreedte. Als u Hallo oorspronkelijke volume dat wordt hersteld, is verwijderd, extra tijd gaat toocreate Hallo lokale ruimte op Hallo-apparaat als onderdeel van Hallo restore-bewerking.

**V:** Moet ik mijn bestaande lokaal volume tooan oudere momentopname vastgemaakt (die is genomen wanneer Hallo volume is gelaagd) toorestore. Hallo volume worden hersteld als lagen in dit geval?

**A:** Nee, Hallo volume worden hersteld als een lokaal vastgemaakt volume. Hoewel Hallo momentopname datums toohello wanneer Hallo volume is gelaagd tijdens het herstellen van bestaande volumes StorSimple gebruikt altijd Hallo type volume op schijf Hallo omdat deze momenteel bestaat.

**V:** Ik mijn lokaal vastgemaakt volume onlangs hebt uitgebreid, maar moet nu toorestore Hallo gegevens tooa tijdstip waarop Hallo volume kleiner is. Wordt terugzetten van de grootte van het huidige volume Hallo en moet ik tooextend Hallo grootte van Hallo volume nadat de Hallo terugzetten is voltooid?

**A:** Ja, Hallo herstellen wordt de grootte van Hallo volume en moet u tooextend Hallo grootte van Hallo volume nadat Hallo terugzetten is voltooid.

**V:** Kan ik Hallo-type van een volume wijzigen tijdens het terugzetten?

**A.**Nee, u Hallo volumetype niet wijzigen tijdens het terugzetten.

* Volumes die zijn verwijderd zijn als Hallo type opgeslagen in momentopname Hallo hersteld.
* Bestaande volumes zijn hersteld op basis van hun huidige type, ongeacht het Hallo-type die zijn opgeslagen in momentopname Hallo (Zie de vorige twee toohello vragen).

**V:** Ik heb mijn lokaal vastgemaakt volume toorestore nodig, maar ik heb een onjuist punt in tijd momentopname. Kan ik Hallo huidige restore-bewerking annuleren?

**A:** Ja, kunt u een herstelbewerking continu annuleren. Hallo-status van Hallo volume wordt teruggedraaid toohello status aan begin Hallo van Hallo terugzetten. Er geen schrijfbewerkingen die zijn aangebracht toohello volume terwijl Hallo terugzetten werd uitgevoerd is verloren gegaan.

**V:** Ik een restore-bewerking op een van mijn lokaal vastgemaakte volumes gestart en wordt nu een momentopname wordt weergegeven in de catalogus van mijn achterstand die ik niet nu maken. Wat wordt dit gebruikt?

**A:** Dit is Hallo tijdelijke momentopname die eerdere toohello restore-bewerking is gemaakt en wordt gebruikt voor terugdraaien als Hallo terugzetten is geannuleerd of mislukt. Deze momentopname; niet verwijderen Deze worden automatisch verwijderd als Hallo herstellen voltooid is. Dit kan gebeuren als de hersteltaak alleen lokaal volumes of een combinatie van lokaal vastgemaakte en gelaagde volumes vastgemaakte is. Hallo hersteltaak alleen gelaagde volumes bevat, wordt wordt vervolgens dit gedrag niet uitgevoerd als.

**V:** Kan ik een lokaal vastgemaakt volume kloon?

**A:** Ja, kunt u. Hallo lokaal vastgemaakt volume wordt echter als een gelaagd volume standaard worden gekloond. Meer informatie over het te[een lokaal vastgemaakt volume klonen](storsimple-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>Vragen over mislukte via een lokaal vastgemaakt volume
**V:** Ik heb nodig toofail via mijn apparaat tooanother fysiek apparaat. Mijn lokaal vastgemaakte volumes mislukken dan lokaal vastgemaakt of gelaagde?

**A:** Afhankelijk van Hallo softwareversie van het doelapparaat hello, lokaal vastgemaakte volumes failover plaats als:

* Lokaal vastgemaakt als Hallo doelapparaat wordt uitgevoerd op StorSimple 8000 update series 2
* Gelaagde als Hallo doelapparaat wordt uitgevoerd op StorSimple bijwerken 8000 series 1.x
* Als het doelapparaat Hallo Hallo cloud toestel lagen (software-update voor versie 2 of 1.x bijwerken)

Meer informatie over [failover en DR van lokaal vastgemaakte volumes op versies van](storsimple-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**V:** Lokaal vastgemaakte volumes direct herstellen tijdens herstel na noodgeval (DR)?

**A:** Ja, lokaal vastgemaakte volumes zijn hersteld onmiddellijk tijdens failover. Hallo-metagegevens voor Hallo volume is uit Hallo cloud opgehaald als onderdeel van de failoverbewerking hello, Hallo volume online brengen op het doelapparaat Hallo en zodra toegankelijk zijn voor het Hallo-host. Ondertussen Hallo volumegegevens toodownload wordt voortgezet op de achtergrond Hallo en verminderde prestaties op deze volumes voor de duur van Hallo failover Hallo kunnen optreden.

**V:** Zie ik Hallo failover-taak is voltooid, hoe kan ik bijhouden Hallo voortgang van lokaal vastgemaakt volume dat wordt hersteld op het doelapparaat Hallo?

**A:** Tijdens een failoverbewerking Hallo failover-taak wordt als voltooid gemarkeerd wanneer alle Hallo volumes in Hallo failover set zijn onmiddellijk teruggezet en online brengen op Hallo doelapparaat. Dit omvat alle lokaal vastgemaakte volumes die mogelijk zijn via; is mislukt echter worden lokale garanties Hallo gegevens pas beschikbaar wanneer alle Hallo-gegevens voor Hallo volume is gedownload. U kunt deze voortgang voor elk lokaal vastgemaakt volume dat is mislukt door bewaking Hallo bijbehorende hersteltaken die zijn gemaakt als onderdeel van Hallo failover volgen. Deze het herstellen van afzonderlijke taken wordt alleen gemaakt voor lokaal vastgemaakte volumes.

**V:** Kan ik Hallo-type van een volume wijzigen tijdens de failover?

**A:** U kunt de Hallo volumetype Nee, niet wijzigen tijdens een failover. Als u via tooanother fysiek mislukken wordt apparaat met StorSimple 8000 serie update 2, Hallo volumes failover worden uitgevoerd op basis van Hallo volume dat is opgeslagen in momentopname Hallo. Wanneer failover tooany andere apparaatversie op een, raadpleegt u toohello vraag boven op Hallo volumetype na een failover.

**V:** Kan ik een volumecontainer met lokaal vastgemaakte volumes toohello cloud toestel failover?

**A:** Ja, kunt u. Hallo lokaal vastgemaakte volumes wordt als gelaagde volumes failover worden uitgevoerd. Meer informatie over [failover en DR van lokaal vastgemaakte volumes op versies van](storsimple-device-failover-disaster-recovery.md#considerations-for-device-failover)

