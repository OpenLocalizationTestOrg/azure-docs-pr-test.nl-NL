---
title: aaaStorSimple 8000 Series Update 2.2 release-opmerkingen | Microsoft Docs
description: Beschrijft de nieuwe functies hello, problemen en tijdelijke oplossingen voor StorSimple 8000 Series Update 2.2.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5cf03ea8-2a0f-4552-b6dc-7ea517783d7b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/18/2016
ms.author: alkohli
ms.openlocfilehash: a2902126f4011fa9ade64f63a8abdec095874fb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-22-release-notes"></a>StorSimple 8000 Series Update 2.2 release-opmerkingen
## <a name="overview"></a>Overzicht
Hallo volgende releaseopmerkingen beschrijven Hallo nieuwe functies en Hallo kritieke open problemen identificeren voor StorSimple 8000 Series Update 2.2. Ze bevatten ook een lijst met software-updates voor Hallo StorSimple is opgenomen in deze release. 

Update 2.2 kan worden toegepast tooany StorSimple-apparaat met Release (GA) of Update 0.1 via Update 2.1. Hallo apparaatversie die is gekoppeld aan Update 2.2 is 6.3.9600.17708.

Controleer Hallo gegevens in Hallo release notes voordat u Hallo implementeert in uw StorSimple-oplossing bijwerken.

> [!IMPORTANT]
> * 2.2-update heeft alleen software-updates. Het duurt ongeveer 1,5 tot 2 uur tooinstall deze update. 
> * Als u Update 2.1 worden uitgevoerd, raden wij aan dat u de Update 2.2 zo snel mogelijk toepassen.
> * Voor nieuwe releases, kunnen er geen updates onmiddellijk omdat we een gefaseerde implementatie van updates Hallo doen. Wacht een paar dagen en vervolgens zoeken naar updates opnieuw als deze is binnenkort beschikbaar.
> 
> 

## <a name="whats-new-in-update-22"></a>Wat is er nieuw in Update 2.2
Hallo zijn volgende belangrijke verbeteringen aangebracht in Update 2.2.

* **Ruimte vrijmaken optimalisatie geautomatiseerde** – wanneer gegevens worden verwijderd op dun ingerichte volumes hello ongebruikte opslagruimte adresblokken moet toobe vrijgemaakt. Deze release heeft verbeterde Hallo ruimte vrijmaken proces uit Hallo cloud waardoor Hallo ongebruikte ruimte worden beschikbare sneller als vergeleken toohello vorige versies.
* **Prestatieverbeteringen momentopname** – Update 2.2 heeft verbeterde Hallo tijd tooprocess een cloudmomentopname van een in bepaalde scenario's waarin grote volumes worden gebruikt en er is minimaal toono gegevensverloop. Een scenario dat u van deze uitbreiding profiteren wilt zou Hallo archief volumes zijn.
* **Beperken van ondersteuningspakket verzamelen** : Er zijn verbeteringen in Hallo manier Hallo ondersteuningspakket is verzameld en worden geüpload in deze release. 
* **Bijwerken van verbeteringen van de betrouwbaarheid** – deze release bevat oplossingen voor problemen die in een verbeterde betrouwbaarheid van de Update resulteren.

## <a name="issues-fixed-in-update-22"></a>Problemen in Update 2.2 opgelost
Hallo na tabellen bevat een samenvatting van problemen die Updates 2.2 en 2.1 zijn opgelost.    

| Nee | Functie | Probleem | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- |
| 1 |Host-prestaties |In Hallo eerder release, hostzijde prestatieproblemen zijn waargenomen tijdens het maken van een lokaal vastgemaakt volume Hallo en tijdens de conversie op Hallo van een gelaagd volume tooa lokaal vastgemaakt volume. Deze problemen zijn opgelost in deze release waardoor wat leidt tot een verbetering van de prestaties van de Hallo host tijdens Hallo volume maken en de conversie-procedures. |Ja |Nee |
| 2 |Lokaal vastgemaakte volumes |In zeldzame gevallen zou Hallo systeem vastlopen bij het maken van een lokaal vastgemaakt volume. Deze fout is verholpen in deze release. |Ja |Nee |
| 3 |lagen |Er zijn sporadisch loopt vast bij het Hallo-metagegevens voor Hallo StorSimple Cloud toestellen (8010 en 8020) lagen te Hallo cloud. Dit probleem is opgelost in deze release. |Nee |Ja |
| 4 |Het maken van momentopnamen |Er zijn problemen met gerelateerde toohello maken van incrementele momentopnamen in scenario's met grote volumes en minimale toono gegevensverloop. Deze problemen zijn opgelost in deze release. |Ja |Ja |
| 5 |Openstack verificatie |Wanneer u Openstack als cloudserviceprovider hello, Hallo gebruiker zou uitvoeren in een gerelateerde toohello incidentele bug authenticatie waarbij Hallo JSON parser resulteerde in een crash. Dit probleem wordt opgelost in deze release. |Ja |Nee |
| 6 |Host-zijde kopiëren |In eerdere versies van software met een bug incidentele gerelateerd toohello ODX timing is gedetecteerd bij het kopiëren van gegevens Hallo van één volume tooanother volume. Dit resulteert in een failover van de domeincontroller en Hallo-systeem kan mogelijk gaat u in de herstelmodus overgaat. Dit probleem wordt opgelost in deze release. |Ja |Nee |
| 7 |Windows Management Instrumentation (WMI) |In eerdere versies Hallo van software, er zijn meerdere exemplaren van web proxy mislukt met uitzondering van Hallo '<ManagementException> fout bij het laden van Provider '. Deze fout is te wijten tooa WMI-geheugenlek en is nu opgelost. |Ja |Nee |
| 8 |Update |In bepaalde uitzonderlijke gevallen in eerdere versies van software, Hallo ontvangen Hallo gebruiker een 'CisPowershellHcsscripterror' wanneer u probeert tooscan of installatie-updates. Dit probleem is opgelost in deze release. |Ja |Ja |
| 9 |Ondersteuningspakket |In deze release zijn er verbeteringen toohello manier Hallo ondersteuningspakket is verzameld en worden geüpload. |Ja |Ja |

## <a name="known-issues-in-update-22"></a>Bekende problemen in Update 2.2
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

## <a name="controller-and-firmware-updates-in-update-22"></a>Controller en firmware-updates in de Update 2.2
Deze release heeft alleen uit software-updates. Echter, als u een eerdere tooUpdate van versie 2 bijwerkt, moet u tooinstall stuurprogramma Storport, Spaceport, en (in sommige gevallen) schijf firmware-updates op uw apparaat.

Voor meer informatie over hoe tooinstall Hallo stuurprogramma, Storport Spaceport en schijf firmware-updates, Zie [installeren Update 2.2](storsimple-install-update-21.md) op uw StorSimple-apparaat.

## <a name="virtual-device-updates-in-update-22"></a>Virtueel apparaat-updates in de Update 2.2
Deze update kan niet worden toegepast toohello virtueel apparaat. Nieuwe virtuele apparaten moet toobe gemaakt. 

## <a name="next-step"></a>Volgende stap
Meer informatie over hoe te[installeren Update 2.2](storsimple-install-update-21.md) op uw StorSimple-apparaat.

