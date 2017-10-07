---
title: aaaCustom code voor Azure Logic Apps met Azure Functions | Microsoft Docs
description: Maken en uitvoeren van aangepaste code voor Azure Logic Apps met Azure Functions
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="cc0f5-103">Toevoegen en het uitvoeren van aangepaste code voor logic apps via Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cc0f5-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="cc0f5-104">aangepaste codefragmenten toorun van C# of node.js in logic apps, kunt u aangepaste functies via Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="cc0f5-105">[Azure Functions](../azure-functions/functions-overview.md) biedt server gratis computergebruik in Microsoft Azure en zijn handig voor het uitvoeren van deze taken:</span><span class="sxs-lookup"><span data-stu-id="cc0f5-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="cc0f5-106">Geavanceerde opmaak of compute van velden in logic apps</span><span class="sxs-lookup"><span data-stu-id="cc0f5-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="cc0f5-107">Berekeningen in een werkstroom.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="cc0f5-108">Hallo logic app-functionaliteit met functies die worden ondersteund in C# of node.js uitbreiden</span><span class="sxs-lookup"><span data-stu-id="cc0f5-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="cc0f5-109">Aangepaste functies voor uw logische apps maken</span><span class="sxs-lookup"><span data-stu-id="cc0f5-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="cc0f5-110">Het is raadzaam dat u een functie in hello Azure Functions-portal, Hallo **Generic Webhook - knooppunt** of **Generic Webhook - C#** sjablonen.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="cc0f5-111">Hallo resultaat maakt een sjabloon die accepteert een door het automatisch ingevuld `application/json` van een logische app.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="cc0f5-112">Functies die u van deze sjablonen maakt worden automatisch gedetecteerd en worden weergegeven in Hallo Logic App-ontwerper onder **Azure Functions in mijn regio.**</span><span class="sxs-lookup"><span data-stu-id="cc0f5-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="cc0f5-113">In de Azure-portal op Hallo Hallo **integreren** deelvenster voor de functie, de sjabloon moet worden weergegeven die **modus** instellen te**Webhook** en **Webhook type** te is ingesteld,**algemene JSON**.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="cc0f5-114">Webhook functies een aanvraag accepteren en doorgegeven aan de methode Hallo via een `data` variabele.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="cc0f5-115">U kunt toegang tot Hallo eigenschappen van uw payload met puntnotatie zoals `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="cc0f5-116">Voor een eenvoudige JavaScript-functie die een DateTime-waarde naar een datumtekenreeks converteert, ziet er bijvoorbeeld Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc0f5-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="cc0f5-117">Azure-functies aanroepen vanuit logic apps</span><span class="sxs-lookup"><span data-stu-id="cc0f5-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="cc0f5-118">toolist hello containers in uw abonnement en selecteer Hallo-functie die u wilt dat toocall in Logic App-ontwerper, klikt u op Hallo **acties** menu en selecteer een van de **Azure Functions in mijn regio**.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="cc0f5-119">Nadat u de functie Hallo selecteert, bent u toospecify gevraagd een object van de nettolading van de invoer.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="cc0f5-120">Dit object is Hallo-bericht dat logic app verzendt toohello functie Hallo en moet een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="cc0f5-121">Bijvoorbeeld, als u wilt dat toopass in Hallo **laatst gewijzigd** datum na een trigger Salesforce Hallo functie nettolading kan eruitzien als in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="cc0f5-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![Datum van laatste wijziging][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="cc0f5-123">Trigger logische apps van een functie</span><span class="sxs-lookup"><span data-stu-id="cc0f5-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="cc0f5-124">U kunt een logische app van binnen een functie activeren.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="cc0f5-125">Zie [Logic apps als aanroepbare eindpunten](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="cc0f5-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="cc0f5-126">Een logische app met een handmatige trigger maken en vervolgens genereren binnen de functie van een HTTP POST toohello handmatige trigger-URL met Hallo nettolading die u wilt toohello logische app verzonden.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="cc0f5-127">Een functie maken vanuit Logic App-ontwerper</span><span class="sxs-lookup"><span data-stu-id="cc0f5-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="cc0f5-128">U kunt ook een node.js-webhook-functie maken vanuit Hallo designer.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="cc0f5-129">Selecteer eerst **Azure Functions in mijn regio** en kies vervolgens een container voor uw functie.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="cc0f5-130">Als u nog een container hebt, moet u toocreate van Hallo [Azure Functions-portal](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="cc0f5-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="cc0f5-131">Selecteer vervolgens **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-131">Then select **Create New**.</span></span>  

<span data-ttu-id="cc0f5-132">een sjabloon op basis van Hallo gegevens die u toocompute wilt, toogenerate Geef Hallo context-object dat u van plan bent toopass in een functie.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="cc0f5-133">Dit object moet een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-133">This object must be a JSON object.</span></span> <span data-ttu-id="cc0f5-134">Bijvoorbeeld, als u in Hallo bestandsinhoud van een FTP-actie doorgeeft, Hallo context nettolading ziet eruit als in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="cc0f5-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![De nettolading van de context][2]

> [!NOTE]
> <span data-ttu-id="cc0f5-136">Omdat dit object is niet geconverteerd als een tekenreeks, wordt inhoud Hallo toegevoegd rechtstreeks toohello JSON-nettolading.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="cc0f5-137">Echter, treedt een fout als Hallo-object geen JSON-token is (dat wil zeggen, een tekenreeks of een JSON-object/array).</span><span class="sxs-lookup"><span data-stu-id="cc0f5-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="cc0f5-138">toocast Hallo-object als een tekenreeks toevoegen aanhalingstekens in de eerste illustratie Hallo in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="cc0f5-139">Hallo designer genereert vervolgens een functie-sjabloon dat u inline kunt maken.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="cc0f5-140">Variabelen zijn vooraf gemaakt op basis van dat u van plan toopass in de functie Hallo bent Hallo-context.</span><span class="sxs-lookup"><span data-stu-id="cc0f5-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
