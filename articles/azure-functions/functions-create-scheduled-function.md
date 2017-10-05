---
title: Een functie maken in Azure die volgens een schema wordt uitgevoerd | Microsoft Docs
description: Ontdek hoe u in Azure een functie maakt die wordt uitgevoerd op basis van een schema dat u definieert.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="a2df8-103">Maak een functie in Azure die wordt geactiveerd door een timer</span><span class="sxs-lookup"><span data-stu-id="a2df8-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="a2df8-104">Ontdek hoe u Azure Functions gebruikt om een functie te maken die wordt uitgevoerd op basis van een schema dat u definieert.</span><span class="sxs-lookup"><span data-stu-id="a2df8-104">Learn how to use Azure Functions to create a function that runs based a schedule that you define.</span></span>

![Functie-app maken in Azure Portal](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="a2df8-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a2df8-106">Prerequisites</span></span>

<span data-ttu-id="a2df8-107">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="a2df8-107">To complete this tutorial:</span></span>

+ <span data-ttu-id="a2df8-108">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="a2df8-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="a2df8-109">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="a2df8-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="a2df8-111">Vervolgens maakt u een functie in de nieuwe functie-app.</span><span class="sxs-lookup"><span data-stu-id="a2df8-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="a2df8-112">Een door een timer geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="a2df8-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="a2df8-113">Vouw de functie-app uit en klik op de knop **+** naast **Functies**.</span><span class="sxs-lookup"><span data-stu-id="a2df8-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="a2df8-114">Als dit de eerste functie in de functie-app is, selecteert u **Aangepaste functie**.</span><span class="sxs-lookup"><span data-stu-id="a2df8-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="a2df8-115">U ziet nu de volledige set het functiesjablonen.</span><span class="sxs-lookup"><span data-stu-id="a2df8-115">This displays the complete set of function templates.</span></span>

    ![De Quick Start-pagina van Functions in Azure Portal](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="a2df8-117">Selecteer de sjabloon **TimerTrigger** voor de gewenste taal.</span><span class="sxs-lookup"><span data-stu-id="a2df8-117">Select the **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="a2df8-118">Gebruik vervolgens de instellingen zoals opgegeven in de tabel:</span><span class="sxs-lookup"><span data-stu-id="a2df8-118">Then use the settings as specified in the table:</span></span>

    ![Maak een door een timer geactiveerde functie in Azure Portal.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="a2df8-120">Instelling</span><span class="sxs-lookup"><span data-stu-id="a2df8-120">Setting</span></span> | <span data-ttu-id="a2df8-121">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="a2df8-121">Suggested value</span></span> | <span data-ttu-id="a2df8-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a2df8-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="a2df8-123">**Een naam voor de functie opgeven**</span><span class="sxs-lookup"><span data-stu-id="a2df8-123">**Name your function**</span></span> | <span data-ttu-id="a2df8-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="a2df8-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="a2df8-125">Bepaalt de naam van de door de timer geactiveerde functie.</span><span class="sxs-lookup"><span data-stu-id="a2df8-125">Defines the name of your timer triggered function.</span></span> |
    | <span data-ttu-id="a2df8-126">**[Planning](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="a2df8-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="a2df8-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="a2df8-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="a2df8-128">Een [CRON-expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression) met zes velden aan de hand waarvan uw functie elke minuut wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2df8-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function to run every minute.</span></span> |

2. <span data-ttu-id="a2df8-129">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a2df8-129">Click **Create**.</span></span> <span data-ttu-id="a2df8-130">Er wordt een functie gemaakt in uw gekozen taal en deze wordt elke minuut uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2df8-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="a2df8-131">Controleer of dit correct wordt uitgevoerd door de traceringsinformatie die naar logboeken wordt geschreven te bekijken.</span><span class="sxs-lookup"><span data-stu-id="a2df8-131">Verify execution by viewing trace information written to the logs.</span></span>

    ![De viewer voor functielogboeken in Azure Portal.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="a2df8-133">U kunt het schema voor de functie wijzigen zodat deze minder vaak wordt uitgevoerd (bijvoorbeeld één keer per uur).</span><span class="sxs-lookup"><span data-stu-id="a2df8-133">Now, you can change the function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-the-timer-schedule"></a><span data-ttu-id="a2df8-134">Het timerschema bijwerken</span><span class="sxs-lookup"><span data-stu-id="a2df8-134">Update the timer schedule</span></span>

1. <span data-ttu-id="a2df8-135">Vouw de functie uit en klik op **Integreren**.</span><span class="sxs-lookup"><span data-stu-id="a2df8-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="a2df8-136">Dit is waar u de invoer- en uitvoerbindingen voor de functie definieert en het schema instelt.</span><span class="sxs-lookup"><span data-stu-id="a2df8-136">This is where you define input and output bindings for your function and also set the schedule.</span></span> 

2. <span data-ttu-id="a2df8-137">Voer voor de nieuwe **Planning** een waarde van `0 0 */1 * * *` in en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a2df8-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Het timerschema voor het bijwerken van functies in Azure Portal.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="a2df8-139">U hebt nu een functie die één keer per uur wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2df8-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="a2df8-140">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="a2df8-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="a2df8-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2df8-141">Next steps</span></span>

<span data-ttu-id="a2df8-142">U hebt een functie gemaakt die wordt uitgevoerd op basis van een schema.</span><span class="sxs-lookup"><span data-stu-id="a2df8-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="a2df8-143">Zie voor meer informatie over timeractiveringen [Schedule code execution with Azure Functions](functions-bindings-timer.md) (Code-uitvoering plannen met Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="a2df8-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>