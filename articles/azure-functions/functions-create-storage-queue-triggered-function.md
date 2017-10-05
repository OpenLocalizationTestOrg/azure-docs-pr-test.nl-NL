---
title: Een functie in Azure maken die wordt geactiveerd door wachtrijberichten | Microsoft Docs
description: Gebruik Azure Functions voor het maken van een functie zonder server die wordt aangeroepen door berichten die zijn verzonden naar een Azure Storage-wachtrij.
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
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="9e646-103">Een door Azure Queue Storage geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="9e646-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="9e646-104">Ontdek hoe u een functie maakt die wordt geactiveerd wanneer er berichten worden verzonden naar een Azure Storage-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="9e646-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![Bekijk het bericht in de logboeken.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="9e646-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9e646-106">Prerequisites</span></span>

- <span data-ttu-id="9e646-107">De [Microsoft Azure Storage Explorer](http://storageexplorer.com/) downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="9e646-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="9e646-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e646-108">An Azure subscription.</span></span> <span data-ttu-id="9e646-109">Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="9e646-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="9e646-110">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="9e646-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="9e646-112">Vervolgens maakt u een functie in de nieuwe functie-app.</span><span class="sxs-lookup"><span data-stu-id="9e646-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="9e646-113">Een door een wachtrij geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="9e646-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="9e646-114">Vouw de functie-app uit en klik op de knop **+** naast **Functies**.</span><span class="sxs-lookup"><span data-stu-id="9e646-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="9e646-115">Als dit de eerste functie in de functie-app is, selecteert u **Aangepaste functie**.</span><span class="sxs-lookup"><span data-stu-id="9e646-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="9e646-116">U ziet nu de volledige set het functiesjablonen.</span><span class="sxs-lookup"><span data-stu-id="9e646-116">This displays the complete set of function templates.</span></span>

    ![De Quick Start-pagina van Functions in Azure Portal](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="9e646-118">Selecteer de sjabloon **QueueTrigger** voor de gewenste taal en gebruik de instellingen die zijn opgegeven in de tabel.</span><span class="sxs-lookup"><span data-stu-id="9e646-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![Maak de door de opslagwachtrij geactiveerde functie.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="9e646-120">Instelling</span><span class="sxs-lookup"><span data-stu-id="9e646-120">Setting</span></span> | <span data-ttu-id="9e646-121">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="9e646-121">Suggested value</span></span> | <span data-ttu-id="9e646-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9e646-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="9e646-123">**Wachtrijnaam**</span><span class="sxs-lookup"><span data-stu-id="9e646-123">**Queue name**</span></span>   | <span data-ttu-id="9e646-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="9e646-124">myqueue-items</span></span>    | <span data-ttu-id="9e646-125">De naam van de wachtrij waarmee u verbinding moet maken in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9e646-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="9e646-126">**Opslagaccountverbinding**</span><span class="sxs-lookup"><span data-stu-id="9e646-126">**Storage account connection**</span></span> | <span data-ttu-id="9e646-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="9e646-127">AzureWebJobStorage</span></span> | <span data-ttu-id="9e646-128">U kunt de opslagaccountverbinding gebruiken die al door de functie-app wordt gebruikt of u kunt een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="9e646-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="9e646-129">**Een naam voor de functie opgeven**</span><span class="sxs-lookup"><span data-stu-id="9e646-129">**Name your function**</span></span> | <span data-ttu-id="9e646-130">Uniek in uw functie-app</span><span class="sxs-lookup"><span data-stu-id="9e646-130">Unique in your function app</span></span> | <span data-ttu-id="9e646-131">Naam van deze door een wachtrij geactiveerde functie.</span><span class="sxs-lookup"><span data-stu-id="9e646-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="9e646-132">Klik op **Maken** om de functie te maken.</span><span class="sxs-lookup"><span data-stu-id="9e646-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="9e646-133">Vervolgens maakt u verbinding met uw Azure Storage-account en maakt u de opslagwachtrij **myqueue-items**.</span><span class="sxs-lookup"><span data-stu-id="9e646-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="9e646-134">De wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="9e646-134">Create the queue</span></span>

1. <span data-ttu-id="9e646-135">Klik in de functie op **Integreren**, vouw **Documentatie** uit en kopieer de **Accountnaam** en de **Accountsleutel**.</span><span class="sxs-lookup"><span data-stu-id="9e646-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="9e646-136">Met deze referenties kunt u verbinding maken met het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9e646-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="9e646-137">Als u uw opslagaccount al hebt verbonden, gaat u naar stap 4.</span><span class="sxs-lookup"><span data-stu-id="9e646-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![Haal de verbindingsreferenties voor het opslagaccount op.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="9e646-139">v</span><span class="sxs-lookup"><span data-stu-id="9e646-139">v</span></span>

1. <span data-ttu-id="9e646-140">Voer het hulpprogramma [Microsoft Azure Storage Explorer](http://storageexplorer.com/) uit, klik op het verbindingspictogram aan de linkerkant, kies **Een opslagaccountnaam en -sleutel gebruiken** en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9e646-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Voer het hulpprogramma Storage Account Explorer uit.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="9e646-142">Voer de **Accountnaam** en de **Accountsleutel** van stap 1 in. Klik op **Volgende** en vervolgens op **Verbinding maken**.</span><span class="sxs-lookup"><span data-stu-id="9e646-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Voer de opslagreferenties in en maak verbinding.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="9e646-144">Vouw het gekoppelde opslagaccount uit. Klik met de rechtermuisknop op **Wachtrijen**, klik op **Wachtrij maken**, typ `myqueue-items` en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="9e646-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Maak een opslagwachtrij.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="9e646-146">Nu u een opslagwachtrij hebt, kunt u de functie testen door een bericht toe te voegen aan de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="9e646-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="9e646-147">De functie testen</span><span class="sxs-lookup"><span data-stu-id="9e646-147">Test the function</span></span>

1. <span data-ttu-id="9e646-148">Blader in Azure Portal naar de functie, vouw de **Logboeken** onderaan de pagina uit en zorg ervoor dat logboekstreaming niet wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="9e646-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="9e646-149">Vouw in Storage Explorer uw opslagaccount, **Wachtrijen** en **myqueue-items** uit en klik vervolgens op **Bericht toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9e646-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Voeg een bericht toe aan de wachtrij.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="9e646-151">Typ uw "Hallo wereld"-</span><span class="sxs-lookup"><span data-stu-id="9e646-151">Type your "Hello World!"</span></span> <span data-ttu-id="9e646-152">bericht in **Berichttekst** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e646-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="9e646-153">Wacht een paar seconden en ga vervolgens terug naar de functielogboeken en controleer of het nieuwe bericht is gelezen.</span><span class="sxs-lookup"><span data-stu-id="9e646-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![Bekijk het bericht in de logboeken.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="9e646-155">Klik in Storage Explorer op **Vernieuwen** en controleer of het bericht is verwerkt en niet langer in de wachtrij staat.</span><span class="sxs-lookup"><span data-stu-id="9e646-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9e646-156">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="9e646-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="9e646-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e646-157">Next steps</span></span>

<span data-ttu-id="9e646-158">U hebt een functie gemaakt die wordt uitgevoerd wanneer er een bericht wordt toegevoegd aan een opslagwachtrij.</span><span class="sxs-lookup"><span data-stu-id="9e646-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="9e646-159">Zie [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md) (Opslagwachtrijbindingen van Azure Functions) voor meer informatie over activeringen van Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="9e646-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>