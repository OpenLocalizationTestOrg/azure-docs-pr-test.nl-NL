---
title: Microsoft Azure StorSimple virtuele matrix back-zelfstudie | Microsoft Docs
description: Beschrijft hoe u back-up van virtuele StorSimple-matrix-shares en -volumes.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c926f0c80ce56cac3106ad97ec3ec2e18a8e2cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="16d4a-103">Back-up shares of volumes op uw virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="16d4a-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="16d4a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="16d4a-104">Overview</span></span>

<span data-ttu-id="16d4a-105">De virtuele StorSimple-matrix is een hybride cloud-opslag on-premises virtuele apparaat die kan worden geconfigureerd als een bestandsserver of een iSCSI-server.</span><span class="sxs-lookup"><span data-stu-id="16d4a-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="16d4a-106">De virtuele matrix kan de gebruiker geplande en handmatige back-ups van de shares of volumes maken op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="16d4a-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span></span> <span data-ttu-id="16d4a-107">Wanneer geconfigureerd als een bestandsserver, kunt u ook herstel op itemniveau.</span><span class="sxs-lookup"><span data-stu-id="16d4a-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="16d4a-108">Deze zelfstudie wordt beschreven hoe geplande en handmatige back-ups maken en herstel op itemniveau voor het herstellen van een verwijderd bestand op uw virtuele matrix uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="16d4a-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span></span>

