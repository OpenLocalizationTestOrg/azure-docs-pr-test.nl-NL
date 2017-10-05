---
title: Een cloudservice automatisch schalen in de klassieke portal | Microsoft Docs
description: (klassiek) Informatie over het configureren van regels voor automatisch schalen voor een cloud service-web-rol of functie worker in Azure met behulp van de klassieke portal.
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
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="28531-103">Het automatisch schalen voor een Cloudservice in de klassieke portal configureren</span><span class="sxs-lookup"><span data-stu-id="28531-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="28531-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="28531-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="28531-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="28531-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="28531-106">U kunt instellingen voor automatische voor uw Webrol of functie worker configureren op de pagina schaal van de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="28531-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="28531-107">U kunt ook handmatig schalen in plaats van automatisch schalen op basis van regels.</span><span class="sxs-lookup"><span data-stu-id="28531-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="28531-108">Dit artikel is gericht op Cloud Service-web- en werkrollen rollen.</span><span class="sxs-lookup"><span data-stu-id="28531-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="28531-109">Wanneer u een virtuele machine (klassiek) rechtstreeks maakt, wordt deze gehost in een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="28531-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="28531-110">Sommige van deze informatie geldt voor deze typen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="28531-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="28531-111">Schalen van een beschikbaarheidsset van virtuele machines wordt alleen afgesloten ze in- of uitschakelen op basis van de scale-regels die u configureert.</span><span class="sxs-lookup"><span data-stu-id="28531-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="28531-112">Zie voor meer informatie over virtuele Machines en beschikbaarheidssets [de beschikbaarheid van virtuele Machines beheren](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28531-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="28531-113">U kunt de volgende informatie voordat u configureert voor uw toepassing schalen:</span><span class="sxs-lookup"><span data-stu-id="28531-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="28531-114">Schalen wordt beïnvloed door de belangrijkste informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="28531-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="28531-115">Grotere rolinstanties gebruik meer kernen.</span><span class="sxs-lookup"><span data-stu-id="28531-115">Larger role instances use more cores.</span></span> <span data-ttu-id="28531-116">U kunt een toepassing alleen binnen de limiet van kernen schalen voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="28531-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="28531-117">Bijvoorbeeld, Stel dat uw abonnement heeft een limiet van 20 kernen.</span><span class="sxs-lookup"><span data-stu-id="28531-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="28531-118">Als u een toepassing met twee middelgrote cloudservices (in totaal 4 kernen) uitvoert, kunt u alleen opschalen andere cloud service-implementaties in uw abonnement door de resterende 16 kernen.</span><span class="sxs-lookup"><span data-stu-id="28531-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="28531-119">Zie voor meer informatie over grootten [Cloud Service Sizes](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="28531-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="28531-120">U moet een wachtrij maken en deze koppelen aan een rol voordat u een toepassing op basis van een bericht drempelwaarde kunt schalen.</span><span class="sxs-lookup"><span data-stu-id="28531-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="28531-121">Zie voor meer informatie [het gebruik van de Queue Storage-Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="28531-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="28531-122">U kunt de resources die zijn gekoppeld aan uw cloudservice schalen.</span><span class="sxs-lookup"><span data-stu-id="28531-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="28531-123">Zie voor meer informatie over het koppelen van resources [procedure: een bron koppelen aan een cloudservice](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="28531-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="28531-124">Om hoge beschikbaarheid van uw toepassing, moet u ervoor zorgen dat deze wordt geïmplementeerd met twee of meer rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="28531-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="28531-125">Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="28531-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="28531-126">Planning schalen</span><span class="sxs-lookup"><span data-stu-id="28531-126">Schedule scaling</span></span>
<span data-ttu-id="28531-127">Standaard alle rollen niet op een specifiek schema.</span><span class="sxs-lookup"><span data-stu-id="28531-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="28531-128">Daarom instellingen gewijzigd van toepassing op alle tijden en alle dagen in het jaar.</span><span class="sxs-lookup"><span data-stu-id="28531-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="28531-129">Als u wilt, kunt u de installatie handmatig of automatisch schalen voor een van de volgende modi:</span><span class="sxs-lookup"><span data-stu-id="28531-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="28531-130">Weekdagen</span><span class="sxs-lookup"><span data-stu-id="28531-130">Weekdays</span></span>
* <span data-ttu-id="28531-131">Tijdens het weekend</span><span class="sxs-lookup"><span data-stu-id="28531-131">Weekends</span></span>
* <span data-ttu-id="28531-132">Week nachten</span><span class="sxs-lookup"><span data-stu-id="28531-132">Week nights</span></span>
* <span data-ttu-id="28531-133">Uitvoeren van de week</span><span class="sxs-lookup"><span data-stu-id="28531-133">Week mornings</span></span>
* <span data-ttu-id="28531-134">Specifieke datums</span><span class="sxs-lookup"><span data-stu-id="28531-134">Specific dates</span></span>
* <span data-ttu-id="28531-135">Specifiek datumbereik</span><span class="sxs-lookup"><span data-stu-id="28531-135">Specific date ranges</span></span>

<span data-ttu-id="28531-136">De instelling van de planning is geconfigureerd in de [klassieke Azure-portal](https://manage.windowsazure.com/) op de</span><span class="sxs-lookup"><span data-stu-id="28531-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="28531-137">**Cloudservices** > **\[uw cloudservice\]** > **Scale** > **\[productie of Staging\]**  pagina.</span><span class="sxs-lookup"><span data-stu-id="28531-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="28531-138">Klik op de **instellen van tijden waarop planning** knop voor elke rol die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="28531-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![Cloudservice automatisch schalen op basis van een planning][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="28531-140">Handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="28531-140">Manual scale</span></span>
<span data-ttu-id="28531-141">Op de **Scale** pagina, u kunt handmatig vergroten of verkleinen het aantal exemplaren in een cloudservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="28531-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="28531-142">Deze instelling is geconfigureerd voor elke planning die u hebt gemaakt of aan alle tijd als u een planning niet hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="28531-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="28531-143">In de [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op de naam van de cloudservice om het dashboard te openen.</span><span class="sxs-lookup"><span data-stu-id="28531-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="28531-144">Als u de cloudservice niet ziet, moet u mogelijk gewijzigd van **productie** naar **fasering** of vice versa.</span><span class="sxs-lookup"><span data-stu-id="28531-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="28531-145">Klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="28531-145">Click **Scale**.</span></span>
3. <span data-ttu-id="28531-146">Selecteer de planning die u wilt schalen opties voor het wijzigen.</span><span class="sxs-lookup"><span data-stu-id="28531-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="28531-147">*Geen geplande tijden* is de standaardwaarde als er geen schema's gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="28531-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="28531-148">Zoeken naar de **schaal op metriek** sectie en selecteer ****.</span><span class="sxs-lookup"><span data-stu-id="28531-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="28531-149">Dit is de standaardinstelling voor alle functies.</span><span class="sxs-lookup"><span data-stu-id="28531-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="28531-150">Elke rol in de cloudservice heeft een schuifregelaar voor het wijzigen van het aantal exemplaren moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="28531-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![De functie van een cloud-service handmatig schalen][manual_scale]
   
    <span data-ttu-id="28531-152">Als u meer exemplaren nodig hebt, moet u mogelijk wijzigen de [cloud van de grootte van de virtuele machine service](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="28531-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="28531-153">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="28531-153">Click **Save**.</span></span>  
   <span data-ttu-id="28531-154">Rolinstanties worden toegevoegd of verwijderd op basis van uw selecties.</span><span class="sxs-lookup"><span data-stu-id="28531-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="28531-155">Wanneer u ziet ![][tip_icon] de muis bewegen en u hulp over welke specifieke instelling komt.</span><span class="sxs-lookup"><span data-stu-id="28531-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="28531-156">Automatische scale - CPU</span><span class="sxs-lookup"><span data-stu-id="28531-156">Automatic scale - CPU</span></span>
<span data-ttu-id="28531-157">Deze modus wordt geschaald als het gemiddelde percentage van CPU-gebruik boven of onder de opgegeven drempelwaarden gaat.</span><span class="sxs-lookup"><span data-stu-id="28531-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="28531-158">Rolinstanties zijn gemaakt of verwijderd als dit gebeurt.</span><span class="sxs-lookup"><span data-stu-id="28531-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="28531-159">In de [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op de naam van de cloudservice om het dashboard te openen.</span><span class="sxs-lookup"><span data-stu-id="28531-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="28531-160">Als u de cloudservice niet ziet, moet u mogelijk gewijzigd van **productie** naar **fasering** of vice versa.</span><span class="sxs-lookup"><span data-stu-id="28531-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="28531-161">Klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="28531-161">Click **Scale**.</span></span>
3. <span data-ttu-id="28531-162">Selecteer de planning die u wilt schalen opties voor het wijzigen.</span><span class="sxs-lookup"><span data-stu-id="28531-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="28531-163">*Geen geplande tijden* is de standaardwaarde als er geen schema's gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="28531-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="28531-164">Zoeken naar de **schaal op metriek** sectie en selecteer **CPU**.</span><span class="sxs-lookup"><span data-stu-id="28531-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="28531-165">U kunt nu een minimum en maximum aantal rollen instanties, het doel CPU-gebruik (voor het activeren van een schaal van) en hoeveel exemplaren omhoog en omlaag schalen door configureren.</span><span class="sxs-lookup"><span data-stu-id="28531-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![De functie van een cloud-service schalen door cpu-belasting][cpu_scale]

> [!TIP]
> <span data-ttu-id="28531-167">Wanneer u ziet ![][tip_icon] de muis bewegen en u hulp over welke specifieke instelling komt.</span><span class="sxs-lookup"><span data-stu-id="28531-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="28531-168">Automatische scale - wachtrij</span><span class="sxs-lookup"><span data-stu-id="28531-168">Automatic scale - Queue</span></span>
<span data-ttu-id="28531-169">Deze modus wordt automatisch geschaald als het aantal berichten in een wachtrij boven of onder een bepaalde drempelwaarde vallen gaat.</span><span class="sxs-lookup"><span data-stu-id="28531-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="28531-170">Rolinstanties zijn gemaakt of verwijderd als dit gebeurt.</span><span class="sxs-lookup"><span data-stu-id="28531-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="28531-171">In de [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op de naam van de cloudservice om het dashboard te openen.</span><span class="sxs-lookup"><span data-stu-id="28531-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="28531-172">Als u de cloudservice niet ziet, moet u mogelijk gewijzigd van **productie** naar **fasering** of vice versa.</span><span class="sxs-lookup"><span data-stu-id="28531-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="28531-173">Klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="28531-173">Click **Scale**.</span></span>
3. <span data-ttu-id="28531-174">Zoeken naar de **schaal op metriek** sectie en selecteer **wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="28531-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="28531-175">U kunt nu een minimum en maximum aantal exemplaren van de functies, de wachtrij en het aantal Wachtrijberichten voor het verwerken voor elk exemplaar en hoeveel exemplaren omhoog en omlaag schalen door configureren.</span><span class="sxs-lookup"><span data-stu-id="28531-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![De functie van een cloud-service schalen door een berichtenwachtrij][queue_scale]

> [!TIP]
> <span data-ttu-id="28531-177">Wanneer u ziet ![][tip_icon] de muis bewegen en u hulp over welke specifieke instelling komt.</span><span class="sxs-lookup"><span data-stu-id="28531-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="28531-178">Gekoppelde resources schalen</span><span class="sxs-lookup"><span data-stu-id="28531-178">Scale linked resources</span></span>
<span data-ttu-id="28531-179">Vaak wanneer u een rol schalen, is het nuttig voor het schalen van de database die de toepassing ook wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="28531-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="28531-180">Als u de database een koppeling naar de cloudservice, kunt u de instellingen voor schalen voor die bron openen door te klikken op de koppeling.</span><span class="sxs-lookup"><span data-stu-id="28531-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="28531-181">In de [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op de naam van de cloudservice om het dashboard te openen.</span><span class="sxs-lookup"><span data-stu-id="28531-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="28531-182">Als u de cloudservice niet ziet, moet u mogelijk gewijzigd van **productie** naar **fasering** of vice versa.</span><span class="sxs-lookup"><span data-stu-id="28531-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="28531-183">Klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="28531-183">Click **Scale**.</span></span>
3. <span data-ttu-id="28531-184">Zoeken naar de **gekoppelde resources** sectie en klik op **scale voor deze database beheren**.</span><span class="sxs-lookup"><span data-stu-id="28531-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="28531-185">Als er geen een **gekoppelde resources** sectie u waarschijnlijk geen gekoppelde resources.</span><span class="sxs-lookup"><span data-stu-id="28531-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
