---
title: aaaReplace een PCM op uw StorSimple 8000 series apparaat | Microsoft Docs
description: Legt uit hoe tooremove en vervang Hallo stroom en koeling Module (PCM) op uw StorSimple-apparaat
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="c1514-103">Vervangen van een stroom en koeling Module op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="c1514-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="c1514-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c1514-104">Overview</span></span>
<span data-ttu-id="c1514-105">Hallo stroom en koeling Module (PCM) in uw Microsoft Azure StorSimple-apparaat bestaat uit een voeding en koeling van ventilatoren die worden beheerd via Hallo primaire en EBOD behuizingen.</span><span class="sxs-lookup"><span data-stu-id="c1514-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="c1514-106">Er is slechts één model van PCM die is gecertificeerd voor elke behuizing.</span><span class="sxs-lookup"><span data-stu-id="c1514-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="c1514-107">Hallo primaire behuizing is gecertificeerd voor een 764 W PCM en Hallo EBOD behuizing is gecertificeerd voor een 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="c1514-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="c1514-108">Hoewel Hallo PCMs voor primaire behuizing Hallo en Hallo EBOD behuizing verschillend zijn, is Hallo vervangingsprocedure identiek zijn.</span><span class="sxs-lookup"><span data-stu-id="c1514-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="c1514-109">Deze zelfstudie wordt uitgelegd hoe:</span><span class="sxs-lookup"><span data-stu-id="c1514-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="c1514-110">Een PCM verwijderen</span><span class="sxs-lookup"><span data-stu-id="c1514-110">Remove a PCM</span></span>
* <span data-ttu-id="c1514-111">Een vervangende PCM installeren</span><span class="sxs-lookup"><span data-stu-id="c1514-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1514-112">Voordat u verwijdert en vervangt een PCM Lees Hallo veiligheidsinformatie in [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="c1514-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="c1514-113">Voordat u een PCM vervangen</span><span class="sxs-lookup"><span data-stu-id="c1514-113">Before you replace a PCM</span></span>
<span data-ttu-id="c1514-114">Zich bewust zijn van de volgende belangrijke problemen op voordat u uw PCM vervangt Hallo:</span><span class="sxs-lookup"><span data-stu-id="c1514-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="c1514-115">Als voeding van Hallo Hallo PCM mislukt, laat defecte Hallo-module geïnstalleerd maar Hallo netsnoer te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c1514-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="c1514-116">Hallo-ventilator wordt tooreceive vermogen afkomstig van Hallo behuizing blijven en doorgaan met het juiste koeling tooprovide.</span><span class="sxs-lookup"><span data-stu-id="c1514-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="c1514-117">Als Hallo ventilator mislukt, moet Hallo PCM toobe direct vervangen.</span><span class="sxs-lookup"><span data-stu-id="c1514-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="c1514-118">Voordat u Hallo PCM verwijdert, Verbreek Hallo power Hallo PCM door het uitschakelen van de belangrijkste switch hello (indien aanwezig) of door het netsnoer Hallo fysiek verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c1514-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="c1514-119">Dit biedt een waarschuwing tooyour-systeem afsluiten power dreigt.</span><span class="sxs-lookup"><span data-stu-id="c1514-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="c1514-120">Moet u ervoor zorgen dat andere PCM functioneert Hallo steeds werking van het systeem voordat defecte PCM vervangen Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1514-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="c1514-121">Een defecte PCM moet worden vervangen door een volledig operationeel PCM zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="c1514-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="c1514-122">Vervanging van PCM-module duurt slechts enkele minuten toocomplete, maar deze moet worden voltooid binnen 10 minuten na het verwijderen is mislukt Hallo PCM tooprevent oververhitting.</span><span class="sxs-lookup"><span data-stu-id="c1514-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="c1514-123">Houd er rekening mee dat Hallo vervanging 764 W PCM-modules uit Hallo factory verzonden geen Hallo back-up batterij module bevatten.</span><span class="sxs-lookup"><span data-stu-id="c1514-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="c1514-124">U moet tooremove Hallo accu van uw defecte PCM en plaatst u deze in Hallo vervanging module voorafgaande tooperforming Hallo vervanging.</span><span class="sxs-lookup"><span data-stu-id="c1514-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="c1514-125">Voor meer informatie Zie hoe te[verwijderen en voeg een back-up batterij module](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="c1514-125">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="c1514-126">Een PCM verwijderen</span><span class="sxs-lookup"><span data-stu-id="c1514-126">Remove a PCM</span></span>
<span data-ttu-id="c1514-127">Volg deze instructies wanneer u klaar tooremove een stroom en koeling Module (PCM) van uw Microsoft Azure StorSimple-apparaat bent.</span><span class="sxs-lookup"><span data-stu-id="c1514-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="c1514-128">Voordat u uw PCM verwijdert, moet u controleren of u een juiste vervangende (764 W voor primaire behuizing Hallo) of 580 W voor Hallo EBOD behuizing hebben.</span><span class="sxs-lookup"><span data-stu-id="c1514-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="c1514-129">een PCM tooremove</span><span class="sxs-lookup"><span data-stu-id="c1514-129">tooremove a PCM</span></span>
1. <span data-ttu-id="c1514-130">Klik in de klassieke Azure-portal hello, **instellingen > Monitor > Hardware health**.</span><span class="sxs-lookup"><span data-stu-id="c1514-130">In hello Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="c1514-131">Controleer de status van Hallo PCM onderdelen onder Hallo **gedeelde onderdelen** tooidentify die PCM is mislukt:</span><span class="sxs-lookup"><span data-stu-id="c1514-131">Check hello status of hello PCM components under **Shared components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="c1514-132">Als een voeding in PCM 0 is mislukt, de status van Hallo **Power Supply in PCM 0** rood.</span><span class="sxs-lookup"><span data-stu-id="c1514-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="c1514-133">Als een voeding in PCM-1 is mislukt, de status van Hallo **Power Supply in PCM 1** rood.</span><span class="sxs-lookup"><span data-stu-id="c1514-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="c1514-134">Als het Hallo-ventilator in PCM-1 is mislukt, status van een Hallo **koeling van 0 voor PCM 0** of **koeling 1 voor PCM 0** rood.</span><span class="sxs-lookup"><span data-stu-id="c1514-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="c1514-135">Back-mislukte PCM op Hallo van primaire behuizing Hallo Hallo vinden.</span><span class="sxs-lookup"><span data-stu-id="c1514-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="c1514-136">Als u een model 8600 uitvoert, moet u Hallo primaire behuizing vinden door Hallo eenheid identificatie systeemnummer op Hallo LED frontpaneel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c1514-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="c1514-137">Hallo-eenheid-ID weergegeven op de primaire behuizing Hallo is standaard **00**, terwijl Hallo standaard eenheid-ID op Hallo EBOD behuizing weergegeven **01**.</span><span class="sxs-lookup"><span data-stu-id="c1514-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="c1514-138">Hallo en de volgende tabel wordt uitgelegd Hallo voorpaneel Hallo LED worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c1514-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![Systeem-ID op voorpaneel OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="c1514-140">**Afbeelding 1** voorzijde Configuratiescherm Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="c1514-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="c1514-141">Label</span><span class="sxs-lookup"><span data-stu-id="c1514-141">Label</span></span> | <span data-ttu-id="c1514-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c1514-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c1514-143">1</span><span class="sxs-lookup"><span data-stu-id="c1514-143">1</span></span> |<span data-ttu-id="c1514-144">Knop Dempen</span><span class="sxs-lookup"><span data-stu-id="c1514-144">Mute button</span></span> |
   | <span data-ttu-id="c1514-145">2</span><span class="sxs-lookup"><span data-stu-id="c1514-145">2</span></span> |<span data-ttu-id="c1514-146">Inschakelen van het systeem</span><span class="sxs-lookup"><span data-stu-id="c1514-146">System power</span></span> |
   | <span data-ttu-id="c1514-147">3</span><span class="sxs-lookup"><span data-stu-id="c1514-147">3</span></span> |<span data-ttu-id="c1514-148">Module-fout</span><span class="sxs-lookup"><span data-stu-id="c1514-148">Module fault</span></span> |
   | <span data-ttu-id="c1514-149">4</span><span class="sxs-lookup"><span data-stu-id="c1514-149">4</span></span> |<span data-ttu-id="c1514-150">Logische-fout</span><span class="sxs-lookup"><span data-stu-id="c1514-150">Logical fault</span></span> |
   | <span data-ttu-id="c1514-151">5</span><span class="sxs-lookup"><span data-stu-id="c1514-151">5</span></span> |<span data-ttu-id="c1514-152">Eenheid-ID weergeven</span><span class="sxs-lookup"><span data-stu-id="c1514-152">Unit ID display</span></span> |
3. <span data-ttu-id="c1514-153">Hallo indicatielampjes in Hallo achterzijde van de primaire behuizing Hallo bewaking kan ook worden gebruikt tooidentify Hallo defecte PCM.</span><span class="sxs-lookup"><span data-stu-id="c1514-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="c1514-154">Zie de volgende Hallo diagram en toounderstand hoe tabel toouse Hallo LED's toolocate Hallo defecte PCM.</span><span class="sxs-lookup"><span data-stu-id="c1514-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="c1514-155">Bijvoorbeeld, als hello geleid bijbehorende toohello **ventilator mislukken** is belicht, Hallo ventilator is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c1514-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="c1514-156">Op dezelfde manier als hello geleid hoort te**AC mislukken** is belicht, Hallo voeding is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c1514-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![Backplane van apparaat PCM bewaking LED](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="c1514-158">**Afbeelding 2** Back van PCM met LED</span><span class="sxs-lookup"><span data-stu-id="c1514-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="c1514-159">Label</span><span class="sxs-lookup"><span data-stu-id="c1514-159">Label</span></span> | <span data-ttu-id="c1514-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c1514-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c1514-161">1</span><span class="sxs-lookup"><span data-stu-id="c1514-161">1</span></span> |<span data-ttu-id="c1514-162">Fout in Echtheidsvoorwaarde power</span><span class="sxs-lookup"><span data-stu-id="c1514-162">AC power failure</span></span> |
   | <span data-ttu-id="c1514-163">2</span><span class="sxs-lookup"><span data-stu-id="c1514-163">2</span></span> |<span data-ttu-id="c1514-164">Ventilator mislukt</span><span class="sxs-lookup"><span data-stu-id="c1514-164">Fan failure</span></span> |
   | <span data-ttu-id="c1514-165">3</span><span class="sxs-lookup"><span data-stu-id="c1514-165">3</span></span> |<span data-ttu-id="c1514-166">Fout met betrekking tot accu</span><span class="sxs-lookup"><span data-stu-id="c1514-166">Battery fault</span></span> |
   | <span data-ttu-id="c1514-167">4</span><span class="sxs-lookup"><span data-stu-id="c1514-167">4</span></span> |<span data-ttu-id="c1514-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="c1514-168">PCM OK</span></span> |
   | <span data-ttu-id="c1514-169">5</span><span class="sxs-lookup"><span data-stu-id="c1514-169">5</span></span> |<span data-ttu-id="c1514-170">DC-stroomstoring</span><span class="sxs-lookup"><span data-stu-id="c1514-170">DC power failure</span></span> |
   | <span data-ttu-id="c1514-171">6</span><span class="sxs-lookup"><span data-stu-id="c1514-171">6</span></span> |<span data-ttu-id="c1514-172">Accu in orde</span><span class="sxs-lookup"><span data-stu-id="c1514-172">Battery healthy</span></span> |
4. <span data-ttu-id="c1514-173">Raadpleeg de volgende diagram van Hallo achterzijde Hallo StorSimple-apparaat toolocate Hallo mislukt PCM module toohello.</span><span class="sxs-lookup"><span data-stu-id="c1514-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="c1514-174">PCM 0 op Hallo links en PCM 1 op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="c1514-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="c1514-175">Hallo-tabel die volgt bevat uitleg over Hallo-modules.</span><span class="sxs-lookup"><span data-stu-id="c1514-175">hello table that follows explains hello modules.</span></span>
   
     ![Backplane apparaat primaire behuizing modules](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="c1514-177">**Afbeelding 3** achterzijde van het apparaat met de invoegtoepassing modules</span><span class="sxs-lookup"><span data-stu-id="c1514-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="c1514-178">Label</span><span class="sxs-lookup"><span data-stu-id="c1514-178">Label</span></span> | <span data-ttu-id="c1514-179">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c1514-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c1514-180">1</span><span class="sxs-lookup"><span data-stu-id="c1514-180">1</span></span> |<span data-ttu-id="c1514-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="c1514-181">PCM 0</span></span> |
   | <span data-ttu-id="c1514-182">2</span><span class="sxs-lookup"><span data-stu-id="c1514-182">2</span></span> |<span data-ttu-id="c1514-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="c1514-183">PCM 1</span></span> |
   | <span data-ttu-id="c1514-184">3</span><span class="sxs-lookup"><span data-stu-id="c1514-184">3</span></span> |<span data-ttu-id="c1514-185">Controller 0</span><span class="sxs-lookup"><span data-stu-id="c1514-185">Controller 0</span></span> |
   | <span data-ttu-id="c1514-186">4</span><span class="sxs-lookup"><span data-stu-id="c1514-186">4</span></span> |<span data-ttu-id="c1514-187">Controller 1</span><span class="sxs-lookup"><span data-stu-id="c1514-187">Controller 1</span></span> |
5. <span data-ttu-id="c1514-188">Schakel afmelden Hallo defecte PCM en Hallo levering netsnoer verbreken.</span><span class="sxs-lookup"><span data-stu-id="c1514-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="c1514-189">U kunt nu Hallo PCM verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c1514-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="c1514-190">Hallo vergrendeling en Hallo-zijde van PCM handelen tussen uw miniatuur en wijsvinger hello te vatten en ze samen tooopen Hallo ingang verondersteld.</span><span class="sxs-lookup"><span data-stu-id="c1514-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![De PCM-ingang openen](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="c1514-192">**Afbeelding 4** openen Hallo PCM verwerken</span><span class="sxs-lookup"><span data-stu-id="c1514-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="c1514-193">Hallo greep verwerken en Hallo PCM verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c1514-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![PCM-apparaat verwijderen](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="c1514-195">**Afbeelding 5** verwijderd Hallo PCM</span><span class="sxs-lookup"><span data-stu-id="c1514-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="c1514-196">Een vervangende PCM installeren</span><span class="sxs-lookup"><span data-stu-id="c1514-196">Install a replacement PCM</span></span>
<span data-ttu-id="c1514-197">Volg deze instructies tooinstall een PCM in uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c1514-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="c1514-198">Zorg ervoor dat u Hallo back-up batterij module voorafgaande tooinstalling Hallo vervanging PCM (geldt alleen in W PCMs too764) hebt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="c1514-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="c1514-199">Voor meer informatie Zie hoe te[verwijderen en voeg een back-up batterij module](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="c1514-199">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="c1514-200">een PCM tooinstall</span><span class="sxs-lookup"><span data-stu-id="c1514-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="c1514-201">Controleer of u Hallo juiste vervangende PCM voor deze bijlage.</span><span class="sxs-lookup"><span data-stu-id="c1514-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="c1514-202">Hallo primaire behuizing moet een 764 W PCM en Hallo EBOD behuizing moet een 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="c1514-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="c1514-203">U moet niet proberen toouse 580 W PCM in primaire behuizing Hallo Hallo of Hallo 764 W PCM in Hallo EBOD behuizing.</span><span class="sxs-lookup"><span data-stu-id="c1514-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="c1514-204">Hallo volgende afbeelding toont waar tooidentify deze informatie op Hallo dat label toohello PCM aangebracht.</span><span class="sxs-lookup"><span data-stu-id="c1514-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![Apparaat PCM-Label](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="c1514-206">**Afbeelding 6** PCM-label</span><span class="sxs-lookup"><span data-stu-id="c1514-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="c1514-207">Controleren op beschadigingen toohello behuizing, met bijzondere aandacht toohello connectors.</span><span class="sxs-lookup"><span data-stu-id="c1514-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c1514-208">**Installeer geen Hallo module als een verbindingslijn pincodes verbogen zijn.**</span><span class="sxs-lookup"><span data-stu-id="c1514-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="c1514-209">Open positie, dia Hallo module in Hallo behuizing Hello PCM op Hallo verwerken.</span><span class="sxs-lookup"><span data-stu-id="c1514-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![Installatie van PCM-apparaat](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="c1514-211">**Afbeelding 7** installeren Hallo PCM</span><span class="sxs-lookup"><span data-stu-id="c1514-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="c1514-212">Hallo PCM-ingang handmatig af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="c1514-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="c1514-213">U moet een klik horen als het Hallo-ingang vergrendeling stelt.</span><span class="sxs-lookup"><span data-stu-id="c1514-213">You should hear a click as hello handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1514-214">tooensure die connector pincodes Hallo hebt ingeschakeld, u kunt voorzichtig op Hallo ingang tug zonder Hallo vergrendeling vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="c1514-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="c1514-215">Als Hallo PCM dia uit's wordt verwezen naar dat die Hallo-vergrendeling is afgesloten voordat het Hallo-connectors die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="c1514-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   
5. <span data-ttu-id="c1514-216">Hallo kabels toohello power stroombron en toohello PCM verbinden.</span><span class="sxs-lookup"><span data-stu-id="c1514-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="c1514-217">Hallo stam vrijstelling bales beveiligen.</span><span class="sxs-lookup"><span data-stu-id="c1514-217">Secure hello strain relief bales.</span></span>
7. <span data-ttu-id="c1514-218">Hallo PCM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c1514-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="c1514-219">Controleren of Hallo vervanging geslaagd is: Ga tooyour apparaat in hello Azure-portal van uw StorSimple-apparaat Manager-service, en vervolgens te**instellingen > Monitor > Hardware health**.</span><span class="sxs-lookup"><span data-stu-id="c1514-219">Verify that hello replacement was successful: in hello Azure portal of your StorSimple Device Manager service, navigate tooyour device and then too**Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="c1514-220">Onder Hallo **gedeelde onderdelen**, moet de status van de Hallo Hallo PCM groen.</span><span class="sxs-lookup"><span data-stu-id="c1514-220">Under hello **Shared components**, hello status of hello PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1514-221">Het kan enkele minuten duren voordat Hallo vervanging PCM toocompletely initialiseren.</span><span class="sxs-lookup"><span data-stu-id="c1514-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1514-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1514-222">Next steps</span></span>
<span data-ttu-id="c1514-223">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="c1514-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

