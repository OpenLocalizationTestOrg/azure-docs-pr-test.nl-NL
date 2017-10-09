---
title: aaaStorSimple Snapshot Manager back-upcatalogus | Microsoft Docs
description: Hierin wordt beschreven hoe toouse StorSimple Snapshot Manager MMC-module tooview Hallo en back-upcatalogus Hallo beheren.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>Gebruik StorSimple Snapshot Manager toomanage Hallo back-upcatalogus

## <a name="overview"></a>Overzicht
Hallo primaire functie van StorSimple Snapshot Manager is tooallow u toocreate toepassingsconsistente back-up van de StorSimple-volumes in de vorm Hallo van momentopnamen. Momentopnamen worden vermeld in een XML-bestand met de naam een *back-upcatalogus*. back-upcatalogus Hallo ordent momentopnamen op volume groep en vervolgens op de lokale momentopname of cloudmomentopname van de.

Deze zelfstudie wordt beschreven hoe u kunt Hallo **back-upcatalogus** knooppunt toocomplete Hallo taken te volgen:

* Een volume herstellen
* Klonen van een volume of een volume-groep
* Verwijderen van een back-up
* Herstellen van een bestand
* Hallo Storsimple Snapshot Manager-database herstellen

U kunt back-upcatalogus Hallo weergeven door het uitbreiden van Hallo **back-upcatalogus** knooppunt in Hallo **bereik** deelvenster en vervolgens uitbreiden Hallo volume groep.