<span data-ttu-id="16d4a-109">Deze zelfstudie geldt voor de StorSimple virtuele matrices alleen.</span><span class="sxs-lookup"><span data-stu-id="16d4a-109">This tutorial applies to the StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="16d4a-110">Voor informatie over 8000-serie, gaat u naar [een back-up voor 8000 series apparaat maken](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="16d4a-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="16d4a-111">Back-up-shares en -volumes</span><span class="sxs-lookup"><span data-stu-id="16d4a-111">Back up shares and volumes</span></span>

<span data-ttu-id="16d4a-112">Back-ups punt in tijd beveiliging bieden, verbeteren de herstelmogelijkheden en hersteltijden voor shares en -volumes te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="16d4a-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="16d4a-113">U kunt back-up een share of het volume op uw StorSimple-apparaat op twee manieren: **geplande** of **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="16d4a-114">Elk van de methoden wordt in de volgende secties besproken.</span><span class="sxs-lookup"><span data-stu-id="16d4a-114">Each of the methods is discussed in the following sections.</span></span>

## <a name="change-the-backup-start-time"></a><span data-ttu-id="16d4a-115">De begintijd voor back-ups wijzigen</span><span class="sxs-lookup"><span data-stu-id="16d4a-115">Change the backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="16d4a-116">In deze release worden geplande back-ups gemaakt door een standaardbeleid dat wordt dagelijks wordt uitgevoerd op een opgegeven periode zijn uitgevoerd en een back-up alle shares of volumes op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="16d4a-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="16d4a-117">Het is niet mogelijk te maken van aangepaste beleidsregels voor geplande back-ups op dit moment.</span><span class="sxs-lookup"><span data-stu-id="16d4a-117">It is not possible to create custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="16d4a-118">Uw virtuele StorSimple-matrix heeft een standaard back-upbeleid dat begint op een bepaald tijdstip van de dag (22.30) en een back-up alle shares of volumes op het apparaat eenmaal per dag.</span><span class="sxs-lookup"><span data-stu-id="16d4a-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="16d4a-119">U kunt de tijd waarop de back-up wordt gestart, maar de frequentie en de bewaarperiode (die geeft het aantal back-ups wilt behouden) kunnen niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="16d4a-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="16d4a-120">Tijdens deze back-ups, het virtuele apparaat voor volledige back-up.</span><span class="sxs-lookup"><span data-stu-id="16d4a-120">During these backups, the entire virtual device is backed up.</span></span> <span data-ttu-id="16d4a-121">Dit kan mogelijk invloed op de prestaties van het apparaat en van invloed zijn op de werkbelastingen die worden geïmplementeerd op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="16d4a-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span></span> <span data-ttu-id="16d4a-122">Daarom raden we u aan deze back-ups te plannen voor daluren.</span><span class="sxs-lookup"><span data-stu-id="16d4a-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="16d4a-123">Om te wijzigen van de standaard back-begintijd, voer de volgende stappen in de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="16d4a-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="16d4a-124">De begintijd voor het standaard back-upbeleid wijzigen</span><span class="sxs-lookup"><span data-stu-id="16d4a-124">To change the start time for the default backup policy</span></span>

1. <span data-ttu-id="16d4a-125">Ga naar **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-125">Go to **Devices**.</span></span> <span data-ttu-id="16d4a-126">De lijst met apparaten die zijn geregistreerd bij uw StorSimple-apparaat Manager-service wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="16d4a-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![Navigeer naar apparaten](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="16d4a-128">Selecteer en klikt u op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="16d4a-128">Select and click your device.</span></span> <span data-ttu-id="16d4a-129">De **instellingen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="16d4a-129">The **Settings** blade will be displayed.</span></span> <span data-ttu-id="16d4a-130">Ga naar **beheren > back-upbeleid**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-130">Go to **Manage > Backup policies**.</span></span>
   
    ![Selecteer het apparaat](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="16d4a-132">In de **back-upbeleid** blade de begintijd van de standaardwaarde is 22:30.</span><span class="sxs-lookup"><span data-stu-id="16d4a-132">In the **Backup policies** blade, the default start time is 22:30.</span></span> <span data-ttu-id="16d4a-133">U kunt de nieuwe begintijd voor de dagelijkse planning opgeven in de tijdzone apparaat.</span><span class="sxs-lookup"><span data-stu-id="16d4a-133">You can specify the new start time for the daily schedule in device time zone.</span></span>
   
    ![Navigeer naar de back-upbeleid](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="16d4a-135">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="16d4a-136">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="16d4a-136">Take a manual backup</span></span>

<span data-ttu-id="16d4a-137">Naast de geplande back-ups, kunt u nemen (op aanvraag) van een handmatige back-up van apparaatgegevens op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="16d4a-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="16d4a-138">Een handmatige back-up maken</span><span class="sxs-lookup"><span data-stu-id="16d4a-138">To create a manual backup</span></span>

1. <span data-ttu-id="16d4a-139">Ga naar **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-139">Go to **Devices**.</span></span> <span data-ttu-id="16d4a-140">Selecteer uw apparaat en met de rechtermuisknop op **...**  aan de rechterkant in de geselecteerde rij.</span><span class="sxs-lookup"><span data-stu-id="16d4a-140">Select your device and right-click **...** at the far right in the selected row.</span></span> <span data-ttu-id="16d4a-141">Selecteer in het contextmenu **back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-141">From the context menu, select **Take backup**.</span></span>
   
    ![Navigeer om de back-up maken](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="16d4a-143">In de **back-up maken** blade, klikt u op **back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-143">In the **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="16d4a-144">Dit wordt back-up alle shares op de bestandsserver of alle volumes op uw iSCSI-server.</span><span class="sxs-lookup"><span data-stu-id="16d4a-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span></span> 
   
    ![back-up wordt gestart](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="16d4a-146">Een op aanvraag back-up wordt gestart en u ziet dat er een back-uptaak is gestart.</span><span class="sxs-lookup"><span data-stu-id="16d4a-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![back-up wordt gestart](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="16d4a-148">Zodra de taak is voltooid, wordt u nogmaals gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="16d4a-148">Once the job has successfully completed, you are notified again.</span></span> <span data-ttu-id="16d4a-149">Het back-upproces vervolgens wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="16d4a-149">The backup process then starts.</span></span>
   
    ![back-uptaak gemaakt](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="16d4a-151">De voortgang van de back-ups volgen en bekijk de taakdetails, klikt u op de melding.</span><span class="sxs-lookup"><span data-stu-id="16d4a-151">To track the progress of the backups and look at the job details, click the notification.</span></span> <span data-ttu-id="16d4a-152">Hiermee gaat u naar **taakgegevens**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-152">This takes you to  **Job details**.</span></span>
   
     ![details van de back-uptaak](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="16d4a-154">Nadat de back-up voltooid is, gaat u naar **Management > back-upcatalogus**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-154">After the backup is complete, go to **Management > Backup catalog**.</span></span> <span data-ttu-id="16d4a-155">U ziet een cloudmomentopname van alle shares (of volumes) op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="16d4a-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span></span>
   
    ![Voltooide back-up](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="16d4a-157">Bestaande back-ups weergeven</span><span class="sxs-lookup"><span data-stu-id="16d4a-157">View existing backups</span></span>
<span data-ttu-id="16d4a-158">Als u wilt weergeven van de bestaande back-ups, moet u de volgende stappen uitvoeren in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="16d4a-158">To view the existing backups, perform the following steps in the Azure portal.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="16d4a-159">Bestaande back-ups weergeven</span><span class="sxs-lookup"><span data-stu-id="16d4a-159">To view existing backups</span></span>

1. <span data-ttu-id="16d4a-160">Ga naar **apparaten** blade.</span><span class="sxs-lookup"><span data-stu-id="16d4a-160">Go to **Devices** blade.</span></span> <span data-ttu-id="16d4a-161">Selecteer en klikt u op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="16d4a-161">Select and click your device.</span></span> <span data-ttu-id="16d4a-162">In de **instellingen** blade, gaat u naar **Management > back-upcatalogus**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span></span>
   
    ![Navigeer naar de back-upcatalogus](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="16d4a-164">Geef de volgende criteria moet worden gebruikt voor het filteren van:</span><span class="sxs-lookup"><span data-stu-id="16d4a-164">Specify the following criteria to be used for filtering:</span></span>
   
    - <span data-ttu-id="16d4a-165">**Tijdsbereik** – kan **afgelopen 1 uur**, **afgelopen 24 uur**, **afgelopen 7 dagen**, **afgelopen 30 dagen**, **afgelopen jaar**, en **aangepaste datum**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="16d4a-166">**Apparaten** – Selecteer in de lijst met bestandsservers of iSCSI-servers geregistreerd bij uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="16d4a-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="16d4a-167">**Geïnitieerd** – automatisch kunnen worden **geplande** (door een back-upbeleid) of **handmatig** gestart (door u).</span><span class="sxs-lookup"><span data-stu-id="16d4a-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Back-ups filteren](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="16d4a-169">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="16d4a-169">Click **Apply**.</span></span> <span data-ttu-id="16d4a-170">De gefilterde lijst met back-ups wordt weergegeven in de **back-upcatalogus** blade.</span><span class="sxs-lookup"><span data-stu-id="16d4a-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span></span> <span data-ttu-id="16d4a-171">Opmerking alleen 100 back-elementen kunnen worden weergegeven op een bepaald moment.</span><span class="sxs-lookup"><span data-stu-id="16d4a-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Bijgewerkte back-upcatalogus](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="16d4a-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16d4a-173">Next steps</span></span>

<span data-ttu-id="16d4a-174">Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="16d4a-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

