---
title: een functie in Azure geactiveerd door Wachtrijberichten aaaCreate | Microsoft Docs
description: Gebruik Azure Functions toocreate een zonder server-functie die wordt opgeroepen door een berichten verzonden tooan Azure Storage-wachtrij.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a><span data-ttu-id="045e4-103">Berichten tooan Azure Storage-wachtrij met behulp van functies toevoegen</span><span class="sxs-lookup"><span data-stu-id="045e4-103">Add messages tooan Azure Storage queue using Functions</span></span>

<span data-ttu-id="045e4-104">Azure Functions geeft invoer en uitvoer bindingen u een declaratieve manier tooconnect tooexternal servicegegevens uit een functie.</span><span class="sxs-lookup"><span data-stu-id="045e4-104">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="045e4-105">In dit onderwerp informatie over hoe een bestaande functie door toe te voegen die binding uitvoer tooupdate verzendt berichten tooAzure Queue storage.</span><span class="sxs-lookup"><span data-stu-id="045e4-105">In this topic, learn how tooupdate an existing function by adding an output binding that sends messages tooAzure Queue storage.</span></span>  

![Bericht wordt weergegeven in Logboeken Hallo.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a><span data-ttu-id="045e4-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="045e4-107">Prerequisites</span></span> 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* <span data-ttu-id="045e4-108">Hallo installeren [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="045e4-108">Install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <span data-ttu-id="045e4-109"><a name="add-binding"></a>Een uitvoerbinding toevoegen</span><span class="sxs-lookup"><span data-stu-id="045e4-109"><a name="add-binding"></a>Add an output binding</span></span>
 
1. <span data-ttu-id="045e4-110">Vouw de functie-app en de functie uit.</span><span class="sxs-lookup"><span data-stu-id="045e4-110">Expand both your function app and your function.</span></span>

2. <span data-ttu-id="045e4-111">Selecteer **integreren** en **+ nieuw uitvoer**, en kies vervolgens **Azure Queue storage** en kies **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="045e4-111">Select **Integrate** and **+ New output**, then choose **Azure Queue storage** and choose **Select**.</span></span>
    
    ![Een wachtrij uitvoer binding tooa opslagfunctie toevoegen in hello Azure-portal.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="045e4-113">Hallo-instellingen zoals opgegeven in de tabel hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="045e4-113">Use hello settings as specified in hello table:</span></span> 

    ![Een wachtrij uitvoer binding tooa opslagfunctie toevoegen in hello Azure-portal.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="045e4-115">Instelling</span><span class="sxs-lookup"><span data-stu-id="045e4-115">Setting</span></span>      |  <span data-ttu-id="045e4-116">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="045e4-116">Suggested value</span></span>   | <span data-ttu-id="045e4-117">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="045e4-117">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="045e4-118">**Wachtrijnaam**</span><span class="sxs-lookup"><span data-stu-id="045e4-118">**Queue name**</span></span>   | <span data-ttu-id="045e4-119">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="045e4-119">myqueue-items</span></span>    | <span data-ttu-id="045e4-120">Hallo-naam van Hallo wachtrij tooconnect tooin uw Storage-account.</span><span class="sxs-lookup"><span data-stu-id="045e4-120">hello name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="045e4-121">**Opslagaccountverbinding**</span><span class="sxs-lookup"><span data-stu-id="045e4-121">**Storage account connection**</span></span> | <span data-ttu-id="045e4-122">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="045e4-122">AzureWebJobStorage</span></span> | <span data-ttu-id="045e4-123">U kunt Hallo storage-account verbinding is al wordt gebruikt door de functie-app gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="045e4-123">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="045e4-124">**Naam van de berichtparameter**</span><span class="sxs-lookup"><span data-stu-id="045e4-124">**Message parameter name**</span></span> | <span data-ttu-id="045e4-125">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="045e4-125">outputQueueItem</span></span> | <span data-ttu-id="045e4-126">Hallo-naam van de binding uitvoerparameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="045e4-126">hello name of hello output binding parameter.</span></span> | 

4. <span data-ttu-id="045e4-127">Klik op **opslaan** tooadd Hallo binding.</span><span class="sxs-lookup"><span data-stu-id="045e4-127">Click **Save** tooadd hello binding.</span></span>
 
<span data-ttu-id="045e4-128">Nu dat u een uitvoer-binding die is gedefinieerd hebt, moet u tooupdate Hallo code toouse Hallo binding tooadd berichten tooa wachtrij.</span><span class="sxs-lookup"><span data-stu-id="045e4-128">Now that you have an output binding defined, you need tooupdate hello code toouse hello binding tooadd messages tooa queue.</span></span>  

## <a name="update-hello-function-code"></a><span data-ttu-id="045e4-129">Hallo functiecode bijwerken</span><span class="sxs-lookup"><span data-stu-id="045e4-129">Update hello function code</span></span>

1. <span data-ttu-id="045e4-130">Selecteer uw functiecode toodisplay Hallo functie in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="045e4-130">Select your function toodisplay hello function code in hello editor.</span></span> 

2. <span data-ttu-id="045e4-131">Voor een C#-functie, werkt de functiedefinitie van de als volgt tooadd hello **outputQueueItem** storage binding-parameter.</span><span class="sxs-lookup"><span data-stu-id="045e4-131">For a C# function, update your function definition as follows tooadd hello **outputQueueItem** storage binding parameter.</span></span> <span data-ttu-id="045e4-132">Sla deze stap over voor een JavaScript-functie.</span><span class="sxs-lookup"><span data-stu-id="045e4-132">Skip this step for a JavaScript function.</span></span>

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. <span data-ttu-id="045e4-133">Hallo volgen op code toohello functie vlak voordat het Hallo-methode retourneert toevoegen.</span><span class="sxs-lookup"><span data-stu-id="045e4-133">Add hello following code toohello function just before hello method returns.</span></span> <span data-ttu-id="045e4-134">Hallo relevante codefragment voor Hallo taal van de functie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="045e4-134">Use hello appropriate snippet for hello language of your function.</span></span>

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. <span data-ttu-id="045e4-135">Selecteer **opslaan** toosave wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="045e4-135">Select **Save** toosave changes.</span></span>

<span data-ttu-id="045e4-136">Hallo-waarde doorgegeven toohello HTTP-trigger is opgenomen in een toegevoegde toohello berichtenwachtrij.</span><span class="sxs-lookup"><span data-stu-id="045e4-136">hello value passed toohello HTTP trigger is included in a message added toohello queue.</span></span>
 
## <a name="test-hello-function"></a><span data-ttu-id="045e4-137">Hallo functie testen</span><span class="sxs-lookup"><span data-stu-id="045e4-137">Test hello function</span></span> 

1. <span data-ttu-id="045e4-138">Nadat het Hallo codewijzigingen zijn opgeslagen, selecteert u **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="045e4-138">After hello code changes are saved, select **Run**.</span></span> 

    ![Een wachtrij uitvoer binding tooa opslagfunctie toevoegen in hello Azure-portal.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. <span data-ttu-id="045e4-140">Controleer Hallo logboeken toomake ervoor Hallo-functie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="045e4-140">Check hello logs toomake sure that hello function succeeded.</span></span> <span data-ttu-id="045e4-141">Een nieuwe wachtrij met de naam **outqueue** in uw opslagaccount is gemaakt door Hallo runtime van Functions wanneer Hallo uitvoer binding voor het eerst is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="045e4-141">A new queue named **outqueue** is created in your Storage account by hello Functions runtime when hello output binding is first used.</span></span>

<span data-ttu-id="045e4-142">Vervolgens kunt u tooyour storage account tooverify Hallo nieuwe wachtrij en het Hallo-bericht dat u tooit toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="045e4-142">Next, you can connect tooyour storage account tooverify hello new queue and hello message you added tooit.</span></span> 

## <a name="connect-toohello-queue"></a><span data-ttu-id="045e4-143">Verbinding maken met toohello wachtrij</span><span class="sxs-lookup"><span data-stu-id="045e4-143">Connect toohello queue</span></span>

<span data-ttu-id="045e4-144">Overslaan Hallo eerste drie stappen uit als u al hebt geïnstalleerd Opslagverkenner en het opslagaccount tooyour verbonden.</span><span class="sxs-lookup"><span data-stu-id="045e4-144">Skip hello first three steps if you have already installed Storage Explorer and connected it tooyour storage account.</span></span>    

1. <span data-ttu-id="045e4-145">Kies in de functie **integreren** en nieuwe Hallo **Azure Queue storage** binding uitvoer uit en vouw vervolgens **documentatie**.</span><span class="sxs-lookup"><span data-stu-id="045e4-145">In your function, choose **Integrate** and hello new **Azure Queue storage** output binding, then expand **Documentation**.</span></span> <span data-ttu-id="045e4-146">Kopieer de **Accountnaam** en de **Accountsleutel**.</span><span class="sxs-lookup"><span data-stu-id="045e4-146">Copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="045e4-147">U gebruikt deze referenties tooconnect toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="045e4-147">You use these credentials tooconnect toohello storage account.</span></span>
 
    ![Hallo Storage-account verbindingsreferenties ophalen.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. <span data-ttu-id="045e4-149">Hallo uitvoeren [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, selecteer Hallo verbinding pictogram aan de linkerkant hello, kiest u **gebruik van een naam van het opslagaccount en de sleutel**, en selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="045e4-149">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select hello connect icon on hello left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![Hallo Account Opslagverkenner hulpprogramma uitvoeren.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. <span data-ttu-id="045e4-151">Plakken Hallo **accountnaam** en **accountsleutel** stap van 1 in hun bijbehorende velden en selecteer vervolgens **volgende**, en **Connect**.</span><span class="sxs-lookup"><span data-stu-id="045e4-151">Paste hello **Account name** and **Account key** from step 1 into their corresponding fields, then select **Next**, and **Connect**.</span></span> 
  
    ![Hallo storage-referenties te plakken en verbinding maken.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. <span data-ttu-id="045e4-153">Vouw Hallo gekoppeld opslagaccount **wachtrijen** en controleer of er een wachtrij met de naam **rapportberichten items** bestaat.</span><span class="sxs-lookup"><span data-stu-id="045e4-153">Expand hello attached storage account, expand **Queues** and verify that a queue named **myqueue-items** exists.</span></span> <span data-ttu-id="045e4-154">U ziet ook een bericht al in de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="045e4-154">You should also see a message already in hello queue.</span></span>  
 
    ![Maak een opslagwachtrij.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="045e4-156">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="045e4-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="045e4-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="045e4-157">Next steps</span></span>

<span data-ttu-id="045e4-158">U kunt een bestaande functie voor uitvoer binding tooan hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="045e4-158">You have added an output binding tooan existing function.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="045e4-159">Zie voor meer informatie over opslag voor binding tooQueue [bindingen van Azure Functions Storage wachtrij](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="045e4-159">For more information about binding tooQueue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 



