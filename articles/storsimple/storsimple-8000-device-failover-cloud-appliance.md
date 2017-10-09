---
title: aaaStorSimple failover disaster recovery tooa StorSimple Cloud toestel | Microsoft Docs
description: Meer informatie over hoe toofail via uw fysieke apparaat tooa van StorSimple 8000 series toestel cloud.
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="00ffc-103">Tooyour StorSimple Cloud toestel failover</span><span class="sxs-lookup"><span data-stu-id="00ffc-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="00ffc-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="00ffc-104">Overview</span></span>

<span data-ttu-id="00ffc-105">Deze zelfstudie wordt Hallo stappen vereist toofail via een fysiek apparaat tooa voor StorSimple 8000 serie StorSimple Cloud toestel beschreven als er een noodgeval.</span><span class="sxs-lookup"><span data-stu-id="00ffc-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="00ffc-106">StorSimple gebruikt Hallo apparaat failover-functie toomigrate gegevens vanaf een fysiek Bronapparaat in Hallo datacenter tooa cloud toestel in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="00ffc-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="00ffc-107">Hallo richtlijnen in deze zelfstudie geldt tooStorSimple 8000 series fysieke apparaten en apparaten van cloud met versies van de software Update 3 en hoger.</span><span class="sxs-lookup"><span data-stu-id="00ffc-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="00ffc-108">toolearn meer informatie over failover-apparaat en hoe deze gebruikt toorecover na een noodgeval te gaan[Failover en herstel na noodgevallen voor StorSimple 8000 series apparaten](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="00ffc-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="00ffc-109">toofail via een fysiek apparaat tooanother fysieke StorSimple-apparaat, gaat u te[failover fysieke StorSimple-apparaat tooa](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="00ffc-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="00ffc-110">toofail via een tooitself apparaat gaat te[failover toohello dezelfde fysieke StorSimple-apparaat](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="00ffc-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00ffc-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="00ffc-111">Prerequisites</span></span>

- <span data-ttu-id="00ffc-112">Zorg ervoor dat u Hallo aandachtspunten voor failover-apparaat hebt bekeken.</span><span class="sxs-lookup"><span data-stu-id="00ffc-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="00ffc-113">Voor meer informatie gaat te[algemene overwegingen voor het apparaat failover](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="00ffc-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="00ffc-114">Een StorSimple Cloud toestel gemaakt en geconfigureerd voordat u deze procedure uitvoert, moet u hebben.</span><span class="sxs-lookup"><span data-stu-id="00ffc-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="00ffc-115">Als uitgevoerd bijwerken van versie 3 of hoger, kunt u overwegen een toestel 8020 cloud voor Hallo Noodherstel.</span><span class="sxs-lookup"><span data-stu-id="00ffc-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="00ffc-116">Hallo 8020 model heeft van 64 TB en Premium-opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="00ffc-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="00ffc-117">Voor meer informatie gaat te[implementeren en beheren van een StorSimple-apparaat met Cloud](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="00ffc-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="00ffc-118">Stappen toofail via tooa cloud toestel</span><span class="sxs-lookup"><span data-stu-id="00ffc-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="00ffc-119">Volgende stappen toorestore Hallo apparaat tooa doel StorSimple Cloud toestel Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="00ffc-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="00ffc-120">Controleer of deze Hallo volumecontainer toofail via gewenste cloudmomentopnamen is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="00ffc-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="00ffc-121">Voor meer informatie gaat te[gebruik StorSimple Apparaatbeheer service toocreate back-ups](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="00ffc-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="00ffc-122">Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="00ffc-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="00ffc-123">In Hallo **apparaten** blade, Ga toohello lijst met apparaten die verbonden zijn met uw service.</span><span class="sxs-lookup"><span data-stu-id="00ffc-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="00ffc-124">![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="00ffc-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="00ffc-125">Selecteer en klik op het bronapparaat.</span><span class="sxs-lookup"><span data-stu-id="00ffc-125">Select and click your source device.</span></span> <span data-ttu-id="00ffc-126">Hallo Bronapparaat heeft Hallo volumecontainers die u wilt dat toofail via.</span><span class="sxs-lookup"><span data-stu-id="00ffc-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="00ffc-127">Ga te**instellingen > Volumecontainers**.</span><span class="sxs-lookup"><span data-stu-id="00ffc-127">Go too**Settings > Volume Containers**.</span></span>

    ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="00ffc-129">Selecteer een volumecontainer dat u toofail via tooanother apparaat dat wilt.</span><span class="sxs-lookup"><span data-stu-id="00ffc-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="00ffc-130">Klik op Hallo volume container toodisplay Hallo lijst van volumes in deze container.</span><span class="sxs-lookup"><span data-stu-id="00ffc-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="00ffc-131">Selecteer een volume, klik met de rechtermuisknop en klik op **Offline nemen** tootake Hallo volume offline.</span><span class="sxs-lookup"><span data-stu-id="00ffc-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="00ffc-133">Herhaal dit proces voor alle Hallo volumes in de volumecontainer Hallo.</span><span class="sxs-lookup"><span data-stu-id="00ffc-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="00ffc-135">De vorige stap herhalen Hallo voor alle volumecontainers Hallo gewenst toofail via tooanother apparaat.</span><span class="sxs-lookup"><span data-stu-id="00ffc-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="00ffc-136">Ga terug toohello **apparaten** blade.</span><span class="sxs-lookup"><span data-stu-id="00ffc-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="00ffc-137">Hallo opdrachtbalk en klik op **failover**.</span><span class="sxs-lookup"><span data-stu-id="00ffc-137">From hello command bar, click **Fail over**.</span></span>

    ![Klik op mislukken via](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="00ffc-139">In Hallo **failover** blade Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="00ffc-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="00ffc-140">Klik op **bron**.</span><span class="sxs-lookup"><span data-stu-id="00ffc-140">Click **Source**.</span></span> <span data-ttu-id="00ffc-141">Hallo volume containers toofail via selecteren.</span><span class="sxs-lookup"><span data-stu-id="00ffc-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="00ffc-142">**Alleen Hallo volumecontainers met momentopnamen van de gekoppelde cloud en offline volumes worden weergegeven.**</span><span class="sxs-lookup"><span data-stu-id="00ffc-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="00ffc-143">![Bron selecteren](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="00ffc-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="00ffc-144">Klik op **doel**.</span><span class="sxs-lookup"><span data-stu-id="00ffc-144">Click **Target**.</span></span> <span data-ttu-id="00ffc-145">Selecteer een doel-cloud-toestel Hallo vervolgkeuzelijst met beschikbare apparaten.</span><span class="sxs-lookup"><span data-stu-id="00ffc-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="00ffc-146">**Alleen Hallo-apparaten waarvoor voldoende capaciteit bron tooaccommodate volumecontainers worden in Hallo lijst weergegeven.**</span><span class="sxs-lookup"><span data-stu-id="00ffc-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![Doel selecteren](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="00ffc-148">Controleer Hallo failover-instellingen onder **samenvatting** en selecteer Hallo selectievakje die aangeeft of Hallo volumes in de geselecteerde volumecontainers offline zijn.</span><span class="sxs-lookup"><span data-stu-id="00ffc-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![Failover-instellingen controleren](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="00ffc-150">Er wordt een failover-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="00ffc-150">A failover job is created.</span></span> <span data-ttu-id="00ffc-151">toomonitor hello failover taak, klikt u op Hallo taakmeldingen.</span><span class="sxs-lookup"><span data-stu-id="00ffc-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![Monitor voor failover-taak](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="00ffc-153">Nadat het Hallo-failover is voltooid, gaat u terug toohello **apparaten** blade.</span><span class="sxs-lookup"><span data-stu-id="00ffc-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="00ffc-154">Selecteer Hallo-apparaat dat is gebruikt als doel Hallo voor Hallo failover.</span><span class="sxs-lookup"><span data-stu-id="00ffc-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![Selecteer het apparaat](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="00ffc-156">Klik op **Volumecontainers**.</span><span class="sxs-lookup"><span data-stu-id="00ffc-156">Click **Volume Containers**.</span></span> <span data-ttu-id="00ffc-157">Alle Hallo-volumecontainers, samen met de Hallo volumes van de oude apparaat hello, moeten worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="00ffc-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="00ffc-158">Als het Hallo-volumecontainer waarvoor u failover is lokaal vastgemaakt volumes, zijn deze volumes als gelaagde volumes kan niet via.</span><span class="sxs-lookup"><span data-stu-id="00ffc-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="00ffc-159">Lokaal vastgemaakte volumes worden niet ondersteund op een StorSimple-apparaat met Cloud.</span><span class="sxs-lookup"><span data-stu-id="00ffc-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Doel-volumecontainers weergeven](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="00ffc-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="00ffc-161">Next steps</span></span>

* <span data-ttu-id="00ffc-162">Nadat u hebt een failover uitgevoerd, moet u wellicht te[deactiveren of verwijderen van uw StorSimple-apparaat](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="00ffc-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="00ffc-163">Voor informatie over hoe toouse StorSimple Apparaatbeheer Hallo service, gaat u te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="00ffc-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

