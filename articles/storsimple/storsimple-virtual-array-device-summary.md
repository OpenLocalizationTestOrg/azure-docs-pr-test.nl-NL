---
title: Virtuele StorSimple-matrix apparaat samenvatting blade | Microsoft Docs
description: Beschrijft de samenvatting blade apparaat voor StorSimple Apparaatbeheer en wordt uitgelegd hoe u hiermee de status van uw virtuele StorSimple-matrix.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="39361-103">Gebruik de samenvatting blade apparaat voor StorSimple Apparaatbeheer verbonden met virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="39361-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="39361-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="39361-104">Overview</span></span>

<span data-ttu-id="39361-105">De blade Apparaatbeheer StorSimple-apparaat wordt een samenvatting weergegeven van een virtueel StorSimple-matrix die is geregistreerd met een bepaalde StorSimple Apparaatbeheer markeren die apparaat-problemen die aandacht vereisen een systeembeheerder.</span><span class="sxs-lookup"><span data-stu-id="39361-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="39361-106">In deze zelfstudie maakt u kennis met de samenvatting blade apparaat, wordt de inhoud en de functie wordt uitgelegd en beschrijft de taken die u vanuit deze blade uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="39361-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="39361-107">De samenvatting apparaat-blade bevat de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="39361-107">The device summary blade displays the following information:</span></span>

![Apparaat-dashboard](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="39361-109">Beheer</span><span class="sxs-lookup"><span data-stu-id="39361-109">Management</span></span>

<span data-ttu-id="39361-110">In de blade StorSimple-apparaat ziet u de opties voor het beheren van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="39361-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="39361-111">Ziet u de opdrachten voor het beheer aan de bovenkant van de blade en aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="39361-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="39361-112">Gebruik deze opties shares of volumes, toevoegen of bijwerken of failover van uw virtuele matrix.</span><span class="sxs-lookup"><span data-stu-id="39361-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="39361-113">Het gebied essentials bevat enkele belangrijke eigenschappen zoals de status, model, versie, evenals een koppeling naar de **Webgebruikersinterface** van de matrix.</span><span class="sxs-lookup"><span data-stu-id="39361-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="39361-114">Als u zich op een intern netwerk, kunt u rechtstreeks starten de [lokale webgebruikersinterface](storsimple-ova-web-ui-admin.md) voor het beheren van uw virtuele matrix.</span><span class="sxs-lookup"><span data-stu-id="39361-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![Apparaat essentials](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="39361-116">Samenvatting StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="39361-116">StorSimple device summary</span></span>

* <span data-ttu-id="39361-117">De **waarschuwingen** tegel biedt een momentopname van de actieve waarschuwingen voor uw virtuele matrix gegroepeerd op de ernst van waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="39361-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="39361-118">Klik op de tegel openen de **waarschuwingen** blade en klik vervolgens op een afzonderlijke waarschuwing u meer details over deze waarschuwing, inclusief alle aanbevolen acties.</span><span class="sxs-lookup"><span data-stu-id="39361-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="39361-119">U kunt ook de waarschuwing wissen als het probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="39361-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="39361-120">De **capaciteit** tegel worden weergegeven voor de primaire opslag die is ingericht en resterende in het virtuele apparaat ten opzichte van de totale opslag beschikbaar voor dezelfde.</span><span class="sxs-lookup"><span data-stu-id="39361-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="39361-121">**Ingericht** verwijst naar de hoeveelheid opslagruimte die is voorbereid en toegewezen voor gebruik, **resterend** verwijst naar de resterende capaciteit die kan worden ingericht op dit apparaat.</span><span class="sxs-lookup"><span data-stu-id="39361-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="39361-122">De **resterende gelaagde** capaciteit is de beschikbare capaciteit die kan worden ingericht met inbegrip van de cloud, terwijl de **resterende lokale** is de resterende capaciteit op de schijven die aan deze virtuele matrix is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="39361-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="39361-123">In de **gebruik** grafiek, vindt u de primaire opslag in uw virtuele matrix gebruikt, evenals de cloudopslag verbruikt gedurende de afgelopen 7 dagen, de standaard time-outperiode.</span><span class="sxs-lookup"><span data-stu-id="39361-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="39361-124">Gebruik de **bewerken** optie in de rechterbovenhoek van de grafiek naar een ander tijdstip schaal kiezen.</span><span class="sxs-lookup"><span data-stu-id="39361-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="39361-125">De **Shares** of **Volumes** tegel bevat een samenvatting van het aantal shares of volumes op uw apparaat op status gegroepeerd.</span><span class="sxs-lookup"><span data-stu-id="39361-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="39361-126">Klik op de tegel openen de **Shares** of **Volumes** blade lijst en klik vervolgens op een afzonderlijke share of het volume weergeven of wijzigen van de eigenschappen ervan.</span><span class="sxs-lookup"><span data-stu-id="39361-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="39361-127">Zie voor meer informatie hoe [shares kunt beheren](storsimple-virtual-array-manage-shares.md) of [volumes beheren](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="39361-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39361-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="39361-128">Next steps</span></span>
<span data-ttu-id="39361-129">Leer hoe u het volgende doet:</span><span class="sxs-lookup"><span data-stu-id="39361-129">Learn how to:</span></span>
- [<span data-ttu-id="39361-130">Shares op een virtueel StorSimple-matrix beheren</span><span class="sxs-lookup"><span data-stu-id="39361-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="39361-131">Beheren van volumes op een virtueel StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="39361-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

