---
title: een cloudservice aaaAuto schalen in de klassieke portal Hallo | Microsoft Docs
description: (klassiek) Meer informatie over hoe toouse Hallo regels voor klassieke portal tooconfigure automatisch schalen voor een cloud service-Webrol of worker-rol in Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="2631c-103">Hoe tooconfigure automatisch schalen voor een Cloudservice in de klassieke portal Hallo</span><span class="sxs-lookup"><span data-stu-id="2631c-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2631c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2631c-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="2631c-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2631c-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="2631c-106">U kunt instellingen voor automatische voor uw Webrol of functie worker configureren op Hallo Scale pagina Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2631c-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="2631c-107">U kunt ook handmatig schalen in plaats van automatisch schalen op basis van regels.</span><span class="sxs-lookup"><span data-stu-id="2631c-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="2631c-108">Dit artikel is gericht op Cloud Service-web- en werkrollen rollen.</span><span class="sxs-lookup"><span data-stu-id="2631c-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="2631c-109">Wanneer u een virtuele machine (klassiek) rechtstreeks maakt, wordt deze gehost in een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="2631c-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="2631c-110">Sommige van deze informatie is van toepassing toothese typen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2631c-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="2631c-111">Schalen van een beschikbaarheidsset van virtuele machines wordt alleen afgesloten ze in- of uitschakelen op basis van Hallo scale regels die u configureert.</span><span class="sxs-lookup"><span data-stu-id="2631c-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="2631c-112">Zie voor meer informatie over virtuele Machines en beschikbaarheidssets [beheren Hallo beschikbaarheid van virtuele Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2631c-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="2631c-113">Hallo volgende informatie voordat u de schaal van uw toepassing configureren, moet u overwegen:</span><span class="sxs-lookup"><span data-stu-id="2631c-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="2631c-114">Schalen wordt beïnvloed door de belangrijkste informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="2631c-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="2631c-115">Grotere rolinstanties gebruik meer kernen.</span><span class="sxs-lookup"><span data-stu-id="2631c-115">Larger role instances use more cores.</span></span> <span data-ttu-id="2631c-116">U kunt een toepassing alleen binnen het Hallo-limiet van kernen schalen voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="2631c-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="2631c-117">Bijvoorbeeld, Stel dat uw abonnement heeft een limiet van 20 kernen.</span><span class="sxs-lookup"><span data-stu-id="2631c-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="2631c-118">Als u een toepassing met twee middelgrote cloudservices (in totaal 4 kernen) uitvoert, kunt u alleen opschalen andere cloud service-implementaties in uw abonnement door Hallo resterende 16 kernen.</span><span class="sxs-lookup"><span data-stu-id="2631c-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="2631c-119">Zie voor meer informatie over grootten [Cloud Service Sizes](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="2631c-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="2631c-120">U moet een wachtrij maken en deze koppelen aan een rol voordat u een toepassing op basis van een bericht drempelwaarde kunt schalen.</span><span class="sxs-lookup"><span data-stu-id="2631c-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="2631c-121">Zie voor meer informatie [hoe toouse Queue Storage-Service Hallo](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="2631c-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="2631c-122">U kunt de resources die gekoppeld tooyour zijn schalen cloudservice.</span><span class="sxs-lookup"><span data-stu-id="2631c-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="2631c-123">Zie voor meer informatie over het koppelen van resources [hoe: koppelen van een cloudservice voor resource tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="2631c-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="2631c-124">tooenable hoge beschikbaarheid van uw toepassing, moet u zorgen dat deze wordt geïmplementeerd met twee of meer rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="2631c-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="2631c-125">Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="2631c-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="2631c-126">Planning schalen</span><span class="sxs-lookup"><span data-stu-id="2631c-126">Schedule scaling</span></span>
<span data-ttu-id="2631c-127">Standaard alle rollen niet op een specifiek schema.</span><span class="sxs-lookup"><span data-stu-id="2631c-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="2631c-128">Daarom toepassing instellingen gewijzigd tooall tijdstippen en alle dagen in de loop Hallo jaar.</span><span class="sxs-lookup"><span data-stu-id="2631c-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="2631c-129">Als u wilt, kunt u handmatig of automatisch schalen voor een van de volgende modi Hallo kunt instellen:</span><span class="sxs-lookup"><span data-stu-id="2631c-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="2631c-130">Weekdagen</span><span class="sxs-lookup"><span data-stu-id="2631c-130">Weekdays</span></span>
* <span data-ttu-id="2631c-131">Tijdens het weekend</span><span class="sxs-lookup"><span data-stu-id="2631c-131">Weekends</span></span>
* <span data-ttu-id="2631c-132">Week nachten</span><span class="sxs-lookup"><span data-stu-id="2631c-132">Week nights</span></span>
* <span data-ttu-id="2631c-133">Uitvoeren van de week</span><span class="sxs-lookup"><span data-stu-id="2631c-133">Week mornings</span></span>
* <span data-ttu-id="2631c-134">Specifieke datums</span><span class="sxs-lookup"><span data-stu-id="2631c-134">Specific dates</span></span>
* <span data-ttu-id="2631c-135">Specifiek datumbereik</span><span class="sxs-lookup"><span data-stu-id="2631c-135">Specific date ranges</span></span>

<span data-ttu-id="2631c-136">Hallo planning instelling is geconfigureerd in Hallo [klassieke Azure-portal](https://manage.windowsazure.com/) op Hallo</span><span class="sxs-lookup"><span data-stu-id="2631c-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="2631c-137">**Cloudservices** > **\[uw cloudservice\]** > **Scale** > **\[productie of Staging\]**  pagina.</span><span class="sxs-lookup"><span data-stu-id="2631c-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="2631c-138">Klik op Hallo **instellen van tijden waarop planning** knop voor elke rol die u wilt dat toochange.</span><span class="sxs-lookup"><span data-stu-id="2631c-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Cloudservice automatisch schalen op basis van een planning][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="2631c-140">Handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="2631c-140">Manual scale</span></span>
<span data-ttu-id="2631c-141">Op Hallo **Scale** pagina, u kunt handmatig vergroten of verkleinen Hallo aantal exemplaren in een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="2631c-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="2631c-142">Deze instelling is geconfigureerd voor elke schema dat u hebt gemaakt of tooall tijd als u een planning niet hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2631c-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="2631c-143">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.</span><span class="sxs-lookup"><span data-stu-id="2631c-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="2631c-144">Als u de cloudservice niet ziet, moet u mogelijk toochange van **productie** te**fasering** of vice versa.</span><span class="sxs-lookup"><span data-stu-id="2631c-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="2631c-145">Klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="2631c-145">Click **Scale**.</span></span>
3. <span data-ttu-id="2631c-146">Hallo schema u opties voor schaling toochange wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="2631c-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="2631c-147">*Geen geplande tijden* is Hallo standaard als er geen schema's gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="2631c-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="2631c-148">Hallo zoeken **schaal op metriek** sectie en selecteer ****.</span><span class="sxs-lookup"><span data-stu-id="2631c-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="2631c-149">Dit is de standaardinstelling Hallo voor alle functies.</span><span class="sxs-lookup"><span data-stu-id="2631c-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="2631c-150">Elke rol in Hallo cloud-service heeft een schuifregelaar voor het wijzigen van het aantal exemplaren toouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="2631c-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![De functie van een cloud-service handmatig schalen][manual_scale]
   
    <span data-ttu-id="2631c-152">Als u meer exemplaren nodig hebt, moet u mogelijk toochange hello [cloud van de grootte van de virtuele machine service](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="2631c-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="2631c-153">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2631c-153">Click **Save**.</span></span>  
   <span data-ttu-id="2631c-154">Rolinstanties worden toegevoegd of verwijderd op basis van uw selecties.</span><span class="sxs-lookup"><span data-stu-id="2631c-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="2631c-155">Wanneer u ziet ![][tip_icon] uw tooit muis verplaatsen en u hulp over welke specifieke instelling komt.</span><span class="sxs-lookup"><span data-stu-id="2631c-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="2631c-156">Automatische scale - CPU</span><span class="sxs-lookup"><span data-stu-id="2631c-156">Automatic scale - CPU</span></span>
<span data-ttu-id="2631c-157">Deze modus wordt geschaald als Hallo gemiddelde percentage van CPU-gebruik boven of onder de opgegeven drempelwaarden gaat.</span><span class="sxs-lookup"><span data-stu-id="2631c-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="2631c-158">Rolinstanties zijn gemaakt of verwijderd als dit gebeurt.</span><span class="sxs-lookup"><span data-stu-id="2631c-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="2631c-159">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.</span><span class="sxs-lookup"><span data-stu-id="2631c-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="2631c-160">Als u de cloudservice niet ziet, moet u mogelijk toochange van **productie** te**fasering** of vice versa.</span><span class="sxs-lookup"><span data-stu-id="2631c-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="2631c-161">Klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="2631c-161">Click **Scale**.</span></span>
3. <span data-ttu-id="2631c-162">Hallo schema u opties voor schaling toochange wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="2631c-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="2631c-163">*Geen geplande tijden* is Hallo standaard als er geen schema's gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="2631c-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="2631c-164">Hallo zoeken **schaal op metriek** sectie en selecteer **CPU**.</span><span class="sxs-lookup"><span data-stu-id="2631c-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="2631c-165">U kunt nu een minimum en maximum aantal rollen instanties, Hallo doel CPU-gebruik (tootrigger een schaal van) en hoeveel exemplaren tooscale omhoog en omlaag door configureren.</span><span class="sxs-lookup"><span data-stu-id="2631c-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![De functie van een cloud-service schalen door cpu-belasting][cpu_scale]

> [!TIP]
> <span data-ttu-id="2631c-167">Wanneer u ziet ![][tip_icon] uw tooit muis verplaatsen en u hulp over welke specifieke instelling komt.</span><span class="sxs-lookup"><span data-stu-id="2631c-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="2631c-168">Automatische scale - wachtrij</span><span class="sxs-lookup"><span data-stu-id="2631c-168">Automatic scale - Queue</span></span>
<span data-ttu-id="2631c-169">Deze modus wordt automatisch geschaald als het aantal berichten in een wachtrij Hallo boven of onder een bepaalde drempelwaarde vallen gaat.</span><span class="sxs-lookup"><span data-stu-id="2631c-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="2631c-170">Rolinstanties zijn gemaakt of verwijderd als dit gebeurt.</span><span class="sxs-lookup"><span data-stu-id="2631c-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="2631c-171">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.</span><span class="sxs-lookup"><span data-stu-id="2631c-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="2631c-172">Als u de cloudservice niet ziet, moet u mogelijk toochange van **productie** te**fasering** of vice versa.</span><span class="sxs-lookup"><span data-stu-id="2631c-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="2631c-173">Klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="2631c-173">Click **Scale**.</span></span>
3. <span data-ttu-id="2631c-174">Hallo zoeken **schaal op metriek** sectie en selecteer **wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="2631c-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="2631c-175">U kunt nu een minimum en maximum aantal exemplaren van de functies, Hallo wachtrij en het aantal van de wachtrij berichten tooprocess voor elk exemplaar en hoeveel exemplaren tooscale omhoog en omlaag door configureren.</span><span class="sxs-lookup"><span data-stu-id="2631c-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![De functie van een cloud-service schalen door een berichtenwachtrij][queue_scale]

> [!TIP]
> <span data-ttu-id="2631c-177">Wanneer u ziet ![][tip_icon] uw tooit muis verplaatsen en u hulp over welke specifieke instelling komt.</span><span class="sxs-lookup"><span data-stu-id="2631c-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="2631c-178">Gekoppelde resources schalen</span><span class="sxs-lookup"><span data-stu-id="2631c-178">Scale linked resources</span></span>
<span data-ttu-id="2631c-179">Vaak wanneer u een rol schalen, is een nuttig tooscale Hallo database die Hallo toepassing ook wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2631c-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="2631c-180">Als u Hallo database toohello cloudservice koppelt, kunt u instellingen voor die bron schalen door te klikken op de desbetreffende koppeling Hallo Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="2631c-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="2631c-181">In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.</span><span class="sxs-lookup"><span data-stu-id="2631c-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="2631c-182">Als u de cloudservice niet ziet, moet u mogelijk toochange van **productie** te**fasering** of vice versa.</span><span class="sxs-lookup"><span data-stu-id="2631c-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="2631c-183">Klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="2631c-183">Click **Scale**.</span></span>
3. <span data-ttu-id="2631c-184">Hallo zoeken **gekoppelde resources** sectie en klik op **scale voor deze database beheren**.</span><span class="sxs-lookup"><span data-stu-id="2631c-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2631c-185">Als er geen een **gekoppelde resources** sectie u waarschijnlijk geen gekoppelde resources.</span><span class="sxs-lookup"><span data-stu-id="2631c-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
