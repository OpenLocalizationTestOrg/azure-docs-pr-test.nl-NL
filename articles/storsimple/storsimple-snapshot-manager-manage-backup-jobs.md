---
title: aaaStorSimple Snapshot Manager back-uptaken | Microsoft Docs
description: Hierin wordt beschreven hoe toouse StorSimple Snapshot Manager MMC-module tooview Hallo en beheren van back-uptaken voor geplande, voltooide en die momenteel worden uitgevoerd.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>StorSimple Snapshot Manager tooview gebruiken en beheren van back-uptaken

## <a name="overview"></a>Overzicht
Hallo **taken** knooppunt in Hallo **bereik** deelvenster bevat Hallo **geplande**, **afgelopen 24 uur**, en **met**back-up van taken die u hebt gestart, interactief of door een geconfigureerde beleid. 

Deze zelfstudie wordt uitgelegd hoe u kunt Hallo **taken** knooppunt toodisplay informatie over back-uptaken voor geplande, recente en die momenteel worden uitgevoerd. (Hallo lijst met taken en de bijbehorende informatie wordt weergegeven in Hallo **resultaten** deelvenster.) Bovendien kunt u met de rechtermuisknop op een vermelde taak en contextmenu met een lijst met beschikbare acties weergegeven.

## <a name="view-scheduled-jobs"></a>Geplande taken weergeven
Gebruik hello te volgen procedure tooview geplande back-uptaken.

#### <a name="tooview-scheduled-jobs"></a>tooview geplande taken
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager. 
2. In Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik op **geplande**. Hallo volgende informatie wordt weergegeven in Hallo **resultaten** deelvenster:
   
   * **Naam** – hello naam van het Hallo geplande momentopname
   * **Voer vervolgens** : Hallo datum en tijd van de volgende geplande momentopname Hallo
   * **Laatste uitvoering** : Hallo datum en tijd van de meest recente geplande momentopname Hallo
     
     > [!NOTE]
     > Hallo voor eenmalige alleen momentopnamen, **volgende uitvoeren** en **laatste start** Hallo identiek zijn.
     
     ![Geplande back-uptaken](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. tooperform aanvullende acties op een bepaalde taak met de rechtermuisknop op de taaknaam Hallo in Hallo **resultaten** deelvenster en selecteer een van de menuopties Hallo.

## <a name="view-recent-jobs"></a>Recente taken weergeven
Gebruik hello te volgen procedure tooview back-up- en hersteltaken die zijn voltooid in Hallo afgelopen 24 uur.

#### <a name="tooview-recent-jobs"></a>tooview recente taken
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik op **afgelopen 24 uur**. Hallo **resultaten** deelvenster ziet u back-uptaken voor Hallo afgelopen 24 uur (tooa maximaal 64 taken). Hallo volgende informatie wordt weergegeven in Hallo **resultaten** deelvenster, afhankelijk van Hallo **weergave** opties die u opgeeft:
   
   * **Naam** – hello naam van het Hallo geplande momentopname.
   * **Gestart** : Hallo datum en tijd wanneer Hallo momentopname is begonnen.
   * **Gestopt** : Hallo datum en tijd wanneer Hallo momentopname is voltooid of is beëindigd.
   * **Verstreken** – Hallo hoeveelheid tijd tussen Hallo **gestart** en **gestopt** tijden.
   * **Status** – Hallo status van taak Hallo onlangs voltooid. **Geslaagde** geeft aan dat Hallo back-up is gemaakt. **Kan geen** geeft aan dat Hallo-taak niet kan worden uitgevoerd.
   * **Informatie** – Hallo reden voor Hallo mislukken.
   * **Bytes verwerkt (MB)** – hello en de hoeveelheid gegevens uit Hallo volume groep die is verwerkt (in MB). 
     
     ![Taken die zijn uitgevoerd in Hallo afgelopen 24 uur](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. tooperform aanvullende acties op een bepaalde taak met de rechtermuisknop op de taaknaam Hallo in Hallo **resultaten** deelvenster en selecteer een van de menuopties Hallo.
   
    ![Een taak verwijderen](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>Actieve taken weergeven
Gebruik hello te volgen procedure tooview taken die momenteel worden uitgevoerd.

#### <a name="tooview-currently-running-jobs"></a>tooview momenteel actieve taken
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik op **met**. Afhankelijk van Hallo **weergave** opties die u opgeeft, Hallo volgende informatie wordt weergegeven in Hallo **resultaten** deelvenster:
   
   * **Naam** – hello naam van het Hallo geplande momentopname.
   * **Gestart** : Hallo datum en tijd wanneer Hallo momentopname is begonnen.
   * **Controlepunt** – Hallo van de huidige actie Hallo back-up.
   * **Status** – Hallo percentage voltooid.
   * **Verstreken** – Hallo hoeveelheid tijd is verstreken sinds het begin van Hallo back-up. 
   * **Gemiddelde doorvoer (MB)** – verhouding van totaal aantal bytes van toothat verwerkte gegevens van de totale tijd voor het verwerken van (MB).
   * **Bytes verwerkt (MB)** : totaal aantal bytes van gegevens die zijn verwerkt (in MB).
   * **Bytes geschreven (MB)** : totaal aantal bytes van gegevens die zijn geschreven (in MB). Het bevat Hallo gegevens, evenals Hallo metagegevens en is daarom meestal groter is dan Hallo Bytes verwerkt.
     
     ![Taken worden uitgevoerd](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. tooperform aanvullende acties op een bepaalde taak met de rechtermuisknop op de taaknaam Hallo in Hallo **resultaten** deelvenster en selecteer een van de menuopties Hallo.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).
* Meer informatie over hoe te[StorSimple Snapshot Manager toomanage Hallo back-upcatalogus gebruiken](storsimple-snapshot-manager-manage-backup-catalog.md).

