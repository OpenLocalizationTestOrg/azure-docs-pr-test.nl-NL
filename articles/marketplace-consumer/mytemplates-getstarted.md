---
title: aaaGet slag met persoonlijke sjablonen | Microsoft Docs
description: Toevoegen, beheren en delen van uw persoonlijke sjablonen met hello Azure-portal, hello Azure CLI of PowerShell.
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="fc846-103">Aan de slag met persoonlijke sjablonen in hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fc846-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="fc846-104">Een [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) sjabloon is een declaratief sjabloon gebruikt toodefine uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="fc846-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="fc846-105">U kunt definiëren Hallo resources toodeploy voor een oplossing en geef parameters en variabelen die u in staat tooinput waarden voor verschillende omgevingen stellen.</span><span class="sxs-lookup"><span data-stu-id="fc846-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="fc846-106">Hallo sjabloon bestaat uit JSON en uitdrukkingen die u kunt tooconstruct waarden voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="fc846-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="fc846-107">Kunt u Hallo nieuwe **sjablonen** mogelijkheden in Hallo [Azure Portal](https://portal.azure.com) samen met de Hallo **Microsoft.Gallery** resourceprovider als een uitbreiding van Hallo [ Azure Marketplace](https://azure.microsoft.com/marketplace/) toocreate tooenable gebruikers, beheren en implementeren van persoonlijke sjablonen vanuit een persoonlijke bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="fc846-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="fc846-108">Dit document vindt u bij het toevoegen, beheren en delen van een persoonlijk **sjabloon** met behulp van hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="fc846-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="fc846-109">Richtlijnen</span><span class="sxs-lookup"><span data-stu-id="fc846-109">Guidance</span></span>
<span data-ttu-id="fc846-110">Hallo volgende tips kunt u profiteren van **sjablonen** bij het werken met uw oplossingen:</span><span class="sxs-lookup"><span data-stu-id="fc846-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="fc846-111">Een **sjabloon** is een inkapselende resource met een Resource Manager-sjabloon en aanvullende metagegevens.</span><span class="sxs-lookup"><span data-stu-id="fc846-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="fc846-112">Dit werkt op dezelfde manier tooan item in Hallo Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fc846-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="fc846-113">Hallo belangrijkste verschil is dat het een persoonlijk item als tegengestelde toohello openbaar Marketplace-item is.</span><span class="sxs-lookup"><span data-stu-id="fc846-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="fc846-114">Hallo **sjablonen** bibliotheek geschikt is voor gebruikers hoeven toocustomize implementaties.</span><span class="sxs-lookup"><span data-stu-id="fc846-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="fc846-115">**Sjablonen** zijn handig voor gebruikers die een eenvoudige opslagplaats in Azure nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="fc846-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="fc846-116">Begin met een bestaand Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="fc846-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="fc846-117">Zoek sjablonen in [github](https://github.com/Azure/azure-quickstart-templates) of [exporteer een sjabloon](../azure-resource-manager/resource-manager-export-template.md) vanuit een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fc846-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="fc846-118">**Sjablonen** gebonden toohello-gebruiker die deze publiceert.</span><span class="sxs-lookup"><span data-stu-id="fc846-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="fc846-119">Hallo de naam van uitgever is zichtbaar tooeveryone die tooit leestoegang heeft.</span><span class="sxs-lookup"><span data-stu-id="fc846-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="fc846-120">**Sjablonen** zijn resources van de Resource Manager en kunnen na publicatie niet meer worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="fc846-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="fc846-121">Een sjabloonresource toevoegen</span><span class="sxs-lookup"><span data-stu-id="fc846-121">Add a Template resource</span></span>
<span data-ttu-id="fc846-122">Er zijn twee manieren toocreate een **sjabloon** resource in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc846-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="fc846-123">Methode 1: Maak een nieuwe sjabloonresource vanuit een bestaande resourcegroep</span><span class="sxs-lookup"><span data-stu-id="fc846-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="fc846-124">Navigeer tooan bestaande resourcegroep in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="fc846-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="fc846-125">Klik op **Sjabloon exporteren** in **Instellingen**.</span><span class="sxs-lookup"><span data-stu-id="fc846-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="fc846-126">Zodra het Hallo Resource Manager-sjabloon is geëxporteerd, gebruikt u Hallo **sjabloon opslaan** knop toosave het toohello **sjablonen** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="fc846-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="fc846-127">Meer informatie over het exporteren van sjablonen vindt u [hier](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="fc846-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="fc846-128">
   ![Resourcegroep exporteren](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="fc846-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="fc846-129">Selecteer Hallo **tooTemplate opslaan** opdrachtknop.</span><span class="sxs-lookup"><span data-stu-id="fc846-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="fc846-130">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="fc846-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="fc846-131">Naam: naam van het object hello (Opmerking: dit is een naam op basis van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc846-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="fc846-132">Alle naamsbeperkingen zijn van toepassing en de naam kan achteraf niet meer worden gewijzigd).</span><span class="sxs-lookup"><span data-stu-id="fc846-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="fc846-133">Beschrijving – korte samenvatting van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="fc846-133">Description – Quick summary about hello template.</span></span>
     
     ![Sjabloon opslaan](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="fc846-135">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fc846-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fc846-136">Hallo blade sjabloon exporteren geeft een melding weer wanneer hello geëxporteerde Resource Manager-sjabloon fouten bevat, maar u kunt nog steeds kunnen toosave deze Resource Manager-sjabloon toohello sjablonen.</span><span class="sxs-lookup"><span data-stu-id="fc846-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="fc846-137">Zorg ervoor dat Controleer en corrigeer eventuele Resource Manager voordat opnieuw distribueren Hallo geëxporteerd Resource Manager-sjabloon sjabloonproblemen.</span><span class="sxs-lookup"><span data-stu-id="fc846-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="fc846-138">Methode 2: Een nieuwe sjabloonresource toevoegen door middel van bladeren</span><span class="sxs-lookup"><span data-stu-id="fc846-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="fc846-139">U kunt ook toevoegen een nieuwe **sjabloon** helemaal met Hallo + knop toevoegen in **Bladeren > sjablonen**.</span><span class="sxs-lookup"><span data-stu-id="fc846-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="fc846-140">U moet een naam, beschrijving en Hallo Resource Manager-sjabloon JSON tooprovide.</span><span class="sxs-lookup"><span data-stu-id="fc846-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![Sjabloon toevoegen](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="fc846-142">Microsoft.Gallery is een op tenants gebaseerde resourceprovider van Azure.</span><span class="sxs-lookup"><span data-stu-id="fc846-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="fc846-143">Hallo is sjabloonresource gebonden toohello-gebruiker die deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fc846-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="fc846-144">Het is niet gebonden tooany bepaald abonnement.</span><span class="sxs-lookup"><span data-stu-id="fc846-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="fc846-145">Een abonnement moet toobe ervoor gekozen alleen bij het implementeren van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="fc846-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="fc846-146">Sjabloonresources bekijken</span><span class="sxs-lookup"><span data-stu-id="fc846-146">View Template resources</span></span>
<span data-ttu-id="fc846-147">Alle **sjablonen** tooyou beschikbaar die kan worden weergegeven wanneer **Bladeren > sjablonen**.</span><span class="sxs-lookup"><span data-stu-id="fc846-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="fc846-148">Dit zijn zowel **sjablonen** die u hebt gemaakt als sjablonen met verschillende bevoegdheidsniveaus die met u zijn gedeeld.</span><span class="sxs-lookup"><span data-stu-id="fc846-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="fc846-149">Meer informatie in Hallo [toegangsbeheer](#access-control-for-a-tenant-resource-provider) hieronder.</span><span class="sxs-lookup"><span data-stu-id="fc846-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Sjabloon weergeven](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="fc846-151">U kunt Hallo weergeven van een **sjabloon** door te klikken op een item in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc846-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![Sjabloon weergeven](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="fc846-153">Een sjabloonresource bewerken</span><span class="sxs-lookup"><span data-stu-id="fc846-153">Edit a Template resource</span></span>
<span data-ttu-id="fc846-154">U kunt starten Hallo bewerken stroom voor een **sjabloon** door Hallo-item op Hallo zoeklijst rechtermuisknop te klikken of door te kiezen opdrachtknop Hallo-bewerken.</span><span class="sxs-lookup"><span data-stu-id="fc846-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![Sjabloon bewerken](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="fc846-156">U kunt Hallo beschrijving of de sjabloontekst van Resource Manager-bewerken.</span><span class="sxs-lookup"><span data-stu-id="fc846-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="fc846-157">U kunt Hallo-naam niet bewerken omdat deze de naam van een Resource Manager-resource.</span><span class="sxs-lookup"><span data-stu-id="fc846-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="fc846-158">Wanneer u Hallo Resource Manager-sjabloon JSON bewerkt zullen we dit valideren tooensure dat het een geldige JSON is.</span><span class="sxs-lookup"><span data-stu-id="fc846-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="fc846-159">Kies **OK** en vervolgens **opslaan** toosave uw bijgewerkte sjabloon.</span><span class="sxs-lookup"><span data-stu-id="fc846-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![Sjabloon bewerken](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="fc846-161">Eenmaal Hallo **sjabloon** wordt opgeslagen ziet u een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc846-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![Sjabloon bewerken](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="fc846-163">Een sjabloonresource implementeren</span><span class="sxs-lookup"><span data-stu-id="fc846-163">Deploy a Template resource</span></span>
<span data-ttu-id="fc846-164">U kunt elk **sjabloon** implementeren waarvoor u een **lees**machtiging heeft.</span><span class="sxs-lookup"><span data-stu-id="fc846-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="fc846-165">Hallo implementatie stroom wordt Hallo standaard Azure-sjabloon implementatie blade gestart.</span><span class="sxs-lookup"><span data-stu-id="fc846-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="fc846-166">Vul Hallo waarden voor Hallo Resource Manager-sjabloon parameters tooproceed met Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="fc846-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![Sjabloon implementeren](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="fc846-168">Een sjabloonresource delen</span><span class="sxs-lookup"><span data-stu-id="fc846-168">Share a Template resource</span></span>
<span data-ttu-id="fc846-169">U kunt een **sjabloon**resource delen met anderen.</span><span class="sxs-lookup"><span data-stu-id="fc846-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="fc846-170">Delen gedraagt zich op dezelfde manier te[roltoewijzing voor een resource in Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="fc846-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="fc846-171">Hallo **sjabloon** eigenaar biedt machtigingen tooother gebruikers die kunnen communiceren met een sjabloonresource.</span><span class="sxs-lookup"><span data-stu-id="fc846-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="fc846-172">Hallo persoon of groep personen die u deelt Hallo **sjabloon** met worden kunnen toosee Hallo Resource Manager-sjabloon en de galerie-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="fc846-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="fc846-173">Toegangsbeheer voor Microsoft.Gallery-resources Hallo</span><span class="sxs-lookup"><span data-stu-id="fc846-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="fc846-174">Rol</span><span class="sxs-lookup"><span data-stu-id="fc846-174">Role</span></span> | <span data-ttu-id="fc846-175">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="fc846-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="fc846-176">Eigenaar</span><span class="sxs-lookup"><span data-stu-id="fc846-176">Owner</span></span> |<span data-ttu-id="fc846-177">Volledige controle over de sjabloonresource Hallo onder andere het delen</span><span class="sxs-lookup"><span data-stu-id="fc846-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="fc846-178">Lezer</span><span class="sxs-lookup"><span data-stu-id="fc846-178">Reader</span></span> |<span data-ttu-id="fc846-179">Sjabloonresource lezen en kunnen op Hallo sjabloonresource</span><span class="sxs-lookup"><span data-stu-id="fc846-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="fc846-180">Inzender</span><span class="sxs-lookup"><span data-stu-id="fc846-180">Contributor</span></span> |<span data-ttu-id="fc846-181">Kunnen bewerken en verwijderen op Hallo sjabloonresource.</span><span class="sxs-lookup"><span data-stu-id="fc846-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="fc846-182">Gebruiker delen Hallo sjabloon niet met anderen</span><span class="sxs-lookup"><span data-stu-id="fc846-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="fc846-183">Selecteer **Share** op Hallo bladeritem met de rechtermuisknop te klikken of op Hallo weergave blade van een specifiek item.</span><span class="sxs-lookup"><span data-stu-id="fc846-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="fc846-184">Hiermee opent u een omgeving om het sjabloon te delen.</span><span class="sxs-lookup"><span data-stu-id="fc846-184">This launches a Share experience.</span></span>

![Sjabloon delen](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="fc846-186">U kunt nu een rol en een gebruiker of groep tooprovide toegang tooa bepaalde **sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="fc846-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="fc846-187">Hallo beschikbare rollen zijn eigenaar, lezer en Inzender.</span><span class="sxs-lookup"><span data-stu-id="fc846-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="fc846-188">Meer informatie in Hallo [toegangsbeheer](#access-control-for-a-tenant-resource-provider) sectie hierboven.</span><span class="sxs-lookup"><span data-stu-id="fc846-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Sjabloon delen](media/share-template-portal2b.png)  <br />

![Sjabloon delen](media/share-template-portal3b.png)  <br />

<span data-ttu-id="fc846-191">Klik op **Selecteren** en vervolgens op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="fc846-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="fc846-192">U kunt nu zien Hallo gebruikers of groepen hebt u toohello resource toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fc846-192">You can now see hello users or groups you added toohello resource.</span></span>

![Sjabloon delen](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="fc846-194">Een sjabloon kan alleen worden gedeeld met gebruikers en groepen in Hallo dezelfde Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="fc846-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="fc846-195">Als u een sjabloon met een e-mailadres dat zich niet in uw tenant deelt, wordt een uitnodiging verzonden hello gebruiker toojoin hello tenant als gast waarin wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="fc846-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fc846-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fc846-196">Next steps</span></span>
* <span data-ttu-id="fc846-197">toolearn over het maken van Resource Manager-sjablonen, Zie [sjablonen te bewerken](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="fc846-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="fc846-198">Zie toounderstand Hallo functies die u kunt gebruiken in een Resource Manager-sjabloon [sjabloonfuncties](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="fc846-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="fc846-199">Zie [Best practices voor het ontwerpen van Azure Resource Manager-sjablonen](../azure-resource-manager/best-practices-resource-manager-design-templates.md) voor meer informatie over het ontwerpen van uw sjablonen</span><span class="sxs-lookup"><span data-stu-id="fc846-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

