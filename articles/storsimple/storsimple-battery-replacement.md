---
title: aaaReplace accu op Microsoft Azure StorSimple-apparaat | Microsoft Docs
description: Beschrijft hoe tooremove, vervangen en onderhouden van Hallo back-up batterij module op uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="12d5e-103">Vervang Hallo back-up batterij module op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="12d5e-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="12d5e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="12d5e-104">Overview</span></span>
<span data-ttu-id="12d5e-105">heeft een extra batterij pack Hallo primaire enclosure stroom en koeling Module (PCM) op uw Microsoft Azure StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="12d5e-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="12d5e-106">Dit pakket biedt power zodat hello StorSimple-apparaat kunt gegevens opslaan als er verlies van AC power toohello primaire behuizing.</span><span class="sxs-lookup"><span data-stu-id="12d5e-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="12d5e-107">Dit pack accu is waarnaar wordt verwezen tooas hello *back-up batterij module*.</span><span class="sxs-lookup"><span data-stu-id="12d5e-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="12d5e-108">Er bestaat een Hallo back-up batterij module alleen voor primaire behuizing Hallo in uw StorSimple-apparaat (Hallo EBOD behuizing bevat geen een back-up batterij module).</span><span class="sxs-lookup"><span data-stu-id="12d5e-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="12d5e-109">Deze zelfstudie wordt uitgelegd hoe:</span><span class="sxs-lookup"><span data-stu-id="12d5e-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="12d5e-110">Hallo back-up batterij module verwijderen</span><span class="sxs-lookup"><span data-stu-id="12d5e-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="12d5e-111">Een nieuwe back-up batterij-module installeren</span><span class="sxs-lookup"><span data-stu-id="12d5e-111">Install a new backup battery module</span></span>
* <span data-ttu-id="12d5e-112">Hallo back-up batterij module onderhouden</span><span class="sxs-lookup"><span data-stu-id="12d5e-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12d5e-113">Voordat verwijderen en het vervangen van een module back-up batterij Lees Hallo veiligheidsinformatie in Hallo [inleiding tooStorSimple Hardwarevervanging onderdeel](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="12d5e-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="12d5e-114">Hallo back-up batterij module verwijderen</span><span class="sxs-lookup"><span data-stu-id="12d5e-114">Remove hello backup battery module</span></span>
<span data-ttu-id="12d5e-115">Hallo back-up batterij-module voor uw StorSimple-apparaat is een field-replaceable unit.</span><span class="sxs-lookup"><span data-stu-id="12d5e-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="12d5e-116">Voordat deze wordt geïnstalleerd in Hallo PCM, moet Hallo accu module in de originele verpakking worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="12d5e-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="12d5e-117">Volgende stappen tooremove Hallo back-up batterij Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="12d5e-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="12d5e-118">tooremove hello back-up batterij module</span><span class="sxs-lookup"><span data-stu-id="12d5e-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="12d5e-119">In klassieke Azure-portal hello, gaat u te**apparaten** > **onderhoud** > **hardwarestatus**.</span><span class="sxs-lookup"><span data-stu-id="12d5e-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="12d5e-120">Onder **gedeelde onderdelen**, status van de batterij Hallo Hallo bekijken.</span><span class="sxs-lookup"><span data-stu-id="12d5e-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="12d5e-121">Identificeer Hallo PCM in welke Hallo accu is mislukt.</span><span class="sxs-lookup"><span data-stu-id="12d5e-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="12d5e-122">Afbeelding 1 toont Hallo achterzijde Hallo StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="12d5e-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Backplane apparaat primaire behuizing modules](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="12d5e-124">**Afbeelding 1** achterzijde van het primaire apparaat van PCM en controller modules</span><span class="sxs-lookup"><span data-stu-id="12d5e-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="12d5e-125">Label</span><span class="sxs-lookup"><span data-stu-id="12d5e-125">Label</span></span> | <span data-ttu-id="12d5e-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="12d5e-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="12d5e-127">1</span><span class="sxs-lookup"><span data-stu-id="12d5e-127">1</span></span> |<span data-ttu-id="12d5e-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="12d5e-128">PCM 0</span></span> |
   | <span data-ttu-id="12d5e-129">2</span><span class="sxs-lookup"><span data-stu-id="12d5e-129">2</span></span> |<span data-ttu-id="12d5e-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="12d5e-130">PCM 1</span></span> |
   | <span data-ttu-id="12d5e-131">3</span><span class="sxs-lookup"><span data-stu-id="12d5e-131">3</span></span> |<span data-ttu-id="12d5e-132">Controller 0</span><span class="sxs-lookup"><span data-stu-id="12d5e-132">Controller 0</span></span> |
   | <span data-ttu-id="12d5e-133">4</span><span class="sxs-lookup"><span data-stu-id="12d5e-133">4</span></span> |<span data-ttu-id="12d5e-134">Controller 1</span><span class="sxs-lookup"><span data-stu-id="12d5e-134">Controller 1</span></span> |
   
    <span data-ttu-id="12d5e-135">Zoals wordt weergegeven door de waarde 3 in afbeelding 2 hello, Hallo bewaking indicator geleid op PCM 0 die overeenkomt met te**accu veroorzaakt** moet worden belicht.</span><span class="sxs-lookup"><span data-stu-id="12d5e-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Backplane van apparaat PCM-bewaking indicatielampjes](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="12d5e-137">**Afbeelding 2** Back van PCM tonen Hallo indicatielampjes bewaking</span><span class="sxs-lookup"><span data-stu-id="12d5e-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="12d5e-138">Label</span><span class="sxs-lookup"><span data-stu-id="12d5e-138">Label</span></span> | <span data-ttu-id="12d5e-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="12d5e-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="12d5e-140">1</span><span class="sxs-lookup"><span data-stu-id="12d5e-140">1</span></span> |<span data-ttu-id="12d5e-141">Fout in Echtheidsvoorwaarde power</span><span class="sxs-lookup"><span data-stu-id="12d5e-141">AC power failure</span></span> |
   | <span data-ttu-id="12d5e-142">2</span><span class="sxs-lookup"><span data-stu-id="12d5e-142">2</span></span> |<span data-ttu-id="12d5e-143">Ventilator mislukt</span><span class="sxs-lookup"><span data-stu-id="12d5e-143">Fan failure</span></span> |
   | <span data-ttu-id="12d5e-144">3</span><span class="sxs-lookup"><span data-stu-id="12d5e-144">3</span></span> |<span data-ttu-id="12d5e-145">Fout met betrekking tot accu</span><span class="sxs-lookup"><span data-stu-id="12d5e-145">Battery fault</span></span> |
   | <span data-ttu-id="12d5e-146">4</span><span class="sxs-lookup"><span data-stu-id="12d5e-146">4</span></span> |<span data-ttu-id="12d5e-147">PCM OK</span><span class="sxs-lookup"><span data-stu-id="12d5e-147">PCM OK</span></span> |
   | <span data-ttu-id="12d5e-148">5</span><span class="sxs-lookup"><span data-stu-id="12d5e-148">5</span></span> |<span data-ttu-id="12d5e-149">DC-stroomstoring</span><span class="sxs-lookup"><span data-stu-id="12d5e-149">DC power failure</span></span> |
   | <span data-ttu-id="12d5e-150">6</span><span class="sxs-lookup"><span data-stu-id="12d5e-150">6</span></span> |<span data-ttu-id="12d5e-151">Accu in orde</span><span class="sxs-lookup"><span data-stu-id="12d5e-151">Battery healthy</span></span> |
3. <span data-ttu-id="12d5e-152">tooremove hello PCM met een mislukte batterij Hallo stappen in [verwijderen van een PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="12d5e-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="12d5e-153">Met Hallo PCM verwijderd, lift en draaien Hallo accu module omhoog verwerken, zoals aangegeven in de volgende afbeelding Hallo en pull-up tooremove Hallo accu.</span><span class="sxs-lookup"><span data-stu-id="12d5e-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Verwijderen van de batterij van PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="12d5e-155">**Afbeelding 3** Hallo accu verwijderen uit Hallo PCM</span><span class="sxs-lookup"><span data-stu-id="12d5e-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="12d5e-156">Hallo-module in Hallo veld replaceable unit verpakking plaatsen.</span><span class="sxs-lookup"><span data-stu-id="12d5e-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="12d5e-157">Hallo defecte eenheid tooMicrosoft voor de juiste onderhoud en verwerken retourneren.</span><span class="sxs-lookup"><span data-stu-id="12d5e-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="12d5e-158">Een nieuwe back-up batterij-module installeren</span><span class="sxs-lookup"><span data-stu-id="12d5e-158">Install a new backup battery module</span></span>
<span data-ttu-id="12d5e-159">Volgende stappen tooinstall Hallo vervanging accu van de module Hallo PCM in primaire behuizing van uw StorSimple-apparaat Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="12d5e-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="12d5e-160">tooinstall hello accu module</span><span class="sxs-lookup"><span data-stu-id="12d5e-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="12d5e-161">Hallo back-up batterij module in de juiste richting Hallo in Hallo PCM plaatsen.</span><span class="sxs-lookup"><span data-stu-id="12d5e-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="12d5e-162">Druk op omlaag Hallo accu module verwerkt alle Hallo manier tooseat Hallo-connector.</span><span class="sxs-lookup"><span data-stu-id="12d5e-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="12d5e-163">Vervang PCM in primaire behuizing Hallo Hallo door Hallo richtlijnen in [vervangen van een stroom en koeling Module op uw StorSimple-apparaat](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="12d5e-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="12d5e-164">Nadat het Hallo-vervanging is voltooid, gaat u te**apparaten** > **onderhoud** > **hardwarestatus** in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="12d5e-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="12d5e-165">Controleer of Hallo status van Hallo accu toomake ervoor Hallo-installatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="12d5e-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="12d5e-166">Groene status geeft aan of Hallo accu in orde is.</span><span class="sxs-lookup"><span data-stu-id="12d5e-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="12d5e-167">Hallo back-up batterij module onderhouden</span><span class="sxs-lookup"><span data-stu-id="12d5e-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="12d5e-168">In uw StorSimple-apparaat biedt Hallo back-up batterij module power toohello controller tijdens een power verlies-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="12d5e-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="12d5e-169">Hierdoor kan Hallo StorSimple-apparaat toosave kritieke gegevens voorafgaande tooshutting omlaag op een gecontroleerde manier.</span><span class="sxs-lookup"><span data-stu-id="12d5e-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="12d5e-170">Hallo-systeem kan twee opeenvolgende verlies gebeurtenissen verwerken met twee volledig opgeladen batterijen in Hallo PCMs.</span><span class="sxs-lookup"><span data-stu-id="12d5e-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="12d5e-171">In de klassieke Azure-portal hello, Hallo **hardwarestatus** op Hallo **onderhoud** pagina geeft aan of Hallo accu is defect of Hallo einde van de levenscyclus bijna is bereikt.</span><span class="sxs-lookup"><span data-stu-id="12d5e-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="12d5e-172">Hallo Accustatus wordt aangegeven door **accu in PCM 0** of **accu in PCM 1** onder **gedeelde onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="12d5e-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="12d5e-173">Deze pagina wordt weergegeven een **GEDEGRADEERD** staat zijn voor het einde van de levensduur nadert, en **mislukt** voor einde van de levenscyclus bereikt.</span><span class="sxs-lookup"><span data-stu-id="12d5e-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="12d5e-174">Hallo accu kan rapporteren **mislukt** gewoon moet toobe in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="12d5e-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="12d5e-175">Als hello **GEDEGRADEERD** status wordt weergegeven, wordt aangeraden Hallo na verloop van de actie:</span><span class="sxs-lookup"><span data-stu-id="12d5e-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="12d5e-176">Hallo-systeem kan zich recente stroomuitval of Hallo batterijen kunnen worden periodieke momenteel onderhoudswerkzaamheden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12d5e-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="12d5e-177">Houd rekening met Hallo system 12 uur voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="12d5e-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="12d5e-178">Als het Hallo-status is nog steeds **GEDEGRADEERD** na 12 uur van continue verbinding tooAC power Hello-controllers en PCMs wordt uitgevoerd, klikt u vervolgens Hallo batterij moet toobe vervangen.</span><span class="sxs-lookup"><span data-stu-id="12d5e-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="12d5e-179">Neem [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) voor een module van de back-up batterij vervanging.</span><span class="sxs-lookup"><span data-stu-id="12d5e-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="12d5e-180">Als de status van de Hallo na 12 uur OK wordt, Hallo accu operationeel is en deze alleen kosten met zich mee onderhoud nodig.</span><span class="sxs-lookup"><span data-stu-id="12d5e-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="12d5e-181">Als er niet is een gekoppelde verlies van netstroom en Hallo PCM is ingeschakeld en aangesloten tooAC power, moet Hallo accu toobe vervangen.</span><span class="sxs-lookup"><span data-stu-id="12d5e-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="12d5e-182">[Neem contact op met Microsoft Support](storsimple-contact-microsoft-support.md) tooorder een module van de back-up batterij vervanging.</span><span class="sxs-lookup"><span data-stu-id="12d5e-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12d5e-183">Dispose Hallo mislukt accu volgens toonational en regionale voorschriften.</span><span class="sxs-lookup"><span data-stu-id="12d5e-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="12d5e-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12d5e-184">Next steps</span></span>
<span data-ttu-id="12d5e-185">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="12d5e-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

