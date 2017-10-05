---
title: Bewaking van Azure Functions | Microsoft Docs
description: Informatie over het bewaken van uw Azure-functies.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="0aeea-104">Azure Functions controleren</span><span class="sxs-lookup"><span data-stu-id="0aeea-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="0aeea-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0aeea-105">Overview</span></span> 


<span data-ttu-id="0aeea-106">De **Monitor** tabblad voor elke functie u deze kunt kunt bekijken van elke uitvoering van een functie.</span><span class="sxs-lookup"><span data-stu-id="0aeea-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Tabblad van Azure Functions-monitor](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="0aeea-108">Op uitvoering van een, kunt u deze kunt bekijken van de duur van de invoergegevens, fouten en bijbehorende logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="0aeea-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="0aeea-109">Dit is handig voor foutopsporing en prestaties afstemmen van uw functies.</span><span class="sxs-lookup"><span data-stu-id="0aeea-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="0aeea-110">Wanneer u de [verbruik die als host fungeert voor plan](functions-overview.md#pricing) voor Azure Functions, de **bewaking** tegel in de overzichtsblade van functie-App niet alle gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0aeea-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="0aeea-111">Dit is omdat het platform dynamisch schaalbaar en beheert de compute-exemplaren voor u, zodat deze metrische gegevens niet op een plan verbruik zinvolle zijn.</span><span class="sxs-lookup"><span data-stu-id="0aeea-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="0aeea-112">Als u wilt het gebruik van uw Apps functie bewaken, moet u in plaats daarvan de instructies in dit artikel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0aeea-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="0aeea-113">De volgende Schermafbeelding toont een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0aeea-113">The following screen-shot shows an example:</span></span>
> 
> ![Bewaking op de belangrijkste resourceblade](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="0aeea-115">Realtime-controle</span><span class="sxs-lookup"><span data-stu-id="0aeea-115">Real-time monitoring</span></span>

<span data-ttu-id="0aeea-116">Realtime-controle is beschikbaar door te klikken op **stream live gebeurtenis** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0aeea-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Live gebeurtenis stroom optie voor het tabblad monitor](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="0aeea-118">Wordt in een nieuw browsertabblad een diagram worden weergegeven aan de stroom live gebeurtenissen zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0aeea-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Voorbeeld van de stream Live gebeurtenis](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="0aeea-120">Er is een bekend probleem dat ertoe leiden uw gegevens dat kan niet kunnen worden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="0aeea-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="0aeea-121">Als dit zich voordoet, moet u mogelijk het browsertabblad met de stream live gebeurtenis sluiten en klik vervolgens op **stream live gebeurtenis** opnieuw toe te staan dat uw stream gebeurtenisgegevens correct te vullen.</span><span class="sxs-lookup"><span data-stu-id="0aeea-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="0aeea-122">De stream live gebeurtenis wordt de volgende statistieken voor de functie grafiek:</span><span class="sxs-lookup"><span data-stu-id="0aeea-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="0aeea-123">Uitvoeringen per seconde is gestart</span><span class="sxs-lookup"><span data-stu-id="0aeea-123">Executions started per second</span></span>
* <span data-ttu-id="0aeea-124">Uitvoeringen per seconde worden voltooid</span><span class="sxs-lookup"><span data-stu-id="0aeea-124">Executions completed per second</span></span>
* <span data-ttu-id="0aeea-125">Uitvoeringen mislukte per seconde</span><span class="sxs-lookup"><span data-stu-id="0aeea-125">Executions failed per second</span></span>
* <span data-ttu-id="0aeea-126">Gemiddelde uitvoeringstijd in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="0aeea-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="0aeea-127">Deze statistieken zijn realtime maar de werkelijke grafieken van de uitvoering van gegevens mogelijk van de latentie van ongeveer 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="0aeea-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="0aeea-128">Bewaking van logboekbestanden vanaf een opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="0aeea-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="0aeea-129">U kunt logboekbestanden met een opdrachtregel-sessie op een lokaal werkstation met de Azure-opdrachtregelinterface (CLI) of PowerShell streamen.</span><span class="sxs-lookup"><span data-stu-id="0aeea-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="0aeea-130">Bewaking van de functie app-logboekbestanden met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0aeea-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="0aeea-131">Aan de slag [Azure CLI installeren](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="0aeea-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="0aeea-132">Meld u aan bij uw Azure-account met de volgende opdracht of een van de andere opties behandeld in, [aanmelden bij Azure met Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0aeea-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="0aeea-133">Gebruik de volgende opdracht om te kunnen inschakelen voor Azure CLI Service Management (ASM):.</span><span class="sxs-lookup"><span data-stu-id="0aeea-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="0aeea-134">Als u meerdere abonnementen hebt, gebruikt u de volgende opdrachten om te lijst van uw abonnementen en het huidige abonnement aan het abonnement dat functie-app bevat.</span><span class="sxs-lookup"><span data-stu-id="0aeea-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="0aeea-135">De volgende opdracht wordt de logboekbestanden van uw app functie aan de opdrachtregel stream:</span><span class="sxs-lookup"><span data-stu-id="0aeea-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="0aeea-136">Bewaking van de functie app-logboekbestanden met PowerShell</span><span class="sxs-lookup"><span data-stu-id="0aeea-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="0aeea-137">Aan de slag [Azure PowerShell installeren en configureren](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0aeea-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="0aeea-138">Uw Azure-account toevoegen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0aeea-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="0aeea-139">Als u meerdere abonnementen hebt, kunt u deze met de naam met de volgende opdracht om te zien of het juiste abonnement de momenteel geselecteerde op basis van vermelden `IsCurrent` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="0aeea-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="0aeea-140">Als u de actief abonnement met de functie-app met instellen moet, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0aeea-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="0aeea-141">Stream de logboeken naar uw PowerShell-sessie met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0aeea-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="0aeea-142">Raadpleeg voor meer informatie [hoe: logboeken voor web-apps Stream](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="0aeea-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0aeea-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0aeea-143">Next steps</span></span>
<span data-ttu-id="0aeea-144">Zie de volgende bronnen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="0aeea-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="0aeea-145">Een functie testen</span><span class="sxs-lookup"><span data-stu-id="0aeea-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="0aeea-146">Een functie schalen</span><span class="sxs-lookup"><span data-stu-id="0aeea-146">Scale a function</span></span>](functions-scale.md)

