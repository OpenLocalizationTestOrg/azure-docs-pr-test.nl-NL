---
title: Azure-portal gebruiken voor het beheren van Azure-resources | Microsoft Docs
description: Azure portal en Azure Resource Manager gebruiken voor het beheren van uw resources. Toont het werken met dashboards voor het bewaken van resources.
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
ms.openlocfilehash: 7a94fd5065de93384460e851627a9813d439956b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="11e9e-104">Azure-resources via de portal beheren</span><span class="sxs-lookup"><span data-stu-id="11e9e-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11e9e-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="11e9e-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="11e9e-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="11e9e-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="11e9e-107">Portal</span><span class="sxs-lookup"><span data-stu-id="11e9e-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="11e9e-108">REST API</span><span class="sxs-lookup"><span data-stu-id="11e9e-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="11e9e-109">Dit onderwerp wordt beschreven hoe u de [Azure-portal](https://portal.azure.com) met [Azure Resource Manager](resource-group-overview.md) voor het beheren van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="11e9e-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="11e9e-110">Zie voor meer informatie over het implementeren van resources via de portal, [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="11e9e-111">Op dit moment ondersteunt niet elke service de portal of de resourcemanager.</span><span class="sxs-lookup"><span data-stu-id="11e9e-111">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="11e9e-112">Voor deze services die u wilt gebruiken, de [klassieke portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="11e9e-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="11e9e-113">Zie voor de status van elke service, [Azure portal beschikbaarheid grafiek](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="11e9e-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="11e9e-114">Resourcegroepen beheren</span><span class="sxs-lookup"><span data-stu-id="11e9e-114">Manage resource groups</span></span>

<span data-ttu-id="11e9e-115">Een resourcegroep is een container met verwante resources voor een Azure-oplossing.</span><span class="sxs-lookup"><span data-stu-id="11e9e-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="11e9e-116">De resourcegroep kan alle resources voor de oplossing bevatten of enkel de resources die u als groep wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="11e9e-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="11e9e-117">U bepaalt hoe resources worden toegewezen aan resourcegroepen op basis van wat voor uw organisatie het meest zinvol is.</span><span class="sxs-lookup"><span data-stu-id="11e9e-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="11e9e-118">In het algemeen resources die dezelfde levenscyclus naar dezelfde resourcegroep delen, zodat u kunt eenvoudig implementeren, bijwerken en ze als een groep verwijderen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="11e9e-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="11e9e-119">De resourcegroep slaat metagegevens op over de resources.</span><span class="sxs-lookup"><span data-stu-id="11e9e-119">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="11e9e-120">Dat is de reden waarom u moet aangeven waar die metagegevens moeten worden opgeslagen als u een locatie voor de resourcegroep opgeeft.</span><span class="sxs-lookup"><span data-stu-id="11e9e-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="11e9e-121">In verband met nalevingsvereisten moet u er mogelijk voor zorgen dat uw gegevens worden opgeslagen in een bepaalde regio.</span><span class="sxs-lookup"><span data-stu-id="11e9e-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="11e9e-122">Selecteer om te zien alle resourcegroepen in uw abonnement, **resourcegroepen**.</span><span class="sxs-lookup"><span data-stu-id="11e9e-122">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![resourcegroepen bladeren](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="11e9e-124">U maakt een lege resourcegroep selecteren **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="11e9e-124">To create an empty resource group, select **Add**.</span></span>
   
    ![toevoegen van resourcegroep](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="11e9e-126">Geef een naam en locatie voor de nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="11e9e-126">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="11e9e-127">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="11e9e-127">Select **Create**.</span></span>
   
    ![resourcegroep maken](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="11e9e-129">U wilt selecteren **vernieuwen** om te zien van de resourcegroep hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11e9e-129">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![vernieuwen van resourcegroep](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="11e9e-131">Selecteer voor het aanpassen van de weergegeven informatie voor uw resourcegroepen **kolommen**.</span><span class="sxs-lookup"><span data-stu-id="11e9e-131">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![kolommen aanpassen](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="11e9e-133">Selecteer de kolommen wilt toevoegen en selecteer vervolgens **Update**.</span><span class="sxs-lookup"><span data-stu-id="11e9e-133">Select the columns to add, and then select **Update**.</span></span>
   
    ![kolommen toevoegen](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="11e9e-135">Zie voor meer informatie over het implementeren van resources op uw nieuwe resourcegroep, [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="11e9e-136">U kunt de blade vastmaken aan uw dashboard voor snelle toegang tot een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="11e9e-136">For quick access to a resource group, you can pin the blade to your dashboard.</span></span>
   
    ![pincode resourcegroep](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="11e9e-138">Het dashboard toont de resourcegroep en de bijbehorende bronnen.</span><span class="sxs-lookup"><span data-stu-id="11e9e-138">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="11e9e-139">U kunt ofwel de resourcegroepen of een van de daarbij behorende bronnen om te navigeren naar het item selecteren.</span><span class="sxs-lookup"><span data-stu-id="11e9e-139">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![pincode resourcegroep](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="11e9e-141">Tag resources</span><span class="sxs-lookup"><span data-stu-id="11e9e-141">Tag resources</span></span>
<span data-ttu-id="11e9e-142">U kunt tags toepassen resourcegroepen en resources voor uw assets logische manier te organiseren.</span><span class="sxs-lookup"><span data-stu-id="11e9e-142">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="11e9e-143">Zie voor meer informatie over het werken met labels [met labels om uw Azure-resources te organiseren](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="11e9e-144">Resources controleren</span><span class="sxs-lookup"><span data-stu-id="11e9e-144">Monitor resources</span></span>
<span data-ttu-id="11e9e-145">Wanneer u een resource selecteert, geeft de resourceblade standaard grafieken en tabellen voor bewaking van dat resourcetype.</span><span class="sxs-lookup"><span data-stu-id="11e9e-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="11e9e-146">Selecteer een resource die en u ziet de **bewaking** sectie.</span><span class="sxs-lookup"><span data-stu-id="11e9e-146">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="11e9e-147">Dit omvat grafieken die relevant voor het brontype zijn.</span><span class="sxs-lookup"><span data-stu-id="11e9e-147">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="11e9e-148">De volgende afbeelding ziet u de bewakingsgegevens voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="11e9e-148">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![bewaking weergeven](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="11e9e-150">U kunt een gedeelte van de blade vastmaken aan uw dashboard met het weglatingsteken (...) boven de sectie selecteren.</span><span class="sxs-lookup"><span data-stu-id="11e9e-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="11e9e-151">U kunt ook de grootte van de sectie in de blade aanpassen of verwijder deze volledig.</span><span class="sxs-lookup"><span data-stu-id="11e9e-151">You can also customize the size the section in the blade or remove it completely.</span></span> <span data-ttu-id="11e9e-152">De volgende afbeelding laat zien hoe vastmaken, aanpassen of verwijderen van de CPU en geheugen-sectie.</span><span class="sxs-lookup"><span data-stu-id="11e9e-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![sectie van de pincode](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="11e9e-154">Na het vastmaken van de sectie aan het dashboard, ziet u de samenvatting op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="11e9e-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="11e9e-155">En onmiddellijk te selecteren, gaat u naar meer informatie over de gegevens.</span><span class="sxs-lookup"><span data-stu-id="11e9e-155">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![weergave-dashboard](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="11e9e-157">Om volledig aanpassen aan de gegevens die u via de portal bewaken, navigeer naar uw standaarddashboard en selecteer **nieuwe dashboard**.</span><span class="sxs-lookup"><span data-stu-id="11e9e-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="11e9e-159">Geef een naam op voor uw nieuwe dashboard en sleep tegels op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="11e9e-159">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="11e9e-160">De tegels worden gefilterd door verschillende opties.</span><span class="sxs-lookup"><span data-stu-id="11e9e-160">The tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="11e9e-162">Zie voor meer informatie over het werken met dashboards, [maken en delen van dashboards in de Azure portal](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="11e9e-163">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="11e9e-163">Manage resources</span></span>
<span data-ttu-id="11e9e-164">In de blade voor een resource ziet u de opties voor het beheren van de resource.</span><span class="sxs-lookup"><span data-stu-id="11e9e-164">In the blade for a resource, you see the options for managing the resource.</span></span> <span data-ttu-id="11e9e-165">De portal geeft beheeropties voor die bepaald resourcetype.</span><span class="sxs-lookup"><span data-stu-id="11e9e-165">The portal presents management options for that particular resource type.</span></span> <span data-ttu-id="11e9e-166">Ziet u de opdrachten voor het beheer aan de bovenkant van de resourceblade en aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="11e9e-166">You see the management commands across the top of the resource blade and on the left side.</span></span>

![Resources beheren](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="11e9e-168">U kunt bewerkingen zoals het starten en stoppen van een virtuele machine of opnieuw configureren van de eigenschappen van de virtuele machine uitvoeren van deze opties.</span><span class="sxs-lookup"><span data-stu-id="11e9e-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="11e9e-169">Resources verplaatsen</span><span class="sxs-lookup"><span data-stu-id="11e9e-169">Move resources</span></span>
<span data-ttu-id="11e9e-170">Als u resources verplaatsen naar een andere resourcegroep of een ander abonnement wilt, Zie [resources verplaatsen naar de nieuwe resourcegroep of abonnement](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="11e9e-171">Resources vergrendelen</span><span class="sxs-lookup"><span data-stu-id="11e9e-171">Lock resources</span></span>
<span data-ttu-id="11e9e-172">U kunt een abonnement, resourcegroep of resource om te voorkomen dat andere gebruikers in uw organisatie per ongeluk verwijderen of wijzigen van kritieke bronnen vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="11e9e-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="11e9e-173">Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="11e9e-174">Uw abonnement en kosten weergeven</span><span class="sxs-lookup"><span data-stu-id="11e9e-174">View your subscription and costs</span></span>
<span data-ttu-id="11e9e-175">U kunt informatie weergeven over uw abonnement en de samengevoegde kosten voor al uw resources.</span><span class="sxs-lookup"><span data-stu-id="11e9e-175">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="11e9e-176">Selecteer **abonnementen** en het abonnement dat u wilt zien.</span><span class="sxs-lookup"><span data-stu-id="11e9e-176">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="11e9e-177">U wellicht slechts één abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="11e9e-177">You might only have one subscription to select.</span></span>

![abonnement](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="11e9e-179">Binnen de abonnementsblade ziet u een frequentie branden.</span><span class="sxs-lookup"><span data-stu-id="11e9e-179">Within the subscription blade, you see a burn rate.</span></span>

![frequentie branden](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="11e9e-181">En een uitsplitsing van de kosten per resourcetype.</span><span class="sxs-lookup"><span data-stu-id="11e9e-181">And, a breakdown of costs by resource type.</span></span>

![de kosten van resource](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="11e9e-183">Sjabloon exporteren</span><span class="sxs-lookup"><span data-stu-id="11e9e-183">Export template</span></span>
<span data-ttu-id="11e9e-184">Na het instellen van de resourcegroep, is het raadzaam om de Resource Manager-sjabloon voor de resourcegroep weer te geven.</span><span class="sxs-lookup"><span data-stu-id="11e9e-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="11e9e-185">De sjabloon exporteren biedt twee voordelen:</span><span class="sxs-lookup"><span data-stu-id="11e9e-185">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="11e9e-186">Omdat de sjabloon de volledige infrastructuur bevat, kunt u eenvoudig toekomstige implementaties van de oplossing automatiseren.</span><span class="sxs-lookup"><span data-stu-id="11e9e-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="11e9e-187">U kunt meer vertrouwd raken met de sjabloonsyntaxis van de door te kijken in de notatie JSON (JavaScript Object) dat uw oplossing vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="11e9e-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="11e9e-188">Zie voor stapsgewijze instructies [Azure Resource Manager-sjabloon exporteren uit bestaande resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="11e9e-189">Resourcegroep of resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="11e9e-189">Delete resource group or resources</span></span>
<span data-ttu-id="11e9e-190">Verwijderen van een resourcegroep, worden alle resources daarin verwijderd.</span><span class="sxs-lookup"><span data-stu-id="11e9e-190">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="11e9e-191">U kunt ook afzonderlijke resources binnen een resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="11e9e-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="11e9e-192">Wilt u voorzichtig wanneer u een resourcegroep verwijderen omdat er mogelijk resources in andere resourcegroepen die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="11e9e-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span></span> <span data-ttu-id="11e9e-193">Resource Manager wordt niet gekoppelde resources verwijderd, maar ze werken mogelijk niet goed zonder de verwachte bronnen.</span><span class="sxs-lookup"><span data-stu-id="11e9e-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span></span>

![Groep verwijderen](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="11e9e-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11e9e-195">Next steps</span></span>
* <span data-ttu-id="11e9e-196">Voor activiteitenlogboeken, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="11e9e-197">Zie voor meer informatie over een implementatie, [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="11e9e-198">Zie voor het implementeren van resources via de portal [implementeren van resources met Resource Manager-sjablonen en Azure-portal](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="11e9e-199">Zie voor het beheren van toegang tot bronnen [roltoewijzingen gebruiken voor het beheren van toegang tot de resources van uw Azure-abonnement](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="11e9e-200">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="11e9e-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

