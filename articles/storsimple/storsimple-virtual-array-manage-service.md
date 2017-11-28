---
title: aaaDeploy StorSimple-apparaat Manager-service | Microsoft Docs
description: Legt uit hoe toocreate en delete Hallo Apparaatbeheer StorSimple-service in hello Azure-portal en beschrijft hoe toomanage serviceregistratiesleutel Hallo.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="8c73e-103">Hallo Apparaatbeheer StorSimple-service voor virtuele StorSimple-matrix implementeren</span><span class="sxs-lookup"><span data-stu-id="8c73e-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="8c73e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8c73e-104">Overview</span></span>

<span data-ttu-id="8c73e-105">Hallo StorSimple-apparaat Manager-service wordt uitgevoerd in Microsoft Azure en verbindt toomultiple StorSimple-apparaten.</span><span class="sxs-lookup"><span data-stu-id="8c73e-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="8c73e-106">Nadat u Hallo service maakt, kunt u dit toomanage Hallo apparaten Hallo Microsoft Azure portal wordt uitgevoerd in een browser gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8c73e-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="8c73e-107">Hiermee kunt u toomonitor alle Hallo-apparaten die verbonden toohello Apparaatbeheer StorSimple zijn-service vanaf een centrale locatie, waardoor administratieve last voor het minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="8c73e-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="8c73e-108">Hallo algemene taken gerelateerde tooa StorSimple-apparaat Manager-service zijn:</span><span class="sxs-lookup"><span data-stu-id="8c73e-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="8c73e-109">Een service maken</span><span class="sxs-lookup"><span data-stu-id="8c73e-109">Create a service</span></span>
* <span data-ttu-id="8c73e-110">Een service verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c73e-110">Delete a service</span></span>
* <span data-ttu-id="8c73e-111">Hallo-serviceregistratiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="8c73e-111">Get hello service registration key</span></span>
* <span data-ttu-id="8c73e-112">Hallo-serviceregistratiesleutel genereren</span><span class="sxs-lookup"><span data-stu-id="8c73e-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="8c73e-113">Deze zelfstudie wordt beschreven hoe tooperform van Hallo voorgaande taken.</span><span class="sxs-lookup"><span data-stu-id="8c73e-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="8c73e-114">Hallo informatie in dit artikel is van toepassing alleen tooStorSimple virtuele matrices.</span><span class="sxs-lookup"><span data-stu-id="8c73e-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="8c73e-115">Voor meer informatie over StorSimple 8000-serie gaat te[een StorSimple Manager-service implementeren](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="8c73e-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="8c73e-116">Een service maken</span><span class="sxs-lookup"><span data-stu-id="8c73e-116">Create a service</span></span>

<span data-ttu-id="8c73e-117">toocreate een service, moet u toohave:</span><span class="sxs-lookup"><span data-stu-id="8c73e-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="8c73e-118">Een abonnement met een Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="8c73e-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="8c73e-119">Een actieve Microsoft Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="8c73e-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="8c73e-120">Hallo factuurgegevens die wordt gebruikt voor toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="8c73e-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="8c73e-121">U kunt ook toogenerate een opslagaccount wanneer u Hallo service maakt.</span><span class="sxs-lookup"><span data-stu-id="8c73e-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="8c73e-122">Een enkele service kunt meerdere apparaten beheren.</span><span class="sxs-lookup"><span data-stu-id="8c73e-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="8c73e-123">Een apparaat niet kan echter meerdere services omvatten.</span><span class="sxs-lookup"><span data-stu-id="8c73e-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="8c73e-124">Een grote onderneming kan meerdere service-exemplaren toowork met verschillende abonnementen behoren, organisaties of zelfs implementatie locaties hebben.</span><span class="sxs-lookup"><span data-stu-id="8c73e-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="8c73e-125">U moet afzonderlijke exemplaren van het StorSimple-apparaat Manager service toomanage StorSimple 8000 series apparaten en virtuele StorSimple-matrices.</span><span class="sxs-lookup"><span data-stu-id="8c73e-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="8c73e-126">Volgende stappen toocreate een service Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8c73e-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="8c73e-127">Een service verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c73e-127">Delete a service</span></span>

