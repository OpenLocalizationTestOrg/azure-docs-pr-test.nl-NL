---
title: Uw eerste functie maken vanuit Azure Portal | Microsoft Docs
description: Leer hoe u uw eerste serverloze Azure-functie kunt maken met behulp van Azure Portal.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="3e04c-103">Uw eerste functie maken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3e04c-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="3e04c-104">Met Azure Functions kunt u uw code in een serverloze omgeving uitvoeren zonder dat u eerst een virtuele machine moet maken of een webtoepassing moet publiceren.</span><span class="sxs-lookup"><span data-stu-id="3e04c-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="3e04c-105">In dit onderwerp leert u hoe met Azure Functions een 'Hallo wereld-functie' in Azure Portal kunt maken.</span><span class="sxs-lookup"><span data-stu-id="3e04c-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Functie-app maken in Azure Portal](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="3e04c-107">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="3e04c-107">Log in to Azure</span></span>

<span data-ttu-id="3e04c-108">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3e04c-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="3e04c-109">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="3e04c-109">Create a function app</span></span>

<span data-ttu-id="3e04c-110">U moet een functie-app hebben die als host fungeert voor de uitvoering van uw functies.</span><span class="sxs-lookup"><span data-stu-id="3e04c-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="3e04c-111">Met een functie-app kunt u functies groeperen in een logische eenheid, zodat u resources eenvoudiger kunt beheren, implementeren en delen.</span><span class="sxs-lookup"><span data-stu-id="3e04c-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="3e04c-112">Vervolgens maakt u een functie in de nieuwe functie-app.</span><span class="sxs-lookup"><span data-stu-id="3e04c-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="3e04c-113"><a name="create-function"></a>Een door HTTP geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="3e04c-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="3e04c-114">Vouw de nieuwe functie-app uit en klik vervolgens op de knop  **+**  naast **Functies**.</span><span class="sxs-lookup"><span data-stu-id="3e04c-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="3e04c-115">Selecteer op de pagina **Ga snel aan de slag** de optie **WebHook + API**, **Kies een taal** voor uw functie en klik op **Deze functie maken**.</span><span class="sxs-lookup"><span data-stu-id="3e04c-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![De Quick Start van Azure Functions in Azure Portal.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="3e04c-117">Een functie wordt gemaakt in de door u gekozen taal met de sjabloon voor een door HTTP geactiveerde functie.</span><span class="sxs-lookup"><span data-stu-id="3e04c-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="3e04c-118">U kunt de nieuwe functie uitvoeren door een HTTP-aanvraag te verzenden.</span><span class="sxs-lookup"><span data-stu-id="3e04c-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="3e04c-119">De functie testen</span><span class="sxs-lookup"><span data-stu-id="3e04c-119">Test the function</span></span>

1. <span data-ttu-id="3e04c-120">Klik in de nieuwe functie op **</> Functie-URL ophalen**, selecteer **Standaard (functietoets)** en klik vervolgens op **Kopieer**.</span><span class="sxs-lookup"><span data-stu-id="3e04c-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![De functie-URL vanuit Azure Portal kopiëren](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="3e04c-122">Plak de URL van de functie in de adresbalk van uw browser.</span><span class="sxs-lookup"><span data-stu-id="3e04c-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="3e04c-123">Voeg de queryreeks `&name=<yourname>` toe aan het einde van deze URL en druk op de toets `Enter` op het toetsenbord om de aanvraag uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3e04c-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="3e04c-124">Hier ziet u een voorbeeld van het antwoord dat wordt geretourneerd door de functie in de Edge-browser:</span><span class="sxs-lookup"><span data-stu-id="3e04c-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![Het antwoord van de functie in de browser.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="3e04c-126">De aanvraag-URL bevat een sleutel die standaard is vereist, en waarmee u via HTTP toegang hebt tot de functie.</span><span class="sxs-lookup"><span data-stu-id="3e04c-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="3e04c-127">Wanneer uw functie wordt uitgevoerd, wordt traceringsinformatie naar de logboeken geschreven.</span><span class="sxs-lookup"><span data-stu-id="3e04c-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="3e04c-128">Als u de trace-uitvoer van de vorige uitvoering wilt zien, gaat u terug naar de functie in de portal en klikt u op de pijl-omhoog onder aan het scherm om de **logboeken** uit te klappen.</span><span class="sxs-lookup"><span data-stu-id="3e04c-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![De viewer voor functielogboeken in Azure Portal.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="3e04c-130">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="3e04c-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="3e04c-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3e04c-131">Next steps</span></span>

<span data-ttu-id="3e04c-132">U hebt een functie-app met een eenvoudige door HTTP geactiveerde functie gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e04c-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="3e04c-133">Zie [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Azure Functions-HTTP- en webhookbindingen) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3e04c-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



