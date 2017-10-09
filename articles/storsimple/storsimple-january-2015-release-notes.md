---
title: aaaStorSimple 8000 bijwerken 0,2 release-opmerkingen | Microsoft Docs
description: Hierin wordt beschreven Hallo nieuwe functies en oplossingen, open problemen en beschikbare tijdelijke oplossingen voor Hallo januari 2015 Microsoft Azure StorSimple versie (Update 0.2).
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d9684ae3-b38f-4678-9d70-e5dbc6b03350
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: 1cee795df0b53d9b9276bc33074cf1a7aa188835
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>StorSimple 8000 serie Update 0,2 release-opmerkingen - januari 2015
## <a name="overview"></a>Overzicht
Hallo identificeren volgende releaseopmerkingen Hallo kritieke open problemen voor Hallo januari 2015-release van Microsoft Azure StorSimple. Ze bevatten ook een lijst met Hallo StorSimple-software en firmware-updates die zijn opgenomen in deze release. Dit is de tweede versie Hallo nadat Hallo StorSimple 8000 Series Release-versie beschikbaar is gesteld over het algemeen in juli 2014.

Hallo fysiek apparaat softwareversie van Hallo oktober update wordt niet door deze update worden gewijzigd. Toobe versie 6.3.9600.17312 gaat door. Hallo-installatiekopie die wordt gebruikt door de installatiekopie van een virtueel apparaat Hallo is gewijzigd in deze release. Daarom worden alle Hallo nieuwe virtuele apparaten gemaakt na 1/20/2015 Hallo versie als 6.3.9600.17361 weergegeven.  

Controleer de volgende gegevens in de release-opmerkingen voor update van januari 2015 Hallo HALLO hallo.

> [!IMPORTANT]
> * Deze update is niet beschikbaar via Windows Update en net als bij andere updates kan niet worden geïnstalleerd. Uw apparaat ontvangt geen deze update, zelfs als u updates Hallo hebt toegepast met behulp van Hallo klassieke Azure-portal. Deze update is alleen van toepassing toovirtual-apparaten die zijn gemaakt na 20 januari 2015. 
> * Hallo bevat januari release van StorSimple niet alle updates toohello fysieke StorSimple-apparaat. U kunt nog steeds beschikbaar Windows updates toohello virtueel apparaat toepassen, met inbegrip van recente beveiligingsupdates oplossingen, maar u ziet een wijziging in de versie voor fysieke StorSimple-apparaat Hallo.
> 
> 

