---
title: aaaReplace accu op Microsoft Azure StorSimple 8000 series apparaat | Microsoft Docs
description: Beschrijft hoe tooremove, vervangen en onderhouden van Hallo back-up batterij module op uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="a3a39-103">Vervang Hallo back-up batterij module op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="a3a39-103">Replace hello backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="a3a39-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a3a39-104">Overview</span></span>
<span data-ttu-id="a3a39-105">heeft een extra batterij pack Hallo primaire enclosure stroom en koeling Module (PCM) op uw Microsoft Azure StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="a3a39-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="a3a39-106">Dit pakket biedt power zodat hello StorSimple-apparaat kunt gegevens opslaan als er verlies van AC power toohello primaire behuizing.</span><span class="sxs-lookup"><span data-stu-id="a3a39-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="a3a39-107">Dit pack accu is waarnaar wordt verwezen tooas hello *back-up batterij module*.</span><span class="sxs-lookup"><span data-stu-id="a3a39-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="a3a39-108">Er bestaat een Hallo back-up batterij module alleen voor primaire behuizing Hallo in uw StorSimple-apparaat (Hallo EBOD behuizing bevat geen een back-up batterij module).</span><span class="sxs-lookup"><span data-stu-id="a3a39-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="a3a39-109">Deze zelfstudie wordt uitgelegd hoe:</span><span class="sxs-lookup"><span data-stu-id="a3a39-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="a3a39-110">Hallo back-up batterij module verwijderen</span><span class="sxs-lookup"><span data-stu-id="a3a39-110">Remove hello backup battery module</span></span>
* <span data-ttu-id="a3a39-111">Een nieuwe back-up batterij-module installeren</span><span class="sxs-lookup"><span data-stu-id="a3a39-111">Install a new backup battery module</span></span>
* <span data-ttu-id="a3a39-112">Hallo back-up batterij module onderhouden</span><span class="sxs-lookup"><span data-stu-id="a3a39-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3a39-113">Voordat verwijderen en het vervangen van een module back-up batterij Lees Hallo veiligheidsinformatie in Hallo [inleiding tooStorSimple Hardwarevervanging onderdeel](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="a3a39-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="a3a39-114">Hallo back-up batterij module verwijderen</span><span class="sxs-lookup"><span data-stu-id="a3a39-114">Remove hello backup battery module</span></span>
<span data-ttu-id="a3a39-115">Hallo back-up batterij-module voor uw StorSimple-apparaat is een field-replaceable unit.</span><span class="sxs-lookup"><span data-stu-id="a3a39-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="a3a39-116">Voordat deze wordt geïnstalleerd in Hallo PCM, moet Hallo accu module in de originele verpakking worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a3a39-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="a3a39-117">Volgende stappen tooremove Hallo back-up batterij Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a3a39-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="a3a39-118">tooremove hello back-up batterij module</span><span class="sxs-lookup"><span data-stu-id="a3a39-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="a3a39-119">Ga in de Azure-portal hello, blade tooyour Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="a3a39-119">In hello Azure portal, go tooyour StorSimple Device Manager service blade.</span></span> <span data-ttu-id="a3a39-120">Ga te**apparaten** en selecteer vervolgens het apparaat op Hallo lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="a3a39-120">Go too**Devices** and then select your device from hello list of devices.</span></span> <span data-ttu-id="a3a39-121">Navigeer te**Monitor** > **Hardware health**.</span><span class="sxs-lookup"><span data-stu-id="a3a39-121">Navigate too**Monitor** > **Hardware health**.</span></span> <span data-ttu-id="a3a39-122">Onder **gedeelde onderdelen**, status van de batterij Hallo Hallo bekijken.</span><span class="sxs-lookup"><span data-stu-id="a3a39-122">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="a3a39-123">Identificeer Hallo PCM in welke Hallo accu is mislukt.</span><span class="sxs-lookup"><span data-stu-id="a3a39-123">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="a3a39-124">Afbeelding 1 toont Hallo achterzijde Hallo StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="a3a39-124">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Backplane apparaat primaire behuizing modules](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="a3a39-126">**Afbeelding 1** achterzijde van het primaire apparaat van PCM en controller modules</span><span class="sxs-lookup"><span data-stu-id="a3a39-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="a3a39-127">Label</span><span class="sxs-lookup"><span data-stu-id="a3a39-127">Label</span></span> | <span data-ttu-id="a3a39-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a3a39-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="a3a39-129">1</span><span class="sxs-lookup"><span data-stu-id="a3a39-129">1</span></span> |<span data-ttu-id="a3a39-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="a3a39-130">PCM 0</span></span> |
   | <span data-ttu-id="a3a39-131">2</span><span class="sxs-lookup"><span data-stu-id="a3a39-131">2</span></span> |<span data-ttu-id="a3a39-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="a3a39-132">PCM 1</span></span> |
   | <span data-ttu-id="a3a39-133">3</span><span class="sxs-lookup"><span data-stu-id="a3a39-133">3</span></span> |<span data-ttu-id="a3a39-134">Controller 0</span><span class="sxs-lookup"><span data-stu-id="a3a39-134">Controller 0</span></span> |
   | <span data-ttu-id="a3a39-135">4</span><span class="sxs-lookup"><span data-stu-id="a3a39-135">4</span></span> |<span data-ttu-id="a3a39-136">Controller 1</span><span class="sxs-lookup"><span data-stu-id="a3a39-136">Controller 1</span></span> |
   
    <span data-ttu-id="a3a39-137">Zoals wordt weergegeven door de waarde 3 in afbeelding 2 hello, Hallo bewaking indicator geleid op PCM 0 die overeenkomt met te**accu veroorzaakt** moet worden belicht.</span><span class="sxs-lookup"><span data-stu-id="a3a39-137">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Backplane van apparaat PCM-bewaking indicatielampjes](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="a3a39-139">**Afbeelding 2** Back van PCM tonen Hallo indicatielampjes bewaking</span><span class="sxs-lookup"><span data-stu-id="a3a39-139">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="a3a39-140">Label</span><span class="sxs-lookup"><span data-stu-id="a3a39-140">Label</span></span> | <span data-ttu-id="a3a39-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a3a39-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="a3a39-142">1</span><span class="sxs-lookup"><span data-stu-id="a3a39-142">1</span></span> |<span data-ttu-id="a3a39-143">Fout in Echtheidsvoorwaarde power</span><span class="sxs-lookup"><span data-stu-id="a3a39-143">AC power failure</span></span> |
   | <span data-ttu-id="a3a39-144">2</span><span class="sxs-lookup"><span data-stu-id="a3a39-144">2</span></span> |<span data-ttu-id="a3a39-145">Ventilator mislukt</span><span class="sxs-lookup"><span data-stu-id="a3a39-145">Fan failure</span></span> |
   | <span data-ttu-id="a3a39-146">3</span><span class="sxs-lookup"><span data-stu-id="a3a39-146">3</span></span> |<span data-ttu-id="a3a39-147">Fout met betrekking tot accu</span><span class="sxs-lookup"><span data-stu-id="a3a39-147">Battery fault</span></span> |
   | <span data-ttu-id="a3a39-148">4</span><span class="sxs-lookup"><span data-stu-id="a3a39-148">4</span></span> |<span data-ttu-id="a3a39-149">PCM OK</span><span class="sxs-lookup"><span data-stu-id="a3a39-149">PCM OK</span></span> |
   | <span data-ttu-id="a3a39-150">5</span><span class="sxs-lookup"><span data-stu-id="a3a39-150">5</span></span> |<span data-ttu-id="a3a39-151">DC-stroomstoring</span><span class="sxs-lookup"><span data-stu-id="a3a39-151">DC power failure</span></span> |
   | <span data-ttu-id="a3a39-152">6</span><span class="sxs-lookup"><span data-stu-id="a3a39-152">6</span></span> |<span data-ttu-id="a3a39-153">Accu in orde</span><span class="sxs-lookup"><span data-stu-id="a3a39-153">Battery healthy</span></span> |
3. <span data-ttu-id="a3a39-154">tooremove hello PCM met een mislukte batterij Hallo stappen in [verwijderen van een PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="a3a39-154">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="a3a39-155">Met Hallo PCM verwijderd, lift en draaien Hallo accu module omhoog verwerken, zoals aangegeven in de volgende afbeelding Hallo en pull-up tooremove Hallo accu.</span><span class="sxs-lookup"><span data-stu-id="a3a39-155">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Verwijderen van de batterij van PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="a3a39-157">**Afbeelding 3** Hallo accu verwijderen uit Hallo PCM</span><span class="sxs-lookup"><span data-stu-id="a3a39-157">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="a3a39-158">Hallo-module in Hallo veld replaceable unit verpakking plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a3a39-158">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="a3a39-159">Hallo defecte eenheid tooMicrosoft voor de juiste onderhoud en verwerken retourneren.</span><span class="sxs-lookup"><span data-stu-id="a3a39-159">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="a3a39-160">Een nieuwe back-up batterij-module installeren</span><span class="sxs-lookup"><span data-stu-id="a3a39-160">Install a new backup battery module</span></span>
<span data-ttu-id="a3a39-161">Volgende stappen tooinstall Hallo vervanging accu van de module Hallo PCM in primaire behuizing van uw StorSimple-apparaat Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a3a39-161">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="a3a39-162">tooinstall hello accu module</span><span class="sxs-lookup"><span data-stu-id="a3a39-162">tooinstall hello battery module</span></span>
1. <span data-ttu-id="a3a39-163">Hallo back-up batterij module in de juiste richting Hallo in Hallo PCM plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a3a39-163">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="a3a39-164">Druk op omlaag Hallo accu module verwerkt alle Hallo manier tooseat Hallo-connector.</span><span class="sxs-lookup"><span data-stu-id="a3a39-164">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="a3a39-165">Vervang PCM in primaire behuizing Hallo Hallo door Hallo richtlijnen in [vervangen van een stroom en koeling Module op uw StorSimple-apparaat](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="a3a39-165">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="a3a39-166">Nadat Hallo vervanging voltooid is, gaat u tooyour apparaat en ga vervolgens te**Monitor** > **Hardware health** in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a3a39-166">After hello replacement is complete, go tooyour device and then go too**Monitor** > **Hardware health** in hello Azure portal.</span></span> <span data-ttu-id="a3a39-167">Controleer of Hallo status van Hallo accu toomake ervoor Hallo-installatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="a3a39-167">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="a3a39-168">Groene status geeft aan of Hallo accu in orde is.</span><span class="sxs-lookup"><span data-stu-id="a3a39-168">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="a3a39-169">Hallo back-up batterij module onderhouden</span><span class="sxs-lookup"><span data-stu-id="a3a39-169">Maintain hello backup battery module</span></span>
<span data-ttu-id="a3a39-170">In uw StorSimple-apparaat biedt Hallo back-up batterij module power toohello controller tijdens een power verlies-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="a3a39-170">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="a3a39-171">Hierdoor kan Hallo StorSimple-apparaat toosave kritieke gegevens voorafgaande tooshutting omlaag op een gecontroleerde manier.</span><span class="sxs-lookup"><span data-stu-id="a3a39-171">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="a3a39-172">Hallo-systeem kan twee opeenvolgende verlies gebeurtenissen verwerken met twee volledig opgeladen batterijen in Hallo PCMs.</span><span class="sxs-lookup"><span data-stu-id="a3a39-172">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="a3a39-173">Hallo in hello Azure-portal, **Hardware health** onder Hallo **Monitor** blade geeft aan of Hallo accu is defect of Hallo einde van de levenscyclus bijna is bereikt.</span><span class="sxs-lookup"><span data-stu-id="a3a39-173">In hello Azure portal, hello **Hardware health** under hello **Monitor** blade indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="a3a39-174">Hallo Accustatus wordt aangegeven door **accu in PCM 0** of **accu in PCM 1** onder **gedeelde onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="a3a39-174">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="a3a39-175">Deze blade ziet een **GEDEGRADEERD** staat zijn voor het einde van de levensduur nadert, en **mislukt** voor einde van de levenscyclus bereikt.</span><span class="sxs-lookup"><span data-stu-id="a3a39-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="a3a39-176">Hallo accu kan rapporteren **mislukt** gewoon moet toobe in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="a3a39-176">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>


<span data-ttu-id="a3a39-177">Als hello **GEDEGRADEERD** status wordt weergegeven, wordt aangeraden Hallo na verloop van de actie:</span><span class="sxs-lookup"><span data-stu-id="a3a39-177">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="a3a39-178">Hallo-systeem kan zich recente stroomuitval of Hallo batterijen kunnen worden periodieke momenteel onderhoudswerkzaamheden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a3a39-178">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="a3a39-179">Houd rekening met Hallo system 12 uur voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="a3a39-179">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="a3a39-180">Als het Hallo-status is nog steeds **GEDEGRADEERD** na 12 uur van continue verbinding tooAC power Hello-controllers en PCMs wordt uitgevoerd, klikt u vervolgens Hallo batterij moet toobe vervangen.</span><span class="sxs-lookup"><span data-stu-id="a3a39-180">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="a3a39-181">Neem [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor een module van de back-up batterij vervanging.</span><span class="sxs-lookup"><span data-stu-id="a3a39-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="a3a39-182">Als de status van de Hallo na 12 uur OK wordt, Hallo accu operationeel is en deze alleen kosten met zich mee onderhoud nodig.</span><span class="sxs-lookup"><span data-stu-id="a3a39-182">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="a3a39-183">Als er niet is een gekoppelde verlies van netstroom en Hallo PCM is ingeschakeld en aangesloten tooAC power, moet Hallo accu toobe vervangen.</span><span class="sxs-lookup"><span data-stu-id="a3a39-183">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="a3a39-184">[Neem contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder een module van de back-up batterij vervanging.</span><span class="sxs-lookup"><span data-stu-id="a3a39-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3a39-185">Dispose Hallo mislukt accu volgens toonational en regionale voorschriften.</span><span class="sxs-lookup"><span data-stu-id="a3a39-185">Dispose of hello failed battery according toonational and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3a39-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3a39-186">Next steps</span></span>
<span data-ttu-id="a3a39-187">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="a3a39-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

