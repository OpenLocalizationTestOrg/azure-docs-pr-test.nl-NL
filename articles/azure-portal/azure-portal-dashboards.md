---
title: aaaCreate en Azure portal dashboards delen | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe dashboards toocreate en bewerken in hello Azure-portal.
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a><span data-ttu-id="0fbe4-103">Maken en delen van dashboards in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0fbe4-103">Create and share dashboards in hello Azure portal</span></span>
<span data-ttu-id="0fbe4-104">U kunt meerdere dashboards maken en ze delen met anderen die toegang tooyour Azure hebben abonnementen.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-104">You can create multiple dashboards and share them with others who have access tooyour Azure subscriptions.</span></span>  <span data-ttu-id="0fbe4-105">In dit artikel gaat door Hallo grondbeginselen van het maken, bewerken, publiceren en beheren van toegang toodashboards.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-105">This article goes through hello basics of creating, editing, publishing, and managing access toodashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="0fbe4-106">Een dashboard maken</span><span class="sxs-lookup"><span data-stu-id="0fbe4-106">Create a dashboard</span></span>
<span data-ttu-id="0fbe4-107">toocreate een dashboard, selecteer Hallo **nieuwe dashboard** knop volgende toohello huidige de naam van dashboard.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-107">toocreate a dashboard, select hello **New dashboard** button next toohello current dashboard's name.</span></span>  

