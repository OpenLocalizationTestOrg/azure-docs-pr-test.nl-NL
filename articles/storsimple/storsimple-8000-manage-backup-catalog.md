---
title: aaaManage uw StorSimple-back-upcatalogus | Microsoft Docs
description: Legt uit hoe toouse hello StorSimple Apparaatbeheer service back-upcatalogus pagina toolist selecteren en back-upsets verwijderen.
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>Hallo Apparaatbeheer StorSimple-service toomanage uw back-upcatalogus gebruiken
## <a name="overview"></a>Overzicht
Hallo StorSimple-apparaat Manager-service **back-upcatalogus** blade geeft alle Hallo back-upsets die worden gemaakt wanneer de handmatige of geplande back-ups worden gemaakt. U kunt alle Hallo back-ups van deze pagina toolist gebruiken voor een back-upbeleid of een volume, selecteer of verwijderen back-ups, of een back-toorestore gebruiken of een volume klonen.

Deze zelfstudie wordt uitgelegd hoe toolist, selecteer en delete een back-upset. toolearn hoe toorestore uw apparaat bij back-up, gaat u te[uw apparaat terugzetten vanaf een back-upset](storsimple-8000-restore-from-backup-set-u2.md). hoe tooclone een volume te gaan toolearn[klonen van een StorSimple-volume](storsimple-8000-clone-volume-u2.md).

![Back-upcatalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

Hallo **back-upcatalogus** blade biedt een query toonarrow uw selectie back-upset. U kunt back-upsets Hallo die zijn opgehaald, op basis van de volgende parameters Hallo filteren:

* **Apparaat** – Hallo-apparaat op welke Hallo back-upset is gemaakt.
* **Back-upbeleid of Volume** – Hallo back-upbeleid of volume dat is gekoppeld aan deze back-upset.
* **Van en naar** – Hallo bereik datum en tijd wanneer Hallo back-upset is gemaakt.

Hallo gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:

* **Naam** – hello naam van back-upbeleid Hallo of volumes die zijn gekoppeld aan de back-upset Hallo.
* **De grootte van** – werkelijke grootte van de back-upset Hallo Hallo.
* **Gemaakt op** : Hallo datum en tijd waarop Hallo back-ups zijn gemaakt. 
* **Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen. Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op Hallo-apparaat dat een cloudmomentopname toohello back-up van volumegegevens in de cloud Hallo verwijst. Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.
* **Gestart door** – Hallo back-ups automatisch kunnen worden gestart door een schema of handmatig door een gebruiker. U kunt een back-upbeleid tooschedule back-ups. U kunt ook hello gebruiken **back-up maken** optie tootake een handmatige back-up.

## <a name="list-backup-sets-for-a-backup-policy"></a>Lijst met back-up wordt ingesteld voor een back-upbeleid
Volgende stappen toolist Hallo alle Hallo back-ups voor een back-upbeleid voltooien.

#### <a name="toolist-backup-sets"></a>back-upsets toolist
1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **back-upcatalogus**.

2. Filter Hallo selecties als volgt:
   
   1. Hallo tijdsperiode opgeven.
   2. Selecteer het juiste apparaat Hallo.
   3. Filteren op **back-up maken van beleid** tooview Hallo bijbehorende Hallo back-ups.
   3. Kies in de back-upbeleid vervolgkeuzelijst Hallo **alle** tooview alle back-ups op Hallo geselecteerd Hallo apparaat.
   4. Klik op **toepassen** tooexecute deze query.
      
      Hallo back-ups die zijn gekoppeld aan de back-upbeleid Hallo geselecteerd moeten worden weergegeven in de lijst Hallo van back-upsets.

      ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>Selecteer een back-upset
Volledige Hallo tooselect stappen na een back-up instellen voor een volume of back-up-beleid.

#### <a name="tooselect-a-backup-set"></a>een back-upset tooselect
1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **back-upcatalogus**.
2. Filter Hallo selecties als volgt:
   
   1. Hallo tijdsperiode opgeven. 
   2. Selecteer het juiste apparaat Hallo. 
   3. Filteren op een volume of back-up beleid voor back-up Hallo gewenste tooselect.
   4. Klik op **toepassen** tooexecute deze query.
      
      Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.

      ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Selecteer en breid uit een back-upset. U ziet nu de back-upsets Hallo uitgesplitst Hallo volumes die deze bevat. Hallo **herstellen** en **verwijderen** opties zijn beschikbaar via Hallo contextmenu (Klik met de rechtermuisknop) voor back-upset Hallo. U kunt een van deze acties uitvoeren op Hallo back-upset die u hebt geselecteerd.

    ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>Een back-upset verwijderen
Een back-up verwijderen als u niet langer wenst dat tooretain Hallo-gegevens gekoppeld. Volgende stappen toodelete een back-upset Hallo uitvoeren.

#### <a name="toodelete-a-backup-set"></a>een back-upset toodelete
 Ga tooyour Apparaatbeheer StorSimple-service en klik op **back-upcatalogus**.
2. Filter Hallo selecties als volgt:
   
   1. Hallo tijdsperiode opgeven. 
   2. Selecteer het juiste apparaat Hallo. 
   3. Filteren op een volume of back-up beleid voor back-up Hallo gewenste tooselect.
   4. Klik op **toepassen** tooexecute deze query.
      
      Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.

      ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Selecteer en breid uit een back-upset. U ziet nu de back-upsets Hallo uitgesplitst Hallo volumes die deze bevat. Hallo **herstellen** en **verwijderen** opties zijn beschikbaar via Hallo contextmenu (Klik met de rechtermuisknop) voor back-upset Hallo. Met de rechtermuisknop op de back-upset Hallo geselecteerd en selecteer in het contextmenu hello, **verwijderen**.

    ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. Wanneer u wordt gevraagd om bevestiging, Raadpleeg Hallo weergegeven informatie en klik op **verwijderen**. de geselecteerde back-up Hello wordt permanent verwijderd.

    ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. U wordt gewaarschuwd wanneer Hallo verwijdering uitgevoerd wordt en wanneer is voltooid. Nadat de Hallo verwijdering is voltooid, kunt u Hallo query op deze pagina vernieuwen. back-upset Hallo verwijderd weergegeven niet meer in de lijst Hallo van back-upsets.

    ![Ga toobackup catalogus](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[gebruik Hallo back-upcatalogus toorestore uw apparaat bij een back-upset](storsimple-8000-restore-from-backup-set-u2.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

