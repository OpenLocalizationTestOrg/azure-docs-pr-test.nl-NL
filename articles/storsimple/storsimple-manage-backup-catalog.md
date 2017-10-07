---
title: aaaManage uw StorSimple-back-upcatalogus | Microsoft Docs
description: Legt uit hoe toouse hello StorSimple Manager service back-upcatalogus pagina toolist selecteren en back-upsets voor een volume verwijderen.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>Hallo StorSimple Manager-service toomanage uw back-upcatalogus gebruiken
## <a name="overview"></a>Overzicht
Hallo StorSimple Manager-service **back-upcatalogus** pagina wordt weergegeven voor alle Hallo back-upsets die worden gemaakt wanneer de handmatige of geplande back-ups worden gemaakt. U kunt alle Hallo back-ups van deze pagina toolist gebruiken voor een back-upbeleid of een volume, selecteer of verwijderen back-ups, of een back-toorestore gebruiken of een volume klonen.

Deze zelfstudie wordt uitgelegd hoe toolist, selecteer en delete een back-upset. toolearn hoe toorestore uw apparaat bij back-up, gaat u te[uw apparaat terugzetten vanaf een back-upset](storsimple-restore-from-backup-set.md). hoe tooclone een volume te gaan toolearn[klonen van een StorSimple-volume](storsimple-clone-volume.md).

![Back-upcatalogus](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Hallo **back-upcatalogus** pagina vindt u een query toonarrow uw selectie back-upset. U kunt back-upsets Hallo die zijn opgehaald, op basis van de volgende parameters Hallo filteren:

* **Apparaat** – Hallo-apparaat op welke Hallo back-upset is gemaakt.
* **Back-up maken van beleid of Volume** – Hallo back-upbeleid of volume dat is gekoppeld aan deze back-upset.
* **Van en naar** – Hallo bereik datum en tijd wanneer Hallo back-upset is gemaakt.

Hallo gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:

* **Naam** – hello naam van back-upbeleid Hallo of volumes die zijn gekoppeld aan de back-upset Hallo.
* **De grootte van** – werkelijke grootte van de back-upset Hallo Hallo.
* **Gemaakt op** : Hallo datum en tijd waarop Hallo back-ups zijn gemaakt. 
* **Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen. Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op Hallo-apparaat dat een cloudmomentopname toohello back-up van volumegegevens in de cloud Hallo verwijst. Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.
* **Gestart door** – Hallo back-ups automatisch kunnen worden gestart door een schema of handmatig door een gebruiker. U kunt een back-upbeleid tooschedule back-ups. U kunt ook hello gebruiken **back-up maken** optie tootake een handmatige back-up.

## <a name="list-backup-sets-for-a-volume"></a>Lijst met back-up wordt ingesteld voor een volume
De volgende volledige Hallo stappen toolist alle Hallo back-ups voor een volume.

#### <a name="toolist-backup-sets"></a>back-upsets toolist
1. Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad.
2. Filter Hallo selecties als volgt:
   
   1. Selecteer het juiste apparaat Hallo.
   2. In de vervolgkeuzelijst hello, kiest u een volume tooview Hallo bijbehorende Hallo back-ups.
   3. Hallo tijdsperiode opgeven.
   4. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute deze query.
      
      Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume moeten worden weergegeven in de lijst Hallo van back-upsets.

## <a name="select-a-backup-set"></a>Selecteer een back-upset
Volledige Hallo tooselect stappen na een back-up instellen voor een volume of back-up-beleid.

#### <a name="tooselect-a-backup-set"></a>een back-upset tooselect
1. Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad.
2. Filter Hallo selecties als volgt:
   
   1. Selecteer het juiste apparaat Hallo.
   2. Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.
   3. Hallo tijdsperiode opgeven.
   4. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute deze query.
      
      Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.
3. Selecteer en breid uit een back-upset. Hallo **herstellen** en **verwijderen** opties onder Hallo van Hallo pagina worden weergegeven. U kunt een van deze acties uitvoeren op Hallo back-upset die u hebt geselecteerd.

## <a name="delete-a-backup-set"></a>Een back-upset verwijderen
Een back-up verwijderen als u niet langer wenst dat tooretain Hallo-gegevens gekoppeld. Volgende stappen toodelete een back-upset Hallo uitvoeren.

#### <a name="toodelete-a-backup-set"></a>een back-upset toodelete
1. Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus tabblad**.
2. Filter Hallo selecties als volgt:
   
   1. Selecteer het juiste apparaat Hallo.
   2. Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.
   3. Hallo tijdsperiode opgeven.
   4. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute deze query.
      
      Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.
3. Selecteer en breid uit een back-upset. Hallo **herstellen** en **verwijderen** opties onder Hallo van Hallo pagina worden weergegeven. Klik op **Verwijderen**.
4. U wordt gewaarschuwd wanneer Hallo verwijdering uitgevoerd wordt en wanneer is voltooid. Nadat de Hallo verwijdering is voltooid, kunt u Hallo query op deze pagina vernieuwen. back-upset Hallo verwijderd weergegeven niet meer in de lijst Hallo van back-upsets.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[gebruik Hallo back-upcatalogus toorestore uw apparaat bij een back-upset](storsimple-restore-from-backup-set.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

