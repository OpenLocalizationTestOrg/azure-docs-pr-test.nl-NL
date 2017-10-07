---
title: uw eerste functie van Azure Portal Hallo aaaCreate | Microsoft Docs
description: Meer informatie over hoe uw eerste Azure-functie voor het gebruik van zonder server worden uitgevoerd toocreate hello Azure-portal.
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
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="9e69a-103">Maken van uw eerste functie in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9e69a-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="9e69a-104">Azure Functions, kunt u uw code in een omgeving zonder server uitvoeren zonder toofirst een virtuele machine maken of een webtoepassing publiceert.</span><span class="sxs-lookup"><span data-stu-id="9e69a-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="9e69a-105">In dit onderwerp informatie over hoe toouse functioneert toocreate een functie "Hallo wereld" in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9e69a-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Functie-app maken in hello Azure-portal](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="9e69a-107">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="9e69a-107">Log in tooAzure</span></span>

<span data-ttu-id="9e69a-108">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9e69a-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="9e69a-109">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="9e69a-109">Create a function app</span></span>

<span data-ttu-id="9e69a-110">U moet een functie-app toohost Hallo uitvoering van uw functies hebben.</span><span class="sxs-lookup"><span data-stu-id="9e69a-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="9e69a-111">Met een functie-app kunt u functies groeperen in een logische eenheid, zodat u resources eenvoudiger kunt beheren, implementeren en delen.</span><span class="sxs-lookup"><span data-stu-id="9e69a-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="9e69a-112">Vervolgens maakt u een functie in nieuwe Hallo-functie-app.</span><span class="sxs-lookup"><span data-stu-id="9e69a-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="9e69a-113"><a name="create-function"></a>Een door HTTP geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="9e69a-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="9e69a-114">Vouw uw nieuwe functie-app en klik op Hallo  **+**  knop naast te**functies**.</span><span class="sxs-lookup"><span data-stu-id="9e69a-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="9e69a-115">In Hallo **snel aan de slag** pagina **WebHook + API**, **een taal kiezen** voor uw functie en klik op **maken van deze functie** .</span><span class="sxs-lookup"><span data-stu-id="9e69a-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Functies in Quick Start hello Azure-portal.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="9e69a-117">Een functie wordt gemaakt in uw gekozen taal met Hallo-sjabloon voor een functie HTTP is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9e69a-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="9e69a-118">U kunt de nieuwe functie Hallo uitvoeren door een HTTP-aanvraag te verzenden.</span><span class="sxs-lookup"><span data-stu-id="9e69a-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="9e69a-119">Hallo functie testen</span><span class="sxs-lookup"><span data-stu-id="9e69a-119">Test hello function</span></span>

1. <span data-ttu-id="9e69a-120">Klik in de nieuwe functie op **</> Functie-URL ophalen**, selecteer **Standaard (functietoets)** en klik vervolgens op **Kopieer**.</span><span class="sxs-lookup"><span data-stu-id="9e69a-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Hallo function URL kopiëren van hello Azure-portal](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="9e69a-122">Hallo function URL in de adresbalk van uw browser plakken.</span><span class="sxs-lookup"><span data-stu-id="9e69a-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="9e69a-123">Hallo-queryreeks toevoegen `&name=<yourname>` toothis URL en druk op Hallo `Enter` sleutel op uw toetsenbord tooexecute Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9e69a-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="9e69a-124">Hallo Hieronder volgt een voorbeeld van het Hallo-antwoord geretourneerd door de functie Hallo in de browser Edge Hallo:</span><span class="sxs-lookup"><span data-stu-id="9e69a-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![De reactie van de functie in Hallo browser.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="9e69a-126">Hallo-aanvraag URL bevat een sleutel die is vereist, standaard tooaccess uw functie via HTTP.</span><span class="sxs-lookup"><span data-stu-id="9e69a-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="9e69a-127">Wanneer de functie wordt uitgevoerd, is traceringsinformatie toohello Logboeken geschreven.</span><span class="sxs-lookup"><span data-stu-id="9e69a-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="9e69a-128">toosee hello trace-uitvoer van de vorige uitvoering hello, tooyour functie in de portal Hallo retourneren en klik op Hallo pijl onderaan Hallo Hallo scherm tooexpand **logboeken**.</span><span class="sxs-lookup"><span data-stu-id="9e69a-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![Functies melden viewer hello Azure-portal.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="9e69a-130">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="9e69a-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="9e69a-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e69a-131">Next steps</span></span>

<span data-ttu-id="9e69a-132">U hebt een functie-app met een eenvoudige door HTTP geactiveerde functie gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9e69a-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="9e69a-133">Zie [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Azure Functions-HTTP- en webhookbindingen) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9e69a-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



