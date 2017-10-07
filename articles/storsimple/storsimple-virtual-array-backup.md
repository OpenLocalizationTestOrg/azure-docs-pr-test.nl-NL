---
title: aaaMicrosoft virtuele StorSimple-matrix Azure back-zelfstudie | Microsoft Docs
description: Hierin wordt beschreven hoe tooback up virtuele StorSimple-matrix deelt en volumes.
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
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="052a6-103">Back-up shares of volumes op uw virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="052a6-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="052a6-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="052a6-104">Overview</span></span>

<span data-ttu-id="052a6-105">Hallo virtuele StorSimple-matrix is een hybride cloud-opslag on-premises virtuele apparaat die kan worden geconfigureerd als een bestandsserver of een iSCSI-server.</span><span class="sxs-lookup"><span data-stu-id="052a6-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="052a6-106">Hallo virtuele matrix kunt Hallo gebruiker toocreate geplande en handmatige back-ups van alle Hallo shares of volumes op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="052a6-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="052a6-107">Wanneer geconfigureerd als een bestandsserver, kunt u ook herstel op itemniveau.</span><span class="sxs-lookup"><span data-stu-id="052a6-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="052a6-108">Deze zelfstudie wordt beschreven hoe toocreate gepland en handmatige back-ups en herstel op itemniveau toorestore een verwijderd bestand op uw virtuele matrix uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="052a6-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="052a6-109">Deze zelfstudie geldt toohello StorSimple virtuele matrices alleen.</span><span class="sxs-lookup"><span data-stu-id="052a6-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="052a6-110">Voor informatie over 8000-serie gaat te[een back-up voor 8000 series apparaat maken](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="052a6-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="052a6-111">Back-up-shares en -volumes</span><span class="sxs-lookup"><span data-stu-id="052a6-111">Back up shares and volumes</span></span>

