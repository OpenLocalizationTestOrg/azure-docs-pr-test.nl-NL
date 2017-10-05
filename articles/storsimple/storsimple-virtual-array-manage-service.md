---
title: Service Manager voor StorSimple-apparaat implementeren | Microsoft Docs
description: Wordt uitgelegd hoe u maken en verwijderen van de service Manager voor StorSimple-apparaat in de Azure portal en wordt beschreven hoe u de serviceregistratiesleutel beheren.
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
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="b56af-103">Implementeer de service Manager voor StorSimple-apparaat voor virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="b56af-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="b56af-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b56af-104">Overview</span></span>

<span data-ttu-id="b56af-105">De StorSimple-apparaat Manager-service wordt uitgevoerd in Microsoft Azure en verbinding maakt met meerdere StorSimple-apparaten.</span><span class="sxs-lookup"><span data-stu-id="b56af-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="b56af-106">Nadat u de service hebt gemaakt, kunt u deze kunt gebruiken voor het beheren van de apparaten uit de Microsoft Azure-portal uitgevoerd in een browser.</span><span class="sxs-lookup"><span data-stu-id="b56af-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="b56af-107">Hiermee kunt u voor het bewaken van de apparaten die zijn verbonden met de service Manager voor StorSimple-apparaat vanaf een centrale locatie, waardoor administratieve last voor het minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="b56af-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="b56af-108">De algemene taken met betrekking tot een service Manager voor StorSimple-apparaat zijn:</span><span class="sxs-lookup"><span data-stu-id="b56af-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="b56af-109">Een service maken</span><span class="sxs-lookup"><span data-stu-id="b56af-109">Create a service</span></span>
* <span data-ttu-id="b56af-110">Een service verwijderen</span><span class="sxs-lookup"><span data-stu-id="b56af-110">Delete a service</span></span>
* <span data-ttu-id="b56af-111">De serviceregistratiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="b56af-111">Get the service registration key</span></span>
* <span data-ttu-id="b56af-112">Opnieuw genereren van de serviceregistratiesleutel</span><span class="sxs-lookup"><span data-stu-id="b56af-112">Regenerate the service registration key</span></span>

<span data-ttu-id="b56af-113">Deze zelfstudie wordt beschreven hoe elk van de voorgaande taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b56af-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="b56af-114">De informatie in dit artikel is alleen van toepassing op virtuele StorSimple-matrices.</span><span class="sxs-lookup"><span data-stu-id="b56af-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="b56af-115">Voor meer informatie over StorSimple 8000-serie gaat u naar [een StorSimple Manager-service implementeren](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="b56af-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="b56af-116">Een service maken</span><span class="sxs-lookup"><span data-stu-id="b56af-116">Create a service</span></span>

<span data-ttu-id="b56af-117">Voor het maken van een service, moet u beschikken over:</span><span class="sxs-lookup"><span data-stu-id="b56af-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="b56af-118">Een abonnement met een Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="b56af-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="b56af-119">Een actieve Microsoft Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="b56af-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="b56af-120">De informatie die wordt gebruikt voor toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="b56af-120">The billing information that is used for access management</span></span>

<span data-ttu-id="b56af-121">U kunt ook kiezen voor het genereren van een opslagaccount bij het maken van de service.</span><span class="sxs-lookup"><span data-stu-id="b56af-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="b56af-122">Een enkele service kunt meerdere apparaten beheren.</span><span class="sxs-lookup"><span data-stu-id="b56af-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="b56af-123">Een apparaat niet kan echter meerdere services omvatten.</span><span class="sxs-lookup"><span data-stu-id="b56af-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="b56af-124">Een grote onderneming kan meerdere exemplaren van de service te werken met verschillende abonnementen behoren, organisaties of zelfs implementatie locaties hebben.</span><span class="sxs-lookup"><span data-stu-id="b56af-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="b56af-125">U moet afzonderlijke exemplaren van StorSimple-apparaat Manager-service voor het beheren van apparaten voor StorSimple 8000 serie en virtuele StorSimple-matrices.</span><span class="sxs-lookup"><span data-stu-id="b56af-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="b56af-126">Voer de volgende stappen uit voor het maken van een service.</span><span class="sxs-lookup"><span data-stu-id="b56af-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="b56af-127">Een service verwijderen</span><span class="sxs-lookup"><span data-stu-id="b56af-127">Delete a service</span></span>

<span data-ttu-id="b56af-128">Zorg voordat u een service hebt verwijderd, dat geen verbonden apparaten wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b56af-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="b56af-129">Als de service gebruikt wordt, schakelt u verbonden apparaten.</span><span class="sxs-lookup"><span data-stu-id="b56af-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="b56af-130">De bewerking deactiveren server de verbinding tussen het apparaat en de service, maar behouden van de apparaatgegevens in de cloud.</span><span class="sxs-lookup"><span data-stu-id="b56af-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b56af-131">Een service wordt verwijderd, de bewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b56af-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="b56af-132">Elk apparaat dat is met de service moet worden de fabrieksinstellingen voordat deze kan worden gebruikt met een andere service.</span><span class="sxs-lookup"><span data-stu-id="b56af-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="b56af-133">In dit scenario wordt de lokale gegevens op het apparaat, evenals de configuratie niet verloren.</span><span class="sxs-lookup"><span data-stu-id="b56af-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="b56af-134">Voer de volgende stappen uit om een service te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b56af-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="b56af-135">Een service verwijderen</span><span class="sxs-lookup"><span data-stu-id="b56af-135">To delete a service</span></span>

