---
title: Opmerkingen bij de release van de aaaStorSimple 8000 Series Update 3 | Microsoft Docs
description: Beschrijft de nieuwe functies hello, problemen en tijdelijke oplossingen voor StorSimple 8000 Series Update 3.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 2158aa7a-4ac3-42ba-8796-610d1adb984d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5bfcba61f7f210531437f650eafaad4dbd8c7c45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-3-release-notes-for-your-storsimple-8000-series-device"></a>3 release-opmerkingen voor uw StorSimple 8000 serie-apparaat bijwerken

## <a name="overview"></a>Overzicht
Hallo volgende releaseopmerkingen beschrijven Hallo nieuwe functies en Hallo kritieke open problemen identificeren voor StorSimple 8000 Series Update 3. Ze bevatten ook een lijst met software-updates voor Hallo StorSimple is opgenomen in deze release. 

Update 3 kan worden toegepast tooany StorSimple-apparaat met Release (GA) of Update 0.1 via Update 2.2. Hallo apparaatversie die is gekoppeld met Update 3 is 6.3.9600.17759.

Controleer Hallo gegevens in Hallo release notes voordat u Hallo implementeert in uw StorSimple-oplossing bijwerken.

> [!IMPORTANT]
> * Update 3 is apparaatsoftware, LSI stuurprogramma en firmware en Storport en Spaceport werkt. Het duurt ongeveer 1,5 tot 2 uur tooinstall deze update. 
> * Voor nieuwe releases, kunnen er geen updates onmiddellijk omdat we een gefaseerde implementatie van updates Hallo doen. Wacht een paar dagen en vervolgens zoeken naar updates opnieuw als deze is binnenkort beschikbaar.
> 
> 

## <a name="whats-new-in-update-3"></a>Wat is er nieuw in Update 3
Hallo zijn volgende belangrijke verbeteringen en correcties aangebracht in Update 3.