<span data-ttu-id="052a6-112">Back-ups punt in tijd beveiliging bieden, verbeteren de herstelmogelijkheden en hersteltijden voor shares en -volumes te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="052a6-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="052a6-113">U kunt back-up een share of het volume op uw StorSimple-apparaat op twee manieren: **geplande** of **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="052a6-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="052a6-114">Elk van de methoden hello wordt besproken in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="052a6-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="052a6-115">De back-begintijd Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="052a6-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="052a6-116">In deze release worden geplande back-ups gemaakt door een standaardbeleid dat wordt dagelijks wordt uitgevoerd op een opgegeven periode zijn uitgevoerd en een back-up alle Hallo shares of volumes op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="052a6-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="052a6-117">Het is niet mogelijk toocreate aangepaste beleidsregels voor geplande back-ups op dit moment.</span><span class="sxs-lookup"><span data-stu-id="052a6-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="052a6-118">Uw virtuele StorSimple-matrix heeft een standaard back-upbeleid dat begint op een bepaald tijdstip van de dag (22.30) en een back-up alle Hallo shares of volumes op Hallo apparaat eenmaal per dag.</span><span class="sxs-lookup"><span data-stu-id="052a6-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="052a6-119">U kunt wijzigen Hallo tijd op welke Hallo back-up wordt gestart, maar de Hallo frequentie en het Hallo bewaren (die geeft het aantal back-ups tooretain Hallo) kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="052a6-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="052a6-120">Tijdens deze back-ups, Hallo gehele virtuele apparaat back-up.</span><span class="sxs-lookup"><span data-stu-id="052a6-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="052a6-121">Dit kan mogelijk invloed hebben op prestaties Hallo Hallo-apparaat en van invloed zijn op Hallo werkbelastingen die zijn geïmplementeerd op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="052a6-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="052a6-122">Daarom raden we u aan deze back-ups te plannen voor daluren.</span><span class="sxs-lookup"><span data-stu-id="052a6-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="052a6-123">toochange hello standaardback-up begintijd, voert u stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="052a6-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="052a6-124">toochange hello begintijd voor back-upbeleid voor Hallo-standaard</span><span class="sxs-lookup"><span data-stu-id="052a6-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="052a6-125">Ga te**apparaten**.</span><span class="sxs-lookup"><span data-stu-id="052a6-125">Go too**Devices**.</span></span> <span data-ttu-id="052a6-126">Hallo-lijst met apparaten die zijn geregistreerd bij uw StorSimple-apparaat Manager-service wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="052a6-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![Navigeer toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="052a6-128">Selecteer en klikt u op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="052a6-128">Select and click your device.</span></span> <span data-ttu-id="052a6-129">Hallo **instellingen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="052a6-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="052a6-130">Ga te**beheren > back-upbeleid**.</span><span class="sxs-lookup"><span data-stu-id="052a6-130">Go too**Manage > Backup policies**.</span></span>
   
    ![Selecteer het apparaat](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="052a6-132">In Hallo **back-upbeleid** blade Hallo standaardbegintijd is 22:30.</span><span class="sxs-lookup"><span data-stu-id="052a6-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="052a6-133">In de tijdzone apparaat kunt u nieuwe begintijd Hallo voor Hallo dagelijks schema.</span><span class="sxs-lookup"><span data-stu-id="052a6-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![Navigeer toobackup beleid](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="052a6-135">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="052a6-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="052a6-136">Maak een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="052a6-136">Take a manual backup</span></span>

<span data-ttu-id="052a6-137">Bovendien tooscheduled back-ups, u kunt nemen handmatige (op aanvraag) reservekopie van apparaatgegevens op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="052a6-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="052a6-138">toocreate een handmatige back-up</span><span class="sxs-lookup"><span data-stu-id="052a6-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="052a6-139">Ga te**apparaten**.</span><span class="sxs-lookup"><span data-stu-id="052a6-139">Go too**Devices**.</span></span> <span data-ttu-id="052a6-140">Selecteer uw apparaat en met de rechtermuisknop op **...**  op Hallo uiterst rechts in de geselecteerde rij Hallo.</span><span class="sxs-lookup"><span data-stu-id="052a6-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="052a6-141">Selecteer in het contextmenu hello, **back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="052a6-141">From hello context menu, select **Take backup**.</span></span>
   
    ![Navigeer tootake back-up](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="052a6-143">In Hallo **back-up maken** blade, klikt u op **back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="052a6-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="052a6-144">Dit wordt back-up alle Hallo shares op de bestandsserver Hallo of alle Hallo-volumes op de iSCSI-server.</span><span class="sxs-lookup"><span data-stu-id="052a6-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![back-up wordt gestart](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="052a6-146">Een op aanvraag back-up wordt gestart en u ziet dat er een back-uptaak is gestart.</span><span class="sxs-lookup"><span data-stu-id="052a6-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![back-up wordt gestart](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="052a6-148">Zodra het Hallo-taak is voltooid, wordt u nogmaals gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="052a6-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="052a6-149">back-upproces Hallo vervolgens wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="052a6-149">hello backup process then starts.</span></span>
   
    ![back-uptaak gemaakt](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="052a6-151">tootrack hello voortgang van de back-ups Hallo en bekijk de taakdetails hello, klik op Hallo-melding.</span><span class="sxs-lookup"><span data-stu-id="052a6-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="052a6-152">Hiermee gaat u verder te **taakgegevens**.</span><span class="sxs-lookup"><span data-stu-id="052a6-152">This takes you too **Job details**.</span></span>
   
     ![details van de back-uptaak](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="052a6-154">Nadat het Hallo back-up is voltooid, gaat u te**Management > back-upcatalogus**.</span><span class="sxs-lookup"><span data-stu-id="052a6-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="052a6-155">U ziet een cloudmomentopname van alle shares hello (of volumes) op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="052a6-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Voltooide back-up](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="052a6-157">Bestaande back-ups weergeven</span><span class="sxs-lookup"><span data-stu-id="052a6-157">View existing backups</span></span>
<span data-ttu-id="052a6-158">tooview hello bestaande back-ups uitvoeren Hallo stappen te volgen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="052a6-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="052a6-159">tooview bestaande back-ups</span><span class="sxs-lookup"><span data-stu-id="052a6-159">tooview existing backups</span></span>

1. <span data-ttu-id="052a6-160">Ga te**apparaten** blade.</span><span class="sxs-lookup"><span data-stu-id="052a6-160">Go too**Devices** blade.</span></span> <span data-ttu-id="052a6-161">Selecteer en klikt u op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="052a6-161">Select and click your device.</span></span> <span data-ttu-id="052a6-162">In Hallo **instellingen** blade te gaan**Management > back-upcatalogus**.</span><span class="sxs-lookup"><span data-stu-id="052a6-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Navigeer toobackup catalogus](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="052a6-164">Geef Hallo criteria toobe gebruikt voor het filteren te volgen:</span><span class="sxs-lookup"><span data-stu-id="052a6-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="052a6-165">**Tijdsbereik** – kan **afgelopen 1 uur**, **afgelopen 24 uur**, **afgelopen 7 dagen**, **afgelopen 30 dagen**, **afgelopen jaar**, en **aangepaste datum**.</span><span class="sxs-lookup"><span data-stu-id="052a6-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="052a6-166">**Apparaten** – Selecteer in de lijst Hallo van bestandsservers of iSCSI-servers geregistreerd bij uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="052a6-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="052a6-167">**Geïnitieerd** – automatisch kunnen worden **geplande** (door een back-upbeleid) of **handmatig** gestart (door u).</span><span class="sxs-lookup"><span data-stu-id="052a6-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Back-ups filteren](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="052a6-169">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="052a6-169">Click **Apply**.</span></span> <span data-ttu-id="052a6-170">Hallo gefilterde lijst van back-ups wordt weergegeven in Hallo **back-upcatalogus** blade.</span><span class="sxs-lookup"><span data-stu-id="052a6-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="052a6-171">Opmerking alleen 100 back-elementen kunnen worden weergegeven op een bepaald moment.</span><span class="sxs-lookup"><span data-stu-id="052a6-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Bijgewerkte back-upcatalogus](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="052a6-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="052a6-173">Next steps</span></span>

<span data-ttu-id="052a6-174">Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="052a6-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

