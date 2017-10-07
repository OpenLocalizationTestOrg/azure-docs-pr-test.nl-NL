---
title: aaaStorSimple 8000 bijwerken 0,1 release-opmerkingen | Microsoft Docs
description: Hierin wordt beschreven Hallo nieuwe functies en oplossingen, open problemen en beschikbare tijdelijke oplossingen voor Hallo oktober 2014 Microsoft Azure StorSimple versie (Update 0,1).
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>StorSimple 8000 serie Update 0,1 release-opmerkingen – oktober 2014
## <a name="overview"></a>Overzicht
Hallo na de release-opmerkingen identificeren Hallo kritieke open problemen voor StorSimple 8000 serie Update 0.1 in oktober 2014 is uitgebracht. Ze bevatten ook een lijst met Hallo StorSimple-software en firmware-updates die zijn opgenomen in deze release. Dit is de eerste versie Hallo nadat Hallo StorSimple 8000 Series Release versie algemeen beschikbaar is in juli 2014 is gedaan en toosoftware versie 6.3.9600.17312 komt overeen.  

U wordt aangeraden dat u zoeken en toepassen van beschikbare updates onmiddellijk nadat u Hallo-apparaat installeert. U kunt ook toodownload automatische updates inschakelen en belangrijke updates van Microsoft installeren zodra ze worden vrijgegeven. Voor meer informatie Zie hoe te[uw StorSimple-apparaat bijwerken](storsimple-update-device.md).  

Controleer Hallo gegevens in de releaseopmerkingen Hallo voordat u Hallo-updates in uw StorSimple-oplossing implementeren.  

> [!IMPORTANT]
> * Gebruik Hallo StorSimple Manager-service en niet Windows PowerShell voor StorSimple tooinstall Hallo die oktober bijgewerkt.  
> * Hallo-updates worden meestal ongeveer 3 uur toocomplete uitgevoerd.  
> * Hallo bevat release van oktober van StorSimple niet alle updates toohello virtuele StorSimple-apparaat. U kunt nog steeds alle beschikbare Windows-updates, inclusief recente beveiligingsupdates, toepassen, maar niet ziet u een wijziging in de versie voor het virtuele apparaat Hallo.  
> 
> 

Zorg ervoor dat Hallo volgende vereisten zijn voldaan voorafgaande tooupdating uw StorSimple-apparaat.  

