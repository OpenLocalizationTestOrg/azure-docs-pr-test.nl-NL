---
title: een functie in Azure geactiveerd door Wachtrijberichten aaaCreate | Microsoft Docs
description: Gebruik Azure Functions toocreate een zonder server-functie die wordt opgeroepen door een berichten verzonden tooan Azure Storage-wachtrij.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="260fd-103">Een door Azure Queue Storage geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="260fd-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="260fd-104">Meer informatie over hoe toocreate een functie die wordt geactiveerd wanneer berichten worden verzonden tooan Azure Storage-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="260fd-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="260fd-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="260fd-106">Prerequisites</span></span>

- <span data-ttu-id="260fd-107">Download en installeer Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="260fd-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="260fd-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="260fd-108">An Azure subscription.</span></span> <span data-ttu-id="260fd-109">Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="260fd-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="260fd-110">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="260fd-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="260fd-112">Vervolgens maakt u een functie in nieuwe Hallo-functie-app.</span><span class="sxs-lookup"><span data-stu-id="260fd-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="260fd-113">Een door een wachtrij geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="260fd-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="260fd-114">Vouw de functie-app en klik op Hallo  **+**  knop naast te**functies**.</span><span class="sxs-lookup"><span data-stu-id="260fd-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="260fd-115">Als dit eerste functie in uw app functie hello, selecteer **aangepaste functie**.</span><span class="sxs-lookup"><span data-stu-id="260fd-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="260fd-116">De volledige set Hallo van functie-sjablonen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="260fd-116">This displays hello complete set of function templates.</span></span>

    ![Functies Quick Start-pagina in hello Azure-portal](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="260fd-118">Selecteer Hallo **QueueTrigger** sjabloon voor de gewenste taal en Hallo-instellingen zoals opgegeven in de tabel hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="260fd-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![De opslagfunctie wachtrij geactiveerd Hallo maken.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="260fd-120">Instelling</span><span class="sxs-lookup"><span data-stu-id="260fd-120">Setting</span></span> | <span data-ttu-id="260fd-121">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="260fd-121">Suggested value</span></span> | <span data-ttu-id="260fd-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="260fd-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="260fd-123">**Wachtrijnaam**</span><span class="sxs-lookup"><span data-stu-id="260fd-123">**Queue name**</span></span>   | <span data-ttu-id="260fd-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="260fd-124">myqueue-items</span></span>    | <span data-ttu-id="260fd-125">Naam van Hallo wachtrij tooconnect tooin uw Storage-account.</span><span class="sxs-lookup"><span data-stu-id="260fd-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="260fd-126">**Opslagaccountverbinding**</span><span class="sxs-lookup"><span data-stu-id="260fd-126">**Storage account connection**</span></span> | <span data-ttu-id="260fd-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="260fd-127">AzureWebJobStorage</span></span> | <span data-ttu-id="260fd-128">U kunt Hallo storage-account verbinding is al wordt gebruikt door de functie-app gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="260fd-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="260fd-129">**Een naam voor de functie opgeven**</span><span class="sxs-lookup"><span data-stu-id="260fd-129">**Name your function**</span></span> | <span data-ttu-id="260fd-130">Uniek in uw functie-app</span><span class="sxs-lookup"><span data-stu-id="260fd-130">Unique in your function app</span></span> | <span data-ttu-id="260fd-131">Naam van deze door een wachtrij geactiveerde functie.</span><span class="sxs-lookup"><span data-stu-id="260fd-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="260fd-132">Klik op **maken** toocreate uw functie.</span><span class="sxs-lookup"><span data-stu-id="260fd-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="260fd-133">Vervolgens maakt u verbinding tooyour Azure Storage-account en Hallo maken **rapportberichten items** storage-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="260fd-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="260fd-134">Hallo wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="260fd-134">Create hello queue</span></span>

1. <span data-ttu-id="260fd-135">Klik in de functie op **Integreren**, vouw **Documentatie** uit en kopieer de **Accountnaam** en de **Accountsleutel**.</span><span class="sxs-lookup"><span data-stu-id="260fd-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="260fd-136">U gebruikt deze referenties tooconnect toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="260fd-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="260fd-137">Als u al uw storage-account hebt gekoppeld, slaat u toostep 4.</span><span class="sxs-lookup"><span data-stu-id="260fd-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Hallo Storage-account verbindingsreferenties ophalen.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="260fd-139">v</span><span class="sxs-lookup"><span data-stu-id="260fd-139">v</span></span>

1. <span data-ttu-id="260fd-140">Hallo uitvoeren [Microsoft Azure Storage Explorer](http://storageexplorer.com/) hulpprogramma, klikt u op Hallo verbinding pictogram aan de linkerkant hello, kiest u **gebruik van een naam van het opslagaccount en de sleutel**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="260fd-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Hallo Account Opslagverkenner hulpprogramma uitvoeren.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="260fd-142">Voer Hallo **accountnaam** en **accountsleutel** uit stap 1, klikt u op **volgende** en vervolgens **Connect**.</span><span class="sxs-lookup"><span data-stu-id="260fd-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Geef referenties op Hallo opslag en verbinding maken.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="260fd-144">Vouw Hallo gekoppeld opslagaccount, met de rechtermuisknop op **wachtrijen**, klikt u op **wachtrij maken**, type `myqueue-items`, en druk op enter.</span><span class="sxs-lookup"><span data-stu-id="260fd-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Maak een opslagwachtrij.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="260fd-146">Nu dat u een opslagwachtrij hebt, kunt u Hallo functie testen door een berichtenwachtrij toohello toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="260fd-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="260fd-147">Hallo functie testen</span><span class="sxs-lookup"><span data-stu-id="260fd-147">Test hello function</span></span>

1. <span data-ttu-id="260fd-148">Terug in hello Azure-portal, vouw bladeren tooyour functie Hallo **logboeken** Hallo onderaan pagina Hallo en zorg ervoor dat in dit logboek streaming wordt niet onderbroken.</span><span class="sxs-lookup"><span data-stu-id="260fd-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="260fd-149">Vouw in Storage Explorer uw opslagaccount, **Wachtrijen** en **myqueue-items** uit en klik vervolgens op **Bericht toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="260fd-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Een berichtenwachtrij toohello toevoegen.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="260fd-151">Typ uw "Hallo wereld"-</span><span class="sxs-lookup"><span data-stu-id="260fd-151">Type your "Hello World!"</span></span> <span data-ttu-id="260fd-152">bericht in **Berichttekst** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="260fd-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="260fd-153">Wacht een paar seconden en vervolgens gaat u terug tooyour functie Logboeken en controleer of dat nieuwe Hallo-bericht is gelezen uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="260fd-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="260fd-155">Klik in Opslagverkenner op **vernieuwen** en controleer of het Hallo-bericht dat is verwerkt en is niet langer in de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="260fd-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="260fd-156">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="260fd-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="260fd-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="260fd-157">Next steps</span></span>

<span data-ttu-id="260fd-158">U kunt een functie die wordt uitgevoerd als er een bericht wordt toegevoegd tooa opslagwachtrij hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="260fd-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="260fd-159">Zie [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md) (Opslagwachtrijbindingen van Azure Functions) voor meer informatie over activeringen van Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="260fd-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>