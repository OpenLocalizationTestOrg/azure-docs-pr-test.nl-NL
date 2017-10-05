---
title: Vervangen van een domeincontroller StorSimple EBOD | Microsoft Docs
description: Legt uit hoe verwijdert en vervangt u een of beide EBOD domeincontrollers op een StorSimple 8600-apparaat.
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
ms.openlocfilehash: 23d819ddc3bbcbaf2847cdcc9191407ead0ff43d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="21206-103">Vervangen van een domeincontroller EBOD op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="21206-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="21206-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="21206-104">Overview</span></span>
<span data-ttu-id="21206-105">Deze zelfstudie wordt uitgelegd hoe ter vervanging van een defecte EBOD controllermodule op uw Microsoft Azure StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="21206-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="21206-106">Ter vervanging van een module van de domeincontroller EBOD, moet u:</span><span class="sxs-lookup"><span data-stu-id="21206-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="21206-107">De defecte EBOD controller verwijderen</span><span class="sxs-lookup"><span data-stu-id="21206-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="21206-108">Een nieuwe EBOD controller installeren</span><span class="sxs-lookup"><span data-stu-id="21206-108">Install a new EBOD controller</span></span>

<span data-ttu-id="21206-109">Houd rekening met de volgende informatie voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="21206-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="21206-110">Lege EBOD modules moeten worden ingevoegd in alle ongebruikte sleuven.</span><span class="sxs-lookup"><span data-stu-id="21206-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="21206-111">De behuizing cool niet goed als een site wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="21206-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="21206-112">De controller EBOD hot verwisselbare is en kan worden verwijderd of vervangen.</span><span class="sxs-lookup"><span data-stu-id="21206-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="21206-113">Verwijder een mislukte module niet totdat u een vervangende hebt.</span><span class="sxs-lookup"><span data-stu-id="21206-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="21206-114">Wanneer u het proces voor het vervangen start, moet u deze voltooit binnen 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="21206-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21206-115">Voordat u probeert te verwijderen of vervangen van een StorSimple-onderdeel, zorg ervoor dat u wordt aangeraden de [veiligheid pictogram conventies](storsimple-safety.md#safety-icon-conventions) en andere [voorzorgsmaatregelen](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="21206-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="21206-116">Een controller EBOD verwijderen</span><span class="sxs-lookup"><span data-stu-id="21206-116">Remove an EBOD controller</span></span>
<span data-ttu-id="21206-117">Zorg dat de andere EBOD controller-module actief en wordt uitgevoerd is voordat de mislukte EBOD controllermodule in uw StorSimple-apparaat kan worden vervangen.</span><span class="sxs-lookup"><span data-stu-id="21206-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="21206-118">De volgende procedure en tabel wordt uitgelegd hoe de controller EBOD module verwijderen.</span><span class="sxs-lookup"><span data-stu-id="21206-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="21206-119">Een module EBOD verwijderen</span><span class="sxs-lookup"><span data-stu-id="21206-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="21206-120">Open de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="21206-120">Open the Azure classic portal.</span></span>
2. <span data-ttu-id="21206-121">Navigeer naar **apparaten** > **onderhoud** > **hardwarestatus**, en controleer of de status van de LED voor de actieve EBOD-controller module groen is en de LED voor de mislukte EBOD controller-module is rood.</span><span class="sxs-lookup"><span data-stu-id="21206-121">Navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="21206-122">Zoek de mislukte EBOD controllermodule aan het einde van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="21206-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="21206-123">Verwijder de kabels die verbinding maken met de module van de domeincontroller EBOD de domeincontroller voordat u de module EBOD buiten het systeem.</span><span class="sxs-lookup"><span data-stu-id="21206-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="21206-124">Noteer de precieze SAS-poort van de module die EBOD domeincontroller die is verbonden met de domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="21206-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="21206-125">U moet het systeem herstellen naar deze configuratie nadat u de module EBOD vervangen.</span><span class="sxs-lookup"><span data-stu-id="21206-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="21206-126">Normaal gesproken is dit poort A, die wordt aangeduid als **worden gehost in** in het volgende diagram.</span><span class="sxs-lookup"><span data-stu-id="21206-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   > 
   > 
   
    ![Backplane van EBOD-controller](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="21206-128">**Afbeelding 1** EBOD van Back-module</span><span class="sxs-lookup"><span data-stu-id="21206-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="21206-129">Label</span><span class="sxs-lookup"><span data-stu-id="21206-129">Label</span></span> | <span data-ttu-id="21206-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="21206-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="21206-131">1</span><span class="sxs-lookup"><span data-stu-id="21206-131">1</span></span> |<span data-ttu-id="21206-132">Fout met betrekking tot LED</span><span class="sxs-lookup"><span data-stu-id="21206-132">Fault LED</span></span> |
   | <span data-ttu-id="21206-133">2</span><span class="sxs-lookup"><span data-stu-id="21206-133">2</span></span> |<span data-ttu-id="21206-134">Power LED</span><span class="sxs-lookup"><span data-stu-id="21206-134">Power LED</span></span> |
   | <span data-ttu-id="21206-135">3</span><span class="sxs-lookup"><span data-stu-id="21206-135">3</span></span> |<span data-ttu-id="21206-136">SAS-connectors</span><span class="sxs-lookup"><span data-stu-id="21206-136">SAS connectors</span></span> |
   | <span data-ttu-id="21206-137">4</span><span class="sxs-lookup"><span data-stu-id="21206-137">4</span></span> |<span data-ttu-id="21206-138">SAS LED 's</span><span class="sxs-lookup"><span data-stu-id="21206-138">SAS LEDs</span></span> |
   | <span data-ttu-id="21206-139">5</span><span class="sxs-lookup"><span data-stu-id="21206-139">5</span></span> |<span data-ttu-id="21206-140">Seriële poorten factory alleen voor gebruik</span><span class="sxs-lookup"><span data-stu-id="21206-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="21206-141">6</span><span class="sxs-lookup"><span data-stu-id="21206-141">6</span></span> |<span data-ttu-id="21206-142">Poort (Host in)</span><span class="sxs-lookup"><span data-stu-id="21206-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="21206-143">7</span><span class="sxs-lookup"><span data-stu-id="21206-143">7</span></span> |<span data-ttu-id="21206-144">Poort B (Host out)</span><span class="sxs-lookup"><span data-stu-id="21206-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="21206-145">8</span><span class="sxs-lookup"><span data-stu-id="21206-145">8</span></span> |<span data-ttu-id="21206-146">Poort C (alleen Factory gebruik)</span><span class="sxs-lookup"><span data-stu-id="21206-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="21206-147">Een nieuwe EBOD controller installeren</span><span class="sxs-lookup"><span data-stu-id="21206-147">Install a new EBOD controller</span></span>
<span data-ttu-id="21206-148">De volgende procedure en tabel wordt uitgelegd hoe u een domeincontroller EBOD module in uw StorSimple-apparaat installeert.</span><span class="sxs-lookup"><span data-stu-id="21206-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="21206-149">Een controller EBOD installeren</span><span class="sxs-lookup"><span data-stu-id="21206-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="21206-150">Controleer het apparaat EBOD voor schade, met name op de interface-connector.</span><span class="sxs-lookup"><span data-stu-id="21206-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="21206-151">Installeer de nieuwe EBOD controller niet als een pincodes verbogen zijn.</span><span class="sxs-lookup"><span data-stu-id="21206-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="21206-152">Schuif de module met de vergrendelingen in de open positie in de behuizing totdat de vergrendelingen benaderen.</span><span class="sxs-lookup"><span data-stu-id="21206-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![EBOD controller installeren](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="21206-154">**Afbeelding 2** de EBOD controller-module installeren</span><span class="sxs-lookup"><span data-stu-id="21206-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="21206-155">Sluit de vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="21206-155">Close the latch.</span></span> <span data-ttu-id="21206-156">U moet een klik horen als het slot stelt.</span><span class="sxs-lookup"><span data-stu-id="21206-156">You should hear a click as the latch engages.</span></span>
   
    ![Vrijgeven van EBOD vergrendeling](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="21206-158">**Afbeelding 3** sluiten van de module EBOD vergrendeling</span><span class="sxs-lookup"><span data-stu-id="21206-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="21206-159">Sluit de kabels.</span><span class="sxs-lookup"><span data-stu-id="21206-159">Reconnect the cables.</span></span> <span data-ttu-id="21206-160">Gebruik de exacte configuratie die aanwezig zijn voordat de vervangende was.</span><span class="sxs-lookup"><span data-stu-id="21206-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="21206-161">Zie het volgende diagram en de volgende tabel voor meer informatie over het aansluiten van de kabels.</span><span class="sxs-lookup"><span data-stu-id="21206-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![Uw apparaat 4U voor power bekabelen](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="21206-163">**Afbeelding 4**.</span><span class="sxs-lookup"><span data-stu-id="21206-163">**Figure 4**.</span></span> <span data-ttu-id="21206-164">Opnieuw verbinding te maken kabels</span><span class="sxs-lookup"><span data-stu-id="21206-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="21206-165">Label</span><span class="sxs-lookup"><span data-stu-id="21206-165">Label</span></span> | <span data-ttu-id="21206-166">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="21206-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="21206-167">1</span><span class="sxs-lookup"><span data-stu-id="21206-167">1</span></span> |<span data-ttu-id="21206-168">Primaire behuizing</span><span class="sxs-lookup"><span data-stu-id="21206-168">Primary enclosure</span></span> |
   | <span data-ttu-id="21206-169">2</span><span class="sxs-lookup"><span data-stu-id="21206-169">2</span></span> |<span data-ttu-id="21206-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="21206-170">PCM 0</span></span> |
   | <span data-ttu-id="21206-171">3</span><span class="sxs-lookup"><span data-stu-id="21206-171">3</span></span> |<span data-ttu-id="21206-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="21206-172">PCM 1</span></span> |
   | <span data-ttu-id="21206-173">4</span><span class="sxs-lookup"><span data-stu-id="21206-173">4</span></span> |<span data-ttu-id="21206-174">Controller 0</span><span class="sxs-lookup"><span data-stu-id="21206-174">Controller 0</span></span> |
   | <span data-ttu-id="21206-175">5</span><span class="sxs-lookup"><span data-stu-id="21206-175">5</span></span> |<span data-ttu-id="21206-176">Controller 1</span><span class="sxs-lookup"><span data-stu-id="21206-176">Controller 1</span></span> |
   | <span data-ttu-id="21206-177">6</span><span class="sxs-lookup"><span data-stu-id="21206-177">6</span></span> |<span data-ttu-id="21206-178">EBOD-controller 0</span><span class="sxs-lookup"><span data-stu-id="21206-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="21206-179">7</span><span class="sxs-lookup"><span data-stu-id="21206-179">7</span></span> |<span data-ttu-id="21206-180">EBOD controller 1</span><span class="sxs-lookup"><span data-stu-id="21206-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="21206-181">8</span><span class="sxs-lookup"><span data-stu-id="21206-181">8</span></span> |<span data-ttu-id="21206-182">EBOD behuizing</span><span class="sxs-lookup"><span data-stu-id="21206-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="21206-183">9</span><span class="sxs-lookup"><span data-stu-id="21206-183">9</span></span> |<span data-ttu-id="21206-184">Power Distribution Units</span><span class="sxs-lookup"><span data-stu-id="21206-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21206-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="21206-185">Next steps</span></span>
<span data-ttu-id="21206-186">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="21206-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

