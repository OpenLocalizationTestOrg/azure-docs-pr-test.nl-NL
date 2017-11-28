---
title: aaaDeactivate en verwijderen van een Microsoft Azure StorSimple virtuele matrix | Microsoft Docs
description: Hierin wordt beschreven hoe tooremove StorSimple-apparaat uit de service door het eerst deactiveren en vervolgens te verwijderen.
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
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="ce94f-103">Deactiveren en verwijderen van een virtueel StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="ce94f-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="ce94f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ce94f-104">Overview</span></span>

<span data-ttu-id="ce94f-105">Wanneer u een virtueel StorSimple-matrix deactiveert, verbreekt Hallo verbinding tussen Hallo-apparaat en Hallo bijbehorende Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="ce94f-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="ce94f-106">Deze zelfstudie wordt uitgelegd hoe:</span><span class="sxs-lookup"><span data-stu-id="ce94f-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="ce94f-107">Een apparaat deactiveren</span><span class="sxs-lookup"><span data-stu-id="ce94f-107">Deactivate a device</span></span> 
* <span data-ttu-id="ce94f-108">Een gedeactiveerde apparaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="ce94f-108">Delete a deactivated device</span></span>

<span data-ttu-id="ce94f-109">Hallo-informatie in dit artikel is van toepassing alleen tooStorSimple virtuele matrices.</span><span class="sxs-lookup"><span data-stu-id="ce94f-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="ce94f-110">Ga voor informatie over 8000-serie, toohow te[deactiveren of verwijderen van een apparaat](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="ce94f-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="ce94f-111">Wanneer toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="ce94f-111">When toodeactivate?</span></span>

<span data-ttu-id="ce94f-112">Deactivering is een permanente bewerking en kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ce94f-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="ce94f-113">U kunt een gedeactiveerde apparaat niet opnieuw registreren met Hallo StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="ce94f-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="ce94f-114">U kunt toodeactivate moet en verwijderen van een virtueel StorSimple-matrix in Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="ce94f-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="ce94f-115">**De geplande failover** : het apparaat online is en u toofail van plan bent op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="ce94f-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="ce94f-116">Als u van plan bent tooupgrade tooa groter apparaat, moet u mogelijk toofail via uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="ce94f-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="ce94f-117">Nadat Hallo Gegevenseigendom wordt overgedragen en Hallo failover voltooid is, wordt het bronvolume Hallo automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ce94f-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="ce94f-118">**Niet-geplande failover** : het apparaat offline is en u toofail dan Hallo-apparaat nodig.</span><span class="sxs-lookup"><span data-stu-id="ce94f-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="ce94f-119">Dit scenario optreden tijdens een noodgeval wanneer er een storing in Hallo datacenter en het primaire apparaat niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="ce94f-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="ce94f-120">U van plan bent toofail via Hallo apparaat tooa secundair apparaat.</span><span class="sxs-lookup"><span data-stu-id="ce94f-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="ce94f-121">Nadat Hallo Gegevenseigendom wordt overgedragen en Hallo failover voltooid is, wordt het bronvolume Hallo automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ce94f-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="ce94f-122">**Buiten gebruik stellen** : U wilt dat toodecommission Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="ce94f-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="ce94f-123">Hiervoor moet u toofirst Hallo-apparaat deactiveren en vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ce94f-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="ce94f-124">Wanneer u een apparaat deactiveert, u niet langer toegang tot alle gegevens die lokaal wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ce94f-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="ce94f-125">U kunt alleen toegang herstellen Hallo gegevens en opgeslagen in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="ce94f-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="ce94f-126">Als u tookeep Hallo apparaatgegevens na deactivering plant, moet u een cloudmomentopname van al uw gegevens nemen voordat u een apparaat deactiveren.</span><span class="sxs-lookup"><span data-stu-id="ce94f-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="ce94f-127">Deze cloudmomentopname met de kunt u toorecover alle gegevens in een later stadium Hallo.</span><span class="sxs-lookup"><span data-stu-id="ce94f-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="ce94f-128">Een apparaat deactiveren</span><span class="sxs-lookup"><span data-stu-id="ce94f-128">Deactivate a device</span></span>

