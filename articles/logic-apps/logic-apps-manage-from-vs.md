---
title: aaaManage logische apps in Visual Studio - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="b27f8-103">Beheren van uw logische apps met Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="b27f8-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="b27f8-104">Hoewel hello [Azure-portal](https://portal.azure.com/) een uitstekende manier biedt u toodesign en Azure Logic Apps beheren, kunt u Visual Studio Cloud Explorer voor het beheren van veel Azure activa, met inbegrip van logische apps.</span><span class="sxs-lookup"><span data-stu-id="b27f8-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="b27f8-105">Visual Studio Cloud Explorer kunt u bladeren, beheren, bewerken en download gepubliceerde logic apps.</span><span class="sxs-lookup"><span data-stu-id="b27f8-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="b27f8-106">Beheertaken omvatten inschakelen, uitschakelen en historie weergeven die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b27f8-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="b27f8-107">Voordat u kunt toegang tot en beheren van uw logische apps in Visual Studio, installeren en configureren van deze Visual Studio-hulpprogramma's voor Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b27f8-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b27f8-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b27f8-108">Prerequisites</span></span>

* [<span data-ttu-id="b27f8-109">Visual Studio 2015 of Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b27f8-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="b27f8-110">[Nieuwste Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 of hoger)</span><span class="sxs-lookup"><span data-stu-id="b27f8-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="b27f8-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="b27f8-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="b27f8-112">De website toohello toegang wanneer u de ontwerpfunctie Hallo</span><span class="sxs-lookup"><span data-stu-id="b27f8-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="b27f8-113">Installeer Visual Studio-hulpprogramma's voor Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b27f8-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="b27f8-114">Nadat u Hallo vereisten hebt geïnstalleerd, downloaden en installeren van hello Azure Logic Apps-Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b27f8-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="b27f8-115">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b27f8-115">Open Visual Studio.</span></span> <span data-ttu-id="b27f8-116">Op Hallo **extra** selecteert u **uitbreidingen en Updates**.</span><span class="sxs-lookup"><span data-stu-id="b27f8-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="b27f8-117">Vouw Hallo **Online** categorie zodat u online in Hallo Visual Studio-galerie zoeken kunt.</span><span class="sxs-lookup"><span data-stu-id="b27f8-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="b27f8-118">Blader of zoek naar **Logic Apps** totdat u **Azure Logic Apps-Tools voor Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b27f8-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="b27f8-119">toodownload en installatie Hallo-extensie, klikt u op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="b27f8-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="b27f8-120">Visual Studio starten na de installatie.</span><span class="sxs-lookup"><span data-stu-id="b27f8-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="b27f8-121">toodownload hello Azure Logic Apps-Tools voor Visual Studio gaat u rechtstreeks toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="b27f8-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="b27f8-122">Bladeren naar logische apps in de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="b27f8-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="b27f8-123">tooopen Cloud Explorer op Hallo **weergave** menu kiezen **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b27f8-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="b27f8-124">Blader naar uw logische app, resourcegroep of brontype.</span><span class="sxs-lookup"><span data-stu-id="b27f8-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="b27f8-125">Als u bladert per resourcetype, selecteert u uw Azure-abonnement, vouw Hallo **Logic Apps** uit en selecteer uw logische app.</span><span class="sxs-lookup"><span data-stu-id="b27f8-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="b27f8-126">Als u door de resourcegroep bladeren, vouwt u de resourcegroep Hallo met uw logische app en selecteer uw logische app.</span><span class="sxs-lookup"><span data-stu-id="b27f8-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="b27f8-127">tooview opdrachten voor uw logische app, met de rechtermuisknop op uw logische app of aan de onderkant van de Hallo van Cloud Explorer, kiezen uit Hallo **acties** menu.</span><span class="sxs-lookup"><span data-stu-id="b27f8-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![Blader naar uw logische app](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="b27f8-129">Uw logische app met Logic Apps Designer bewerken</span><span class="sxs-lookup"><span data-stu-id="b27f8-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="b27f8-130">Vanuit de Cloud Explorer kunt u een momenteel geïmplementeerde logische app openen in Hallo dezelfde designer die u in hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b27f8-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="b27f8-131">tooedit uw logische app, in de Cloud Explorer met de rechtermuisknop op uw logische app en selecteer **geopend met Logic App Editor**.</span><span class="sxs-lookup"><span data-stu-id="b27f8-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="b27f8-132">toopublish uw toohello updates cloud, kies **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="b27f8-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="b27f8-133">Kies een nieuw run toostart **uitvoeren Trigger**.</span><span class="sxs-lookup"><span data-stu-id="b27f8-133">toostart a new run, choose **Run Trigger**.</span></span>

![Logic Apps Designer](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="b27f8-135">Vanuit Hallo designer kunt u ook **downloaden** een logische app.</span><span class="sxs-lookup"><span data-stu-id="b27f8-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="b27f8-136">Deze actie automatisch parameterizes Hallo logic app definitie en Hallo definitie opgeslagen als een Azure Resource Manager-implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="b27f8-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="b27f8-137">U kunt deze implementatie tooyour Azure-resourcegroep sjabloonproject toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b27f8-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="b27f8-138">Uw logische app uitvoeringsgeschiedenis bladeren</span><span class="sxs-lookup"><span data-stu-id="b27f8-138">Browse your logic app run history</span></span>

<span data-ttu-id="b27f8-139">tooview hello geschiedenis voor uw logische app uitvoeren met de rechtermuisknop op uw logische app en selecteer **Open uitvoeringsgeschiedenis**.</span><span class="sxs-lookup"><span data-stu-id="b27f8-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="b27f8-140">tooreorder uw uitvoeringsgeschiedenis op basis van een Hallo eigenschappen weergegeven, selecteer Hallo kolomkop te klikken.</span><span class="sxs-lookup"><span data-stu-id="b27f8-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![geschiedenis uitvoeren](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="b27f8-142">tooshow Hallo geschiedenis voor een instantie uitvoeren zodat u resultaten, inclusief Hallo invoer en uitvoer van elke stap uitgevoerd Hallo kunt bekijken: Dubbelklik op een van de Hallo exemplaren uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b27f8-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![Uitvoeringsgeschiedenis resultaten, invoer en uitvoer van de stappen](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="b27f8-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b27f8-144">Next steps</span></span>

* [<span data-ttu-id="b27f8-145">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="b27f8-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="b27f8-146">Ontwerpen, bouwen en implementeren van logische apps in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b27f8-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="b27f8-147">Algemene voorbeelden en scenario's weergeven</span><span class="sxs-lookup"><span data-stu-id="b27f8-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="b27f8-148">Video: Automatiseren van bedrijfsprocessen met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b27f8-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="b27f8-149">Video: Uw systemen integreren met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b27f8-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
