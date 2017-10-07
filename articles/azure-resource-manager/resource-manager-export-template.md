---
title: aaaExport Azure Resource Manager-sjabloon | Microsoft Docs
description: Azure Resource Manager tooexport een sjabloon van een bestaande resourcegroep gebruiken.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="8851f-103">Een Azure Resource Manager-sjabloon uit bestaande resources exporteren</span><span class="sxs-lookup"><span data-stu-id="8851f-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="8851f-104">In dit artikel leert u hoe tooexport Resource Manager-sjabloon uit bestaande resources in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="8851f-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="8851f-105">U kunt deze gegenereerde sjabloon toogain een beter begrip van de sjabloonsyntaxis van de gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8851f-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="8851f-106">Er zijn twee manieren tooexport een sjabloon:</span><span class="sxs-lookup"><span data-stu-id="8851f-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="8851f-107">U kunt exporteren Hallo **werkelijke sjabloon die wordt gebruikt voor de implementatie van**.</span><span class="sxs-lookup"><span data-stu-id="8851f-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="8851f-108">Hallo geëxporteerde sjabloon bevat alle Hallo parameters en variabelen exact zo worden weergegeven in de oorspronkelijke sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="8851f-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="8851f-109">Deze methode is handig als u resources via de portal Hallo geïmplementeerd en wilt toosee Hallo sjabloon toocreate die bronnen.</span><span class="sxs-lookup"><span data-stu-id="8851f-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="8851f-110">Deze sjabloon kan ongewijzigd worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8851f-110">This template is readily usable.</span></span> 
* <span data-ttu-id="8851f-111">U kunt exporteren een **sjabloon met de huidige status van de resourcegroep Hallo Hallo gegenereerd**.</span><span class="sxs-lookup"><span data-stu-id="8851f-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="8851f-112">Hallo geëxporteerde sjabloon is niet op basis van een sjabloon die u voor implementatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8851f-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="8851f-113">In plaats daarvan wordt een sjabloon die een momentopname van de resourcegroep Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8851f-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="8851f-114">geëxporteerde sjabloon Hallo heeft veel vastgelegde waarden en waarschijnlijk niet zoveel parameters zoals u normaal gesproken zou definiëren.</span><span class="sxs-lookup"><span data-stu-id="8851f-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="8851f-115">Deze methode is handig wanneer u Hallo resourcegroep hebt gewijzigd na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="8851f-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="8851f-116">Deze sjabloon moet meestal worden aangepast voordat deze kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8851f-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="8851f-117">Dit onderwerp bevat beide benaderingen via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="8851f-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="8851f-118">Resources implementeren</span><span class="sxs-lookup"><span data-stu-id="8851f-118">Deploy resources</span></span>
<span data-ttu-id="8851f-119">Laten we beginnen door het implementeren van resources tooAzure die u gebruiken kunt voor het exporteren als een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8851f-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="8851f-120">Als u al een resourcegroep in uw abonnement dat u wilt dat tooexport tooa sjabloon hebt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="8851f-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="8851f-121">Hallo rest van dit artikel wordt ervan uitgegaan dat u hebt geïmplementeerd Hallo WebApp en SQL database-oplossing in deze sectie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8851f-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="8851f-122">Als u een andere oplossing gebruikt, wordt uw ervaring mogelijk enigszins verschillen, maar Hallo stappen zijn van een sjabloon tooexport Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="8851f-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="8851f-123">In Hallo [Azure-portal](https://portal.azure.com), selecteer **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="8851f-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![Nieuw selecteren](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="8851f-125">Zoeken naar **webtoepassing + SQL** en selecteer het uit de beschikbare opties Hallo.</span><span class="sxs-lookup"><span data-stu-id="8851f-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![zoeken naar web-app + SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="8851f-127">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="8851f-127">Select **Create**.</span></span>

      ![Maken selecteren](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="8851f-129">Hallo vereist waarden opgeven voor het Hallo-webtoepassing en SQL-database.</span><span class="sxs-lookup"><span data-stu-id="8851f-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="8851f-130">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="8851f-130">Select **Create**.</span></span>

      ![waarden voor web-app en SQL-database opgeven](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="8851f-132">Hallo-implementatie kan een paar minuten duren.</span><span class="sxs-lookup"><span data-stu-id="8851f-132">hello deployment may take a minute.</span></span> <span data-ttu-id="8851f-133">Nadat het Hallo-implementatie is voltooid, bevat uw abonnement Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="8851f-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="8851f-134">Sjabloon weergeven vanuit implementatiegeschiedenis</span><span class="sxs-lookup"><span data-stu-id="8851f-134">View template from deployment history</span></span>
1. <span data-ttu-id="8851f-135">Ga toohello resourcegroepblade voor uw nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8851f-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="8851f-136">Let op dat die blade Hallo Hallo resultaten van de laatste implementatie Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8851f-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="8851f-137">Selecteer deze koppeling.</span><span class="sxs-lookup"><span data-stu-id="8851f-137">Select this link.</span></span>
   
      ![resourcegroepblade](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="8851f-139">U ziet een geschiedenis van de implementaties voor Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="8851f-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="8851f-140">In uw geval bevat Hallo blade waarschijnlijk slechts een implementatie.</span><span class="sxs-lookup"><span data-stu-id="8851f-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="8851f-141">Selecteer deze implementatie.</span><span class="sxs-lookup"><span data-stu-id="8851f-141">Select this deployment.</span></span>
   
     ![laatste implementatie](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="8851f-143">Hallo-blade geeft een samenvatting van Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="8851f-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="8851f-144">Hallo samenvatting bevat Hallo status van Hallo-implementatie en bewerkingen en Hallo-waarden die u hebt opgegeven voor de parameters.</span><span class="sxs-lookup"><span data-stu-id="8851f-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="8851f-145">toosee hello sjabloon die u voor implementatie hello, selecteer gebruikt **sjabloon weergeven**.</span><span class="sxs-lookup"><span data-stu-id="8851f-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![implementatiesamenvatting bekijken](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="8851f-147">Resource Manager haalt Hallo zeven bestanden voor u te volgen:</span><span class="sxs-lookup"><span data-stu-id="8851f-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="8851f-148">**Sjabloon** -Hallo-sjabloon die Hallo-infrastructuur voor uw oplossing definieert.</span><span class="sxs-lookup"><span data-stu-id="8851f-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="8851f-149">Tijdens het maken van Hallo storage-account via de portal Hallo Resource Manager een sjabloon toodeploy gebruikt deze en de sjabloon is opgeslagen voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="8851f-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="8851f-150">**Parameters** -een parameterbestand dat u toopass waarden tijdens de implementatie kunt.</span><span class="sxs-lookup"><span data-stu-id="8851f-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="8851f-151">Hallo waarden bevat die u hebt opgegeven tijdens de eerste implementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="8851f-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="8851f-152">U kunt deze waarden wijzigen wanneer u Hallo sjabloon opnieuw implementeert.</span><span class="sxs-lookup"><span data-stu-id="8851f-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="8851f-153">**CLI** -Azure vanaf de opdrachtregel-line-interface (CLI) scriptbestand dat u toodeploy Hallo sjabloon kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8851f-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="8851f-154">**CLI 2.0** -Azure vanaf de opdrachtregel-line-interface (CLI) scriptbestand dat u toodeploy Hallo sjabloon kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8851f-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="8851f-155">**PowerShell** -een Azure PowerShell-scriptbestand dat u toodeploy Hallo sjabloon kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8851f-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="8851f-156">**.NET** -A .NET-klasse die u toodeploy Hallo sjabloon kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8851f-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="8851f-157">**Ruby** -A Ruby-klasse die u toodeploy Hallo sjabloon kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8851f-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="8851f-158">Hallo-bestanden zijn beschikbaar via de koppelingen tussen Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="8851f-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="8851f-159">Standaard worden Hallo blade Hallo sjabloon weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8851f-159">By default, hello blade displays hello template.</span></span>
      
       ![sjabloon weergeven](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="8851f-161">Deze sjabloon is de werkelijke sjabloon Hallo toocreate gebruikt uw web-app en de SQL-database.</span><span class="sxs-lookup"><span data-stu-id="8851f-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="8851f-162">U ziet dat deze parameters waarmee u verschillende waarden voor de tooprovide tijdens de implementatie bevat.</span><span class="sxs-lookup"><span data-stu-id="8851f-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="8851f-163">Zie toolearn meer informatie over het Hallo-structuur van een sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8851f-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="8851f-164">Hallo-sjabloon uit de resourcegroep exporteren</span><span class="sxs-lookup"><span data-stu-id="8851f-164">Export hello template from resource group</span></span>
<span data-ttu-id="8851f-165">Als u handmatig gewijzigd van uw resources of resources toegevoegd in meerdere implementaties, komt bij het ophalen van een sjabloon van Hallo implementatiegeschiedenis niet overeen met huidige status van de resourcegroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8851f-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="8851f-166">Deze sectie leest u hoe tooexport een sjabloon die overeenkomt met de huidige status van de resourcegroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8851f-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="8851f-167">U kunt geen sjablonen voor een resourcegroep met meer dan 200 bronnen exporteren.</span><span class="sxs-lookup"><span data-stu-id="8851f-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="8851f-168">tooview hello sjabloon voor een resourcegroep, selecteer **automatiseringsscript**.</span><span class="sxs-lookup"><span data-stu-id="8851f-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![resourcegroep exporteren](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="8851f-170">Resource Manager Hallo resources in de resourcegroep Hallo geëvalueerd en genereert een sjabloon voor deze resources.</span><span class="sxs-lookup"><span data-stu-id="8851f-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="8851f-171">Niet alle brontypen Hallo export sjabloonfunctie.</span><span class="sxs-lookup"><span data-stu-id="8851f-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="8851f-172">Mogelijk ziet u een foutmelding weergegeven dat er een probleem met Hallo exporteren is.</span><span class="sxs-lookup"><span data-stu-id="8851f-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="8851f-173">U leert hoe toohandle die problemen bij Hallo [problemen met het exporteren van Fix](#fix-export-issues) sectie.</span><span class="sxs-lookup"><span data-stu-id="8851f-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="8851f-174">Er wordt opnieuw zes Hallo-bestanden die u tooredeploy Hallo oplossing kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8851f-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="8851f-175">Deze tijd Hallo-sjabloon is echter enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="8851f-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="8851f-176">U ziet dat deze gegenereerde sjabloon Hallo bevat minder parameters dan Hallo-sjabloon in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="8851f-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="8851f-177">Veel van de waarden hello (zoals de locatie en de SKU-waarden) zijn ook hardgecodeerd in deze sjabloon in plaats van een parameterwaarde accepteren.</span><span class="sxs-lookup"><span data-stu-id="8851f-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="8851f-178">Vóór het hergebruik van deze sjabloon kunt u tooedit Hallo sjabloon toomake beter gebruik van parameters.</span><span class="sxs-lookup"><span data-stu-id="8851f-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="8851f-179">U hebt een aantal opties voor u doorgaat toowork met deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8851f-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="8851f-180">Hallo-sjabloon downloaden en deze lokaal werkt met een JSON-editor.</span><span class="sxs-lookup"><span data-stu-id="8851f-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="8851f-181">Of u kunt de sjabloonbibliotheek tooyour Hallo opslaan en werken via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="8851f-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="8851f-182">Als u vertrouwd met een JSON-editor zoals bent [tegenover Code](https://code.visualstudio.com/) of [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), werkt u liever lokaal Hallo-sjabloon downloaden en gebruiken van deze editor.</span><span class="sxs-lookup"><span data-stu-id="8851f-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="8851f-183">toowork lokaal, selecteer **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="8851f-183">toowork locally, select **Download**.</span></span>
   
      ![sjabloon downloaden](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="8851f-185">Als u niet zijn ingesteld met een JSON-editor, kunt u liever bewerken Hallo sjabloon via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="8851f-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="8851f-186">Hallo rest van dit onderwerp wordt ervan uitgegaan dat u hebt de sjabloonbibliotheek tooyour Hallo opgeslagen in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="8851f-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="8851f-187">U er echter Hallo dezelfde syntaxis toohello sjabloon wijzigt of lokaal werkt met een JSON-editor of via het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="8851f-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="8851f-188">toowork via Hallo-portal, selecteer **toolibrary toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8851f-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![toolibrary toevoegen](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="8851f-190">Wanneer u een sjabloon toohello bibliotheek toevoegt, geeft u Hallo sjabloon een naam en beschrijving.</span><span class="sxs-lookup"><span data-stu-id="8851f-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="8851f-191">Selecteer vervolgens **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8851f-191">Then, select **Save**.</span></span>
   
     ![sjabloonwaarden instellen](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="8851f-193">Selecteer een sjabloon in de bibliotheek opgeslagen tooview **meer services**, type **sjablonen** toofilter resultaten, selecteer **sjablonen**.</span><span class="sxs-lookup"><span data-stu-id="8851f-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![sjablonen zoeken](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="8851f-195">Selecteer de sjabloon Hallo met Hallo-naam die u hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8851f-195">Select hello template with hello name you saved.</span></span>
   
      ![sjabloon selecteren](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="8851f-197">Hallo-sjabloon aanpassen</span><span class="sxs-lookup"><span data-stu-id="8851f-197">Customize hello template</span></span>
<span data-ttu-id="8851f-198">Hallo geëxporteerde sjabloon werkt goed dat als u wilt dat toocreate Hallo dezelfde web-app en SQL-database voor elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="8851f-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="8851f-199">Resource Manager biedt echter opties die u in staat stellen sjablonen met veel meer flexibiliteit te implementeren.</span><span class="sxs-lookup"><span data-stu-id="8851f-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="8851f-200">Dit artikel laat zien hoe tooadd parameters op voor het Hallo-database de beheerdersnaam van de en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8851f-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="8851f-201">U kunt deze dezelfde benadering tooadd meer flexibiliteit voor andere waarden in de sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="8851f-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="8851f-202">toocustomize hello sjabloon, selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="8851f-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![sjabloon weergeven](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="8851f-204">Hallo-sjabloon selecteren.</span><span class="sxs-lookup"><span data-stu-id="8851f-204">Select hello template.</span></span>
   
     ![sjabloon bewerken](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="8851f-206">toobe kunnen toopass Hallo waarden die u toospecify tijdens de implementatie wellicht toevoegen Hallo na twee parameters toohello **parameters** sectie in Hallo sjabloon:</span><span class="sxs-lookup"><span data-stu-id="8851f-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="8851f-207">toouse hello nieuwe parameters, Hallo SQL server-definitie in Hallo vervangen **resources** sectie.</span><span class="sxs-lookup"><span data-stu-id="8851f-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="8851f-208">U ziet dat **administratorLogin** en **administratorLoginPassword** nu parameterwaarden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8851f-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="8851f-209">Selecteer **OK** als u klaar bewerken Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8851f-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="8851f-210">Selecteer **opslaan** toosave Hallo wijzigingen toohello sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8851f-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![sjabloon opslaan](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="8851f-212">tooredeploy hello bijgewerkt sjabloon, selecteer **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="8851f-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![sjabloon implementeren](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="8851f-214">Parameterwaarden opgeven en selecteer een resource groep toodeploy Hallo bronnen.</span><span class="sxs-lookup"><span data-stu-id="8851f-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="8851f-215">Problemen met exports oplossen</span><span class="sxs-lookup"><span data-stu-id="8851f-215">Fix export issues</span></span>
<span data-ttu-id="8851f-216">Niet alle brontypen Hallo export sjabloonfunctie.</span><span class="sxs-lookup"><span data-stu-id="8851f-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="8851f-217">Dit probleem handmatig tooresolve Hallo ontbrekende resources toevoegen terug in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8851f-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="8851f-218">Fout bij het Hallo-bericht bevat Hallo brontypen die niet kunnen worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="8851f-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="8851f-219">Zoek dat resourcetype in de Engelstalige [naslaghandleiding over sjablonen](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="8851f-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="8851f-220">Bijvoorbeeld, toomanually toevoegen van een virtuele netwerkgateway, Zie [Microsoft.Network/virtualNetworkGateways sjabloonverwijzing](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="8851f-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="8851f-221">Exporteren geeft alleen problemen bij het exporteren vanuit een resourcegroep, niet bij het exporteren vanuit de geschiedenis van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="8851f-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="8851f-222">Als uw laatste implementatie nauwkeurig Hallo huidige status van de resourcegroep hello vertegenwoordigt, moet u Hallo sjabloon exporteren uit Hallo implementatiegeschiedenis in plaats van vanaf Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8851f-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="8851f-223">Alleen exporteren uit een resourcegroep wanneer u wijzigingen toohello resourcegroep die niet zijn gedefinieerd in één sjabloon hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8851f-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8851f-224">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8851f-224">Next steps</span></span>
<span data-ttu-id="8851f-225">U hebt geleerd hoe een sjabloon uit resources die u hebt gemaakt in de portal Hallo tooexport.</span><span class="sxs-lookup"><span data-stu-id="8851f-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="8851f-226">U kunt een sjabloon implementeren via [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md) of [REST API](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="8851f-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="8851f-227">hoe een sjabloon via PowerShell, tooexport zien toosee [Azure PowerShell gebruiken met Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8851f-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="8851f-228">hoe een sjabloon via Azure CLI tooexport zien toosee [gebruik hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8851f-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

