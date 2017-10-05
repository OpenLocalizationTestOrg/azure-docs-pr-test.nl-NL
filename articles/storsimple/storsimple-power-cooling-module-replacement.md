---
title: Vervang een PCM op uw StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe verwijdert en vervangt u de stroom en koeling Module (PCM) op uw StorSimple-apparaat
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 2a956de58b279a013913631a077d7b03c6327f72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="ac083-103">Vervangen van een stroom en koeling Module op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="ac083-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="ac083-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ac083-104">Overview</span></span>
<span data-ttu-id="ac083-105">De stroom en koeling Module (PCM) in uw Microsoft Azure StorSimple-apparaat bestaat uit een voeding en koeling van ventilatoren die worden beheerd via de primaire en EBOD behuizingen.</span><span class="sxs-lookup"><span data-stu-id="ac083-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="ac083-106">Er is slechts één model van PCM die is gecertificeerd voor elke behuizing.</span><span class="sxs-lookup"><span data-stu-id="ac083-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="ac083-107">De primaire behuizing is gecertificeerd voor een 764 W PCM en de behuizing EBOD is gecertificeerd voor een 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="ac083-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="ac083-108">Hoewel de PCMs voor de primaire behuizing en de behuizing EBOD verschillend zijn, is de vervangingsprocedure is vrijwel identiek.</span><span class="sxs-lookup"><span data-stu-id="ac083-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="ac083-109">Deze zelfstudie wordt uitgelegd hoe:</span><span class="sxs-lookup"><span data-stu-id="ac083-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="ac083-110">Een PCM verwijderen</span><span class="sxs-lookup"><span data-stu-id="ac083-110">Remove a PCM</span></span>
* <span data-ttu-id="ac083-111">Een vervangende PCM installeren</span><span class="sxs-lookup"><span data-stu-id="ac083-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac083-112">Voordat verwijderen en een PCM vervangen Lees de veiligheidsinformatie in [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="ac083-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="ac083-113">Voordat u een PCM vervangen</span><span class="sxs-lookup"><span data-stu-id="ac083-113">Before you replace a PCM</span></span>
<span data-ttu-id="ac083-114">Let op de volgende belangrijke problemen voordat u uw PCM vervangt:</span><span class="sxs-lookup"><span data-stu-id="ac083-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="ac083-115">Als de voeding van de PCM mislukt, laat de defecte module geïnstalleerd, maar het netsnoer verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ac083-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="ac083-116">De ventilator blijven power ontvangen van de behuizing en doorgaan met het juiste koeling bieden.</span><span class="sxs-lookup"><span data-stu-id="ac083-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="ac083-117">Als de ventilator mislukt, wordt de PCM moet onmiddellijk worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="ac083-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="ac083-118">Voordat u de PCM verwijdert, Verbreek de verbinding met de kracht van de PCM door het uitschakelen van de belangrijkste switch (indien aanwezig) of door het netsnoer fysiek verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ac083-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="ac083-119">Dit biedt een waarschuwing op uw systeem afsluiten power dreigt.</span><span class="sxs-lookup"><span data-stu-id="ac083-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="ac083-120">Zorg ervoor dat de andere PCM functionele voor voortdurende systeembewerkingen voordat de defecte PCM worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="ac083-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="ac083-121">Een defecte PCM moet worden vervangen door een volledig operationeel PCM zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="ac083-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="ac083-122">Vervanging van PCM-module duurt slechts enkele minuten duren, maar deze moet worden voltooid binnen 10 minuten van het verwijderen van de mislukte PCM om te voorkomen dat oververhitting.</span><span class="sxs-lookup"><span data-stu-id="ac083-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="ac083-123">Houd er rekening mee vervanging 764 W PCM modules verzonden van de fabriek hebben niet de back-up batterij-module.</span><span class="sxs-lookup"><span data-stu-id="ac083-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="ac083-124">U moet de batterij verwijderen uit uw defecte PCM en plaatst u deze in de module vervanging voordat de vervangende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ac083-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="ac083-125">Zie voor meer informatie hoe [verwijderen en voeg een back-up batterij module](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="ac083-125">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="ac083-126">Een PCM verwijderen</span><span class="sxs-lookup"><span data-stu-id="ac083-126">Remove a PCM</span></span>
<span data-ttu-id="ac083-127">Volg deze instructies wanneer u klaar bent voor het verwijderen van een stroom en koeling Module (PCM) van uw Microsoft Azure StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ac083-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="ac083-128">Voordat u uw PCM verwijdert, moet u controleren of u een juiste vervangende (764 W voor de primaire behuizing) of 580 W voor de behuizing EBOD hebben.</span><span class="sxs-lookup"><span data-stu-id="ac083-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>
> 
> 

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="ac083-129">Een PCM verwijderen</span><span class="sxs-lookup"><span data-stu-id="ac083-129">To remove a PCM</span></span>
1. <span data-ttu-id="ac083-130">Klik in de klassieke Azure-portal op **apparaten** > **onderhoud** > **hardwarestatus**.</span><span class="sxs-lookup"><span data-stu-id="ac083-130">In the Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="ac083-131">Controleer de status van de PCM-componenten onder **gedeelde onderdelen** geven aan welke PCM is mislukt:</span><span class="sxs-lookup"><span data-stu-id="ac083-131">Check the status of the PCM components under **Shared Components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="ac083-132">Als een voeding in PCM 0 is mislukt, wordt de status van **Power Supply in PCM 0** rood.</span><span class="sxs-lookup"><span data-stu-id="ac083-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="ac083-133">Als een voeding in PCM-1 is mislukt, wordt de status van **Power Supply in PCM 1** rood.</span><span class="sxs-lookup"><span data-stu-id="ac083-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="ac083-134">Als de ventilator in PCM-1 is mislukt, wordt de status van een **koeling van 0 voor PCM 0** of **koeling 1 voor PCM 0** rood.</span><span class="sxs-lookup"><span data-stu-id="ac083-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="ac083-135">Zoek de mislukte PCM op de achterkant van de primaire behuizing.</span><span class="sxs-lookup"><span data-stu-id="ac083-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="ac083-136">Als u een model 8600 uitvoert, moet u de primaire behuizing vinden door het systeem eenheid id-nummer op het voorpaneel LED-scherm weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ac083-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="ac083-137">De standaardwaarde eenheid-ID weergegeven op de primaire behuizing is **00**, terwijl de standaardwaarde eenheid-ID weergegeven op de behuizing EBOD **01**.</span><span class="sxs-lookup"><span data-stu-id="ac083-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="ac083-138">Het volgende diagram en de volgende tabel wordt uitgelegd het voorpaneel van de weergave LED.</span><span class="sxs-lookup"><span data-stu-id="ac083-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![Systeem-ID op voorpaneel OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="ac083-140">**Afbeelding 1** voorzijde deelvenster van het apparaat</span><span class="sxs-lookup"><span data-stu-id="ac083-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="ac083-141">Label</span><span class="sxs-lookup"><span data-stu-id="ac083-141">Label</span></span> | <span data-ttu-id="ac083-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ac083-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="ac083-143">1</span><span class="sxs-lookup"><span data-stu-id="ac083-143">1</span></span> |<span data-ttu-id="ac083-144">Knop Dempen</span><span class="sxs-lookup"><span data-stu-id="ac083-144">Mute button</span></span> |
   | <span data-ttu-id="ac083-145">2</span><span class="sxs-lookup"><span data-stu-id="ac083-145">2</span></span> |<span data-ttu-id="ac083-146">Inschakelen van het systeem</span><span class="sxs-lookup"><span data-stu-id="ac083-146">System power</span></span> |
   | <span data-ttu-id="ac083-147">3</span><span class="sxs-lookup"><span data-stu-id="ac083-147">3</span></span> |<span data-ttu-id="ac083-148">Module-fout</span><span class="sxs-lookup"><span data-stu-id="ac083-148">Module fault</span></span> |
   | <span data-ttu-id="ac083-149">4</span><span class="sxs-lookup"><span data-stu-id="ac083-149">4</span></span> |<span data-ttu-id="ac083-150">Logische-fout</span><span class="sxs-lookup"><span data-stu-id="ac083-150">Logical fault</span></span> |
   | <span data-ttu-id="ac083-151">5</span><span class="sxs-lookup"><span data-stu-id="ac083-151">5</span></span> |<span data-ttu-id="ac083-152">Eenheid-ID weergeven</span><span class="sxs-lookup"><span data-stu-id="ac083-152">Unit ID display</span></span> |
3. <span data-ttu-id="ac083-153">De bewaking LED aan de achterzijde van de primaire behuizing kan ook worden gebruikt voor het identificeren van de defecte PCM.</span><span class="sxs-lookup"><span data-stu-id="ac083-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="ac083-154">Zie het volgende diagram en tabel om te begrijpen hoe de LED's gebruiken om te vinden van de defecte PCM.</span><span class="sxs-lookup"><span data-stu-id="ac083-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="ac083-155">Bijvoorbeeld, als de LED die overeenkomt met de **ventilator mislukken** is belicht, de ventilator is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ac083-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="ac083-156">Op dezelfde manier als de LED die overeenkomt met **AC mislukken** is belicht, de voeding is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ac083-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![Backplane van apparaat PCM bewaking LED](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="ac083-158">**Afbeelding 2** Back van PCM met LED</span><span class="sxs-lookup"><span data-stu-id="ac083-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="ac083-159">Label</span><span class="sxs-lookup"><span data-stu-id="ac083-159">Label</span></span> | <span data-ttu-id="ac083-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ac083-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="ac083-161">1</span><span class="sxs-lookup"><span data-stu-id="ac083-161">1</span></span> |<span data-ttu-id="ac083-162">Fout in Echtheidsvoorwaarde power</span><span class="sxs-lookup"><span data-stu-id="ac083-162">AC power failure</span></span> |
   | <span data-ttu-id="ac083-163">2</span><span class="sxs-lookup"><span data-stu-id="ac083-163">2</span></span> |<span data-ttu-id="ac083-164">Ventilator mislukt</span><span class="sxs-lookup"><span data-stu-id="ac083-164">Fan failure</span></span> |
   | <span data-ttu-id="ac083-165">3</span><span class="sxs-lookup"><span data-stu-id="ac083-165">3</span></span> |<span data-ttu-id="ac083-166">Fout met betrekking tot accu</span><span class="sxs-lookup"><span data-stu-id="ac083-166">Battery fault</span></span> |
   | <span data-ttu-id="ac083-167">4</span><span class="sxs-lookup"><span data-stu-id="ac083-167">4</span></span> |<span data-ttu-id="ac083-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="ac083-168">PCM OK</span></span> |
   | <span data-ttu-id="ac083-169">5</span><span class="sxs-lookup"><span data-stu-id="ac083-169">5</span></span> |<span data-ttu-id="ac083-170">DC-stroomstoring</span><span class="sxs-lookup"><span data-stu-id="ac083-170">DC power failure</span></span> |
   | <span data-ttu-id="ac083-171">6</span><span class="sxs-lookup"><span data-stu-id="ac083-171">6</span></span> |<span data-ttu-id="ac083-172">Accu in orde</span><span class="sxs-lookup"><span data-stu-id="ac083-172">Battery healthy</span></span> |
4. <span data-ttu-id="ac083-173">Raadpleeg het volgende diagram van de achterkant van het StorSimple-apparaat Zoek de mislukte PCM-module.</span><span class="sxs-lookup"><span data-stu-id="ac083-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="ac083-174">PCM 0 is aan de linkerkant en PCM-1 is aan de rechterkant.</span><span class="sxs-lookup"><span data-stu-id="ac083-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="ac083-175">De volgende tabel wordt uitgelegd dat de modules.</span><span class="sxs-lookup"><span data-stu-id="ac083-175">The table that follows explains the modules.</span></span>
   
     ![Backplane apparaat primaire behuizing modules](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="ac083-177">**Afbeelding 3** achterzijde van het apparaat met de invoegtoepassing modules</span><span class="sxs-lookup"><span data-stu-id="ac083-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="ac083-178">Label</span><span class="sxs-lookup"><span data-stu-id="ac083-178">Label</span></span> | <span data-ttu-id="ac083-179">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ac083-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="ac083-180">1</span><span class="sxs-lookup"><span data-stu-id="ac083-180">1</span></span> |<span data-ttu-id="ac083-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="ac083-181">PCM 0</span></span> |
   | <span data-ttu-id="ac083-182">2</span><span class="sxs-lookup"><span data-stu-id="ac083-182">2</span></span> |<span data-ttu-id="ac083-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="ac083-183">PCM 1</span></span> |
   | <span data-ttu-id="ac083-184">3</span><span class="sxs-lookup"><span data-stu-id="ac083-184">3</span></span> |<span data-ttu-id="ac083-185">Controller 0</span><span class="sxs-lookup"><span data-stu-id="ac083-185">Controller 0</span></span> |
   | <span data-ttu-id="ac083-186">4</span><span class="sxs-lookup"><span data-stu-id="ac083-186">4</span></span> |<span data-ttu-id="ac083-187">Controller 1</span><span class="sxs-lookup"><span data-stu-id="ac083-187">Controller 1</span></span> |
5. <span data-ttu-id="ac083-188">Schakel de defecte PCM en Verbreek de verbinding met het netsnoer levering.</span><span class="sxs-lookup"><span data-stu-id="ac083-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="ac083-189">U kunt nu de PCM verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ac083-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="ac083-190">De vergrendeling en de kant van de greep PCM tussen uw miniatuur en wijsvinger te vatten en verondersteld ze samen als u wilt openen van de greep.</span><span class="sxs-lookup"><span data-stu-id="ac083-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![De PCM-ingang openen](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="ac083-192">**Afbeelding 4** de PCM-ingang openen</span><span class="sxs-lookup"><span data-stu-id="ac083-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="ac083-193">De ingang houvastOpening en verwijder de PCM.</span><span class="sxs-lookup"><span data-stu-id="ac083-193">Grip the handle and remove the PCM.</span></span>
   
    ![PCM-apparaat verwijderen](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="ac083-195">**Afbeelding 5** de PCM verwijderen</span><span class="sxs-lookup"><span data-stu-id="ac083-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="ac083-196">Een vervangende PCM installeren</span><span class="sxs-lookup"><span data-stu-id="ac083-196">Install a replacement PCM</span></span>
<span data-ttu-id="ac083-197">Volg deze instructies voor het installeren van een PCM in uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ac083-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="ac083-198">Zorg ervoor dat u de back-up batterij module voordat u installeert de vervangende PCM (geldt voor alleen 764 W PCMs) hebt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ac083-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="ac083-199">Zie voor meer informatie hoe [verwijderen en voeg een back-up batterij module](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="ac083-199">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="ac083-200">Voor het installeren van een PCM</span><span class="sxs-lookup"><span data-stu-id="ac083-200">To install a PCM</span></span>
1. <span data-ttu-id="ac083-201">Controleer of u de juiste vervangende PCM voor deze bijlage.</span><span class="sxs-lookup"><span data-stu-id="ac083-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="ac083-202">De primaire behuizing moet een 764 W PCM en de behuizing EBOD moet een 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="ac083-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="ac083-203">U moet niet proberen om de 580 W PCM in de primaire behuizing of de 764 W PCM in de behuizing EBOD te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ac083-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="ac083-204">De volgende afbeelding toont waar u deze informatie op het label dat wordt aangebracht op de PCM identificeren.</span><span class="sxs-lookup"><span data-stu-id="ac083-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![Apparaat PCM-Label](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="ac083-206">**Afbeelding 6** PCM-label</span><span class="sxs-lookup"><span data-stu-id="ac083-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="ac083-207">Controleer op beschadiging van de behuizing, met bijzondere aandacht voor de connectors.</span><span class="sxs-lookup"><span data-stu-id="ac083-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ac083-208">**Installeer de module niet als een verbindingslijn pincodes verbogen zijn.**</span><span class="sxs-lookup"><span data-stu-id="ac083-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="ac083-209">Met de PCM-ingang op positie open de module de schuifregelaar in de behuizing.</span><span class="sxs-lookup"><span data-stu-id="ac083-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![Installatie van PCM-apparaat](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="ac083-211">**Afbeelding 7** de PCM installeren</span><span class="sxs-lookup"><span data-stu-id="ac083-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="ac083-212">De PCM-ingang handmatig af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="ac083-212">Manually close the PCM handle.</span></span> <span data-ttu-id="ac083-213">U moet een klik horen, zoals de vergrendeling ingang stelt.</span><span class="sxs-lookup"><span data-stu-id="ac083-213">You should hear a click as the handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ac083-214">Om ervoor te zorgen dat de pincodes connector hebt ingeschakeld, kunt u voorzichtig tug op de greep zonder de vergrendeling vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="ac083-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="ac083-215">Als de PCM dia uit, betekent dit dat de vergrendeling is gesloten voordat de connectors die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="ac083-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="ac083-216">De power-kabels aansluiten op de stroombron en op de PCM.</span><span class="sxs-lookup"><span data-stu-id="ac083-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="ac083-217">Beveilig de stam vrijstelling bales.</span><span class="sxs-lookup"><span data-stu-id="ac083-217">Secure the strain relief bales.</span></span> 
7. <span data-ttu-id="ac083-218">De PCM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ac083-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="ac083-219">Controleren of de vervanging geslaagd is: Ga in de klassieke Azure-portal van uw StorSimple Manager-service naar **apparaten** > **onderhoud**  >   **Hardwarestatus**.</span><span class="sxs-lookup"><span data-stu-id="ac083-219">Verify that the replacement was successful: in the Azure classic portal of your StorSimple Manager service, navigate to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="ac083-220">Onder **gedeelde onderdelen**, de status van de PCM moeten groene.</span><span class="sxs-lookup"><span data-stu-id="ac083-220">Under **Shared Components**, the status of the PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ac083-221">Duurt enkele minuten duren voordat de vervangende PCM volledig geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="ac083-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="ac083-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac083-222">Next steps</span></span>
<span data-ttu-id="ac083-223">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="ac083-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

