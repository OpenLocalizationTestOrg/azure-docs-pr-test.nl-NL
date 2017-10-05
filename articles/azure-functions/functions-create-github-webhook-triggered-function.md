---
title: Een functie in Azure maken die wordt geactiveerd door een GitHub-webhook | Microsoft Docs
description: Gebruik Azure Functions voor het maken van een functie zonder server die wordt aangeroepen door een GitHub-webhook.
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
ms.openlocfilehash: 038bb4cf0a9278416261c05ddaa0ee97d83b63c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="52797-103">Een door een GitHub-webhook geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="52797-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="52797-104">Ontdek hoe u een functie maakt die wordt geactiveerd door een HTTP-webhookaanvraag met een specifieke GitHub-nettolading.</span><span class="sxs-lookup"><span data-stu-id="52797-104">Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Een door een GitHub-webhook geactiveerde functie in Azure Portal](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="52797-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="52797-106">Prerequisites</span></span>

+ <span data-ttu-id="52797-107">Een GitHub-account met ten minste één project.</span><span class="sxs-lookup"><span data-stu-id="52797-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="52797-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="52797-108">An Azure subscription.</span></span> <span data-ttu-id="52797-109">Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="52797-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="52797-110">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="52797-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="52797-112">Vervolgens maakt u een functie in de nieuwe functie-app.</span><span class="sxs-lookup"><span data-stu-id="52797-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="52797-113">Een door een GitHub-webhook geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="52797-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="52797-114">Vouw de functie-app uit en klik op de knop **+** naast **Functies**.</span><span class="sxs-lookup"><span data-stu-id="52797-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="52797-115">Als dit de eerste functie in de functie-app is, selecteert u **Aangepaste functie**.</span><span class="sxs-lookup"><span data-stu-id="52797-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="52797-116">U ziet nu de volledige set het functiesjablonen.</span><span class="sxs-lookup"><span data-stu-id="52797-116">This displays the complete set of function templates.</span></span>

    ![De Quick Start-pagina van Functions in Azure Portal](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="52797-118">Selecteer de **GitHub WebHook** sjabloon voor de gewenste taal.</span><span class="sxs-lookup"><span data-stu-id="52797-118">Select the **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="52797-119">**Geef de functie een naam** en selecteer vervolgens **Maken**.</span><span class="sxs-lookup"><span data-stu-id="52797-119">**Name your function**, then select **Create**.</span></span>

     ![Een door een GitHub-webhook geactiveerde functie maken in Azure Portal](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="52797-121">Klik in de nieuwe functie op **</> Functie-URL ophalen**, kopieer de waarden en sla deze op.</span><span class="sxs-lookup"><span data-stu-id="52797-121">In your new function, click **</> Get function URL**, then copy and save the values.</span></span> <span data-ttu-id="52797-122">Doe hetzelfde voor **</> GitHub-geheim ophalen**.</span><span class="sxs-lookup"><span data-stu-id="52797-122">Do the same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="52797-123">U hebt deze waarden nodig voor het configureren van de webhook in GitHub.</span><span class="sxs-lookup"><span data-stu-id="52797-123">You use these values to configure the webhook in GitHub.</span></span>

    ![De functiecode controleren](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="52797-125">Vervolgens maakt u een webhook in uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="52797-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-the-webhook"></a><span data-ttu-id="52797-126">De webhook configureren</span><span class="sxs-lookup"><span data-stu-id="52797-126">Configure the webhook</span></span>

1. <span data-ttu-id="52797-127">Navigeer naar een van uw opslagplaatsen in GitHub.</span><span class="sxs-lookup"><span data-stu-id="52797-127">In GitHub, navigate to a repository that you own.</span></span> <span data-ttu-id="52797-128">U kunt ook een opslagplaats gebruiken die u hebt gesplitst.</span><span class="sxs-lookup"><span data-stu-id="52797-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="52797-129">Als u een opslagplaats moet splitsen, gebruikt u <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="52797-129">If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="52797-130">Klik achtereenvolgens op **Instellingen**, **Webhooks** en **Webhook toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="52797-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Een GitHub-webhook toevoegen](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="52797-132">Gebruik de instellingen zoals die in de tabel zijn opgegeven en klik vervolgens op **Webhook toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="52797-132">Use settings as specified in the table, then click **Add webhook**.</span></span>

    ![Webhook-URL en geheim instellen](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="52797-134">Instelling</span><span class="sxs-lookup"><span data-stu-id="52797-134">Setting</span></span> | <span data-ttu-id="52797-135">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="52797-135">Suggested value</span></span> | <span data-ttu-id="52797-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="52797-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="52797-137">**URL van de nettolading**</span><span class="sxs-lookup"><span data-stu-id="52797-137">**Payload URL**</span></span> | <span data-ttu-id="52797-138">Gekopieerde waarde</span><span class="sxs-lookup"><span data-stu-id="52797-138">Copied value</span></span> | <span data-ttu-id="52797-139">Gebruik de waarde die wordt geretourneerd door **</> Functie-URL ophalen**.</span><span class="sxs-lookup"><span data-stu-id="52797-139">Use the value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="52797-140">**Geheim**</span><span class="sxs-lookup"><span data-stu-id="52797-140">**Secret**</span></span>   | <span data-ttu-id="52797-141">Gekopieerde waarde</span><span class="sxs-lookup"><span data-stu-id="52797-141">Copied value</span></span> | <span data-ttu-id="52797-142">Gebruik de waarde die wordt geretourneerd door **</> GitHub-geheim ophalen**.</span><span class="sxs-lookup"><span data-stu-id="52797-142">Use the value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="52797-143">**Inhoudstype**</span><span class="sxs-lookup"><span data-stu-id="52797-143">**Content type**</span></span> | <span data-ttu-id="52797-144">application/json</span><span class="sxs-lookup"><span data-stu-id="52797-144">application/json</span></span> | <span data-ttu-id="52797-145">De functie verwacht een JSON-nettolading.</span><span class="sxs-lookup"><span data-stu-id="52797-145">The function expects a JSON payload.</span></span> |
| <span data-ttu-id="52797-146">Gebeurtenistriggers</span><span class="sxs-lookup"><span data-stu-id="52797-146">Event triggers</span></span> | <span data-ttu-id="52797-147">Ik wil afzonderlijke gebeurtenissen selecteren</span><span class="sxs-lookup"><span data-stu-id="52797-147">Let me select individual events</span></span> | <span data-ttu-id="52797-148">We willen alleen activeren bij gebeurtenissen met een opmerking bij actie van het item.</span><span class="sxs-lookup"><span data-stu-id="52797-148">We only want to trigger on issue comment events.</span></span>  |
| | <span data-ttu-id="52797-149">Opmerking bij actie item</span><span class="sxs-lookup"><span data-stu-id="52797-149">Issue comment</span></span> |  |

<span data-ttu-id="52797-150">Nu is de webhook zo geconfigureerd dat de functie wordt geactiveerd wanneer er een nieuwe probleemopmerking wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="52797-150">Now, the webhook is configured to trigger your function when a new issue comment is added.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="52797-151">De functie testen</span><span class="sxs-lookup"><span data-stu-id="52797-151">Test the function</span></span>

1. <span data-ttu-id="52797-152">Open in uw GitHub-opslagplaats het tabblad **Problemen** in een nieuw browservenster.</span><span class="sxs-lookup"><span data-stu-id="52797-152">In your GitHub repository, open the **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="52797-153">Klik in het nieuwe venster op **Nieuw probleem**, voer een titel in en klik op **Nieuw probleem verzenden**.</span><span class="sxs-lookup"><span data-stu-id="52797-153">In the new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="52797-154">Typ een opmerking bij probleem en klik op **Opmerking**.</span><span class="sxs-lookup"><span data-stu-id="52797-154">In the issue, type a comment and click **Comment**.</span></span>

    ![Voeg een opmerking bij de actie van het item van GitHub toe.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="52797-156">Ga terug naar de portal en bekijk de logboeken.</span><span class="sxs-lookup"><span data-stu-id="52797-156">Go back to the portal and view the logs.</span></span> <span data-ttu-id="52797-157">Hier ziet u een traceervermelding met de tekst van de nieuwe opmerking.</span><span class="sxs-lookup"><span data-stu-id="52797-157">You should see a trace entry with the new comment text.</span></span>

     ![Bekijk de tekst van de opmerking in de logboeken.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="52797-159">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="52797-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="52797-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52797-160">Next steps</span></span>

<span data-ttu-id="52797-161">U hebt een functie gemaakt die wordt uitgevoerd wanneer er een aanvraag wordt ontvangen van een GitHub-webhook.</span><span class="sxs-lookup"><span data-stu-id="52797-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="52797-162">Zie [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md) (Azure Functions-HTTP- en webhookbindingen) voor meer informatie over webhooktriggers.</span><span class="sxs-lookup"><span data-stu-id="52797-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
