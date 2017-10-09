---
title: Opmerkingen bij de release van de aaaStorSimple 8000 Series Update 2 | Microsoft Docs
description: Beschrijft de nieuwe functies hello, problemen en tijdelijke oplossingen voor StorSimple 8000 Series Update 2.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: e2c8bffd-7fc5-4b77-b632-a4f59edacc3a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 36c75aad900c7b1286a924732967b8ee519a3d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>Opmerkingen bij de release van de StorSimple 8000 Series Update 2
## <a name="overview"></a>Overzicht
Hallo volgende releaseopmerkingen beschrijven Hallo nieuwe functies en Hallo kritieke open problemen identificeren voor StorSimple 8000 Series Update 2. Ze bevatten ook een lijst met Hallo StorSimple-software, stuurprogramma en schijf firmware-updates is opgenomen in deze release. 

Update 2 kan worden toegepast tooany StorSimple-apparaat met Release (GA) of Update 0.1 via Update 1.2. Hallo apparaatversie die is gekoppeld met Update 2 is 6.3.9600.17673.

Controleer Hallo gegevens in Hallo release notes voordat u Hallo implementeert in uw StorSimple-oplossing bijwerken.

> [!IMPORTANT]
> * Het duurt ongeveer 4-7 uur tooinstall deze update (inclusief updates voor Windows hello). 
> * Update 2 heeft de software, LSI stuurprogramma en SSD-firmware-updates.
> * Voor nieuwe releases, kunnen er geen updates onmiddellijk omdat we een gefaseerde implementatie van updates Hallo doen. Wacht een paar dagen en vervolgens zoeken naar updates opnieuw als deze is binnenkort beschikbaar.
> 
> 

## <a name="whats-new-in-update-2"></a>Wat is er nieuw in Update 2
Update 2 introduceert Hallo volgende nieuwe functies.

* **Lokaal vastgemaakte volumes** – In eerdere versies van Hallo StorSimple 8000 serie blokken met gegevens gelaagde toohello cloud op basis van gebruik zijn. Er is geen manier tooguarantee die blokken op lokale zou blijven. Bij Update 2 bij het maken van een volume, kunt u aanwijzen een volume lokaal vastgemaakt en primaire gegevens van het volume niet meer gelaagde toohello cloud. Momentopnamen van lokaal vastgemaakte volumes worden nog steeds toohello cloud voor back-up gekopieerd zodat Hallo cloud kan worden gebruikt voor hersteldoeleinden gegevens mobiliteit en noodherstel. Bovendien kunt u Hallo volumetype (dat wil zeggen, gelaagde volumes toolocally vastgemaakt volumes te converteren en converteren lokaal vastgemaakte volumes tootiered). 
* **StorSimple-apparaat verbeteringen** – voorheen Hallo StorSimple 8000-serie Hallo virtueel apparaat als een oplossing voor herstel of ontwikkeling en testen van noodherstel geplaatst. Er is slechts één model van het virtuele apparaat (model 1100). Update 2 introduceert twee modellen van het virtuele apparaat: 
  
  * 8010 (voorheen opgeroepen hello 1100) – geen wijziging; heeft een capaciteit van 30 TB en maakt gebruik van Azure standard-opslag.
  * 8020 – heeft een capaciteit van 64 TB en maakt gebruik van Azure Premium-opslag voor verbeterde prestaties.
    
    Er is een enkel VHD voor beide modellen virtuele apparaat (8010/8020). Wanneer u het virtuele apparaat hello eerst, detecteert Hallo platform parameters en past de juiste modelversie Hallo.
* **Netwerkverbeteringen** – Update 2 Hallo netwerkverbeteringen volgende bevat:
  
  * Meerdere NIC's kunnen worden ingeschakeld voor Hallo cloud zodat failover zich voordoen kan als een NIC is mislukt.
  * Routering verbeteringen, met vaste metrische gegevens voor cloud blokken ingeschakeld.
  * Online opnieuw uit met mislukte resources voordat u een failover.
  * Nieuwe waarschuwingen voor servicefouten.
