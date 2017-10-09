---
title: aaaView en beheren van taken StorSimple | Microsoft Docs
description: Hallo StorSimple Manager-servicepagina taken worden beschreven en hoe toouse het tootrack recente, huidige en geplande back-uptaken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a>Hallo StorSimple Manager-service tooview gebruiken en beheren van StorSimple-taken (Update 2)
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Overzicht
Hallo **taken** pagina biedt één centrale portal voor weergeven en beheren van taken die zijn gestart op apparaten tooyour StorSimple Manager-service is verbonden. U kunt geplande, actieve, voltooide, geannuleerde en mislukte taken voor meerdere apparaten weergeven. Resultaten zijn in tabelvorm gepresenteerd. 

![Pagina taken](./media/storsimple-manage-jobs-u2/jobs.png)

U bent geïnteresseerd door te filteren op velden zoals Hallo-taken kunt u snel vinden:

* **Status** – taken kunnen worden uitgevoerd, voltooide, geannuleerde, is mislukt, geannuleerd of voltooid met fouten.
* **Van en naar** – taken kunnen worden gefilterd op basis van Hallo datum en tijd bereik.
* **Type** – Hallo taaktype kan worden back-up, handmatige back-up, herstel, kloon, apparaat-failover, lokaal vastgemaakt volume maakt, volume wijzigen, bijwerken en ondersteuning voor pakket- of virtuele apparaten inrichten.
* **Apparaten** – taken zijn gestart op een bepaalde verbonden apparaat tooyour-service.
  Hallo gefilterde taken worden vervolgens in een tabel weergegeven op basis van de Hallo Hallo volgende kenmerken:
  
  * **Type** : back-up, handmatige back-up, herstel, kloon, apparaat-failover, lokaal vastgemaakt volume maakt, volume wijzigen, bijwerken en ondersteuning voor pakket- of virtuele apparaten inrichten.
  * **Status** – uitgevoerd, voltooide, geannuleerde, is mislukt, geannuleerd of voltooid met fouten.
  * **Entiteit** – Hallo taken kunnen worden gekoppeld aan een volume, een back-upbeleid of een apparaat. De taak van een kloon is bijvoorbeeld gekoppeld aan een volume dat een geplande back-uptaak gekoppeld aan een back-upbeleid is. Een apparaat-taak is gemaakt als gevolg van een noodherstel (DR) of een herstelbewerking.
  * **Apparaat** – hello naam van het Hallo-apparaat op welke Hallo taak is gestart.
  * **Gestart op** – Hallo tijd waarop het Hallo-taak is gestart.
  * **Voortgang** – Hallo percentage een actieve taak is voltooid. Dit moet altijd 100% zijn voor een voltooide taak.

Hallo-lijst met taken wordt elke 30 seconden vernieuwd.

U kunt Hallo op deze pagina van de volgende taak-gerelateerde activiteiten uitvoeren:

* Details van de taak weergeven
* Een taak annuleren

## <a name="view-job-details"></a>Details van de taak weergeven
Hallo volgende stappen tooview Hallo details van elke taak uitvoeren.

#### <a name="tooview-job-details"></a>taakdetails tooview
1. Op Hallo **taken** pagina, Hallo taak of taken die u bent geïnteresseerd door het uitvoeren van een query met de juiste filters weergegeven. U kunt zoeken voor voltooid, uitvoeren of taken geannuleerd.
2. Selecteer een taak.
3. Klik onder aan de pagina Hallo Hallo op **Details**.
4. In Hallo **back-up taakdetails** in het dialoogvenster u Hallo status, details, tijdstatistieken en statistieken van de gegevens kunt weergeven.
   
    ![De pagina details taak](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a>Een taak annuleren
Hallo te volgen stappen toocancel een actieve taak uitvoeren.

> [!NOTE]
> Sommige taken, zoals een volumetype toochange Hallo volume te wijzigen of het uitbreiden van een volume kunnen niet worden geannuleerd.
> 
> 

### <a name="toocancel-a-job"></a>een taak toocancel
1. Op Hallo **taken** pagina, Hallo actieve taken die u door het uitvoeren van een query met de juiste filters toocancel wilt weergeven.
2. Hallo taak selecteren.
3. Klik onder aan de pagina Hallo Hallo op **annuleren**.
4. Klik op **Ja** als u om bevestiging wordt gevraagd.

Deze taak is nu geannuleerd.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[beheren van uw StorSimple-back-upbeleid](storsimple-manage-backup-policies.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

