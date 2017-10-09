---
title: een controller StorSimple EBOD aaaReplace | Microsoft Docs
description: Legt uit hoe tooremove en Vervang een of beide EBOD domeincontrollers op een StorSimple 8600-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="21029-103">Vervangen van een domeincontroller EBOD op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="21029-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="21029-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="21029-104">Overview</span></span>
<span data-ttu-id="21029-105">Deze zelfstudie wordt uitgelegd hoe tooreplace een defecte EBOD controllermodule op uw Microsoft Azure StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="21029-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="21029-106">een module van de domeincontroller EBOD tooreplace, moet u:</span><span class="sxs-lookup"><span data-stu-id="21029-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="21029-107">Hallo defecte EBOD controller verwijderen</span><span class="sxs-lookup"><span data-stu-id="21029-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="21029-108">Een nieuwe EBOD controller installeren</span><span class="sxs-lookup"><span data-stu-id="21029-108">Install a new EBOD controller</span></span>

<span data-ttu-id="21029-109">Houd rekening met Hallo volgende informatie voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="21029-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="21029-110">Lege EBOD modules moeten worden ingevoegd in alle ongebruikte sleuven.</span><span class="sxs-lookup"><span data-stu-id="21029-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="21029-111">Hallo behuizing cool niet goed als een site wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="21029-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="21029-112">Hallo EBOD controller hot verwisselbare is en kan worden verwijderd of vervangen.</span><span class="sxs-lookup"><span data-stu-id="21029-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="21029-113">Verwijder een mislukte module niet totdat u een vervangende hebt.</span><span class="sxs-lookup"><span data-stu-id="21029-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="21029-114">Wanneer u een proces voor het vervangen van Hallo initieert, moet u deze voltooit binnen 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="21029-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21029-115">Voordat u probeert tooremove of vervangen van een StorSimple-onderdeel, zorg ervoor dat u wordt aangeraden Hallo [veiligheid pictogram conventies](storsimple-safety.md#safety-icon-conventions) en andere [voorzorgsmaatregelen](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="21029-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="21029-116">Een controller EBOD verwijderen</span><span class="sxs-lookup"><span data-stu-id="21029-116">Remove an EBOD controller</span></span>
<span data-ttu-id="21029-117">Voordat vervangen Hallo EBOD controllermodule in uw StorSimple-apparaat mislukt, controleert u of die Hallo andere EBOD controller-module is actief en wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="21029-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="21029-118">Hallo volgende procedure en tabel wordt uitgelegd hoe tooremove Hallo EBOD controllermodule.</span><span class="sxs-lookup"><span data-stu-id="21029-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="21029-119">een module EBOD tooremove</span><span class="sxs-lookup"><span data-stu-id="21029-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="21029-120">Open hello klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="21029-120">Open hello Azure classic portal.</span></span>
2. <span data-ttu-id="21029-121">Navigeer te**apparaten** > **onderhoud** > **hardwarestatus**, en controleer of dat de status Hallo Hallo geleid voor actieve EBOD Hallo Controllermodule groen is en Hallo LED voor Hallo mislukt EBOD controllermodule is rood.</span><span class="sxs-lookup"><span data-stu-id="21029-121">Navigate too**Devices** > **Maintenance** > **Hardware Status**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="21029-122">Zoek Hallo mislukt EBOD controllermodule op Hallo achterzijde Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="21029-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="21029-123">Hallo-kabels die verbinding maken met Hallo EBOD controller module toohello domeincontroller alvorens Hallo EBOD module buiten het Hallo-systeem worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="21029-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="21029-124">Noteer Hallo exacte SAS-poort van Hallo EBOD controllermodule die verbonden toohello controller is.</span><span class="sxs-lookup"><span data-stu-id="21029-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="21029-125">U zult vereist toorestore Hallo systeemconfiguratie toothis nadat u Hallo EBOD module vervangen.</span><span class="sxs-lookup"><span data-stu-id="21029-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="21029-126">Normaal gesproken is dit poort A, die wordt aangeduid als **worden gehost in** in het volgende diagram Hallo.</span><span class="sxs-lookup"><span data-stu-id="21029-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   > 
   > 
   
    ![Backplane van EBOD-controller](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="21029-128">**Afbeelding 1** EBOD van Back-module</span><span class="sxs-lookup"><span data-stu-id="21029-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="21029-129">Label</span><span class="sxs-lookup"><span data-stu-id="21029-129">Label</span></span> | <span data-ttu-id="21029-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="21029-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="21029-131">1</span><span class="sxs-lookup"><span data-stu-id="21029-131">1</span></span> |<span data-ttu-id="21029-132">Fout met betrekking tot LED</span><span class="sxs-lookup"><span data-stu-id="21029-132">Fault LED</span></span> |
   | <span data-ttu-id="21029-133">2</span><span class="sxs-lookup"><span data-stu-id="21029-133">2</span></span> |<span data-ttu-id="21029-134">Power LED</span><span class="sxs-lookup"><span data-stu-id="21029-134">Power LED</span></span> |
   | <span data-ttu-id="21029-135">3</span><span class="sxs-lookup"><span data-stu-id="21029-135">3</span></span> |<span data-ttu-id="21029-136">SAS-connectors</span><span class="sxs-lookup"><span data-stu-id="21029-136">SAS connectors</span></span> |
   | <span data-ttu-id="21029-137">4</span><span class="sxs-lookup"><span data-stu-id="21029-137">4</span></span> |<span data-ttu-id="21029-138">SAS LED 's</span><span class="sxs-lookup"><span data-stu-id="21029-138">SAS LEDs</span></span> |
   | <span data-ttu-id="21029-139">5</span><span class="sxs-lookup"><span data-stu-id="21029-139">5</span></span> |<span data-ttu-id="21029-140">Seriële poorten factory alleen voor gebruik</span><span class="sxs-lookup"><span data-stu-id="21029-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="21029-141">6</span><span class="sxs-lookup"><span data-stu-id="21029-141">6</span></span> |<span data-ttu-id="21029-142">Poort (Host in)</span><span class="sxs-lookup"><span data-stu-id="21029-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="21029-143">7</span><span class="sxs-lookup"><span data-stu-id="21029-143">7</span></span> |<span data-ttu-id="21029-144">Poort B (Host out)</span><span class="sxs-lookup"><span data-stu-id="21029-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="21029-145">8</span><span class="sxs-lookup"><span data-stu-id="21029-145">8</span></span> |<span data-ttu-id="21029-146">Poort C (alleen Factory gebruik)</span><span class="sxs-lookup"><span data-stu-id="21029-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="21029-147">Een nieuwe EBOD controller installeren</span><span class="sxs-lookup"><span data-stu-id="21029-147">Install a new EBOD controller</span></span>
<span data-ttu-id="21029-148">Hallo volgende procedure en tabel wordt uitgelegd hoe tooinstall een module van de domeincontroller EBOD in uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="21029-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="21029-149">een controller EBOD tooinstall</span><span class="sxs-lookup"><span data-stu-id="21029-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="21029-150">Controleer Hallo EBOD apparaat voor schade, met name toohello interface connector.</span><span class="sxs-lookup"><span data-stu-id="21029-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="21029-151">Installeer geen Hallo nieuwe EBOD domeincontroller als een pincodes verbogen zijn.</span><span class="sxs-lookup"><span data-stu-id="21029-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="21029-152">Met de Hallo vergrendelingen in Hallo openen positie, dia Hallo module in Hallo behuizing totdat Hallo vergrendelingen benaderen.</span><span class="sxs-lookup"><span data-stu-id="21029-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![EBOD controller installeren](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="21029-154">**Afbeelding 2** installeren Hallo EBOD controllermodule</span><span class="sxs-lookup"><span data-stu-id="21029-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="21029-155">Sluit Hallo-vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="21029-155">Close hello latch.</span></span> <span data-ttu-id="21029-156">U moet een klik horen als Hallo vergrendeling stelt.</span><span class="sxs-lookup"><span data-stu-id="21029-156">You should hear a click as hello latch engages.</span></span>
   
    ![Vrijgeven van EBOD vergrendeling](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="21029-158">**Afbeelding 3** hello EBOD module vergrendeling sluiten</span><span class="sxs-lookup"><span data-stu-id="21029-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="21029-159">Hallo kabels verbinden.</span><span class="sxs-lookup"><span data-stu-id="21029-159">Reconnect hello cables.</span></span> <span data-ttu-id="21029-160">Hallo exacte configuratie die voordat de vervangende hello was gebruiken.</span><span class="sxs-lookup"><span data-stu-id="21029-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="21029-161">Zie volgende diagram Hallo en tabel voor meer informatie over het tooconnect Hallo kabels.</span><span class="sxs-lookup"><span data-stu-id="21029-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Uw apparaat 4U voor power bekabelen](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="21029-163">**Afbeelding 4**.</span><span class="sxs-lookup"><span data-stu-id="21029-163">**Figure 4**.</span></span> <span data-ttu-id="21029-164">Opnieuw verbinding te maken kabels</span><span class="sxs-lookup"><span data-stu-id="21029-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="21029-165">Label</span><span class="sxs-lookup"><span data-stu-id="21029-165">Label</span></span> | <span data-ttu-id="21029-166">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="21029-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="21029-167">1</span><span class="sxs-lookup"><span data-stu-id="21029-167">1</span></span> |<span data-ttu-id="21029-168">Primaire behuizing</span><span class="sxs-lookup"><span data-stu-id="21029-168">Primary enclosure</span></span> |
   | <span data-ttu-id="21029-169">2</span><span class="sxs-lookup"><span data-stu-id="21029-169">2</span></span> |<span data-ttu-id="21029-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="21029-170">PCM 0</span></span> |
   | <span data-ttu-id="21029-171">3</span><span class="sxs-lookup"><span data-stu-id="21029-171">3</span></span> |<span data-ttu-id="21029-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="21029-172">PCM 1</span></span> |
   | <span data-ttu-id="21029-173">4</span><span class="sxs-lookup"><span data-stu-id="21029-173">4</span></span> |<span data-ttu-id="21029-174">Controller 0</span><span class="sxs-lookup"><span data-stu-id="21029-174">Controller 0</span></span> |
   | <span data-ttu-id="21029-175">5</span><span class="sxs-lookup"><span data-stu-id="21029-175">5</span></span> |<span data-ttu-id="21029-176">Controller 1</span><span class="sxs-lookup"><span data-stu-id="21029-176">Controller 1</span></span> |
   | <span data-ttu-id="21029-177">6</span><span class="sxs-lookup"><span data-stu-id="21029-177">6</span></span> |<span data-ttu-id="21029-178">EBOD-controller 0</span><span class="sxs-lookup"><span data-stu-id="21029-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="21029-179">7</span><span class="sxs-lookup"><span data-stu-id="21029-179">7</span></span> |<span data-ttu-id="21029-180">EBOD controller 1</span><span class="sxs-lookup"><span data-stu-id="21029-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="21029-181">8</span><span class="sxs-lookup"><span data-stu-id="21029-181">8</span></span> |<span data-ttu-id="21029-182">EBOD behuizing</span><span class="sxs-lookup"><span data-stu-id="21029-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="21029-183">9</span><span class="sxs-lookup"><span data-stu-id="21029-183">9</span></span> |<span data-ttu-id="21029-184">Power Distribution Units</span><span class="sxs-lookup"><span data-stu-id="21029-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21029-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="21029-185">Next steps</span></span>
<span data-ttu-id="21029-186">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="21029-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

