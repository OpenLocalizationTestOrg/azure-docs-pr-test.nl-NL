---
title: aaaManaging Azure-resources met Cloud Explorer | Microsoft Docs
description: Meer informatie over hoe toouse Cloud Explorer toobrowse Azure resources vanuit Visual Studio en beheren.
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
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="620a1-103">Hallo-resources die zijn gekoppeld aan uw Azure-accounts in Visual Studio Cloud Explorer beheren</span><span class="sxs-lookup"><span data-stu-id="620a1-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="620a1-104">Cloud Explorer kunt u tooview uw Azure-resources en resourcegroepen inspecteren van de eigenschappen en acties van diagnostische gegevens vanuit Visual Studio belangrijke ontwikkelaar uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="620a1-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="620a1-105">Zoals Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is gebouwd op Hallo Azure Resource Manager-stack.</span><span class="sxs-lookup"><span data-stu-id="620a1-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="620a1-106">Daarom Cloud Explorer begrijpt resources, zoals Azure-resourcegroepen en Azure-services zoals Logic apps en API apps en ondersteunt de [toegangsbeheer op basis van rollen](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="620a1-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="620a1-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="620a1-107">Prerequisites</span></span>
- <span data-ttu-id="620a1-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) Hello **Azure-workload** geselecteerd, of een eerdere versie van Visual Studio met Hallo [Microsoft Azure SDK voor .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="620a1-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="620a1-109">Microsoft Azure-account: als u geen account hebt, kunt u [aanmelden voor een gratis proefversie](http://go.microsoft.com/fwlink/?LinkId=623901) of [uw voordelen als Visual Studio-abonnee activeren](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="620a1-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="620a1-110">Selecteer tooview Cloud Explorer **weergave** > **Cloud Explorer** op de menubalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="620a1-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="620a1-111">Een Azure-account tooCloud Explorer toevoegen</span><span class="sxs-lookup"><span data-stu-id="620a1-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="620a1-112">tooview hello resources die zijn gekoppeld aan een Azure-account, moet u eerst Hallo account tooCloud Explorer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="620a1-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="620a1-113">In **Cloud Explorer**, selecteer **Azure Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="620a1-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="620a1-115">Selecteer **nieuwe account toevoegt**.</span><span class="sxs-lookup"><span data-stu-id="620a1-115">Select **Add new account**.</span></span> 

    ![Koppeling voor cloud Explorer account toevoegen](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="620a1-117">Meld u bij de Azure-account waarvan u de gewenste bronnen toohello toobrowse.</span><span class="sxs-lookup"><span data-stu-id="620a1-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="620a1-118">Zodra tooan Azure-account aangemeld, wordt Hallo-abonnementen die zijn gekoppeld aan dit account weergegeven.</span><span class="sxs-lookup"><span data-stu-id="620a1-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="620a1-119">Selecteer de selectievakjes voor abonnementen van Hallo account u wilt toobrowse en selecteer vervolgens Hallo **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="620a1-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: Selecteer een Azure-abonnementen toodisplay](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="620a1-121">Na het selecteren van Hallo abonnementen waarvan u de gewenste bronnen weergegeven toobrowse, deze abonnementen en bronnen in Hallo Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="620a1-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Cloud Explorer resource weergeven voor een Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="620a1-123">Een Azure-account verwijderen uit Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="620a1-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="620a1-124">In **Cloud Explorer**, selecteer **Azure Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="620a1-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="620a1-126">Selecteer volgende toohello account u wilt dat tooremove, **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="620a1-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Pictogram instellingen cloud Explorer Azure-account](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="620a1-128">Brontypen of resourcegroepen weergeven</span><span class="sxs-lookup"><span data-stu-id="620a1-128">View resource types or resource groups</span></span>
<span data-ttu-id="620a1-129">tooview uw Azure-resources kunt u ofwel **brontypen** of **resourcegroepen** weergeven.</span><span class="sxs-lookup"><span data-stu-id="620a1-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="620a1-130">In **Cloud Explorer**, selecteer Hallo resource vervolgkeuzelijsten.</span><span class="sxs-lookup"><span data-stu-id="620a1-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Cloud Explorer dropdown tooselect Hallo gewenste bronnen lijstweergave](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="620a1-132">Selecteer in het contextmenu hello, Hallo gewenst weergave:</span><span class="sxs-lookup"><span data-stu-id="620a1-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="620a1-133">**Brontypen** weergave - Hallo algemene gebruikt op Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), ziet u uw Azure-resources ingedeeld volgens hun type, zoals web-apps, storage-accounts en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="620a1-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="620a1-134">**Resourcegroepen** view - categoriseert Azure-bronnen door hello Azure-resourcegroep waaraan ze gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="620a1-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="620a1-135">Een resourcegroep is een bundel van Azure-resources, meestal worden gebruikt door een specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="620a1-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="620a1-136">Zie toolearn meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="620a1-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="620a1-137">Hallo volgende afbeelding toont een vergelijking van Hallo twee resourceweergaven:</span><span class="sxs-lookup"><span data-stu-id="620a1-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Cloud Explorer resource weergaven vergelijking](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="620a1-139">Weergeven en bronnen in de Cloud Explorer navigeert</span><span class="sxs-lookup"><span data-stu-id="620a1-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="620a1-140">toonavigate tooan Azure-resource en de informatie in de Cloud Explorer bekijken, vouwt u het type of de bijbehorende brongroep Hallo-item en selecteer vervolgens Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="620a1-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="620a1-141">Wanneer u een resource selecteert, informatie wordt weergegeven in tabbladen Hallo twee - **acties** en **eigenschappen** - Hallo onderaan Cloud Explorer in.</span><span class="sxs-lookup"><span data-stu-id="620a1-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="620a1-142">**Acties** tabblad - lijsten Hallo acties u kunt uitvoeren in de Cloud Explorer voor de resource Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="620a1-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="620a1-143">U kunt ook weergeven deze opties met de rechtermuisknop op Hallo resource tooview het contextmenu.</span><span class="sxs-lookup"><span data-stu-id="620a1-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="620a1-144">**Eigenschappen** tabblad - toont Hallo eigenschappen van Hallo resource, zoals de type Landinstellingen en resource-groep waaraan deze gekoppeld is.</span><span class="sxs-lookup"><span data-stu-id="620a1-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="620a1-145">Hallo toont volgende afbeelding een voorbeeld van de vergelijking van wat u op elk tabblad voor een App Service ziet:</span><span class="sxs-lookup"><span data-stu-id="620a1-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="620a1-146">Elke resource heeft Hallo actie **openen in de portal**.</span><span class="sxs-lookup"><span data-stu-id="620a1-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="620a1-147">Als u deze actie kiest, Cloud Explorer Hallo geselecteerd resource weergegeven in Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="620a1-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="620a1-148">Hallo **openen in de portal** functie is handig voor toodeeply genest resources navigeren.</span><span class="sxs-lookup"><span data-stu-id="620a1-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="620a1-149">Aanvullende acties en eigenschapswaarden mogelijk ook weergegeven op basis van hello Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="620a1-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="620a1-150">Web-apps en logic apps ook bijvoorbeeld Hallo acties **openen in browser** en **foutopsporingsprogramma koppelen** bovendien te**openen in de portal**.</span><span class="sxs-lookup"><span data-stu-id="620a1-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="620a1-151">Acties tooopen editors worden weergegeven wanneer u een account-opslag-blob, wachtrij of tabel.</span><span class="sxs-lookup"><span data-stu-id="620a1-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="620a1-152">Apps van Azure hebben **URL** en **Status** eigenschappen, terwijl de opslagbronnen eigenschappen van sleutel en verbinding-tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="620a1-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="620a1-153">Resources zoeken in de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="620a1-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="620a1-154">toolocate resources met een specifieke naam in uw Azure-account-abonnementen, voer de naam van de Hallo in Hallo **Search** vak in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="620a1-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Resources zoeken in de Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="620a1-156">Als u tekens in Hallo **Search** vak alleen bronnen die overeenkomen met die tekens worden weergegeven in Hallo resourcestructuur.</span><span class="sxs-lookup"><span data-stu-id="620a1-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
