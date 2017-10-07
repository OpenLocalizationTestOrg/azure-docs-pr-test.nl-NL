---
title: een functie in Azure geactiveerd door een GitHub webhook aaaCreate | Microsoft Docs
description: Azure Functions toocreate een zonder server-functie die wordt opgeroepen door een GitHub webhook gebruiken.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="f9752-103">Een door een GitHub-webhook geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="f9752-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="f9752-104">Meer informatie over hoe toocreate een functie die wordt veroorzaakt door een HTTP-webhook-aanvraag met een GitHub-specifieke nettolading.</span><span class="sxs-lookup"><span data-stu-id="f9752-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Github Webhook geactiveerd functie in hello Azure-portal](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="f9752-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f9752-106">Prerequisites</span></span>

+ <span data-ttu-id="f9752-107">Een GitHub-account met ten minste één project.</span><span class="sxs-lookup"><span data-stu-id="f9752-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="f9752-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f9752-108">An Azure subscription.</span></span> <span data-ttu-id="f9752-109">Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="f9752-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="f9752-110">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="f9752-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="f9752-112">Vervolgens maakt u een functie in nieuwe Hallo-functie-app.</span><span class="sxs-lookup"><span data-stu-id="f9752-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="f9752-113">Een door een GitHub-webhook geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="f9752-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="f9752-114">Vouw de functie-app en klik op Hallo  **+**  knop naast te**functies**.</span><span class="sxs-lookup"><span data-stu-id="f9752-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="f9752-115">Als dit eerste functie in uw app functie hello, selecteer **aangepaste functie**.</span><span class="sxs-lookup"><span data-stu-id="f9752-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="f9752-116">De volledige set Hallo van functie-sjablonen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f9752-116">This displays hello complete set of function templates.</span></span>

    ![Functies Quick Start-pagina in hello Azure-portal](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="f9752-118">Selecteer Hallo **GitHub WebHook** sjabloon voor de gewenste taal.</span><span class="sxs-lookup"><span data-stu-id="f9752-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="f9752-119">**Geef de functie een naam** en selecteer vervolgens **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f9752-119">**Name your function**, then select **Create**.</span></span>

     ![Maak een GitHub webhook geactiveerd-functie in hello Azure-portal](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="f9752-121">Klik in de nieuwe functie op **<> / Get function URL**, kopiëren en opslaan van Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="f9752-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="f9752-122">Hetzelfde geldt voor Hallo **<> / ophalen van GitHub geheim**.</span><span class="sxs-lookup"><span data-stu-id="f9752-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="f9752-123">U gebruikt deze waarden tooconfigure hello webhook in GitHub.</span><span class="sxs-lookup"><span data-stu-id="f9752-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Hallo functiecode bekijken](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="f9752-125">Vervolgens maakt u een webhook in uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f9752-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="f9752-126">Hallo webhook configureren</span><span class="sxs-lookup"><span data-stu-id="f9752-126">Configure hello webhook</span></span>

1. <span data-ttu-id="f9752-127">Navigeer in GitHub, tooa opslagplaats waarvan u eigenaar.</span><span class="sxs-lookup"><span data-stu-id="f9752-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="f9752-128">U kunt ook een opslagplaats gebruiken die u hebt gesplitst.</span><span class="sxs-lookup"><span data-stu-id="f9752-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="f9752-129">Als u een opslagplaats toofork moet, gebruikt u <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="f9752-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="f9752-130">Klik achtereenvolgens op **Instellingen**, **Webhooks** en **Webhook toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f9752-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Een GitHub-webhook toevoegen](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="f9752-132">Instellingen zoals opgegeven in de tabel hello gebruiken en klik vervolgens op **webhook toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f9752-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Hallo webhook-URL en geheim instellen](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="f9752-134">Instelling</span><span class="sxs-lookup"><span data-stu-id="f9752-134">Setting</span></span> | <span data-ttu-id="f9752-135">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="f9752-135">Suggested value</span></span> | <span data-ttu-id="f9752-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f9752-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="f9752-137">**URL van de nettolading**</span><span class="sxs-lookup"><span data-stu-id="f9752-137">**Payload URL**</span></span> | <span data-ttu-id="f9752-138">Gekopieerde waarde</span><span class="sxs-lookup"><span data-stu-id="f9752-138">Copied value</span></span> | <span data-ttu-id="f9752-139">Hallo-waarde geretourneerd door **<> / Get function URL**.</span><span class="sxs-lookup"><span data-stu-id="f9752-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="f9752-140">**Geheim**</span><span class="sxs-lookup"><span data-stu-id="f9752-140">**Secret**</span></span>   | <span data-ttu-id="f9752-141">Gekopieerde waarde</span><span class="sxs-lookup"><span data-stu-id="f9752-141">Copied value</span></span> | <span data-ttu-id="f9752-142">Hallo-waarde geretourneerd door **<> / ophalen van GitHub geheim**.</span><span class="sxs-lookup"><span data-stu-id="f9752-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="f9752-143">**Inhoudstype**</span><span class="sxs-lookup"><span data-stu-id="f9752-143">**Content type**</span></span> | <span data-ttu-id="f9752-144">application/json</span><span class="sxs-lookup"><span data-stu-id="f9752-144">application/json</span></span> | <span data-ttu-id="f9752-145">Hallo functie verwacht een JSON-nettolading.</span><span class="sxs-lookup"><span data-stu-id="f9752-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="f9752-146">Gebeurtenistriggers</span><span class="sxs-lookup"><span data-stu-id="f9752-146">Event triggers</span></span> | <span data-ttu-id="f9752-147">Ik wil afzonderlijke gebeurtenissen selecteren</span><span class="sxs-lookup"><span data-stu-id="f9752-147">Let me select individual events</span></span> | <span data-ttu-id="f9752-148">We willen alleen tootrigger op probleem Opmerking gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="f9752-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="f9752-149">Opmerking bij actie item</span><span class="sxs-lookup"><span data-stu-id="f9752-149">Issue comment</span></span> |  |

<span data-ttu-id="f9752-150">Nu Hallo webhook geconfigureerde tootrigger is de functie wanneer een nieuwe probleem opmerking wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f9752-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="f9752-151">Hallo functie testen</span><span class="sxs-lookup"><span data-stu-id="f9752-151">Test hello function</span></span>

1. <span data-ttu-id="f9752-152">Open in uw GitHub-opslagplaats Hallo **problemen** tabblad in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="f9752-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="f9752-153">Op het nieuwe venster Hallo **nieuwe probleem**, typt u een titel en klik vervolgens op **indienen van nieuwe probleem**.</span><span class="sxs-lookup"><span data-stu-id="f9752-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="f9752-154">Typ een opmerking in Hallo probleem, en klik op **Opmerking**.</span><span class="sxs-lookup"><span data-stu-id="f9752-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![Voeg een opmerking bij de actie van het item van GitHub toe.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="f9752-156">Ga terug toohello portal en bekijk Hallo Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f9752-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="f9752-157">Hier ziet u een vermelding in het traceerlogboek door Hallo nieuwe opmerkingstekst.</span><span class="sxs-lookup"><span data-stu-id="f9752-157">You should see a trace entry with hello new comment text.</span></span>

     ![De tekst hello opmerking in Hallo logboeken weergeven.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="f9752-159">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="f9752-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="f9752-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f9752-160">Next steps</span></span>

<span data-ttu-id="f9752-161">U hebt een functie gemaakt die wordt uitgevoerd wanneer er een aanvraag wordt ontvangen van een GitHub-webhook.</span><span class="sxs-lookup"><span data-stu-id="f9752-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="f9752-162">Zie [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Azure Functions-HTTP- en webhookbindingen) voor meer informatie over webhooktriggers.</span><span class="sxs-lookup"><span data-stu-id="f9752-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
