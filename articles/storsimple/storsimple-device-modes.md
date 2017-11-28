---
title: aaaChange hello StorSimple-apparaatmodus | Microsoft Docs
description: Beschrijving van de modi van Hallo StorSimple-apparaat en wordt uitgelegd hoe toouse Windows PowerShell voor StorSimple toochange Hallo apparaatmodus.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="ef54e-103">Modus voor Hallo apparaat wijzigen op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="ef54e-103">Change hello device mode on your StorSimple device</span></span>
<span data-ttu-id="ef54e-104">Dit artikel bevat een korte beschrijving van Hallo verschillende modi waarin uw StorSimple-apparaat kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ef54e-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="ef54e-105">Uw StorSimple-apparaat kan worden gebruikt in de drie beschikbare modi: standaard, onderhoud en herstel.</span><span class="sxs-lookup"><span data-stu-id="ef54e-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="ef54e-106">Na het lezen van dit artikel wordt u het volgende weten:</span><span class="sxs-lookup"><span data-stu-id="ef54e-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="ef54e-107">Welke modi Hallo StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="ef54e-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="ef54e-108">Hoe toofigure uit in welke modus Hallo StorSimple-apparaat bevindt zich in</span><span class="sxs-lookup"><span data-stu-id="ef54e-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="ef54e-109">Hoe toochange van toomaintenance normale modus en *omgekeerd*</span><span class="sxs-lookup"><span data-stu-id="ef54e-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="ef54e-110">Hallo hierboven beheertaken kan alleen worden uitgevoerd via Windows PowerShell-interface Hallo van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ef54e-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="ef54e-111">Over de modi van StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="ef54e-111">About StorSimple device modes</span></span>
<span data-ttu-id="ef54e-112">Uw StorSimple-apparaat kan werken in de modus Normaal, onderhoud of herstellen.</span><span class="sxs-lookup"><span data-stu-id="ef54e-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="ef54e-113">Elk van deze modi wordt kort hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="ef54e-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="ef54e-114">Normale modus</span><span class="sxs-lookup"><span data-stu-id="ef54e-114">Normal mode</span></span>
<span data-ttu-id="ef54e-115">Dit is gedefinieerd als Hallo normale operationele modus voor volledig geconfigureerde StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ef54e-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="ef54e-116">Standaard moet uw apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="ef54e-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="ef54e-117">Onderhoudsmodus</span><span class="sxs-lookup"><span data-stu-id="ef54e-117">Maintenance mode</span></span>
<span data-ttu-id="ef54e-118">Soms hello StorSimple-apparaat moet mogelijk toobe in onderhoudsmodus geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ef54e-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="ef54e-119">Deze modus kunt u tooperform onderhoud op Hallo-apparaat en verstoren updates installeert, zoals gerelateerde toodisk firmware.</span><span class="sxs-lookup"><span data-stu-id="ef54e-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="ef54e-120">U kunt Hallo system plaatsen in de onderhoudsmodus alleen via Hallo Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ef54e-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="ef54e-121">Alle i/o-aanvragen zijn in deze modus onderbroken.</span><span class="sxs-lookup"><span data-stu-id="ef54e-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="ef54e-122">Services zoals niet-vluchtige RAM-geheugen (NVRAM) of de clusteringservice Hallo zijn ook gestopt.</span><span class="sxs-lookup"><span data-stu-id="ef54e-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="ef54e-123">Beide domeincontrollers Hallo worden opnieuw opgestart wanneer u in of uit deze modus.</span><span class="sxs-lookup"><span data-stu-id="ef54e-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="ef54e-124">Wanneer u de onderhoudsmodus Hallo afsluit, worden alle Hallo-services wordt hervat en moeten in orde.</span><span class="sxs-lookup"><span data-stu-id="ef54e-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="ef54e-125">Dit kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="ef54e-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="ef54e-126">**Onderhoudsmodus wordt alleen ondersteund op een apparaat naar behoren werkt. Dit wordt niet ondersteund op een apparaat waarop een of beide Hallo domeincontrollers niet functioneren.**
> </span><span class="sxs-lookup"><span data-stu-id="ef54e-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="ef54e-127">Modus voor herstel</span><span class="sxs-lookup"><span data-stu-id="ef54e-127">Recovery mode</span></span>
<span data-ttu-id="ef54e-128">Herstelmodus kan als 'Veilige modus voor Windows met netwerkondersteuning' worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="ef54e-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="ef54e-129">Herstelmodus stelt Hallo Microsoft Support team en kan ze tooperform diagnostics op Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="ef54e-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="ef54e-130">Hallo voornaamste doel van de herstelmodus is tooretrieve Hallo het systeemlogboek in Logboeken.</span><span class="sxs-lookup"><span data-stu-id="ef54e-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="ef54e-131">Als uw systeem in de herstelmodus overgaat wordt, neemt u contact op met Microsoft Support voor volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="ef54e-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="ef54e-132">Voor meer informatie gaat te[contact opnemen met Microsoft ondersteuning](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="ef54e-132">For more information, go too[Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ef54e-133">**In de herstelmodus kunt u geen Hallo apparaat plaatsen. Als Hallo-apparaat in orde is, probeert herstelmodus tooget Hallo apparaat in een status waarin medewerkers van Microsoft Support, deze kunnen bekijken.**</span><span class="sxs-lookup"><span data-stu-id="ef54e-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="ef54e-134">Modus van StorSimple-apparaat bepalen</span><span class="sxs-lookup"><span data-stu-id="ef54e-134">Determine StorSimple device mode</span></span>
#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="ef54e-135">toodetermine hello huidige apparaatmodus</span><span class="sxs-lookup"><span data-stu-id="ef54e-135">toodetermine hello current device mode</span></span>
1. <span data-ttu-id="ef54e-136">Meld u bij de seriële console van toohello apparaat Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ef54e-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="ef54e-137">Bekijkt hello bannerbericht aangegeven in de seriële consolemenu Hallo Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ef54e-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="ef54e-138">Dit bericht expliciet wordt aangegeven of Hallo-apparaat in de modus voor onderhoud of herstel.</span><span class="sxs-lookup"><span data-stu-id="ef54e-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="ef54e-139">Als het Hallo-bericht geen specifieke gegevens die betrekking hebben toohello system modus bevat, is het Hallo-apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="ef54e-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="ef54e-140">Modus wijzigen Hallo StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="ef54e-140">Change hello StorSimple device mode</span></span>
<span data-ttu-id="ef54e-141">U kunt plaatsen Hallo StorSimple-apparaat in onderhoud-modus (van de normale modus) tooperform onderhoud of onderhoud modus updates installeren.</span><span class="sxs-lookup"><span data-stu-id="ef54e-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="ef54e-142">Voer Hallo onderhoudsmodus tooenter of exit procedures te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef54e-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef54e-143">Controleer of beide apparaatcontrollers zijn in orde door het openen van Hallo voordat het in de onderhoudsmodus, **hardwarestatus** op Hallo **onderhoud** pagina in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ef54e-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="ef54e-144">Als een of beide Hallo domeincontrollers niet in orde zijn, moet u contact op met Microsoft Support voor de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef54e-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="ef54e-145">Voor meer informatie gaat te[contact opnemen met Microsoft ondersteuning](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="ef54e-145">For more information, go too[Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="ef54e-146">tooenter onderhoudsmodus</span><span class="sxs-lookup"><span data-stu-id="ef54e-146">tooenter maintenance mode</span></span>
1. <span data-ttu-id="ef54e-147">Meld u bij de seriële console van toohello apparaat Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ef54e-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="ef54e-148">In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="ef54e-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="ef54e-149">Geef desgevraagd Hallo **wachtwoord apparaatbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="ef54e-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="ef54e-150">is het standaardwachtwoord Hallo: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="ef54e-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="ef54e-151">Typ het volgende achter de opdrachtprompt Hallo</span><span class="sxs-lookup"><span data-stu-id="ef54e-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="ef54e-152">U ziet een waarschuwingsbericht weergegeven waarin staat dat onderhoudsmodus worden alle i/o-aanvragen verstoren Hallo verbinding toohello klassieke Azure-portal-server en wordt u gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="ef54e-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="ef54e-153">Type **Y** tooenter-onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="ef54e-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="ef54e-154">Beide domeincontrollers wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="ef54e-154">Both controllers will restart.</span></span> <span data-ttu-id="ef54e-155">Wanneer Hallo opnieuw opstarten voltooid is, verschijnt er een ander bericht die aangeeft dat het Hallo-apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="ef54e-155">When hello restart is complete, another message will appear indicating that hello device is in maintenance mode.</span></span>

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="ef54e-156">tooexit onderhoudsmodus</span><span class="sxs-lookup"><span data-stu-id="ef54e-156">tooexit maintenance mode</span></span>
1. <span data-ttu-id="ef54e-157">Meld u aan de seriële console van toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="ef54e-157">Log on toohello device serial console.</span></span> <span data-ttu-id="ef54e-158">Controleer van Hallo bannerbericht aangegeven dat uw apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="ef54e-158">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="ef54e-159">Typ het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="ef54e-159">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="ef54e-160">Een waarschuwing en een bevestigingsbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ef54e-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="ef54e-161">Type **Y** tooexit-onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="ef54e-161">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="ef54e-162">Beide domeincontrollers wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="ef54e-162">Both controllers will restart.</span></span> <span data-ttu-id="ef54e-163">Wanneer Hallo opnieuw opstarten voltooid is, verschijnt er een ander bericht die aangeeft dat het Hallo-apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="ef54e-163">When hello restart is complete, another message will appear indicating that hello device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef54e-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef54e-164">Next steps</span></span>
<span data-ttu-id="ef54e-165">Meer informatie over hoe te[normaal en onderhoud modus updates toepassen](storsimple-update-device.md) op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ef54e-165">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

