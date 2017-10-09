---
title: een StorSimple-volume van back-up aaaRestore | Microsoft Docs
description: Legt uit hoe toouse Hallo StorSimple Manager service back-upcatalogus pagina toorestore een StorSimple-volume vanuit een back-upset.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Een StorSimple-volume herstelt vanuit een back-upset
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Overzicht
Hallo **back-upcatalogus** pagina wordt weergegeven voor alle Hallo back-upsets die worden gemaakt wanneer de handmatige of automatische back-ups worden gemaakt. U kunt alle Hallo back-ups van deze pagina toolist gebruiken voor een back-upbeleid of een volume, selecteer of verwijderen back-ups, of een back-toorestore gebruiken of een volume klonen.

 ![Back-pagina van de catalogus](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

Deze zelfstudie wordt uitgelegd hoe toouse hello **back-upcatalogus** pagina toorestore een volume op uw apparaat bij een back-upset.

## <a name="how-toouse-hello-backup-catalog"></a>Hoe toouse Hallo back-upcatalogus
Hallo **back-upcatalogus** pagina vindt u een query waarmee u toonarrow uw selectie back-upset. U kunt Hallo back-upsets die worden opgehaald op basis van de volgende parameters Hallo filteren:

* **Apparaat** – Hallo-apparaat op welke Hallo back-upset is gemaakt.
* **Back-up maken van beleid** of **volume** – Hallo back-upbeleid of volume dat is gekoppeld aan deze back-upset.
* **Van** en **naar** – Hallo bereik datum en tijd wanneer Hallo back-upset is gemaakt.

Hallo gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:

* **Naam** – hello naam van back-upbeleid Hallo of volumes die zijn gekoppeld aan de back-upset Hallo.
* **De grootte van** – werkelijke grootte van de back-upset Hallo Hallo.
* **Gemaakt op** : Hallo datum en tijd waarop Hallo back-ups zijn gemaakt. 
* **Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen. Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op Hallo-apparaat dat een cloudmomentopname toohello back-up van volumegegevens in de cloud Hallo verwijst. Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.
* **Gestart door** – Hallo back-ups worden geïnitieerd automatisch volgens tooa schema of handmatig door een gebruiker. (U kunt een back-upbeleid tooschedule back-ups. U kunt ook hello gebruiken **back-up maken** optie tootake een interactieve back-up.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Hoe toorestore uw StorSimple-volume van een back-up
U kunt Hallo **back-upcatalogus** pagina toorestore uw StorSimple-volume van een specifieke back-up. 

> [!WARNING]
> Terugzetten vanuit een back-up wordt vervangen door bestaande volumes Hallo van Hallo back-up. Hierdoor kunnen Hallo verlies van gegevens die is geschreven nadat Hallo back-up is gemaakt.
> 
> 

Voordat u een herstelpunt op een volume hebt gestart, zorg ervoor dat de Hallo volume offline is. U moet tootake Hallo volume offline op host Hallo eerst en vervolgens Hallo apparaat. Volg de stappen Hallo in [offline zetten van een volume](storsimple-manage-volumes.md#take-a-volume-offline). Volgende stappen toorestore een volume uit een back-upset Hallo uitvoeren.

### <a name="toorestore-from-a-backup-set"></a>toorestore vanuit een back-upset
1. Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad.
   
    ![Back-upcatalogus](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. Selecteer een back-up als volgt instellen:
   
   1. Selecteer het juiste apparaat Hallo.
   2. Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.
   3. Hallo tijdsperiode opgeven.
   4. Klik op het vinkje Hallo ![vinkje](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) tooexecute deze query.
      
      Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.
3. Vouw Hallo back-upset tooview Hallo gekoppeld volumes. Deze volumes moeten op Hallo host en het apparaat offline worden genomen voordat u ze kunt herstellen. Volg de stappen Hallo in [offline zetten van een volume](storsimple-manage-volumes.md#take-a-volume-offline).
   
   > [!IMPORTANT]
   > Zorg ervoor dat u hebt ondernomen Hallo volumes offline op Hallo host eerst voordat u Hallo volumes offline op Hallo-apparaat nemen. Als u niet Hallo volumes offline op Hallo host nemen, kan deze toodata beschadiging leiden.
   > 
   > 
4. Selecteer een back-upset. Klik op **herstellen** Hallo Hallo pagina onderaan in.
5. U wordt gevraagd om bevestiging. 
   
    ![Bevestigingspagina](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. Raadpleeg Hallo terugzetten informatie en klik op het vinkje Hallo ![vinkje](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png). Er wordt nu een hersteltaak die u bekijken kunt door het openen van Hallo **taken** pagina. 
7. Nadat het Hallo herstellen is voltooid, kunt u controleren dat Hallo inhoud van uw volumes worden vervangen door de volumes van Hallo back-up.

![Video beschikbaar](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe gebruikt u de Hallo klonen en herstellen van functies in StorSimple toorecover verwijderde bestanden, klikt u op [hier](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[beheren StorSimple-volumes](storsimple-manage-volumes.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

