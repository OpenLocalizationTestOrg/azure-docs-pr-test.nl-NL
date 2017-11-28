---
title: aaaCreate een functie die wordt uitgevoerd volgens een schema in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een functie in Azure die wordt uitgevoerd op basis van een planning die u definieert.
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
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="7f910-103">Maak een functie in Azure die wordt geactiveerd door een timer</span><span class="sxs-lookup"><span data-stu-id="7f910-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="7f910-104">Meer informatie over hoe toouse Azure Functions toocreate een functie die wordt uitgevoerd op basis van een planning die u definieert.</span><span class="sxs-lookup"><span data-stu-id="7f910-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Functie-app maken in hello Azure-portal](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="7f910-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7f910-106">Prerequisites</span></span>

<span data-ttu-id="7f910-107">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="7f910-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="7f910-108">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="7f910-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="7f910-109">Een Azure-functie-app maken</span><span class="sxs-lookup"><span data-stu-id="7f910-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![De functie-app is gemaakt.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="7f910-111">Vervolgens maakt u een functie in nieuwe Hallo-functie-app.</span><span class="sxs-lookup"><span data-stu-id="7f910-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="7f910-112">Een door een timer geactiveerde functie maken</span><span class="sxs-lookup"><span data-stu-id="7f910-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="7f910-113">Vouw de functie-app en klik op Hallo  **+**  knop naast te**functies**.</span><span class="sxs-lookup"><span data-stu-id="7f910-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="7f910-114">Als dit eerste functie in uw app functie hello, selecteer **aangepaste functie**.</span><span class="sxs-lookup"><span data-stu-id="7f910-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="7f910-115">De volledige set Hallo van functie-sjablonen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f910-115">This displays hello complete set of function templates.</span></span>

    ![Functies Quick Start-pagina in hello Azure-portal](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="7f910-117">Selecteer Hallo **TimerTrigger** sjabloon voor de gewenste taal.</span><span class="sxs-lookup"><span data-stu-id="7f910-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="7f910-118">Gebruik vervolgens Hallo instellingen zoals opgegeven in de tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="7f910-118">Then use hello settings as specified in hello table:</span></span>

    ![Maak een geactiveerd door de timerfunctie in hello Azure-portal.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="7f910-120">Instelling</span><span class="sxs-lookup"><span data-stu-id="7f910-120">Setting</span></span> | <span data-ttu-id="7f910-121">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="7f910-121">Suggested value</span></span> | <span data-ttu-id="7f910-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7f910-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="7f910-123">**Een naam voor de functie opgeven**</span><span class="sxs-lookup"><span data-stu-id="7f910-123">**Name your function**</span></span> | <span data-ttu-id="7f910-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="7f910-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="7f910-125">Hallo-naam van de timerfunctie geactiveerd definieert.</span><span class="sxs-lookup"><span data-stu-id="7f910-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="7f910-126">**[Planning](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="7f910-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="7f910-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="7f910-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="7f910-128">Een veld zes [CRON expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression) die uw toorun functie plant u elke minuut.</span><span class="sxs-lookup"><span data-stu-id="7f910-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="7f910-129">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7f910-129">Click **Create**.</span></span> <span data-ttu-id="7f910-130">Er wordt een functie gemaakt in uw gekozen taal en deze wordt elke minuut uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f910-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="7f910-131">Controleer of u kan worden uitgevoerd door toohello Logboeken geschreven traceringsinformatie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7f910-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![Functies melden viewer hello Azure-portal.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="7f910-133">U kunt nu de planning van de functie Hallo wijzigen zodat deze minder vaak zoals één keer per uur wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f910-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="7f910-134">Hallo timer schema bijwerken</span><span class="sxs-lookup"><span data-stu-id="7f910-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="7f910-135">Vouw de functie uit en klik op **Integreren**.</span><span class="sxs-lookup"><span data-stu-id="7f910-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="7f910-136">Dit is waar u definieert u welke invoer en uitvoer van de bindingen voor de functie en ook Hallo-planning instellen.</span><span class="sxs-lookup"><span data-stu-id="7f910-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="7f910-137">Voer voor de nieuwe **Planning** een waarde van `0 0 */1 * * *` in en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7f910-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Functies bijwerken in hello Azure-portal timer planning.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="7f910-139">U hebt nu een functie die één keer per uur wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f910-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="7f910-140">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="7f910-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="7f910-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f910-141">Next steps</span></span>

<span data-ttu-id="7f910-142">U hebt een functie gemaakt die wordt uitgevoerd op basis van een schema.</span><span class="sxs-lookup"><span data-stu-id="7f910-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="7f910-143">Zie voor meer informatie over timeractiveringen [Schedule code execution with Azure Functions](functions-bindings-timer.md) (Code-uitvoering plannen met Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="7f910-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>