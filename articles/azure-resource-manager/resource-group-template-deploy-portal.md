---
title: Azure portal gebruiken voor het implementeren van Azure-resources | Microsoft Docs
description: Azure portal en Azure Resource Manager gebruiken voor het implementeren van uw resources.
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
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="3cd1f-103">Resources implementeren met Resource Manager-sjablonen en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3cd1f-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3cd1f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cd1f-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="3cd1f-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3cd1f-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="3cd1f-106">Portal</span><span class="sxs-lookup"><span data-stu-id="3cd1f-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="3cd1f-107">REST API</span><span class="sxs-lookup"><span data-stu-id="3cd1f-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="3cd1f-108">Dit onderwerp wordt beschreven hoe u de [Azure-portal](https://portal.azure.com) met [Azure Resource Manager](resource-group-overview.md) voor het implementeren van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="3cd1f-109">Zie voor meer informatie over het beheren van uw resources, [beheren Azure-resources via de portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="3cd1f-110">Op dit moment ondersteunt niet elke service de portal of de resourcemanager.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="3cd1f-111">Voor deze services die u wilt gebruiken, de [klassieke portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="3cd1f-112">Zie voor de status van elke service, [Azure portal beschikbaarheid grafiek](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="3cd1f-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="3cd1f-113">Create resource group</span></span>
1. <span data-ttu-id="3cd1f-114">U maakt een lege resourcegroep selecteren **nieuw** > **Management** > **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![lege resourcegroep maken](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="3cd1f-116">Wijs hieraan een naam en locatie en, indien nodig, selecteert u een abonnement.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="3cd1f-117">U moet een locatie opgeven voor de resourcegroep omdat de resourcegroep metagegevens over de bronnen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="3cd1f-118">Om wettelijke redenen kan u wilt opgeven waar de metagegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="3cd1f-119">In het algemeen is het raadzaam dat u een locatie waar de meeste van uw resources opgeven.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="3cd1f-120">Met behulp van dezelfde locatie, kan de sjabloon vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-120">Using the same location can simplify your template.</span></span>
   
    ![setwaarden](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="3cd1f-122">Resources van Marketplace implementeren</span><span class="sxs-lookup"><span data-stu-id="3cd1f-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="3cd1f-123">Nadat u een resourcegroep hebt gemaakt, kunt u kunt resources van de Marketplace implementeren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="3cd1f-124">De Marketplace biedt vooraf gedefinieerde oplossingen voor algemene scenario's.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="3cd1f-125">Selecteer voor het starten van een implementatie **nieuw** en het type resource dat u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="3cd1f-126">Vervolgens zoekt u naar de specifieke versie van de resource die u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![resource implementeren](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="3cd1f-128">Als u de specifieke oplossing die u wilt implementeren niet ziet, kunt u de Marketplace voor het zoeken.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![zoeken marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="3cd1f-130">Afhankelijk van het type geselecteerde bron hebt u een verzameling van de relevante eigenschappen in te stellen vóór de implementatie.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="3cd1f-131">Deze opties wordt hier niet weergegeven als ze afhankelijk van het resourcetype variëren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="3cd1f-132">Voor alle typen, moet u een resourcegroep bestemming.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="3cd1f-133">De volgende afbeelding laat zien hoe een web-app maken en deze implementeren in de resourcegroep die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![resourcegroep maken](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="3cd1f-135">U kunt ook een resourcegroep maken bij het implementeren van uw resources.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="3cd1f-136">Selecteer **nieuw** en geef de resourcegroep een naam.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![nieuwe resourcegroep maken](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="3cd1f-138">Uw implementatie begint.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-138">Your deployment begins.</span></span> <span data-ttu-id="3cd1f-139">De implementatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="3cd1f-140">Als de implementatie is voltooid, ziet u een melding.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-140">When the deployment has finished, you see a notification.</span></span>
   
    ![melding weergeven](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="3cd1f-142">Na implementatie van uw resources, kunt u meer resources toevoegen aan de resourcegroep met behulp van de **toevoegen** opdracht op de blade met resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![resource toevoegen](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="3cd1f-144">Resources met aangepaste sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="3cd1f-144">Deploy resources from custom template</span></span>
<span data-ttu-id="3cd1f-145">Als u wilt uitvoeren van een implementatie, maar geen gebruik van de sjablonen in de Marketplace, kunt u een aangepaste sjabloon die de infrastructuur voor uw oplossing definieert.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="3cd1f-146">Zie voor meer informatie over het maken van sjablonen, [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="3cd1f-147">Voor het implementeren van een aangepaste sjabloon via de portal, selecteer **nieuw**, en beginnen met zoeken voor **sjabloonimplementatie** totdat u deze in de opties kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![de sjabloonimplementatie zoeken](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="3cd1f-149">Selecteer **sjabloonimplementatie** uit de beschikbare bronnen.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![sjabloonimplementatie selecteren](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="3cd1f-151">Open de lege sjabloon die beschikbaar is voor het aanpassen van na het starten van de sjabloonimplementatie.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![Sjabloon maken](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="3cd1f-153">Voeg de syntaxis van de JSON die definieert de resources die u wilt implementeren in de editor.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="3cd1f-154">Selecteer **opslaan** wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-154">Select **Save** when done.</span></span> <span data-ttu-id="3cd1f-155">Zie voor instructies over het schrijven van de JSON-syntaxis [overzicht voor Resource Manager-sjabloon](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![sjabloon bewerken](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="3cd1f-157">Of, kunt u een bestaande sjabloon van de [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="3cd1f-158">Deze sjablonen worden aangeleverd door de community.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-158">These templates are contributed by the community.</span></span> <span data-ttu-id="3cd1f-159">Deze omvatten algemene scenario's en iemand een sjabloon die is vergelijkbaar met wat u probeert te implementeren hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="3cd1f-160">U kunt de sjablonen om te vinden die overeenkomt met het scenario zoeken.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![Quick Start-sjabloon selecteren](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="3cd1f-162">U kunt de geselecteerde sjabloon weergeven in de editor.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="3cd1f-163">Na het opgeven van de waarden, selecteer **maken** om de sjabloon te implementeren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![sjabloon implementeren](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="3cd1f-165">Resources van een sjabloon die is opgeslagen in uw account implementeren</span><span class="sxs-lookup"><span data-stu-id="3cd1f-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="3cd1f-166">De portal kunt u een sjabloon opslaan in uw Azure-account en het later opnieuw te implementeren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="3cd1f-167">Voor meer informatie over het werken met deze sjablonen, opgeslagen [aan de slag met persoonlijke sjablonen in de Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="3cd1f-168">Selecteer uw opgeslagen sjablonen vindt **Bladeren** > **sjablonen**.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![Bladeren in sjablonen](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="3cd1f-170">Selecteer in de lijst met sjablonen die zijn opgeslagen in uw account, degene die u werken wilt op.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![opgeslagen sjablonen](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="3cd1f-172">Selecteer **implementeren** deze opgeslagen sjabloon opnieuw implementeren.</span><span class="sxs-lookup"><span data-stu-id="3cd1f-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![opgeslagen sjabloon implementeren](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="3cd1f-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cd1f-174">Next steps</span></span>
* <span data-ttu-id="3cd1f-175">Controlelogboeken Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="3cd1f-176">Zie voor het oplossen van implementatiefouten [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="3cd1f-177">Zie voor het ophalen van een sjabloon van een implementatie of de resourcegroep, [Azure Resource Manager-sjabloon exporteren uit bestaande resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="3cd1f-178">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="3cd1f-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