* **Bijwerken van verbeteringen** : In bijwerken 1.2 en eerder, Hallo StorSimple 8000 series via twee kanalen is bijgewerkt: Windows Update voor clustering, iSCSI, en enzovoort en Microsoft Update voor binaire bestanden en -firmware.
    Update 2 gebruikt Microsoft Update voor alle updatepakketten. Hierdoor tooless tijd patchen of failovers doet. 
* **Firmware-updates** – hello volgende firmware-updates zijn opgenomen:
  
  * LSI: lsi_sas2.sys productversie 2.00.72.10
  * Alleen SSD (Er zijn geen updates HDD): XMGG, XGEG KZ50, F6C2 en VR08
* **Proactieve ondersteuning** – Update 2 kunt u Microsoft toopull aanvullende diagnostische gegevens van het Hallo-apparaat. Als onze teamleden identificeert de apparaten die problemen ondervindt, we betere uitgerust toocollect informatie van Hallo-apparaat en problemen diagnosticeren. **Update 2 accepteert, kunnen we tooprovide deze proactieve ondersteuning**.    

## <a name="issues-fixed-in-update-2"></a>Problemen opgelost met Update 2
Hallo na tabellen bevat een samenvatting van problemen die zijn verholpen in Updates 2.    

| Nee. | Functie | Probleem | Van toepassing is toophysical apparaat | Van toepassing is toovirtual apparaat |
| --- | --- | --- | --- | --- |
| 1 |Netwerkinterfaces |Na een upgrade tooUpdate 1 Hallo StorSimple Manager-service heeft gerapporteerd dat Hallo Data2 en Data3 poorten op een domeincontroller is mislukt. Dit probleem is opgelost. |Ja |Nee |
| 2 |Updates |Na een upgrade tooUpdate 1 akoestisch alarm waarschuwingen is opgetreden in Hallo klassieke Azure-portal op meerdere apparaten. Dit probleem is opgelost. |Ja |Nee |
| 3 |Openstack verificatie |Wanneer u Openstack als uw cloudserviceprovider, kan een foutbericht dat uw cloud-verificatie-tekenreeks te lang is. Dit probleem is opgelost. |Ja |Nee |

## <a name="known-issues-in-update-2"></a>Bekende problemen in Update 2
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
| 20 |Lokaal vastgemaakte volumes |Als u een gelaagd volume (gemaakt en gekloonde met Update 1.2 of eerder) tooconvert probeert tooa lokaal vastgemaakt volume en uw apparaat is bijna geen schijfruimte meer of er is een onderbreking van de cloud en hello clone(s) beschadigd kunnen raken. |Dit probleem treedt alleen op volumes die gemaakt en gekloonde met vooraf Update 2-software zijn. Dit moet een incidentele scenario. | | |
| 21 |Volumeconversie |Hallo ACRs gekoppelde tooa volume niet bijwerken tijdens een volumeconversie van het uitgevoerd wordt (gelaagde toolocally vastgemaakt of andersom). Hallo ACRs bijwerken kan leiden tot beschadiging van gegevens. |Indien nodig, Hallo ACRs voorafgaande toohello volumeconversie bijwerken en maak geen verdere ACR updates terwijl Hallo conversie uitgevoerd wordt. | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Controller en firmware-updates in de Update 2
Deze release updates Hallo stuurprogramma en Hallo schijf firmware op uw apparaat.

* Voor meer informatie over Hallo LSI firmware bijwerken, Zie Microsoft Knowledge base-artikel 3121900. 
* Voor meer informatie over Hallo schijf firmware bijwerken, Zie Microsoft Knowledge base-artikel 3121899.

## <a name="virtual-device-updates-in-update-2"></a>Virtueel apparaat-updates in de Update 2
Deze update kan niet worden toegepast toohello virtueel apparaat. Nieuwe virtuele apparaten moet toobe gemaakt. 

## <a name="next-step"></a>Volgende stap
Meer informatie over hoe te[installeren Update 2](storsimple-install-update-2.md) op uw StorSimple-apparaat.

