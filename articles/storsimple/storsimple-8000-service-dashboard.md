---
title: Gebruik StorSimple 8000 series apparaatoverzicht | Microsoft Docs
description: Beschrijving van de samenvatting blade voor StorSimple-service en wordt uitgelegd hoe u hiermee de status van uw StorSimple-oplossing.
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: d987a4ae170f21532a886552cbe1eb5a0d25fc3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="abcce-103">De service samenvatting blade voor StorSimple 8000 series apparaat gebruiken</span><span class="sxs-lookup"><span data-stu-id="abcce-103">Use the service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="abcce-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="abcce-104">Overview</span></span>

<span data-ttu-id="abcce-105">De samenvatting blade voor Apparaatbeheer van StorSimple-service geeft een overzicht van de apparaten die zijn verbonden met de Apparaatbeheer StorSimple-service, die apparaten die aandacht vereisen een systeembeheerder is gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="abcce-105">The StorSimple Device Manager service summary blade provides a summary view of all the devices that are connected to the StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="abcce-106">Deze zelfstudie maakt u kennis met de service samenvatting blade, worden de Dashboardinhoud en de functie en beschrijft de taken die u op deze pagina uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="abcce-106">This tutorial introduces the service summary blade, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![Serviceoverzicht](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="abcce-108">Opdrachten voor beheer</span><span class="sxs-lookup"><span data-stu-id="abcce-108">Management commands</span></span>

<span data-ttu-id="abcce-109">In de StorSimple-service samenvatting blade ziet u de opties voor het beheren van uw StorSimple-apparaat Manager-service en de apparaten van het StorSimple 8000 serie geregistreerd bij deze service.</span><span class="sxs-lookup"><span data-stu-id="abcce-109">In the StorSimple service summary blade, you see the options for managing your StorSimple Device Manager service and the StorSimple 8000 series devices registered to this service.</span></span> <span data-ttu-id="abcce-110">Ziet u de opdrachten voor het beheer aan de bovenkant van de blade en aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="abcce-110">You see the management commands across the top of the blade and on the left side.</span></span>

![Opdrachtbalk](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="abcce-112">Gebruik deze opties verschillende bewerkingen uitvoeren zoals shares of volumes of monitor voor de verschillende taken die worden uitgevoerd op het StorSimple-apparaten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="abcce-112">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="abcce-113">Essentials</span><span class="sxs-lookup"><span data-stu-id="abcce-113">Essentials</span></span>

<span data-ttu-id="abcce-114">Het gebied essentials worden enkele belangrijke eigenschappen zoals de resourcegroep, de locatie en het abonnement waarin uw StorSimple-apparaat Manager is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="abcce-114">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![Essentials](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="abcce-116">Serviceoverzicht StorSimple-Apparaatbeheer</span><span class="sxs-lookup"><span data-stu-id="abcce-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="abcce-117">De **waarschuwingen** tegel biedt een momentopname van de actieve waarschuwingen op alle apparaten, gegroepeerd op de ernst van waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="abcce-117">The **Alerts** tile provides a snapshot of all the active alerts across all devices, grouped by alert severity.</span></span>

    ![Tegel waarschuwingen](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="abcce-119">Op de tegel klikt, wordt de **waarschuwingen** blade waar u kunt klikken op een afzonderlijke waarschuwing om aanvullende informatie over deze waarschuwing weer te geven inclusief alle aanbevolen acties.</span><span class="sxs-lookup"><span data-stu-id="abcce-119">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="abcce-120">U kunt ook de waarschuwing wissen als het probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="abcce-120">You can also clear the alert if the issue has been resolved.</span></span>

    ![Klik op de tegel waarschuwingen](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="abcce-122">De **capaciteit** tegel geeft de primaire opslag die is ingericht en resterende op alle apparaten ten opzichte van de totale opslagruimte beschikbaar op alle apparaten bevat.</span><span class="sxs-lookup"><span data-stu-id="abcce-122">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="abcce-123">**Ingericht** verwijst naar de hoeveelheid opslagruimte die is voorbereid en toegewezen voor gebruik, **resterend** verwijst naar de resterende capaciteit die kan worden ingericht op alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="abcce-123">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all devices.</span></span>

    ![Capaciteit tegel](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="abcce-125">De **resterende gelaagde** capaciteit is de beschikbare capaciteit die kan worden ingericht met inbegrip van de cloud, terwijl de **resterende lokale** is de resterende capaciteit op de schijven die zijn gekoppeld aan apparaten uit de StorSimple 8000 serie.</span><span class="sxs-lookup"><span data-stu-id="abcce-125">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="abcce-126">In de **gebruik** grafiek, kunt u de relevante metrische gegevens voor uw apparaten bekijken.</span><span class="sxs-lookup"><span data-stu-id="abcce-126">In the **Usage** chart, you can see the relevant metrics for your devices.</span></span> <span data-ttu-id="abcce-127">U kunt de primaire opslagruimte gebruikt op alle apparaten en de cloudopslag die wordt gebruikt door apparaten gedurende de afgelopen 7 dagen, de standaardwaarde periode weergeven.</span><span class="sxs-lookup"><span data-stu-id="abcce-127">You can view the primary storage used across all devices, and the cloud storage consumed by devices over the past 7 days, the default time period.</span></span> 

    ![Tegel gebruik](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="abcce-129">Als u een ander tijdstip schaal, gebruiken de **bewerken** optie in de rechterbovenhoek van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="abcce-129">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Klik op de tegel gebruik](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![De grafiekgegevens exporteren](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="abcce-132">De **apparaten** tegel bevat een samenvatting van het aantal StorSimple 8000 series apparaten in uw Apparaatbeheer van StorSimple gegroepeerd op de apparaatstatus.</span><span class="sxs-lookup"><span data-stu-id="abcce-132">The **Devices** tile provides a summary of the number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![Apparaten tegel](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="abcce-134">Klik op deze tegel openen de **apparaten** blade lijst en klik vervolgens op een afzonderlijk apparaat om te zoomen op de samenvatting voor apparaten die specifiek zijn voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="abcce-134">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="abcce-135">U kunt ook apparaatspecifieke acties uitvoeren vanaf een bepaald apparaat samenvatting blade.</span><span class="sxs-lookup"><span data-stu-id="abcce-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="abcce-136">Voor meer informatie over de samenvatting blade apparaat, gaat u naar [apparaat samenvatting blade](storsimple-8000-device-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="abcce-136">For more information about the device summary blade, go to [Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![Klik op de tegel apparaten](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-the-activity-logs"></a><span data-ttu-id="abcce-138">Bekijk de activiteitenlogboeken</span><span class="sxs-lookup"><span data-stu-id="abcce-138">View the activity logs</span></span>

<span data-ttu-id="abcce-139">Als u wilt weergeven van de verschillende bewerkingen uitgevoerd binnen uw StorSimple-Apparaatbeheer de **activiteitenlogboeken** koppeling aan de linkerkant van de blade voor een overzicht van het StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="abcce-139">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="abcce-140">Hiermee gaat u naar de **activiteitenlogboeken** blade waar u een van de recente bewerkingen uitgevoerd overzicht.</span><span class="sxs-lookup"><span data-stu-id="abcce-140">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![Activiteitenlogboeken](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="abcce-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="abcce-142">Next steps</span></span>

* <span data-ttu-id="abcce-143">Meer informatie over het [de Apparaatbeheer StorSimple-service gebruiken voor het beheren van uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="abcce-143">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

