---
title: aaaUse StorSimple 8000 series apparaatoverzicht | Microsoft Docs
description: Hallo Apparaatbeheer StorSimple-apparaat overzicht beschrijft en hoe toouse deze metrische gegevens tooview storage en verbonden initiators en zoeken Hallo serienummer en de IQN.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="6d676-103">Hallo apparaatoverzicht in service Manager voor StorSimple-apparaat gebruiken</span><span class="sxs-lookup"><span data-stu-id="6d676-103">Use hello device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="6d676-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6d676-104">Overview</span></span>
<span data-ttu-id="6d676-105">Hallo StorSimple-apparaat samenvatting blade geeft een overzicht van gegevens voor een specifieke StorSimple-apparaat, in tegenstelling toohello service samenvatting blade waarmee u informatie over alle Hallo apparaten opgenomen in de Microsoft Azure StorSimple-oplossing.</span><span class="sxs-lookup"><span data-stu-id="6d676-105">hello StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast toohello service summary blade, which gives you information about all hello devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="6d676-106">Hallo apparaat samenvatting blade geeft een overzicht van een StorSimple 8000 serie-apparaat dat is geregistreerd bij een gegeven StorSimple apparaat Manager markeren die apparaat-problemen die aandacht vereisen een systeembeheerder.</span><span class="sxs-lookup"><span data-stu-id="6d676-106">hello device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="6d676-107">Deze zelfstudie Hallo apparaat samenvatting blade introduceert, wordt uitgelegd Hallo inhoud en de functie en Hallo worden taken beschreven die u vanuit deze blade uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="6d676-107">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="6d676-108">Hallo apparaat samenvatting blade geeft Hallo volgende informatie weer:</span><span class="sxs-lookup"><span data-stu-id="6d676-108">hello device summary blade displays hello following information:</span></span>

