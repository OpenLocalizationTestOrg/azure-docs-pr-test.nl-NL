---
title: aaaStorSimple 8000 bijwerken 0,3 release-opmerkingen | Microsoft Docs
description: Hierin wordt beschreven Hallo nieuwe functies en oplossingen, open problemen en beschikbare tijdelijke oplossingen voor Hallo februari 2015 Microsoft Azure StorSimple versie (Update 0.3).
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>StorSimple 8000 serie Update 0,3 release-opmerkingen - februari 2015
## <a name="overview"></a>Overzicht
na de release-opmerkingen Hallo identificeren Hallo kritieke open problemen voor StorSimple 8000 serie Update 0.3 uitgebracht in februari 2015. Ze bevatten ook een lijst met Hallo StorSimple-software en firmware-updates die zijn opgenomen in deze release. Dit is Hallo derde release nadat Hallo StorSimple 8000 Series Release versie algemeen beschikbaar is in juli 2014 is gedaan.

Hallo apparaat softwareversie van Hallo januari update wordt niet door deze update worden gewijzigd. Toobe versie 6.3.9600.17312 gaat door. U kunt bevestigen dat Hallo-update is geïnstalleerd door het controleren van Hallo **laatst bijgewerkt** datum. Als Hallo datum 2-10-2015 of hoger, klikt u vervolgens Hallo update is geïnstalleerd.  

U wordt aangeraden dat u zoeken en toepassen van beschikbare updates onmiddellijk nadat u uw StorSimple-apparaat geïnstalleerd. U kunt ook toodownload automatische updates inschakelen en belangrijke updates van Microsoft installeren zodra ze worden vrijgegeven. Zie voor meer informatie [uw StorSimple-apparaat bijwerken](storsimple-update-device.md).  

Controleer Hallo gegevens in Hallo release notes voordat u Hallo implementeert in uw StorSimple-oplossing bijwerken.  

> [!IMPORTANT]
> * Gebruik Hallo StorSimple Manager-service en niet Windows PowerShell voor StorSimple tooinstall Hallo februari update.   
> * Het duurt ongeveer een uur tooinstall deze update. Echter, als u cumulatieve updates installeert, Hallo kan duren ongeveer 3 uur toocomplete.  
> * Hallo bevat februari release van StorSimple niet alle updates toohello virtuele StorSimple-apparaat. U kunt nog steeds beschikbaar Windows updates toohello virtueel apparaat toepassen, met inbegrip van recente beveiligingsupdates oplossingen, maar u ziet een wijziging in de versie voor het virtuele apparaat Hallo.  
> 
> 

Zorg ervoor dat Hallo volgende vereisten zijn voldaan voorafgaande tooupdating uw StorSimple-apparaat.  

