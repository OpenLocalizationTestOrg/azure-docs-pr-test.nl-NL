---
title: aaaManage uw StorSimple-back-upbeleid | Microsoft Docs
description: Legt uit hoe Hallo StorSimple Manager-service toocreate gebruiken en beheren van handmatige back-ups, back-upschema en bewaren van back-up.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a>Hallo StorSimple Manager-service toomanage back-upbeleid gebruiken
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Manager-service Hallo **back-upbeleid** pagina toocontrol back-processen en het bewaren van de back-up voor uw StorSimple-volumes. Ook wordt beschreven hoe toocomplete een handmatige back-up.

Hallo **back-upbeleid** pagina kunt u back-upbeleid toomanage en planning van lokale en cloudmomentopnamen. (Back-upbeleid zijn gebruikte tooconfigure back-upschema's en het bewaren van de back-up voor een verzameling van volumes). Back-upbeleid kunnen u tootake een momentopname van meerdere volumes tegelijkertijd. Dit betekent dat Hallo back-ups die zijn gemaakt door een back-upbeleid crashconsistent exemplaren. Deze pagina bevat Hallo back-upbeleid, hun typen, volumes Hallo die zijn gekoppeld, Hallo aantal back-ups behouden en Hallo optie tooenable deze beleidsregels.

Hallo **back-upbeleid** pagina kunt u ook toofilter Hallo bestaande back-upbeleid door een of meer van de volgende velden Hallo:

* **De naam van beleid** – hello naam gekoppeld aan het Hallo-beleid. verschillende soorten beleid Hallo zijn onder andere:
  
  * Geplande beleidsregels die expliciet zijn gemaakt door gebruiker Hallo.
  * Automatische beleidsregels die worden gemaakt wanneer Hallo standaardback-up voor deze optie volume gelijktijdig Hallo met maken van volumes is ingeschakeld. Deze beleidsregels zijn benoemde als VolumeName_Default waarbij volumenaam toohello-naam van het StorSimple-volume is geconfigureerd door de gebruiker in de klassieke Azure-portal Hallo HALLO hallo verwijst. Hallo automatische beleid resulteert in dagelijkse cloudmomentopnamen beginnen bij 22.30 tijd op het apparaat.
  * Beleidsregels die oorspronkelijk zijn gemaakt in Hallo StorSimple Snapshot Manager geïmporteerd. Deze hebben een code die wordt beschreven Hallo StorSimple Snapshot Manager host die Hallo beleidsregels zijn geïmporteerd uit.
* **Volumes** – Hallo volumes die zijn gekoppeld aan het Hallo-beleid. Alle Hallo volumes die zijn gekoppeld aan een back-upbeleid worden gegroepeerd wanneer back-ups worden gemaakt.
* **Laatste geslaagde back-up** – Hallo-datum en tijd van Hallo laatste geslaagde back-up die is uitgevoerd met dit beleid.
* **Volgende back-up** – Hallo-datum en tijd van Hallo volgende geplande back-up die door dit beleid wordt gestart.
* **Planningen** – aantal schema's die zijn gekoppeld aan de back-upbeleid Hallo Hallo.

Hallo veelgebruikte bewerkingen die u op deze pagina uitvoeren kunt zijn:

* Een back-upbeleid toevoegen 
* Toevoegen of wijzigen van een planning 
* Een back-upbeleid te verwijderen 
* Maak een handmatige back-up 
* Een aangepaste back-upbeleid maken met meerdere volumes en schema 's 

## <a name="add-a-backup-policy"></a>Een back-upbeleid toevoegen
Toevoegen van een back-upbeleid tooautomatically planning uw back-ups. Voer Hallo stappen te volgen in hello Azure classic portal tooadd een back-upbeleid voor uw StorSimple-apparaat. Nadat u Hallo beleid hebt toegevoegd, kunt u een schema definiëren (Zie [toevoegen of wijzigen van een planning](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

![Video beschikbaar](./media/storsimple-manage-backup-policies/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe toocreate een lokaal of in de cloud back-up-beleid, klikt u op [hier](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Toevoegen of wijzigen van een planning
U kunt toevoegen of wijzigen van een planning die is aangesloten tooan bestaande back-upbeleid op uw StorSimple-apparaat. Hallo stappen te volgen in hello Azure classic portal tooadd uitvoeren of een schema wijzigen.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a>Een back-upbeleid te verwijderen
Voer Hallo stappen te volgen in hello Azure classic portal toodelete een back-upbeleid op uw StorSimple-apparaat.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Maak een handmatige back-up
Hallo stappen te volgen in (hello Azure classic portal toocreate op aanvraag handmatige) back-up voor één volume uitvoeren.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Een aangepaste back-upbeleid maken met meerdere volumes en schema 's
Hallo stappen te volgen in hello Azure classic portal toocreate een aangepaste back-upbeleid met meerdere volumes en schema's uitvoeren.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).

