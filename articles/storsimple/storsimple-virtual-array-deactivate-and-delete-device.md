---
title: Deactiveren en verwijderen van een Microsoft Azure StorSimple virtuele matrix | Microsoft Docs
description: Beschrijving van het StorSimple-apparaat verwijderen uit de service met deze eerst te deactiveren en vervolgens te verwijderen.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 8dea36f92b034f8c6cdb6875634848d37f4c6606
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="107e8-103">Deactiveren en verwijderen van een virtueel StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="107e8-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="107e8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="107e8-104">Overview</span></span>

<span data-ttu-id="107e8-105">Wanneer u een virtueel StorSimple-matrix deactiveert, verbreekt u de verbinding tussen het apparaat en de bijbehorende Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="107e8-105">When you deactivate a StorSimple Virtual Array, you break the connection between the device and the corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="107e8-106">Deze zelfstudie wordt uitgelegd hoe:</span><span class="sxs-lookup"><span data-stu-id="107e8-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="107e8-107">Een apparaat deactiveren</span><span class="sxs-lookup"><span data-stu-id="107e8-107">Deactivate a device</span></span> 
* <span data-ttu-id="107e8-108">Een gedeactiveerde apparaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="107e8-108">Delete a deactivated device</span></span>

<span data-ttu-id="107e8-109">De informatie in dit artikel is alleen van toepassing op virtuele StorSimple-matrices.</span><span class="sxs-lookup"><span data-stu-id="107e8-109">The information in this article applies to StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="107e8-110">Voor informatie over 8000-serie, gaat u naar het [deactiveren of verwijderen van een apparaat](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="107e8-110">For information on 8000 series, go to how to [deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-to-deactivate"></a><span data-ttu-id="107e8-111">Wanneer voor het deactiveren?</span><span class="sxs-lookup"><span data-stu-id="107e8-111">When to deactivate?</span></span>

<span data-ttu-id="107e8-112">Deactivering is een permanente bewerking en kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="107e8-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="107e8-113">U kunt een gedeactiveerde apparaat kan niet opnieuw registreren met de service Manager voor StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="107e8-113">You cannot register a deactivated device with the StorSimple Device Manager service again.</span></span> <span data-ttu-id="107e8-114">Mogelijk moet u deactiveren en verwijderen van een virtueel StorSimple-matrix in de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="107e8-114">You may need to deactivate and delete a StorSimple Virtual Array in the following scenarios:</span></span>

* <span data-ttu-id="107e8-115">**De geplande failover** : het apparaat online is en u van plan bent uw apparaat failover.</span><span class="sxs-lookup"><span data-stu-id="107e8-115">**Planned failover** : Your device is online and you plan to fail over your device.</span></span> <span data-ttu-id="107e8-116">Als u van plan bent om te werken naar een grotere apparaat, kunt u wellicht een failover van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="107e8-116">If you are planning to upgrade to a larger device, you may need to fail over your device.</span></span> <span data-ttu-id="107e8-117">Nadat de Gegevenseigendom wordt overgedragen en de failover voltooid is, wordt het bronapparaat automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="107e8-117">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="107e8-118">**Niet-geplande failover** : het apparaat offline is en u moet het apparaat een failover.</span><span class="sxs-lookup"><span data-stu-id="107e8-118">**Unplanned failover** : Your device is offline and you need to fail over the device.</span></span> <span data-ttu-id="107e8-119">Dit scenario kan optreden tijdens een noodgeval wanneer er een storing in het datacenter en het primaire apparaat niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="107e8-119">This scenario may occur during a disaster when there is an outage in the datacenter and your primary device is down.</span></span> <span data-ttu-id="107e8-120">U van plan bent het apparaat een tweede apparaat failover.</span><span class="sxs-lookup"><span data-stu-id="107e8-120">You plan to fail over the device to a secondary device.</span></span> <span data-ttu-id="107e8-121">Nadat de Gegevenseigendom wordt overgedragen en de failover voltooid is, wordt het bronapparaat automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="107e8-121">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="107e8-122">**Buiten gebruik stellen** : U wilt dat het apparaat buiten gebruik stellen.</span><span class="sxs-lookup"><span data-stu-id="107e8-122">**Decommission** : You want to decommission the device.</span></span> <span data-ttu-id="107e8-123">Hiervoor moet u eerst het apparaat te deactiveren en vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="107e8-123">This requires you to first deactivate the device and then delete it.</span></span> <span data-ttu-id="107e8-124">Wanneer u een apparaat deactiveert, u niet langer toegang tot alle gegevens die lokaal wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="107e8-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="107e8-125">U kunt alleen toegang tot en het herstellen van de gegevens die zijn opgeslagen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="107e8-125">You can only access and recover the data stored in the cloud.</span></span> <span data-ttu-id="107e8-126">Als u van plan bent de gegevens van het apparaat om na te behouden deactivering, moet u een cloudmomentopname van al uw gegevens nemen voordat u een apparaat deactiveren.</span><span class="sxs-lookup"><span data-stu-id="107e8-126">If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="107e8-127">Deze cloudmomentopname met de kunt u alle gegevens in een later stadium te herstellen.</span><span class="sxs-lookup"><span data-stu-id="107e8-127">This cloud snapshot allows you to recover all the data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="107e8-128">Een apparaat deactiveren</span><span class="sxs-lookup"><span data-stu-id="107e8-128">Deactivate a device</span></span>

<span data-ttu-id="107e8-129">U kunt uw apparaat, moet u de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="107e8-129">To deactivate your device, perform the following steps.</span></span>

#### <a name="to-deactivate-the-device"></a><span data-ttu-id="107e8-130">Het apparaat deactiveren</span><span class="sxs-lookup"><span data-stu-id="107e8-130">To deactivate the device</span></span>

1. <span data-ttu-id="107e8-131">In uw service, gaat u naar **Management > apparaten**.</span><span class="sxs-lookup"><span data-stu-id="107e8-131">In your service, go to **Management > Devices**.</span></span> <span data-ttu-id="107e8-132">In de **apparaten** blade, klikt u op en selecteer het apparaat dat u wilt deactiveren.</span><span class="sxs-lookup"><span data-stu-id="107e8-132">In the **Devices** blade, click and select the device that you wish to deactivate.</span></span>
   
    ![Selecteer het apparaat te deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="107e8-134">In uw **apparaat dashboard** blade, klikt u op **... Meer** en selecteer in de lijst **deactiveren**.</span><span class="sxs-lookup"><span data-stu-id="107e8-134">In your **Device dashboard** blade, click **… More** and from the list, select **Deactivate**.</span></span>
   
    ![Klikt u op deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="107e8-136">In de **deactiveren** blade, typ de naam van het apparaat en klik vervolgens op **deactiveren**.</span><span class="sxs-lookup"><span data-stu-id="107e8-136">In the **Deactivate** blade, type the device name and then click **Deactivate**.</span></span> 
   
    ![Bevestig deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="107e8-138">Het proces deactiveren wordt gestart en duurt een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="107e8-138">The deactivate process starts and takes a few minutes to complete.</span></span>
   
    ![Deactiveren wordt uitgevoerd](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="107e8-140">Na de deactivering, de lijst met apparaten wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="107e8-140">After deactivation, the list of devices refreshes.</span></span>
   
    ![Volledige deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="107e8-142">Nu kunt u dit apparaat verwijderen.</span><span class="sxs-lookup"><span data-stu-id="107e8-142">You can now delete this device.</span></span>

## <a name="delete-the-device"></a><span data-ttu-id="107e8-143">Het apparaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="107e8-143">Delete the device</span></span>

<span data-ttu-id="107e8-144">Een apparaat moet eerst worden gedeactiveerd om het te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="107e8-144">A device has to be first deactivated to delete it.</span></span> <span data-ttu-id="107e8-145">Als u een apparaat verwijdert, wordt deze verwijderd uit de lijst met apparaten die zijn verbonden met de service.</span><span class="sxs-lookup"><span data-stu-id="107e8-145">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="107e8-146">De service kan niet langer dan de verwijderde apparaatinschrijvingsbeheerder beheren.</span><span class="sxs-lookup"><span data-stu-id="107e8-146">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="107e8-147">De gegevens die zijn gekoppeld aan het apparaat blijft echter in de cloud.</span><span class="sxs-lookup"><span data-stu-id="107e8-147">The data associated with the device however remains in the cloud.</span></span> <span data-ttu-id="107e8-148">Deze gegevens worden vervolgens kosten toenemen.</span><span class="sxs-lookup"><span data-stu-id="107e8-148">This data then accrues charges.</span></span>

<span data-ttu-id="107e8-149">Als u wilt verwijderen van het apparaat, moet u de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="107e8-149">To delete the device, perform the following steps.</span></span>

#### <a name="to-delete-the-device"></a><span data-ttu-id="107e8-150">Het apparaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="107e8-150">To delete the device</span></span>

1. <span data-ttu-id="107e8-151">In uw StorSimple-Apparaatbeheer gaat u naar **Management > apparaten**.</span><span class="sxs-lookup"><span data-stu-id="107e8-151">In your StorSimple Device Manager, go to **Management > Devices**.</span></span> <span data-ttu-id="107e8-152">In de **apparaten** blade, selecteer een gedeactiveerde apparaat dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="107e8-152">In the **Devices** blade, select a deactivated device that you wish to delete.</span></span>
2. <span data-ttu-id="107e8-153">In de **apparaat dashboard** blade, klikt u op **... Meer** en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="107e8-153">In the **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Selecteer het apparaat verwijderen](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="107e8-155">In de **verwijderen** blade, typ de naam van uw apparaat om te bevestigen en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="107e8-155">In the **Delete** blade, type the name of your device to confirm the deletion and then click **Delete**.</span></span> <span data-ttu-id="107e8-156">Als u het apparaat verwijdert, verwijdert niet de cloudgegevens die zijn gekoppeld aan het apparaat.</span><span class="sxs-lookup"><span data-stu-id="107e8-156">Deleting the device does not delete the cloud data associated with the device.</span></span> 
   
   ![De verwijdering bevestigen](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="107e8-158">De verwijdering wordt gestart en duurt een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="107e8-158">The deletion starts and takes a few minutes to complete.</span></span>
   
   ![Bezig met verwijderen](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="107e8-160">Nadat het apparaat wordt verwijderd, kunt u de bijgewerkte lijst met apparaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="107e8-160">After the device is deleted, you can view the updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="107e8-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="107e8-161">Next steps</span></span>

* <span data-ttu-id="107e8-162">Ga voor meer informatie over de failover naar [Failover en herstel na noodgevallen van uw virtuele StorSimple-matrix](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="107e8-162">For information on how to fail over, go to [Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="107e8-163">Voor meer informatie over het gebruik van de service Manager voor StorSimple-apparaat, gaat u naar [de Apparaatbeheer StorSimple-service gebruiken voor het beheren van uw virtuele StorSimple-matrix](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="107e8-163">To learn more about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

