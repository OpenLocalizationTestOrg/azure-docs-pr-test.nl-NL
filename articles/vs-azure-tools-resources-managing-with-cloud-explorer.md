---
title: Het beheren van Azure-resources met Cloud Explorer | Microsoft Docs
description: Informatie over het gebruik van Cloud Explorer om te zoeken en beheren van Azure-resources in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 6e6d8d559f0251b71bfa6d529ead82a246cb3235
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="60066-103">De bronnen die zijn gekoppeld aan uw Azure-accounts in Visual Studio Cloud Explorer beheren</span><span class="sxs-lookup"><span data-stu-id="60066-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="60066-104">Cloud Explorer kunt u uw Azure-resources en resourcegroepen bekijken, controleren van de eigenschappen en belangrijke ontwikkelaar diagnostics acties uitvoeren vanuit in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60066-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="60066-105">Als de [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is gebaseerd op de Azure Resource Manager-stack.</span><span class="sxs-lookup"><span data-stu-id="60066-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span></span> <span data-ttu-id="60066-106">Daarom Cloud Explorer begrijpt resources, zoals Azure-resourcegroepen en Azure-services zoals Logic apps en API apps en ondersteunt de [toegangsbeheer op basis van rollen](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="60066-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="60066-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="60066-107">Prerequisites</span></span>
- <span data-ttu-id="60066-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) met de **Azure-workload** geselecteerd, of een eerdere versie van Visual Studio met de [Microsoft Azure SDK voor .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="60066-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="60066-109">Microsoft Azure-account: als u geen account hebt, kunt u [aanmelden voor een gratis proefversie](http://go.microsoft.com/fwlink/?LinkId=623901) of [uw voordelen als Visual Studio-abonnee activeren](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="60066-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="60066-110">Als u wilt weergeven Cloud Explorer, selecteer **weergave** > **Cloud Explorer** op de menubalk.</span><span class="sxs-lookup"><span data-stu-id="60066-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-to-cloud-explorer"></a><span data-ttu-id="60066-111">Toevoegen van een Azure account toe aan de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="60066-111">Add an Azure account to Cloud Explorer</span></span>
<span data-ttu-id="60066-112">Als u wilt weergeven van de resources die zijn gekoppeld aan een Azure-account, moet u eerst de account toevoegen aan Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="60066-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span></span> 

1. <span data-ttu-id="60066-113">In **Cloud Explorer**, selecteer **Azure Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="60066-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="60066-115">Selecteer **nieuwe account toevoegt**.</span><span class="sxs-lookup"><span data-stu-id="60066-115">Select **Add new account**.</span></span> 

    ![Koppeling voor cloud Explorer account toevoegen](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="60066-117">Meld u aan bij de Azure-account waarvan bronnen die u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="60066-117">Log in to the Azure account whose resources you want to browse.</span></span> 

1. <span data-ttu-id="60066-118">Zodra u aangemeld bij een Azure-account, wordt de abonnementen die zijn gekoppeld aan dit account weergegeven.</span><span class="sxs-lookup"><span data-stu-id="60066-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span></span> <span data-ttu-id="60066-119">Schakel de selectievakjes voor de account-abonnementen die u wilt bladeren en selecteer vervolgens **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="60066-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: Selecteer een Azure-abonnementen om weer te geven](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="60066-121">Na het selecteren van de abonnementen waarvan u wilt bladeren bronnen weergegeven die abonnementen en bronnen in de Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="60066-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span></span>

    ![Cloud Explorer resource weergeven voor een Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="60066-123">Een Azure-account verwijderen uit Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="60066-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="60066-124">In **Cloud Explorer**, selecteer **Azure Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="60066-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="60066-126">Naast het account dat u wilt verwijderen, selecteert u **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="60066-126">Next to the account you want to remove, select **Remove**.</span></span>

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="60066-128">Brontypen of resourcegroepen weergeven</span><span class="sxs-lookup"><span data-stu-id="60066-128">View resource types or resource groups</span></span>
<span data-ttu-id="60066-129">Als u wilt weergeven van uw Azure-resources, kunt u ofwel **brontypen** of **resourcegroepen** weergeven.</span><span class="sxs-lookup"><span data-stu-id="60066-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="60066-130">In **Cloud Explorer**, selecteert u de vervolgkeuzelijsten resource.</span><span class="sxs-lookup"><span data-stu-id="60066-130">In **Cloud Explorer**, select the resource view dropdown.</span></span>

    ![Cloud Explorer de vervolgkeuzelijst de gewenste bronnen weergave selecteren](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="60066-132">Selecteer de gewenste weergave in het contextmenu:</span><span class="sxs-lookup"><span data-stu-id="60066-132">From the context menu, select the desired view:</span></span> 

    - <span data-ttu-id="60066-133">**Brontypen** view - de algemene weergave gebruikt op de [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), ziet u uw Azure-resources ingedeeld volgens hun type, zoals web-apps, storage-accounts en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="60066-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="60066-134">**Resourcegroepen** view - categoriseert Azure-bronnen door de Azure-resourcegroep waaraan ze gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="60066-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span></span> <span data-ttu-id="60066-135">Een resourcegroep is een bundel van Azure-resources, meestal worden gebruikt door een specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="60066-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="60066-136">Zie voor meer informatie over Azure-resourcegroepen, [overzicht van Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60066-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="60066-137">De volgende afbeelding toont een vergelijking van de twee weergaven:</span><span class="sxs-lookup"><span data-stu-id="60066-137">The following image shows a comparison of the two resource views:</span></span>

    ![Cloud Explorer resource weergaven vergelijking](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="60066-139">Weergeven en bronnen in de Cloud Explorer navigeert</span><span class="sxs-lookup"><span data-stu-id="60066-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="60066-140">Om te navigeren naar een Azure-resource en de informatie in de Cloud Explorer bekijken, vouwt u het type of de bijbehorende brongroep van het item en selecteer vervolgens de resource.</span><span class="sxs-lookup"><span data-stu-id="60066-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span></span> <span data-ttu-id="60066-141">Wanneer u een resource selecteert, wordt informatie weergegeven in de twee tabbladen - **acties** en **eigenschappen** - aan de onderkant van de Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="60066-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="60066-142">**Acties** tabblad - vindt u de acties die u kunt nu in de Cloud Explorer voor de geselecteerde bron.</span><span class="sxs-lookup"><span data-stu-id="60066-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span></span> <span data-ttu-id="60066-143">U kunt ook deze opties weergeven met de rechtermuisknop op de bron om de contextmenu weer te geven.</span><span class="sxs-lookup"><span data-stu-id="60066-143">You can also view these options by right-clicking the resource to view its context menu.</span></span>

- <span data-ttu-id="60066-144">**Eigenschappen** tabblad - geeft de eigenschappen van de resource, zoals de type Landinstellingen en resource-groep waaraan deze gekoppeld is.</span><span class="sxs-lookup"><span data-stu-id="60066-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="60066-145">De volgende afbeelding toont een voorbeeld van de vergelijking van wat u op elk tabblad voor een App Service ziet:</span><span class="sxs-lookup"><span data-stu-id="60066-145">The following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="60066-146">Elke resource heeft de actie **openen in de portal**.</span><span class="sxs-lookup"><span data-stu-id="60066-146">Every resource has the action **Open in portal**.</span></span> <span data-ttu-id="60066-147">Als u deze actie kiest, Cloud Explorer worden weergegeven voor de geselecteerde resource in de [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="60066-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="60066-148">De **openen in de portal** functie is handig voor het navigeren naar diep geneste resources.</span><span class="sxs-lookup"><span data-stu-id="60066-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span></span>

<span data-ttu-id="60066-149">Aanvullende acties en eigenschapswaarden mogelijk ook weergegeven op basis van de Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="60066-149">Additional actions and property values may also appear based on the Azure resource.</span></span> <span data-ttu-id="60066-150">Bijvoorbeeld, web-apps en logic apps hebben de acties **openen in browser** en **foutopsporingsprogramma koppelen** naast **openen in de portal**.</span><span class="sxs-lookup"><span data-stu-id="60066-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span></span> <span data-ttu-id="60066-151">Bewerkingen voor het openen van editors worden weergegeven wanneer u een account-opslag-blob, wachtrij of tabel.</span><span class="sxs-lookup"><span data-stu-id="60066-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="60066-152">Apps van Azure hebben **URL** en **Status** eigenschappen, terwijl de opslagbronnen eigenschappen van sleutel en verbinding-tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="60066-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="60066-153">Resources zoeken in de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="60066-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="60066-154">Voer de naam in om te zoeken resources met een specifieke naam in de abonnementen voor uw Azure-account, de **Search** vak in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="60066-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span></span>

![Resources zoeken in de Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="60066-156">Als u tekens in de **Search** vak alleen bronnen die overeenkomen met die tekens worden weergegeven in de resourcestructuur.</span><span class="sxs-lookup"><span data-stu-id="60066-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span></span>
