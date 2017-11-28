---
title: aaaHow toouse Azure queue storage met Hallo WebJobs SDK
description: Meer informatie over hoe toouse Azure queue storage Hello WebJobs SDK. Maken en verwijderen van wachtrijen; invoegen, inspecteren, ophalen en verwijderen van Wachtrijberichten en meer.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="c1d8a-104">Hoe toouse Azure queue storage Hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="c1d8a-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="c1d8a-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c1d8a-105">Overview</span></span>
<span data-ttu-id="c1d8a-106">Deze handleiding bevat C#-codevoorbeelden die laten zien hoe toouse hello Azure WebJobs SDK versie 1.x Hello Azure queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="c1d8a-107">Hallo handleiding wordt ervan uitgegaan dat u weet [hoe een webtaak-project in Visual Studio met verbinding toocreate dat punt tooyour storage-account tekenreeksen](websites-dotnet-webjobs-sdk-get-started.md) of te[meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="c1d8a-108">Hallo codefragmenten de meeste functies, alleen weergeven niet code die wordt gemaakt van Hallo Hallo `JobHost` object zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="c1d8a-109">Hallo handleiding bevat de volgende onderwerpen Hallo:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="c1d8a-110">Hoe tootrigger een functie wanneer er een wachtrijbericht wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="c1d8a-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="c1d8a-111">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-111">String queue messages</span></span>
  * <span data-ttu-id="c1d8a-112">POCO-berichtenwachtrij-berichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-112">POCO queue messages</span></span>
  * <span data-ttu-id="c1d8a-113">Async-functies</span><span class="sxs-lookup"><span data-stu-id="c1d8a-113">Async functions</span></span>
  * <span data-ttu-id="c1d8a-114">Typen Hallo QueueTrigger kenmerk werkt met</span><span class="sxs-lookup"><span data-stu-id="c1d8a-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="c1d8a-115">Polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="c1d8a-115">Polling algorithm</span></span>
  * <span data-ttu-id="c1d8a-116">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="c1d8a-116">Multiple instances</span></span>
  * <span data-ttu-id="c1d8a-117">Parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="c1d8a-117">Parallel execution</span></span>
  * <span data-ttu-id="c1d8a-118">Wachtrij of wachtrij bericht metagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="c1d8a-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="c1d8a-119">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-119">Graceful shutdown</span></span>
