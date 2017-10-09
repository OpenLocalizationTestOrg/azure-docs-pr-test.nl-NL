---
title: aaaView en beheren van virtuele StorSimple-matrix taken | Microsoft Docs
description: Hallo StorSimple Apparaatbeheer servicepagina taken worden beschreven en hoe toouse het tootrack recente en de huidige taken voor Hallo virtuele StorSimple-matrix.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a>Hallo Apparaatbeheer StorSimple-service tooview taken gebruiken voor Hallo virtuele StorSimple-matrix
## <a name="overview"></a>Overzicht
Hallo **taken** blade biedt één centrale portal voor het weergeven en beheren van taken die zijn gestart op de virtuele matrices die verbonden tooyour StorSimple-apparaat Manager-service zijn. U kunt actieve voltooide en mislukte taken voor meerdere virtuele apparaten weergeven. Resultaten zijn in tabelvorm gepresenteerd.

![Blade taken](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

U bent geïnteresseerd door te filteren op velden zoals Hallo-taken kunt u snel vinden:

* **Tijdsbereik** – taken kunnen worden gefilterd op basis van Hallo datum en tijd bereik.
* **Apparaten** – taken zijn gestart op een specifiek apparaat verbonden tooyour-service. Hallo gefilterde taken worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:
  
  * **Naam** – Hallo taaknaam mag **alle**, **back-up**, **kloon**, **failover**, **updates downloaden** , of **updates installeren**.
  * **Status** – taken kunnen worden **alle**, **Bezig**, **geslaagd**, of **mislukt**, of **geannuleerd**.
  * **Entiteit** – Hallo taken kunnen worden gekoppeld aan een volume, share of apparaat.
  * **Apparaat** – hello naam van het Hallo-apparaat op welke Hallo taak is gestart.
  * **Gestart op** – Hallo tijd waarop het Hallo-taak is gestart.
  * **Duur** – hello duur voor op welke Hallo-taak werd uitgevoerd.
* **Status** – u kunt zoeken naar alle, uitgevoerd, is voltooid of mislukte taken.
* **Taaktype** – Hallo taaktype worden all, back-up, herstel, failover, downloaden van updates of updates installeren.

Hallo-lijst met taken wordt elke 30 seconden vernieuwd.

## <a name="view-job-details"></a>Details van de taak weergeven
Hallo volgende stappen tooview Hallo details van elke taak uitvoeren.

#### <a name="tooview-job-details"></a>taakdetails tooview
1. Op Hallo **taken** blade, weergave Hallo taak of taken die u bent geïnteresseerd door het uitvoeren van een query met de juiste filters. U kunt zoeken naar is voltooid of actieve taken.
2. Selecteer een taak uit Hallo in tabelvorm lijst met taken.
   
    ![Blade taak](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. Klik onder aan de pagina Hallo Hallo op **Details**.
4. In Hallo **Details** in het dialoogvenster vindt u de status, details en statistieken. Hallo volgende afbeelding toont een voorbeeld van Hallo **back-up taakdetails** in het dialoogvenster.
   
    ![Taakdetails](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a>Taakfouten wanneer Hallo virtuele machine in Hallo hypervisor is onderbroken
Wanneer een taak wordt uitgevoerd op uw virtuele StorSimple-matrix en het Hallo-apparaat (virtuele machine is ingericht in de hypervisor) voor meer dan 15 minuten is onderbroken, Hallo taak mislukt. Dit is vanwege tooyour virtuele StorSimple-matrix tijd wordt niet gesynchroniseerd met de Hallo Microsoft Azure-tijd. 

U ziet Hallo volgende fout: "de tijd op het apparaat is niet gesynchroniseerd met Microsoft Azure-tijd Hallo door meer dan 15 minuten. Zorg ervoor dat Hallo hypervisor en Hallo apparaat tijden zijn gesynchroniseerd met een clientverzoeken NTP. Controleer of er geen verbindingsproblemen zijn. problemen met de netwerkverbinding van tootroubleshoot diagnostische tests uitvoeren van Hallo lokale webgebruikersinterface van uw virtuele apparaat."

Deze fouten van toepassing toobackup, herstellen, bijwerken en failover-taken. Als uw virtuele machine is ingericht in Hyper-V, synchroniseert Hallo machine tijd uiteindelijk met de hypervisor. Wanneer dit gebeurt, kunt u de taak opnieuw te starten.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over hoe toouse Hallo lokale web UI tooadminister uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).