<span data-ttu-id="8c73e-128">Zorg voordat u een service hebt verwijderd, dat geen verbonden apparaten wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8c73e-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="8c73e-129">Als het Hallo-service wordt gebruikt, schakelt u Hallo verbonden apparaten.</span><span class="sxs-lookup"><span data-stu-id="8c73e-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="8c73e-130">Hallo deactiveren bewerking Hallo verbinding tussen Hallo-apparaat en Hallo service-Server, maar Hallo apparaat-gegevens in de cloud Hallo behouden blijven.</span><span class="sxs-lookup"><span data-stu-id="8c73e-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c73e-131">Als een service is verwijderd, Hallo-bewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c73e-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="8c73e-132">Elk apparaat dat werd gebruikt Hallo-service moet toobe fabrieksinstellingen voordat deze kan worden gebruikt met een andere service.</span><span class="sxs-lookup"><span data-stu-id="8c73e-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="8c73e-133">In dit scenario Hallo lokale gegevens op het Hallo-apparaat, evenals Hallo-configuratie niet verloren.</span><span class="sxs-lookup"><span data-stu-id="8c73e-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="8c73e-134">Volgende stappen toodelete een service Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8c73e-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="8c73e-135">toodelete een service</span><span class="sxs-lookup"><span data-stu-id="8c73e-135">toodelete a service</span></span>

