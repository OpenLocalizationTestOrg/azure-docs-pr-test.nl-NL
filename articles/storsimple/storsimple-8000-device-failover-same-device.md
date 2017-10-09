---
title: aaaStorSimple failover, herstel na noodgevallen voor apparaten 8000 serie | Microsoft Docs
description: Meer informatie over hoe toofail via uw StorSimple-apparaat toohello hetzelfde apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="1597f-103">Uw StorSimple-apparaat fysiek apparaat toosame failover</span><span class="sxs-lookup"><span data-stu-id="1597f-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="1597f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1597f-104">Overview</span></span>

<span data-ttu-id="1597f-105">Deze zelfstudie wordt Hallo stappen vereist toofail via een StorSimple 8000 series fysiek apparaat tooitself beschreven als er een noodgeval.</span><span class="sxs-lookup"><span data-stu-id="1597f-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="1597f-106">Hallo failover-functie toomigrate apparaatgegevens vanaf een fysiek Bronapparaat StorSimple gebruikt in Hallo datacenter tooanother fysieke apparaat.</span><span class="sxs-lookup"><span data-stu-id="1597f-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="1597f-107">Hallo richtlijnen in deze zelfstudie geldt tooStorSimple 8000 series fysieke apparaten met versies van de software Update 3 en hoger.</span><span class="sxs-lookup"><span data-stu-id="1597f-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="1597f-108">toolearn meer informatie over failover-apparaat en hoe deze gebruikt toorecover na een noodgeval te gaan[Failover en herstel na noodgevallen voor StorSimple 8000 series apparaten](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="1597f-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="1597f-109">toofail via een fysiek apparaat tooanother fysiek apparaat, gaat u te[failover toohello dezelfde fysieke StorSimple-apparaat](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="1597f-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="1597f-110">toofail via een StorSimple fysiek apparaat tooa StorSimple Cloud toestel, gaat u te[tooa StorSimple Cloud toestel failover](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="1597f-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1597f-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1597f-111">Prerequisites</span></span>

- <span data-ttu-id="1597f-112">Zorg ervoor dat u Hallo aandachtspunten voor failover-apparaat hebt bekeken.</span><span class="sxs-lookup"><span data-stu-id="1597f-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="1597f-113">Voor meer informatie gaat te[algemene overwegingen voor het apparaat failover](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="1597f-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="1597f-114">Stappen toofail via toohello hetzelfde apparaat</span><span class="sxs-lookup"><span data-stu-id="1597f-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="1597f-115">Uitvoeren van de volgende stappen uit als u toofail via toohello moet Hallo hetzelfde apparaat.</span><span class="sxs-lookup"><span data-stu-id="1597f-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="1597f-116">Momentopnamen cloud van alle Hallo volumes in uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="1597f-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="1597f-117">Voor meer informatie gaat te[gebruik StorSimple Apparaatbeheer service toocreate back-ups](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="1597f-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="1597f-118">De standaardinstellingen van uw apparaat toofactory opnieuw.</span><span class="sxs-lookup"><span data-stu-id="1597f-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="1597f-119">Ga als volgt Hallo gedetailleerde instructies in [hoe de standaardinstellingen voor een StorSimple-apparaat toofactory tooreset](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="1597f-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="1597f-120">Ga toohello Apparaatbeheer StorSimple-service en selecteer vervolgens **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="1597f-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="1597f-121">In Hallo **apparaten** blade Hallo oude apparaat moet worden weergegeven als **Offline**.</span><span class="sxs-lookup"><span data-stu-id="1597f-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Offline Bronapparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="1597f-123">Uw apparaat configureren en het opnieuw registreren met uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="1597f-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="1597f-124">Hallo nieuw ingeschreven apparaat moet worden weergegeven als **tooset gereed**.</span><span class="sxs-lookup"><span data-stu-id="1597f-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="1597f-125">Hallo apparaatnaam voor het nieuwe apparaat Hallo is Hallo hetzelfde als het oude apparaat Hallo maar toegevoegd met een cijfer tooindicate dat Hallo-apparaat opnieuw instellen van toofactory standaard was en opnieuw geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="1597f-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![Nieuw ingeschreven apparaat gereed tooset up](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="1597f-127">Voor het nieuwe apparaat hello, Apparaatinstelling Hallo.</span><span class="sxs-lookup"><span data-stu-id="1597f-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="1597f-128">Voor meer informatie gaat te[stap 4: minimale apparaatconfiguratie voltooien](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="1597f-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="1597f-129">Op Hallo **apparaten** blade Hallo Hallo apparaat statuswijzigingen te**Online**.</span><span class="sxs-lookup"><span data-stu-id="1597f-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1597f-130">**Minimale configuratie Hallo eerst te voltooien of uw DR mislukken.**</span><span class="sxs-lookup"><span data-stu-id="1597f-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Nieuw ingeschreven apparaat online is](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="1597f-132">Selecteer Hallo oude apparaat (offline status) en uit de opdrachtbalk hello, klikt u op **failover**.</span><span class="sxs-lookup"><span data-stu-id="1597f-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="1597f-133">In Hallo **failover** blade oude apparaat selecteren als bron Hallo en geef Hallo doelapparaat zoals Hallo apparaat opnieuw is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="1597f-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Overzicht van failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="1597f-135">Voor gedetailleerde instructies te verwijzen[tooanother fysiek apparaat failover](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="1597f-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="1597f-136">Een hersteltaak van het apparaat wordt gemaakt dat u vanaf Hallo bewaken kunt **taken** blade.</span><span class="sxs-lookup"><span data-stu-id="1597f-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="1597f-137">Nadat het Hallo-taak is voltooid, toegang tot Hallo nieuwe apparaat en navigeer toohello **volumecontainers** blade.</span><span class="sxs-lookup"><span data-stu-id="1597f-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="1597f-138">Controleren of alle Hallo volumecontainers van het oude apparaat Hallo toohello nieuw apparaat zijn gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="1597f-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Volumecontainers gemigreerd](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="1597f-140">Nadat het Hallo failover is voltooid, kunt u deactiveren en Hallo oude apparaat verwijderen uit Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="1597f-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="1597f-141">Selecteer Hallo oude apparaat (offline), klik met de rechtermuisknop en selecteer vervolgens **deactiveren**.</span><span class="sxs-lookup"><span data-stu-id="1597f-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="1597f-142">Nadat het Hallo-apparaat wordt gedeactiveerd, wordt Hallo status van Hallo-apparaat bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1597f-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Het bronvolume is gedeactiveerd](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="1597f-144">Selecteer Hallo gedeactiveerd apparaat, klik met de rechtermuisknop en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1597f-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="1597f-145">Hierdoor Hallo-apparaat wordt verwijderd uit het Hallo-lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="1597f-145">This deletes hello device from hello list of devices.</span></span>

    ![Het bronvolume is verwijderd](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="1597f-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1597f-147">Next steps</span></span>

* <span data-ttu-id="1597f-148">Nadat u hebt een failover uitgevoerd, moet u wellicht te[deactiveren of verwijderen van uw StorSimple-apparaat](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="1597f-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="1597f-149">Voor informatie over hoe toouse StorSimple Apparaatbeheer Hallo service, gaat u te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1597f-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