<span data-ttu-id="ce94f-129">toodeactivate uw apparaat Hallo volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ce94f-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="ce94f-130">toodeactivate hello apparaat</span><span class="sxs-lookup"><span data-stu-id="ce94f-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="ce94f-131">Ga te in uw service**Management > apparaten**.</span><span class="sxs-lookup"><span data-stu-id="ce94f-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="ce94f-132">In Hallo **apparaten** blade, klikt u op en selecteer Hallo-apparaat dat u wenst dat toodeactivate.</span><span class="sxs-lookup"><span data-stu-id="ce94f-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Selecteer welk apparaat toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="ce94f-134">In uw **apparaat dashboard** blade, klikt u op **... Meer** en selecteer in de lijst Hallo **deactiveren**.</span><span class="sxs-lookup"><span data-stu-id="ce94f-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Klikt u op deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="ce94f-136">In Hallo **deactiveren** blade, type Hallo apparaatnaam en klik vervolgens op **deactiveren**.</span><span class="sxs-lookup"><span data-stu-id="ce94f-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Bevestig deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="ce94f-138">Hallo deactiveren proces gestart en duurt een paar minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ce94f-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Deactiveren wordt uitgevoerd](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="ce94f-140">Na de deactivering, Hallo lijst met apparaten wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="ce94f-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Volledige deactiveren](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="ce94f-142">Nu kunt u dit apparaat verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ce94f-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="ce94f-143">Hallo-apparaat verwijderen</span><span class="sxs-lookup"><span data-stu-id="ce94f-143">Delete hello device</span></span>

<span data-ttu-id="ce94f-144">Een apparaat heeft de eerste gedeactiveerde toodelete toobe deze.</span><span class="sxs-lookup"><span data-stu-id="ce94f-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="ce94f-145">Als u een apparaat verwijdert, wordt deze verwijderd uit Hallo lijst met apparaten verbonden toohello service.</span><span class="sxs-lookup"><span data-stu-id="ce94f-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="ce94f-146">Hallo-service kunt niet meer dan Hallo verwijderd apparaat beheren.</span><span class="sxs-lookup"><span data-stu-id="ce94f-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="ce94f-147">Hallo-gegevens die zijn gekoppeld met Hallo apparaat blijft echter in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="ce94f-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="ce94f-148">Deze gegevens worden vervolgens kosten toenemen.</span><span class="sxs-lookup"><span data-stu-id="ce94f-148">This data then accrues charges.</span></span>

<span data-ttu-id="ce94f-149">toodelete hello apparaat Hallo volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ce94f-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="ce94f-150">toodelete hello apparaat</span><span class="sxs-lookup"><span data-stu-id="ce94f-150">toodelete hello device</span></span>

1. <span data-ttu-id="ce94f-151">Gaat u in uw StorSimple-Apparaatbeheer te**Management > apparaten**.</span><span class="sxs-lookup"><span data-stu-id="ce94f-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="ce94f-152">In Hallo **apparaten** blade een gedeactiveerde apparaat dat u wenst dat toodelete selecteert.</span><span class="sxs-lookup"><span data-stu-id="ce94f-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="ce94f-153">In Hallo **apparaat dashboard** blade, klikt u op **... Meer** en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="ce94f-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Selecteer welk apparaat toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="ce94f-155">In Hallo **verwijderen** blade, type Hallo-naam van uw apparaat tooconfirm Hallo verwijderen en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="ce94f-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="ce94f-156">Verwijderen Hallo-apparaat verwijdert geen Hallo cloudgegevens die zijn gekoppeld aan het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ce94f-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![De verwijdering bevestigen](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="ce94f-158">Hallo verwijdering wordt gestart en duurt een paar minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ce94f-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Bezig met verwijderen](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="ce94f-160">Nadat het Hallo-apparaat wordt verwijderd, kunt u Hallo bijgewerkt lijst met apparaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="ce94f-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce94f-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ce94f-161">Next steps</span></span>

* <span data-ttu-id="ce94f-162">Voor meer informatie over toofail over te gaan[Failover en herstel na noodgevallen van uw virtuele StorSimple-matrix](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="ce94f-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="ce94f-163">toolearn informatie over hoe toouse Hallo Apparaatbeheer StorSimple-service, gaan te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw virtuele StorSimple-matrix](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ce94f-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