![dashboard maken](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="0fbe4-109">Deze actie wordt een nieuw, leeg, persoonlijke dashboard gemaakt en wordt u aanpassing modus kunt u uw dashboard name en toevoegen of tegels opnieuw rangschikken.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="0fbe4-110">In deze modus tegel Hallo samenvouwbare galerie vergt via Hallo linkernavigatievenster menu.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-110">When in this mode, hello collapsible tile gallery takes over hello left navigation menu.</span></span>  <span data-ttu-id="0fbe4-111">Hallo tegel galerij kunt u tegels vinden voor uw Azure-resources op verschillende manieren: u kunt bladeren door [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups), door resource typt, by [tag](../azure-resource-manager/resource-group-using-tags.md), of door te zoeken voor uw resource met de naam.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-111">hello tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![dashboard aanpassen](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="0fbe4-113">Tegels toevoegen door slepen en neerzetten op Hallo dashboard oppervlak elke gewenste locatie.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-113">Add tiles by dragging and dropping them onto hello dashboard surface wherever you want.</span></span>

<span data-ttu-id="0fbe4-114">Er is een nieuwe categorie met de naam **algemene** voor tegels die niet gekoppeld aan een bepaalde bron zijn.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="0fbe4-115">In dit voorbeeld vastmaken we Hallo Markdown tegel.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-115">In this example, we pin hello Markdown tile.</span></span>  <span data-ttu-id="0fbe4-116">U dit dashboard tegel tooadd aangepaste inhoud tooyour gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-116">You use this tile tooadd custom content tooyour dashboard.</span></span>  <span data-ttu-id="0fbe4-117">Hallo tegel ondersteunt tekst zonder opmaak, [Markdown-syntaxis](https://daringfireball.net/projects/markdown/syntax), en een beperkte set van HTML-code.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-117">hello tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="0fbe4-118">(Voor de veiligheid, niet zoiets als injecteren `<script>` tags of bepaalde element stijlen van CSS die met het Hallo-portal conflicteren mogelijk gebruiken.)</span><span class="sxs-lookup"><span data-stu-id="0fbe4-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with hello portal.)</span></span> 

![markdown toevoegen](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="0fbe4-120">Een dashboard bewerken</span><span class="sxs-lookup"><span data-stu-id="0fbe4-120">Edit a dashboard</span></span>
<span data-ttu-id="0fbe4-121">Nadat uw dashboard is gemaakt, kunt u tegels van Hallo tegel galerie of Hallo tegel representatie van blades vastmaken.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-121">After creating your dashboard, you can pin tiles from hello tile gallery or hello tile representation of blades.</span></span> <span data-ttu-id="0fbe4-122">Laten we vastmaken Hallo-weergave van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-122">Let's pin hello representation of our resource group.</span></span> <span data-ttu-id="0fbe4-123">U kunt ofwel bij het bladeren door Hallo item, of van de resourcegroepblade Hallo vastmaken.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-123">You can either pin when browsing hello item, or from hello resource group blade.</span></span> <span data-ttu-id="0fbe4-124">Beide benaderingen leiden tot Hallo tegel weergave van de resourcegroep Hallo vastmaken.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-124">Both approaches result in pinning hello tile representation of hello resource group.</span></span>

![Pincode toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="0fbe4-126">Na het vastmaken Hallo item, wordt deze weergegeven op uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-126">After pinning hello item, it appears on your dashboard.</span></span>

![weergave-dashboard](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="0fbe4-128">Nu dat we een Markdown-tegel en een dashboard resource groep vastgemaakt toohello hebben, kunnen we vergroten of verkleinen en Hallo tegels rangschikken in een geschikte indeling.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-128">Now that we have a Markdown tile and a resource group pinned toohello dashboard, we can resize and rearrange hello tiles into a suitable layout.</span></span>

<span data-ttu-id="0fbe4-129">Door de muiswijzer en '...' selecteren of met de rechtermuisknop op een tegel ziet u alle contextuele Hallo-opdrachten voor deze tegel.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-129">By hovering and selecting "…" or right-clicking on a tile you can see all hello contextual commands for that tile.</span></span> <span data-ttu-id="0fbe4-130">Standaard zijn er twee items:</span><span class="sxs-lookup"><span data-stu-id="0fbe4-130">By default, there are two items:</span></span>

1. <span data-ttu-id="0fbe4-131">**Losmaken van dashboard** – verwijdert Hallo tegel vanuit Hallo-dashboard</span><span class="sxs-lookup"><span data-stu-id="0fbe4-131">**Unpin from dashboard** – removes hello tile from hello dashboard</span></span>
2. <span data-ttu-id="0fbe4-132">**Aanpassen** – krijgt de modus aanpassen</span><span class="sxs-lookup"><span data-stu-id="0fbe4-132">**Customize** – enters customize mode</span></span>

![tegel aanpassen](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="0fbe4-134">Door te selecteren aanpassen, kunt u het formaat en tegels opnieuw rangschikken.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="0fbe4-135">tooresize een tegel, selecteer Hallo nieuwe grootte in Hallo contextafhankelijke menu, zoals wordt weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-135">tooresize a tile, select hello new size from hello contextual menu, as shown in hello following image.</span></span>

![tegel vergroten of verkleinen](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="0fbe4-137">Of als Hallo tegel elke grootte ondersteunt, kunt u Hallo onder rechterhoek toohello gewenst grootte.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-137">Or, if hello tile supports any size, you can drag hello bottom right-hand corner toohello desired size.</span></span>

![tegel vergroten of verkleinen](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="0fbe4-139">Na het formaat van tegels wijzigen, moet u Hallo-dashboard weergeven.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-139">After resizing tiles, view hello dashboard.</span></span>

![tegel](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="0fbe4-141">Zodra u klaar bent met een dashboard aanpassen, selecteert u Hallo **gedaan aanpassen** tooexit modus aanpassen of met de rechtermuisknop op en selecteer **gedaan aanpassen** in het contextmenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-141">Once you are finished customizing a dashboard, simply select hello **Done customizing** tooexit customize mode or right-click and select **Done customizing** from hello context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="0fbe4-142">Een dashboard publiceren en beheren van toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="0fbe4-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="0fbe4-143">Wanneer u een dashboard maakt, is het persoonlijke standaard, wat betekent dat u bent Hallo enige die deze kan zien.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-143">When you create a dashboard, it is private by default, which means you are hello only person who can see it.</span></span>  <span data-ttu-id="0fbe4-144">toomake deze zichtbaar tooothers gebruiken Hallo **Share** knop die wordt weergegeven naast de andere opdrachten dashboard Hallo.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-144">toomake it visible tooothers, use hello **Share** button that appears alongside hello other dashboard commands.</span></span>

![dashboard delen](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="0fbe4-146">U wordt gevraagd een abonnement en de resource-groep voor uw dashboard toobe gepubliceerd naar toochoose.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-146">You are asked toochoose a subscription and resource group for your dashboard toobe published to.</span></span> <span data-ttu-id="0fbe4-147">tooseamlessly dashboards integreren in Hallo ecosysteem, we hebben gedeelde dashboards geïmplementeerd als Azure-resources (zodat u niet delen door een e-mailadres in te voeren).</span><span class="sxs-lookup"><span data-stu-id="0fbe4-147">tooseamlessly integrate dashboards into hello ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="0fbe4-148">Toegang tot toohello informatie weergegeven voor de meeste Hallo tegels in Hallo portal vallen [Azure Toegangsbeheerrol](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0fbe4-148">Access toohello information displayed by most of hello tiles in hello portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="0fbe4-149">Gedeelde dashboards zijn vanuit een access control-perspectief niet anders als een virtuele machine of een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="0fbe4-150">Stel dat u hebt een Azure-abonnement en leden van uw team zijn toegewezen rollen Hallo van **eigenaar**, **Inzender**, of **lezer** van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-150">Let's say you have an Azure subscription and members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** of hello subscription.</span></span>  <span data-ttu-id="0fbe4-151">Gebruikers die eigenaar of inzenders kunnen toolist, weergave zijn, maken, wijzigen of verwijderen van dashboards binnen dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-151">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="0fbe4-152">Gebruikers die lezers zijn kunnen toolist en bekijk de dashboards zijn, maar kunnen niet worden gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-152">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="0fbe4-153">Gebruikers met leestoegang hebben kunnen toomake lokale bewerkingen tooa gedeelde dashboard zijn, maar er kan geen toopublish zijn die wijzigingen back toohello-server.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-153">Users with reader access are able toomake local edits tooa shared dashboard, but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="0fbe4-154">Ze kunnen echter een persoonlijke kopie van Hallo dashboard voor eigen gebruik maken.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-154">However, they can make a private copy of hello dashboard for their own use.</span></span>  <span data-ttu-id="0fbe4-155">Afzonderlijke tegels op Hallo dashboard afdwingen als altijd hun eigen regels voor toegang op basis van Hallo bronnen die ze met overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-155">As always, individual tiles on hello dashboard enforce their own access control rules based on hello resources they correspond to.</span></span>  

<span data-ttu-id="0fbe4-156">Voor het gemak Hallo portal ervaring handleidingen u naar een patroon waar u dashboards in een resourcegroep plaatsen opgeroepen de publiceren **dashboards**.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-156">For convenience, hello portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![dashboard publiceren](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="0fbe4-158">U kunt een resourcegroep dashboard tooa bepaalde ook toopublish.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-158">You can also choose toopublish a dashboard tooa particular resource group.</span></span>  <span data-ttu-id="0fbe4-159">Hallo-toegangsbeheer voor dit dashboard komt overeen met de Hallo toegangsbeheer voor Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-159">hello access control for that dashboard matches hello access control for hello resource group.</span></span>  <span data-ttu-id="0fbe4-160">Gebruikers die kunnen resources in die resourcegroep Hallo beheren hebben ook toegang toohello dashboards.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-160">Users that can manage hello resources in that resource group also have access toohello dashboards.</span></span>

![dashboard tooresource groep publiceren](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="0fbe4-162">Nadat uw dashboard is gepubliceerd, Hallo **delen + toegang** besturingselementvenster wordt vernieuwen en u meer informatie over Hallo gepubliceerde dashboard, met inbegrip van een koppeling toomanage toegang toohello gebruikersdashboard weergeven.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-162">After your dashboard is published, hello **Sharing + access** control pane will refresh and show you information about hello published dashboard, including a link toomanage user access toohello dashboard.</span></span>  <span data-ttu-id="0fbe4-163">Deze koppeling wordt gestart Hallo standaard rollen gebaseerd toegangsbeheer blade gebruikt toomanage toegang voor een Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-163">This link launches hello standard Role Based Access Control blade used toomanage access for any Azure resource.</span></span>  <span data-ttu-id="0fbe4-164">U kunt altijd teruggaan toothis weergeven door te selecteren **Share**.</span><span class="sxs-lookup"><span data-stu-id="0fbe4-164">You can always get back toothis view by selecting **Share**.</span></span>

![toegang beheren](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="0fbe4-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0fbe4-166">Next steps</span></span>
* <span data-ttu-id="0fbe4-167">toomanage resources, Zie [beheren Azure-resources via de portal](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0fbe4-167">toomanage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="0fbe4-168">toodeploy resources, Zie [implementeren van resources met Resource Manager-sjablonen en Azure-portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0fbe4-168">toodeploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

