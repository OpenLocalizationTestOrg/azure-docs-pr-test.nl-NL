---
title: Azure portal toomanage aaaUse Azure-resources | Microsoft Docs
description: Azure portal en Azure Resource Manager toomanage uw resources gebruiken. Toont hoe toowork met dashboards toomonitor resources.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="b825a-104">Azure-resources via de portal beheren</span><span class="sxs-lookup"><span data-stu-id="b825a-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b825a-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b825a-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="b825a-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="b825a-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="b825a-107">Portal</span><span class="sxs-lookup"><span data-stu-id="b825a-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="b825a-108">REST API</span><span class="sxs-lookup"><span data-stu-id="b825a-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="b825a-109">Dit onderwerp wordt beschreven hoe toouse hello [Azure-portal](https://portal.azure.com) met [Azure Resource Manager](resource-group-overview.md) toomanage uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="b825a-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="b825a-110">toolearn over het implementeren van resources via de portal hello, Zie [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="b825a-111">Op dit moment ondersteunt niet elke service Hallo portal of de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b825a-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="b825a-112">Voor deze services, moet u toouse hello [klassieke portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b825a-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="b825a-113">Zie voor Hallo status van elke service, [Azure portal beschikbaarheid grafiek](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="b825a-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="b825a-114">Resourcegroepen beheren</span><span class="sxs-lookup"><span data-stu-id="b825a-114">Manage resource groups</span></span>

<span data-ttu-id="b825a-115">Een resourcegroep is een container met verwante resources voor een Azure-oplossing.</span><span class="sxs-lookup"><span data-stu-id="b825a-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="b825a-116">Hallo resourcegroep kan alle Hallo resources voor Hallo oplossing of alleen de gewenste toomanage als een groep resources bevatten.</span><span class="sxs-lookup"><span data-stu-id="b825a-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="b825a-117">U bepalen hoe u resources tooallocate tooresource groepen op basis van het wat zinvol Hallo meeste voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="b825a-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="b825a-118">In het algemeen toevoegen resources die Hallo delen dezelfde levenscyclus toohello dezelfde resource groeperen, zodat u kunt eenvoudig implementeren, bijwerken en deze als een groep te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b825a-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="b825a-119">Hallo resourcegroep slaat metagegevens over Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="b825a-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="b825a-120">Daarom wanneer u een locatie voor resourcegroep Hallo opgeeft, geeft u aan waar de metagegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b825a-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="b825a-121">Om wettelijke redenen, moet u mogelijk tooensure die uw gegevens worden opgeslagen in een bepaald gebied.</span><span class="sxs-lookup"><span data-stu-id="b825a-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="b825a-122">alle Hallo resourcegroepen in uw abonnement, selecteert u toosee **resourcegroepen**.</span><span class="sxs-lookup"><span data-stu-id="b825a-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![resourcegroepen bladeren](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="b825a-124">Selecteer toocreate een lege resourcegroep **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b825a-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![toevoegen van resourcegroep](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="b825a-126">Geef een naam en locatie voor de nieuwe resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="b825a-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="b825a-127">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="b825a-127">Select **Create**.</span></span>
   
    ![resourcegroep maken](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="b825a-129">Mogelijk moet u tooselect **vernieuwen** toosee Hallo onlangs gemaakt resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b825a-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![vernieuwen van resourcegroep](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="b825a-131">toocustomize hello informatie weergegeven voor de bronnengroepen selecteren **kolommen**.</span><span class="sxs-lookup"><span data-stu-id="b825a-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![kolommen aanpassen](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="b825a-133">Hallo kolommen tooadd selecteren en selecteer vervolgens **Update**.</span><span class="sxs-lookup"><span data-stu-id="b825a-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![kolommen toevoegen](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="b825a-135">Zie toolearn over het implementeren van resources tooyour nieuwe resourcegroep [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="b825a-136">U kunt voor snelle toegang tooa resourcegroep, Hallo blade tooyour dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="b825a-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![pincode resourcegroep](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="b825a-138">Hallo dashboard toont de Hallo resourcegroep en de bijbehorende bronnen.</span><span class="sxs-lookup"><span data-stu-id="b825a-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="b825a-139">U kunt resourcegroepen hello of een van de resources toonavigate toohello item selecteren.</span><span class="sxs-lookup"><span data-stu-id="b825a-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![pincode resourcegroep](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="b825a-141">Tag resources</span><span class="sxs-lookup"><span data-stu-id="b825a-141">Tag resources</span></span>
<span data-ttu-id="b825a-142">U kunt tags tooresource groepen toepassen en resources toologically uw assets ordenen.</span><span class="sxs-lookup"><span data-stu-id="b825a-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="b825a-143">Zie voor meer informatie over het werken met labels [Using tags tooorganize uw Azure-resources](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="b825a-144">Resources controleren</span><span class="sxs-lookup"><span data-stu-id="b825a-144">Monitor resources</span></span>
<span data-ttu-id="b825a-145">Wanneer u een resource selecteert, geeft de resourceblade Hallo standaard grafieken en tabellen voor bewaking van dat resourcetype.</span><span class="sxs-lookup"><span data-stu-id="b825a-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="b825a-146">Selecteer een resource en kennisgeving Hallo **bewaking** sectie.</span><span class="sxs-lookup"><span data-stu-id="b825a-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="b825a-147">Dit omvat grafieken die relevant toohello resourcetype zijn.</span><span class="sxs-lookup"><span data-stu-id="b825a-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="b825a-148">Hallo toont volgende afbeelding Hallo standaardinstellingen voor bewaking van gegevens voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="b825a-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![bewaking weergeven](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="b825a-150">U kunt een gedeelte van Hallo blade tooyour dashboard vastmaken Hallo weglatingsteken (...) boven Hallo sectie selecteert.</span><span class="sxs-lookup"><span data-stu-id="b825a-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="b825a-151">U kunt ook Hallo grootte Hallo sectie Hallo blade aanpassen of verwijder deze volledig.</span><span class="sxs-lookup"><span data-stu-id="b825a-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="b825a-152">Hallo volgende afbeelding ziet u hoe toopin, aanpassen of verwijderen van Hallo CPU en geheugen-sectie.</span><span class="sxs-lookup"><span data-stu-id="b825a-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![sectie van de pincode](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="b825a-154">Na het Hallo sectie toohello dashboard vastmaken, ziet u Hallo samenvatting op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="b825a-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="b825a-155">En onmiddellijk selecteren gaat u gegevens over Hallo toomore.</span><span class="sxs-lookup"><span data-stu-id="b825a-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![weergave-dashboard](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="b825a-157">toocompletely aanpassen Hallo gegevens controleren via de portal hello, navigeer tooyour standaarddashboard en selecteer **nieuwe dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b825a-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="b825a-159">Geef een naam op voor uw nieuwe dashboard en sleep tegels op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="b825a-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="b825a-160">Hallo tegels worden gefilterd door verschillende opties.</span><span class="sxs-lookup"><span data-stu-id="b825a-160">hello tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="b825a-162">toolearn over het werken met dashboards, Zie [maken en delen van dashboards in hello Azure-portal](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="b825a-163">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="b825a-163">Manage resources</span></span>
<span data-ttu-id="b825a-164">In Hallo blade voor een resource ziet u opties voor het beheren van Hallo resource Hallo.</span><span class="sxs-lookup"><span data-stu-id="b825a-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="b825a-165">Hallo portal geeft beheeropties voor die bepaald resourcetype.</span><span class="sxs-lookup"><span data-stu-id="b825a-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="b825a-166">Opdrachten voor het beheer van Hallo ziet u aan de bovenkant Hallo van Hallo resourceblade en aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="b825a-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![Resources beheren](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="b825a-168">U kunt bewerkingen zoals het starten en stoppen van een virtuele machine of Hallo eigenschappen van Hallo virtuele machine opnieuw uitvoeren van deze opties.</span><span class="sxs-lookup"><span data-stu-id="b825a-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="b825a-169">Resources verplaatsen</span><span class="sxs-lookup"><span data-stu-id="b825a-169">Move resources</span></span>
<span data-ttu-id="b825a-170">Als u toomove resources tooanother resourcegroep of een ander abonnement nodig hebt, raadpleegt u [verplaatsen van resources toonew resourcegroep of abonnement](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="b825a-171">Resources vergrendelen</span><span class="sxs-lookup"><span data-stu-id="b825a-171">Lock resources</span></span>
<span data-ttu-id="b825a-172">U kunt vergrendelen een abonnement, resourcegroep of resource tooprevent andere gebruikers in uw organisatie per ongeluk worden kritieke bronnen wijzigen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b825a-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="b825a-173">Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="b825a-174">Uw abonnement en kosten weergeven</span><span class="sxs-lookup"><span data-stu-id="b825a-174">View your subscription and costs</span></span>
<span data-ttu-id="b825a-175">U kunt informatie over uw abonnement en Hallo samengevouwen kosten weergeven voor al uw resources.</span><span class="sxs-lookup"><span data-stu-id="b825a-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="b825a-176">Selecteer **abonnementen** en gewenste toosee Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b825a-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="b825a-177">U wellicht slechts één abonnement tooselect.</span><span class="sxs-lookup"><span data-stu-id="b825a-177">You might only have one subscription tooselect.</span></span>

![abonnement](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="b825a-179">Binnen abonnementsblade hello ziet u een frequentie branden.</span><span class="sxs-lookup"><span data-stu-id="b825a-179">Within hello subscription blade, you see a burn rate.</span></span>

![frequentie branden](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="b825a-181">En een uitsplitsing van de kosten per resourcetype.</span><span class="sxs-lookup"><span data-stu-id="b825a-181">And, a breakdown of costs by resource type.</span></span>

![de kosten van resource](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="b825a-183">Sjabloon exporteren</span><span class="sxs-lookup"><span data-stu-id="b825a-183">Export template</span></span>
<span data-ttu-id="b825a-184">Na het instellen van de resourcegroep, kunt u tooview Hallo Resource Manager-sjabloon voor de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="b825a-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="b825a-185">Uitvoer Hallo sjabloon biedt twee voordelen:</span><span class="sxs-lookup"><span data-stu-id="b825a-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="b825a-186">Omdat het Hallo-sjabloon bevat alle Hallo volledige infrastructuur, kunt u eenvoudig toekomstige implementaties van Hallo oplossing automatiseren.</span><span class="sxs-lookup"><span data-stu-id="b825a-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="b825a-187">U kunt meer vertrouwd raken met de sjabloonsyntaxis van de door te kijken Hallo notatie JSON (JavaScript Object) dat uw oplossing vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="b825a-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="b825a-188">Zie voor stapsgewijze instructies [Azure Resource Manager-sjabloon exporteren uit bestaande resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="b825a-189">Resourcegroep of resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="b825a-189">Delete resource group or resources</span></span>
<span data-ttu-id="b825a-190">Verwijderen van een resourcegroep, worden alle Hallo resources daarin verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b825a-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="b825a-191">U kunt ook afzonderlijke resources binnen een resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b825a-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="b825a-192">Gewenste tooexercise voorzichtig wanneer u een resourcegroep verwijderen omdat er mogelijk resources in andere resourcegroepen die gekoppelde tooit zijn.</span><span class="sxs-lookup"><span data-stu-id="b825a-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="b825a-193">Resource Manager wordt niet gekoppelde resources verwijderd, maar ze werken mogelijk niet goed zonder Hallo verwacht bronnen.</span><span class="sxs-lookup"><span data-stu-id="b825a-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![Groep verwijderen](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="b825a-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b825a-195">Next steps</span></span>
* <span data-ttu-id="b825a-196">tooview activiteitenlogboeken, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="b825a-197">Zie details over een implementatie tooview [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="b825a-198">toodeploy resources via de portal hello, Zie [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="b825a-199">toomanage toegang tooresources, Zie [rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="b825a-200">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b825a-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

