---
title: Maken, bouwen en implementeren van logische apps in Visual Studio - Azure Logic Apps | Microsoft Docs
description: Visual Studio-projecten maken zodat u kunt ontwerpen, bouwen en implementeren van Azure Logic Apps.
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: e7f5cf483d22e4c60dedbe5176ceb0bc8b2b6e66
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="1e956-103">Ontwerpen, bouwen en implementeren van Azure Logic Apps in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e956-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="1e956-104">Hoewel de [Azure-portal](https://portal.azure.com/) biedt een goede manier om te maken en beheren van Azure Logic Apps, u kunt Visual Studio gebruiken voor het ontwerpen, bouwen en implementeren van uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="1e956-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to create and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="1e956-105">Visual Studio biedt uitgebreide hulpmiddelen zoals de Logic App-ontwerper voor u logic apps maken, implementatie en automatisering sjablonen configureren en implementeren met elke omgeving.</span><span class="sxs-lookup"><span data-stu-id="1e956-105">Visual Studio provides rich tools like the Logic App Designer for you to create logic apps, configure deployment and automation templates, and deploy to any environment.</span></span> 

<span data-ttu-id="1e956-106">Aan de slag met Azure Logic Apps meer [uw eerste logische app maken in de Azure-portal](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1e956-106">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="1e956-107">Installatiestappen</span><span class="sxs-lookup"><span data-stu-id="1e956-107">Installation steps</span></span>

<span data-ttu-id="1e956-108">Als u wilt installeren en configureren van Visual Studio-hulpprogramma's voor Azure Logic Apps, de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="1e956-108">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1e956-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1e956-109">Prerequisites</span></span>

* <span data-ttu-id="1e956-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) of Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="1e956-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="1e956-111">[Nieuwste Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 of hoger)</span><span class="sxs-lookup"><span data-stu-id="1e956-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="1e956-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e956-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="1e956-113">Toegang tot het Internet wanneer u de ontwerpfunctie</span><span class="sxs-lookup"><span data-stu-id="1e956-113">Access to the web when using the embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="1e956-114">Installeer Visual Studio-hulpprogramma's voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1e956-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="1e956-115">Nadat u de vereisten:</span><span class="sxs-lookup"><span data-stu-id="1e956-115">After you install the prerequisites:</span></span>

1. <span data-ttu-id="1e956-116">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e956-116">Open Visual Studio.</span></span> <span data-ttu-id="1e956-117">Op de **extra** selecteert u **uitbreidingen en Updates**.</span><span class="sxs-lookup"><span data-stu-id="1e956-117">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="1e956-118">Vouw de **Online** categorie zodat u kunt online zoeken.</span><span class="sxs-lookup"><span data-stu-id="1e956-118">Expand the **Online** category so you can search online.</span></span>
3. <span data-ttu-id="1e956-119">Blader of zoek naar **Logic Apps** totdat u **Azure Logic Apps-Tools voor Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="1e956-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="1e956-120">Als u wilt downloaden en installeren van de extensie, klikt u op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="1e956-120">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="1e956-121">Visual Studio starten na de installatie.</span><span class="sxs-lookup"><span data-stu-id="1e956-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="1e956-122">U kunt ook downloaden [Azure Logic Apps-Tools voor Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) en de [Azure Logic Apps-Tools voor Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) rechtstreeks vanuit Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1e956-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and the [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from the Visual Studio Marketplace.</span></span>

<span data-ttu-id="1e956-123">Nadat u de installatie hebt voltooid, kunt u de Azure-resourcegroepproject met Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="1e956-123">After you finish installation, you can use the Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="1e956-124">Uw project maken</span><span class="sxs-lookup"><span data-stu-id="1e956-124">Create your project</span></span>

1. <span data-ttu-id="1e956-125">Op de **bestand** menu, gaat u naar **nieuw**, en selecteer **Project**.</span><span class="sxs-lookup"><span data-stu-id="1e956-125">On the **File** menu, go to **New**, and select **Project**.</span></span> <span data-ttu-id="1e956-126">Of als uw project toevoegen aan een bestaande oplossing, gaat u naar **toevoegen**, en selecteer **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="1e956-126">Or to add your project to an existing solution, go to **Add**, and select **New Project**.</span></span>

    ![Menu Bestand](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="1e956-128">In de **nieuw Project** venster vinden **Cloud**, en selecteer **Azure-resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="1e956-128">In the **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="1e956-129">Naam van uw project en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e956-129">Name your project, and click **OK**.</span></span>

    ![Nieuw project toevoegen](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="1e956-131">Selecteer de **logische App** sjabloon die u maakt een lege logic app-implementatiesjabloon moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1e956-131">Select the **Logic App** template, which creates a blank logic app deployment template for you to use.</span></span> <span data-ttu-id="1e956-132">Nadat u de sjabloon hebt geselecteerd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e956-132">After you select your template, click **OK**.</span></span>

    ![Selecteer de sjabloon voor logische Apps](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="1e956-134">U hebt nu uw app-project logica toegevoegd aan uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="1e956-134">You've now added your logic app project to your solution.</span></span> 
    <span data-ttu-id="1e956-135">Uw implementatiebestand moet in Solution Explorer, worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1e956-135">In the Solution Explorer, your deployment file should appear.</span></span>

    ![Implementatiebestand](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="1e956-137">Uw logische app maken met Logic App-ontwerper</span><span class="sxs-lookup"><span data-stu-id="1e956-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="1e956-138">Wanneer u een Azure-resourcegroepproject met een logische app hebt, kunt u de ontwerpfunctie voor Logic App openen in Visual Studio om uw werkstroom te maken.</span><span class="sxs-lookup"><span data-stu-id="1e956-138">When you have an Azure Resource Group project that contains a logic app, you can open the Logic App Designer in Visual Studio to create your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="1e956-139">De ontwerpfunctie vereist een internetverbinding beschikken om de query-connectors voor de beschikbare eigenschappen en -gegevens.</span><span class="sxs-lookup"><span data-stu-id="1e956-139">The designer requires an internet connection to query connectors for available properties and data.</span></span> <span data-ttu-id="1e956-140">Als u de Dynamics CRM Online-connector gebruikt, vraagt de ontwerpfunctie voor uw CRM-exemplaar om weer te geven van de beschikbare aangepaste en de standaardeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="1e956-140">For example, if you use the Dynamics CRM Online connector, the designer queries your CRM instance to show available custom and default properties.</span></span>

1. <span data-ttu-id="1e956-141">Met de rechtermuisknop op uw `<template>.json` bestand en selecteer **openen met Logic App-ontwerper**.</span><span class="sxs-lookup"><span data-stu-id="1e956-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="1e956-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="1e956-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="1e956-143">Kies uw Azure-abonnement, resourcegroep en locatie voor de implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="1e956-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e956-144">Het ontwerpen van een logische app, maakt resources van de API-verbinding die query voor eigenschappen tijdens de ontwerp.</span><span class="sxs-lookup"><span data-stu-id="1e956-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="1e956-145">Visual Studio gebruikt de geselecteerde resourcegroep voor deze verbindingen maken tijdens de ontwerpfase.</span><span class="sxs-lookup"><span data-stu-id="1e956-145">Visual Studio uses your selected resource group to create those connections during design time.</span></span> <span data-ttu-id="1e956-146">Als u wilt weergeven of wijzigen van de API-verbindingen, gaat u naar de Azure-portal en bladert u naar **API verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="1e956-146">To view or change any API Connections, go to the Azure portal, and browse for **API Connections**.</span></span>

    ![Abonnement kiezen](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="1e956-148">De ontwerpfunctie maakt gebruik van de definitie van de `<template>.json` -bestand voor rendering.</span><span class="sxs-lookup"><span data-stu-id="1e956-148">The designer uses the definition in the `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="1e956-149">Maken en ontwerpen van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="1e956-149">Create and design your logic app.</span></span> <span data-ttu-id="1e956-150">Uw implementatiesjabloon is bijgewerkt met de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1e956-150">Your deployment template is updated with your changes.</span></span>

    ![App-ontwerper logica in Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="1e956-152">Visual Studio voegt `Microsoft.Web/connections` bronnen zijn voor uw bronbestand voor de verbindingen uw logische app vereist is voor werking.</span><span class="sxs-lookup"><span data-stu-id="1e956-152">Visual Studio adds `Microsoft.Web/connections` resources to your resource file for any connections your logic app needs to function.</span></span> <span data-ttu-id="1e956-153">De eigenschappen van deze verbinding kunnen worden ingesteld bij het implementeren van, en nadat u hebt geïmplementeerd beheerd **API verbindingen** in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e956-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in the Azure portal.</span></span>

### <a name="switch-to-json-code-view"></a><span data-ttu-id="1e956-154">Overschakelen naar de codeweergave JSON</span><span class="sxs-lookup"><span data-stu-id="1e956-154">Switch to JSON code view</span></span>

<span data-ttu-id="1e956-155">Als u wilt weergeven in de JSON-weergave voor uw logische app, selecteer de **codeweergave** tabblad aan de onderkant van de ontwerpfunctie.</span><span class="sxs-lookup"><span data-stu-id="1e956-155">To show the JSON representation for your logic app, select the **Code View** tab at the bottom of the designer.</span></span>

<span data-ttu-id="1e956-156">Als u wilt overschakelen naar de volledige resource JSON, met de rechtermuisknop op de `<template>.json` bestand en selecteer **Open**.</span><span class="sxs-lookup"><span data-stu-id="1e956-156">To switch back to the full resource JSON, right-click the `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-to-visual-studio-deployment-templates"></a><span data-ttu-id="1e956-157">Verwijzingen voor afhankelijke resources toevoegen aan Visual Studio-implementatiesjablonen</span><span class="sxs-lookup"><span data-stu-id="1e956-157">Add references for dependent resources to Visual Studio deployment templates</span></span>

<span data-ttu-id="1e956-158">Als u wilt dat uw logische app om te verwijzen naar afhankelijke resources, kunt u [Azure Resource Manager-sjabloonfuncties](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in uw sjabloon logic app-implementatie.</span><span class="sxs-lookup"><span data-stu-id="1e956-158">When you want your logic app to reference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="1e956-159">Bijvoorbeeld, kunt u uw logische app om te verwijzen naar een Azure-functie of integratiepakket account die u samen met uw logische app wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="1e956-159">For example, you might want your logic app to reference an Azure Function or integration account that you want to deploy alongside your logic app.</span></span> <span data-ttu-id="1e956-160">Volg deze richtlijnen over het gebruik van parameters in de implementatiesjabloon voor, zodat de Logic App Designer correct wordt gerenderd.</span><span class="sxs-lookup"><span data-stu-id="1e956-160">Follow these guidelines about how to use parameters in your deployment template so that the Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="1e956-161">U kunt logische app parameters in deze soorten triggers en acties:</span><span class="sxs-lookup"><span data-stu-id="1e956-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="1e956-162">Onderliggende werkstroom</span><span class="sxs-lookup"><span data-stu-id="1e956-162">Child workflow</span></span>
*   <span data-ttu-id="1e956-163">Functie-app</span><span class="sxs-lookup"><span data-stu-id="1e956-163">Function app</span></span>
*   <span data-ttu-id="1e956-164">APIM aanroep</span><span class="sxs-lookup"><span data-stu-id="1e956-164">APIM call</span></span>
*   <span data-ttu-id="1e956-165">De URL van de runtime verbinding API</span><span class="sxs-lookup"><span data-stu-id="1e956-165">API connection runtime URL</span></span>
*   <span data-ttu-id="1e956-166">Verbindingspad API</span><span class="sxs-lookup"><span data-stu-id="1e956-166">API connection path</span></span>

<span data-ttu-id="1e956-167">En u kunt een sjabloonfuncties, zoals parameters, variabelen, resourceId, concat, enzovoort. Dit is hoe u de resource-ID van het Azure-functie kunt vervangen:</span><span class="sxs-lookup"><span data-stu-id="1e956-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace the Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="1e956-168">En waar u parameters wilt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1e956-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="1e956-169">Als een ander voorbeeld kunt u de Service Bus-verzendbewerking bericht voorzien:</span><span class="sxs-lookup"><span data-stu-id="1e956-169">As another example you can parameterize the Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="1e956-170">host.runtimeUrl is optioneel en kan worden verwijderd uit de sjabloon, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="1e956-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="1e956-171">Voor Logic App Designer werken wanneer u parameters gebruiken, moet u standaardwaarden, bijvoorbeeld opgeven:</span><span class="sxs-lookup"><span data-stu-id="1e956-171">For the Logic App Designer to work when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="1e956-172">Uw logische app opslaan</span><span class="sxs-lookup"><span data-stu-id="1e956-172">Save your logic app</span></span>

<span data-ttu-id="1e956-173">Als u wilt uw logische app op elk gewenst moment opslaan, gaat u naar **bestand** > **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1e956-173">To save your logic app at anytime, go to **File** > **Save**.</span></span> <span data-ttu-id="1e956-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="1e956-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="1e956-175">Als uw logische app fouten heeft bij het opslaan van uw app, worden deze weergegeven in de Visual Studio **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="1e956-175">If your logic app has any errors when you save your app, they appear in the Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="1e956-176">Uw logische app vanuit Visual Studio implementeren</span><span class="sxs-lookup"><span data-stu-id="1e956-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="1e956-177">Na het configureren van uw app kunt u rechtstreeks vanuit Visual Studio in een paar stappen implementeren.</span><span class="sxs-lookup"><span data-stu-id="1e956-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="1e956-178">Met de rechtermuisknop op uw project in Solution Explorer en Ga naar **implementeren** > **nieuwe implementatie...**</span><span class="sxs-lookup"><span data-stu-id="1e956-178">In Solution Explorer, right-click your project, and go to **Deploy** > **New Deployment...**</span></span>

    ![Nieuwe implementatie](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="1e956-180">Wanneer u wordt gevraagd, moet u zich aanmelden bij uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1e956-180">When you're prompted, sign in to your Azure subscription.</span></span> 

3. <span data-ttu-id="1e956-181">Nu moet u de details voor de resourcegroep waar u uw logische app implementeren.</span><span class="sxs-lookup"><span data-stu-id="1e956-181">Now you must select the details for the resource group where you want to deploy your logic app.</span></span> <span data-ttu-id="1e956-182">Wanneer u bent klaar, selecteert u **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="1e956-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e956-183">Zorg ervoor dat u het juiste bestand voor de sjabloon en parameters voor de resourcegroep selecteert.</span><span class="sxs-lookup"><span data-stu-id="1e956-183">Make sure that you select the correct template and parameters file for the resource group.</span></span> <span data-ttu-id="1e956-184">Als u implementeren in een productieomgeving wilt, bijvoorbeeld het parameterbestand productie kiezen.</span><span class="sxs-lookup"><span data-stu-id="1e956-184">For example, if you want to deploy to a production environment, choose the production parameters file.</span></span>

    ![Implementeren in resourcegroep](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="1e956-186">Status van de implementatie wordt weergegeven in de **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="1e956-186">The deployment status appears in the **Output** window.</span></span> 
    <span data-ttu-id="1e956-187">U moet selecteren **Azure inrichting** in de **tonen de uitvoer van** lijst.</span><span class="sxs-lookup"><span data-stu-id="1e956-187">You might have to select **Azure Provisioning** in the **Show output from** list.</span></span>

    ![Implementatie statusuitvoer](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="1e956-189">U kunt in de toekomst bewerken van uw logische app in broncodebeheer en Visual Studio gebruiken voor het implementeren van nieuwe versies.</span><span class="sxs-lookup"><span data-stu-id="1e956-189">In the future, you can edit your logic app in source control, and use Visual Studio to deploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="1e956-190">Als u de definitie van de Azure-portal rechtstreeks wijzigt, worden deze wijzigingen overschreven wanneer u vanuit Visual Studio opnieuw implementeert.</span><span class="sxs-lookup"><span data-stu-id="1e956-190">If you change the definition in the Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-to-an-existing-resource-group-project"></a><span data-ttu-id="1e956-191">Uw logische app toevoegen aan een bestaande resourcegroep-project</span><span class="sxs-lookup"><span data-stu-id="1e956-191">Add your logic app to an existing Resource Group project</span></span>

<span data-ttu-id="1e956-192">Als u een bestaand project voor de resourcegroep hebt, kunt u uw logische app toevoegen aan het project in het venster JSON-overzicht.</span><span class="sxs-lookup"><span data-stu-id="1e956-192">If you have an existing Resource Group project, you can add your logic app to that project in the JSON Outline window.</span></span> <span data-ttu-id="1e956-193">U kunt ook een andere logische app naast de app die u eerder hebt gemaakt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1e956-193">You can also add another logic app alongside the app you previously created.</span></span>

1. <span data-ttu-id="1e956-194">Open het `<template>.json`-bestand.</span><span class="sxs-lookup"><span data-stu-id="1e956-194">Open the `<template>.json` file.</span></span>

2. <span data-ttu-id="1e956-195">De JSON-overzicht om venster te openen, gaat u naar **weergave** > **overige vensters** > **JSON-overzicht**.</span><span class="sxs-lookup"><span data-stu-id="1e956-195">To open the JSON Outline window, go to **View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="1e956-196">Als u wilt een resource toevoegen aan het sjabloonbestand, klikt u op **Resource toevoegen** aan de bovenkant van het venster JSON-overzicht.</span><span class="sxs-lookup"><span data-stu-id="1e956-196">To add a resource to the template file, click **Add Resource** at the top of the JSON Outline window.</span></span> <span data-ttu-id="1e956-197">Of in het venster JSON-overzicht met de rechtermuisknop op **resources**, en selecteer **nieuwe Resource toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1e956-197">Or in the JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Venster JSON-overzicht](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="1e956-199">In de **Resource toevoegen** in het dialoogvenster, zoeken en selecteert u **logische App**.</span><span class="sxs-lookup"><span data-stu-id="1e956-199">In the **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="1e956-200">Naam van uw logische app en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1e956-200">Name your logic app, and choose **Add**.</span></span>

    ![Resource toevoegen](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="1e956-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e956-202">Next Steps</span></span>

* [<span data-ttu-id="1e956-203">Logic apps beheren met Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="1e956-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="1e956-204">Algemene voorbeelden en scenario's weergeven</span><span class="sxs-lookup"><span data-stu-id="1e956-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="1e956-205">Meer informatie over het automatiseren van bedrijfsprocessen met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1e956-205">Learn how to automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="1e956-206">Meer informatie over het integreren van uw systemen met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1e956-206">Learn how to integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
