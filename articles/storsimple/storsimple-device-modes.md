---
title: De StorSimple-apparaat-modus wijzigen | Microsoft Docs
description: Beschrijft de modus voor de StorSimple-apparaat en wordt uitgelegd hoe u Windows PowerShell voor StorSimple om de apparatuurmodus te wijzigen.
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
ms.openlocfilehash: 33c65bf2eecff3914f3227c76f7d638a4507e1f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="51c86-103">Wijzig de apparatuurmodus op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="51c86-103">Change the device mode on your StorSimple device</span></span>
<span data-ttu-id="51c86-104">Dit artikel bevat een korte beschrijving van de verschillende modi waarin uw StorSimple-apparaat kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="51c86-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="51c86-105">Uw StorSimple-apparaat kan worden gebruikt in de drie beschikbare modi: standaard, onderhoud en herstel.</span><span class="sxs-lookup"><span data-stu-id="51c86-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="51c86-106">Na het lezen van dit artikel wordt u het volgende weten:</span><span class="sxs-lookup"><span data-stu-id="51c86-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="51c86-107">Welke de StorSimple-apparaat-modi</span><span class="sxs-lookup"><span data-stu-id="51c86-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="51c86-108">Hoe om te achterhalen welke modus de StorSimple-apparaat bevindt zich in</span><span class="sxs-lookup"><span data-stu-id="51c86-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="51c86-109">Het wijzigen van de normale naar de onderhoudsmodus en *omgekeerd*</span><span class="sxs-lookup"><span data-stu-id="51c86-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="51c86-110">De bovenstaande beheertaken kunnen alleen worden uitgevoerd via de Windows PowerShell-interface van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="51c86-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="51c86-111">Over de modi van StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="51c86-111">About StorSimple device modes</span></span>
<span data-ttu-id="51c86-112">Uw StorSimple-apparaat kan werken in de modus Normaal, onderhoud of herstellen.</span><span class="sxs-lookup"><span data-stu-id="51c86-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="51c86-113">Elk van deze modi wordt kort hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="51c86-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="51c86-114">Normale modus</span><span class="sxs-lookup"><span data-stu-id="51c86-114">Normal mode</span></span>
<span data-ttu-id="51c86-115">Dit is gedefinieerd als de normale operationele modus voor volledig geconfigureerde StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="51c86-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="51c86-116">Standaard moet uw apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="51c86-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="51c86-117">Onderhoudsmodus</span><span class="sxs-lookup"><span data-stu-id="51c86-117">Maintenance mode</span></span>
<span data-ttu-id="51c86-118">Soms moet het StorSimple-apparaat kan worden geplaatst in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="51c86-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="51c86-119">Deze modus kunt u onderhoud uitvoeren op het apparaat en verstoren updates, zoals die betrekking hebben op firmware van de schijf installeren.</span><span class="sxs-lookup"><span data-stu-id="51c86-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="51c86-120">U kunt het systeem plaatsen in de onderhoudsmodus alleen via de Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51c86-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="51c86-121">Alle i/o-aanvragen zijn in deze modus onderbroken.</span><span class="sxs-lookup"><span data-stu-id="51c86-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="51c86-122">Services zoals niet-vluchtige RAM-geheugen (NVRAM) of de clusteringservice ook worden gestopt.</span><span class="sxs-lookup"><span data-stu-id="51c86-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="51c86-123">Beide domeincontrollers worden opnieuw opgestart wanneer u in of uit deze modus.</span><span class="sxs-lookup"><span data-stu-id="51c86-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="51c86-124">Wanneer u de onderhoudsmodus afsluit, worden alle services wordt hervat en moeten in orde.</span><span class="sxs-lookup"><span data-stu-id="51c86-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="51c86-125">Dit kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="51c86-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="51c86-126">**Onderhoudsmodus wordt alleen ondersteund op een apparaat naar behoren werkt. Dit wordt niet ondersteund op een apparaat waarop een of beide van de domeincontrollers niet functioneren.**
> </span><span class="sxs-lookup"><span data-stu-id="51c86-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="51c86-127">Modus voor herstel</span><span class="sxs-lookup"><span data-stu-id="51c86-127">Recovery mode</span></span>
<span data-ttu-id="51c86-128">Herstelmodus kan als 'Veilige modus voor Windows met netwerkondersteuning' worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="51c86-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="51c86-129">Herstelmodus stelt het team van Microsoft Support en kan ze voor het uitvoeren van diagnostische gegevens op het systeem.</span><span class="sxs-lookup"><span data-stu-id="51c86-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="51c86-130">Het voornaamste doel van de herstelmodus is voor het ophalen van het systeemlogboek in Logboeken.</span><span class="sxs-lookup"><span data-stu-id="51c86-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="51c86-131">Als uw systeem in de herstelmodus overgaat wordt, neemt u contact op met Microsoft Support voor volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="51c86-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="51c86-132">Ga voor meer informatie naar [contact opnemen met Microsoft ondersteuning](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="51c86-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="51c86-133">**U kunt het apparaat in herstelmodus plaatsen. Als het apparaat in orde is, probeert op te halen van het apparaat in een status waarin medewerkers van Microsoft Support Bekijk deze herstelmodus.**</span><span class="sxs-lookup"><span data-stu-id="51c86-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="51c86-134">Modus van StorSimple-apparaat bepalen</span><span class="sxs-lookup"><span data-stu-id="51c86-134">Determine StorSimple device mode</span></span>
#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="51c86-135">Om te bepalen van de huidige apparatuurmodus</span><span class="sxs-lookup"><span data-stu-id="51c86-135">To determine the current device mode</span></span>
1. <span data-ttu-id="51c86-136">Meld u aan bij de seriële console van het apparaat door de stappen in [PuTTY gebruiken om verbinding maken met de seriële console van het apparaat](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="51c86-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="51c86-137">Bekijk het bannerbericht aangegeven in het menu van de seriële console van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="51c86-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="51c86-138">Dit bericht expliciet geeft aan of het apparaat in de modus voor onderhoud of herstel.</span><span class="sxs-lookup"><span data-stu-id="51c86-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="51c86-139">Als het bericht geen specifieke gegevens met betrekking tot de systeem-modus bevat, is het apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="51c86-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="51c86-140">De modus StorSimple-apparaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="51c86-140">Change the StorSimple device mode</span></span>
<span data-ttu-id="51c86-141">U kunt het StorSimple-apparaat plaatsen in de onderhoudsmodus (van de normale modus) voor het uitvoeren van onderhoud of onderhoud modus updates installeren.</span><span class="sxs-lookup"><span data-stu-id="51c86-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="51c86-142">Voer de volgende procedures om in of uit de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="51c86-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51c86-143">Voordat u de onderhoudsmodus invoert, of beide apparaatcontrollers in orde zijn met het openen van de **hardwarestatus** op de **onderhoud** pagina in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="51c86-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="51c86-144">Als een of beide domeincontrollers niet in orde, neem dan contact op met Microsoft Support voor de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="51c86-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="51c86-145">Ga voor meer informatie naar [contact opnemen met Microsoft ondersteuning](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="51c86-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="51c86-146">Onderhoudsmodus invoeren</span><span class="sxs-lookup"><span data-stu-id="51c86-146">To enter maintenance mode</span></span>
1. <span data-ttu-id="51c86-147">Meld u aan bij de seriële console van het apparaat door de stappen in [PuTTY gebruiken om verbinding maken met de seriële console van het apparaat](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="51c86-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="51c86-148">Kies in het menu van de seriële console optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="51c86-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="51c86-149">Geef desgevraagd de **wachtwoord apparaatbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="51c86-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="51c86-150">Is het standaardwachtwoord: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="51c86-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="51c86-151">Typ het volgende achter de opdrachtprompt</span><span class="sxs-lookup"><span data-stu-id="51c86-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="51c86-152">Hier ziet u een waarschuwingsbericht weergegeven waarin staat dat onderhoudsmodus wordt verstoord alle i/o-aanvragen en de verbinding met de klassieke Azure portal-server en wordt u gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="51c86-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="51c86-153">Type **Y** onderhoudsmodus invoeren.</span><span class="sxs-lookup"><span data-stu-id="51c86-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="51c86-154">Beide domeincontrollers wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="51c86-154">Both controllers will restart.</span></span> <span data-ttu-id="51c86-155">Wanneer het opnieuw opstarten voltooid is, verschijnt er een ander bericht waarmee wordt aangegeven dat het apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="51c86-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span></span>

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="51c86-156">Om af te sluiten van onderhoudsmodus</span><span class="sxs-lookup"><span data-stu-id="51c86-156">To exit maintenance mode</span></span>
1. <span data-ttu-id="51c86-157">Meld u bij de seriële console van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="51c86-157">Log on to the device serial console.</span></span> <span data-ttu-id="51c86-158">Controleer de van het bannerbericht aangegeven dat uw apparaat in de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="51c86-158">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="51c86-159">Typ het volgende achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="51c86-159">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="51c86-160">Een waarschuwing en een bevestigingsbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="51c86-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="51c86-161">Type **Y** om af te sluiten van de onderhoudsmodus.</span><span class="sxs-lookup"><span data-stu-id="51c86-161">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="51c86-162">Beide domeincontrollers wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="51c86-162">Both controllers will restart.</span></span> <span data-ttu-id="51c86-163">Wanneer het opnieuw opstarten voltooid is, verschijnt er een ander bericht waarmee wordt aangegeven dat het apparaat in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="51c86-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51c86-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51c86-164">Next steps</span></span>
<span data-ttu-id="51c86-165">Meer informatie over hoe [normaal en onderhoud modus updates toepassen](storsimple-update-device.md) op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="51c86-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

