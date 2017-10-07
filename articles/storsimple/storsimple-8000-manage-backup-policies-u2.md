---
title: aaaManage StorSimple 8000 serie back-upbeleid | Microsoft Docs
description: Legt uit hoe Hallo Apparaatbeheer StorSimple-service toocreate gebruiken en handmatige back-ups, back-upschema en bewaren van back-up op een StorSimple 8000 series apparaat beheren.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>Hallo Apparaatbeheer StorSimple-service gebruiken in Azure portal toomanage back-upbeleid


## <a name="overview"></a>Overzicht

Deze zelfstudie wordt uitgelegd hoe toouse StorSimple-apparaat Manager-service Hallo **back-up maken van beleid** blade toocontrol back-processen en het bewaren van de back-up voor uw StorSimple-volumes. Ook wordt beschreven hoe toocomplete een handmatige back-up.

Wanneer u back-up van een volume, kunt u toocreate kiezen een momentopname van een lokale of een cloudmomentopname van de. Als u een back-up van een lokaal vastgemaakt volume, raden wij aan dat u opgeeft dat een cloudmomentopname. Maken van een groot aantal lokale momentopnamen van een lokaal vastgemaakt volume samen met een gegevensset die een groot aantal verloop heeft resulteert in een situatie waarin u kan snel worden uitgevoerd buiten het lokale ruimte. Als u ervoor tootake lokale momentopnamen kiest, raden wij minder dagelijkse momentopnamen tooback duren voordat de meest recente status hello, behouden voor een dag en verwijder deze.

Wanneer u een cloud momentopname van een lokaal vastgemaakt volume, kopieert u alleen Hallo gewijzigd gegevens toohello cloud, waar het ontdubbeld en gecomprimeerd.

## <a name="hello-backup-policy-blade"></a>blade Hallo back-upbeleid

Hallo **back-up maken van beleid** blade voor uw StorSimple-apparaat kunt u back-upbeleid toomanage en planning van lokale en cloudmomentopnamen. Back-upbeleid zijn gebruikte tooconfigure back-upschema en de back-up van de bewaarperiode voor een verzameling van volumes. Back-upbeleid kunnen u tootake een momentopname van meerdere volumes tegelijkertijd. Dit betekent dat Hallo back-ups die zijn gemaakt door een back-upbeleid crashconsistent exemplaren.

Hallo back-upbeleid in tabelvorm aanbieding kunt ook u toofilter Hallo bestaande back-upbeleid door een of meer van de volgende velden Hallo:

* **De naam van beleid** – hello naam gekoppeld aan het Hallo-beleid. verschillende soorten beleid Hallo zijn onder andere:

  * Geplande beleidsregels die expliciet zijn gemaakt door gebruiker Hallo.
  * Beleidsregels die oorspronkelijk zijn gemaakt in Hallo StorSimple Snapshot Manager geïmporteerd. Deze hebben een code die wordt beschreven Hallo StorSimple Snapshot Manager host die Hallo beleidsregels zijn geïmporteerd uit.

  > [!NOTE]
  > Automatische of standaard back-upbeleid zijn niet meer ingeschakeld bij Hallo volume maken.

* **Laatste geslaagde back-up** – Hallo-datum en tijd van Hallo laatste geslaagde back-up die is uitgevoerd met dit beleid.

* **Volgende back-up** – Hallo-datum en tijd van Hallo volgende geplande back-up die door dit beleid wordt gestart.

* **Volumes** – Hallo volumes die zijn gekoppeld aan het Hallo-beleid. Alle Hallo volumes die zijn gekoppeld aan een back-upbeleid worden gegroepeerd wanneer back-ups worden gemaakt.

* **Planningen** – aantal schema's die zijn gekoppeld aan de back-upbeleid Hallo Hallo.

Hallo veelgebruikte bewerkingen die u voor back-upbeleid uitvoeren kunt zijn:

* Een back-upbeleid toevoegen
* Toevoegen of wijzigen van een planning
* Toevoegen of verwijderen van een volume
* Een back-upbeleid te verwijderen
* Maak een handmatige back-up

## <a name="add-a-backup-policy"></a>Een back-upbeleid toevoegen

Toevoegen van een back-upbeleid tooautomatically planning uw back-ups. Wanneer u een volume maakt, is er geen back-standaardbeleid die zijn gekoppeld aan het volume. U moet tooadd en toewijzen van een back-upbeleid tooprotect volumegegevens.

Volgende stappen uit in Azure portal tooadd een back-upbeleid voor uw StorSimple-apparaat Hallo Hallo uitvoeren. Nadat u Hallo beleid hebt toegevoegd, kunt u een schema definiëren (Zie [toevoegen of wijzigen van een planning](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>Toevoegen of wijzigen van een planning

U kunt toevoegen of wijzigen van een planning die is aangesloten tooan bestaande back-upbeleid op uw StorSimple-apparaat. Uitvoeren van de volgende stappen uit in Azure portal tooadd Hallo Hallo of te wijzigen.

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>Toevoegen of verwijderen van een volume

U kunt toevoegen of verwijderen van een volume toegewezen tooa back-upbeleid op uw StorSimple-apparaat. Volgende stappen uit in Azure portal tooadd Hallo Hallo uitvoeren of verwijderen van een volume.

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>Een back-upbeleid te verwijderen

Voer Hallo stappen te volgen in hello Azure portal toodelete een back-upbeleid op uw StorSimple-apparaat.

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Maak een handmatige back-up

Hallo stappen te volgen in (hello Azure portal toocreate op aanvraag handmatige) back-up voor één volume uitvoeren.

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).

