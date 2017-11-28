---
title: Maken en de Azure portal dashboards delen | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe maken en bewerken van dashboards in de Azure portal.
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
ms.openlocfilehash: 5429e68723448ff5db6ef0ed8da1b927e97e6dd9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-share-dashboards-in-the-azure-portal"></a><span data-ttu-id="beda9-103">Maken en delen van dashboards in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="beda9-103">Create and share dashboards in the Azure portal</span></span>
<span data-ttu-id="beda9-104">U kunt meerdere dashboards maken en ze delen met anderen die toegang tot uw Azure-abonnementen hebben.</span><span class="sxs-lookup"><span data-stu-id="beda9-104">You can create multiple dashboards and share them with others who have access to your Azure subscriptions.</span></span>  <span data-ttu-id="beda9-105">In dit artikel gaat met de grondbeginselen van het maken, bewerken, publiceren en beheren van toegang tot dashboards.</span><span class="sxs-lookup"><span data-stu-id="beda9-105">This article goes through the basics of creating, editing, publishing, and managing access to dashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="beda9-106">Een dashboard maken</span><span class="sxs-lookup"><span data-stu-id="beda9-106">Create a dashboard</span></span>
<span data-ttu-id="beda9-107">Als u een dashboard, selecteert de **nieuwe dashboard** knop naast de naam van het dashboard.</span><span class="sxs-lookup"><span data-stu-id="beda9-107">To create a dashboard, select the **New dashboard** button next to the current dashboard's name.</span></span>  

![dashboard maken](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="beda9-109">Deze actie wordt een nieuw, leeg, persoonlijke dashboard gemaakt en wordt u aanpassing modus kunt u uw dashboard name en toevoegen of tegels opnieuw rangschikken.</span><span class="sxs-lookup"><span data-stu-id="beda9-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="beda9-110">In deze modus, neemt de galerie samenvouwbare tegel op het navigatiemenu links.</span><span class="sxs-lookup"><span data-stu-id="beda9-110">When in this mode, the collapsible tile gallery takes over the left navigation menu.</span></span>  <span data-ttu-id="beda9-111">De tegel galerie kunt u tegels vinden voor uw Azure-resources op verschillende manieren: u kunt bladeren door [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups), door resource typt, by [tag](../azure-resource-manager/resource-group-using-tags.md), of door te zoeken voor uw resource met de naam.</span><span class="sxs-lookup"><span data-stu-id="beda9-111">The tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![dashboard aanpassen](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="beda9-113">Tegels toevoegen door slepen en neerzetten op het dashboard voor aanvallen op elke gewenste locatie.</span><span class="sxs-lookup"><span data-stu-id="beda9-113">Add tiles by dragging and dropping them onto the dashboard surface wherever you want.</span></span>

<span data-ttu-id="beda9-114">Er is een nieuwe categorie met de naam **algemene** voor tegels die niet gekoppeld aan een bepaalde bron zijn.</span><span class="sxs-lookup"><span data-stu-id="beda9-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="beda9-115">In dit voorbeeld wordt de Markdown-tegel vastmaken.</span><span class="sxs-lookup"><span data-stu-id="beda9-115">In this example, we pin the Markdown tile.</span></span>  <span data-ttu-id="beda9-116">Deze tegel kunt u aangepaste inhoud toevoegen aan uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="beda9-116">You use this tile to add custom content to your dashboard.</span></span>  <span data-ttu-id="beda9-117">De tegel ondersteunt tekst zonder opmaak, [Markdown-syntaxis](https://daringfireball.net/projects/markdown/syntax), en een beperkte set van HTML-code.</span><span class="sxs-lookup"><span data-stu-id="beda9-117">The tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="beda9-118">(Voor de veiligheid, niet zoiets als injecteren `<script>` tags of bepaalde element stijlen van CSS die met de portal conflicteren mogelijk gebruiken.)</span><span class="sxs-lookup"><span data-stu-id="beda9-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with the portal.)</span></span> 

