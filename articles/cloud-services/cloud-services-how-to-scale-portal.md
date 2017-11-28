---
title: een cloudservice aaaAuto schalen in Hallo-portal | Microsoft Docs
description: Meer informatie over hoe toouse Hallo regels voor automatisch schalen portal tooconfigure voor een cloud service-Webrol of worker-rol in Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="30df2-103">Hoe tooconfigure automatisch schalen voor een Cloudservice in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="30df2-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30df2-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="30df2-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="30df2-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="30df2-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="30df2-106">Voorwaarden kunnen worden ingesteld voor een cloud service-werkrol die een schaal in- of opnieuw activeren.</span><span class="sxs-lookup"><span data-stu-id="30df2-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="30df2-107">Hallo voorwaarden voor het Hallo-rol kunnen worden gebaseerd op Hallo CPU, schijf of netwerkbelasting van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="30df2-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="30df2-108">U kunt ook een voorwaarde op basis van een bericht wachtrij of Hallo metric van sommige andere Azure-resource die is gekoppeld aan uw abonnement instellen.</span><span class="sxs-lookup"><span data-stu-id="30df2-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="30df2-109">Dit artikel is gericht op Cloud Service-web- en werkrollen rollen.</span><span class="sxs-lookup"><span data-stu-id="30df2-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="30df2-110">Wanneer u een virtuele machine (klassiek) rechtstreeks maakt, wordt deze gehost in een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="30df2-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="30df2-111">U kunt een standaard virtuele machine schalen door te koppelen met een [beschikbaarheidsset](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) en handmatig inschakelen of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="30df2-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="30df2-112">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="30df2-112">Considerations</span></span>
<span data-ttu-id="30df2-113">Hallo volgende informatie voordat u de schaal van uw toepassing configureren, moet u overwegen:</span><span class="sxs-lookup"><span data-stu-id="30df2-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="30df2-114">Schalen wordt beïnvloed door de belangrijkste informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="30df2-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="30df2-115">Grotere rolinstanties gebruik meer kernen.</span><span class="sxs-lookup"><span data-stu-id="30df2-115">Larger role instances use more cores.</span></span> <span data-ttu-id="30df2-116">U kunt een toepassing alleen binnen het Hallo-limiet van kernen schalen voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="30df2-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="30df2-117">Bijvoorbeeld, Stel dat uw abonnement heeft een limiet van 20 kernen.</span><span class="sxs-lookup"><span data-stu-id="30df2-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="30df2-118">Als u een toepassing met twee middelgrote cloudservices (in totaal 4 kernen) uitvoert, kunt u alleen opschalen andere cloud service-implementaties in uw abonnement door Hallo resterende 16 kernen.</span><span class="sxs-lookup"><span data-stu-id="30df2-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="30df2-119">Zie voor meer informatie over grootten [Cloud Service Sizes](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="30df2-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="30df2-120">U kunt schalen op basis van een wachtrij bericht drempelwaarde.</span><span class="sxs-lookup"><span data-stu-id="30df2-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="30df2-121">Voor meer informatie over het toouse wachtrijen, Zie [hoe toouse Queue Storage-Service Hallo](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="30df2-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="30df2-122">U kunt ook andere resources zijn gekoppeld aan uw abonnement schalen.</span><span class="sxs-lookup"><span data-stu-id="30df2-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="30df2-123">tooenable hoge beschikbaarheid van uw toepassing, moet u zorgen dat deze wordt geïmplementeerd met twee of meer rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="30df2-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="30df2-124">Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="30df2-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="30df2-125">Waar schaal bevindt</span><span class="sxs-lookup"><span data-stu-id="30df2-125">Where scale is located</span></span>
<span data-ttu-id="30df2-126">Nadat u uw cloudservice selecteert, moet u Hallo cloud service blade zichtbaar hebben.</span><span class="sxs-lookup"><span data-stu-id="30df2-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="30df2-127">Op Hallo cloud service blade op Hallo **rollen en instanties** tegel, selecteer Hallo-naam van de cloudservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="30df2-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="30df2-128">**BELANGRIJKE**: Zorg ervoor dat tooclick Hallo cloud service rol, niet Hallo rolinstantie die lager is dan het Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="30df2-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="30df2-129">Selecteer Hallo **scale** tegel.</span><span class="sxs-lookup"><span data-stu-id="30df2-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="30df2-130">Automatische schaal</span><span class="sxs-lookup"><span data-stu-id="30df2-130">Automatic scale</span></span>
<span data-ttu-id="30df2-131">U kunt instellingen voor een rol configureren met de twee modi **handmatige** of **automatische**.</span><span class="sxs-lookup"><span data-stu-id="30df2-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="30df2-132">Handmatige is zoals u zou verwachten, instellen van Hallo absolute telling van exemplaren.</span><span class="sxs-lookup"><span data-stu-id="30df2-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="30df2-133">Automatische kunt u echter tooset regels die hoe en door het veel u bepalen wordt geschaald.</span><span class="sxs-lookup"><span data-stu-id="30df2-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="30df2-134">Set Hallo **schalen door** te optie**planning en prestaties regels**.</span><span class="sxs-lookup"><span data-stu-id="30df2-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![Cloud services-schaalinstellingen met profiel en de regel](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="30df2-136">Een bestaand profiel.</span><span class="sxs-lookup"><span data-stu-id="30df2-136">An existing profile.</span></span>
2. <span data-ttu-id="30df2-137">Een regel voor Hallo bovenliggende profiel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="30df2-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="30df2-138">Voeg een ander profiel.</span><span class="sxs-lookup"><span data-stu-id="30df2-138">Add another profile.</span></span>

<span data-ttu-id="30df2-139">Selecteer **profiel**.</span><span class="sxs-lookup"><span data-stu-id="30df2-139">Select **Add Profile**.</span></span> <span data-ttu-id="30df2-140">Hallo profiel bepaalt welke modus gewenste toouse voor Hallo schaal: **altijd**, **terugkeerpatroon**, **vaste datum**.</span><span class="sxs-lookup"><span data-stu-id="30df2-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="30df2-141">Nadat u hebt geconfigureerd profiel Hallo en regels, selecteert u Hallo **opslaan** pictogram Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="30df2-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="30df2-142">Profiel</span><span class="sxs-lookup"><span data-stu-id="30df2-142">Profile</span></span>
<span data-ttu-id="30df2-143">Hallo profiel stelt minimum en maximum aantal exemplaren voor Hallo schalen en ook als het bereik van deze actief is.</span><span class="sxs-lookup"><span data-stu-id="30df2-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="30df2-144">**Altijd**</span><span class="sxs-lookup"><span data-stu-id="30df2-144">**Always**</span></span>

    <span data-ttu-id="30df2-145">Bewaar dit bereik van de exemplaren beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="30df2-145">Always keep this range of instances available.</span></span>  

    ![Cloudservice, die altijd schalen](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="30df2-147">**Terugkeerpatroon**</span><span class="sxs-lookup"><span data-stu-id="30df2-147">**Recurrence**</span></span>

    <span data-ttu-id="30df2-148">Kies een set van de dagen van Hallo week tooscale.</span><span class="sxs-lookup"><span data-stu-id="30df2-148">Choose a set of days of hello week tooscale.</span></span>

    ![Cloud-service schalen met een terugkerende planning](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="30df2-150">**Vaste datum**</span><span class="sxs-lookup"><span data-stu-id="30df2-150">**Fixed Date**</span></span>

    <span data-ttu-id="30df2-151">Een vaste datum bereik tooscale Hallo rol.</span><span class="sxs-lookup"><span data-stu-id="30df2-151">A fixed date range tooscale hello role.</span></span>

    ![CLoud-service schalen met een vaste datum](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="30df2-153">Nadat u hebt geconfigureerd profiel hello, selecteert u Hallo **OK** knop Hallo Hallo profiel blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="30df2-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="30df2-154">Regel</span><span class="sxs-lookup"><span data-stu-id="30df2-154">Rule</span></span>
<span data-ttu-id="30df2-155">Regels tooa profiel worden toegevoegd en vertegenwoordigen een voorwaarde waarmee Hallo schaal wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="30df2-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="30df2-156">Hallo regel trigger is gebaseerd op een waarde van de cloudservice hello (CPU-gebruik, schijfactiviteit of netwerkactiviteit) toowhich kunt u een waarde voor de voorwaarde toevoegen.</span><span class="sxs-lookup"><span data-stu-id="30df2-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="30df2-157">U kunt bovendien Hallo-geactiveerd op basis van een bericht wachtrij of Hallo metric van sommige andere Azure-resource die is gekoppeld aan uw abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="30df2-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="30df2-158">Nadat u de regel Hallo hebt geconfigureerd, selecteert u Hallo **OK** knop Hallo Hallo regel blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="30df2-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="30df2-159">Back-toomanual schaal</span><span class="sxs-lookup"><span data-stu-id="30df2-159">Back toomanual scale</span></span>
<span data-ttu-id="30df2-160">Navigeer toohello [schalen instellingen](#where-scale-is-located) en set Hallo **schalen door** optie te**aantal instanties dat ik handmatig invoeren**.</span><span class="sxs-lookup"><span data-stu-id="30df2-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![Cloud services-schaalinstellingen met profiel en de regel](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="30df2-162">Deze instelling verwijdert automatisch schalen uit Hallo-rol en vervolgens kunt u exemplaren Hallo rechtstreeks instellen.</span><span class="sxs-lookup"><span data-stu-id="30df2-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="30df2-163">optie voor Hallo schaal (handmatig of automatisch).</span><span class="sxs-lookup"><span data-stu-id="30df2-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="30df2-164">Een rol exemplaar schuifregelaar tooset Hallo exemplaren tooscale aan.</span><span class="sxs-lookup"><span data-stu-id="30df2-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="30df2-165">Exemplaren van Hallo rol tooscale aan.</span><span class="sxs-lookup"><span data-stu-id="30df2-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="30df2-166">Nadat u de schaalinstellingen Hallo hebt geconfigureerd, selecteert u Hallo **opslaan** pictogram Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="30df2-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
