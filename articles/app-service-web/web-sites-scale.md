---
title: aaaScale van een app in Azure | Microsoft Docs
description: Meer informatie over hoe tooscale van een app in Azure App Service tooadd capaciteit en onderdelen.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="2a674-103">Een app in Azure opschalen</span><span class="sxs-lookup"><span data-stu-id="2a674-103">Scale up an app in Azure</span></span>
<span data-ttu-id="2a674-104">Dit artikel ziet u hoe tooscale uw app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2a674-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="2a674-105">Er zijn twee werkstromen voor vergroten/verkleinen, scale-en scale-out en in dit artikel wordt uitgelegd Hallo opschaling van de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="2a674-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="2a674-106">[Omhoog schalen](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): ophalen van meer CPU, geheugen, schijfruimte en extra functies, zoals toegewezen virtuele machines (VM's), aangepaste domeinen en certificaten, sleuven, automatisch schalen en meer.</span><span class="sxs-lookup"><span data-stu-id="2a674-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="2a674-107">U opschalen door Hallo prijscategorie van de App Service-plan waartoe uw app behoort.</span><span class="sxs-lookup"><span data-stu-id="2a674-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="2a674-108">[Uitschalen](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): verhoog het aantal VM-exemplaren die uw app uitvoeren Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a674-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="2a674-109">U kunt uitschalen tooas veel als 20 exemplaren, afhankelijk van uw prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="2a674-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="2a674-110">[App Service-omgevingen](../app-service/app-service-app-service-environments-readme.md) in **Premium** laag wordt verder verhogen voor uw scale-out aantal too50 exemplaren.</span><span class="sxs-lookup"><span data-stu-id="2a674-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="2a674-111">Zie voor meer informatie over het uitbreiden van [aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="2a674-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="2a674-112">Hier vindt u out hoe toouse automatisch schalen, namelijk tooscale exemplaren automatisch op basis van vooraf gedefinieerde regels en schema's.</span><span class="sxs-lookup"><span data-stu-id="2a674-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="2a674-113">Hallo scale instellingen nemen alleen seconden tooapply en gelden voor alle apps in uw [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a674-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="2a674-114">Ze geen toochange u uw code nodig of uw toepassing opnieuw distribueren.</span><span class="sxs-lookup"><span data-stu-id="2a674-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="2a674-115">Zie voor meer informatie over het Hallo-prijzen en -functies van afzonderlijke App Service-abonnementen [App Service-prijsinformatie](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="2a674-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="2a674-116">Voordat u een App Service-plan van Hallo overschakelt **vrije** laag, moet u eerst Hallo verwijderen [bestedingslimieten](https://azure.microsoft.com/pricing/spending-limits/) voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a674-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="2a674-117">tooview of wijzig de opties voor uw Microsoft Azure App Service-abonnement, Zie [Microsoft Azure-abonnementen][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="2a674-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="2a674-118">Uw prijscategorie opschalen</span><span class="sxs-lookup"><span data-stu-id="2a674-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="2a674-119">Open in uw browser Hallo [Azure-portal][portal].</span><span class="sxs-lookup"><span data-stu-id="2a674-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="2a674-120">Klik op de blade van uw app **alle instellingen**, en klik vervolgens op **omhoog schalen**.</span><span class="sxs-lookup"><span data-stu-id="2a674-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Navigeer tooscale van uw app in Azure.][ChooseWHP]
3. <span data-ttu-id="2a674-122">Kies uw laag en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="2a674-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="2a674-123">Hallo **meldingen** tabblad knippert een groene **geslaagd** als Hallo-bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="2a674-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="2a674-124">Verwante bronnen schalen</span><span class="sxs-lookup"><span data-stu-id="2a674-124">Scale related resources</span></span>
<span data-ttu-id="2a674-125">Als uw app, is afhankelijk van andere services, zoals Azure SQL Database- of Azure Storage, kunt u ook die op basis van de behoeften van uw resources schalen.</span><span class="sxs-lookup"><span data-stu-id="2a674-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="2a674-126">Deze resources niet worden geschaald met Hallo App Service-abonnement en moeten afzonderlijk worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="2a674-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="2a674-127">In **Essentials**, klikt u op Hallo **resourcegroep** koppeling.</span><span class="sxs-lookup"><span data-stu-id="2a674-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![Verwante bronnen van uw Azure-app opschalen](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="2a674-129">In Hallo **samenvatting** deel uit van Hallo **resourcegroep** blade, klik op een resource die u tooscale wilt.</span><span class="sxs-lookup"><span data-stu-id="2a674-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="2a674-130">Hallo volgende schermafbeelding ziet u een resource van de SQL-Database en een Azure Storage-resource.</span><span class="sxs-lookup"><span data-stu-id="2a674-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Navigeer tooresource groep blade tooscale van uw app in Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="2a674-132">Voor een SQL-Database-resource, klikt u op **instellingen** > **prijscategorie** tooscale Hallo prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="2a674-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![Opschalen Hallo SQL-Database back-end voor uw app in Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="2a674-134">Kunt u ook inschakelen [geo-replicatie](../sql-database/sql-database-geo-replication-overview.md) voor uw exemplaar van SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="2a674-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="2a674-135">Voor een Azure Storage-resource, klikt u op **instellingen** > **configuratie** tooscale van uw opties voor opslag.</span><span class="sxs-lookup"><span data-stu-id="2a674-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![Opschalen hello Azure Storage-account die wordt gebruikt door uw app in Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="2a674-137">Meer informatie over functies voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2a674-137">Learn about developer features</span></span>
<span data-ttu-id="2a674-138">Afhankelijk van de Hallo prijscategorie, hello volgende ontwikkelaars functies zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="2a674-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="2a674-139">Bitness</span><span class="sxs-lookup"><span data-stu-id="2a674-139">Bitness</span></span>
* <span data-ttu-id="2a674-140">Hallo **Basic**, **standaard**, en **Premium** lagen ondersteuning bieden voor 64-bits en 32-bits toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2a674-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="2a674-141">Hallo **vrije** en **gedeelde** plan lagen ondersteunt alleen 32-bits toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2a674-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="2a674-142">Ondersteuning voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="2a674-142">Debugger support</span></span>
* <span data-ttu-id="2a674-143">Foutopsporing ondersteuning is beschikbaar voor Hallo **vrije**, **gedeelde**, en **Basic** modi op één verbinding per App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a674-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="2a674-144">Foutopsporing ondersteuning is beschikbaar voor Hallo **standaard** en **Premium** modi op vijf gelijktijdige verbindingen per App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a674-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="2a674-145">Meer informatie over andere functies</span><span class="sxs-lookup"><span data-stu-id="2a674-145">Learn about other features</span></span>
* <span data-ttu-id="2a674-146">Zie voor gedetailleerde informatie over alle functies in App Service Hallo resterende Hallo plannen, inclusief prijzen en -onderdelen van belang tooall gebruikers (met inbegrip van ontwikkelaars), [App Service-prijsinformatie](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="2a674-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="2a674-147">Als u wilt dat tooget gestart met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/) waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="2a674-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2a674-148">U hebt geen creditcard vereist en er bent nergens toe verplicht.</span><span class="sxs-lookup"><span data-stu-id="2a674-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="2a674-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a674-149">Next steps</span></span>
* <span data-ttu-id="2a674-150">tooget de slag met Azure, Zie [gratis proefversie van Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a674-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2a674-151">Voor informatie over prijzen, ondersteuning en SLA, gaat u naar Hallo koppelingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="2a674-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="2a674-152">Prijsinformatie voor gegevensoverdracht</span><span class="sxs-lookup"><span data-stu-id="2a674-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="2a674-153">Microsoft Azure-ondersteuningsplannen</span><span class="sxs-lookup"><span data-stu-id="2a674-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="2a674-154">Serviceovereenkomsten</span><span class="sxs-lookup"><span data-stu-id="2a674-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="2a674-155">Prijsinformatie voor SQL-Database</span><span class="sxs-lookup"><span data-stu-id="2a674-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="2a674-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="2a674-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="2a674-157">Prijsinformatie voor App Service</span><span class="sxs-lookup"><span data-stu-id="2a674-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="2a674-158">App Service prijsinformatie - SSL-verbindingen</span><span class="sxs-lookup"><span data-stu-id="2a674-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="2a674-159">Zie voor meer informatie over Azure App Service aanbevolen procedures voor het bouwen van een schaalbare en flexibele architectuur, inclusief [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a674-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="2a674-160">Zie voor video's over het schalen van App Service-apps Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="2a674-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="2a674-161">Wanneer Azure Websites - met Stefan Schackow tooScale</span><span class="sxs-lookup"><span data-stu-id="2a674-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="2a674-162">Automatische schaling van Azure Websites, CPU of geplande - met Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="2a674-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="2a674-163">Hoe Azure Websites schaal - met Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="2a674-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
