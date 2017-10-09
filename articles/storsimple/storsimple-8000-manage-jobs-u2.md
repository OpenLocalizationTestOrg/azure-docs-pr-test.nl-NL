---
title: aaaView en beheren van taken voor StorSimple 8000 serie | Microsoft Docs
description: Beschrijving van de blade taken Hallo Apparaatbeheer StorSimple-service en hoe toouse het tootrack recente, huidige en geplande back-uptaken.
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
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>Hallo Apparaatbeheer StorSimple-service tooview gebruiken en beheren van taken (Update 3 en hoger)

## <a name="overview"></a>Overzicht
Hallo **taken** blade biedt één centrale portal voor het weergeven en beheren van taken die zijn gestart op apparaten tooyour StorSimple-apparaat Manager-service is verbonden. U kunt geplande, actieve, voltooide, geannuleerde en mislukte taken voor meerdere apparaten weergeven. Resultaten zijn in tabelvorm gepresenteerd.

![Blade taken](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

U bent geïnteresseerd door te filteren op velden zoals Hallo-taken kunt u snel vinden:

* **Status** – taken kunnen worden uitgevoerd, is voltooid, geannuleerd, is mislukt, annuleren of voltooid met fouten.
* **Tijdsbereik** – taken kunnen worden gefilterd op basis van Hallo datum en tijd bereik. Hallo-bereik is 1 uur, afgelopen 24 uur, afgelopen 7 dagen, afgelopen 30 dagen, afgelopen jaar of aangepaste datum uit het verleden.
* **Type** – Hallo taaktype mag geplande back-up, handmatige back-up, herstel back-up, volume klonen, failover volumecontainers, lokaal vastgemaakt volume maakt, volume wijzigen, updates installeren, verzamelen van Ondersteuningslogboeken en cloud toestel maken.
* **Apparaten** – taken zijn gestart op een bepaalde verbonden apparaat tooyour-service.
  
Hallo gefilterde taken worden vervolgens in een tabel weergegeven op basis van de Hallo Hallo volgende kenmerken:
  
* **Naam** – geplande back-up, handmatige back-up en terugzetten van back-up, kloon volume, failover volumecontainers, lokaal vastgemaakt volume maakt, volume wijzigen, updates installeren, verzamelen van Ondersteuningslogboeken of cloud toestel maken.
* **Status** – uitgevoerd, voltooide, geannuleerde, is mislukt, geannuleerd of voltooid met fouten.
* **Entiteit** – Hallo taken kunnen worden gekoppeld aan een volume, een back-upbeleid of een apparaat. De taak van een kloon is bijvoorbeeld gekoppeld aan een volume dat een geplande back-uptaak gekoppeld aan een back-upbeleid is. Een apparaat-taak is gemaakt als gevolg van een noodherstel (DR) of een herstelbewerking.
* **Apparaat** – hello naam van het Hallo-apparaat op welke Hallo taak is gestart.
* **Gestart op** – Hallo tijd waarop het Hallo-taak is gestart.
* **Duur** – Hallo tijd vereist toocomplete Hallo taak.

Hallo-lijst met taken wordt elke 30 seconden vernieuwd.

U kunt Hallo op deze pagina van de volgende taak-gerelateerde activiteiten uitvoeren:

* Details van de taak weergeven
* Een taak annuleren

## <a name="view-job-details"></a>Details van de taak weergeven
Hallo volgende stappen tooview Hallo details van elke taak uitvoeren.

#### <a name="tooview-job-details"></a>taakdetails tooview
1. Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **taken**.

2. In Hallo **taken** blade, weergave Hallo taak of taken die u bent geïnteresseerd door het uitvoeren van een query met de juiste filters. U kunt zoeken voor voltooid, uitvoeren of taken geannuleerd.

    ![Blade taak](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. Selecteer en klik op een taak.

    ![Blade taak](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. U kunt Hallo job details blade Hallo status, details, tijdstatistieken en statistieken van de gegevens weergeven.
   
    ![Taakdetails](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>Een taak annuleren
Hallo te volgen stappen toocancel een actieve taak uitvoeren.

> [!NOTE]
> Sommige taken, zoals een volumetype toochange Hallo volume te wijzigen of het uitbreiden van een volume kunnen niet worden geannuleerd.


### <a name="toocancel-a-job"></a>een taak toocancel
1. Op Hallo **taken** pagina, Hallo actieve taken die u door het uitvoeren van een query met de juiste filters toocancel wilt weergeven. Hallo taak selecteren.

2. Met de rechtermuisknop op Hallo geselecteerde taak tooinvoke Hallo-contextmenu en klik op **annuleren**.

    ![Taakdetails](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. Klik op **Ja** als u om bevestiging wordt gevraagd. Deze taak is nu geannuleerd.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[beheren van uw StorSimple-back-upbeleid](storsimple-8000-manage-backup-policies-u2.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

