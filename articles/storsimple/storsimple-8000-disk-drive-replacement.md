---
title: Vervangen van een harde schijf op een apparaat van de serie StorSimple 8000 | Microsoft Docs
description: Legt uit hoe u een harde schijf op een primaire behuizing StorSimple of een behuizing EBOD vervangen.
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
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: bb259b626ecd4dcbaa8f1c465f1ece4516aa8881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="3179a-103">Vervangen van een harde schijf op uw StorSimple 8000 series apparaat</span><span class="sxs-lookup"><span data-stu-id="3179a-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="3179a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3179a-104">Overview</span></span>
<span data-ttu-id="3179a-105">Deze zelfstudie wordt uitgelegd hoe u kunt verwijderen en vervangen door een slecht werkende of mislukte harde schijf op een Microsoft Azure StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="3179a-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="3179a-106">Ter vervanging van een harde schijf, moet u:</span><span class="sxs-lookup"><span data-stu-id="3179a-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="3179a-107">Werking stellen van de antitamper vergrendeling</span><span class="sxs-lookup"><span data-stu-id="3179a-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="3179a-108">De schijf verwijderen</span><span class="sxs-lookup"><span data-stu-id="3179a-108">Remove the disk drive</span></span>
* <span data-ttu-id="3179a-109">De vervangende schijf installeren</span><span class="sxs-lookup"><span data-stu-id="3179a-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3179a-110">Voordat verwijderen en een schijf vervangen Lees de veiligheidsinformatie in [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="3179a-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="3179a-111">Werking stellen van de antitamper vergrendeling</span><span class="sxs-lookup"><span data-stu-id="3179a-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="3179a-112">Deze procedure wordt uitgelegd hoe de antitamper vergrendelingen op uw StorSimple-apparaat kunnen worden in- of uitgeschakeld wanneer u de schijfstations vervangt.</span><span class="sxs-lookup"><span data-stu-id="3179a-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="3179a-113">De antitamper vergrendelingen zijn aangebracht in het station carrier verwerkt en ze toegankelijk zijn via een kleine opening in de sectie vergrendeling van de greep.</span><span class="sxs-lookup"><span data-stu-id="3179a-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="3179a-114">Schijven worden geleverd met vergrendelingen zijn ingesteld op de vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="3179a-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="3179a-115">Voor het ontgrendelen van de antitamper vergrendeling</span><span class="sxs-lookup"><span data-stu-id="3179a-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="3179a-116">In de ruimte in de greep en in een socket, invoegen zorgvuldig de LOCK (een 'tamperproof' T10 draai die Microsoft opgegeven).</span><span class="sxs-lookup"><span data-stu-id="3179a-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   <span data-ttu-id="3179a-117">Als de antitamper vergrendeling is geactiveerd, is de rode indicator is zichtbaar in de ruimte.</span><span class="sxs-lookup"><span data-stu-id="3179a-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
  
    ![Vergrendelde schijfstation](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="3179a-119">**Afbeelding 1** antivirusprogramma draagbare vergrendeling is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="3179a-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="3179a-120">Label</span><span class="sxs-lookup"><span data-stu-id="3179a-120">Label</span></span> | <span data-ttu-id="3179a-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3179a-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="3179a-122">1</span><span class="sxs-lookup"><span data-stu-id="3179a-122">1</span></span> |<span data-ttu-id="3179a-123">Indicator opening</span><span class="sxs-lookup"><span data-stu-id="3179a-123">Indicator aperture</span></span> |
   | <span data-ttu-id="3179a-124">2</span><span class="sxs-lookup"><span data-stu-id="3179a-124">2</span></span> |<span data-ttu-id="3179a-125">Antitamper vergrendelen</span><span class="sxs-lookup"><span data-stu-id="3179a-125">Antitamper lock</span></span> |
2. <span data-ttu-id="3179a-126">De sleutel in een Linksomdraaiend richting draaien totdat de rode indicator niet zichtbaar in de opening boven de sleutel is.</span><span class="sxs-lookup"><span data-stu-id="3179a-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="3179a-127">Verwijder de sleutel.</span><span class="sxs-lookup"><span data-stu-id="3179a-127">Remove the key.</span></span>
   
    ![Niet-vergrendelde schijfstation](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="3179a-129">**Afbeelding 2** ontgrendeld harde schijf</span><span class="sxs-lookup"><span data-stu-id="3179a-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="3179a-130">De harde schijf kan nu worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3179a-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="3179a-131">Volg de stappen in omgekeerde volgorde de vergrendeling bezighouden.</span><span class="sxs-lookup"><span data-stu-id="3179a-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="3179a-132">De schijf verwijderen</span><span class="sxs-lookup"><span data-stu-id="3179a-132">Remove the disk drive</span></span>
<span data-ttu-id="3179a-133">Uw StorSimple-apparaat ondersteunt een RAID 10-achtige spaties opslagconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="3179a-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="3179a-134">Dit betekent dat het normaal gesproken met een mislukte schijf SSD-schijf (SSD werken kan) of harde schijf drive (HDD).</span><span class="sxs-lookup"><span data-stu-id="3179a-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="3179a-135">Als uw systeem meer dan één niet-werkende schijf heeft, verwijder niet meer dan één SSD of harde schijf uit het systeem op elk punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="3179a-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="3179a-136">Dit kan leiden tot verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="3179a-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="3179a-137">Zorg ervoor dat u een vervangende SSD plaatsen in een sleuf dat eerder een SSD bevatte.</span><span class="sxs-lookup"><span data-stu-id="3179a-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="3179a-138">Plaats een vervangende harde schijf op dezelfde manier in een sleuf dat eerder een harde schijf bevatte.</span><span class="sxs-lookup"><span data-stu-id="3179a-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="3179a-139">Sleuven zijn in de Azure portal genummerd van 0 – 11.</span><span class="sxs-lookup"><span data-stu-id="3179a-139">In the Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="3179a-140">Daarom als de portal ziet u een schijf in de sleuf 2 is mislukt, op het apparaat, zoekt de defecte schijf in de derde sleuf vanaf de bovenkant links.</span><span class="sxs-lookup"><span data-stu-id="3179a-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="3179a-141">Schijven worden verwijderd en vervangen terwijl het systeem werkt.</span><span class="sxs-lookup"><span data-stu-id="3179a-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="3179a-142">Een station verwijderen</span><span class="sxs-lookup"><span data-stu-id="3179a-142">To remove a drive</span></span>
1. <span data-ttu-id="3179a-143">Om te identificeren van de defecte schijf, in de Azure portal, gaat u naar het apparaat **instellingen > Hardware health**.</span><span class="sxs-lookup"><span data-stu-id="3179a-143">To identify the failed disk, in the Azure portal, go to your device **Settings > Hardware health**.</span></span> <span data-ttu-id="3179a-144">Omdat een schijf kan niet in de primaire behuizing en/of een behuizing EBOD (als u van een model 8600 gebruikmaakt), kijk naar de status van de schijven onder **gedeelde onderdelen** en klikt u onder **EBOD gedeelde onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="3179a-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="3179a-145">Een niet-werkende schijf in de behuizing worden weergegeven met een rode status.</span><span class="sxs-lookup"><span data-stu-id="3179a-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="3179a-146">Zoek de stations vooraan in de primaire behuizing of de EBOD behuizing.</span><span class="sxs-lookup"><span data-stu-id="3179a-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="3179a-147">Als de schijf ontgrendeld is, gaat u verder met de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="3179a-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="3179a-148">Als de schijf is vergrendeld, ontgrendelt u het via de volgende procedure in [werking stellen van de vergrendeling antitamper](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="3179a-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="3179a-149">Druk op de zwarte vergrendeling op de schijf carrier module en pull-de ingang van station carrier af en opslag van het begin van het chassis.</span><span class="sxs-lookup"><span data-stu-id="3179a-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span>
   
    ![Schijfstation ingang vrijgeven](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="3179a-151">**Afbeelding 3** vrijgave van de ingang station</span><span class="sxs-lookup"><span data-stu-id="3179a-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="3179a-152">Wanneer de ingang van de provider station volledig is uitgebreid, schuif de drager station buiten het chassis.</span><span class="sxs-lookup"><span data-stu-id="3179a-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Schijf buiten het schijfstation Verschuivend](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="3179a-154">**Afbeelding 4** Verschuivend het schijfstation buiten de provider</span><span class="sxs-lookup"><span data-stu-id="3179a-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="3179a-155">De vervangende schijf installeren</span><span class="sxs-lookup"><span data-stu-id="3179a-155">Install the replacement disk drive</span></span>
<span data-ttu-id="3179a-156">Wanneer een station in uw StorSimple-apparaat is mislukt en u deze hebt verwijderd, volgt u deze procedure wilt vervangen door een nieuwe schijf.</span><span class="sxs-lookup"><span data-stu-id="3179a-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="3179a-157">Invoegen van een station</span><span class="sxs-lookup"><span data-stu-id="3179a-157">To insert a drive</span></span>
1. <span data-ttu-id="3179a-158">Zorg ervoor dat de ingang van de provider station volledig is uitgebreid, zoals wordt weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="3179a-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![Harde schijf met de ingang uitgebreid](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="3179a-160">**Afbeelding 5** station met de ingang uitgebreid</span><span class="sxs-lookup"><span data-stu-id="3179a-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="3179a-161">De provider station de schuifregelaar helemaal in het chassis.</span><span class="sxs-lookup"><span data-stu-id="3179a-161">Slide the drive carrier all the way into the chassis.</span></span>
   
    ![Schijf naar schijf carrier Verschuivend](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="3179a-163">**Afbeelding 6** Verschuivend de station-provider in het chassis</span><span class="sxs-lookup"><span data-stu-id="3179a-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="3179a-164">Met de drager station is geplaatst, sluit u de ingang van station carrier terwijl u de provider station in het chassis push totdat de schijf carrier ingang in een vergrendelde positie uitlijnen.</span><span class="sxs-lookup"><span data-stu-id="3179a-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="3179a-165">Gebruik de LOCK die werd geleverd door Microsoft (tamperproof Torx draai) de ingang carrier op hun plaats door in te schakelen de installatie van de vergrendeling inschakelen van een kwartaal rechtsom.</span><span class="sxs-lookup"><span data-stu-id="3179a-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="3179a-166">Controleer of de vervanging is gelukt en het station operationeel is.</span><span class="sxs-lookup"><span data-stu-id="3179a-166">Verify that the replacement was successful and the drive is operational.</span></span> <span data-ttu-id="3179a-167">Toegang tot de Azure-portal en navigeer naar **instellingen** > **Hardware health**.</span><span class="sxs-lookup"><span data-stu-id="3179a-167">Access the Azure portal and navigate to **Settings** > **Hardware health**.</span></span> <span data-ttu-id="3179a-168">Onder **gedeelde onderdelen** of **EBOD gedeelde onderdelen**, de stationsstatus moet groen, die aangeeft of dit in orde is.</span><span class="sxs-lookup"><span data-stu-id="3179a-168">Under **Shared components** or **EBOD shared components**, the drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="3179a-169">Het duurt enkele uren groen inschakelen na de vervanging van de schijfstatus van de.</span><span class="sxs-lookup"><span data-stu-id="3179a-169">It may take several hours for the disk status to turn green after the replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="3179a-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3179a-170">Next steps</span></span>
<span data-ttu-id="3179a-171">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="3179a-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

