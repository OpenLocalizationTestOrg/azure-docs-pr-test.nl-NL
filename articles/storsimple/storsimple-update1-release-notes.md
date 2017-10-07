---
title: aaaStorSimple 8000 Series Update 1.2 release-opmerkingen | Microsoft Docs
description: Beschrijft de nieuwe functies hello, problemen en tijdelijke oplossingen voor StorSimple 8000 Series Update 1.2.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>1.2 release-opmerkingen voor uw StorSimple 8000 serie-apparaat bijwerken

## <a name="overview"></a>Overzicht
Hello volgende releaseopmerkingen beschrijven Hallo nieuwe functies en kritieke open problemen Hallo voor StorSimple 8000 Series Update 1.2 identificeren. Ze bevatten ook een lijst van Hallo StorSimple software, stuurprogramma en schijf firmware-updates is opgenomen in deze release. 

Update 1.2 kan worden toegepast tooany StorSimple-apparaat met Release (GA), Update 0.1, Update 0.2 of Update 0.3-software. Update 1.2 is niet beschikbaar als uw apparaat met Update 1 of Update 1.1. Als u uw apparaat wordt uitgevoerd Release (GA), neemt u [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) tooassist u met deze update installeert.

Hallo tabel lijsten Hallo apparaat softwareversies overeenkomt tooUpdates 1, 1.1 en 1.2 te volgen.

| Als de update wordt uitgevoerd... | Dit is de versie van uw apparaat software. |
| --- | --- |
| 1.2 bijwerken |6.3.9600.17584 |
| 1.1 bijwerken |6.3.9600.17521 |
| Update 1.0 |6.3.9600.17491 |

Controleer Hallo gegevens in Hallo release notes voordat u Hallo implementeert in uw StorSimple-oplossing bijwerken. Voor meer informatie Zie hoe te[Update 1.2 installeren op uw StorSimple-apparaat](storsimple-install-update-1.md). 

> [!IMPORTANT]
> * Het duurt ongeveer 5 tot 10 uur tooinstall deze update (inclusief Hallo Windows-Updates). 
> * 1.2-update heeft software, LSI stuurprogramma en schijf firmware-updates. tooinstall, volg de instructies in Hallo in [Update 1.2 installeren op uw StorSimple-apparaat](storsimple-install-update-1.md).
> * Voor nieuwe releases, kunnen er geen updates onmiddellijk omdat we een gefaseerde implementatie van updates Hallo doen. Zoeken naar updates in een paar dagen opnieuw als deze is binnenkort beschikbaar.
> 
> 

## <a name="whats-new-in-update-12"></a>Wat is er nieuw in Update 1.2
Deze functies zijn voor het eerst uitgebracht met Update 1 die aangebracht beschikbaar tooa beperkte groep gebruikers is. Hallo StorSimple gebruikers de meeste ziet met de release van Update 1.2 Hallo Hallo volgende nieuwe functies en verbeteringen:

