---
title: aaaStorSimple failover, herstel na noodgevallen voor apparaten 8000 serie | Microsoft Docs
description: Meer informatie over hoe toofail via uw tooitself StorSimple-apparaat, een ander fysiek apparaat of een cloud-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>Failover en herstel na noodgevallen voor uw StorSimple 8000 series apparaat

## <a name="overview"></a>Overzicht

Dit artikel wordt beschreven Hallo apparaat failover-functie voor Hallo StorSimple 8000 series apparaten en hoe deze functie kan worden gebruikt toorecover StorSimple-apparaten als een noodsituatie voordoet. StorSimple gebruikt apparaat failover toomigrate Hallo gegevens uit een Bronapparaat op Hallo datacenter tooanother doelapparaat. Hallo-instructies in dit artikel is van toepassing tooStorSimple 8000 series fysieke apparaten en apparaten van cloud met versies van de software Update 3 en hoger.

Hallo maakt gebruik van StorSimple **apparaten** blade toostart Hallo apparaat failover-functie in geval van een noodgeval Hallo. Deze blade bevat alle Hallo StorSimple-apparaten verbonden tooyour Apparaatbeheer StorSimple-service.

![Blade voor apparaten](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>Noodherstel (DR) en failover-apparaat

In een (DR) noodherstelscenario Hallo primair apparaat niet meer werkt. StorSimple maakt gebruik van het primaire apparaat Hallo als _bron_ en verplaatst Hallo gekoppeld cloud gegevens tooanother _doel_ apparaat. Dit proces is waarnaar wordt verwezen tooas hello *failover*. Hallo volgende afbeelding ziet u Hallo-proces van failover.

![Wat gebeurt er in failover-apparaat?](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

Hallo doelapparaat voor een failover kan niet een fysiek apparaat of zelfs een cloud-apparaat. Hallo doelapparaat mogelijk zich in Hallo dezelfde of een andere geografische locatie dan Hallo het bronvolume.

Tijdens de failover hello, kunt u volumecontainers voor migratie. Hallo-eigenaar van deze volumecontainers verandert StorSimple vervolgens van Hallo apparaat toohello doel het bronvolume. Zodra de volumecontainers Hallo eigendom wijzigen, worden deze containers in StorSimple uit Hallo Bronapparaat verwijderd. Nadat het Hallo verwijdering is voltooid, kunt u back Hallo doelapparaat mislukken. _Failback_ overdrachten Hallo eigendom back toohello oorspronkelijke Bronapparaat.

### <a name="cloud-snapshot-used-during-device-failover"></a>Cloudmomentopname gebruikt tijdens de failover van apparaat

Hallo recentste cloud back-up is na een DR gebruikte toorestore hello toohello doelapparaat. Zie voor meer informatie over cloudmomentopnamen [hello StorSimple Apparaatbeheer service tootake een handmatige back-up gebruiken](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup).

Op een serie StorSimple 8000 zijn back-upbeleid gekoppeld aan back-ups. Als er meerdere back-upbeleid hello hetzelfde volume en vervolgens selecteert StorSimple Hallo back-upbeleid met Hallo kunt u het grootste aantal volumes. StorSimple gebruikt vervolgens Hallo meest recente back-up van Hallo geselecteerd back-upbeleid toorestore Hallo gegevens op het doelapparaat Hallo.

Stel dat er zijn twee back-upbeleid, *defaultPol* en *customPol*:

* *defaultPol*: één volume *vol1*, dagelijkse begint bij 10:30 uur uitgevoerd.
* *customPol*: vier volumes *vol1*, *vol2*, *vol3*, *vol4*, dagelijkse begint bij 10:00 uur uitgevoerd.

In dit geval StorSimple bepaalt de volgorde voor crashconsistentie en maakt gebruik van *customPol* omdat deze meerdere volumes bevat. Hallo meest recente back-up van dit beleid is gebruikte toorestore gegevens. Voor meer informatie over het toocreate en beheren van back-upbeleid, gaat u te[hello StorSimple Apparaatbeheer service toomanage back-upbeleid gebruiken](storsimple-8000-manage-backup-policies-u2.md).

## <a name="common-considerations-for-device-failover"></a>Algemene overwegingen voor het apparaat failover

Voordat u een apparaat een failover, controleert u Hallo volgende informatie:

* Voordat een apparaat failover wordt gestart, moeten alle Hallo volumes in de volumecontainers Hallo offline zijn. In een niet-geplande failover gaat StotSimple volumes automatisch offline. Maar als u een geplande failover (tootest DR) uitvoert, moet u alle Hallo volumes offline halen.
* Alleen Hallo volumecontainers waarvoor een gekoppeld cloudmomentopname worden vermeld voor herstel na Noodgevallen. Er moet ten minste één volumecontainer met toorecover momentopnamegegevens van een gekoppelde cloud.
* Als er cloudmomentopnamen die meerdere volumecontainers overbruggen, wordt StorSimple overgenomen door deze volumecontainers als een set. In een zeldzame exemplaar als lokale momentopnamen die meerdere volumecontainers overbruggen, maar momentopnamen van de gekoppelde cloud niet doet, StorSimple Hallo lokale momentopnamen een failover en Hallo lokale gegevens verloren na Noodherstel.
* Hallo beschikbaar doelapparaten voor herstel na Noodgevallen zijn apparaten waarop voldoende ruimte tooaccommodate Hallo containers geselecteerde volume. Alle apparaten die niet over voldoende ruimte beschikken, worden niet vermeld als doelapparaten.
* Na een DR (voor een bepaalde duur) Hallo data access-prestaties aanzienlijk kan worden beïnvloed, als Hallo apparaat tooaccess nodig gegevens uit de cloud Hallo Hallo en lokaal opslaan.

#### <a name="device-failover-across-software-versions"></a>Apparaat failover tussen softwareversies

Een StorSimple-apparaat Manager-service in een implementatie met meerdere apparaten, fysieke kan hebben en de cloud, alle actieve andere softwareversies.

Gebruik tabel toodetermine volgen als u kunt een failover of mislukken back tooanother-apparaat met een ander software-versie en de werking van Hallo volumetypen tijdens DR Hallo.

#### <a name="failover-and-failback-across-software-versions"></a>Failover en failback over softwareversies

| Failover / failback van | Fysiek apparaat | Cloudapparaat |
| --- | --- | --- |
| Update 3 tooUpdate 4 |Gelaagde volumes dan gelaagde mislukken. <br></br>Lokaal vastgemaakte volumes failover uitgevoerd als lokaal vastgemaakt. <br></br> Na een failover wanneer u een momentopname op Hallo Update 4 apparaat [bijhouden op basis van heatmap](storsimple-update4-release-notes.md#whats-new-in-update-4) in gang. |Lokaal vastgemaakt failover als gelaagde volumes. |
| Update 4 tooUpdate 3 |Gelaagde volumes dan gelaagde mislukken. <br></br>Lokaal vastgemaakte volumes failover uitgevoerd als lokaal vastgemaakt. <br></br> Back-ups gebruikt toorestore heatmap metagegevens behouden. <br></br>Bijhouden op basis van Heatmap is niet beschikbaar in Update 3 na een failback. |Lokaal vastgemaakt failover als gelaagde volumes. |


## <a name="device-failover-scenarios"></a>Apparaat failover-scenario 's

Als er een ramp, kunt u via uw StorSimple-apparaat kunt toofail kiezen:

* [het fysieke apparaat tooa](storsimple-8000-device-failover-physical-device.md).
* [tooitself](storsimple-8000-device-failover-same-device.md).
* [tooa cloud toestel](storsimple-8000-device-failover-cloud-appliance.md).

Hallo voorgaande artikelen bevatten gedetailleerde stappen voor elk Hallo bovenstaande gevallen failover.


## <a name="failback"></a>Failback

Update 3 en hoger ondersteuning StorSimple ook voor failback. Failback is alleen Hallo van failover omkeren, Hallo doel Hallo bron en wordt Hallo oorspronkelijke Bronapparaat tijdens de failover van Hallo nu Hallo doelapparaat. 

Stopt hello i/o- en activiteit van de toepassing en de oorspronkelijke locatie back toohello overgangen tijdens de failback, StorSimple Hallo back toohello primaire gegevenslocatie opnieuw worden gesynchroniseerd.

Nadat een failover voltooid is, voert StorSimple Hallo van de volgende activiteiten:

* StorSimple schoongemaakt hello volumecontainers die worden overgenomen van het bronvolume Hallo.
* StorSimple initieert een achtergrondtaak per volumecontainer (failover) op het bronvolume Hallo. Als u toofail probeert doen terwijl Hallo bezig is, ontvangt u een melding toothat effect. Wacht totdat het Hallo-taak is voltooid toostart Hallo failback.
* Hallo tijd toocomplete Hallo verwijdering van volumecontainers, is afhankelijk van verschillende factoren zoals de hoeveelheid gegevens, de leeftijd van Hallo gegevens, het aantal back-ups en beschikbare Hallo netwerkbandbreedte voor Hallo-bewerking.

Als u van plan bent testfailovers of failbacks te testen, kunt u het beste testen volumecontainers met minder gegevens (GB). Meestal kunt u beginnen Hallo failback 24 uur na het Hallo-failover is voltooid.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

Q. **Wat gebeurt er als Hallo DR mislukt of gedeeltelijk geslaagd is?**

A. Als Hallo DR mislukt, wordt u aangeraden dat u het opnieuw proberen. Hallo tweede apparaat failover-taak is op de hoogte van de voortgang van de eerste taak Hallo Hallo en start vanaf dat moment en hoger.

Q. **Kan ik een apparaat verwijderen terwijl Hallo apparaat failover uitgevoerd wordt?**

A. U kunt een apparaat niet verwijderen, terwijl een DR uitgevoerd wordt. U kunt uw apparaat alleen verwijderen als Hallo DR voltooid is. U kunt de voortgang Hallo apparaat failover-taak in Hallo **taken** blade.

Q. **Wanneer Hallo garbagecollection begint op het bronvolume Hallo zodat Hallo lokale gegevens op het bronvolume is verwijderd?**

A. Garbagecollection is ingeschakeld op het bronvolume Hallo alleen als Hallo-apparaat is volledig opgeschoond. Hallo opschonen bevat objecten die failover van Hallo Bronapparaat zoals volumes, back-objecten (geen gegevens), volumecontainers en beleidsregels voor het opruimen.

Q. **Wat gebeurt er als Hallo taak die is gekoppeld aan Hallo volumecontainers in het bronvolume Hallo verwijderen mislukt?**

A.  Als Hallo verwijderen van taak mislukt, kunt u Hallo volumecontainers handmatig verwijderen. In Hallo **apparaten** blade, selecteer uw Bronapparaat en klik op **volumecontainers**. Selecteer Hallo volumecontainers die u via en Hallo onder Hallo blade in is mislukt, klikt u op **verwijderen**. Nadat u alle Hallo hebt verwijderd volumecontainers op het bronvolume Hallo failover, kunt u beginnen met Hallo failback. Voor meer informatie gaat te[verwijderen van een volumecontainer](storsimple-8000-manage-volume-containers.md#delete-a-volume-container).

## <a name="business-continuity-disaster-recovery-bcdr"></a>Herstel van zakelijke continuïteit na noodgevallen (BCDR)

Een zakelijke continuïteit (BCDR) noodherstelscenario treedt op wanneer Hallo volledige Azure-datacenter niet meer werkt. Dit scenario kan invloed hebben op uw StorSimple-apparaat Manager-service en Hallo bijbehorende StorSimple-apparaten.

Als een StorSimple-apparaat is geregistreerd, net voordat een noodgeval is opgetreden, mogelijk een van de fabrieksinstellingen tooundergo moet op dit apparaat. Na noodgevallen Hallo Hallo StorSimple-apparaat wordt weergegeven in hello Azure-portal als offline. Dit apparaat moet worden verwijderd uit het Hallo-portal. Hallo apparaat toofactory beginwaarden en registreer deze opnieuw met de Hallo-service.

## <a name="next-steps"></a>Volgende stappen

Als u klaar tooperform de failover van een apparaat bent, kies een van Hallo scenario's voor gedetailleerde instructies te volgen:

- [Het fysieke apparaat tooanother failover](storsimple-8000-device-failover-physical-device.md)
- [Failover toohello dezelfde apparaat](storsimple-8000-device-failover-same-device.md)
- [TooStorSimple Cloud toestel failover](storsimple-8000-device-failover-cloud-appliance.md)

Als u uw apparaat hebt failover, kies een Hallo volgende opties:

* [Deactiveren of verwijderen van uw StorSimple-apparaat](storsimple-8000-deactivate-and-delete-device.md).
* [Gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

