---
title: aaaChange StorSimple-apparaatmodus | Microsoft Docs
description: Beschrijving van de modi van Hallo StorSimple-apparaat en wordt uitgelegd hoe toouse Windows PowerShell voor StorSimple toochange Hallo apparaatmodus.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>Modus voor Hallo apparaat wijzigen op uw StorSimple-apparaat

Dit artikel bevat een korte beschrijving van Hallo verschillende modi waarin uw StorSimple-apparaat kan worden uitgevoerd. Uw StorSimple-apparaat kan worden gebruikt in de drie beschikbare modi: standaard, onderhoud en herstel.

Na het lezen van dit artikel wordt u het volgende weten:

* Welke modi Hallo StorSimple-apparaat
* Hoe toofigure uit in welke modus Hallo StorSimple-apparaat bevindt zich in
* Hoe toochange van toomaintenance normale modus en *omgekeerd*

Hallo hierboven beheertaken kan alleen worden uitgevoerd via Windows PowerShell-interface Hallo van uw StorSimple-apparaat.

## <a name="about-storsimple-device-modes"></a>Over de modi van StorSimple-apparaat

Uw StorSimple-apparaat kan werken in de modus Normaal, onderhoud of herstellen. Elk van deze modi wordt kort hieronder beschreven.

### <a name="normal-mode"></a>Normale modus

Dit is gedefinieerd als Hallo normale operationele modus voor volledig geconfigureerde StorSimple-apparaat. Standaard moet uw apparaat in de normale modus.

### <a name="maintenance-mode"></a>Onderhoudsmodus

Soms hello StorSimple-apparaat moet mogelijk toobe in onderhoudsmodus geplaatst. Deze modus kunt u tooperform onderhoud op Hallo-apparaat en verstoren updates installeert, zoals gerelateerde toodisk firmware.

U kunt Hallo system plaatsen in de onderhoudsmodus alleen via Hallo Windows PowerShell voor StorSimple. Alle i/o-aanvragen zijn in deze modus onderbroken. Services zoals niet-vluchtige RAM-geheugen (NVRAM) of de clusteringservice Hallo zijn ook gestopt. Beide domeincontrollers Hallo worden opnieuw opgestart wanneer u in of uit deze modus. Wanneer u de onderhoudsmodus Hallo afsluit, worden alle Hallo-services wordt hervat en moeten in orde. Dit kan enkele minuten duren.

> [!NOTE]
> **Onderhoudsmodus wordt alleen ondersteund op een apparaat naar behoren werkt. Dit wordt niet ondersteund op een apparaat waarop een of beide Hallo domeincontrollers niet functioneren.**


### <a name="recovery-mode"></a>Modus voor herstel

Herstelmodus kan als 'Veilige modus voor Windows met netwerkondersteuning' worden beschreven. Herstelmodus stelt Hallo Microsoft Support team en kan ze tooperform diagnostics op Hallo-systeem. Hallo voornaamste doel van de herstelmodus is tooretrieve Hallo het systeemlogboek in Logboeken.

Als uw systeem in de herstelmodus overgaat wordt, neemt u contact op met Microsoft Support voor volgende stappen. Voor meer informatie gaat te[contact opnemen met Microsoft ondersteuning](storsimple-8000-contact-microsoft-support.md).

> [!NOTE]
> **In de herstelmodus kunt u geen Hallo apparaat plaatsen. Als Hallo-apparaat in orde is, probeert herstelmodus tooget Hallo apparaat in een status waarin medewerkers van Microsoft Support, deze kunnen bekijken.**

## <a name="determine-storsimple-device-mode"></a>Modus van StorSimple-apparaat bepalen

#### <a name="toodetermine-hello-current-device-mode"></a>toodetermine hello huidige apparaatmodus

1. Meld u bij de seriële console van toohello apparaat Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Bekijkt hello bannerbericht aangegeven in de seriële consolemenu Hallo Hallo-apparaat. Dit bericht expliciet wordt aangegeven of Hallo-apparaat in de modus voor onderhoud of herstel. Als het Hallo-bericht geen specifieke gegevens die betrekking hebben toohello system modus bevat, is het Hallo-apparaat in de normale modus.

## <a name="change-hello-storsimple-device-mode"></a>Modus wijzigen Hallo StorSimple-apparaat

U kunt plaatsen Hallo StorSimple-apparaat in onderhoud-modus (van de normale modus) tooperform onderhoud of onderhoud modus updates installeren. Voer Hallo onderhoudsmodus tooenter of exit procedures te volgen.

> [!IMPORTANT]
> Controleer of beide apparaatcontrollers zijn in orde door het openen van Hallo voordat het in de onderhoudsmodus, **apparaatinstellingen > Hardware health** voor uw apparaat in hello Azure-portal. Als een of beide Hallo domeincontrollers niet in orde zijn, moet u contact op met Microsoft Support voor de volgende stappen Hallo. Voor meer informatie gaat te[contact opnemen met Microsoft ondersteuning](storsimple-8000-contact-microsoft-support.md).
 

#### <a name="tooenter-maintenance-mode"></a>tooenter onderhoudsmodus

1. Meld u bij de seriële console van toohello apparaat Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**. Geef desgevraagd Hallo **wachtwoord apparaatbeheerder**. is het standaardwachtwoord Hallo: `Password1`.
3. Typ het volgende achter de opdrachtprompt Hallo 
   
    `Enter-HcsMaintenanceMode`
4. U ziet een waarschuwingsbericht weergegeven waarin staat dat onderhoudsmodus worden alle i/o-aanvragen verstoren Hallo verbinding toohello Azure-portal-server en wordt u gevraagd om bevestiging. Type **Y** tooenter-onderhoudsmodus.
5. Beide domeincontrollers wordt opnieuw opgestart. Wanneer Hallo opnieuw opstarten voltooid is, wordt Hallo seriële console banner aangeven dat Hallo-apparaat in de onderhoudsmodus. Hieronder ziet u een voorbeeld van de uitvoer.

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a>tooexit onderhoudsmodus

1. Meld u aan de seriële console van toohello apparaat. Controleer van Hallo bannerbericht aangegeven dat uw apparaat in de onderhoudsmodus.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
    `Exit-HcsMaintenanceMode`
3. Een waarschuwing en een bevestigingsbericht wordt weergegeven. Type **Y** tooexit-onderhoudsmodus.
4. Beide domeincontrollers wordt opnieuw opgestart. Wanneer Hallo opnieuw opstarten voltooid is, Hallo seriële console banner geeft aan dat het Hallo-apparaat in de normale modus. Hieronder ziet u een voorbeeld van de uitvoer.

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[normaal en onderhoud modus updates toepassen](storsimple-update-device.md) op uw StorSimple-apparaat.

