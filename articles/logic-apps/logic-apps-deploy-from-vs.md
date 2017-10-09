---
title: aaaCreate, bouwen en implementeren van logische apps in Visual Studio - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="7113c-103">Ontwerpen, bouwen en implementeren van Azure Logic Apps in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7113c-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="7113c-104">Hoewel hello [Azure-portal](https://portal.azure.com/) een uitstekende manier biedt u toocreate en Azure Logic Apps beheren, kunt u Visual Studio voor het ontwerpen, bouwen en implementeren van uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="7113c-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="7113c-105">Visual Studio biedt uitgebreide hulpmiddelen zoals Hallo Logic App-ontwerper voor u toocreate logic apps, implementatie en automatisering sjablonen configureren en implementeren van tooany-omgeving.</span><span class="sxs-lookup"><span data-stu-id="7113c-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="7113c-106">de slag met Azure Logic Apps tooget meer [hoe toocreate uw eerste logische app in Azure-portal Hallo](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7113c-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="7113c-107">Installatiestappen</span><span class="sxs-lookup"><span data-stu-id="7113c-107">Installation steps</span></span>

<span data-ttu-id="7113c-108">tooinstall en Visual Studio-hulpprogramma's configureren voor Azure Logic Apps, volgt u deze stappen.</span><span class="sxs-lookup"><span data-stu-id="7113c-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7113c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7113c-109">Prerequisites</span></span>

* <span data-ttu-id="7113c-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) of Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7113c-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="7113c-111">[Nieuwste Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 of hoger)</span><span class="sxs-lookup"><span data-stu-id="7113c-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="7113c-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7113c-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="7113c-113">De website toohello toegang wanneer u de ontwerpfunctie Hallo</span><span class="sxs-lookup"><span data-stu-id="7113c-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="7113c-114">Installeer Visual Studio-hulpprogramma's voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="7113c-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="7113c-115">Nadat u Hallo-vereisten:</span><span class="sxs-lookup"><span data-stu-id="7113c-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="7113c-116">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7113c-116">Open Visual Studio.</span></span> <span data-ttu-id="7113c-117">Op Hallo **extra** selecteert u **uitbreidingen en Updates**.</span><span class="sxs-lookup"><span data-stu-id="7113c-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="7113c-118">Vouw Hallo **Online** categorie zodat u kunt online zoeken.</span><span class="sxs-lookup"><span data-stu-id="7113c-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="7113c-119">Blader of zoek naar **Logic Apps** totdat u **Azure Logic Apps-Tools voor Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="7113c-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="7113c-120">toodownload en installatie Hallo-extensie, klikt u op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="7113c-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="7113c-121">Visual Studio starten na de installatie.</span><span class="sxs-lookup"><span data-stu-id="7113c-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="7113c-122">U kunt ook downloaden [Azure Logic Apps-Tools voor Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) en Hallo [Azure Logic Apps-Tools voor Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) rechtstreeks vanuit Visual Studio Marketplace Hallo.</span><span class="sxs-lookup"><span data-stu-id="7113c-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="7113c-123">Nadat u de installatie hebt voltooid, kunt u hello Azure-resourcegroepproject met Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="7113c-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="7113c-124">Uw project maken</span><span class="sxs-lookup"><span data-stu-id="7113c-124">Create your project</span></span>

1. <span data-ttu-id="7113c-125">Op Hallo **bestand** menu te gaan**nieuw**, en selecteer **Project**.</span><span class="sxs-lookup"><span data-stu-id="7113c-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="7113c-126">Of tooadd uw project tooan bestaande oplossing, ga te**toevoegen**, en selecteer **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="7113c-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![Menu Bestand](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="7113c-128">In Hallo **nieuw Project** venster vinden **Cloud**, en selecteer **Azure-resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="7113c-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="7113c-129">Naam van uw project en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7113c-129">Name your project, and click **OK**.</span></span>

    ![Nieuw project toevoegen](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="7113c-131">Selecteer Hallo **logische App** sjabloon waarmee u een lege logic app-implementatiesjabloon voor u toouse maakt.</span><span class="sxs-lookup"><span data-stu-id="7113c-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="7113c-132">Nadat u de sjabloon hebt geselecteerd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7113c-132">After you select your template, click **OK**.</span></span>

    ![Selecteer de sjabloon voor logische Apps](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="7113c-134">U hebt nu uw oplossing logic app-project tooyour toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7113c-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="7113c-135">Uw implementatiebestand moet in Hallo Solution Explorer, worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7113c-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![Implementatiebestand](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="7113c-137">Uw logische app maken met Logic App-ontwerper</span><span class="sxs-lookup"><span data-stu-id="7113c-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="7113c-138">Wanneer u een Azure-resourcegroepproject met een logische app hebt, kunt u Hallo Logic App-ontwerper openen in Visual Studio toocreate uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="7113c-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="7113c-139">Hallo designer vereist een internetverbinding te connectors voor de beschikbare eigenschappen en gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="7113c-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="7113c-140">Als u Hallo Dynamics CRM Online connector gebruikt, vraagt Hallo designer bijvoorbeeld uw CRM-exemplaar tooshow beschikbaar aangepaste en de standaardeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="7113c-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="7113c-141">Met de rechtermuisknop op uw `<template>.json` bestand en selecteer **openen met Logic App-ontwerper**.</span><span class="sxs-lookup"><span data-stu-id="7113c-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="7113c-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="7113c-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="7113c-143">Kies uw Azure-abonnement, resourcegroep en locatie voor de implementatiesjabloon.</span><span class="sxs-lookup"><span data-stu-id="7113c-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7113c-144">Het ontwerpen van een logische app, maakt resources van de API-verbinding die query voor eigenschappen tijdens de ontwerp.</span><span class="sxs-lookup"><span data-stu-id="7113c-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="7113c-145">Visual Studio maakt gebruik van de geselecteerde resource groep toocreate deze verbindingen tijdens het ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="7113c-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="7113c-146">tooview of wijzigen van de API-verbindingen, gaat u toohello Azure-portal en bladert u naar **API verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="7113c-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![Abonnement kiezen](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="7113c-148">Hallo designer gebruikt Hallo definitie in Hallo `<template>.json` bestand voor de rendering.</span><span class="sxs-lookup"><span data-stu-id="7113c-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="7113c-149">Maken en ontwerpen van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="7113c-149">Create and design your logic app.</span></span> <span data-ttu-id="7113c-150">Uw implementatiesjabloon is bijgewerkt met de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="7113c-150">Your deployment template is updated with your changes.</span></span>

    ![App-ontwerper logica in Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="7113c-152">Visual Studio voegt `Microsoft.Web/connections` resources te uw resourcebestand voor de verbindingen uw logische app moet toofunction.</span><span class="sxs-lookup"><span data-stu-id="7113c-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="7113c-153">De eigenschappen van deze verbinding kunnen worden ingesteld bij het implementeren van, en nadat u hebt geïmplementeerd beheerd **API verbindingen** in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7113c-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="7113c-154">Switch tooJSON codeweergave</span><span class="sxs-lookup"><span data-stu-id="7113c-154">Switch tooJSON code view</span></span>

<span data-ttu-id="7113c-155">tooshow hello JSON-weergave voor uw logische app, selecteer Hallo **codeweergave** tabblad onderin Hallo Hallo Designer.</span><span class="sxs-lookup"><span data-stu-id="7113c-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="7113c-156">tooswitch back-toohello volledige resource JSON, met de rechtermuisknop op Hallo `<template>.json` bestand en selecteer **Open**.</span><span class="sxs-lookup"><span data-stu-id="7113c-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="7113c-157">Verwijzingen voor afhankelijke resources tooVisual Studio implementatiesjablonen toevoegen</span><span class="sxs-lookup"><span data-stu-id="7113c-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="7113c-158">Als u wilt dat uw logische app tooreference afhankelijke resources, kunt u [Azure Resource Manager-sjabloonfuncties](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in uw sjabloon logic app-implementatie.</span><span class="sxs-lookup"><span data-stu-id="7113c-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="7113c-159">Bijvoorbeeld, kunt u uw logische app tooreference een Azure-functie of integratiepakket account dat u wilt dat toodeploy samen met uw logische app.</span><span class="sxs-lookup"><span data-stu-id="7113c-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="7113c-160">Volg deze richtlijnen over hoe toouse parameters in de implementatiesjabloon voor de zodat die Logic App-ontwerper Hallo correct wordt gerenderd.</span><span class="sxs-lookup"><span data-stu-id="7113c-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="7113c-161">U kunt logische app parameters in deze soorten triggers en acties:</span><span class="sxs-lookup"><span data-stu-id="7113c-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="7113c-162">Onderliggende werkstroom</span><span class="sxs-lookup"><span data-stu-id="7113c-162">Child workflow</span></span>
*   <span data-ttu-id="7113c-163">Functie-app</span><span class="sxs-lookup"><span data-stu-id="7113c-163">Function app</span></span>
*   <span data-ttu-id="7113c-164">APIM aanroep</span><span class="sxs-lookup"><span data-stu-id="7113c-164">APIM call</span></span>
*   <span data-ttu-id="7113c-165">De URL van de runtime verbinding API</span><span class="sxs-lookup"><span data-stu-id="7113c-165">API connection runtime URL</span></span>
*   <span data-ttu-id="7113c-166">Verbindingspad API</span><span class="sxs-lookup"><span data-stu-id="7113c-166">API connection path</span></span>

<span data-ttu-id="7113c-167">En u kunt een sjabloonfuncties, zoals parameters, variabelen, resourceId, concat, enzovoort. Dit is hoe u kunt vervangen hello Azure-functie resource-ID:</span><span class="sxs-lookup"><span data-stu-id="7113c-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="7113c-168">En waar u parameters wilt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7113c-168">And where you would use parameters:</span></span>

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
<span data-ttu-id="7113c-169">Als een ander voorbeeld kunt u Service Bus bericht verzendbewerking Hallo voorzien:</span><span class="sxs-lookup"><span data-stu-id="7113c-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

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
> <span data-ttu-id="7113c-170">host.runtimeUrl is optioneel en kan worden verwijderd uit de sjabloon, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="7113c-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="7113c-171">Voor Hallo Logic App-ontwerper toowork wanneer u parameters, moet u standaardwaarden opgeven, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7113c-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
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

### <a name="save-your-logic-app"></a><span data-ttu-id="7113c-172">Uw logische app opslaan</span><span class="sxs-lookup"><span data-stu-id="7113c-172">Save your logic app</span></span>

<span data-ttu-id="7113c-173">toosave uw logische app op elk gewenst moment, ga te**bestand** > **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7113c-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="7113c-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="7113c-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="7113c-175">Als uw logische app fouten heeft bij het opslaan van uw app, worden deze weergegeven in Visual Studio Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="7113c-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="7113c-176">Uw logische app vanuit Visual Studio implementeren</span><span class="sxs-lookup"><span data-stu-id="7113c-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="7113c-177">Na het configureren van uw app kunt u rechtstreeks vanuit Visual Studio in een paar stappen implementeren.</span><span class="sxs-lookup"><span data-stu-id="7113c-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="7113c-178">Met de rechtermuisknop op uw project in Solution Explorer en ga te**implementeren** > **nieuwe implementatie...**</span><span class="sxs-lookup"><span data-stu-id="7113c-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![Nieuwe implementatie](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="7113c-180">Wanneer u wordt gevraagd, meld u aan tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7113c-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="7113c-181">U moet nu Hallo details voor de resourcegroep Hallo waar u toodeploy uw logische app wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="7113c-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="7113c-182">Wanneer u bent klaar, selecteert u **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="7113c-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7113c-183">Zorg ervoor dat u de juiste sjabloon Hallo en parameterbestand voor resourcegroep Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="7113c-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="7113c-184">Als u toodeploy tooa productie-omgeving wilt, bijvoorbeeld Hallo productie parameterbestand kiezen.</span><span class="sxs-lookup"><span data-stu-id="7113c-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Tooresource groep implementeren](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="7113c-186">Hallo-Implementatiestatus wordt weergegeven in Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="7113c-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="7113c-187">Moet u wellicht tooselect **Azure inrichting** in Hallo **tonen de uitvoer van** lijst.</span><span class="sxs-lookup"><span data-stu-id="7113c-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![Implementatie statusuitvoer](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="7113c-189">In toekomstige Hallo, kunt u uw logische app in broncodebeheer bewerken en nieuwe versies van Visual Studio toodeploy gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7113c-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="7113c-190">Als u rechtstreeks Hallo definitie in hello Azure-portal wijzigt, worden deze wijzigingen overschreven wanneer u vanuit Visual Studio opnieuw implementeert.</span><span class="sxs-lookup"><span data-stu-id="7113c-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="7113c-191">Uw logische app tooan bestaande resourcegroep project toevoegen</span><span class="sxs-lookup"><span data-stu-id="7113c-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="7113c-192">Als u een bestaand project voor de resourcegroep hebt, kunt u uw logische app toothat-project in het venster van de JSON-overzicht Hallo kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7113c-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="7113c-193">U kunt ook een andere logische app naast Hallo-app die u eerder hebt gemaakt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7113c-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="7113c-194">Open Hallo `<template>.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="7113c-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="7113c-195">tooopen hello JSON overzichtsvenster te gaan**weergave** > **overige vensters** > **JSON-overzicht**.</span><span class="sxs-lookup"><span data-stu-id="7113c-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="7113c-196">tooadd toohello sjabloon bronbestand, klikt u op **Resource toevoegen** Hallo boven aan het venster van de JSON-overzicht Hallo.</span><span class="sxs-lookup"><span data-stu-id="7113c-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="7113c-197">Of met de rechtermuisknop in het venster JSON-overzicht hello, **resources**, en selecteer **nieuwe Resource toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7113c-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Venster JSON-overzicht](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="7113c-199">In Hallo **Resource toevoegen** in het dialoogvenster, zoeken en selecteert u **logische App**.</span><span class="sxs-lookup"><span data-stu-id="7113c-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="7113c-200">Naam van uw logische app en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7113c-200">Name your logic app, and choose **Add**.</span></span>

    ![Resource toevoegen](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="7113c-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7113c-202">Next Steps</span></span>

* [<span data-ttu-id="7113c-203">Logic apps beheren met Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="7113c-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="7113c-204">Algemene voorbeelden en scenario's weergeven</span><span class="sxs-lookup"><span data-stu-id="7113c-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="7113c-205">Meer informatie over hoe tooautomate bedrijfsprocessen met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="7113c-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="7113c-206">Meer informatie over hoe toointegrate uw systemen met Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="7113c-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