* **Migratie van de apparaten van 5000 7000-serie too8000 reeks** – deze release introduceert een nieuwe migratiefunctie waarmee Hallo StorSimple 5000 7000 series toestel gebruikers toomigrate hun gegevens tooa StorSimple 8000 series fysieke apparaat of een virtueel apparaat. Hallo migratiefunctie heeft twee belangrijkste waardevoorstellen:                                                                  
  
  * **Zakelijke continuïteit**, doordat de migratie van bestaande gegevens op 5000 7000-serie toestellen too8000 reeks apparaten.
  * **Verbeterde functie aanbiedingen van Hallo 8000 series apparaten**, zoals efficiënt gecentraliseerd beheer van meerdere apparaten via de StorSimple Manager-service voor een betere klasse van hardware en firmware, virtuele apparaten, gegevensmobiliteit bijgewerkt en functies in toekomstige roadmap Hallo.
    
    Raadpleeg toohello [Migratiehandleiding](http://www.microsoft.com/download/details.aspx?id=47322) voor meer informatie over het toomigrate een StorSimple 5000 7000-serie tooan 8000 series-apparaat. 
* **Beschikbaarheid in hello Azure Government Portal** – StorSimple is nu beschikbaar in hello Azure Government portal. Zie hoe te[implementeren van een StorSimple-apparaat in hello Azure Government Portal](storsimple-deployment-walkthrough-gov.md).
* **Ondersteuning voor andere cloudserviceproviders** – hello andere cloudserviceproviders ondersteund Amazon S3, Amazon S3 met RRS, HP en OpenStack (bèta) zijn.
* **Bijwerken van toolatest Storage-API's** – met deze versie StorSimple is bijgewerkt toohello meest recente Azure Storage-service API's. StorSimple 8000 series apparaten die worden uitgevoerd vóór het bijwerken 1 softwareversies (Release 0,1 0,2 en 0,3) met een versie van Azure Storage-Service-API's ouder is dan 17 juli 2009 Hallo. Zoals vermeld in de Hallo bijgewerkt [aankondiging over het verwijderen van opslag-versies](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx), door 1 augustus 2016 krijgen deze API wordt afgeschaft. Het is noodzakelijk dat u van toepassing hello StorSimple 8000 Series Update 1 eerdere tooAugust 1, 2016. Als u toodo zo niet, meer StorSimple-apparaten correct werkt.
* **Ondersteuning voor Zone redundante opslag (ZRS)** – met Hallo upgrade toohello meest recente versie van Hallo Storage-API's, Zone redundante opslag (ZRS) in toevoeging tooLocally redundante opslag (LRS) en geografisch redundante Hallo StorSimple 8000 series ondersteunt Opslag (GRS). Raadpleeg toothis [artikel op Azure redundantie opslagopties](../storage/common/storage-redundancy.md) voor ZRS meer informatie.
* **Verbeterde ervaring voor initiële implementeren en bijwerken** : In deze release Hallo installatie en processen van de update zijn verbeterd. Hallo installatie via de wizard setup hello wordt Verbeterde tooprovide feedback toohello gebruiker als Hallo netwerk configuratie en firewall-instellingen onjuist zijn. Aanvullende diagnostische cmdlets hebt opgegeven toohelp u bij het oplossen van netwerken van Hallo-apparaat. Zie Hallo [probleemoplossing implementatie artikel](storsimple-troubleshoot-deployment.md) voor meer informatie over diagnostische nieuwe cmdlets van hello worden gebruikt voor het oplossen van problemen.

## <a name="issues-fixed-in-update-12"></a>Problemen in Update 1.2 opgelost
Hallo volgende tabel bevat een samenvatting van problemen die Updates 1.2, 1.1 en 1 zijn opgelost.    

| Nee. | Functie | Probleem | Opgelost in Update | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- | --- |
| 1 |Windows PowerShell voor StorSimple |Wanneer een gebruiker Hallo StorSimple-apparaat op afstand toegang te krijgen met Windows PowerShell voor StorSimple en vervolgens de wizard setup Hallo worden gestart, wordt een crash zo snel Data 0 IP is ingevoerd is opgetreden. Deze fout is nu opgelost in Update 1. |Update 1 |Ja |Ja |
| 2 |Fabrieksinstellingen terugzetten |In sommige gevallen, wanneer u de fabrieksinstellingen terug te zetten, uitgevoerd Hallo StorSimple-apparaat is vastgelopen en dit bericht weergegeven: **toofactory opnieuw instellen wordt uitgevoerd (fase 8)**. Dit het geval als u op CTRL + C gedrukt terwijl Hallo cmdlet werd uitgevoerd. Deze fout is nu hersteld. |Update 1 |Ja |Nee |
| 3 |Fabrieksinstellingen terugzetten |Nadat een factory is mislukt, dubbele domeincontroller opnieuw hebt ingesteld, kunt u tooproceed met de apparaatregistratieservice zijn toegestaan. Dit resulteert in een niet-ondersteunde systeemconfiguratie. Een foutbericht wordt weergegeven in Update 1 en registratie is geblokkeerd op een apparaat dat een mislukte op Fabrieksinstellingen terugzetten is. |Update 1 |Ja |Nee |
| 4 |Fabrieksinstellingen terugzetten |In sommige gevallen zijn false positief verschil waarschuwingen gegenereerd. Op apparaten met Update 1 wordt niet langer onjuist verschil waarschuwingen gegenereerd. |Update 1 |Ja |Nee |
| 5 |Fabrieksinstellingen terugzetten |Fabrieksinstellingen is onderbroken voorafgaande toocompletion Hallo herstelmodus apparaat ingevoerd als staat niet toe dat u tooaccess Windows PowerShell voor StorSimple. Deze fout is nu hersteld. |Update 1 |Ja |Nee |
| 6 |Herstel na noodgevallen |Een disaster recovery (DR)-fout is verholpen waarin DR tijdens de detectie van back-ups op het doelapparaat Hallo Hallo mislukken. |Update 1 |Ja |Ja |
| 7 |Bewaking LED 's |In bepaalde gevallen LED's Hallo achterzijde toestel bewaking niet gespecificeerd juiste status. Hallo blauw LED is uitgeschakeld. DATA 0 en 1 LED's van gegevens zijn knippert zelfs wanneer deze interfaces niet zijn geconfigureerd. Hallo-probleem is opgelost en bewaking LED's nu geven aan de juiste status Hallo. |Update 1 |Ja |Nee |
| 8 |Bewaking LED 's |In bepaalde gevallen wordt na het toepassen van Update 1 Hallo blauw licht op Hallo actieve controller uitgeschakeld waardoor harde tooidentify Hallo actieve controller. Dit probleem is verholpen in deze release van de patch. |1.2 bijwerken |Ja |Nee |
| 9 |Netwerkinterfaces |In eerdere versies van kan een StorSimple-apparaat dat is geconfigureerd met een niet-routeerbare gateway offline gaan. In deze release is Hallo routering metriek voor Data 0 gedaan Hallo laagste; zelfs als andere netwerkinterfaces ingeschakeld voor de cloud zijn, wordt er daarom alle Hallo cloud-verkeer van Hallo apparaat worden gerouteerd via Data 0. |Update 1 |Ja |Ja |
| 10 |Back-ups |Een fout in Update 1, die de back-ups toofail heeft veroorzaakt nadat 24 dagen is verholpen in Hallo patch vrijgeven Update 1.1. |1.1 bijwerken |Ja |Ja |
| 11 |Back-ups |Een bug in eerdere versies heeft geleid tot slechte prestaties voor cloudmomentopnamen van met lage wijziging tarieven. Deze fout is verholpen in deze release van de patch. |1.2 bijwerken |Ja |Ja |
| 12 |Updates |In deze release van de patch is een fout in Update 1, die een mislukte upgrade gemeld en Hallo domeincontrollers toogo veroorzaakt in de herstelmodus overgaat opgelost. |1.2 bijwerken |Ja |Ja |

## <a name="known-issues-in-update-12"></a>Bekende problemen in Update 1.2
Hallo volgende tabel bevat een samenvatting van bekende problemen in deze release.

| Nee. | Functie | Probleem | Opmerkingen/tijdelijke oplossing | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- | --- |
| 1 |Schijf quorum |In zeldzame gevallen, als Hallo meerderheid van de schijven in Hallo EBOD behuizing van een 8600-apparaat niet zijn verbonden met waardoor geen quorum schijf vervolgens Hallo opslaggroep worden offline. Blijft deze offline zelfs als Hallo schijven opnieuw worden verbonden. |U moet tooreboot Hallo apparaat. Als Hallo probleem zich blijft voordoen, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 2 |Onjuiste besturings-ID |Als een vervangende domeincontroller wordt uitgevoerd, kan controller 0 als controller 1 weergegeven. Tijdens de vervanging van de domeincontroller, wanneer Hallo afbeelding is geladen vanuit Hallo peer-knooppunt, Hallo besturings-ID kan worden weergegeven in eerste instantie als Hallo peer controller-ID. In zeldzame gevallen kan worden dit probleem ook gezien na opnieuw opstarten. |Er is geen gebruikersactie vereist. Deze situatie wordt automatisch opgelost nadat Hallo controller vervanging voltooid is. |Ja |Nee |
| 3 |Opslagaccounts |Hallo Opslagaccount service toodelete Hallo opslag gebruikt, is een niet-ondersteund scenario. Dit leidt tooa situatie waarin de gebruikersgegevens kan niet worden opgehaald. |Ja |Ja | |
| 4 |Failover van apparaat |Meerdere failovers van een volumecontainer van Hallo dezelfde bron toodifferent apparaat doelapparaten wordt niet ondersteund. Failover van een enkel dode apparaat toomultiple apparaten apparaat brengt Hallo volumecontainers op Hallo eerst failover apparaat is Gegevenseigendom gaan verloren. Na een failover wordt deze volumecontainers worden weergegeven of zich anders gedragen wanneer u ze in de klassieke Azure-portal Hallo weergeeft. | |Ja |Nee |
| 5 |Installeren |Tijdens het StorSimple-Adapter voor SharePoint-installatie moet u tooprovide een apparaat IP-adres om Hallo installeren toofinish is. | |Ja |Nee |
| 6 |Webproxy |Als uw webproxyconfiguratie HTTPS als Hallo opgegeven protocol, en vervolgens uw communicatie apparaat-naar-service worden beïnvloed en Hallo apparaat gaat offline. Ondersteuningspakketten wordt ook gegenereerd in Hallo proces, verbruikt behoorlijk aanspraak op uw apparaat. |Zorg ervoor dat Hallo web proxy-URL bevat HTTP als Hallo opgegeven protocol. Voor meer informatie gaat te[webproxy voor uw apparaat configureren](storsimple-configure-web-proxy.md). |Ja |Nee |
| 7 |Webproxy |Als u configureert en webproxy op een geregistreerd apparaat inschakelt, wordt u toorestart Hallo actieve controller moet op uw apparaat. | |Ja |Nee |
| 8 |Cloud hoge latentie en hoge i/o-werkbelasting |Wanneer uw StorSimple-apparaat een combinatie van zeer hoge cloud latenties (volgorde van seconden) en de hoge i/o-belasting tegenkomt, gaat u Hallo apparaat volumes in een gedegradeerde status en Hallo i/o's mislukken met een 'apparaat niet gereed'-fout. |Toomanually opnieuw opstarten Hallo apparaatcontrollers wordt of u een apparaat failover toorecover uitvoeren vanuit deze situatie. |Ja |Nee |
| 9 |Azure PowerShell |Wanneer u Hallo StorSimple-cmdlet gebruikt **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - eerst 1 - wacht** tooselect Hallo eerste object zodat u kunt een nieuwe maken **VolumeContainer** object Hallo cmdlet retourneert alle Hallo-objecten. |Hallo-cmdlet als volgt haakjes inpakt: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - eerst 1 - wachttijd** |Ja |Ja |
| 10 |Migratie |Wanneer meerdere volumecontainers worden doorgegeven voor migratie, is Hallo ETA voor de meest recente back-up alleen voor de eerste volumecontainer Hallo nauwkeurige. Bovendien start parallelle migratie nadat hello eerste 4 back-ups in de eerste volumecontainer Hallo zijn gemigreerd. |Het is raadzaam dat u een volumecontainer tegelijk migreren. |Ja |Nee |
| 11 |Migratie |Na het terugzetten van Hallo volumes niet toohello back-beleid of Hallo virtuele schijfgroep toegevoegd. |U moet deze volumes tooa back-upbeleid in volgorde toocreate back-ups tooadd. |Ja |Ja |
| 12 |Migratie |Nadat het Hallo-migratie is voltooid, Hallo 5000/7000-serie apparaat moet geen toegang krijgen tot Hallo gegevenscontainers gemigreerd. |Het is raadzaam dat u Hallo verwijdert gegevenscontainers gemigreerd nadat Hallo migratie voltooid en doorgevoerd is. |Ja |Nee |
| 13 |Kloon en Noodherstel |Een StorSimple-apparaat met Update 1 kan niet klonen of uitvoeren van herstel na noodgevallen tooa apparaat vóór update 1 software die wordt uitgevoerd. |U moet tooupdate Hallo doel apparaat tooUpdate 1 tooallow deze bewerkingen |Ja |Ja |
| 14 |Migratie |Configuratieback-up voor de migratie kan op een apparaat 5000 7000-serie mislukken wanneer er groepen met geen gekoppelde volumes volume zijn. |Alle Hallo leeg volume groepen met geen gekoppelde volumes verwijderen en probeer vervolgens Hallo configuratieback-up. |Ja |Nee |

## <a name="physical-device-updates-in-update-12"></a>Fysiek apparaat-updates in de Update 1.2
Als patch update 1.2 toegepaste tooa fysiek apparaat (met eerdere versies-tooUpdate 1), wordt de softwareversie Hallo too6.3.9600.17584 wijzigen.

## <a name="controller-and-firmware-updates-in-update-12"></a>Controller en firmware-updates in de Update 1.2
Deze release updates Hallo stuurprogramma en Hallo schijf firmware op uw apparaat.

* Zie voor meer informatie over Hallo SAS-controller update [Update 1 voor LSI SAS-controllers in Microsoft Azure StorSimple toestel](https://support.microsoft.com/kb/3043005). 
* Zie voor meer informatie over Hallo schijf firmware-update [schijf firmware Update 1 voor Microsoft Azure StorSimple-apparaat](https://support.microsoft.com/kb/3063416).

## <a name="virtual-device-updates-in-update-12"></a>Virtueel apparaat-updates in de Update 1.2
Deze update kan niet worden toegepast toohello virtueel apparaat. Nieuwe virtuele apparaten moet toobe gemaakt. 

## <a name="next-steps"></a>Volgende stappen
* [Update 1.2 op uw apparaat installeert](storsimple-install-update-1.md).