* Zorg ervoor dat beide apparaatcontrollers worden uitgevoerd voordat u op updates scannen. Als een domeincontroller niet wordt uitgevoerd, mislukt de Hallo scan. tooverify die Hallo domeincontrollers in een foutloze toestand te navigeren**hardwarestatus** onder Hallo **onderhoud** pagina. Als er onderdelen die **aandacht**, neem contact op met Microsoft Support voordat u verdergaat.  
* Zorg ervoor dat vaste IP-adressen voor beide Controller 0 en Controller 1 routeerbaar zijn en verbinding toohello Internet maken kunt als deze worden gebruikt voor het onderhoud van Hallo updates toohello apparaat. U kunt Hallo [cmdlet Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping een bekende adres buiten het netwerk zoals outlook.com, tooverify die domeincontroller Hallo Hallo toohello connectiviteit buiten netwerk heeft.  
* Zorg ervoor dat Hallo vereist uitgaande poorten beschikbaar zijn op uw StorSimple-apparaat voor uitgaande communicatie. Zie voor meer informatie, Hallo [netwerkvereisten voor uw StorSimple-apparaat](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).  
* Als Hallo apparaat softwareversie ouder is dan 6.3.9600.17312 (update van oktober 2014), schakelt u Hallo Data 2 en Data 3 poorten als ingeschakeld voordat u update Hallo start. Als u Hallo Data 2 of 3 van de gegevens poorten ingeschakeld tijdens het toepassen van de update Hallo laat, kan dit ertoe leiden dat uw apparaat controller toogo in de herstelmodus overgaat. Houd er rekening mee dat wanneer u Hallo-netwerkinterfaces uitschakelen, alle Hallo gekoppeld volumes zal offline worden gehaald en Hallo i/o worden verstoord gedurende Hallo Hallo-update.  

## <a name="whats-new-in-hello-october-release"></a>Wat is er nieuw in Hallo oktober versie
Deze update omvat Hallo volgende verbeteringen:

* U kunt uw apparaatcontrollers nu Hallo StorSimple Manager service UI toomanage. Hallo management acties omvatten opstarten, afsluiten, of schakel de op een domeincontroller. Voor meer informatie gaat te[StorSimple beheren apparaatcontrollers](storsimple-manage-device-controller.md).  
* U kunt de WAN-bandbreedtetoewijzing op basis van combinaties van tooday van de week en tijd van de dag plannen. Hiermee kunt u toomake beter gebruik van WAN-bandbreedte tijdens de daluren. Andere bandbreedte sjablonen zijn toegestaan voor een ander volumecontainers. Voor meer informatie gaat te[beheren van uw StorSimple bandbreedte sjablonen](storsimple-manage-bandwidth-templates.md).  
* U kunt e-mailmeldingen tooproactively Hallo beheerder (s) en andere bestaande of mogelijk toekomstige problemen melden configureren. Voor meer informatie gaat te[configureren waarschuwingsinstellingen](storsimple-manage-alerts.md#configure-alert-settings).  

## <a name="issues-fixed-in-hello-october-release"></a>Problemen in Hallo oktober release worden opgelost
Hallo bevat volgende tabel een samenvatting van fouten die in deze update worden verholpen.  

| Nee. | Functie | Probleem | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- |
| 1 |Netwerkinterfaces |In vorige Hallo release, Hallo netwerkinterfaces DATA 2 en DATA 3 in Hallo software zijn gewisseld. Dit probleem is opgelost in deze update. Hallo-instellingen verwijderen en deze netwerkinterfaces uitschakelen voordat u Hallo update installeert. Na de installatie van update hello, hebt u tooreconfigure deze interfaces. |Ja |Nee |
| 2 |Ondersteuningspakket |Hallo vorige release, als u Windows PowerShell Hallo uitgevoerd **Export HcsSupportPackage** cmdlet tooretrieve Hallo Baseboard Management Controller (BMC) zich aanmeldt, Hallo-bewerking is mislukt met de volgende waarschuwing Hallo: 'Hallo bewerking is voltooid op deze domeincontroller, maar niet op Hallo peer domeincontroller vanwege toohello volgende fout(en). Controleer of Hallo peer in orde is en of het huidige knooppunt Hallo verbinding maken met toohello peer." Dit probleem is nu opgelost. |Ja |Nee |
| 3 |Failover van apparaat |In de vorige release hello, er is een kans op inconsistenties in de gegevens als een **detecteren back-up** taak is mislukt tijdens een failover van het apparaat. Dit probleem is nu opgelost. |Ja |Nee |
| 4 |Failover van apparaat |In vorige Hallo release, na een failover apparaat, back-ups zijn zichtbaar maar Hallo gekoppeld volumecontainer is niet aanwezig op het doelapparaat Hallo. Dit probleem is nu opgelost. |Ja |Nee |
| 5 |Failover van apparaat |In de vorige release hello, moet u er een fout is in Hallo opsomming van back-ups cloud tijdens Hallo register restore-bewerking die toodata inconsistentie leiden kan als er problemen met de netwerkverbinding cloud zijn. |Ja |Nee |
| 6 |Firmware-update |In de vorige release Hallo hello apparaat firmware-update-taak is mislukt en een fout die vermeld dat Hallo-cmdlets niet herkend zijn en Hallo update is mislukt als gevolg hiervan wordt weergegeven. Hallo-controller wordt vervolgens werd in de herstelmodus overgaat. Dit probleem is nu opgelost. |Ja |Nee |
| 7 |Installeren |Fouten worden veroorzaakt door het Hallo-apparaat niet wordt replicatie correct tijdens de installatie zijn vastgesteld. |Ja |Nee |
| 8 |Fabrieksinstellingen terugzetten |U kunt nu desgewenst Hallo firmware Controleer voor terugzetten op fabrieksinstellingen overslaan. Dit is een wijziging van de vorige release Hallo. |Ja |Nee |
| 9 |Fabrieksinstellingen terugzetten |In de vorige release Hallo tijdens het uitvoeren van een fabriek reset-cmdlet, zijn firmware versie controles alleen gemaakt voor bepaalde hardwareonderdelen. Aanvullende firmware controles zijn aangebracht na de eerste herstart Hallo in Hallo proces, wat leiden Hallo reset toofail tot kan. Deze oplossing zorgt ervoor dat alle Hallo firmware controles uitgevoerd wanneer Hallo factory reset cmdlet wordt uitgevoerd en voordat Hallo eerste systeem opnieuw worden opgestart. |Ja |Nee |
| 10 |Storage-account key draaien |Hallo **Invoke-HcsmServiceDataEncryptionKeyChange** cmdlet toorotate hello opslagaccountsleutels gebruikt nu prompts Hallo gegevensversleutelingssleutel van gebruiker tooenter Hallo-service. Dit is een wijziging van de vorige release Hallo in welke Hallo gegevensversleutelingssleutel van service is doorgegeven als een inline-parameter. |Ja |Nee |
| 11 |Failback binnen 24 uur |Tijdens het herstel na noodgevallen, hebben Hallo opschonen op het bronvolume Hallo niet duidelijke, waardoor failback toofail plaatsgevonden. Dit probleem is opgelost in deze release. |Ja |Nee |

## <a name="known-issues-in-hello-october-release"></a>Bekende problemen in Hallo oktober release
Hallo volgende tabel bevat een samenvatting van bekende problemen in deze release.

| Nee. | Functie | Probleem | Opmerkingen/tijdelijke oplossing | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- | --- |
| 1 |Fabrieksinstellingen terugzetten |In sommige gevallen, wanneer u de fabrieksinstellingen terug te zetten, uitvoert Hallo StorSimple-apparaat kan blijven steken en dit bericht weergegeven: **toofactory opnieuw instellen wordt uitgevoerd (fase 8)**. Dit gebeurt als u op CTRL + C drukt Hallo cmdlet uitgevoerd wordt. |Druk CTRL + C niet op na het initiëren van de fabrieksinstellingen terug te zetten. Als u al in deze staat, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 2 |Fabrieksinstellingen terugzetten |Voer niet terugzetten op fabrieksinstellingen een StorSimple-apparaat is bijgewerkt van GA tooOctober 2014-release. |Deze bewerking werkt alleen als een patch is geïnstalleerd. Neem contact op met Microsoft Support tooget deze patch vereist. |Ja |Nee |
| 3 |Schijf quorum |In zeldzame gevallen, als Hallo meerderheid van de schijven in Hallo EBOD behuizing van een 8600-apparaat niet zijn verbonden met waardoor geen quorum schijf vervolgens Hallo opslaggroep worden offline. Blijft deze offline zelfs als Hallo schijven opnieuw worden verbonden. |U moet tooreboot Hallo apparaat. Als Hallo probleem zich blijft voordoen, neem contact met Microsoft Support voor de volgende stappen. |Ja |Nee |
| 4 |Cloud momentopname fouten |In zeldzame gevallen een cloudmomentopname van een kan mislukken met fout Hallo **back-up maximumlimiet bereikt**. Dit gebeurt als u meer dan 255 online klonen op Hallo van Hallo hetzelfde apparaat hetzelfde oorspronkelijke volume dat is verwijderd. | |Ja |Ja |
| 5 |Onjuiste besturings-ID |Als een vervangende domeincontroller wordt uitgevoerd, kan controller 0 als controller 1 weergegeven. Tijdens de vervanging van de domeincontroller, wanneer Hallo afbeelding is geladen vanuit Hallo peer-knooppunt, Hallo besturings-ID kan worden weergegeven in eerste instantie als Hallo peer controller-ID. In zeldzame gevallen kan worden dit probleem ook gezien na opnieuw opstarten. |Er is geen gebruikersactie vereist. Deze situatie wordt automatisch opgelost nadat Hallo controller vervanging voltooid is. |Ja |Nee |
| 6 |Controle van grafieken van apparaten |In Hallo StorSimple Manager-service, Hallo apparaat bewaking grafieken werken niet als basis of NTLM-verificatie is ingeschakeld in Hallo proxyserver-configuratie voor Hallo-apparaat. |Webproxyconfiguratie voor Hallo apparaat geregistreerd bij uw StorSimple Manager-service zodanig dat de verificatie is ingesteld tooNONE Hallo wijzigen. toodo deze, Voer Hallo Hallo Windows PowerShell voor StorSimple Set-HcsWebProxy cmdlet. |Ja |Ja |
| 7 |Opslagaccounts |Hallo Opslagaccount service toodelete Hallo opslag gebruikt, is een niet-ondersteund scenario. Dit leidt tooa situatie waarin de gebruikersgegevens kan niet worden opgehaald. | |Ja |Ja |
| 8 |Failover van apparaat |Meerdere failovers van een volumecontainer van Hallo dezelfde bron toodifferent apparaat doelapparaten wordt niet ondersteund. |Failover van een enkel dode apparaat toomultiple apparaten brengt Hallo volumecontainers op Hallo eerst failover apparaat is Gegevenseigendom gaan verloren. Na een failover wordt deze volumecontainers worden weergegeven of zich anders gedragen wanneer u ze in de klassieke Azure-portal Hallo weergeeft. |Ja |Nee |
| 9 |Installeren |Tijdens het StorSimple-Adapter voor SharePoint-installatie moet u tooprovide een apparaat IP-adres om Hallo installeren toofinish is. | |Ja |Nee |
| 10 |Webproxy |Als uw webproxyconfiguratie HTTPS als Hallo opgegeven protocol, en vervolgens uw communicatie apparaat-naar-service worden beïnvloed en Hallo apparaat gaat offline. Ondersteuningspakketten wordt ook gegenereerd in Hallo proces, verbruikt behoorlijk aanspraak op uw apparaat. |Zorg ervoor dat Hallo web proxy-URL bevat HTTP als Hallo opgegeven protocol. Meer informatie over het te[webproxy voor uw apparaat configureren](storsimple-configure-web-proxy.md). |Ja |Nee |
| 11 |Webproxy |Als u configureert en webproxy op een geregistreerd apparaat inschakelt, wordt u toorestart Hallo actieve controller moet op uw apparaat. | |Ja |Nee |
| 12 |Cloud hoge latentie en hoge i/o-werkbelasting |Wanneer uw StorSimple-apparaat een combinatie van zeer hoge cloud latenties (volgorde van seconden) en de hoge i/o-belasting tegenkomt, gaat u Hallo apparaat volumes in een gedegradeerde status en Hallo i/o's mislukken met een 'apparaat niet gereed'-fout. |Toomanually opnieuw opstarten Hallo apparaatcontrollers wordt of u een apparaat failover toorecover uitvoeren vanuit deze situatie. |Ja |Nee |

## <a name="physical-device-updates-in-hello-october-release"></a>Fysieke apparaatupdates Hallo oktober release
Wanneer deze updates toegepast tooa fysieke apparaat zijn, wordt de softwareversie Hallo too6.3.9600.17312 wijzigen. Tenzij anders vermeld, worden deze releaseopmerkingen tooall modellen van het StorSimple-apparaat Hallo toepassen. Zie voor meer informatie over deze updates [oktober 2014 fysieke toestel software-update voor Microsoft Azure StorSimple-apparaat](http://support.microsoft.com/kb/2986997).  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>Serial attached SCSI (SAS)-controller en firmware-updates in Hallo oktober release
Deze release updates Hallo stuurprogramma en Hallo firmware op Hallo SAS-controller van het fysieke apparaat. Zie voor meer informatie over Hallo SAS-controller update [update van oktober 2014 voor LSI SAS-controllers in Microsoft Azure StorSimple toestel](http://support.microsoft.com/kb/2987020).   

Deze release geldt ook een cumulatieve firmware-update die zijn gericht op betrouwbaarheidsproblemen met hardwareonderdelen Hallo-apparaat. Zie voor meer informatie over Hallo firmware-update [oktober 2014 firmware-update voor Microsoft Azure StorSimple-apparaat](http://support.microsoft.com/kb/2987015).  

## <a name="virtual-device-updates-in-hello-october-release"></a>Virtueel apparaatupdates Hallo oktober release
Deze release bevat updates voor het virtuele apparaat Hallo geen. Toepassen van deze update heeft geen invloed op de softwareversie Hallo van een virtueel apparaat.

