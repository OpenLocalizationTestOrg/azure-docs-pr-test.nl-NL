---
title: aaaMonitoring Azure Functions | Microsoft Docs
description: Meer informatie over hoe toomonitor uw Azure-functies.
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
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="65e00-104">Azure Functions controleren</span><span class="sxs-lookup"><span data-stu-id="65e00-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="65e00-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="65e00-105">Overview</span></span> 


<span data-ttu-id="65e00-106">Hallo **Monitor** tabblad voor elke functie u tooreview kunt elke uitvoering van een functie.</span><span class="sxs-lookup"><span data-stu-id="65e00-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Tabblad van Azure Functions-monitor](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="65e00-108">Een uitvoering klikken kunt u tooreview Hallo duur, invoergegevens, fouten en bijbehorende logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="65e00-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="65e00-109">Dit is handig voor foutopsporing en prestaties afstemmen van uw functies.</span><span class="sxs-lookup"><span data-stu-id="65e00-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="65e00-110">Wanneer u Hallo [verbruik die als host fungeert voor plan](functions-overview.md#pricing) voor Azure Functions Hallo **bewaking** tegel in overzichtsblade Hallo-functie-App niet alle gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="65e00-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="65e00-111">Dit is omdat dynamisch schaalbaar en beheert de compute-exemplaren voor u, zodat deze metrische gegevens niet op een plan verbruik zinvolle zijn Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="65e00-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="65e00-112">toomonitor hello gebruik van de functie-Apps, moet u in plaats daarvan gebruiken Hallo richtlijnen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="65e00-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="65e00-113">Hallo-schermopname na toont een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="65e00-113">hello following screen-shot shows an example:</span></span>
> 
> ![Bewaking op de belangrijkste resourceblade Hallo](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="65e00-115">Realtime-controle</span><span class="sxs-lookup"><span data-stu-id="65e00-115">Real-time monitoring</span></span>

<span data-ttu-id="65e00-116">Realtime-controle is beschikbaar door te klikken op **stream live gebeurtenis** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="65e00-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Live gebeurtenis stroom optie voor tabblad Hallo-monitor](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="65e00-118">wordt in een nieuw browsertabblad een diagram worden weergegeven aan Hallo live gebeurtenisstroom zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="65e00-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Voorbeeld van de stream Live gebeurtenis](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="65e00-120">Er is een bekend probleem dat ertoe leiden uw gegevens toofail toobe ingevuld dat kan.</span><span class="sxs-lookup"><span data-stu-id="65e00-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="65e00-121">Als u dit ondervindt, moet u mogelijk tooclose Hallo browser tabblad met Hallo live gebeurtenisstroom en klik vervolgens op **stream live gebeurtenis** opnieuw tooallow het tooproperly de gebeurtenisgegevens stroom vullen.</span><span class="sxs-lookup"><span data-stu-id="65e00-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="65e00-122">Hallo live gebeurtenisstroom wordt graph Hallo statistieken voor uw functie te volgen:</span><span class="sxs-lookup"><span data-stu-id="65e00-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="65e00-123">Uitvoeringen per seconde is gestart</span><span class="sxs-lookup"><span data-stu-id="65e00-123">Executions started per second</span></span>
* <span data-ttu-id="65e00-124">Uitvoeringen per seconde worden voltooid</span><span class="sxs-lookup"><span data-stu-id="65e00-124">Executions completed per second</span></span>
* <span data-ttu-id="65e00-125">Uitvoeringen mislukte per seconde</span><span class="sxs-lookup"><span data-stu-id="65e00-125">Executions failed per second</span></span>
* <span data-ttu-id="65e00-126">Gemiddelde uitvoeringstijd in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="65e00-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="65e00-127">Deze statistieken zijn realtime maar werkelijke grafieken van uitvoeringsgegevens Hallo Hallo mogelijk van de latentie van ongeveer 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="65e00-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="65e00-128">Bewaking van logboekbestanden vanaf een opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="65e00-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="65e00-129">U kunt logboek bestanden tooa opdrachtregel sessie op een lokaal werkstation met hello Azure-opdrachtregelinterface (CLI) of PowerShell streamen.</span><span class="sxs-lookup"><span data-stu-id="65e00-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="65e00-130">Bewaking van de functie app-logboekbestanden Hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65e00-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="65e00-131">tooget gestart, [hello Azure CLI installeren](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="65e00-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="65e00-132">Meld u aan bij uw Azure-account met de volgende Hallo opdracht of een van de andere opties behandeld in, Hallo [tooAzure van hello Azure CLI aanmelden](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="65e00-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="65e00-133">Gebruik Hallo volgende opdracht tooenable Azure CLI Service Management (ASM) modus:.</span><span class="sxs-lookup"><span data-stu-id="65e00-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="65e00-134">Als u meerdere abonnementen hebt, gebruik Hallo opdrachten toolist na uw abonnementen en set Hallo huidige abonnement toohello abonnement dat functie-app bevat.</span><span class="sxs-lookup"><span data-stu-id="65e00-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="65e00-135">Hallo wordt volgende opdracht stream Hallo logboekbestanden van de functie app toohello vanaf de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="65e00-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="65e00-136">Bewaking van de functie app-logboekbestanden met PowerShell</span><span class="sxs-lookup"><span data-stu-id="65e00-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="65e00-137">tooget gestart, [Azure PowerShell installeren en configureren](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65e00-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="65e00-138">Uw Azure-account toevoegen door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="65e00-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="65e00-139">Als u meerdere abonnementen hebt, kunt u deze weergeven met de naam met volgende opdracht toosee als het juiste abonnement is geselecteerd Hallo Hallo op basis van hello `IsCurrent` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="65e00-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="65e00-140">Als u tooset Hallo actief abonnement toohello met de functie-app moet, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="65e00-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="65e00-141">Stroom Hallo logboeken tooyour PowerShell-sessie met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="65e00-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="65e00-142">Voor meer informatie raadpleegt u te[hoe: logboeken voor web-apps Stream](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="65e00-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="65e00-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65e00-143">Next steps</span></span>
<span data-ttu-id="65e00-144">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="65e00-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="65e00-145">Een functie testen</span><span class="sxs-lookup"><span data-stu-id="65e00-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="65e00-146">Een functie schalen</span><span class="sxs-lookup"><span data-stu-id="65e00-146">Scale a function</span></span>](functions-scale.md)

