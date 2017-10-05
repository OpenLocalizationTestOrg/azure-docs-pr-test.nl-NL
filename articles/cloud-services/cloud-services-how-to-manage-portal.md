---
title: Algemene beheertaken voor cloud-service | Microsoft Docs
description: Informatie over het beheren van cloudservices in de Azure portal. Deze voorbeelden worden de Azure portal gebruiken.
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
ms.openlocfilehash: 4650cebe18153e3b10bbec685a66a590348c99e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="95268-104">Cloudservices beheren</span><span class="sxs-lookup"><span data-stu-id="95268-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95268-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="95268-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="95268-106">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="95268-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="95268-107">In de **Cloudservices (klassiek)** gebied van de Azure portal, kunt u de functie van een service of een implementatie bijwerken, een gefaseerde implementatie naar productie promoten, resources koppelen aan uw cloudservice zodat u de bronafhankelijkheden ziet en de resources samen schalen en verwijdert u een cloudservice of een implementatie.</span><span class="sxs-lookup"><span data-stu-id="95268-107">In the **Cloud Services (classic)** area of the Azure portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="95268-108">Meer informatie over het schalen van uw cloudservice is beschikbaar [hier](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95268-108">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="95268-109">Procedure: een functieservice van de cloud of implementatie bijwerken</span><span class="sxs-lookup"><span data-stu-id="95268-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="95268-110">Als u de toepassingscode voor uw cloudservice bijwerken moet, gebruikt u **bijwerken** op de blade cloud-service.</span><span class="sxs-lookup"><span data-stu-id="95268-110">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="95268-111">U kunt een enkele of alle functies bijwerken.</span><span class="sxs-lookup"><span data-stu-id="95268-111">You can update a single role or all roles.</span></span> <span data-ttu-id="95268-112">Als u wilt bijwerken, kunt u een nieuw servicepakket of het serviceconfiguratiebestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="95268-112">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="95268-113">In de [Azure-portal][Azure portal], selecteer de cloudservice die u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="95268-113">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="95268-114">Deze stap wordt de cloud service-exemplaar blade geopend.</span><span class="sxs-lookup"><span data-stu-id="95268-114">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="95268-115">Klik op de blade de **Update** knop.</span><span class="sxs-lookup"><span data-stu-id="95268-115">In the blade, click the **Update** button.</span></span>

    ![Bijwerkknop](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="95268-117">Werk de implementatie met een nieuwe service-pakketbestand (.cspkg) en service-configuratiebestand (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="95268-117">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="95268-119">**Eventueel** bijwerken van het implementatielabel en het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="95268-119">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="95268-120">Als geen rollen slechts één rolexemplaar hebben, selecteert u de **toch implementeren als een of meer rollen met één exemplaar** inschakelen van de upgrade om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="95268-120">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="95268-121">Azure kan alleen garanderen van 99,95% servicebeschikbaarheid tijdens een cloud service-update als elke rol ten minste twee rolexemplaren (virtuele machines heeft).</span><span class="sxs-lookup"><span data-stu-id="95268-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="95268-122">Een virtuele machine verwerkt aanvragen van clients met twee rolexemplaren, terwijl de andere is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="95268-122">With two role instances, one virtual machine processes client requests while the other is updated.</span></span>

6. <span data-ttu-id="95268-123">Controleer **implementatie Start** om de update is toegepast, nadat het uploaden van het pakket is voltooid.</span><span class="sxs-lookup"><span data-stu-id="95268-123">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="95268-124">Klik op **OK** om te beginnen met het bijwerken van de service.</span><span class="sxs-lookup"><span data-stu-id="95268-124">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="95268-125">Hoe: wisselen implementaties voor een gefaseerde implementatie naar productie promoten</span><span class="sxs-lookup"><span data-stu-id="95268-125">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="95268-126">Als u beslist een nieuwe release van een cloudservice, fase implementeren en testen van uw nieuwe release in uw cloud service-testomgeving.</span><span class="sxs-lookup"><span data-stu-id="95268-126">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="95268-127">Gebruik **wisselen** overschakelen van de URL's waarmee de twee implementaties worden aangepakt en een nieuwe release naar productie promoten.</span><span class="sxs-lookup"><span data-stu-id="95268-127">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="95268-128">U kunt wisselen implementaties van de **Cloudservices** pagina of het dashboard.</span><span class="sxs-lookup"><span data-stu-id="95268-128">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="95268-129">In de [Azure-portal][Azure portal], selecteer de cloudservice die u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="95268-129">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="95268-130">Deze stap wordt de cloud service-exemplaar blade geopend.</span><span class="sxs-lookup"><span data-stu-id="95268-130">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="95268-131">Klik op de blade de **wisselen** knop.</span><span class="sxs-lookup"><span data-stu-id="95268-131">In the blade, click the **Swap** button.</span></span>

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="95268-133">Hiermee opent u de volgende bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="95268-133">The following confirmation prompt opens.</span></span>

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="95268-135">Nadat u de informatie over de implementatie controleren, klikt u op **OK** wisselen van de implementaties.</span><span class="sxs-lookup"><span data-stu-id="95268-135">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="95268-136">Het wisselen van de implementatie plaatsvindt snel omdat het enige dat waardoor het virtuele IP-adressen (VIP's) voor de implementaties.</span><span class="sxs-lookup"><span data-stu-id="95268-136">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="95268-137">Als u wilt opslaan compute-kosten, kunt u de staging-implementatie verwijderen nadat u hebt gecontroleerd of uw productie-implementatie werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="95268-137">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="95268-138">Veelgestelde vragen over het wisselen van implementaties</span><span class="sxs-lookup"><span data-stu-id="95268-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="95268-139">**Wat zijn de vereisten voor implementaties wisselen?**</span><span class="sxs-lookup"><span data-stu-id="95268-139">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="95268-140">Er zijn twee belangrijke vereisten voor een geslaagde implementatie wisseling:</span><span class="sxs-lookup"><span data-stu-id="95268-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="95268-141">Als u gebruiken een statische IP-adres voor de productiesite wilt, moet u één voor de faseringsite ook reserveren.</span><span class="sxs-lookup"><span data-stu-id="95268-141">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="95268-142">Anders werkt de wisseling niet.</span><span class="sxs-lookup"><span data-stu-id="95268-142">Otherwise, the swap fails.</span></span>

- <span data-ttu-id="95268-143">Alle exemplaren van uw rollen moeten worden uitgevoerd voordat u de swap kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="95268-143">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="95268-144">U kunt de status van uw exemplaren in de overzichtsblade van de Azure portal controleren.</span><span class="sxs-lookup"><span data-stu-id="95268-144">You can check the status of your instances in the overview blade of the Azure portal.</span></span> <span data-ttu-id="95268-145">U kunt ook de [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) opdracht in Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95268-145">Alternatively, you can use the [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="95268-146">Houd er rekening mee dat Gastbesturingssysteem updates en service operations herstel kan ook worden veroorzaakt worden verwisseld implementatie mislukken.</span><span class="sxs-lookup"><span data-stu-id="95268-146">Note that Guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="95268-147">Zie voor meer informatie [problemen met cloud service-implementatie oplossen](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="95268-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="95268-148">**Heeft een wisseling gevolgen voor de uitvaltijd voor de toepassing? Hoe moet ik verwerken?**</span><span class="sxs-lookup"><span data-stu-id="95268-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="95268-149">Zoals beschreven in de laatste sectie, is een wisseling implementatie doorgaans snelle omdat het een configuratiewijziging in de Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="95268-149">As described in the last section, a deployment swap is typically fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="95268-150">In sommige gevallen kan echter kunt tien of meer seconden duren en leiden tot tijdelijke verbindingsfouten.</span><span class="sxs-lookup"><span data-stu-id="95268-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="95268-151">Om te beperken van invloed op uw klanten, Overweeg de implementatie van [client Pogingslogica](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="95268-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="95268-152">Procedure: een bron koppelen aan een cloudservice</span><span class="sxs-lookup"><span data-stu-id="95268-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="95268-153">De Azure-portal niet is gekoppeld resources samen als de huidige klassieke Azure portal biedt.</span><span class="sxs-lookup"><span data-stu-id="95268-153">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="95268-154">In plaats daarvan implementeert u aanvullende bronnen voor dezelfde resourcegroep wordt gebruikt door de Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="95268-154">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="95268-155">Hoe: implementaties en een cloudservice verwijderen</span><span class="sxs-lookup"><span data-stu-id="95268-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="95268-156">Voordat u een cloudservice verwijderen kunt, moet u elke bestaande implementatie verwijderen.</span><span class="sxs-lookup"><span data-stu-id="95268-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="95268-157">Als u wilt opslaan compute-kosten, kunt u de staging-implementatie verwijderen nadat u hebt gecontroleerd of uw productie-implementatie werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="95268-157">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="95268-158">U wordt gefactureerd voor compute-kosten voor geïmplementeerde rolexemplaren die zijn gestopt.</span><span class="sxs-lookup"><span data-stu-id="95268-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="95268-159">Gebruik de volgende procedure om een implementatie of de cloudservice te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="95268-159">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="95268-160">In de [Azure-portal][Azure portal], selecteer de cloudservice die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="95268-160">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="95268-161">Deze stap wordt de cloud service-exemplaar blade geopend.</span><span class="sxs-lookup"><span data-stu-id="95268-161">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="95268-162">Klik op de blade de **verwijderen** knop.</span><span class="sxs-lookup"><span data-stu-id="95268-162">In the blade, click the **Delete** button.</span></span>

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="95268-164">U kunt de volledige in de cloud-service verwijderen door te controleren **Cloud-service en implementaties** of kies de **productie-implementatie** of de **voorbereide distributie**.</span><span class="sxs-lookup"><span data-stu-id="95268-164">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="95268-166">Klik op de **verwijderen** knop onderaan.</span><span class="sxs-lookup"><span data-stu-id="95268-166">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="95268-167">Als u wilt verwijderen van de cloudservice, klikt u op **cloudservice verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="95268-167">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="95268-168">Op de bevestiging wordt gevraagd, klikt u vervolgens **Ja**.</span><span class="sxs-lookup"><span data-stu-id="95268-168">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="95268-169">Wanneer een cloudservice is verwijderd en uitgebreide bewaking is geconfigureerd, moet u de gegevens handmatig verwijderen uit uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="95268-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account.</span></span> <span data-ttu-id="95268-170">Zie voor meer informatie over waar u het vinden van de metrische gegevens tabellen [dit](cloud-services-how-to-monitor.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="95268-170">For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="95268-171">Hoe: meer informatie over mislukte implementaties</span><span class="sxs-lookup"><span data-stu-id="95268-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="95268-172">De **overzicht** blade bevat een statusbalk aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="95268-172">The **Overview** blade has a status bar at the top.</span></span> <span data-ttu-id="95268-173">Wanneer u op de werkbalk klikt, wordt een nieuwe blade wordt geopend en wordt alle informatie over de fout weergegeven.</span><span class="sxs-lookup"><span data-stu-id="95268-173">When you click the bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="95268-174">Als de implementatie geen fouten bevat, wordt de blade informatie is leeg.</span><span class="sxs-lookup"><span data-stu-id="95268-174">If the deployment does not contain any errors, the information blade is blank.</span></span>

![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="95268-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95268-176">Next steps</span></span>
* <span data-ttu-id="95268-177">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95268-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="95268-178">Meer informatie over hoe [implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95268-178">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="95268-179">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95268-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="95268-180">Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95268-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