* [<span data-ttu-id="c1d8a-120">Hoe een wachtrij toocreate bericht tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="c1d8a-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="c1d8a-121">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-121">String queue messages</span></span>
  * <span data-ttu-id="c1d8a-122">POCO-berichtenwachtrij-berichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-122">POCO queue messages</span></span>
  * <span data-ttu-id="c1d8a-123">Meerdere berichten maken of in een async-functies</span><span class="sxs-lookup"><span data-stu-id="c1d8a-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="c1d8a-124">Typen Hallo wachtrij kenmerk werkt met</span><span class="sxs-lookup"><span data-stu-id="c1d8a-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="c1d8a-125">Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="c1d8a-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="c1d8a-126">Hoe tooread en write blobs tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="c1d8a-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="c1d8a-127">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-127">String queue messages</span></span>
  * <span data-ttu-id="c1d8a-128">POCO-berichtenwachtrij-berichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-128">POCO queue messages</span></span>
  * <span data-ttu-id="c1d8a-129">Typen Hallo Blob kenmerk werkt met</span><span class="sxs-lookup"><span data-stu-id="c1d8a-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="c1d8a-130">Hoe toohandle poison berichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="c1d8a-131">Verwerken van verontreinigde berichten automatische</span><span class="sxs-lookup"><span data-stu-id="c1d8a-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="c1d8a-132">Verwerken van verontreinigde berichten handmatige</span><span class="sxs-lookup"><span data-stu-id="c1d8a-132">Manual poison message handling</span></span>
* [<span data-ttu-id="c1d8a-133">Hoe tooset configuratieopties</span><span class="sxs-lookup"><span data-stu-id="c1d8a-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="c1d8a-134">SDK-verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="c1d8a-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="c1d8a-135">QueueTrigger instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="c1d8a-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="c1d8a-136">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="c1d8a-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="c1d8a-137">Hoe een functie tootrigger handmatig</span><span class="sxs-lookup"><span data-stu-id="c1d8a-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="c1d8a-138">Hoe toowrite registreert</span><span class="sxs-lookup"><span data-stu-id="c1d8a-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="c1d8a-139">Hoe toohandle fouten en time-outs configureren</span><span class="sxs-lookup"><span data-stu-id="c1d8a-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="c1d8a-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1d8a-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="c1d8a-141"><a id="trigger"></a>Hoe tootrigger een functie wanneer er een wachtrijbericht wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="c1d8a-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="c1d8a-142">toowrite een functie die Hallo WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruikt u Hallo `QueueTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="c1d8a-143">Hallo kenmerkconstructor tekenreeksparameter een waarmee Hallo-naam van Hallo wachtrij toopoll.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="c1d8a-144">U kunt ook [Hallo wachtrijnaam dynamisch ingesteld](#config).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="c1d8a-145">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-145">String queue messages</span></span>
<span data-ttu-id="c1d8a-146">Hallo voorbeeld te volgen, Hallo wachtrij bevat een Tekenreeksbericht voor de dus `QueueTrigger` toegepaste tooa tekenreeksparameter met de naam is `logMessage` die Hallo inhoud van de wachtrij het Hallo-bericht bevat.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="c1d8a-147">Hallo functie [schrijft een logboek bericht toohello Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="c1d8a-148">Naast `string`, Hallo is mogelijk een bytematrix een `CloudQueueMessage` object of een POCO die u definieert.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c1d8a-149">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="c1d8a-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c1d8a-150">Hallo voorbeeld te volgen, wachtrij het Hallo-bericht bevat JSON voor een `BlobInformation` object waaronder een `BlobName` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="c1d8a-151">Hallo SDK deserializes automatisch Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="c1d8a-152">Hallo SDK maakt gebruik van Hallo [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize en deserialiseren van berichten.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="c1d8a-153">Als u berichten in wachtrij plaatsen in een programma dat Hallo WebJobs SDK maakt geen gebruik maakt, kunt u code zoals het volgende voorbeeld toocreate een wachtrijbericht POCO Hallo schrijven die Hallo die SDK kan worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="c1d8a-154">Async-functies</span><span class="sxs-lookup"><span data-stu-id="c1d8a-154">Async functions</span></span>
<span data-ttu-id="c1d8a-155">Hallo async-functie na [schrijft een logboek toohello Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="c1d8a-156">Async-functies kunnen duren voordat een [annulering token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), zoals weergegeven in het volgende voorbeeld die een blob kopieert Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="c1d8a-157">(Voor een uitleg van Hallo `queueTrigger` tijdelijke aanduiding, Zie Hallo [Blobs](#blobs) sectie.)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="c1d8a-158"><a id="qtattributetypes"></a>Typen Hallo QueueTrigger kenmerk werkt met</span><span class="sxs-lookup"><span data-stu-id="c1d8a-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="c1d8a-159">U kunt `QueueTrigger` Hello volgende typen:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="c1d8a-160">Een POCO-type dat geserialiseerd als JSON</span><span class="sxs-lookup"><span data-stu-id="c1d8a-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="c1d8a-161"><a id="polling"></a>Polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="c1d8a-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="c1d8a-162">Hallo SDK implementeert een willekeurige exponentiële back-off algoritme tooreduce Hallo effect van niet-actieve wachtrij polling op de opslagkosten voor transactie.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="c1d8a-163">Wanneer een bericht is gevonden, Hallo SDK Wacht twee seconden en wordt er gecontroleerd of een ander bericht; Wanneer er geen bericht is gevonden wacht ongeveer vier seconden alvorens het opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="c1d8a-164">Na meerdere mislukte pogingen tooget een wachtrijbericht, wachttijd Hallo tooincrease voortgezet totdat het Hallo maximale wachttijd, bereikt welke standaardwaarden tooone minuut.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="c1d8a-165">[Hallo maximale wachttijd is configureerbaar](#config).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="c1d8a-166"><a id="instances"></a>Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="c1d8a-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="c1d8a-167">Als uw web-app wordt uitgevoerd op meerdere exemplaren, een doorlopende webtaak wordt uitgevoerd op elke computer en elke machine wordt gewacht op triggers en probeert toorun functies.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="c1d8a-168">Hallo WebJobs SDK wachtrij trigger automatisch wordt voorkomen dat een functie verwerken van een wachtrijbericht meerdere keren; functies hoeft geen toobe toobe idempotent geschreven.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="c1d8a-169">Echter, als u wilt dat tooensure dat slechts één exemplaar van een functie wordt uitgevoerd zelfs als er meerdere exemplaren van Hallo host web-app, kunt u Hallo `Singleton` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="c1d8a-170"><a id="parallel"></a>Parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="c1d8a-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="c1d8a-171">Als er meerdere functies luistert naar verschillende wachtrijen, wordt Hallo SDK aangeroepen ze parallel wanneer berichten tegelijkertijd worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="c1d8a-172">Hallo geldt ook wanneer meerdere berichten worden ontvangen voor een enkele wachtrij.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="c1d8a-173">Standaard Hallo SDK een batch van 16 Wachtrijberichten tegelijk opgehaald en wordt uitgevoerd Hallo-functie die parallel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="c1d8a-174">[Hallo batchgrootte is configureerbaar](#config).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="c1d8a-175">Bij het ophalen van Hallo nummer wordt verwerkt omlaag toohalf van batchgrootte hello, hello SDK opgehaald van een andere batch- en begint met de verwerking van deze berichten.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="c1d8a-176">Maximum aantal gelijktijdige berichten worden verwerkt per functie Hallo is daarom een anderhalf maal Hallo batchgrootte.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="c1d8a-177">Deze beperking geldt afzonderlijk tooeach-functie die een `QueueTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="c1d8a-178">Als u geen parallelle uitvoering voor berichten ontvangen voor een wachtrij wilt, kunt u Hallo batch grootte too1 instellen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="c1d8a-179">Zie ook **meer controle over de verwerking van de wachtrij** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="c1d8a-180"><a id="queuemetadata"></a>Wachtrij of wachtrij bericht metagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="c1d8a-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="c1d8a-181">U kunt Hallo berichteigenschappen volgen door toe te voegen parameters toohello methodehandtekening krijgen:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="c1d8a-182">`DateTimeOffset`expirationTime</span><span class="sxs-lookup"><span data-stu-id="c1d8a-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="c1d8a-183">`DateTimeOffset`insertionTime</span><span class="sxs-lookup"><span data-stu-id="c1d8a-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="c1d8a-184">`DateTimeOffset`nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="c1d8a-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="c1d8a-185">`string`queueTrigger (de berichttekst bevat)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="c1d8a-186">`string`ID</span><span class="sxs-lookup"><span data-stu-id="c1d8a-186">`string` id</span></span>
* <span data-ttu-id="c1d8a-187">`string`popReceipt</span><span class="sxs-lookup"><span data-stu-id="c1d8a-187">`string` popReceipt</span></span>
* <span data-ttu-id="c1d8a-188">`int`dequeueCount</span><span class="sxs-lookup"><span data-stu-id="c1d8a-188">`int` dequeueCount</span></span>

<span data-ttu-id="c1d8a-189">Als u wilt dat toowork rechtstreeks met hello Azure storage-API, u kunt ook toevoegen een `CloudStorageAccount` parameter.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="c1d8a-190">Hallo volgende voorbeeld wordt geschreven alle deze metagegevens tooan INFO-toepassingslogboek.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="c1d8a-191">In voorbeeld Hallo bevatten zowel logMessage als queueTrigger Hallo inhoud van de wachtrij het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="c1d8a-192">Hier volgt een voorbeeld-logboekbestanden geschreven door de voorbeeldcode Hallo:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="c1d8a-193"><a id="graceful"></a>Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="c1d8a-194">Een functie die wordt uitgevoerd in een doorlopende webtaak kan accepteren een `CancellationToken` parameter waarmee Hallo toonotify Hallo besturingssysteemfunctie wanneer hello webtaak is over toobe beëindigd.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="c1d8a-195">U kunt deze melding toomake ervoor Hallo-functie niet onverwacht beëindigd op een manier die gegevens in een inconsistente status heeft blijven.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="c1d8a-196">Hallo volgende voorbeeld wordt getoond hoe toocheck voor aanstaande webtaak beëindiging in een functie.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="c1d8a-197">**Opmerking:** Hallo Dashboard mogelijk niet correct weergegeven Hallo status en de uitvoer van de functies die zijn afgesloten.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="c1d8a-198">Zie voor meer informatie [WebJobs correct afsluiten](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="c1d8a-199"><a id="createqueue"></a>Hoe een wachtrij toocreate bericht tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="c1d8a-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="c1d8a-200">een functie die u een nieuw wachtrijbericht, gebruik Hallo maakt toowrite `Queue` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="c1d8a-201">Zoals `QueueTrigger`, u doorgeeft in Hallo wachtrijnaam als een tekenreeks of kunt u [Hallo wachtrijnaam dynamisch ingesteld](#config).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="c1d8a-202">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-202">String queue messages</span></span>
<span data-ttu-id="c1d8a-203">een nieuwe wachtrijbericht in Hallo wachtrij met de naam 'outputqueue' maakt Hello na niet async-codevoorbeeld met dezelfde inhoud als wachtrij het Hallo-bericht in Hallo wachtrij met de naam 'inputqueue ontvangen' Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="c1d8a-204">(Gebruik voor asynchrone functies `IAsyncCollector<T>` zoals later in deze sectie.)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c1d8a-205">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="c1d8a-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c1d8a-206">toocreate een wachtrijbericht met een POCO in plaats van een tekenreeks, op te geven Hallo POCO typt als een output-parameter toohello `Queue` kenmerkconstructor.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="c1d8a-207">Hallo SDK serialiseert automatisch Hallo object tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="c1d8a-208">Een wachtrijbericht is altijd gemaakt, zelfs als het Hallo-object is null.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="c1d8a-209">Meerdere berichten maken of in een async-functies</span><span class="sxs-lookup"><span data-stu-id="c1d8a-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="c1d8a-210">toocreate meerdere berichten maken Hallo parametertype voor Hallo uitvoerwachtrij `ICollector<T>` of `IAsyncCollector<T>`, zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="c1d8a-211">Het bericht voor elke wachtrij wordt gemaakt bij direct hello `Add` methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="c1d8a-212">Typen Hallo wachtrij kenmerk werkt met</span><span class="sxs-lookup"><span data-stu-id="c1d8a-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="c1d8a-213">U kunt Hallo `Queue` -kenmerk op Hallo parametertypen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="c1d8a-214">`out string`(wachtrijbericht maakt als waarde voor de parameter niet null wanneer de functie Hallo eindigt)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="c1d8a-215">`out byte[]`(werkt als `string`)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="c1d8a-216">`out CloudQueueMessage`(werkt als `string`)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="c1d8a-217">`out POCO`(een serialiseerbaar type, maakt u een bericht met een null-object als Hallo-parameter is null wanneer de functie Hallo eindigt)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="c1d8a-218">`CloudQueue`(voor het maken van berichten handmatig rechtstreeks met Hallo API van Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="c1d8a-219"><a id="ibinder"></a>Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="c1d8a-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="c1d8a-220">Als u toodo moet enkele werken in uw functie voordat u een kenmerk WebJobs SDK, zoals `Queue`, `Blob`, of `Table`, kunt u Hallo `IBinder` interface.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="c1d8a-221">Hallo volgende voorbeeld wordt een bericht invoerwachtrij en maakt u een nieuw bericht Hello dezelfde inhoud in een wachtrij voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="c1d8a-222">Hallo uitvoer wachtrijnaam is ingesteld door code in de hoofdtekst van de functie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="c1d8a-223">Hallo `IBinder` interface kan ook worden gebruikt met Hallo `Table` en `Blob` kenmerken.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="c1d8a-224"><a id="blobs"></a>Hoe tooread en write-blobs en tabellen tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="c1d8a-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="c1d8a-225">Hallo `Blob` en `Table` kenmerken kunt u tooread en blobs en tabellen te schrijven.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="c1d8a-226">Hallo-voorbeelden in deze sectie tooblobs van toepassing.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="c1d8a-227">Zie voor codevoorbeelden die laten hoe tootrigger verwerkt zien wanneer BLOB's worden gemaakt of bijgewerkt, [hoe toouse Azure blob-opslag met Hallo WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), en voor codevoorbeelden die lezen en schrijven van tabellen, Zie [hoe toouse Azure-tabel opslag Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="c1d8a-228">String, Wachtrijberichten activering van blob-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="c1d8a-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="c1d8a-229">Voor een wachtrijbericht met een tekenreeks `queueTrigger` is een tijdelijke aanduiding kunt u in Hallo `Blob` van het kenmerk `blobPath` parameter dat Hallo inhoud van het Hallo-bericht bevat.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="c1d8a-230">Hallo volgende voorbeeld wordt `Stream` tooread en write blobs objecten.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="c1d8a-231">wachtrij het Hallo-bericht is Hallo-naam van een blob die zich in Hallo textblobs container.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="c1d8a-232">Een kopie van de blob met Hallo '-nieuwe ' toegevoegde toohello naam wordt gemaakt in Hallo dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="c1d8a-233">Hallo `Blob` kenmerk constructor heeft een `blobPath` parameter waarmee Hallo-container en de blob-naam.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="c1d8a-234">Zie voor meer informatie over deze tijdelijke aanduiding [hoe toouse Azure blob-opslag met Hallo WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="c1d8a-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="c1d8a-235">Wanneer Hallo kenmerk wordt verfraaid een `Stream` object, een andere constructorparameter geeft u op Hallo `FileAccess` modus lezen, schrijven of lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="c1d8a-236">Hallo volgende voorbeeld wordt een `CloudBlockBlob` toodelete een blob-object.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="c1d8a-237">wachtrij het Hallo-bericht is Hallo-naam van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="c1d8a-238"><a id="pocoblobs"></a>POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="c1d8a-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c1d8a-239">Voor een POCO opgeslagen als JSON in wachtrij het Hallo-bericht, kunt u tijdelijke aanduidingen voor naam van de eigenschappen van het object in Hallo Hallo `Queue` van het kenmerk `blobPath` parameter.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="c1d8a-240">U kunt ook [eigenschapnamen metagegevens in de wachtrij](#queuemetadata) als tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="c1d8a-241">Hallo volgende voorbeeld wordt gekopieerd een blob tooa nieuwe blob met een andere extensie.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="c1d8a-242">wachtrij het Hallo-bericht is een `BlobInformation` -object met `BlobName` en `BlobNameWithoutExtension` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="c1d8a-243">eigenschapnamen Hello worden gebruikt als tijdelijke aanduidingen in Hallo blobpad voor Hallo `Blob` kenmerken.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="c1d8a-244">Hallo SDK maakt gebruik van Hallo [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize en deserialiseren van berichten.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="c1d8a-245">Als u berichten in wachtrij plaatsen in een programma dat Hallo WebJobs SDK maakt geen gebruik maakt, kunt u code zoals het volgende voorbeeld toocreate een wachtrijbericht POCO Hallo schrijven die Hallo die SDK kan worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="c1d8a-246">Als u toodo werken sommige in de functie moet voor het binden van een blob tooan-object, kunt u Hallo-kenmerk in Hallo hoofdtekst van de functie Hallo [zoals eerder besproken voor Hallo wachtrij kenmerk](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="c1d8a-247"><a id="blobattributetypes"></a>Blob-kenmerk met de Hallo kunnen worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="c1d8a-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="c1d8a-248">Hallo `Blob` kenmerk kan worden gebruikt met de volgende typen Hallo:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="c1d8a-249">`Stream`(lezen of schrijven, opgegeven met behulp van Hallo FileAccess constructorparameter)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="c1d8a-250">`string`(gelezen)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-250">`string` (read)</span></span>
* <span data-ttu-id="c1d8a-251">`out string`(schrijven, maakt u een blob alleen als Hallo tekenreeksparameter niet-null is bij het Hallo-functie retourneert)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="c1d8a-252">POCO (lezen)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-252">POCO (read)</span></span>
* <span data-ttu-id="c1d8a-253">uitgaand POCO (schrijven; altijd een blob maakt, maakt als null-object als POCO-parameter null is wanneer Hallo functie retourneert)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="c1d8a-254">`CloudBlobStream`(schrijven)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="c1d8a-255">`ICloudBlob`(Lees- of schrijfbewerking)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="c1d8a-256">`CloudBlockBlob`(Lees- of schrijfbewerking)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="c1d8a-257">`CloudPageBlob`(Lees- of schrijfbewerking)</span><span class="sxs-lookup"><span data-stu-id="c1d8a-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="c1d8a-258"><a id="poison"></a>Hoe toohandle poison berichten</span><span class="sxs-lookup"><span data-stu-id="c1d8a-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="c1d8a-259">Berichten waarvan de inhoud zorgt ervoor een functie toofail dat worden genoemd *berichten poison*.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="c1d8a-260">Hallo-functie is mislukt, wachtrij het Hallo-bericht is niet verwijderd als uiteindelijk wordt opgehaald, waardoor Hallo cyclus toobe herhaald.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="c1d8a-261">Hallo SDK kan automatisch Hallo cyclus worden onderbroken na een beperkt aantal iteraties of u kunt dit handmatig doen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="c1d8a-262">Verwerken van verontreinigde berichten automatische</span><span class="sxs-lookup"><span data-stu-id="c1d8a-262">Automatic poison message handling</span></span>
<span data-ttu-id="c1d8a-263">Hallo SDK zal een functie van too5 keren tooprocess een wachtrijbericht aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="c1d8a-264">Als de vijfde probeer Hallo mislukt, is het Hallo-bericht verplaatste tooa verontreinigd wachtrij.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="c1d8a-265">[Hallo kunt u het maximum aantal pogingen is configureerbaar](#config).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="c1d8a-266">Hallo verontreinigd wachtrij heet *{originalqueuename}*-verontreinigd.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="c1d8a-267">U schrijft een functie tooprocess berichten uit Hallo verontreinigd wachtrij registratie of het verzenden van een melding dat handmatige aandacht nodig is.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="c1d8a-268">In het volgende voorbeeld Hallo Hallo `CopyBlob` functie mislukken wanneer er een wachtrijbericht bevat Hallo-naam van een blob die niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="c1d8a-269">Wanneer dit gebeurt, wordt het Hallo-bericht wordt verplaatst van Hallo copyblobqueue wachtrij toohello copyblobqueue poison wachtrij.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="c1d8a-270">Hallo `ProcessPoisonMessage` vervolgens logboeken Hallo verontreinigd bericht.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="c1d8a-271">Hallo volgende afbeelding ziet u console-uitvoer van deze functies bij het verwerken van een poison-bericht.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![De uitvoer van de console voor het verwerken van verontreinigde berichten](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="c1d8a-273">Verwerken van verontreinigde berichten handmatige</span><span class="sxs-lookup"><span data-stu-id="c1d8a-273">Manual poison message handling</span></span>
<span data-ttu-id="c1d8a-274">U krijgt Hallo aantal keren dat een bericht opgepikt voor verwerking door toe te voegen een `int` parameter met de naam `dequeueCount` tooyour-functie.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="c1d8a-275">U kunt vervolgens het selectievakje hello telling in functiecode in wachtrij- en uw eigen verontreinigd bericht verwerkt wanneer Hallo nummer een drempelwaarde overschrijdt, zoals wordt weergegeven in het volgende voorbeeld Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <span data-ttu-id="c1d8a-276"><a id="config"></a>Hoe tooset configuratieopties</span><span class="sxs-lookup"><span data-stu-id="c1d8a-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="c1d8a-277">U kunt Hallo `JobHostConfiguration` type tooset Hallo volgende configuratieopties:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="c1d8a-278">Hallo SDK verbindingsreeksen in code instellen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="c1d8a-279">Configureer `QueueTrigger` instellingen zoals het maximum aantal in wachtrij.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="c1d8a-280">Wachtrijnamen van de ophalen van configuratie.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="c1d8a-281"><a id="setconnstr"></a>SDK-verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="c1d8a-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="c1d8a-282">Hallo SDK-verbindingsreeksen instellen in de code kunt u toouse uw eigen namen van de tekenreeks verbindingen in configuratiebestanden of omgevingsvariabelen, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="c1d8a-283"><a id="configqueue"></a>QueueTrigger instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="c1d8a-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="c1d8a-284">U kunt Hallo instellingen die van toepassing toohello wachtrij berichtverwerking volgende configureren:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="c1d8a-285">maximum aantal berichten die tegelijkertijd toobe parallel uitgevoerd worden opgepikt Hallo (de standaardwaarde is 16).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="c1d8a-286">Hallo maximum aantal pogingen voordat een wachtrijbericht tooa poison-wachtrij worden verzonden (de standaardwaarde is 5).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="c1d8a-287">Hallo maximale wachttijd voordat opnieuw polling wanneer een wachtrij leeg is (de standaardwaarde is 1 minuut).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="c1d8a-288">Hallo volgende voorbeeld wordt getoond hoe tooconfigure deze instellingen:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="c1d8a-289"><a id="setnamesincode"></a>Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="c1d8a-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="c1d8a-290">Soms wilt u toospecify een wachtrijnaam, een blob-naam of de container of een tabel naam in de code in plaats van harde-code.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="c1d8a-291">U kunt bijvoorbeeld toospecify Hallo wachtrijnaam voor `QueueTrigger` in een configuratie-bestand of de omgeving variabele.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="c1d8a-292">U kunt dit doen door doorgeven in een `NameResolver` toohello object `JobHostConfiguration` type.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="c1d8a-293">U speciale tijdelijke aanduidingen omgeven door procent (%) tekens in constructorparameters WebJobs SDK-kenmerk, opnemen en uw `NameResolver` code geeft Hallo werkelijke waarden toobe gebruikt in plaats van de tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="c1d8a-294">Bijvoorbeeld, Stel dat u wilt dat toouse een wachtrij met de naam logqueuetest in de testomgeving Hallo en één met de naam logqueueprod in productie.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="c1d8a-295">In plaats van een vastgelegde wachtrijnaam, die u wilt toospecify Hallo-naam van een vermelding in Hallo `appSettings` verzameling die de werkelijke wachtrijnaam Hallo zou hebben.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="c1d8a-296">Als hello `appSettings` sleutel logqueue is, de functie eruit als Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="c1d8a-297">Uw `NameResolver` klasse kan vervolgens ophalen Hallo wachtrijnaam van `appSettings` zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="c1d8a-298">U geeft Hallo `NameResolver` klasse in toohello `JobHost` zoals weergegeven in het volgende voorbeeld Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="c1d8a-299">**Opmerking:** Queue, table en blob-namen zijn opgelost telkens wanneer een functie wordt aangeroepen, maar de namen van de blob-containers zijn opgelost, alleen wanneer het Hallo-toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="c1d8a-300">U kunt de naam van de blob-container niet wijzigen terwijl Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="c1d8a-301"><a id="manual"></a>Hoe een functie tootrigger handmatig</span><span class="sxs-lookup"><span data-stu-id="c1d8a-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="c1d8a-302">een functie tootrigger handmatig hello gebruiken `Call` of `CallAsync` methode op Hallo `JobHost` object en Hallo `NoAutomaticTrigger` kenmerk op Hallo-functie, zoals wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <span data-ttu-id="c1d8a-303"><a id="logs"></a>Hoe toowrite registreert</span><span class="sxs-lookup"><span data-stu-id="c1d8a-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="c1d8a-304">Hallo Dashboard ziet u Logboeken op twee plaatsen: Hallo-pagina voor Hallo webtaak en Hallo-pagina voor een specifieke webtaak-aanroep.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Logboeken in webtaak pagina](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Logboeken op de pagina voor functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="c1d8a-307">De uitvoer van de Console-methoden die u in een functie of Hallo aanroepen `Main()` wordt weergegeven in de dashboardpagina Hallo voor Hallo webtaak, niet in Hallo-pagina voor een bepaalde methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="c1d8a-308">Uitvoer van Hallo TextWriter object die u via een parameter in de methodehandtekening weergegeven in de dashboardpagina Hallo voor een methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="c1d8a-309">Console-uitvoer kan niet worden bepaald gekoppelde tooa de methodeaanroep omdat Hallo Console één thread, terwijl veel functies kunnen worden uitgevoerd op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="c1d8a-310">Daarom is Hallo SDK biedt elke functieaanroep met een eigen unieke logboek writer-object.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="c1d8a-311">toowrite [logboeken voor tracering van toepassing](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), gebruik `Console.Out` (maakt logboeken die zijn gemarkeerd als INFO) en `Console.Error` (logboeken die zijn gemarkeerd als fout maakt).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="c1d8a-312">Een alternatief is toouse [tracering of TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)en waarmee u uitgebreid, waarschuwing, kritiek niveaus in de toevoeging tooInfo en de fout.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="c1d8a-313">Logboeken voor tracering van toepassing worden weergegeven in Hallo web app-logboekbestanden, Azure-tabellen, of Azure blobs, afhankelijk van hoe u uw Azure-web-app configureren.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="c1d8a-314">Geldt voor alle Console-uitvoer, Hallo meest recente 100-toepassingslogboeken ook worden weergegeven in de dashboardpagina Hallo voor Hallo webtaak, niet Hallo pagina voor een functie-aanroep.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="c1d8a-315">Console-uitvoer wordt weergegeven in Hallo Dashboard alleen als Hallo programma wordt uitgevoerd in een Azure-webtaak niet als Hallo programma lokaal wordt uitgevoerd of in sommige andere omgeving.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="c1d8a-316">Dashboard logboekregistratie voor scenario's met hoge doorvoer uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="c1d8a-317">Standaard Hallo SDK schrijft logboeken toostorage en deze activiteit kan de prestaties nadelig beïnvloeden tijdens de verwerking van veel berichten.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="c1d8a-318">toodisable logboekregistratie instellen Hallo dashboard connection string toonull zoals in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="c1d8a-319">Hallo volgende voorbeeld ziet u op verschillende manieren toowrite Logboeken:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="c1d8a-320">Hallo in Hallo WebJobs SDK-Dashboard, uitvoer van Hallo `TextWriter` object wordt wanneer u toohello pagina voor een bepaalde gaat functie aanroepen en klik op **wisselknop uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![Klik op de koppeling van de functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Logboeken op de pagina voor functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="c1d8a-323">In Hallo WebJobs SDK-Dashboard, Hallo meest recente 100 regels van de Console uitvoer weergeven van wanneer u toohello pagina voor Hallo webtaak (niet voor functie-aanroep Hallo gaat) en klik op **wisselknop uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![Klik op de uitvoer in-of uitschakelen](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="c1d8a-325">In een doorlopende webtaak toepassingslogboeken weergegeven in/data/taken/continue/*{webjobname}*/job_log.txt in Hallo web-app-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="c1d8a-326">In een Azure blob-toepassing hello logboeken moeten uitzien: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, fout, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="c1d8a-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="c1d8a-327">En in een Azure-tabel Hallo `Console.Out` en `Console.Error` logboeken moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="c1d8a-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![Logboek van de gegevens in de tabel](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Foutenlogboek in tabel](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="c1d8a-330">Als u tooplug in uw eigen berichtenlogboek wilt, Zie [in dit voorbeeld](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="c1d8a-331"><a id="errors"></a>Hoe toohandle fouten en time-outs configureren</span><span class="sxs-lookup"><span data-stu-id="c1d8a-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="c1d8a-332">Hallo WebJobs SDK bevat ook een [time-out](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) kenmerk waarmee u een functie toobe geannuleerd kunt als toocause niet voltooid binnen een opgegeven tijdsduur.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="c1d8a-333">En als u tooraise een waarschuwing wilt als er te veel fouten optreden binnen een opgegeven periode, kunt u Hallo `ErrorTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="c1d8a-334">Hier volgt een [ErrorTrigger voorbeeld](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="c1d8a-335">U kunt ook dynamisch uitschakelen en inschakelen van functies toocontrol of ze kunnen worden geactiveerd, door middel van een configuratieswitch die een app-instelling of de naam van omgevingsvariabele kan worden.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="c1d8a-336">Zie voor voorbeeldcode Hallo `Disable` kenmerk in [hello WebJobs SDK voorbeelden opslagplaats](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="c1d8a-337"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1d8a-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="c1d8a-338">Deze handleiding hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="c1d8a-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="c1d8a-339">Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="c1d8a-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
