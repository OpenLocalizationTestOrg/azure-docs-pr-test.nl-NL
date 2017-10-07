---
title: aaaStorSimple 8000 Release versie release-opmerkingen | Microsoft Docs
description: Beschrijft nieuwe functies Hallo, open problemen en beschikbare oplossingen voor het Hallo juli 2014 Microsoft Azure StorSimple versie.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>Releaseopmerkingen voor StorSimple 8000 Series versie - juli 2014
## <a name="overview"></a>Overzicht
Opmerkingen bij de release van de Hallo volgen problemen Hallo kritieke open voor Hallo StorSimple 8000-serie juli 2014 algemene beschikbaarheid (GA) versie van Microsoft Azure StorSimple. Deze release komt overeen toosoftware versie 6.3.9600.17215.  

Tenzij anders vermeld, worden deze releaseopmerkingen tooall modellen van het StorSimple-apparaat Hallo toepassen. Hallo release-opmerkingen worden voortdurend bijgewerkt; Wanneer er kritieke problemen waarvoor een tijdelijke oplossing nodig worden ontdekt, worden ze toegevoegd. Voordat u uw Microsoft Azure StorSimple-oplossing implementeert, overweeg Hallo informatie te volgen.  

## <a name="known-issues-in-this-release"></a>Bekende problemen in deze release
Hallo volgende tabel bevat een samenvatting van bekende problemen in deze release.  

| Nee. | Functie | Probleem | Opmerkingen/tijdelijke oplossing | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- | --- |
| 1 |Fabrieksinstellingen terugzetten |In sommige gevallen, wanneer u de fabrieksinstellingen terug te zetten, uitvoert Hallo StorSimple-apparaat kan blijven steken en dit bericht weergegeven: **toofactory opnieuw instellen wordt uitgevoerd (fase 8)**. Dit gebeurt als u op CTRL + C drukt Hallo cmdlet uitgevoerd wordt. |Druk CTRL + C niet op na het initiëren van de fabrieksinstellingen terug te zetten. Als u al in deze staat, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 2 |Schijf quorum |In zeldzame gevallen, als Hallo meerderheid van de schijven in Hallo EBOD behuizing van een 8600-apparaat niet zijn verbonden met waardoor geen quorum schijf vervolgens Hallo opslaggroep worden offline. Blijft deze offline zelfs als Hallo schijven opnieuw worden verbonden. |U moet tooreboot Hallo apparaat. Als Hallo probleem zich blijft voordoen, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 3 |Cloud momentopname fouten |In zeldzame gevallen een cloudmomentopname van een kan mislukken met fout Hallo **back-up maximumlimiet bereikt**. Dit gebeurt als u meer dan 255 online klonen op Hallo van Hallo hetzelfde apparaat hetzelfde oorspronkelijke volume dat is verwijderd. | |Ja |Ja |
| 4 |Onjuiste besturings-ID |Als een vervangende domeincontroller wordt uitgevoerd, kan controller 0 als controller 1 weergegeven. Tijdens de vervanging van de domeincontroller, wanneer Hallo afbeelding is geladen vanuit Hallo peer-knooppunt, Hallo besturings-ID kan worden weergegeven in eerste instantie als Hallo peer controller-ID. In zeldzame gevallen kan worden dit probleem ook gezien na opnieuw opstarten. |Er is geen gebruikersactie vereist. Deze situatie wordt automatisch opgelost nadat Hallo controller vervanging voltooid is. |Ja |Nee |
| 5 |Controle van grafieken van apparaten |In Hallo StorSimple Manager-service, Hallo apparaat bewaking grafieken werken niet als basis of NTLM-verificatie is ingeschakeld in Hallo proxyserver-configuratie voor Hallo-apparaat. |Webproxyconfiguratie voor Hallo apparaat geregistreerd bij uw StorSimple Manager-service zodanig dat de verificatie is ingesteld tooNONE Hallo wijzigen. toodo deze, Voer Hallo Hallo Windows PowerShell voor StorSimple Set-HcsWebProxy cmdlet. |Ja |Ja |
| 6 |Opslagaccounts |Hallo Opslagaccount service toodelete Hallo opslag gebruikt, is een niet-ondersteund scenario. Dit leidt tooa situatie waarin de gebruikersgegevens kan niet worden opgehaald. | |Ja |Ja |
| 7 |Failback |Een failback binnen 24 uur van noodherstel (DR) wordt niet ondersteund. | |Ja |Nee |
| 8 |Failover van apparaat |Meerdere failovers van een volumecontainer van Hallo dezelfde bron toodifferent apparaat doelapparaten wordt niet ondersteund. Failover van een enkel dode apparaat toomultiple apparaten brengt Hallo volumecontainers op Hallo eerst failover apparaat is Gegevenseigendom gaan verloren. Na een failover wordt deze volumecontainers worden weergegeven of zich anders gedragen wanneer u ze in de klassieke Azure-portal Hallo weergeeft. | |Ja |Nee |
| 9 |Installeren |Tijdens het StorSimple-Adapter voor SharePoint-installatie moet u tooprovide een apparaat IP-adres voor Hallo installeren toofinish is. | |Ja |Nee |
| 10 |Netwerkinterfaces |Netwerkinterfaces DATA 2 en DATA 3 zijn in Hallo software gewisseld. |Neem contact op met Microsoft Support als u deze interfaces tooconfigure nodig. |Ja |Nee |

