---
title: Logische apps in Visual Studio - Azure Logic Apps beheren | Microsoft Docs
description: Logische apps en andere Azure activa met Visual Studio Cloud Explorer beheren
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: a5bf24de1a7a2b6d4c1ae6416c95d83ef7506da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="bda7b-103">Beheren van uw logische apps met Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="bda7b-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="bda7b-104">Hoewel de [Azure-portal](https://portal.azure.com/) biedt een goede manier om te ontwerpen en beheren van Azure Logic Apps, kunt u Visual Studio Cloud Explorer voor het beheren van veel Azure activa, met inbegrip van logische apps.</span><span class="sxs-lookup"><span data-stu-id="bda7b-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="bda7b-105">Visual Studio Cloud Explorer kunt u bladeren, beheren, bewerken en download gepubliceerde logic apps.</span><span class="sxs-lookup"><span data-stu-id="bda7b-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="bda7b-106">Beheertaken omvatten inschakelen, uitschakelen en historie weergeven die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bda7b-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="bda7b-107">Voordat u kunt toegang tot en beheren van uw logische apps in Visual Studio, installeren en configureren van deze Visual Studio-hulpprogramma's voor Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="bda7b-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bda7b-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bda7b-108">Prerequisites</span></span>

* [<span data-ttu-id="bda7b-109">Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bda7b-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="bda7b-110">[Nieuwste Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 of hoger)</span><span class="sxs-lookup"><span data-stu-id="bda7b-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="bda7b-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="bda7b-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="bda7b-112">Toegang tot het Internet wanneer u de ontwerpfunctie</span><span class="sxs-lookup"><span data-stu-id="bda7b-112">Access to the web when using the embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="bda7b-113">Installeer Visual Studio-hulpprogramma's voor Logic Apps</span><span class="sxs-lookup"><span data-stu-id="bda7b-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="bda7b-114">Nadat u de vereiste onderdelen hebt geïnstalleerd, downloaden en installeren van de Azure Logic Apps-Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bda7b-114">After you install the prerequisites, download and install the Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="bda7b-115">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bda7b-115">Open Visual Studio.</span></span> <span data-ttu-id="bda7b-116">Op de **extra** selecteert u **uitbreidingen en Updates**.</span><span class="sxs-lookup"><span data-stu-id="bda7b-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="bda7b-117">Vouw de **Online** categorie zodat u online in de Visual Studio-galerie zoeken kunt.</span><span class="sxs-lookup"><span data-stu-id="bda7b-117">Expand the **Online** category so you can search online in the Visual Studio Gallery.</span></span>
3. <span data-ttu-id="bda7b-118">Blader of zoek naar **Logic Apps** totdat u **Azure Logic Apps-Tools voor Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bda7b-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="bda7b-119">Als u wilt downloaden en installeren van de extensie, klikt u op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="bda7b-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="bda7b-120">Visual Studio starten na de installatie.</span><span class="sxs-lookup"><span data-stu-id="bda7b-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="bda7b-121">Ga naar de Azure Logic Apps-hulpprogramma's voor Visual Studio rechtstreeks downloaden, de [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="bda7b-121">To download the Azure Logic Apps Tools for Visual Studio directly, go to the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="bda7b-122">Bladeren naar logische apps in de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="bda7b-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="bda7b-123">Cloud Explorer openen op de **weergave** menu kiezen **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bda7b-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="bda7b-124">Blader naar uw logische app, resourcegroep of brontype.</span><span class="sxs-lookup"><span data-stu-id="bda7b-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="bda7b-125">Als u bladert per resourcetype, selecteert u uw Azure-abonnement, vouw de **Logic Apps** uit en selecteer uw logische app.</span><span class="sxs-lookup"><span data-stu-id="bda7b-125">If you browse by resource type, select your Azure subscription, expand the **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="bda7b-126">Als u door de resourcegroep bladeren, vouwt u de resourcegroep met uw logische app en selecteer uw logische app.</span><span class="sxs-lookup"><span data-stu-id="bda7b-126">If you browse by resource group, expand the resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="bda7b-127">Als opdrachten wilt weergeven voor uw logische app, met de rechtermuisknop op uw logische app of aan de onderkant van de Cloud Explorer kiezen uit de **acties** menu.</span><span class="sxs-lookup"><span data-stu-id="bda7b-127">To view commands for your logic app, either right-click your logic app, or at the bottom of Cloud Explorer, choose from the **Actions** menu.</span></span>

    ![Blader naar uw logische app](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="bda7b-129">Uw logische app met Logic Apps Designer bewerken</span><span class="sxs-lookup"><span data-stu-id="bda7b-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="bda7b-130">Vanuit de Cloud Explorer kunt u een momenteel geïmplementeerde logische app openen in de ontwerpfunctie voor dezelfde die u in de Azure portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bda7b-130">From Cloud Explorer, you can open a currently deployed logic app in the same designer that you use in the Azure portal.</span></span> 

* <span data-ttu-id="bda7b-131">Als u wilt bewerken van uw logische app, in de Cloud Explorer met de rechtermuisknop op uw logische app en selecteer **geopend met Logic App Editor**.</span><span class="sxs-lookup"><span data-stu-id="bda7b-131">To edit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="bda7b-132">Als u wilt de updates publiceren naar de cloud, kies **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="bda7b-132">To publish your updates to the cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="bda7b-133">Kies voor het starten van een nieuw run **uitvoeren Trigger**.</span><span class="sxs-lookup"><span data-stu-id="bda7b-133">To start a new run, choose **Run Trigger**.</span></span>

![Logic Apps Designer](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="bda7b-135">In de ontwerpfunctie, kunt u ook **downloaden** een logische app.</span><span class="sxs-lookup"><span data-stu-id="bda7b-135">From the designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="bda7b-136">Deze actie automatisch parameterizes de definitie van logic Apps en de definitie van de opgeslagen als een Azure Resource Manager-implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="bda7b-136">This action automatically parameterizes the logic app definition, and saves the definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="bda7b-137">U kunt deze sjabloon voor de implementatie toevoegen aan uw project Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="bda7b-137">You can add this deployment template to your Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="bda7b-138">Uw logische app uitvoeringsgeschiedenis bladeren</span><span class="sxs-lookup"><span data-stu-id="bda7b-138">Browse your logic app run history</span></span>

<span data-ttu-id="bda7b-139">Als u wilt weergeven van de uitvoeringsgeschiedenis voor uw logische app, met de rechtermuisknop op uw logische app en selecteer **Open uitvoeringsgeschiedenis**.</span><span class="sxs-lookup"><span data-stu-id="bda7b-139">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="bda7b-140">Selecteer de kolomkop om de volgorde van de uitvoeringsgeschiedenis op basis van een van de eigenschappen die worden weergegeven, te.</span><span class="sxs-lookup"><span data-stu-id="bda7b-140">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![geschiedenis uitvoeren](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="bda7b-142">Dubbelklik op een van de exemplaren uitvoeren om weer te geven van de uitvoeringsgeschiedenis voor een exemplaar, zodat u de uitgevoerde resultaten, inclusief de invoer en uitvoer van elke stap kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="bda7b-142">To show the run history for an instance so you can review the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![Uitvoeringsgeschiedenis resultaten, invoer en uitvoer van de stappen](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="bda7b-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bda7b-144">Next steps</span></span>

* [<span data-ttu-id="bda7b-145">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="bda7b-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="bda7b-146">Ontwerpen, bouwen en implementeren van logische apps in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bda7b-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="bda7b-147">Algemene voorbeelden en scenario's weergeven</span><span class="sxs-lookup"><span data-stu-id="bda7b-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="bda7b-148">Video: Automatiseren van bedrijfsprocessen met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="bda7b-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="bda7b-149">Video: Uw systemen integreren met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="bda7b-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
