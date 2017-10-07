---
title: aaaStorSimple 8000 series systeemlimieten | Microsoft Docs
description: Hierin wordt beschreven systeemlimieten en aanbevolen grootten voor StorSimple 8000 series onderdelen en verbindingen.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c7392678-0924-46c6-9c59-1665cb9b6586
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/28/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: def89a2c1d0ddc71f1743e592c5112b09d72e971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-storsimple-8000-series-system-limits"></a>Wat zijn StorSimple 8000 series system beperkingen?

## <a name="overview"></a>Overzicht

StorSimple biedt schaalbare en flexibele opslag voor uw datacenter. Er zijn echter enkele beperkingen die u rekening houden moet bij het plannen, implementeren en uw StorSimple-oplossing werkt. Hallo volgende tabel beschrijft deze limieten en vindt u enkele aanbevelingen zodat u Hallo meest uw StorSimple-oplossing benutten kunt.

| Limiet-id | Limiet | Opmerkingen |
| --- | --- | --- |
| Maximum aantal opslagaccountreferenties |64 | |
| Maximum aantal volumecontainers |64 | |
| Maximum aantal volumes |255 | |
| Maximum aantal lokaal vastgemaakte volumes |32 | |
| Maximum aantal planningen per bandbreedtesjabloon |168 |Een planning voor elk uur wordt elke dag van week hello (24 * 7). |
| Maximale grootte van een gelaagd volume op fysieke apparaten |64 TB voor 8100 en 8600 |8100 en 8600 zijn fysieke apparaten. |
| Maximale grootte van een gelaagd volume op virtuele apparaten in Azure |8010 30 TB <br></br> 64 TB voor de 8020 |8010 als de 8020 zijn virtuele apparaten in Azure die gebruikmaken van Standard-opslag- en Premium-opslag respectievelijk. |
| Maximale grootte van een lokaal vastgemaakt volume op een fysieke apparaten |8.5 TB voor 8100 <br></br> 22,5 TB voor 8600 |8100 en 8600 zijn fysieke apparaten. |
| Maximum aantal iSCSI-verbindingen |512 | |
| Maximum aantal verbindingen iSCSI-initiators |512 | |
| Maximum aantal access control records per apparaat |64 | |
| Maximum aantal volumes per back-upbeleid |20 | |
| Maximum aantal back-ups behouden per schema (in een back-upbeleid) |64 | |
| Maximum aantal planningen per back-upbeleid |10 | |
| Maximum aantal momentopnamen van elk type kunnen worden bewaard per volume |256 |Dit is inclusief lokale momentopnamen en cloud worden opgeslagen. |
| Maximum aantal momentopnamen die gebruikt in elk apparaat worden kunnen |10.000 | |
| Maximum aantal volumes die kunnen worden verwerkt in de parallelle back-up, herstel, of te klonen |16 |<ul><li>Als er meer dan 16 volumes, worden deze opeenvolgend verwerkt verwerking sleuven beschikbaar komen.</li><li>Nieuwe back-ups van een kloon of een herstelde gelaagd volume is pas mogelijk nadat het Hallo-bewerking is voltooid. Back-ups zijn echter voor een lokaal volume nadat Hallo volume online is toegestaan.</li></ul> |
| Terugzetten en herstellen tijd voor gelaagde volumes klonen |< 2 minuten |<ul><li>Hallo-volume wordt binnen twee minuten na het terugzetten of kloon bewerking, ongeacht de volumegrootte Hallo beschikbaar gesteld.</li><li>Hallo volume de prestaties in eerste instantie mogelijk langzamer dan normaal omdat de meeste Hallo gegevens en metagegevens is nog steeds bevindt zich in Hallo cloud. Prestaties kan verhogen als gegevensoverdrachten van Hallo cloud toohello StorSimple-apparaat.</li><li>Hallo totale tijd toodownload metagegevens is afhankelijk van Hallo volumegrootte toegewezen. Metagegevens is automatisch onder Hallo-apparaat op de achtergrond Hallo met Hallo frequentie van 5 minuten per TB aan volumegegevens toegewezen gebracht. Deze snelheid kan worden beïnvloed door Internet bandbreedte toohello cloud.</li><li>Hallo herstellen of de kloonbewerking is voltooid als alle Hallo metagegevens op Hallo-apparaat is.</li><li>Back-upbewerkingen kunnen niet worden uitgevoerd totdat Hallo herstellen of de kloonbewerking is volledig is voltooid. |
| Herstel de tijd voor lokaal vastgemaakte volumes herstellen |< 2 minuten |<ul><li>Hallo-volume wordt binnen twee minuten Hallo terugzetbewerking, ongeacht de volumegrootte Hallo beschikbaar gesteld.</li><li>Hallo volume de prestaties in eerste instantie mogelijk langzamer dan normaal omdat de meeste Hallo gegevens en metagegevens is nog steeds bevindt zich in Hallo cloud. Prestaties kan verhogen als gegevensoverdrachten van Hallo cloud toohello StorSimple-apparaat.</li><li>Hallo totale tijd toodownload metagegevens is afhankelijk van Hallo volumegrootte toegewezen. Metagegevens is automatisch onder Hallo-apparaat op de achtergrond Hallo met Hallo frequentie van 5 minuten per TB aan volumegegevens toegewezen gebracht. Deze snelheid kan worden beïnvloed door Internet bandbreedte toohello cloud.</li><li>In tegenstelling tot gelaagde volumes, voor lokaal vastgemaakte volumes wordt Hallo volumegegevens ook lokaal gedownload op Hallo-apparaat. Hallo restore-bewerking is voltooid als alle Hallo volumegegevens toohello apparaat weer.</li><li>Hallo herstelbewerkingen mogelijk lang. Hallo totale tijd toocomplete Hallo herstellen, is afhankelijk van Hallo grootte van lokaal volume Hallo ingericht, uw internetbandbreedte en Hallo bestaande gegevens op Hallo-apparaat. Back-upbewerkingen op Hallo lokaal vastgemaakt volume zijn toegestaan terwijl het Hallo-herstelbewerking wordt uitgevoerd. |
| Verwerkingssnelheid voor cloudmomentopnamen van de |15 minuten/TB |<ul><li>Minimale tijd toomake cloudmomentopname Hallo gereed is voor het uploaden, per TB aan volumegegevens in de back-up toegewezen. </li><li> Tijd van totale cloud momentopname wordt berekend door toe te voegen die tijd toohello momentopname uploadtijd die wordt beïnvloed door Hallo Internet bandbreedte toocloud. |
| Maximum aantal clients lezen/schrijven doorvoer (wanneer aangeboden via Hallo SSD-laag) * |920/720 MB/s met een enkele 10 GbE-netwerkinterface |Up too2x met MPIO en twee netwerkinterfaces. |
| Maximum aantal clients lezen/schrijven doorvoer (wanneer aangeboden via Hallo HDD-laag) * |120/250 MB/s | |
| Maximum aantal clients lezen/schrijven doorvoer (wanneer aangeboden via Hallo cloudlaag) * voor Update 3 en hoger ** |40/60 MB/s voor gelaagde volumes<br><br>60/80 MB/s voor gelaagde volumes archivering optie is geselecteerd tijdens het maken van volume |Lees doorvoer is afhankelijk van clients genereren en bijhouden van voldoende i/o-wachtrijdiepte. <br><br>Snelheid bereikt, is afhankelijk van Hallo snelheid van Hallo onderliggende opslagaccount gebruikt. |

&#42; Maximale doorvoer per i/o-type is gemeten met 100 procent lezen en schrijven van 100 procent scenario's. Werkelijke doorvoer mogelijk lager en is afhankelijk van i/o mix en de voorwaarden.

&#42; &#42; Prestaties cijfers voorafgaande tooUpdate 3 mogelijk lager.

## <a name="next-steps"></a>Volgende stappen
Bekijk Hallo [StorSimple systeemvereisten](storsimple-8000-system-requirements.md).