![markdown toevoegen](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="beda9-120">Een dashboard bewerken</span><span class="sxs-lookup"><span data-stu-id="beda9-120">Edit a dashboard</span></span>
<span data-ttu-id="beda9-121">Nadat uw dashboard is gemaakt, kunt u tegels van de tegel galerie of de tegel representatie van blades vastmaken.</span><span class="sxs-lookup"><span data-stu-id="beda9-121">After creating your dashboard, you can pin tiles from the tile gallery or the tile representation of blades.</span></span> <span data-ttu-id="beda9-122">Laten we de weergave van onze resourcegroep vastmaken.</span><span class="sxs-lookup"><span data-stu-id="beda9-122">Let's pin the representation of our resource group.</span></span> <span data-ttu-id="beda9-123">Bij het bladeren door het item of vanuit de blade met resourcegroepen kunt u de pincode.</span><span class="sxs-lookup"><span data-stu-id="beda9-123">You can either pin when browsing the item, or from the resource group blade.</span></span> <span data-ttu-id="beda9-124">Beide benaderingen resulteren in de tegel weergave van de resourcegroep vastmaken.</span><span class="sxs-lookup"><span data-stu-id="beda9-124">Both approaches result in pinning the tile representation of the resource group.</span></span>

![Vastmaken aan dashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="beda9-126">Na het vastmaken van het item, wordt deze weergegeven op uw dashboard.</span><span class="sxs-lookup"><span data-stu-id="beda9-126">After pinning the item, it appears on your dashboard.</span></span>

![weergave-dashboard](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="beda9-128">Nu dat we een Markdown-tegel hebben en een resourcegroep is vastgemaakt aan het dashboard, kunnen we vergroten of verkleinen en de tegels rangschikken in een geschikte indeling.</span><span class="sxs-lookup"><span data-stu-id="beda9-128">Now that we have a Markdown tile and a resource group pinned to the dashboard, we can resize and rearrange the tiles into a suitable layout.</span></span>

<span data-ttu-id="beda9-129">Door de muiswijzer en '...' selecteren of met de rechtermuisknop op een tegel ziet u de contextuele opdrachten voor deze tegel.</span><span class="sxs-lookup"><span data-stu-id="beda9-129">By hovering and selecting "…" or right-clicking on a tile you can see all the contextual commands for that tile.</span></span> <span data-ttu-id="beda9-130">Standaard zijn er twee items:</span><span class="sxs-lookup"><span data-stu-id="beda9-130">By default, there are two items:</span></span>

1. <span data-ttu-id="beda9-131">**Losmaken van dashboard** : Hiermee verwijdert u de tegel van het dashboard</span><span class="sxs-lookup"><span data-stu-id="beda9-131">**Unpin from dashboard** – removes the tile from the dashboard</span></span>
2. <span data-ttu-id="beda9-132">**Aanpassen** – krijgt de modus aanpassen</span><span class="sxs-lookup"><span data-stu-id="beda9-132">**Customize** – enters customize mode</span></span>

![tegel aanpassen](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="beda9-134">Door te selecteren aanpassen, kunt u het formaat en tegels opnieuw rangschikken.</span><span class="sxs-lookup"><span data-stu-id="beda9-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="beda9-135">Als u een tegel, selecteert u de nieuwe grootte in de contextafhankelijke menu, zoals wordt weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="beda9-135">To resize a tile, select the new size from the contextual menu, as shown in the following image.</span></span>

![tegel vergroten of verkleinen](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="beda9-137">Of als de tegel elke grootte ondersteunt, kunt u de rechterbovenhoek naar de gewenste grootte slepen.</span><span class="sxs-lookup"><span data-stu-id="beda9-137">Or, if the tile supports any size, you can drag the bottom right-hand corner to the desired size.</span></span>

![tegel vergroten of verkleinen](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="beda9-139">Nadat het formaat van tegels wijzigen, moet u het dashboard weergeven.</span><span class="sxs-lookup"><span data-stu-id="beda9-139">After resizing tiles, view the dashboard.</span></span>

![tegel](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="beda9-141">Zodra u klaar bent met een dashboard aanpassen, selecteer de **gedaan aanpassen** om af te sluiten modus aanpassen of met de rechtermuisknop op en selecteer **gedaan aanpassen** in het contextmenu.</span><span class="sxs-lookup"><span data-stu-id="beda9-141">Once you are finished customizing a dashboard, simply select the **Done customizing** to exit customize mode or right-click and select **Done customizing** from the context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="beda9-142">Een dashboard publiceren en beheren van toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="beda9-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="beda9-143">Wanneer u een dashboard maakt, is het persoonlijke standaard, wat betekent dat u de enige bent die deze kunnen zien.</span><span class="sxs-lookup"><span data-stu-id="beda9-143">When you create a dashboard, it is private by default, which means you are the only person who can see it.</span></span>  <span data-ttu-id="beda9-144">Als u deze zichtbaar voor anderen, gebruikt u de **Share** knop die wordt weergegeven naast de andere opdrachten in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="beda9-144">To make it visible to others, use the **Share** button that appears alongside the other dashboard commands.</span></span>

![dashboard delen](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="beda9-146">U wordt gevraagd een abonnement en resourcegroep voor uw dashboard worden gepubliceerd om te kiezen.</span><span class="sxs-lookup"><span data-stu-id="beda9-146">You are asked to choose a subscription and resource group for your dashboard to be published to.</span></span> <span data-ttu-id="beda9-147">Als u wilt integreren naadloos dashboards in het ecosysteem, hebben we geïmplementeerd gedeelde dashboards als Azure-resources (zodat u niet delen door een e-mailadres in te voeren).</span><span class="sxs-lookup"><span data-stu-id="beda9-147">To seamlessly integrate dashboards into the ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="beda9-148">Toegang tot de gegevens worden weergegeven door de meeste van de tegels in de portal vallen [Azure Toegangsbeheerrol](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="beda9-148">Access to the information displayed by most of the tiles in the portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="beda9-149">Gedeelde dashboards zijn vanuit een access control-perspectief niet anders als een virtuele machine of een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="beda9-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="beda9-150">Stel dat u hebt een Azure-abonnement en leden van uw team zijn toegewezen de functies van **eigenaar**, **Inzender**, of **lezer** van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="beda9-150">Let's say you have an Azure subscription and members of your team have been assigned the roles of **owner**, **contributor**, or **reader** of the subscription.</span></span>  <span data-ttu-id="beda9-151">Gebruikers die eigenaar of inzenders kunnen weergeven, weergeven, maken, wijzigen of verwijderen van dashboards binnen dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="beda9-151">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="beda9-152">Gebruikers die lezers zijn kunnen lijst en weergave dashboards, maar kunnen niet worden gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="beda9-152">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="beda9-153">Gebruikers met leestoegang hebben, kunnen lokale wijzigingen aanbrengen in een gedeelde dashboard, maar niet kunnen deze wijzigingen publiceren naar de server.</span><span class="sxs-lookup"><span data-stu-id="beda9-153">Users with reader access are able to make local edits to a shared dashboard, but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="beda9-154">Ze kunnen nog wel een persoonlijke kopie van het dashboard voor eigen gebruik.</span><span class="sxs-lookup"><span data-stu-id="beda9-154">However, they can make a private copy of the dashboard for their own use.</span></span>  <span data-ttu-id="beda9-155">Afzonderlijke tegels op het dashboard afdwingen als altijd hun eigen regels voor toegang op basis van de resources die ze met overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="beda9-155">As always, individual tiles on the dashboard enforce their own access control rules based on the resources they correspond to.</span></span>  

<span data-ttu-id="beda9-156">Voor het gemak ervaring handleidingen u naar een patroon waar u dashboards in een resourcegroep plaatsen opgeroepen het publiceren van de portal **dashboards**.</span><span class="sxs-lookup"><span data-stu-id="beda9-156">For convenience, the portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![dashboard publiceren](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="beda9-158">U kunt ook een dashboard publiceren aan een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="beda9-158">You can also choose to publish a dashboard to a particular resource group.</span></span>  <span data-ttu-id="beda9-159">Het toegangsbeheer voor dit dashboard komt overeen met het toegangsbeheer voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="beda9-159">The access control for that dashboard matches the access control for the resource group.</span></span>  <span data-ttu-id="beda9-160">Gebruikers die de resources in die resourcegroep kunnen beheren ook hebben toegang tot de dashboards.</span><span class="sxs-lookup"><span data-stu-id="beda9-160">Users that can manage the resources in that resource group also have access to the dashboards.</span></span>

![dashboard publiceren naar de resourcegroep](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="beda9-162">Nadat uw dashboard is gepubliceerd, de **delen + toegang** besturingselementvenster wordt vernieuwd en ziet u informatie over het gepubliceerde dashboard, inclusief een koppeling voor het beheren van de gebruikerstoegang tot het dashboard.</span><span class="sxs-lookup"><span data-stu-id="beda9-162">After your dashboard is published, the **Sharing + access** control pane will refresh and show you information about the published dashboard, including a link to manage user access to the dashboard.</span></span>  <span data-ttu-id="beda9-163">Deze koppeling opent de standaard rollen gebaseerd toegangsbeheer blade gebruikt voor het beheren van toegang voor een Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="beda9-163">This link launches the standard Role Based Access Control blade used to manage access for any Azure resource.</span></span>  <span data-ttu-id="beda9-164">U kunt altijd teruggaan naar deze weergave selecteert **Share**.</span><span class="sxs-lookup"><span data-stu-id="beda9-164">You can always get back to this view by selecting **Share**.</span></span>

![toegang beheren](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="beda9-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="beda9-166">Next steps</span></span>
* <span data-ttu-id="beda9-167">Zie voor het beheren van resources, [beheren Azure-resources via de portal](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="beda9-167">To manage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="beda9-168">Zie voor het implementeren van resources [implementeren van resources met Resource Manager-sjablonen en Azure-portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="beda9-168">To deploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