* **Ruimte vrijmaken wijzigingen geautomatiseerde** – vanaf Update 3 Hallo ruimte vrijmaken algoritmen uitvoeren op Hallo stand-by-controller van Hallo systeem, wat leidt tot sneller wordt uitgevoerd. Raadpleeg voor meer informatie over het Hallo-poorten die vereist toowork met vrijmaken van ruimte zijn, toohello [StorSimple netwerkvereisten](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* **Prestatieverbeteringen** – Update 3 lezen-schrijven prestaties toohello cloud is verbeterd.
* **Verbeteringen migratiegerelateerde** : In deze release bug verschillende oplossingen en verbeteringen zijn gedaan voor Hallo migratiefunctie van 5000/7000-serie apparaten too8000 reeks apparaten. Voor meer informatie over hoe toouse migratiefunctie hello, gaat u te[migratie van 5000/7000-serie apparaat too8000 reeks apparaat](https://gallery.technet.microsoft.com/Azure-StorSimple-50007000-c1a0460b). 
* **Verwante oplossingen bewaking** - In deze release fouten gerelateerd toomonitoring grafieken, servicedashboard en apparaat dashboard zijn opgelost.

## <a name="issues-fixed-in-update-3"></a>Problemen opgelost met Update 3
Hallo na tabellen bevat een samenvatting van problemen die zijn verholpen in Update 3.    

| Nee | Functie | Probleem | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- |
| 1 |Host-zijde gegevensmigratie |In Hallo is oudere versie, Hallo StorSimple Cloud toestel gaat offline tijdens een gegevensmigratie van de host-zijde. Dit probleem is opgelost in deze release. |Nee |Ja |
| 2 |Lokaal vastgemaakte volumes |In de vorige release hello, moet u er problemen verwante tooI/O-fouten, volume conversie storingen en fouten gegevenspad voor lokaal vastgemaakte volumes zijn. Deze problemen zijn hoofdmap veroorzaakt en vaste in deze release. |Ja |Nee |
| 3 |Bewaking |Er zijn meerdere problemen gerelateerde tooreporting eenheden en bewaking evenals apparaat dashboard grafieken waar onjuiste informatie is weergegeven voor lokaal vastgemaakte volumes. Deze problemen zijn opgelost in deze release. |Ja |Nee |
| 4 |I/o zware schrijfbewerkingen |Wanneer u StorSimple voor werkbelastingen met betrekking tot zware schrijfbewerkingen, Hallo gebruiker zou uitvoeren in een bug incidentele Hallo werkset is waar wordt lagen in Hallo cloud. Dit probleem wordt opgelost in deze release. |Ja |Ja |
| 5 |Back-up |In bepaalde uitzonderlijke gevallen in eerdere versies van software, Hallo wanneer de gebruiker heeft een back-up van een externe kloon, ze zouden worden uitgevoerd in de cloud-fouten en Hallo bewerking zou fout optreedt. In deze release Hallo probleem is opgelost en Hallo-bewerking is voltooid. |Ja |Ja |
| 6 |Back-upbeleid |In bepaalde uitzonderlijke gevallen in Hallo eerdere releases van software, moet u er een fout is gerelateerd toohello verwijdering van de back-upbeleid. Dit probleem is opgelost in deze release. |Ja |Ja |

## <a name="known-issues-in-update-3"></a>Bekende problemen in Update 3
Hallo volgende tabel bevat een samenvatting van bekende problemen in deze release.

| Nee. | Functie | Probleem | Opmerkingen / tijdelijke oplossing | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- | --- |
| 1 |Schijf quorum |In zeldzame gevallen, als Hallo meerderheid van de schijven in Hallo EBOD behuizing van een 8600-apparaat niet zijn verbonden met waardoor geen quorum schijf gaat vervolgens Hallo opslaggroep offline. Blijft deze offline zelfs als Hallo schijven opnieuw worden verbonden. |U moet tooreboot Hallo apparaat. Als Hallo probleem zich blijft voordoen, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 2 |Onjuiste besturings-ID |Als een vervangende domeincontroller wordt uitgevoerd, kan controller 0 als controller 1 weergegeven. Tijdens de vervanging van de domeincontroller, wanneer Hallo afbeelding is geladen vanuit Hallo peer-knooppunt, Hallo besturings-ID kan worden weergegeven in eerste instantie als Hallo peer controller-ID. In zeldzame gevallen kan worden dit probleem ook gezien na opnieuw opstarten. |Er is geen gebruikersactie vereist. Deze situatie wordt automatisch opgelost nadat Hallo controller vervanging voltooid is. |Ja |Nee |
| 3 |Opslagaccounts |Hallo Opslagaccount service toodelete Hallo opslag gebruikt, is een niet-ondersteund scenario. Dit leidt tooa situatie waarin de gebruikersgegevens kan niet worden opgehaald. | |Ja |Ja |
| 4 |Failover van apparaat |Meerdere failovers van een volumecontainer van Hallo dezelfde bron toodifferent apparaat doelapparaten wordt niet ondersteund. Failover van een enkel dode apparaat toomultiple apparaten brengt Hallo volumecontainers op Hallo eerst failover apparaat is Gegevenseigendom gaan verloren. Na een failover wordt deze volumecontainers worden weergegeven of zich anders gedragen wanneer u ze in de klassieke Azure-portal Hallo weergeeft. | |Ja |Nee |
| 5 |Installeren |Tijdens het StorSimple-Adapter voor SharePoint-installatie moet u tooprovide een apparaat IP-adres om Hallo installeren toofinish is. | |Ja |Nee |
| 6 |Webproxy |Als uw webproxyconfiguratie HTTPS als Hallo opgegeven protocol, en vervolgens uw communicatie apparaat-naar-service worden beïnvloed en Hallo apparaat gaat offline. Ondersteuningspakketten wordt ook gegenereerd in Hallo proces, verbruikt behoorlijk aanspraak op uw apparaat. |Zorg ervoor dat Hallo web proxy-URL bevat HTTP als Hallo opgegeven protocol. Voor meer informatie gaat te[webproxy voor uw apparaat configureren](storsimple-configure-web-proxy.md). |Ja |Nee |
| 7 |Webproxy |Als u configureert en webproxy op een geregistreerd apparaat inschakelt, wordt u toorestart Hallo actieve controller moet op uw apparaat. | |Ja |Nee |
| 8 |Cloud hoge latentie en hoge i/o-werkbelasting |Wanneer uw StorSimple-apparaat een combinatie van zeer hoge cloud latenties (volgorde van seconden) en de hoge i/o-belasting tegenkomt, gaat u Hallo apparaat volumes in een gedegradeerde status en Hallo i/o's mislukken met een 'apparaat niet gereed'-fout. |Toomanually opnieuw opstarten Hallo apparaatcontrollers wordt of u een apparaat failover toorecover uitvoeren vanuit deze situatie. |Ja |Nee |
| 9 |Azure PowerShell |Wanneer u Hallo StorSimple-cmdlet gebruikt **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - eerst 1 - wacht** tooselect Hallo eerste object zodat u kunt een nieuwe maken **VolumeContainer** object Hallo cmdlet retourneert alle Hallo-objecten. |Hallo-cmdlet als volgt haakjes inpakt: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - eerst 1 - wachttijd** |Ja |Ja |
| 10 |Migratie |Wanneer meerdere volumecontainers worden doorgegeven voor migratie, is Hallo ETA voor de meest recente back-up alleen voor de eerste volumecontainer Hallo nauwkeurige. Bovendien start parallelle migratie nadat hello eerste 4 back-ups in de eerste volumecontainer Hallo zijn gemigreerd. |Het is raadzaam dat u een volumecontainer tegelijk migreren. |Ja |Nee |
| 11 |Migratie |Na het terugzetten van Hallo volumes niet toohello back-beleid of Hallo virtuele schijfgroep toegevoegd. |U moet deze volumes tooa back-upbeleid in volgorde toocreate back-ups tooadd. |Ja |Ja |
| 12 |Migratie |Nadat het Hallo-migratie is voltooid, Hallo 5000/7000-serie apparaat moet geen toegang krijgen tot Hallo gegevenscontainers gemigreerd. |Het is raadzaam dat u Hallo verwijdert gegevenscontainers gemigreerd nadat Hallo migratie voltooid en doorgevoerd is. |Ja |Nee |
| 13 |Kloon en Noodherstel |Een StorSimple-apparaat met Update 1 kan niet klonen of uitvoeren disaster recovery tooa apparaat vóór update 1 software die wordt uitgevoerd. |U moet tooupdate Hallo doel apparaat tooUpdate 1 tooallow deze bewerkingen |Ja |Ja |
| 14 |Migratie |Configuratieback-up voor de migratie kan op een apparaat 5000 7000-serie mislukken wanneer er groepen met geen gekoppelde volumes volume zijn. |Alle Hallo leeg volume groepen met geen gekoppelde volumes verwijderen en probeer vervolgens Hallo configuratieback-up. |Ja |Nee |
| 15 |Azure PowerShell-cmdlets en lokaal vastgemaakte volumes |U kunt een lokaal vastgemaakt volume via Azure PowerShell-cmdlets kan niet maken. (Alle volumes die u via Azure PowerShell maakt worden gelaagd.) |Gebruik altijd Hallo StorSimple Manager-service tooconfigure lokaal vastgemaakte volumes. |Ja |Nee |
| 16 |Beschikbare schijfruimte voor het lokaal vastgemaakte volumes |Als u een lokaal vastgemaakt volume verwijdert, worden Hallo beschikbare schijfruimte voor het nieuwe volumes mogelijk niet meteen bijgewerkt. Hallo StorSimple Manager-service-updates Hallo lokale ruimte beschikbaar ongeveer om het uur. |Wacht tot een uur voordat u toocreate Hallo nieuw volume probeert. |Ja |Nee |
| 17 |Lokaal vastgemaakte volumes |De hersteltaak beschrijft Hallo tijdelijke momentopnameback-up in Hallo back-upcatalogus, maar alleen voor Hallo duur van de hersteltaak Hallo. Bovendien beschrijft de virtuele schijf wordt een groep met voorvoegsel **tmpCollection** op Hallo **back-upbeleid** pagina, maar alleen voor de duur van de Hallo Hallo terugzetten taak. |Dit kan gebeuren als de hersteltaak alleen lokaal volumes of een combinatie van lokaal vastgemaakte en gelaagde volumes vastgemaakte is. Hallo hersteltaak alleen gelaagde volumes bevat, wordt wordt vervolgens dit gedrag niet uitgevoerd als. Er is geen tussenkomst van de gebruiker is vereist. |Ja |Nee |
| 18 |Lokaal vastgemaakte volumes |Als u een hersteltaak annuleren en een failover controller optreedt onmiddellijk daarna Hallo hersteltaak ziet **mislukt** in plaats van **geannuleerd**. Als een hersteltaak mislukt en een failover controller optreedt onmiddellijk daarna Hallo hersteltaak ziet **geannuleerd** in plaats van **mislukt**. |Dit kan gebeuren als de hersteltaak alleen lokaal volumes of een combinatie van lokaal vastgemaakte en gelaagde volumes vastgemaakte is. Hallo hersteltaak alleen gelaagde volumes bevat, wordt wordt vervolgens dit gedrag niet uitgevoerd als. Er is geen tussenkomst van de gebruiker is vereist. |Ja |Nee |
| 19 |Lokaal vastgemaakte volumes |Als u een hersteltaak annuleert of als een terugzetbewerking uitvalt en vervolgens een controller-failover wordt uitgevoerd, een extra hersteltaak wordt weergegeven op Hallo **taken** pagina. |Dit kan gebeuren als de hersteltaak alleen lokaal volumes of een combinatie van lokaal vastgemaakte en gelaagde volumes vastgemaakte is. Hallo hersteltaak alleen gelaagde volumes bevat, wordt wordt vervolgens dit gedrag niet uitgevoerd als. Er is geen tussenkomst van de gebruiker is vereist. |Ja |Nee |
| 20 |Lokaal vastgemaakte volumes |Als u een gelaagd volume (gemaakt en gekloonde met Update 1.2 of eerder) tooconvert probeert tooa lokaal vastgemaakt volume en uw apparaat is bijna geen schijfruimte meer of er is een onderbreking van de cloud en hello clone(s) beschadigd kunnen raken. |Dit probleem treedt alleen op volumes die gemaakt en gekloonde met vooraf Update 2.1-software zijn. Dit moet een incidentele scenario. | | |
| 21 |Volumeconversie |Hallo ACRs gekoppelde tooa volume niet bijwerken tijdens een volumeconversie van het uitgevoerd wordt (gelaagde toolocally vastgemaakt of andersom). Hallo ACRs bijwerken kan leiden tot beschadiging van gegevens. |Indien nodig, Hallo ACRs voorafgaande toohello volumeconversie bijwerken en maak geen verdere ACR updates terwijl Hallo conversie uitgevoerd wordt. | | |
| 22 |Updates |Bij het toepassen van Update 3 Hallo **onderhoud** pagina in hello Azure classic portal wordt weergeven Hallo volgende message gerelateerde tooUpdate 2 - ' StorSimple 8000 series Update 2 Hallo mogelijkheid bevat voor Microsoft tooproactively verzamelen logboekgegevens van uw apparaat wanneer we potentiële problemen detecteren'. Dit is misleidend zoals betekent dit dat het Hallo-apparaat wordt bijgewerkt tooUpdate 2. Nadat het Hallo-apparaat is bijgewerkt succeesfully tooUpdate 3, verdwijnt dit bericht. |Dit probleem wordt opgelost in een toekomstige release. |Ja |Nee |

## <a name="controller-and-firmware-updates-in-update-3"></a>Controller en firmware-updates in de Update 3
Deze release is LSI stuurprogramma en firmware-updates. Voor meer informatie over hoe tooinstall Hallo LSI stuurprogramma's en firmware-updates, Zie [installeren Update 3](storsimple-install-update-3.md) op uw StorSimple-apparaat.

## <a name="virtual-device-updates-in-update-3"></a>Virtueel apparaat-updates in de Update 3
Deze update kan niet worden toegepast toohello StorSimple Cloud toestel (ook wel bekend als Hallo virtueel apparaat). Nieuwe virtuele apparaten moet toobe gemaakt. 

## <a name="next-step"></a>Volgende stap
Meer informatie over hoe te[installeren Update 3](storsimple-install-update-3.md) op uw StorSimple-apparaat.