## <a name="whats-new-in-hello-january-release"></a>Wat is er nieuw in Hallo januari versie
Deze update bevat een oplossing gerelateerde toohello volumes gaat offline op Hallo virtueel apparaat. (Zie [problemen opgelost in deze release](#issues-fixed-in-the-january-release).)  

Hallo-update bevat geen nieuwe functies of functionaliteit.  

## <a name="issues-fixed-in-hello-january-release"></a>Problemen in Hallo januari release worden opgelost
Hallo beschrijft volgende tabel Hallo probleem dat met deze update is verholpen.

| Nee. | Functie | Probleem | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- |
| 1 |Volumes gaat offline |Als hoge cloud latenties zich blijven enkele minuten duren voordoen, off Hallo StorSimple-apparaat-volumes op Hallo-hosts. Deze oplossing verhoogt Hallo drempelwaarde voor cloud latenties, waardoor het minimaliseren van Hallo situaties waardoor Hallo volumes toogo offline op hosts. |Nee |Ja |

## <a name="known-issues-in-hello-january-release"></a>Bekende problemen in Hallo januari release
Hallo volgende tabel bevat een samenvatting van bekende problemen in deze release.

| Nee. | Functie | Probleem | Opmerkingen/tijdelijke oplossing | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- | --- |
| 1 |Fabrieksinstellingen terugzetten |In sommige gevallen, wanneer u de fabrieksinstellingen terug te zetten, uitvoert Hallo StorSimple-apparaat kan blijven steken en dit bericht weergegeven: **toofactory opnieuw instellen wordt uitgevoerd (fase 8).** Dit gebeurt als u op CTRL + C drukt Hallo cmdlet uitgevoerd wordt. |Druk CTRL + C niet op na het initiëren van de fabrieksinstellingen terug te zetten. Als u al in deze staat, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 2 |Schijf quorum |In zeldzame gevallen, als Hallo meerderheid van de schijven in Hallo EBOD behuizing van een 8600-apparaat niet zijn verbonden met waardoor geen quorum schijf vervolgens Hallo opslaggroep worden offline. Blijft deze offline zelfs als Hallo schijven opnieuw worden verbonden. |U moet tooreboot Hallo apparaat. Als Hallo probleem zich blijft voordoen, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 3 |Cloud momentopname fouten |In zeldzame gevallen een cloudmomentopname van een kan mislukken met fout Hallo **back-up maximumlimiet bereikt**. Dit gebeurt als u meer dan 255 online klonen op Hallo van Hallo hetzelfde apparaat hetzelfde oorspronkelijke volume dat is verwijderd. | |Ja |Ja |
| 4 |Onjuiste besturings-ID |Als een vervangende domeincontroller wordt uitgevoerd, kan controller 0 als controller 1 weergegeven. Tijdens de vervanging van de domeincontroller, wanneer Hallo afbeelding is geladen vanuit Hallo peer-knooppunt, Hallo besturings-ID kan worden weergegeven in eerste instantie als Hallo peer controller-ID.  In zeldzame gevallen kan worden dit probleem ook gezien na opnieuw opstarten. |Er is geen gebruikersactie vereist. Deze situatie wordt automatisch opgelost nadat Hallo controller vervanging voltooid is. |Ja |Nee |
| 5 |Controle van grafieken van apparaten |In Hallo StorSimple Manager-service, Hallo apparaat bewaking grafieken werken niet als basis of NTLM-verificatie is ingeschakeld in Hallo proxyserver-configuratie voor Hallo-apparaat. |Webproxyconfiguratie voor Hallo apparaat geregistreerd bij uw StorSimple Manager-service zodanig dat de verificatie is ingesteld tooNONE Hallo wijzigen. toodo deze, Voer Hallo Hallo Windows PowerShell voor StorSimple Set-HcsWebProxy cmdlet. |Ja |Ja |
| 6 |Opslagaccounts |Hallo Opslagaccount service toodelete Hallo opslag gebruikt, is een niet-ondersteund scenario. Dit leidt tooa situatie waarin de gebruikersgegevens kan niet worden opgehaald. | |Ja |Ja |
| 7 |Failover van apparaat |Meerdere failovers van een volumecontainer van Hallo dezelfde bron toodifferent apparaat doelapparaten wordt niet ondersteund. |Failover van een enkel dode apparaat toomultiple apparaten brengt Hallo volumecontainers op Hallo eerst failover apparaat is Gegevenseigendom gaan verloren. Na een failover wordt deze volumecontainers worden weergegeven of zich anders gedragen wanneer u ze in de klassieke Azure-portal Hallo weergeeft. |Ja |Nee |
| 8 |Installeren |Tijdens het StorSimple-Adapter voor SharePoint-installatie moet u tooprovide een apparaat IP-adres om Hallo installeren toofinish is. | |Ja |Nee |
| 9 |Webproxy |Als uw webproxyconfiguratie HTTPS als Hallo opgegeven protocol, en vervolgens uw communicatie apparaat-naar-service worden beïnvloed en Hallo apparaat gaat offline. Ondersteuningspakketten wordt ook gegenereerd in Hallo proces, verbruikt behoorlijk aanspraak op uw apparaat. |Zorg ervoor dat Hallo web proxy-URL bevat HTTP als Hallo opgegeven protocol. Zie voor meer informatie over het te[webproxy voor uw apparaat configureren](storsimple-configure-web-proxy.md). |Ja |Nee |
| 10 |Webproxy |Als u configureert en webproxy op een geregistreerd apparaat inschakelt, wordt u toorestart Hallo actieve controller moet op uw apparaat. | |Ja |Nee |
| 11 |Cloud hoge latentie en hoge i/o-werkbelasting |Wanneer uw StorSimple-apparaat een combinatie van zeer hoge cloud latenties (volgorde van seconden) en de hoge i/o-belasting tegenkomt, gaat u Hallo apparaat volumes in een gedegradeerde status en Hallo i/o's mislukken met een 'apparaat niet gereed'-fout. |Toomanually opnieuw opstarten Hallo apparaatcontrollers wordt of u een apparaat failover toorecover uitvoeren vanuit deze situatie. |Ja |Nee |

## <a name="physical-device-updates-in-hello-january-release"></a>Fysieke apparaatupdates Hallo januari release
Deze update bevat niet alle andere wijzigingen toohello StorSimple-apparaat.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-january-release"></a>Serial attached SCSI (SAS)-controller en firmware-updates in Hallo januari release
Deze release bevat geen updates toohello serial attached SCSI (SAS)-controller of Hallo firmware. Hallo stuurprogramma-update is in Hallo oktober 2014-release. 

## <a name="virtual-device-updates-in-hello-january-release"></a>Virtueel apparaatupdates Hallo januari release
Deze release bevat een bijgewerkte installatiekopie voor het virtuele apparaat Hallo. Alle Hallo virtuele apparaten gemaakt na 20 januari 2015 worden Hallo softwareversie als 6.3.9600.17361 weergegeven.