1. <span data-ttu-id="b56af-136">Ga naar **alle resources**.</span><span class="sxs-lookup"><span data-stu-id="b56af-136">Go to **All resources**.</span></span> <span data-ttu-id="b56af-137">Zoek uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="b56af-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="b56af-138">Selecteer de service die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b56af-138">Select the service that you wish to delete.</span></span>
   
    ![Selecteer de service verwijderen](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="b56af-140">Ga naar uw servicedashboard om te controleren of er zijn geen apparaten die zijn verbonden met de service.</span><span class="sxs-lookup"><span data-stu-id="b56af-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="b56af-141">Als er geen apparaten die zijn geregistreerd met deze service zijn, ziet u ook een bannerbericht naar het effect.</span><span class="sxs-lookup"><span data-stu-id="b56af-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="b56af-142">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b56af-142">Click **Delete**.</span></span>
   
    ![Verwijderen van de service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="b56af-144">Wanneer u om bevestiging gevraagd, klikt u op **Ja** in het bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b56af-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![Service verwijderen bevestigen](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="b56af-146">Duurt enkele minuten duren voordat de service moet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b56af-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="b56af-147">Nadat de service is verwijderd, wordt u gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="b56af-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![Geslaagde service verwijderen](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="b56af-149">De lijst met services wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="b56af-149">The list of services will be refreshed.</span></span>

 ![Bijgewerkte lijst met services](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="b56af-151">De serviceregistratiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="b56af-151">Get the service registration key</span></span>
<span data-ttu-id="b56af-152">Nadat u een service hebt gemaakt, moet u uw StorSimple-apparaat registreren bij de service.</span><span class="sxs-lookup"><span data-stu-id="b56af-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="b56af-153">Voor het registreren van uw eerste StorSimple-apparaat, moet u de serviceregistratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="b56af-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="b56af-154">Om extra apparaten registreren met een bestaande StorSimple-service, moet u zowel de registratiesleutel als de gegevensversleutelingssleutel van service (die is gegenereerd op de eerste apparaat tijdens de registratie).</span><span class="sxs-lookup"><span data-stu-id="b56af-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="b56af-155">Zie voor meer informatie over de gegevensversleutelingssleutel van service [StorSimple security](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="b56af-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="b56af-156">U kunt de registratiesleutel ophalen door het openen van de **sleutels** blade voor uw service.</span><span class="sxs-lookup"><span data-stu-id="b56af-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="b56af-157">Voer de volgende stappen uit om de serviceregistratiesleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="b56af-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="b56af-158">De serviceregistratiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="b56af-158">To get the service registration key</span></span>
1. <span data-ttu-id="b56af-159">In de **StorSimple Apparaatbeheer** blade, gaat u naar **Management &gt;**  **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="b56af-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![De blade Sleutels](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="b56af-161">In de **sleutels** blade een serviceregistratiesleutel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b56af-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="b56af-162">Kopieer de registratiesleutel met behulp van het pictogram kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b56af-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="b56af-163">Houd de serviceregistratiesleutel op een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="b56af-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="b56af-164">U moet deze sleutel, evenals de gegevensversleutelingssleutel service, extra apparaten registreren bij deze service.</span><span class="sxs-lookup"><span data-stu-id="b56af-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="b56af-165">Nadat de serviceregistratiesleutel, moet u uw apparaat via de Windows PowerShell voor StorSimple-interface configureren.</span><span class="sxs-lookup"><span data-stu-id="b56af-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="b56af-166">Opnieuw genereren van de serviceregistratiesleutel</span><span class="sxs-lookup"><span data-stu-id="b56af-166">Regenerate the service registration key</span></span>
<span data-ttu-id="b56af-167">U moet een serviceregistratiesleutel genereren als u nodig zijn voor sleutel rotatie uitgevoerd of als de lijst met servicebeheerders is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b56af-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="b56af-168">Wanneer u de sleutel opnieuw genereren, wordt de nieuwe sleutel alleen gebruikt voor latere apparaten registreren.</span><span class="sxs-lookup"><span data-stu-id="b56af-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="b56af-169">De apparaten die al zijn geregistreerd, worden hierdoor niet beïnvloed door dit proces.</span><span class="sxs-lookup"><span data-stu-id="b56af-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="b56af-170">De volgende stappen voor het genereren van een serviceregistratiesleutel uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b56af-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="b56af-171">Opnieuw genereren van de serviceregistratiesleutel</span><span class="sxs-lookup"><span data-stu-id="b56af-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="b56af-172">In de **StorSimple Apparaatbeheer** blade, gaat u naar **Management &gt;**  **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="b56af-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![De blade Sleutels](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="b56af-174">In de **sleutels** blade, klikt u op **genereren**.</span><span class="sxs-lookup"><span data-stu-id="b56af-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![Klik op opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="b56af-176">In de **opnieuw genereren serviceregistratiesleutel** blade, Controleer de actie vereist als de sleutels opnieuw worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b56af-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="b56af-177">De volgende apparaten die zijn geregistreerd bij deze service gebruikt de nieuwe registratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="b56af-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="b56af-178">Klik op **genereren** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="b56af-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="b56af-179">U ontvangt een melding nadat de registratie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="b56af-179">You will be notified after the registration is complete.</span></span>
   
   ![Bevestig sleutel opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="b56af-181">Een nieuwe registratiecode van de service wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b56af-181">A new service registration key will appear.</span></span>
   
    ![Bevestig sleutel opnieuw genereren](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="b56af-183">Kopieer deze sleutel en sla het voor het registreren van nieuwe apparaten aan deze service.</span><span class="sxs-lookup"><span data-stu-id="b56af-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b56af-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b56af-184">Next steps</span></span>
* <span data-ttu-id="b56af-185">Meer informatie over hoe [aan de slag](storsimple-virtual-array-deploy1-portal-prep.md) met een virtueel StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="b56af-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="b56af-186">Meer informatie over hoe [beheren van uw StorSimple-apparaat](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="b56af-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

