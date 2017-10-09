---
title: aaaReplace een harde schijf op een StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe tooreplace een schijf station op een primaire behuizing StorSimple of een EBOD behuizing.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="0f547-103">Vervangen van een harde schijf op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="0f547-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="0f547-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0f547-104">Overview</span></span>
<span data-ttu-id="0f547-105">Deze zelfstudie wordt uitgelegd hoe u kunt verwijderen en vervangen door een slecht werkende of mislukte harde schijf op een Microsoft Azure StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="0f547-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="0f547-106">tooreplace een harde schijf, moet u:</span><span class="sxs-lookup"><span data-stu-id="0f547-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="0f547-107">Werking stellen Hallo antitamper vergrendelen</span><span class="sxs-lookup"><span data-stu-id="0f547-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="0f547-108">Hallo-schijfstation verwijderen</span><span class="sxs-lookup"><span data-stu-id="0f547-108">Remove hello disk drive</span></span>
* <span data-ttu-id="0f547-109">Hallo vervangende schijf installeren</span><span class="sxs-lookup"><span data-stu-id="0f547-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f547-110">Voordat verwijderen en een schijf vervangen Lees Hallo veiligheidsinformatie in [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="0f547-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="0f547-111">Werking stellen Hallo antitamper vergrendelen</span><span class="sxs-lookup"><span data-stu-id="0f547-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="0f547-112">Deze procedure wordt uitgelegd hoe Hallo antitamper vergrendelingen voor uw StorSimple-apparaat kunnen worden in- of uitgeschakeld wanneer u de schijfstations Hallo vervangt.</span><span class="sxs-lookup"><span data-stu-id="0f547-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="0f547-113">Hallo antitamper vergrendelingen zijn aangebracht in Hallo station carrier verwerkt en ze toegankelijk zijn via een kleine opening in Hallo vergrendeling sectie van Hallo-ingang.</span><span class="sxs-lookup"><span data-stu-id="0f547-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="0f547-114">Schijven worden geleverd met Hallo vergrendelingen set toohello vergrendeld positie.</span><span class="sxs-lookup"><span data-stu-id="0f547-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="0f547-115">toounlock hello antitamper vergrendelen</span><span class="sxs-lookup"><span data-stu-id="0f547-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="0f547-116">Hallo lock-toets (een 'tamperproof' T10 draai die Microsoft opgegeven) zorgvuldig invoegen in Hallo opening in ingang hello en in een socket.</span><span class="sxs-lookup"><span data-stu-id="0f547-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0f547-117">Als Hallo antitamper lock is geactiveerd, is Hallo rode indicator zichtbaar in Hallo opening.</span><span class="sxs-lookup"><span data-stu-id="0f547-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
   > 
   > 
   
    ![Vergrendelde schijfstation](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="0f547-119">**Afbeelding 1** antivirusprogramma draagbare vergrendeling is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="0f547-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="0f547-120">Label</span><span class="sxs-lookup"><span data-stu-id="0f547-120">Label</span></span> | <span data-ttu-id="0f547-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0f547-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0f547-122">1</span><span class="sxs-lookup"><span data-stu-id="0f547-122">1</span></span> |<span data-ttu-id="0f547-123">Indicator opening</span><span class="sxs-lookup"><span data-stu-id="0f547-123">Indicator aperture</span></span> |
   | <span data-ttu-id="0f547-124">2</span><span class="sxs-lookup"><span data-stu-id="0f547-124">2</span></span> |<span data-ttu-id="0f547-125">Antitamper vergrendelen</span><span class="sxs-lookup"><span data-stu-id="0f547-125">Antitamper lock</span></span> |
2. <span data-ttu-id="0f547-126">Hallo-sleutel in een Linksomdraaiend richting draaien totdat Hallo rode indicator niet zichtbaar in Hallo opening hierboven Hallo-sleutel is.</span><span class="sxs-lookup"><span data-stu-id="0f547-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="0f547-127">Hallo sleutel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="0f547-127">Remove hello key.</span></span>
   
    ![Niet-vergrendelde schijfstation](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="0f547-129">**Afbeelding 2** ontgrendeld harde schijf</span><span class="sxs-lookup"><span data-stu-id="0f547-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="0f547-130">Hallo-schijfstation kunnen nu worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0f547-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="0f547-131">Volg de stappen Hallo in omgekeerde tooengage Hallo vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="0f547-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="0f547-132">Hallo-schijfstation verwijderen</span><span class="sxs-lookup"><span data-stu-id="0f547-132">Remove hello disk drive</span></span>
<span data-ttu-id="0f547-133">Uw StorSimple-apparaat ondersteunt een RAID 10-achtige spaties opslagconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="0f547-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="0f547-134">Dit betekent dat het normaal gesproken met een mislukte schijf SSD-schijf (SSD werken kan) of harde schijf drive (HDD).</span><span class="sxs-lookup"><span data-stu-id="0f547-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="0f547-135">Als uw systeem meer dan één niet-werkende schijf heeft, verwijder niet meer dan één SSD of harde schijf van Hallo systeem op elk gewenst moment in de tijd.</span><span class="sxs-lookup"><span data-stu-id="0f547-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="0f547-136">Dit kan leiden tot verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="0f547-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="0f547-137">Zorg ervoor dat u een vervangende SSD plaatsen in een sleuf dat eerder een SSD bevatte.</span><span class="sxs-lookup"><span data-stu-id="0f547-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="0f547-138">Plaats een vervangende harde schijf op dezelfde manier in een sleuf dat eerder een harde schijf bevatte.</span><span class="sxs-lookup"><span data-stu-id="0f547-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="0f547-139">Sleuven zijn in de klassieke Azure-portal hello, genummerd van 0 – 11.</span><span class="sxs-lookup"><span data-stu-id="0f547-139">In hello Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="0f547-140">Daarom als Hallo portal ziet u een schijf in de sleuf 2 is mislukt, op Hallo apparaat zoekt Hallo defecte schijf in de derde sleuf Hallo van Hallo boven links.</span><span class="sxs-lookup"><span data-stu-id="0f547-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="0f547-141">Schijven worden verwijderd en vervangen tijdens het Hallo-systeem werkt.</span><span class="sxs-lookup"><span data-stu-id="0f547-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="0f547-142">een station tooremove</span><span class="sxs-lookup"><span data-stu-id="0f547-142">tooremove a drive</span></span>
1. <span data-ttu-id="0f547-143">tooidentify Hallo van niet-werkende schijf, in Hallo klassieke Azure-portal, gaat u te**apparaten** > **onderhoud** > **hardwarestatus**.</span><span class="sxs-lookup"><span data-stu-id="0f547-143">tooidentify hello failed disk, in hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="0f547-144">Omdat een schijf kan niet in de primaire behuizing Hallo en/of in een behuizing EBOD (als u van een model 8600 gebruikmaakt), Hallo status van schijven Hallo onder bekijken **gedeelde onderdelen** en klikt u onder **EBOD behuizing gedeelde onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="0f547-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="0f547-145">Een niet-werkende schijf in de behuizing worden weergegeven met een rode status.</span><span class="sxs-lookup"><span data-stu-id="0f547-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="0f547-146">Hallo-stations vinden in Hallo voorzijde van primaire behuizing Hallo of Hallo EBOD behuizing.</span><span class="sxs-lookup"><span data-stu-id="0f547-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="0f547-147">Als het Hallo-schijf is ontgrendeld, gaat u verder toohello volgende stap.</span><span class="sxs-lookup"><span data-stu-id="0f547-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="0f547-148">Als het Hallo-schijf is vergrendeld, deze ontgrendelen met na Hallo-procedure in [werking stellen Hallo antitamper vergrendeling](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="0f547-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="0f547-149">Druk op Hallo zwart vergrendelingen op Hallo station carrier module en pull-hallo station carrier ingang af en opslag van Hallo voor van Hallo chassis.</span><span class="sxs-lookup"><span data-stu-id="0f547-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span> 
   
    ![Schijfstation ingang vrijgeven](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="0f547-151">**Afbeelding 3** vrijgeven Hallo station ingang</span><span class="sxs-lookup"><span data-stu-id="0f547-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="0f547-152">Wanneer Hallo station carrier ingang volledig is uitgebreid, schuift u Hallo station carrier buiten het Hallo-chassis.</span><span class="sxs-lookup"><span data-stu-id="0f547-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Schijf buiten het schijfstation Verschuivend](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="0f547-154">**Afbeelding 4** Verschuivend Hallo schijfstation buiten het Hallo-provider</span><span class="sxs-lookup"><span data-stu-id="0f547-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="0f547-155">Hallo vervangende schijf installeren</span><span class="sxs-lookup"><span data-stu-id="0f547-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="0f547-156">Nadat een station in uw StorSimple-apparaat is mislukt en u deze hebt verwijderd, voert u deze procedure tooreplace deze met een nieuwe schijf.</span><span class="sxs-lookup"><span data-stu-id="0f547-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="0f547-157">een station tooinsert</span><span class="sxs-lookup"><span data-stu-id="0f547-157">tooinsert a drive</span></span>
1. <span data-ttu-id="0f547-158">Zorg ervoor dat Hallo station carrier ingang volledig is uitgebreid, zoals wordt weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="0f547-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![Harde schijf met de ingang uitgebreid](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="0f547-160">**Afbeelding 5** station met de ingang uitgebreid</span><span class="sxs-lookup"><span data-stu-id="0f547-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="0f547-161">Schuif Hallo station carrier alle Hallo manier in Hallo chassis.</span><span class="sxs-lookup"><span data-stu-id="0f547-161">Slide hello drive carrier all hello way into hello chassis.</span></span> 
   
    ![Schijf naar schijf carrier Verschuivend](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="0f547-163">**Afbeelding 6** schuifregelaar Hallo station carrier in Hallo-chassis</span><span class="sxs-lookup"><span data-stu-id="0f547-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="0f547-164">Met de Hallo station carrier aanwezig is, sluit Hallo station carrier ingang tijdens de bewerking wordt voortgezet toopush Hallo station carrier in Hallo chassis, tot Hallo station carrier ingang in een vergrendelde positie is uitgelijnd.</span><span class="sxs-lookup"><span data-stu-id="0f547-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="0f547-165">Hallo vergrendeling sleutel gebruiken die werd geleverd door Microsoft (tamperproof Torx draai) toosecure Hallo carrier ingang naar de juiste plaats door in te schakelen Hallo vergrendeling installatie inschakelen van een kwartaal rechtsom.</span><span class="sxs-lookup"><span data-stu-id="0f547-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="0f547-166">Controleer of Hallo vervanging is geslaagd en Hallo station op Hallo klassieke Azure-portal te openen en te navigeren operationele is**onderhoud** > **hardwarestatus**.</span><span class="sxs-lookup"><span data-stu-id="0f547-166">Verify that hello replacement was successful and hello drive is operational by accessing hello Azure classic portal and navigating too**Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="0f547-167">Onder **gedeelde onderdelen** of **EBOD behuizing gedeelde onderdelen**, moet de Hallo stationsstatus groen is, die aangeeft of dit in orde is.</span><span class="sxs-lookup"><span data-stu-id="0f547-167">Under **Shared Components** or **EBOD enclosure Shared Components**, hello drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0f547-168">Het kan enkele uren duren voordat Hallo schijf status tooturn groen na Hallo vervanging.</span><span class="sxs-lookup"><span data-stu-id="0f547-168">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="0f547-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0f547-169">Next steps</span></span>
<span data-ttu-id="0f547-170">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="0f547-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

