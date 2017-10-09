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
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="f9c7a-103">Modus voor Hallo apparaat wijzigen op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="f9c7a-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="f9c7a-104">Dit artikel bevat een korte beschrijving van Hallo verschillende modi waarin uw StorSimple-apparaat kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="f9c7a-105">Uw StorSimple-apparaat kan worden gebruikt in de drie beschikbare modi: standaard, onderhoud en herstel.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="f9c7a-106">Na het lezen van dit artikel wordt u het volgende weten:</span><span class="sxs-lookup"><span data-stu-id="f9c7a-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="f9c7a-107">Welke modi Hallo StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="f9c7a-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="f9c7a-108">Hoe toofigure uit in welke modus Hallo StorSimple-apparaat bevindt zich in</span><span class="sxs-lookup"><span data-stu-id="f9c7a-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="f9c7a-109">Hoe toochange van toomaintenance normale modus en *omgekeerd*</span><span class="sxs-lookup"><span data-stu-id="f9c7a-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="f9c7a-110">Hallo hierboven beheertaken kan alleen worden uitgevoerd via Windows PowerShell-interface Hallo van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="f9c7a-111">Over de modi van StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="f9c7a-111">About StorSimple device modes</span></span>

<span data-ttu-id="f9c7a-112">Uw StorSimple-apparaat kan werken in de modus Normaal, onderhoud of herstellen.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="f9c7a-113">Elk van deze modi wordt kort hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="f9c7a-114">Normale modus</span><span class="sxs-lookup"><span data-stu-id="f9c7a-114">Normal mode</span></span>

<span data-ttu-id="f9c7a-115">Dit is gedefinieerd als Hallo normale operationele modus voor volledig geconfigureerde StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="f9c7a-116">Standaard moet uw apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="f9c7a-117">Onderhoudsmodus</span><span class="sxs-lookup"><span data-stu-id="f9c7a-117">Maintenance mode</span></span>

<span data-ttu-id="f9c7a-118">Soms hello StorSimple-apparaat moet mogelijk toobe in onderhoudsmodus geplaatst.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="f9c7a-119">Deze modus kunt u tooperform onderhoud op Hallo-apparaat en verstoren updates installeert, zoals gerelateerde toodisk firmware.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="f9c7a-120">U kunt Hallo system plaatsen in de onderhoudsmodus alleen via Hallo Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="f9c7a-121">Alle i/o-aanvragen zijn in deze modus onderbroken.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="f9c7a-122">Services zoals niet-vluchtige RAM-geheugen (NVRAM) of de clusteringservice Hallo zijn ook gestopt.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="f9c7a-123">Beide domeincontrollers Hallo worden opnieuw opgestart wanneer u in of uit deze modus.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="f9c7a-124">Wanneer u de onderhoudsmodus Hallo afsluit, worden alle Hallo-services wordt hervat en moeten in orde.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="f9c7a-125">Dit kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c7a-126">**Onderhoudsmodus wordt alleen ondersteund op een apparaat naar behoren werkt. Dit wordt niet ondersteund op een apparaat waarop een of beide Hallo domeincontrollers niet functioneren.**</span><span class="sxs-lookup"><span data-stu-id="f9c7a-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="f9c7a-127">Modus voor herstel</span><span class="sxs-lookup"><span data-stu-id="f9c7a-127">Recovery mode</span></span>

