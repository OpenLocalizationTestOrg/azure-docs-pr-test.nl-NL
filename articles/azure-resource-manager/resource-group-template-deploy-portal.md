---
title: Azure portal toodeploy aaaUse Azure-resources | Microsoft Docs
description: Azure portal en Azure Resource Manager toodeploy uw resources gebruiken.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="27d8f-103">Resources implementeren met Resource Manager-sjablonen en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="27d8f-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27d8f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27d8f-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="27d8f-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="27d8f-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="27d8f-106">Portal</span><span class="sxs-lookup"><span data-stu-id="27d8f-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="27d8f-107">REST API</span><span class="sxs-lookup"><span data-stu-id="27d8f-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="27d8f-108">Dit onderwerp wordt beschreven hoe toouse hello [Azure-portal](https://portal.azure.com) met [Azure Resource Manager](resource-group-overview.md) toodeploy uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="27d8f-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="27d8f-109">Zie toolearn over het beheren van uw resources [beheren Azure-resources via de portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="27d8f-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="27d8f-110">Op dit moment ondersteunt niet elke service Hallo portal of de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="27d8f-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="27d8f-111">Voor deze services, moet u toouse hello [klassieke portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="27d8f-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="27d8f-112">Zie voor Hallo status van elke service, [Azure portal beschikbaarheid grafiek](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="27d8f-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="27d8f-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="27d8f-113">Create resource group</span></span>
1. <span data-ttu-id="27d8f-114">Selecteer toocreate een lege resourcegroep **nieuw** > **Management** > **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="27d8f-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![lege resourcegroep maken](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="27d8f-116">Wijs hieraan een naam en locatie en, indien nodig, selecteert u een abonnement.</span><span class="sxs-lookup"><span data-stu-id="27d8f-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="27d8f-117">Moet u tooprovide een locatie voor resourcegroep Hallo omdat resourcegroep Hallo metagegevens over Hallo resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="27d8f-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="27d8f-118">U kunt om wettelijke redenen toospecify waar deze metagegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="27d8f-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="27d8f-119">In het algemeen is het raadzaam dat u een locatie waar de meeste van uw resources opgeven.</span><span class="sxs-lookup"><span data-stu-id="27d8f-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="27d8f-120">Met behulp van dezelfde Hallo locatie kunt u de sjabloon vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="27d8f-120">Using hello same location can simplify your template.</span></span>
   
    ![setwaarden](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="27d8f-122">Resources van Marketplace implementeren</span><span class="sxs-lookup"><span data-stu-id="27d8f-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="27d8f-123">Nadat u een resourcegroep hebt gemaakt, kunt u resources tooit van Hallo Marketplace kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="27d8f-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="27d8f-124">Hallo Marketplace biedt vooraf gedefinieerde oplossingen voor algemene scenario's.</span><span class="sxs-lookup"><span data-stu-id="27d8f-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="27d8f-125">toostart een implementatie, selecteer **nieuw** en het Hallo-type van resource gewenst toodeploy.</span><span class="sxs-lookup"><span data-stu-id="27d8f-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="27d8f-126">Zoek voor bepaalde versie van Hallo resource Hallo gewenst toodeploy.</span><span class="sxs-lookup"><span data-stu-id="27d8f-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![resource implementeren](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="27d8f-128">Als u bepaalde Hallo-oplossing u graag toodeploy niet ziet, kunt u Hallo Marketplace voor het zoeken.</span><span class="sxs-lookup"><span data-stu-id="27d8f-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![zoeken marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="27d8f-130">Afhankelijk van het type Hallo van geselecteerde bron hebt u een verzameling van de relevante eigenschappen tooset vóór de implementatie.</span><span class="sxs-lookup"><span data-stu-id="27d8f-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="27d8f-131">Deze opties wordt hier niet weergegeven als ze afhankelijk van het resourcetype variëren.</span><span class="sxs-lookup"><span data-stu-id="27d8f-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="27d8f-132">Voor alle typen, moet u een resourcegroep bestemming.</span><span class="sxs-lookup"><span data-stu-id="27d8f-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="27d8f-133">Hallo volgende afbeelding toont hoe toocreate een web-app en implementeert u het toohello-resourcegroep die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="27d8f-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![resourcegroep maken](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="27d8f-135">U kunt ook kunt u een resourcegroep toocreate bepalen bij het implementeren van uw resources.</span><span class="sxs-lookup"><span data-stu-id="27d8f-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="27d8f-136">Selecteer **nieuw** en Hallo resourcegroep een naam geven.</span><span class="sxs-lookup"><span data-stu-id="27d8f-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![nieuwe resourcegroep maken](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="27d8f-138">Uw implementatie begint.</span><span class="sxs-lookup"><span data-stu-id="27d8f-138">Your deployment begins.</span></span> <span data-ttu-id="27d8f-139">Hallo-implementatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="27d8f-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="27d8f-140">Als het Hallo-implementatie is voltooid, ziet u een melding.</span><span class="sxs-lookup"><span data-stu-id="27d8f-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![melding weergeven](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="27d8f-142">Na implementatie van uw resources, kunt u meer resources toohello-resourcegroep toevoegen met behulp van Hallo **toevoegen** opdracht op Hallo resourcegroepblade.</span><span class="sxs-lookup"><span data-stu-id="27d8f-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![resource toevoegen](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="27d8f-144">Resources met aangepaste sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="27d8f-144">Deploy resources from custom template</span></span>
<span data-ttu-id="27d8f-145">Als u tooexecute een implementatie wilt, maar u geen gebruik van Hallo sjablonen in Hallo Marketplace, kunt u een aangepaste sjabloon die Hallo-infrastructuur voor uw oplossing definieert.</span><span class="sxs-lookup"><span data-stu-id="27d8f-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="27d8f-146">toolearn over het maken van sjablonen, Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="27d8f-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="27d8f-147">toodeploy een aangepaste sjabloon via Hallo-portal, selecteer **nieuw**, en beginnen met zoeken voor **sjabloonimplementatie** totdat u deze in Hallo opties kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="27d8f-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![de sjabloonimplementatie zoeken](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="27d8f-149">Selecteer **sjabloonimplementatie** van Hallo beschikbare bronnen.</span><span class="sxs-lookup"><span data-stu-id="27d8f-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![sjabloonimplementatie selecteren](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="27d8f-151">Open na het starten van de sjabloonimplementatie Hallo Hallo lege sjabloon die beschikbaar is voor het aanpassen.</span><span class="sxs-lookup"><span data-stu-id="27d8f-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![Sjabloon maken](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="27d8f-153">Toevoegen in de editor Hallo Hallo JSON syntaxis die Hallo-bronnen die u wilt dat toodeploy definieert.</span><span class="sxs-lookup"><span data-stu-id="27d8f-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="27d8f-154">Selecteer **opslaan** wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="27d8f-154">Select **Save** when done.</span></span> <span data-ttu-id="27d8f-155">Zie voor instructies over het schrijven van Hallo JSON syntaxis [overzicht voor Resource Manager-sjabloon](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="27d8f-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![sjabloon bewerken](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="27d8f-157">Of u kunt een bestaande sjabloon kiezen uit Hallo [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="27d8f-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="27d8f-158">Deze sjablonen zijn die is bijgedragen door Hallo-community.</span><span class="sxs-lookup"><span data-stu-id="27d8f-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="27d8f-159">Deze omvatten algemene scenario's en iemand een sjabloon die is vergelijkbaar toowhat die u probeert toodeploy hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="27d8f-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="27d8f-160">U kunt zoeken Hallo sjablonen toofind iets dat overeenkomt met het scenario.</span><span class="sxs-lookup"><span data-stu-id="27d8f-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![Quick Start-sjabloon selecteren](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="27d8f-162">U kunt de geselecteerde sjabloon Hallo in Hallo-editor weergeven.</span><span class="sxs-lookup"><span data-stu-id="27d8f-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="27d8f-163">Na het Hallo alle andere waarden opgeven, selecteert u **maken** toodeploy Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="27d8f-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![sjabloon implementeren](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="27d8f-165">Resources van een sjabloon opgeslagen tooyour account implementeren</span><span class="sxs-lookup"><span data-stu-id="27d8f-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="27d8f-166">Hallo-portal kunt u een sjabloon tooyour Azure-account toosave en later opnieuw te implementeren.</span><span class="sxs-lookup"><span data-stu-id="27d8f-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="27d8f-167">Voor meer informatie over het werken met deze sjablonen, opgeslagen [aan de slag met persoonlijke sjablonen in Azure-portal Hallo](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="27d8f-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="27d8f-168">toofind uw opgeslagen sjablonen selecteren **Bladeren** > **sjablonen**.</span><span class="sxs-lookup"><span data-stu-id="27d8f-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![Bladeren in sjablonen](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="27d8f-170">Selecteer één u wilt dat toowork op Hallo in Hallo lijst met sjablonen tooyour account opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="27d8f-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![opgeslagen sjablonen](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="27d8f-172">Selecteer **implementeren** tooredeploy dit sjabloon opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="27d8f-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![opgeslagen sjabloon implementeren](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="27d8f-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="27d8f-174">Next steps</span></span>
* <span data-ttu-id="27d8f-175">controlelogboeken tooview, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="27d8f-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="27d8f-176">implementatiefouten tootroubleshoot, Zie [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="27d8f-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="27d8f-177">een sjabloon van een implementatie of de resourcegroep, tooretrieve Zie [Azure Resource Manager-sjabloon exporteren uit bestaande resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="27d8f-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="27d8f-178">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="27d8f-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