* Zorg ervoor dat beide apparaatcontrollers worden uitgevoerd voordat u op updates scannen. Als een domeincontroller niet wordt uitgevoerd, mislukt de Hallo scan. tooverify die Hallo domeincontrollers in een foutloze toestand te navigeren**hardwarestatus** onder Hallo **onderhoud** pagina. Als er onderdelen die **aandacht**, neem contact op met Microsoft Support voordat u verdergaat.
* Zorg ervoor dat vaste IP-adressen voor controller 0 en controller 1 routeerbaar zijn en verbinding toohello Internet kunt maken als deze worden gebruikt voor het onderhoud van Hallo updates toohello apparaat. U kunt Hallo [cmdlet Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping een bekende adres buiten Hallo netwerk, zoals outlook.com, tooverify die domeincontroller Hallo toohello connectiviteit buiten netwerk heeft.
* Zorg ervoor dat de poorten 80 en 443 op uw StorSimple-apparaat voor uitgaande communicatie beschikbaar zijn. Zie voor meer informatie, Hallo [netwerkvereisten voor uw StorSimple-apparaat](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* Als Hallo apparaat softwareversie ouder is dan 6.3.9600.17312 (update van oktober 2014), schakelt u Hallo Data 2 en Data 3 poorten als ingeschakeld voordat u update Hallo start. Hallo Data 2 of 3 van de gegevens verlaten poorten ingeschakeld wanneer u Hallo update toepassen kan ertoe leiden dat uw apparaat controller toogo in de herstelmodus overgaat. Houd er rekening mee dat wanneer u Hallo-netwerkinterfaces uitschakelen, alle Hallo gekoppeld volumes zal offline worden gehaald en Hallo i/o's voor de duur van Hallo update Hallo worden verstoord.  

## <a name="whats-new-in-hello-february-release"></a>Wat is er nieuw in Hallo februari versie
Deze update bevat een oplossing voor Hallo factory reset probleem is opgetreden op apparaten die was zijn bijgewerkt uit Hallo GA release toohello release van oktober 2014. Zie voor meer informatie [problemen opgelost in deze release](#issues-fixed-in-the-february-release).   

Deze update bevat geen nieuwe functies of functionaliteit.  

## <a name="issues-fixed-in-hello-february-release"></a>Problemen in Hallo februari release worden opgelost
Hallo beschrijft volgende tabel Hallo probleem dat met deze update is verholpen.  

| Nee. | Functie | Probleem | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- |
| 1 |Fabrieksinstellingen terugzetten |U probeert tooperform fabrieksinstellingen op een apparaat dat oorspronkelijk had Hallo GA versie (6.3.9600.17215) geïnstalleerd, maar is bijgewerkte toohello release van oktober (versie 6.3.9600.17312). Hallo mislukt de fabrieksinstellingen en Hallo apparaat onstabiel. |Ja |Nee |

## <a name="known-issues-in-hello-february-release"></a>Bekende problemen in Hallo februari release
Hallo volgende tabel bevat een samenvatting van bekende problemen in deze release.

| Nee. | Functie | Probleem | Opmerkingen/tijdelijke oplossing | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- | --- |
| 1 |Fabrieksinstellingen terugzetten |In sommige gevallen, wanneer u de fabrieksinstellingen terug te zetten, uitvoert Hallo StorSimple-apparaat kan blijven steken en dit bericht weergegeven: **toofactory opnieuw instellen wordt uitgevoerd (fase 8)**. Dit gebeurt als u op CTRL + C drukt Hallo cmdlet uitgevoerd wordt. |Druk CTRL + C niet op na het initiëren van de fabrieksinstellingen terug te zetten. Als u al in deze staat, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 2 |Schijf quorum |In zeldzame gevallen, als Hallo meerderheid van de schijven in Hallo EBOD behuizing van een 8600device niet zijn verbonden met waardoor geen quorum schijf vervolgens Hallo opslaggroep worden offline. Blijft deze offline zelfs als Hallo schijven opnieuw worden verbonden. |U moet tooreboot Hallo apparaat. Als Hallo probleem zich blijft voordoen, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 3 |Cloud momentopname fouten |In zeldzame gevallen een cloudmomentopname van een kan mislukken met fout Hallo **back-up maximumlimiet bereikt**. Dit gebeurt als u meer dan 255 online klonen op Hallo van Hallo hetzelfde apparaat hetzelfde oorspronkelijke volume dat is verwijderd. | |Ja |Ja |
| 4 |Onjuiste besturings-ID |Als een vervangende domeincontroller wordt uitgevoerd, kan controller 0 als controller 1 weergegeven. Tijdens de vervanging van de domeincontroller, wanneer Hallo afbeelding is geladen vanuit Hallo peer-knooppunt, Hallo besturings-ID kan worden weergegeven in eerste instantie als Hallo peer controller-ID. In zeldzame gevallen kan worden dit probleem ook gezien na opnieuw opstarten. |Er is geen gebruikersactie vereist. Deze situatie wordt automatisch opgelost nadat Hallo controller vervanging voltooid is. |Ja |Nee |
| 5 |Controle van grafieken van apparaten |In Hallo StorSimple Manager-service, Hallo apparaat bewaking grafieken werken niet als basis of NTLM-verificatie is ingeschakeld in Hallo proxyserver-configuratie voor Hallo-apparaat. |Webproxyconfiguratie voor Hallo apparaat geregistreerd bij uw StorSimple Manager-service zodanig dat de verificatie is ingesteld tooNONE Hallo wijzigen. toodo deze, Voer Hallo Hallo Windows PowerShell voor StorSimple Set-HcsWebProxy cmdlet. |Ja |Ja |
| 6 |Opslagaccounts |Hallo Opslagaccount service toodelete Hallo opslag gebruikt, is een niet-ondersteund scenario. Dit leidt tooa situatie waarin de gebruikersgegevens kan niet worden opgehaald. | |Ja |Ja |
| 7 |Failover van apparaat |Meerdere failovers van een volumecontainer van Hallo dezelfde bron toodifferent apparaat doelapparaten wordt niet ondersteund.    Failover van een enkel dode apparaat toomultiple apparaten brengt Hallo volumecontainers op Hallo eerst failover apparaat is Gegevenseigendom gaan verloren. Na een failover wordt deze volumecontainers worden weergegeven of zich anders gedragen wanneer u ze in de klassieke Azure-portal Hallo weergeeft. | |Ja |Nee |
| 8 |Installeren |Tijdens het StorSimple-Adapter voor SharePoint-installatie moet u tooprovide een apparaat IP-adres om Hallo installeren toofinish is. | |Ja |Nee |
| 9 |Webproxy |Als uw webproxyconfiguratie HTTPS als Hallo opgegeven protocol, en vervolgens uw communicatie apparaat-naar-service worden beïnvloed en Hallo apparaat gaat offline. Ondersteuningspakketten wordt ook gegenereerd in Hallo proces, verbruikt behoorlijk aanspraak op uw apparaat. |Zorg ervoor dat Hallo web proxy-URL bevat HTTP als Hallo opgegeven protocol. Meer informatie over het te[webproxy voor uw apparaat configureren](storsimple-configure-web-proxy.md). |Ja |Nee |
| 10 |Webproxy |Als u configureert en webproxy op een geregistreerd apparaat inschakelt, wordt u toorestart Hallo actieve controller moet op uw apparaat. | |Ja |Nee |
| 11 |Cloud hoge latentie en hoge i/o-werkbelasting |Wanneer uw StorSimple-apparaat een combinatie van zeer hoge cloud latenties (volgorde van seconden) en de hoge i/o-belasting tegenkomt, gaat u Hallo apparaat volumes in een gedegradeerde status en Hallo i/o's mislukken met een 'apparaat niet gereed'-fout. |Toomanually opnieuw opstarten Hallo apparaatcontrollers wordt of u een apparaat failover toorecover uitvoeren vanuit deze situatie. |Ja |Nee |

## <a name="physical-device-updates-in-hello-february-release"></a>Fysieke apparaatupdates Hallo februari release
Deze update correcties Hallo fabrieksinstellingen probleem dat is opgetreden op apparaten die was zijn bijgewerkt uit Hallo GA release toohello release van oktober 2014. Het bevat niet alle andere updates toohello StorSimple-apparaat.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>Serial attached SCSI (SAS)-controller en firmware-updates in Hallo februari release
Deze release bevat geen updates toohello serial attached SCSI (SAS)-controller of Hallo firmware. Hallo stuurprogramma-update is in Hallo oktober 2014-release.  

## <a name="virtual-device-updates-in-hello-february-release"></a>Virtueel apparaatupdates Hallo februari release
Deze release bevat updates voor het virtuele apparaat Hallo geen. Toepassen van deze update heeft geen invloed op de softwareversie Hallo van een virtueel apparaat.