![Samenvatting blade apparaat](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="6d676-110">Opdrachtbalk Management</span><span class="sxs-lookup"><span data-stu-id="6d676-110">Management command bar</span></span>

<span data-ttu-id="6d676-111">In de blade voor Hallo StorSimple-apparaat ziet u Hallo opties voor het beheren van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6d676-111">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="6d676-112">Opdrachten voor het beheer van Hallo ziet u aan de bovenkant Hallo van Hallo blade en aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d676-112">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="6d676-113">Gebruikmaken van deze opties tooadd shares of volumes, bijwerken of failover van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="6d676-113">Use these options tooadd shares or volumes, or update or fail over your device.</span></span>

![Opdrachtbalk Management](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="6d676-115">Essentials</span><span class="sxs-lookup"><span data-stu-id="6d676-115">Essentials</span></span>

<span data-ttu-id="6d676-116">Hallo essentials gebied vastgelegd Hallo belangrijke eigenschappen zoals, Hallo status, model, doel IQN en Hallo softwareversie.</span><span class="sxs-lookup"><span data-stu-id="6d676-116">hello essentials area captures some of hello important properties such as, hello status, model, target IQN, and hello software version.</span></span> 

![Apparaat essentials](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="6d676-118">Bewaking</span><span class="sxs-lookup"><span data-stu-id="6d676-118">Monitoring</span></span>

* <span data-ttu-id="6d676-119">Hallo **waarschuwingen** tegel biedt een momentopname van alle Hallo actieve waarschuwingen voor uw apparaat, gegroepeerd op de ernst van waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="6d676-119">hello **Alerts** tile provides a snapshot of all hello active alerts for your device, grouped by alert severity.</span></span>

    ![Waarschuwing tegel](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="6d676-121">Klik op Hallo tegel tooopen hello **waarschuwingen** blade en klik vervolgens op een afzonderlijke een waarschuwing tooview aanvullende details over deze waarschuwing, inclusief alle aanbevolen acties.</span><span class="sxs-lookup"><span data-stu-id="6d676-121">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="6d676-122">U kunt ook een waarschuwing Hallo wissen als Hallo probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="6d676-122">You can also clear hello alert if hello issue has been resolved.</span></span>

    ![Klik op de tegel waarschuwingen](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="6d676-124">Hallo **Status en gezondheid** tegel biedt inzicht in de status van Hallo hardware-onderdeel voor een apparaat, inclusief het Hallo-Apparaatstatus.</span><span class="sxs-lookup"><span data-stu-id="6d676-124">hello **Status and health** tile provides insights into hello hardware component health for a device including hello device status.</span></span> <span data-ttu-id="6d676-125">de apparaatstatus Hallo mogelijk offline, online, gedeactiveerd of gereed tooset up.</span><span class="sxs-lookup"><span data-stu-id="6d676-125">hello device status may be offline, online, deactivated, or ready tooset up.</span></span>

    ![Tegel status en gezondheid](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="6d676-127">Hallo **Volumes** tegel bevat een samenvatting van Hallo aantal volumes in uw apparaat op status gegroepeerd.</span><span class="sxs-lookup"><span data-stu-id="6d676-127">hello **Volumes** tile provides a summary of hello number of volumes in your device grouped by status.</span></span>

    ![Tegel volumes](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="6d676-129">Klik op Hallo tegel tooopen hello **Volumes** blade lijst en klikt u op een afzonderlijke volume tooview of de eigenschappen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6d676-129">Click hello tile tooopen hello **Volumes** list blade, and then click on an individual volume tooview or modify its properties.</span></span>
    
    ![Klik op de tegel volumes](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="6d676-131">Voor meer informatie Zie hoe te[volumes beheren](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="6d676-131">For more information, see how too[manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="6d676-132">In Hallo **gebruik** grafiek, kunt u Hallo primaire opslag gebruikt via het apparaat en de Hallo cloud-opslag verbruikt Hallo afgelopen 7 dagen, Hallo standaard periode bekijken.</span><span class="sxs-lookup"><span data-stu-id="6d676-132">In hello **Usage** chart, you can view hello primary storage used across your device, and hello cloud storage consumed over hello past 7 days, hello default time period.</span></span>

     ![Tegel gebruik](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="6d676-134">een andere tijdschaal toochoose hello gebruiken **bewerken** optie in de rechterbovenhoek Hallo van Hallo grafiek.</span><span class="sxs-lookup"><span data-stu-id="6d676-134">toochoose a different time scale, use hello **Edit** option in hello top-right corner of hello chart.</span></span>

     ![Gebruiksgrafiek bewerken](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="6d676-136">In deze grafiek, u kunt metrische gegevens voor Hallo totale primaire opslag (Hallo hoeveelheid gegevens die zijn geschreven door hosts tooyour apparaat) weergeven en totale Hallo cloudopslag verbruikt door uw apparaat gedurende een periode.</span><span class="sxs-lookup"><span data-stu-id="6d676-136">In this chart, you can view metrics for hello total primary storage (hello amount of data written by hosts tooyour device) and hello total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="6d676-137">In deze context *primaire opslag* toohello totale hoeveelheid gegevens die zijn geschreven door Hallo host verwijst, en door volumetype kunnen worden onderverdeeld: *primaire gelaagde opslag* bevat zowel lokaal opgeslagen gegevens en gegevens gelaagde toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="6d676-137">In this context, *primary storage* refers toohello total amount of data written by hello host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered toohello cloud.</span></span> <span data-ttu-id="6d676-138">*Primaire lokaal vastgemaakt opslag* bevat alleen gegevens die lokaal zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6d676-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="6d676-139">*Cloudopslag*, op Hallo daarentegen, is een meting van de totale hoeveelheid gegevens die zijn opgeslagen in de cloud Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d676-139">*Cloud storage*, on hello other hand, is a measurement of hello total amount of data stored in hello cloud.</span></span> <span data-ttu-id="6d676-140">Deze opslag bevat gelaagde gegevens en back-ups.</span><span class="sxs-lookup"><span data-stu-id="6d676-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="6d676-141">Hallo-gegevens die zijn opgeslagen in de cloud Hallo is ontdubbeld en gecomprimeerd, terwijl primaire opslag Hallo en de hoeveelheid opslagruimte gebruikt geeft voordat het Hallo-gegevens worden ontdubbeld en gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="6d676-141">hello data stored in hello cloud is deduplicated and compressed, whereas primary storage indicates hello amount of storage used before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="6d676-142">(U kunt deze twee getallen tooget een idee van Hallo compressie tarief vergelijken.) Voor zowel de primaire en cloudopslag, Hallo bedragen die zijn gebaseerd op Hallo bijhouden frequentie die u configureert.</span><span class="sxs-lookup"><span data-stu-id="6d676-142">(You can compare these two numbers tooget an idea of hello compression rate.) For both primary and cloud storage, hello amounts shown are based on hello tracking frequency you configure.</span></span> <span data-ttu-id="6d676-143">Als u een frequentie van één week kiest, klikt u vervolgens ziet Hallo grafiek u bijvoorbeeld gegevens voor elke dag in Hallo vorige week.</span><span class="sxs-lookup"><span data-stu-id="6d676-143">For example, if you choose a one week frequency, then hello chart shows data for each day in hello previous week.</span></span>

     <span data-ttu-id="6d676-144">toosee hello hoeveelheid cloud-opslag verbruikt tijd, selecteer Hallo **CLOUD-opslag gebruikt** optie.</span><span class="sxs-lookup"><span data-stu-id="6d676-144">toosee hello amount of cloud storage consumed over time, select hello **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="6d676-145">toosee hello totale opslag die is geschreven door Hallo host, selecteer Hallo **primaire GELAAGDE opslag gebruikt** en **primaire lokaal VASTGEMAAKT opslag gebruikt** opties.</span><span class="sxs-lookup"><span data-stu-id="6d676-145">toosee hello total storage that has been written by hello host, select hello **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="6d676-146">Zie voor meer informatie [gebruik Hallo StorSimple Apparaatbeheer service toomonitor uw StorSimple-apparaat](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="6d676-146">For more information, see [Use hello StorSimple Device Manager service toomonitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="6d676-147">Hallo **capaciteit** tegel geeft Hallo primaire opslag die is ingericht en de resterende over Hallo apparaat relatieve toohello totale opslag beschikbaar voor dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="6d676-147">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="6d676-148">**Ingericht** toohello en de hoeveelheid opslagruimte die is voorbereid en toegewezen voor gebruik, verwijst **resterend** verwijst toohello resterende capaciteit die kan worden ingericht op dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="6d676-148">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> 

    ![Tegel gebruik](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="6d676-150">Klik op deze tegel tooview hoe Hallo capaciteit is ingericht op de gelaagde en lokaal vastgemaakte volumes.</span><span class="sxs-lookup"><span data-stu-id="6d676-150">Click this tile tooview how hello capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="6d676-151">Hallo **resterende gelaagde** capaciteit is Hallo beschikbare capaciteit die kan worden ingericht met inbegrip van de cloud, tijdens het Hallo **resterende lokale** is Hallo resterende capaciteit op Hallo schijven toothis apparaat is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6d676-151">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis device.</span></span>

    ![Klik op de gebruiksgrafiek](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="6d676-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d676-153">Next steps</span></span>
* <span data-ttu-id="6d676-154">Meer informatie over Hallo [StorSimple-service samenvatting blade](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="6d676-154">Learn more about hello [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="6d676-155">Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6d676-155">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

