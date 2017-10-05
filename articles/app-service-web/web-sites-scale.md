---
title: Een app in Azure opschalen | Microsoft Docs
description: Informatie over het schalen van een app in Azure App Service-capaciteit en functies toevoegen.
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
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="474ef-103">Een app in Azure opschalen</span><span class="sxs-lookup"><span data-stu-id="474ef-103">Scale up an app in Azure</span></span>
<span data-ttu-id="474ef-104">In dit artikel laat zien hoe uw app schalen in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="474ef-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="474ef-105">Er zijn twee werkstromen voor vergroten/verkleinen, scale-en scale-out en in dit artikel wordt uitgelegd de schaal van een workflow.</span><span class="sxs-lookup"><span data-stu-id="474ef-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="474ef-106">[Omhoog schalen](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): ophalen van meer CPU, geheugen, schijfruimte en extra functies, zoals toegewezen virtuele machines (VM's), aangepaste domeinen en certificaten, sleuven, automatisch schalen en meer.</span><span class="sxs-lookup"><span data-stu-id="474ef-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="474ef-107">U opschalen door het wijzigen van de prijscategorie van de App Service-plan waartoe uw app behoort.</span><span class="sxs-lookup"><span data-stu-id="474ef-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="474ef-108">[Uitschalen](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): verhoog het aantal VM-exemplaren die uw app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="474ef-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="474ef-109">U kunt uitschalen naar maximaal 20 instanties, afhankelijk van uw prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="474ef-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="474ef-110">[App Service-omgevingen](../app-service/app-service-app-service-environments-readme.md) in **Premium** laag wordt het aantal scale-out op 50 exemplaren verder verhogen.</span><span class="sxs-lookup"><span data-stu-id="474ef-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="474ef-111">Zie voor meer informatie over het uitbreiden van [aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="474ef-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="474ef-112">U wordt er informatie over het gebruik van automatisch schalen, die is het aantal exemplaren automatisch op basis van vooraf gedefinieerde regels en schema's.</span><span class="sxs-lookup"><span data-stu-id="474ef-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="474ef-113">De scale-instellingen worden alleen seconden toe te passen en gelden voor alle apps in uw [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="474ef-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="474ef-114">Ze hoeft u uw code wijzigen of uw toepassing opnieuw distribueren.</span><span class="sxs-lookup"><span data-stu-id="474ef-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="474ef-115">Zie voor meer informatie over de prijzen en -functies van afzonderlijke App Service-abonnementen [App Service-prijsinformatie](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="474ef-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="474ef-116">Voordat u overschakelt van een App Service-abonnement van de **vrije** laag, moet u eerst verwijderen de [bestedingslimieten](https://azure.microsoft.com/pricing/spending-limits/) voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="474ef-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="474ef-117">Als u wilt weergeven of wijzigen van opties voor uw Microsoft Azure App Service-abonnement, Zie [Microsoft Azure-abonnementen][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="474ef-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="474ef-118">Uw prijscategorie opschalen</span><span class="sxs-lookup"><span data-stu-id="474ef-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="474ef-119">Open in uw browser de [Azure-portal][portal].</span><span class="sxs-lookup"><span data-stu-id="474ef-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="474ef-120">Klik op de blade van uw app **alle instellingen**, en klik vervolgens op **omhoog schalen**.</span><span class="sxs-lookup"><span data-stu-id="474ef-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Navigeer om te schalen van uw app in Azure.][ChooseWHP]
3. <span data-ttu-id="474ef-122">Kies uw laag en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="474ef-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="474ef-123">De **meldingen** tabblad knippert een groene **geslaagd** nadat de bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="474ef-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="474ef-124">Verwante bronnen schalen</span><span class="sxs-lookup"><span data-stu-id="474ef-124">Scale related resources</span></span>
<span data-ttu-id="474ef-125">Als uw app, is afhankelijk van andere services, zoals Azure SQL Database- of Azure Storage, kunt u ook die op basis van de behoeften van uw resources schalen.</span><span class="sxs-lookup"><span data-stu-id="474ef-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="474ef-126">Deze resources niet worden geschaald met het App Service-plan en moeten afzonderlijk worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="474ef-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="474ef-127">In **Essentials**, klikt u op de **resourcegroep** koppeling.</span><span class="sxs-lookup"><span data-stu-id="474ef-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Verwante bronnen van uw Azure-app opschalen](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="474ef-129">In de **samenvatting** deel uit van de **resourcegroep** blade, klik op een resource die u wilt schalen.</span><span class="sxs-lookup"><span data-stu-id="474ef-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="474ef-130">De volgende schermafbeelding ziet u een resource van de SQL-Database en een Azure Storage-resource.</span><span class="sxs-lookup"><span data-stu-id="474ef-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Navigeer naar de resourcegroepblade schalen van uw app in Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="474ef-132">Voor een SQL-Database-resource, klikt u op **instellingen** > **prijscategorie** de prijscategorie schalen.</span><span class="sxs-lookup"><span data-stu-id="474ef-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![De SQL-Database-back-end voor uw app in Azure opschalen](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="474ef-134">Kunt u ook inschakelen [geo-replicatie](../sql-database/sql-database-geo-replication-overview.md) voor uw exemplaar van SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="474ef-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="474ef-135">Voor een Azure Storage-resource, klikt u op **instellingen** > **configuratie** schalen van uw opties voor opslag.</span><span class="sxs-lookup"><span data-stu-id="474ef-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![De Azure Storage-account die wordt gebruikt door uw app in Azure opschalen](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="474ef-137">Meer informatie over functies voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="474ef-137">Learn about developer features</span></span>
<span data-ttu-id="474ef-138">De volgende functies voor ontwikkelaars zijn afhankelijk van de prijscategorie beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="474ef-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="474ef-139">Bitness</span><span class="sxs-lookup"><span data-stu-id="474ef-139">Bitness</span></span>
* <span data-ttu-id="474ef-140">De **Basic**, **standaard**, en **Premium** lagen ondersteuning bieden voor 64-bits en 32-bits toepassingen.</span><span class="sxs-lookup"><span data-stu-id="474ef-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="474ef-141">De **vrije** en **gedeelde** plan lagen ondersteunt alleen 32-bits toepassingen.</span><span class="sxs-lookup"><span data-stu-id="474ef-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="474ef-142">Ondersteuning voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="474ef-142">Debugger support</span></span>
* <span data-ttu-id="474ef-143">Foutopsporing ondersteuning is beschikbaar voor de **vrije**, **gedeelde**, en **Basic** modi op één verbinding per App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="474ef-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="474ef-144">Foutopsporing ondersteuning is beschikbaar voor de **standaard** en **Premium** modi op vijf gelijktijdige verbindingen per App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="474ef-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="474ef-145">Meer informatie over andere functies</span><span class="sxs-lookup"><span data-stu-id="474ef-145">Learn about other features</span></span>
* <span data-ttu-id="474ef-146">Zie voor gedetailleerde informatie over alle van de resterende functies in de App Service-abonnementen, met inbegrip van prijzen en onderdelen van belang zijn voor alle gebruikers (met inbegrip van ontwikkelaars), [App Service-prijsinformatie](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="474ef-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="474ef-147">Als u aan de slag met Azure App Service wilt voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/) waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="474ef-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="474ef-148">U hebt geen creditcard vereist en er bent nergens toe verplicht.</span><span class="sxs-lookup"><span data-stu-id="474ef-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="474ef-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="474ef-149">Next steps</span></span>
* <span data-ttu-id="474ef-150">Aan de slag met Azure Zie [gratis proefversie van Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="474ef-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="474ef-151">Ga naar de volgende koppelingen voor meer informatie over prijzen, ondersteuning en SLA.</span><span class="sxs-lookup"><span data-stu-id="474ef-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="474ef-152">Prijsinformatie voor gegevensoverdracht</span><span class="sxs-lookup"><span data-stu-id="474ef-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="474ef-153">Microsoft Azure-ondersteuningsplannen</span><span class="sxs-lookup"><span data-stu-id="474ef-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="474ef-154">Serviceovereenkomsten</span><span class="sxs-lookup"><span data-stu-id="474ef-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="474ef-155">Prijsinformatie voor SQL-Database</span><span class="sxs-lookup"><span data-stu-id="474ef-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="474ef-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="474ef-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="474ef-157">Prijsinformatie voor App Service</span><span class="sxs-lookup"><span data-stu-id="474ef-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="474ef-158">App Service prijsinformatie - SSL-verbindingen</span><span class="sxs-lookup"><span data-stu-id="474ef-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="474ef-159">Zie voor meer informatie over Azure App Service aanbevolen procedures voor het bouwen van een schaalbare en flexibele architectuur, inclusief [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="474ef-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="474ef-160">Zie de volgende bronnen voor video's over het schalen van App Service-apps:</span><span class="sxs-lookup"><span data-stu-id="474ef-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="474ef-161">Wanneer Azure Websites - met Stefan Schackow schalen</span><span class="sxs-lookup"><span data-stu-id="474ef-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="474ef-162">Automatische schaling van Azure Websites, CPU of geplande - met Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="474ef-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="474ef-163">Hoe Azure Websites schaal - met Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="474ef-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