<span data-ttu-id="f9c7a-128">Herstelmodus kan als 'Veilige modus voor Windows met netwerkondersteuning' worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="f9c7a-129">Herstelmodus stelt Hallo Microsoft Support team en kan ze tooperform diagnostics op Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="f9c7a-130">Hallo voornaamste doel van de herstelmodus is tooretrieve Hallo het systeemlogboek in Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="f9c7a-131">Als uw systeem in de herstelmodus overgaat wordt, neemt u contact op met Microsoft Support voor volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="f9c7a-132">Voor meer informatie gaat te[contact opnemen met Microsoft ondersteuning](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="f9c7a-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f9c7a-133">**In de herstelmodus kunt u geen Hallo apparaat plaatsen. Als Hallo-apparaat in orde is, probeert herstelmodus tooget Hallo apparaat in een status waarin medewerkers van Microsoft Support, deze kunnen bekijken.**</span><span class="sxs-lookup"><span data-stu-id="f9c7a-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="f9c7a-134">Modus van StorSimple-apparaat bepalen</span><span class="sxs-lookup"><span data-stu-id="f9c7a-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="f9c7a-135">toodetermine hello huidige apparaatmodus</span><span class="sxs-lookup"><span data-stu-id="f9c7a-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="f9c7a-136">Meld u bij de seriële console van toohello apparaat Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f9c7a-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="f9c7a-137">Bekijkt hello bannerbericht aangegeven in de seriële consolemenu Hallo Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="f9c7a-138">Dit bericht expliciet wordt aangegeven of Hallo-apparaat in de modus voor onderhoud of herstel.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="f9c7a-139">Als het Hallo-bericht geen specifieke gegevens die betrekking hebben toohello system modus bevat, is het Hallo-apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="f9c7a-140">Modus wijzigen Hallo StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="f9c7a-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="f9c7a-141">U kunt plaatsen Hallo StorSimple-apparaat in onderhoud-modus (van de normale modus) tooperform onderhoud of onderhoud modus updates installeren.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="f9c7a-142">Voer Hallo onderhoudsmodus tooenter of exit procedures te volgen.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9c7a-143">Controleer of beide apparaatcontrollers zijn in orde door het openen van Hallo voordat het in de onderhoudsmodus, **apparaatinstellingen > Hardware health** voor uw apparaat in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="f9c7a-144">Als een of beide Hallo domeincontrollers niet in orde zijn, moet u contact op met Microsoft Support voor de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="f9c7a-145">Voor meer informatie gaat te[contact opnemen met Microsoft ondersteuning](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="f9c7a-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="f9c7a-146">tooenter onderhoudsmodus</span><span class="sxs-lookup"><span data-stu-id="f9c7a-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="f9c7a-147">Meld u bij de seriële console van toohello apparaat Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f9c7a-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="f9c7a-148">In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="f9c7a-149">Geef desgevraagd Hallo **wachtwoord apparaatbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="f9c7a-150">is het standaardwachtwoord Hallo: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="f9c7a-151">Typ het volgende achter de opdrachtprompt Hallo</span><span class="sxs-lookup"><span data-stu-id="f9c7a-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="f9c7a-152">U ziet een waarschuwingsbericht weergegeven waarin staat dat onderhoudsmodus worden alle i/o-aanvragen verstoren Hallo verbinding toohello Azure-portal-server en wordt u gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="f9c7a-153">Type **Y** tooenter-onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="f9c7a-154">Beide domeincontrollers wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-154">Both controllers will restart.</span></span> <span data-ttu-id="f9c7a-155">Wanneer Hallo opnieuw opstarten voltooid is, wordt Hallo seriële console banner aangeven dat Hallo-apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="f9c7a-156">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-156">A sample output is shown below.</span></span>

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

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="f9c7a-157">tooexit onderhoudsmodus</span><span class="sxs-lookup"><span data-stu-id="f9c7a-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="f9c7a-158">Meld u aan de seriële console van toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-158">Log on toohello device serial console.</span></span> <span data-ttu-id="f9c7a-159">Controleer van Hallo bannerbericht aangegeven dat uw apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="f9c7a-160">Typ het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="f9c7a-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="f9c7a-161">Een waarschuwing en een bevestigingsbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="f9c7a-162">Type **Y** tooexit-onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="f9c7a-163">Beide domeincontrollers wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-163">Both controllers will restart.</span></span> <span data-ttu-id="f9c7a-164">Wanneer Hallo opnieuw opstarten voltooid is, Hallo seriële console banner geeft aan dat het Hallo-apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="f9c7a-165">Hieronder ziet u een voorbeeld van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-165">A sample output is shown below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f9c7a-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f9c7a-166">Next steps</span></span>

<span data-ttu-id="f9c7a-167">Meer informatie over hoe te[normaal en onderhoud modus updates toepassen](storsimple-update-device.md) op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="f9c7a-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