1. <span data-ttu-id="8c73e-136">Ga te**alle resources**.</span><span class="sxs-lookup"><span data-stu-id="8c73e-136">Go too**All resources**.</span></span> <span data-ttu-id="8c73e-137">Zoek uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="8c73e-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="8c73e-138">Selecteer desgewenst toodelete Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="8c73e-138">Select hello service that you wish toodelete.</span></span>
   
    ![Selecteer de service toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="8c73e-140">Ga tooyour service dashboard tooensure er zijn geen apparaten verbonden toohello service.</span><span class="sxs-lookup"><span data-stu-id="8c73e-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="8c73e-141">Als er geen apparaten die zijn geregistreerd met deze service zijn, ziet u ook een banner bericht toohello effect.</span><span class="sxs-lookup"><span data-stu-id="8c73e-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="8c73e-142">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="8c73e-142">Click **Delete**.</span></span>
   
    ![Verwijderen van de service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="8c73e-144">Wanneer u om bevestiging gevraagd, klikt u op **Ja** in Hallo bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8c73e-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Service verwijderen bevestigen](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="8c73e-146">Het kan enkele minuten duren voordat Hallo service toobe verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8c73e-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="8c73e-147">Na het Hallo is service verwijderd, u ontvangt een melding.</span><span class="sxs-lookup"><span data-stu-id="8c73e-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Geslaagde service verwijderen](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="8c73e-149">lijst met services Hello wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="8c73e-149">hello list of services will be refreshed.</span></span>

 ![Bijgewerkte lijst met services](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="8c73e-151">Hallo-serviceregistratiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="8c73e-151">Get hello service registration key</span></span>
<span data-ttu-id="8c73e-152">Nadat u een service hebt gemaakt, moet u tooregister uw StorSimple-apparaat met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="8c73e-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="8c73e-153">tooregister uw eerste StorSimple-apparaat, u moet Hallo serviceregistratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="8c73e-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="8c73e-154">tooregister extra apparaten met een bestaande StorSimple-service, moet u zowel de registratiesleutel Hallo en Hallo service gegevensversleutelingssleutel (die is gegenereerd op Hallo eerste apparaat tijdens de registratie).</span><span class="sxs-lookup"><span data-stu-id="8c73e-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="8c73e-155">Zie voor meer informatie over Hallo service gegevensversleutelingssleutel [StorSimple security](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="8c73e-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="8c73e-156">U kunt Hallo registratiesleutel ophalen door het openen van Hallo **sleutels** blade voor uw service.</span><span class="sxs-lookup"><span data-stu-id="8c73e-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="8c73e-157">Volgende stappen tooget hello serviceregistratiesleutel Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8c73e-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="8c73e-158">tooget hello serviceregistratiesleutel</span><span class="sxs-lookup"><span data-stu-id="8c73e-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="8c73e-159">In Hallo **StorSimple Apparaatbeheer** blade te gaan**Management &gt;**  **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="8c73e-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![De blade Sleutels](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="8c73e-161">In Hallo **sleutels** blade een serviceregistratiesleutel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8c73e-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="8c73e-162">Kopieer de registratiesleutel Hallo Hallo kopie pictogram.</span><span class="sxs-lookup"><span data-stu-id="8c73e-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="8c73e-163">Houd de serviceregistratiesleutel Hallo op een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="8c73e-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="8c73e-164">U moet deze sleutel, evenals Hallo service gegevensversleutelingssleutel, tooregister extra apparaten met deze service.</span><span class="sxs-lookup"><span data-stu-id="8c73e-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="8c73e-165">Nadat u hebt verkregen Hallo serviceregistratiesleutel, moet u tooconfigure uw apparaat via Hallo Windows PowerShell voor StorSimple-interface.</span><span class="sxs-lookup"><span data-stu-id="8c73e-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="8c73e-166">Hallo-serviceregistratiesleutel genereren</span><span class="sxs-lookup"><span data-stu-id="8c73e-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="8c73e-167">U moet een serviceregistratiesleutel tooregenerate als u vereiste tooperform sleutel worden gedraaid of als Hallo lijst servicebeheerders is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8c73e-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="8c73e-168">Wanneer u het Hallo-sleutel opnieuw genereren, wordt Hallo nieuwe sleutel alleen gebruikt voor latere apparaten registreren.</span><span class="sxs-lookup"><span data-stu-id="8c73e-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="8c73e-169">Hallo-apparaten die al zijn geregistreerd, worden hierdoor niet beïnvloed door dit proces.</span><span class="sxs-lookup"><span data-stu-id="8c73e-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="8c73e-170">Volgende stappen tooregenerate een serviceregistratiesleutel Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8c73e-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="8c73e-171">tooregenerate hello serviceregistratiesleutel</span><span class="sxs-lookup"><span data-stu-id="8c73e-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="8c73e-172">In Hallo **StorSimple Apparaatbeheer** blade te gaan**Management &gt;**  **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="8c73e-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![De blade Sleutels](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="8c73e-174">In Hallo **sleutels** blade, klikt u op **genereren**.</span><span class="sxs-lookup"><span data-stu-id="8c73e-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Klik op opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="8c73e-176">In Hallo **opnieuw genereren serviceregistratiesleutel** blade revisie Hallo-actie vereist wanneer hello sleutels opnieuw worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8c73e-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="8c73e-177">Alle Hallo latere apparaten die zijn geregistreerd bij deze service zal nieuwe registratiecode Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8c73e-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="8c73e-178">Klik op **genereren** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="8c73e-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="8c73e-179">U wordt gewaarschuwd als Hallo-registratie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="8c73e-179">You will be notified after hello registration is complete.</span></span>
   
   ![Bevestig sleutel opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="8c73e-181">Een nieuwe registratiecode van de service wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8c73e-181">A new service registration key will appear.</span></span>
   
    ![Bevestig sleutel opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="8c73e-183">Kopieer deze sleutel en sla het voor het registreren van nieuwe apparaten aan deze service.</span><span class="sxs-lookup"><span data-stu-id="8c73e-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c73e-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c73e-184">Next steps</span></span>
* <span data-ttu-id="8c73e-185">Meer informatie over hoe te[aan de slag](storsimple-virtual-array-deploy1-portal-prep.md) met een virtueel StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="8c73e-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="8c73e-186">Meer informatie over hoe te[beheren van uw StorSimple-apparaat](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="8c73e-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

