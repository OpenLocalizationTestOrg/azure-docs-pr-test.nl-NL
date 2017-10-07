---
title: beheertaken voor aaaCommon cloud service | Microsoft Docs
description: Meer informatie over hoe toomanage cloud-services in hello Azure-portal. Deze voorbeelden hello Azure-portal gebruiken.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="887e4-104">Hoe tooManage Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="887e4-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="887e4-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="887e4-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="887e4-106">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="887e4-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="887e4-107">In Hallo **Cloudservices (klassiek)** gebied van hello Azure portal, kunt u de functie van een service of een implementatie bijwerken, promoveren van een gefaseerde implementatie tooproduction, resources tooyour cloudservice koppelen zodat u Hallo resource zien kunt afhankelijkheden en schaal Hallo resources samen en verwijder een cloudservice of een implementatie.</span><span class="sxs-lookup"><span data-stu-id="887e4-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="887e4-108">Meer informatie over hoe tooscale uw cloudservice beschikbaar is [hier](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="887e4-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="887e4-109">Procedure: een functieservice van de cloud of implementatie bijwerken</span><span class="sxs-lookup"><span data-stu-id="887e4-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="887e4-110">Als u tooupdate Hallo toepassingscode voor de cloudservice moet, gebruikt **Update** op Hallo cloud service-blade.</span><span class="sxs-lookup"><span data-stu-id="887e4-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="887e4-111">U kunt een enkele of alle functies bijwerken.</span><span class="sxs-lookup"><span data-stu-id="887e4-111">You can update a single role or all roles.</span></span> <span data-ttu-id="887e4-112">tooupdate, kunt u een nieuw servicepakket of het serviceconfiguratiebestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="887e4-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="887e4-113">In Hallo [Azure-portal][Azure portal], Hallo cloudservice u tooupdate wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="887e4-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="887e4-114">Deze stap wordt geopend blade Hallo cloud service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="887e4-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="887e4-115">Klik op Hallo blade Hallo **Update** knop.</span><span class="sxs-lookup"><span data-stu-id="887e4-115">In hello blade, click hello **Update** button.</span></span>

    ![Bijwerkknop](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="887e4-117">Hallo-implementatie met een nieuwe service-pakketbestand (.cspkg) en service-configuratiebestand (.cscfg) bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="887e4-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="887e4-119">**Eventueel** hello implementatielabel en Hallo storage-account bijwerken.</span><span class="sxs-lookup"><span data-stu-id="887e4-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="887e4-120">Als geen rollen hebt slechts één rolexemplaar, selecteert u Hallo **toch implementeren als een of meer rollen met één exemplaar** tooenable Hallo upgrade tooproceed.</span><span class="sxs-lookup"><span data-stu-id="887e4-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="887e4-121">Azure kan alleen garanderen van 99,95% servicebeschikbaarheid tijdens een cloud service-update als elke rol ten minste twee rolexemplaren (virtuele machines heeft).</span><span class="sxs-lookup"><span data-stu-id="887e4-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="887e4-122">Één virtuele machine verwerkt aanvragen van clients met twee rolexemplaren, terwijl andere hello wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="887e4-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="887e4-123">Controleer **implementatie Start** toohave Hallo update toegepast nadat de upload Hallo van Hallo-pakket is voltooid.</span><span class="sxs-lookup"><span data-stu-id="887e4-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="887e4-124">Klik op **OK** toobegin Hallo service bijwerken.</span><span class="sxs-lookup"><span data-stu-id="887e4-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="887e4-125">Procedure: een gefaseerde implementatie tooproduction voor implementaties toopromote wisselen</span><span class="sxs-lookup"><span data-stu-id="887e4-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="887e4-126">Als u besluit een nieuwe release van een cloudservice, fase toodeploy en testen van uw nieuwe release in uw cloud service-testomgeving.</span><span class="sxs-lookup"><span data-stu-id="887e4-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="887e4-127">Gebruik **wisselen** tooswitch Hallo URL's door welke Hallo twee implementaties worden aangepakt en een nieuwe release tooproduction promoveren.</span><span class="sxs-lookup"><span data-stu-id="887e4-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="887e4-128">U kunt implementaties van Hallo omwisselen **Cloudservices** pagina of het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="887e4-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="887e4-129">In Hallo [Azure-portal][Azure portal], Hallo cloudservice u tooupdate wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="887e4-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="887e4-130">Deze stap wordt geopend blade Hallo cloud service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="887e4-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="887e4-131">Klik op Hallo blade Hallo **wisselen** knop.</span><span class="sxs-lookup"><span data-stu-id="887e4-131">In hello blade, click hello **Swap** button.</span></span>

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="887e4-133">Hallo volgende bevestiging wordt gevraagd wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="887e4-133">hello following confirmation prompt opens.</span></span>

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="887e4-135">Nadat u informatie over het implementeren van Hallo controleren, klikt u op **OK** tooswap Hallo implementaties.</span><span class="sxs-lookup"><span data-stu-id="887e4-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="887e4-136">Hallo implementatie wisselen plaatsvindt snel omdat Hallo die wijzigingen alleen Hallo virtuele IP-adressen (VIP's heeft) voor Hallo-implementaties.</span><span class="sxs-lookup"><span data-stu-id="887e4-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="887e4-137">toosave compute-kosten, kunt u verwijderen Hallo staging-implementatie nadat u hebt gecontroleerd of uw productie-implementatie werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="887e4-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="887e4-138">Veelgestelde vragen over het wisselen van implementaties</span><span class="sxs-lookup"><span data-stu-id="887e4-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="887e4-139">**Wat zijn Hallo-vereisten voor implementaties wisselen?**</span><span class="sxs-lookup"><span data-stu-id="887e4-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="887e4-140">Er zijn twee belangrijke vereisten voor een geslaagde implementatie wisseling:</span><span class="sxs-lookup"><span data-stu-id="887e4-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="887e4-141">Als u toouse een statisch IP-adres voor de productiesite wilt, moet u één voor de faseringsite ook reserveren.</span><span class="sxs-lookup"><span data-stu-id="887e4-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="887e4-142">Anders mislukt de Hallo wisselen.</span><span class="sxs-lookup"><span data-stu-id="887e4-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="887e4-143">Alle exemplaren van uw rollen moeten worden uitgevoerd voordat u Hallo wisselen kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="887e4-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="887e4-144">U kunt controleren Hallo status van uw exemplaren in de blade overzicht Hallo Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="887e4-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="887e4-145">U kunt ook hello gebruiken [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) opdracht in Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="887e4-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="887e4-146">Gastbesturingssysteem updates en service operations herstel kan ook leiden tot implementatie worden verwisseld toofail.</span><span class="sxs-lookup"><span data-stu-id="887e4-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="887e4-147">Zie voor meer informatie [problemen met cloud service-implementatie oplossen](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="887e4-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="887e4-148">**Heeft een wisseling gevolgen voor de uitvaltijd voor de toepassing? Hoe moet ik verwerken?**</span><span class="sxs-lookup"><span data-stu-id="887e4-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="887e4-149">Zoals beschreven in de laatste sectie hello, is een wisseling implementatie doorgaans snelle omdat het een configuratiewijziging in hello Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="887e4-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="887e4-150">In sommige gevallen kan echter kunt tien of meer seconden duren en leiden tot tijdelijke verbindingsfouten.</span><span class="sxs-lookup"><span data-stu-id="887e4-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="887e4-151">toolimit impact tooyour klanten, Overweeg de implementatie van [client Pogingslogica](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="887e4-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="887e4-152">Procedure: een bronservice tooa-cloud koppelen</span><span class="sxs-lookup"><span data-stu-id="887e4-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="887e4-153">Hello Azure-portal is niet gekoppeld aan resources samen zoals Hallo huidige klassieke Azure-portal biedt.</span><span class="sxs-lookup"><span data-stu-id="887e4-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="887e4-154">In plaats daarvan implementeren aanvullende bronnen toohello dezelfde resourcegroep wordt gebruikt door Hallo Service in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="887e4-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="887e4-155">Hoe: implementaties en een cloudservice verwijderen</span><span class="sxs-lookup"><span data-stu-id="887e4-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="887e4-156">Voordat u een cloudservice verwijderen kunt, moet u elke bestaande implementatie verwijderen.</span><span class="sxs-lookup"><span data-stu-id="887e4-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="887e4-157">toosave compute-kosten, kunt u verwijderen Hallo staging-implementatie nadat u hebt gecontroleerd of uw productie-implementatie werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="887e4-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="887e4-158">U wordt gefactureerd voor compute-kosten voor geïmplementeerde rolexemplaren die zijn gestopt.</span><span class="sxs-lookup"><span data-stu-id="887e4-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="887e4-159">Gebruik Hallo procedure toodelete na een implementatie of uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="887e4-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="887e4-160">In Hallo [Azure-portal][Azure portal], Hallo cloudservice u toodelete wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="887e4-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="887e4-161">Deze stap wordt geopend blade Hallo cloud service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="887e4-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="887e4-162">Klik op Hallo blade Hallo **verwijderen** knop.</span><span class="sxs-lookup"><span data-stu-id="887e4-162">In hello blade, click hello **Delete** button.</span></span>

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="887e4-164">U kunt Hallo volledige in de cloudservice verwijderen door het controleren van **Cloud-service en implementaties** of kies een Hallo **productie-implementatie** of Hallo **voorbereide distributie**.</span><span class="sxs-lookup"><span data-stu-id="887e4-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="887e4-166">Klik op Hallo **verwijderen** knop Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="887e4-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="887e4-167">toodelete Hallo-cloudservice, klikt u op **cloudservice verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="887e4-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="887e4-168">Klik vervolgens op Hallo bevestiging wordt gevraagd, op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="887e4-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="887e4-169">Wanneer een cloudservice is verwijderd en uitgebreide bewaking is geconfigureerd, moet u Hallo gegevens handmatig verwijderen uit uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="887e4-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="887e4-170">Zie voor meer informatie over waar toofind metrische gegevens tabellen Hallo [dit](cloud-services-how-to-monitor.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="887e4-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="887e4-171">Hoe: meer informatie over mislukte implementaties</span><span class="sxs-lookup"><span data-stu-id="887e4-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="887e4-172">Hallo **overzicht** blade bevat een statusbalk Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="887e4-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="887e4-173">Als u op de balk hello, wordt een nieuwe blade wordt geopend en wordt alle informatie over de fout weergegeven.</span><span class="sxs-lookup"><span data-stu-id="887e4-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="887e4-174">Als het Hallo-implementatie bevat geen fouten, is Hallo informatie blade leeg.</span><span class="sxs-lookup"><span data-stu-id="887e4-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="887e4-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="887e4-176">Next steps</span></span>
* <span data-ttu-id="887e4-177">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="887e4-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="887e4-178">Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="887e4-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="887e4-179">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="887e4-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="887e4-180">Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="887e4-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