* Als u de naam van de groep volume Hallo klikt, Hallo **resultaten** deelvenster Hallo aantal lokale momentopnamen en cloudmomentopnamen die beschikbaar zijn voor Hallo volume groep bevat. 
* Als u op **lokale momentopname** of **Cloudmomentopname**, Hallo **resultaten** deelvenster bevat informatie over elke back-upmomentopname te volgen Hallo (afhankelijk van uw **Weergave** instellingen):
  
  * **Naam** – Hallo tijd Hallo momentopname werd gemaakt.
  * **Type** – of dit een momentopname van een lokale of een cloudmomentopname van de is.
  * **Eigenaar** – Hallo de eigenaar van inhoud. 
  * **Beschikbare** – of Hallo momentopname momenteel beschikbaar is. **De waarde True** geeft aan dat Hallo-momentopname beschikbaar is en kan worden hersteld; **False** geeft aan dat Hallo momentopname is niet meer beschikbaar. 
  * **Geïmporteerd** – of Hallo back-up is geïmporteerd. **De waarde True** geeft aan dat Hallo back-up is geïmporteerd uit Hallo Apparaatbeheer StorSimple-service op Hallo tijd Hallo apparaat is geconfigureerd in StorSimple Snapshot Manager; **False** geeft aan dat het is niet geïmporteerd, maar door StorSimple Snapshot Manager is gemaakt. (U eenvoudig kunt herkennen een groep geïmporteerde volume omdat een achtervoegsel wordt toegevoegd die identificeert Hallo apparaat waaruit Hallo volume groep is geïmporteerd.)
    
    ![Back-upcatalogus](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* Als u wilt uitbreiden **lokale momentopname** of **Cloudmomentopname**, en klik vervolgens op de naam van een afzonderlijke momentopname hello **resultaten** deelvenster Hallo volgende informatie over Hallo bevat de momentopname die u hebt geselecteerd:
  
  * **Naam** – Hallo volume geïdentificeerd met een stationsletter. 
  * **Lokale naam** – Hallo lokale naam van Hallo station (indien beschikbaar). 
  * **Apparaat** – hello naam van het Hallo-apparaat op welke Hallo volume zich bevindt. 
  * **Beschikbare** – of Hallo momentopname momenteel beschikbaar is. **De waarde True** geeft aan dat Hallo-momentopname beschikbaar is en kan worden hersteld; **False** geeft aan dat Hallo momentopname is niet meer beschikbaar. 

## <a name="restore-a-volume"></a>Een volume herstellen
Hallo te volgen procedure toorestore een volume van back-up gebruiken.

#### <a name="prerequisites"></a>Vereisten
Als u dit nog niet hebt gedaan, maakt u een volume en volume-groep en verwijder vervolgens Hallo volume. Standaard StorSimple Snapshot Manager back-ups van een volume voordat deze toobe verwijderd. Deze voorzorgsmaatregel kan geen gegevens verloren gaan als Hallo volume per ongeluk is verwijderd of als Hallo gegevens toobe hersteld om welke reden moeten. 

Hallo-bericht te volgen bij het maken van Hallo voorzorgsmaatregelen back-up weergeven StorSimple Snapshot Manager

![Automatische momentopname bericht](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> U kunt een volume dat deel uitmaakt van een volume-groep niet verwijderen. de optie verwijderen Hallo is niet beschikbaar. <br>
> 
> 

#### <a name="toorestore-a-volume"></a>een volume toorestore
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager. 
2. In Hallo **bereik** deelvenster Vouw Hallo **back-upcatalogus** knooppunt, een volume uitvouwen en klik vervolgens op **lokale momentopnamen** of **Cloudmomentopnamen**. Een lijst met back-upmomentopnamen wordt weergegeven in Hallo **resultaten** deelvenster.
3. Zoeken naar Hallo back-up dat u wilt toorestore, klik met de rechtermuisknop en klik vervolgens op **herstellen**.
   
    ![Terugzetten van back-upcatalogus](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. Typ op de bevestigingspagina hello, Controleer de details hello, **bevestigen**, en klik vervolgens op **OK**. StorSimple Snapshot Manager maakt gebruik van Hallo back-toorestore Hallo volume.
   
    ![Bevestigingsbericht herstellen](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. Als dit wordt uitgevoerd, kunt u de herstelbewerking Hallo bewaken. In Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik vervolgens op **met**. Hallo taakdetails worden weergegeven in Hallo **resultaten** deelvenster. Wanneer de hersteltaak Hallo is voltooid, Hallo taakdetails zijn overgedragen toohello **afgelopen 24 uur** lijst.

## <a name="clone-a-volume-or-volume-group"></a>Klonen van een volume of een volume-groep
Hallo te volgen procedure toocreate dubbel (klonen) van een volume of de volume-groep gebruiken.

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone een volume of volume-groep
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster Vouw Hallo **back-upcatalogus** knooppunt, een volume uitvouwen en klik vervolgens op **Cloudmomentopnamen**. Een lijst van back-ups wordt weergegeven in Hallo **resultaten** deelvenster.
3. Hallo-volume of groep volume dat u tooclone, klik met de rechtermuisknop Hallo volume of de naam van volume wilt en klik op Zoeken **kloon**. Hallo **Cloudmomentopname kloon** dialoogvenster wordt weergegeven.
   
    ![Klonen van een cloudmomentopname](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Volledige Hallo **kloon Cloudmomentopname** in het dialoogvenster als volgt: 
   
   1. In Hallo **naam** in het tekstvak, typ een naam voor Hallo gekloond volume. Deze naam wordt weergegeven in Hallo **Volumes** knooppunt. 
   2. (Optioneel) Selecteer **station**, en selecteer vervolgens een stationsletter op Hallo vervolgkeuzelijst.
   3. (Optioneel) Selecteer **map (NTFS)**, en typt u een pad naar de map of klik op Bladeren en selecteer een locatie voor het Hallo-map. 
   4. Klik op **Create**.
5. Wanneer Hallo klonen proces is voltooid, moet u Hallo gekloond volume initialiseren. Start Serverbeheer en start Schijfbeheer. Zie voor gedetailleerde instructies [volumes koppelen](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Nadat deze is geïnitialiseerd, Hallo volume worden vermeld onder Hallo **Volumes** knooppunt in Hallo **bereik** deelvenster. Als er geen Hallo volume dat wordt vermeld, Hallo-lijst van volumes vernieuwen (Klik met de rechtermuisknop Hallo **Volumes** knooppunt en klik vervolgens op **vernieuwen**).

## <a name="delete-a-backup"></a>Verwijderen van een back-up
Hallo volgen procedure toodelete een momentopname van de back-upcatalogus hello gebruiken. 

> [!NOTE]
> Verwijderen van een momentopname worden back-upgegevens die zijn gekoppeld aan de momentopname Hallo Hallo verwijderd. Proces van het opschonen van gegevens uit de cloud Hallo Hallo kan echter enige tijd duren.<br>


#### <a name="toodelete-a-backup"></a>toodelete een back-up
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster Vouw Hallo **back-upcatalogus** knooppunt, een volume uitvouwen en klik vervolgens op **lokale momentopnamen** of **Cloudmomentopnamen**. Een lijst van momentopnamen wordt weergegeven in Hallo **resultaten** deelvenster.
3. Klik met de rechtermuisknop Hallo momentopname u toodelete wilt en klik vervolgens op **verwijderen**.
4. Wanneer het Hallo-bevestigingsbericht wordt weergegeven, klikt u op **OK**.

## <a name="recover-a-file"></a>Herstellen van een bestand
Als een bestand per ongeluk worden verwijderd van een volume, kunt u Hallo bestand herstellen door op te halen van een momentopname die vooraf datums Hallo verwijdering Hallo momentopname toocreate met een kloon van Hallo volume en vervolgens kopiëren van het Hallo-bestand van Hallo gekloonde volume toohello oorspronkelijke volume.

#### <a name="prerequisites"></a>Vereisten
Voordat u begint, zorg ervoor dat er een recente back-up van Hallo volume groep. Verwijder het bestand opgeslagen op een van de volumes Hallo in die groep volume. Gebruik tot slot de volgende stappen toorestore Hallo verwijderd bestand uit de back-up Hallo. 

#### <a name="toorecover-a-deleted-file"></a>toorecover een verwijderd bestand
1. Klik op Hallo StorSimple Snapshot Manager-pictogram op het bureaublad. Hallo StorSimple Snapshot Manager-console-venster wordt weergegeven. 
2. In Hallo **bereik** deelvenster Vouw Hallo **back-upcatalogus** knooppunt en bladeren tooa momentopname met Hallo verwijderd bestand. Normaal gesproken moet u een momentopname die net vóór Hallo verwijdering is gemaakt.
3. Zoeken naar Hallo volume dat u wilt tooclone, klik met de rechtermuisknop en klik op **kloon**. Hallo **Cloudmomentopname kloon** dialoogvenster wordt weergegeven.
   
    ![Klonen van een cloudmomentopname](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Volledige Hallo **kloon Cloudmomentopname** in het dialoogvenster als volgt: 
   
   1. In Hallo **naam** in het tekstvak, typ een naam voor Hallo gekloond volume. Deze naam wordt weergegeven in Hallo **Volumes** knooppunt. 
   2. (Optioneel) Selecteer **station**, en selecteer vervolgens een stationsletter op Hallo vervolgkeuzelijst. 
   3. (Optioneel) Selecteer **map (NTFS)**, en typ het pad naar een map of klik op **Bladeren** en selecteer een locatie voor Hallo-map. 
   4. Klik op **Create**. 
5. Wanneer Hallo klonen proces is voltooid, moet u Hallo gekloond volume initialiseren. Start Serverbeheer en start Schijfbeheer. Zie voor gedetailleerde instructies [volumes koppelen](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Nadat deze is geïnitialiseerd, Hallo volume worden vermeld onder Hallo **Volumes** knooppunt in Hallo **bereik** deelvenster. 
   
    Als er geen Hallo volume dat wordt vermeld, Hallo-lijst van volumes vernieuwen (Klik met de rechtermuisknop Hallo **Volumes** knooppunt en klik vervolgens op **vernieuwen**).
6. Open Hallo NTFS-map met Hallo gekloond volume, vouw Hallo **Volumes** knooppunt en open vervolgens Hallo gekloond volume. Hallo-bestand dat u toorecover wilt en kopieert u deze primaire volume toohello vinden.
7. Nadat u Hallo-bestand te herstellen, kunt u Hallo NTFS-map met Hallo gekloond volume verwijderen.

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>Hallo StorSimple Snapshot Manager-database herstellen
Regelmatig een back-up Hallo StorSimple Snapshot Manager-database op de hostcomputer Hallo. Als een noodsituatie voordoet of hostcomputer Hallo uitvalt, kunt u het terugzetten van back-up Hallo. Back-up van maken Hallo database is een handmatig proces.

#### <a name="tooback-up-and-restore-hello-database"></a>tooback up en herstel de database Hallo
1. Hallo Microsoft StorSimple Management-Service stoppen:
   
   1. Start Serverbeheer.
   2. Op Hallo Server Manager dashboard op Hallo **extra** selecteert u **Services**.
   3. Op Hallo **Services** venster, selecteer Hallo **Microsoft StorSimple Management Service**.
   4. In Hallo rechtermuisknop deelvenster onder **Microsoft StorSimple Management Service**, klikt u op **Hallo-service stoppen**.
2. Blader op de hostcomputer Hallo tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData is een verborgen map.
   > 
   > 
3. Hallo catalogus XML-bestand, Hallo-bestand kopiëren en opslaan Hallo kopiëren zoeken in een veilige locatie of in Hallo cloud. Als Hallo host mislukt, kunt u deze back-upbestand toohelp herstellen Hallo back-upbeleid dat u hebt gemaakt in StorSimple Snapshot Manager.
   
    ![Azure StorSimple-bestand voor back-upcatalogus](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. Opnieuw opstarten Hallo StorSimple Management-Service van Microsoft: 
   
   1. Op Hallo Server Manager dashboard op Hallo **extra** selecteert u **Services**.
   2. Op Hallo **Services** venster, selecteer Hallo **Microsoft StorSimple Management Service**.
   3. In Hallo rechtermuisknop deelvenster onder **Microsoft StorSimple Management Service**, klikt u op **Hallo-service opnieuw starten**.
5. Blader op de hostcomputer Hallo tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
6. Hallo catalogus XML-bestand verwijderen en vervang deze door Hallo back-up die u hebt gemaakt. 
7. Klik op Hallo bureaublad StorSimple Snapshot Manager pictogram toostart StorSimple Snapshot Manager. 

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple Snapshot Manager tooadminister met uw StorSimple-oplossing](storsimple-snapshot-manager-admin.md).
* Meer informatie over [StorSimple Snapshot Manager-taken en werkstromen](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).

