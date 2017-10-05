---
title: Azure-wachtrijopslag gebruiken met de WebJobs SDK
description: Informatie over het Azure queue storage gebruiken met de WebJobs SDK. Maken en verwijderen van wachtrijen; invoegen, inspecteren, ophalen en verwijderen van Wachtrijberichten en meer.
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
ms.openlocfilehash: 63b987a2c9471f2929b8d2dd605323910d2ad43b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a><span data-ttu-id="67e48-104">Azure-wachtrijopslag gebruiken met de WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="67e48-104">How to use Azure queue storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="67e48-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="67e48-105">Overview</span></span>
<span data-ttu-id="67e48-106">De C#-codevoorbeelden die laten zien hoe de Azure WebJobs SDK-versie van deze handleiding 1.x met de Azure queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="67e48-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span></span>

<span data-ttu-id="67e48-107">De handleiding wordt ervan uitgegaan dat u weet [tekenreeksen dat punt naar uw opslagaccount, het maken van een webtaak-project in Visual Studio met verbinding](websites-dotnet-webjobs-sdk-get-started.md) of [meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="67e48-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="67e48-108">De meeste van de codefragmenten alleen weergeven functies, niet de code die wordt gemaakt de `JobHost` object zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="67e48-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="67e48-109">De handleiding bevat de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="67e48-109">The guide includes the following topics:</span></span>

* [<span data-ttu-id="67e48-110">Het activeren van een functie wanneer er een wachtrijbericht wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="67e48-110">How to trigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="67e48-111">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="67e48-111">String queue messages</span></span>
  * <span data-ttu-id="67e48-112">POCO-berichtenwachtrij-berichten</span><span class="sxs-lookup"><span data-stu-id="67e48-112">POCO queue messages</span></span>
  * <span data-ttu-id="67e48-113">Async-functies</span><span class="sxs-lookup"><span data-stu-id="67e48-113">Async functions</span></span>
  * <span data-ttu-id="67e48-114">Het kenmerk QueueTrigger met werkt typen</span><span class="sxs-lookup"><span data-stu-id="67e48-114">Types the QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="67e48-115">Polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="67e48-115">Polling algorithm</span></span>
  * <span data-ttu-id="67e48-116">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="67e48-116">Multiple instances</span></span>
  * <span data-ttu-id="67e48-117">Parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="67e48-117">Parallel execution</span></span>
  * <span data-ttu-id="67e48-118">Wachtrij of wachtrij bericht metagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="67e48-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="67e48-119">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="67e48-119">Graceful shutdown</span></span>
* [<span data-ttu-id="67e48-120">Het maken van een wachtrijbericht tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="67e48-120">How to create a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="67e48-121">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="67e48-121">String queue messages</span></span>
  * <span data-ttu-id="67e48-122">POCO-berichtenwachtrij-berichten</span><span class="sxs-lookup"><span data-stu-id="67e48-122">POCO queue messages</span></span>
  * <span data-ttu-id="67e48-123">Meerdere berichten maken of in een async-functies</span><span class="sxs-lookup"><span data-stu-id="67e48-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="67e48-124">Het kenmerk wachtrij met werkt typen</span><span class="sxs-lookup"><span data-stu-id="67e48-124">Types the Queue attribute works with</span></span>
  * <span data-ttu-id="67e48-125">Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="67e48-125">Use WebJobs SDK attributes in the body of a function</span></span>
* [<span data-ttu-id="67e48-126">Hoe kunt lezen en schrijven blobs tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="67e48-126">How to read and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="67e48-127">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="67e48-127">String queue messages</span></span>
  * <span data-ttu-id="67e48-128">POCO-berichtenwachtrij-berichten</span><span class="sxs-lookup"><span data-stu-id="67e48-128">POCO queue messages</span></span>
  * <span data-ttu-id="67e48-129">Het kenmerk Blob met werkt typen</span><span class="sxs-lookup"><span data-stu-id="67e48-129">Types the Blob attribute works with</span></span>
* [<span data-ttu-id="67e48-130">Hoe verontreinigde berichten worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="67e48-130">How to handle poison messages</span></span>](#poison)
  * <span data-ttu-id="67e48-131">Verwerken van verontreinigde berichten automatische</span><span class="sxs-lookup"><span data-stu-id="67e48-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="67e48-132">Verwerken van verontreinigde berichten handmatige</span><span class="sxs-lookup"><span data-stu-id="67e48-132">Manual poison message handling</span></span>
* [<span data-ttu-id="67e48-133">Het instellen van configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="67e48-133">How to set configuration options</span></span>](#config)
  * <span data-ttu-id="67e48-134">SDK-verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="67e48-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="67e48-135">QueueTrigger instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="67e48-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="67e48-136">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="67e48-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="67e48-137">Het activeren van een functie handmatig</span><span class="sxs-lookup"><span data-stu-id="67e48-137">How to trigger a function manually</span></span>](#manual)
* [<span data-ttu-id="67e48-138">Het schrijven van Logboeken</span><span class="sxs-lookup"><span data-stu-id="67e48-138">How to write logs</span></span>](#logs)
* [<span data-ttu-id="67e48-139">Het afhandelen van fouten en time-outs configureren</span><span class="sxs-lookup"><span data-stu-id="67e48-139">How to handle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="67e48-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67e48-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="67e48-141"><a id="trigger"></a>Het activeren van een functie wanneer er een wachtrijbericht wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="67e48-141"><a id="trigger"></a> How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="67e48-142">Voor het schrijven van een functie waarmee de WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruik de `QueueTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="67e48-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span></span> <span data-ttu-id="67e48-143">De kenmerkconstructor tekenreeksparameter een waarmee de naam van de wachtrij om te pollen.</span><span class="sxs-lookup"><span data-stu-id="67e48-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="67e48-144">U kunt ook [dynamisch naam van de wachtrij ingesteld](#config).</span><span class="sxs-lookup"><span data-stu-id="67e48-144">You can also [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="67e48-145">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="67e48-145">String queue messages</span></span>
<span data-ttu-id="67e48-146">In het volgende voorbeeld bevat de wachtrij een string-bericht, dus `QueueTrigger` wordt toegepast op een tekenreeksparameter gebruikt met de naam `logMessage` die de inhoud van het bericht uit de wachtrij bevat.</span><span class="sxs-lookup"><span data-stu-id="67e48-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span></span> <span data-ttu-id="67e48-147">De functie [een logboekbericht schrijft naar het Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="67e48-147">The function [writes a log message to the Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="67e48-148">Naast `string`, de parameter is mogelijk een bytematrix een `CloudQueueMessage` object of een POCO die u definieert.</span><span class="sxs-lookup"><span data-stu-id="67e48-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="67e48-149">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="67e48-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="67e48-150">In het volgende voorbeeld bevat de wachtrijbericht JSON voor een `BlobInformation` object waaronder een `BlobName` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="67e48-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="67e48-151">De SDK deserializes automatisch het object.</span><span class="sxs-lookup"><span data-stu-id="67e48-151">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="67e48-152">De SDK gebruikt de [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) voor het serialiseren en deserialiseren van berichten.</span><span class="sxs-lookup"><span data-stu-id="67e48-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="67e48-153">Als u berichten in wachtrij plaatsen in een programma dat geen gebruik maakt van de WebJobs SDK maakt, kunt u code op het volgende voorbeeld voor het maken van een wachtrijbericht POCO die kan worden geparseerd met de SDK schrijven.</span><span class="sxs-lookup"><span data-stu-id="67e48-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="67e48-154">Async-functies</span><span class="sxs-lookup"><span data-stu-id="67e48-154">Async functions</span></span>
<span data-ttu-id="67e48-155">De volgende async-functie [een logboek wordt geschreven naar het Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="67e48-155">The following async function [writes a log to the Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="67e48-156">Async-functies kunnen duren voordat een [annulering token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), zoals wordt weergegeven in het volgende voorbeeld die een blob kopieert.</span><span class="sxs-lookup"><span data-stu-id="67e48-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="67e48-157">(Voor een uitleg van de `queueTrigger` tijdelijke aanduiding, Zie de [Blobs](#blobs) sectie.)</span><span class="sxs-lookup"><span data-stu-id="67e48-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="67e48-158"><a id="qtattributetypes"></a>Het kenmerk QueueTrigger met werkt typen</span><span class="sxs-lookup"><span data-stu-id="67e48-158"><a id="qtattributetypes"></a> Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="67e48-159">U kunt `QueueTrigger` met de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="67e48-159">You can use `QueueTrigger` with the following types:</span></span>

* `string`
* <span data-ttu-id="67e48-160">Een POCO-type dat geserialiseerd als JSON</span><span class="sxs-lookup"><span data-stu-id="67e48-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="67e48-161"><a id="polling"></a>Polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="67e48-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="67e48-162">De SDK implementeert een willekeurige exponentiële back-off-algoritme het effect van niet-actieve wachtrij op de opslagkosten transaction polling beperkt.</span><span class="sxs-lookup"><span data-stu-id="67e48-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="67e48-163">Wanneer een bericht is gevonden, de SDK Wacht twee seconden en wordt er gecontroleerd of een ander bericht; Wanneer er geen bericht is gevonden wacht ongeveer vier seconden alvorens het opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="67e48-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="67e48-164">Na meerdere mislukte pogingen om op te halen van een wachtrijbericht blijft de wachttijd verhogen totdat het de maximale wachttijd, die standaard één minuut bereikt.</span><span class="sxs-lookup"><span data-stu-id="67e48-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="67e48-165">[De maximale wachttijd is configureerbaar](#config).</span><span class="sxs-lookup"><span data-stu-id="67e48-165">[The maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="67e48-166"><a id="instances"></a>Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="67e48-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="67e48-167">Als uw web-app wordt uitgevoerd op meerdere exemplaren, een doorlopende webtaak wordt uitgevoerd op elke computer en elke computer wordt gewacht op triggers en probeert uit te voeren van functies.</span><span class="sxs-lookup"><span data-stu-id="67e48-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="67e48-168">De WebJobs SDK wachtrij trigger automatisch wordt voorkomen dat een functie verwerken van een wachtrijbericht meerdere keren; functies hoeft niet te worden geschreven naar de idempotent worden.</span><span class="sxs-lookup"><span data-stu-id="67e48-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span></span> <span data-ttu-id="67e48-169">Als u ervoor wilt zorgen dat slechts één exemplaar van een functie wordt uitgevoerd zelfs als er meerdere exemplaren van de host-web-app, kunt u de `Singleton` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="67e48-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span></span>

### <span data-ttu-id="67e48-170"><a id="parallel"></a>Parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="67e48-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="67e48-171">Als er meerdere functies luistert naar verschillende wachtrijen, wordt de SDK aangeroepen ze parallel wanneer berichten tegelijkertijd worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="67e48-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="67e48-172">Hetzelfde geldt wanneer meerdere berichten worden ontvangen voor een enkele wachtrij.</span><span class="sxs-lookup"><span data-stu-id="67e48-172">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="67e48-173">Standaard is de SDK opgehaald van een batch van 16 Wachtrijberichten tegelijk, en voert de functie die parallel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="67e48-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="67e48-174">[De batchgrootte is configureerbaar](#config).</span><span class="sxs-lookup"><span data-stu-id="67e48-174">[The batch size is configurable](#config).</span></span> <span data-ttu-id="67e48-175">Wanneer het aantal verwerkte opgehaald omlaag naar de helft van de batchgrootte van de, wordt de SDK opgehaald van een andere batch en begint met de verwerking van deze berichten.</span><span class="sxs-lookup"><span data-stu-id="67e48-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="67e48-176">Daarom is het maximum aantal gelijktijdige berichten worden verwerkt per functie en een half keer de batchgrootte.</span><span class="sxs-lookup"><span data-stu-id="67e48-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="67e48-177">Deze limiet is van toepassing afzonderlijk op elke functie die een `QueueTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="67e48-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="67e48-178">Als u geen parallelle uitvoering voor berichten ontvangen voor een wachtrij wilt, kunt u de batchgrootte instellen op 1.</span><span class="sxs-lookup"><span data-stu-id="67e48-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span></span> <span data-ttu-id="67e48-179">Zie ook **meer controle over de verwerking van de wachtrij** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="67e48-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="67e48-180"><a id="queuemetadata"></a>Wachtrij of wachtrij bericht metagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="67e48-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="67e48-181">U kunt de volgende berichteigenschappen krijgen door parameters toe te voegen aan de methodehandtekening:</span><span class="sxs-lookup"><span data-stu-id="67e48-181">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="67e48-182">`DateTimeOffset`expirationTime</span><span class="sxs-lookup"><span data-stu-id="67e48-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="67e48-183">`DateTimeOffset`insertionTime</span><span class="sxs-lookup"><span data-stu-id="67e48-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="67e48-184">`DateTimeOffset`nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="67e48-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="67e48-185">`string`queueTrigger (de berichttekst bevat)</span><span class="sxs-lookup"><span data-stu-id="67e48-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="67e48-186">`string`ID</span><span class="sxs-lookup"><span data-stu-id="67e48-186">`string` id</span></span>
* <span data-ttu-id="67e48-187">`string`popReceipt</span><span class="sxs-lookup"><span data-stu-id="67e48-187">`string` popReceipt</span></span>
* <span data-ttu-id="67e48-188">`int`dequeueCount</span><span class="sxs-lookup"><span data-stu-id="67e48-188">`int` dequeueCount</span></span>

<span data-ttu-id="67e48-189">Als u samenwerken met de Azure storage-API wilt, u kunt ook toevoegen een `CloudStorageAccount` parameter.</span><span class="sxs-lookup"><span data-stu-id="67e48-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="67e48-190">Het volgende voorbeeld worden alle deze metagegevens van een logboek INFO geschreven.</span><span class="sxs-lookup"><span data-stu-id="67e48-190">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="67e48-191">In het voorbeeld bevatten zowel logMessage als queueTrigger de inhoud van het bericht uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="67e48-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="67e48-192">Hier volgt een voorbeeld-logboekbestanden geschreven door de voorbeeldcode:</span><span class="sxs-lookup"><span data-stu-id="67e48-192">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="67e48-193"><a id="graceful"></a>Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="67e48-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="67e48-194">Een functie die wordt uitgevoerd in een doorlopende webtaak kan accepteren een `CancellationToken` parameter waarmee het besturingssysteem naar de functie waarschuwen wanneer de webtaak wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="67e48-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="67e48-195">U kunt deze melding om ervoor te zorgen dat de functie niet onverwacht beëindigd op een manier die gegevens in een inconsistente status heeft blijven.</span><span class="sxs-lookup"><span data-stu-id="67e48-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="67e48-196">Het volgende voorbeeld laat zien hoe om te controleren voor aanstaande webtaak beëindiging in een functie.</span><span class="sxs-lookup"><span data-stu-id="67e48-196">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="67e48-197">**Opmerking:** het Dashboard mogelijk niet correct weergegeven status en de uitvoer van de functies die zijn afgesloten.</span><span class="sxs-lookup"><span data-stu-id="67e48-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="67e48-198">Zie voor meer informatie [WebJobs correct afsluiten](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="67e48-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="67e48-199"><a id="createqueue"></a>Het maken van een wachtrijbericht tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="67e48-199"><a id="createqueue"></a> How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="67e48-200">Voor het schrijven van een functie die een nieuwe wachtrijbericht maakt, gebruikt u de `Queue` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="67e48-200">To write a function that creates a new queue message, use the `Queue` attribute.</span></span> <span data-ttu-id="67e48-201">Zoals `QueueTrigger`, u doorgeeft in de naam van de wachtrij als een tekenreeks of kunt u [dynamisch naam van de wachtrij ingesteld](#config).</span><span class="sxs-lookup"><span data-stu-id="67e48-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="67e48-202">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="67e48-202">String queue messages</span></span>
<span data-ttu-id="67e48-203">Het volgende niet-async-codevoorbeeld maakt een nieuwe wachtrijbericht in de wachtrij met de naam 'outputqueue' met dezelfde inhoud als het bericht in de wachtrij ontvangen in de wachtrij met de naam 'inputqueue'.</span><span class="sxs-lookup"><span data-stu-id="67e48-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="67e48-204">(Gebruik voor asynchrone functies `IAsyncCollector<T>` zoals later in deze sectie.)</span><span class="sxs-lookup"><span data-stu-id="67e48-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="67e48-205">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="67e48-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="67e48-206">Voor het maken van een wachtrijbericht met een POCO in plaats van een tekenreeks, geeft u het type POCO als een output-parameter voor de `Queue` kenmerkconstructor.</span><span class="sxs-lookup"><span data-stu-id="67e48-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="67e48-207">De SDK serialiseert automatisch het object naar JSON.</span><span class="sxs-lookup"><span data-stu-id="67e48-207">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="67e48-208">Een wachtrijbericht is altijd gemaakt, zelfs als het object null is.</span><span class="sxs-lookup"><span data-stu-id="67e48-208">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="67e48-209">Meerdere berichten maken of in een async-functies</span><span class="sxs-lookup"><span data-stu-id="67e48-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="67e48-210">Controleer het parametertype voor de wachtrij voor de uitvoer voor het maken van meerdere berichten `ICollector<T>` of `IAsyncCollector<T>`, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="67e48-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="67e48-211">Het bericht voor elke wachtrij wordt onmiddellijk gemaakt wanneer de `Add` methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="67e48-211">Each queue message is created immediately when the `Add` method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="67e48-212">Typen die geschikt is voor het kenmerk wachtrij</span><span class="sxs-lookup"><span data-stu-id="67e48-212">Types that the Queue attribute works with</span></span>
<span data-ttu-id="67e48-213">U kunt de `Queue` kenmerk voor de volgende parameter:</span><span class="sxs-lookup"><span data-stu-id="67e48-213">You can use the `Queue` attribute on the following parameter types:</span></span>

* <span data-ttu-id="67e48-214">`out string`(wachtrijbericht maakt als waarde voor de parameter niet null wanneer de functie eindigt)</span><span class="sxs-lookup"><span data-stu-id="67e48-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="67e48-215">`out byte[]`(werkt als `string`)</span><span class="sxs-lookup"><span data-stu-id="67e48-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="67e48-216">`out CloudQueueMessage`(werkt als `string`)</span><span class="sxs-lookup"><span data-stu-id="67e48-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="67e48-217">`out POCO`(een serialiseerbaar type, maakt u een bericht met een null-object als de parameter is null wanneer de functie wordt beëindigd)</span><span class="sxs-lookup"><span data-stu-id="67e48-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="67e48-218">`CloudQueue`(voor het maken van berichten handmatig rechtstreeks met de Azure Storage-API)</span><span class="sxs-lookup"><span data-stu-id="67e48-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span></span>

### <span data-ttu-id="67e48-219"><a id="ibinder"></a>Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="67e48-219"><a id="ibinder"></a>Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="67e48-220">Als u werken in uw functie wilt voordat u een kenmerk WebJobs SDK, zoals `Queue`, `Blob`, of `Table`, kunt u de `IBinder` interface.</span><span class="sxs-lookup"><span data-stu-id="67e48-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="67e48-221">Het volgende voorbeeld wordt een bericht invoerwachtrij en maakt u een nieuw bericht met de inhoud van een wachtrij voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="67e48-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="67e48-222">De naam van de uitvoer-wachtrij is ingesteld door de code in de hoofdtekst van de functie.</span><span class="sxs-lookup"><span data-stu-id="67e48-222">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="67e48-223">De `IBinder` interface kan ook worden gebruikt met de `Table` en `Blob` kenmerken.</span><span class="sxs-lookup"><span data-stu-id="67e48-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="67e48-224"><a id="blobs"></a>Hoe kunnen lezen en schrijven van blobs, tabellen en tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="67e48-224"><a id="blobs"></a> How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="67e48-225">De `Blob` en `Table` kenmerken kunnen u blobs en tabellen lezen en schrijven.</span><span class="sxs-lookup"><span data-stu-id="67e48-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="67e48-226">De voorbeelden in deze sectie zijn van toepassing op blobs.</span><span class="sxs-lookup"><span data-stu-id="67e48-226">The samples in this section apply to blobs.</span></span> <span data-ttu-id="67e48-227">Zie voor codevoorbeelden die laten hoe u zien voor het activeren van processen wanneer BLOB's worden gemaakt of bijgewerkt, [Azure blob storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), en voor codevoorbeelden die lezen en schrijven van tabellen, Zie [het gebruik van Azure-tabel opslag met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="67e48-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="67e48-228">String, Wachtrijberichten activering van blob-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="67e48-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="67e48-229">Voor een wachtrijbericht met een tekenreeks `queueTrigger` is een tijdelijke aanduiding kunt u in de `Blob` van het kenmerk `blobPath` parameter die de inhoud van het bericht bevat.</span><span class="sxs-lookup"><span data-stu-id="67e48-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span></span>

<span data-ttu-id="67e48-230">Het volgende voorbeeld wordt `Stream` objecten te lezen en schrijven blobs.</span><span class="sxs-lookup"><span data-stu-id="67e48-230">The following example uses `Stream` objects to read and write blobs.</span></span> <span data-ttu-id="67e48-231">Bericht uit de wachtrij is de naam van een blob die zich in de container textblobs.</span><span class="sxs-lookup"><span data-stu-id="67e48-231">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="67e48-232">Een kopie van de blob met '-nieuwe ' toegevoegd aan de naam wordt gemaakt in dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="67e48-232">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="67e48-233">De `Blob` kenmerk constructor heeft een `blobPath` parameter waarmee de container en de blob-naam.</span><span class="sxs-lookup"><span data-stu-id="67e48-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span></span> <span data-ttu-id="67e48-234">Zie voor meer informatie over deze tijdelijke aanduiding [Azure blob storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="67e48-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="67e48-235">Wanneer het kenmerk wordt verfraaid een `Stream` object, een andere constructorparameter geeft u de `FileAccess` modus lezen, schrijven of lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="67e48-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="67e48-236">Het volgende voorbeeld wordt een `CloudBlockBlob` object verwijderen van een blob.</span><span class="sxs-lookup"><span data-stu-id="67e48-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span></span> <span data-ttu-id="67e48-237">Bericht uit de wachtrij is de naam van de blob.</span><span class="sxs-lookup"><span data-stu-id="67e48-237">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="67e48-238"><a id="pocoblobs"></a>POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="67e48-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="67e48-239">Voor een POCO opgeslagen als JSON in bericht in de wachtrij, kunt u tijdelijke aanduidingen die eigenschappen van het object in een naam geven de `Queue` van het kenmerk `blobPath` parameter.</span><span class="sxs-lookup"><span data-stu-id="67e48-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="67e48-240">U kunt ook [eigenschapnamen metagegevens in de wachtrij](#queuemetadata) als tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="67e48-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="67e48-241">Het volgende voorbeeld wordt een blob kopieert naar een nieuwe blob met een andere extensie.</span><span class="sxs-lookup"><span data-stu-id="67e48-241">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="67e48-242">Bericht uit de wachtrij is een `BlobInformation` -object met `BlobName` en `BlobNameWithoutExtension` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="67e48-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="67e48-243">De namen van eigenschappen worden gebruikt als tijdelijke aanduidingen in de blobpad voor de `Blob` kenmerken.</span><span class="sxs-lookup"><span data-stu-id="67e48-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="67e48-244">De SDK gebruikt de [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) voor het serialiseren en deserialiseren van berichten.</span><span class="sxs-lookup"><span data-stu-id="67e48-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="67e48-245">Als u berichten in wachtrij plaatsen in een programma dat geen gebruik maakt van de WebJobs SDK maakt, kunt u code op het volgende voorbeeld voor het maken van een wachtrijbericht POCO die kan worden geparseerd met de SDK schrijven.</span><span class="sxs-lookup"><span data-stu-id="67e48-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="67e48-246">Als u werken in de functie wilt voor het binden van een blob naar een object, kunt u het kenmerk in de hoofdtekst van de functie [zoals eerder besproken voor het kenmerk wachtrij](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="67e48-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="67e48-247"><a id="blobattributetypes"></a>U het kenmerk Blob met kunt typen</span><span class="sxs-lookup"><span data-stu-id="67e48-247"><a id="blobattributetypes"></a> Types you can use the Blob attribute with</span></span>
<span data-ttu-id="67e48-248">De `Blob` kenmerk kan worden gebruikt met de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="67e48-248">The `Blob` attribute can be used with the following types:</span></span>

* <span data-ttu-id="67e48-249">`Stream`(lezen of schrijven, opgegeven met behulp van de constructorparameter FileAccess)</span><span class="sxs-lookup"><span data-stu-id="67e48-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="67e48-250">`string`(gelezen)</span><span class="sxs-lookup"><span data-stu-id="67e48-250">`string` (read)</span></span>
* <span data-ttu-id="67e48-251">`out string`(schrijven, maakt u een blob alleen als de tekenreeksparameter is een niet-null wanneer de functie retourneert)</span><span class="sxs-lookup"><span data-stu-id="67e48-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="67e48-252">POCO (lezen)</span><span class="sxs-lookup"><span data-stu-id="67e48-252">POCO (read)</span></span>
* <span data-ttu-id="67e48-253">uitgaand POCO (schrijven; altijd een blob maakt, maakt als null-object als POCO-parameter null is wanneer de functie retourneert)</span><span class="sxs-lookup"><span data-stu-id="67e48-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="67e48-254">`CloudBlobStream`(schrijven)</span><span class="sxs-lookup"><span data-stu-id="67e48-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="67e48-255">`ICloudBlob`(Lees- of schrijfbewerking)</span><span class="sxs-lookup"><span data-stu-id="67e48-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="67e48-256">`CloudBlockBlob`(Lees- of schrijfbewerking)</span><span class="sxs-lookup"><span data-stu-id="67e48-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="67e48-257">`CloudPageBlob`(Lees- of schrijfbewerking)</span><span class="sxs-lookup"><span data-stu-id="67e48-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="67e48-258"><a id="poison"></a>Hoe verontreinigde berichten worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="67e48-258"><a id="poison"></a> How to handle poison messages</span></span>
<span data-ttu-id="67e48-259">Berichten waarvan de inhoud zorgt ervoor dat een functie mislukken worden genoemd *berichten poison*.</span><span class="sxs-lookup"><span data-stu-id="67e48-259">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="67e48-260">De functie mislukt, bericht uit de wachtrij wordt niet verwijderd als uiteindelijk wordt opgehaald, waardoor de cyclus om te worden herhaald.</span><span class="sxs-lookup"><span data-stu-id="67e48-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="67e48-261">De SDK kan automatisch de cyclus worden onderbroken na een beperkt aantal iteraties of u kunt dit handmatig doen.</span><span class="sxs-lookup"><span data-stu-id="67e48-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="67e48-262">Verwerken van verontreinigde berichten automatische</span><span class="sxs-lookup"><span data-stu-id="67e48-262">Automatic poison message handling</span></span>
<span data-ttu-id="67e48-263">De SDK worden aanroepen van een functie 5 maal een wachtrijbericht te verwerken.</span><span class="sxs-lookup"><span data-stu-id="67e48-263">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="67e48-264">Als de vijfde poging is mislukt, wordt het bericht wordt verplaatst naar een poison wachtrij.</span><span class="sxs-lookup"><span data-stu-id="67e48-264">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="67e48-265">[Het maximum aantal nieuwe pogingen is configureerbaar](#config).</span><span class="sxs-lookup"><span data-stu-id="67e48-265">[The maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="67e48-266">De naam van de wachtrij verontreinigd *{originalqueuename}*-verontreinigd.</span><span class="sxs-lookup"><span data-stu-id="67e48-266">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="67e48-267">U kunt schrijven om een functie verwerken van berichten uit de wachtrij verontreinigd door registratie of het verzenden van een melding dat handmatige aandacht nodig is.</span><span class="sxs-lookup"><span data-stu-id="67e48-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="67e48-268">In het volgende voorbeeld de `CopyBlob` functie mislukken wanneer er een wachtrijbericht bevat de naam van een blob die niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="67e48-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="67e48-269">Wanneer dit gebeurt, wordt het bericht uit de wachtrij copyblobqueue verplaatst naar de wachtrij copyblobqueue poison.</span><span class="sxs-lookup"><span data-stu-id="67e48-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="67e48-270">De `ProcessPoisonMessage` meldt zich dan verontreinigd bericht.</span><span class="sxs-lookup"><span data-stu-id="67e48-270">The `ProcessPoisonMessage` then logs the poison message.</span></span>

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
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="67e48-271">De volgende afbeelding toont console-uitvoer van deze functies bij het verwerken van een poison-bericht.</span><span class="sxs-lookup"><span data-stu-id="67e48-271">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![De uitvoer van de console voor het verwerken van verontreinigde berichten](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="67e48-273">Verwerken van verontreinigde berichten handmatige</span><span class="sxs-lookup"><span data-stu-id="67e48-273">Manual poison message handling</span></span>
<span data-ttu-id="67e48-274">U kunt het aantal keren dat een bericht opgepikt voor verwerking ophalen door het toevoegen van een `int` parameter met de naam `dequeueCount` aan de functie.</span><span class="sxs-lookup"><span data-stu-id="67e48-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span></span> <span data-ttu-id="67e48-275">U kunt controleren van de wachtrij halen telling in functiecode en voer uw eigen verontreinigd bericht verwerkt wanneer meer dan een drempelwaarde, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="67e48-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <span data-ttu-id="67e48-276"><a id="config"></a>Het instellen van configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="67e48-276"><a id="config"></a> How to set configuration options</span></span>
<span data-ttu-id="67e48-277">U kunt de `JobHostConfiguration` type in te stellen van de volgende configuratieopties:</span><span class="sxs-lookup"><span data-stu-id="67e48-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span></span>

* <span data-ttu-id="67e48-278">De SDK-verbindingsreeksen in code instellen.</span><span class="sxs-lookup"><span data-stu-id="67e48-278">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="67e48-279">Configureer `QueueTrigger` instellingen zoals het maximum aantal in wachtrij.</span><span class="sxs-lookup"><span data-stu-id="67e48-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="67e48-280">Wachtrijnamen van de ophalen van configuratie.</span><span class="sxs-lookup"><span data-stu-id="67e48-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="67e48-281"><a id="setconnstr"></a>SDK-verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="67e48-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="67e48-282">Instellen van de SDK-verbindingsreeksen in code kunt u uw eigen namen van de tekenreeks verbindingen in configuratiebestanden of omgevingsvariabelen gebruiken zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="67e48-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <span data-ttu-id="67e48-283"><a id="configqueue"></a>QueueTrigger instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="67e48-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="67e48-284">U kunt de volgende instellingen die betrekking hebben op de berichtverwerking wachtrij configureren:</span><span class="sxs-lookup"><span data-stu-id="67e48-284">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="67e48-285">Het maximum aantal berichten die tegelijkertijd worden opgepikt parallel worden uitgevoerd (de standaardwaarde is 16).</span><span class="sxs-lookup"><span data-stu-id="67e48-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="67e48-286">Het maximum aantal pogingen alvorens een wachtrijbericht naar een poison-wachtrij verzonden (de standaardwaarde is 5).</span><span class="sxs-lookup"><span data-stu-id="67e48-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="67e48-287">De maximale wachttijd voordat opnieuw polling wanneer een wachtrij leeg is (de standaardwaarde is 1 minuut).</span><span class="sxs-lookup"><span data-stu-id="67e48-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="67e48-288">Het volgende voorbeeld ziet u hoe deze instellingen te configureren:</span><span class="sxs-lookup"><span data-stu-id="67e48-288">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="67e48-289"><a id="setnamesincode"></a>Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="67e48-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="67e48-290">Soms wilt u de naam van een wachtrij, een blob-naam of -container opgeven of een tabel naam in de code in plaats van harde-code.</span><span class="sxs-lookup"><span data-stu-id="67e48-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="67e48-291">Bijvoorbeeld, u wilt mogelijk opgeven de naam van de wachtrij voor `QueueTrigger` in een configuratie-bestand of de omgeving variabele.</span><span class="sxs-lookup"><span data-stu-id="67e48-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="67e48-292">U kunt dit doen door doorgeven in een `NameResolver` object toe aan de `JobHostConfiguration` type.</span><span class="sxs-lookup"><span data-stu-id="67e48-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span></span> <span data-ttu-id="67e48-293">U speciale tijdelijke aanduidingen omgeven door procent (%) tekens in constructorparameters WebJobs SDK-kenmerk, opnemen en uw `NameResolver` code bevat de werkelijke waarden moet worden gebruikt in plaats van de tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="67e48-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="67e48-294">Stel dat u wilt gebruiken, een wachtrij met de naam logqueuetest in de testomgeving en een benoemde logqueueprod in productie.</span><span class="sxs-lookup"><span data-stu-id="67e48-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="67e48-295">In plaats van een vastgelegde wachtrijnaam, die u wilt opgeven van de naam van een vermelding in de `appSettings` verzameling die de werkelijke wachtrijnaam zou hebben.</span><span class="sxs-lookup"><span data-stu-id="67e48-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span></span> <span data-ttu-id="67e48-296">Als de `appSettings` sleutel logqueue is, de functie eruit als in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="67e48-296">If the `appSettings` key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="67e48-297">Uw `NameResolver` klasse kan vervolgens worden opgehaald uit de naam van de wachtrij `appSettings` zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="67e48-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="67e48-298">U geeft de `NameResolver` -klasse in voor de `JobHost` object, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="67e48-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="67e48-299">**Opmerking:** Queue, table en blob-namen zijn opgelost telkens wanneer een functie wordt aangeroepen, maar de namen van de blob-containers zijn opgelost, alleen wanneer de toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="67e48-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="67e48-300">U kunt de naam van de blob-container niet wijzigen terwijl de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="67e48-300">You can't change blob container name while the job is running.</span></span>

## <span data-ttu-id="67e48-301"><a id="manual"></a>Het activeren van een functie handmatig</span><span class="sxs-lookup"><span data-stu-id="67e48-301"><a id="manual"></a>How to trigger a function manually</span></span>
<span data-ttu-id="67e48-302">Als u wilt een functie handmatig activeren, gebruiken de `Call` of `CallAsync` methode op de `JobHost` object en de `NoAutomaticTrigger` -kenmerk uit voor de functie, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="67e48-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span></span>

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

## <span data-ttu-id="67e48-303"><a id="logs"></a>Het schrijven van Logboeken</span><span class="sxs-lookup"><span data-stu-id="67e48-303"><a id="logs"></a>How to write logs</span></span>
<span data-ttu-id="67e48-304">Het Dashboard toont de logboeken op twee plaatsen: de pagina voor de webtaak en op de pagina voor een specifieke webtaak-aanroep.</span><span class="sxs-lookup"><span data-stu-id="67e48-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Logboeken in webtaak pagina](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Logboeken op de pagina voor functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="67e48-307">De uitvoer van de Console methoden die u in een functie aanroept of in de `Main()` wordt weergegeven op de pagina Dashboard voor de webtaak, niet op de pagina voor het aanroepen van een bepaalde methode.</span><span class="sxs-lookup"><span data-stu-id="67e48-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="67e48-308">De uitvoer van het object TextWriter die u via een parameter in de methodehandtekening wordt weergegeven op de pagina Dashboard voor een methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="67e48-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="67e48-309">Console-uitvoer kan niet worden gekoppeld aan een bepaalde methodeaanroep omdat de Console één thread, is terwijl veel functies kunnen worden uitgevoerd op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="67e48-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="67e48-310">Daarom is de SDK kunt u elke functieaanroep met een eigen unieke logboek writer-object.</span><span class="sxs-lookup"><span data-stu-id="67e48-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="67e48-311">Schrijven van [logboeken voor tracering van toepassing](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), gebruik `Console.Out` (maakt logboeken die zijn gemarkeerd als INFO) en `Console.Error` (logboeken die zijn gemarkeerd als fout maakt).</span><span class="sxs-lookup"><span data-stu-id="67e48-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="67e48-312">Een alternatief is [tracering of TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), waarmee u uitgebreid, waarschuwing, en kritieke niveaus naast gegevens en de fout.</span><span class="sxs-lookup"><span data-stu-id="67e48-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="67e48-313">Logboeken voor tracering van toepassing worden weergegeven in de logboekbestanden web app, Azure-tabellen, of Azure blobs, afhankelijk van hoe u uw Azure-web-app configureren.</span><span class="sxs-lookup"><span data-stu-id="67e48-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="67e48-314">Geldt voor alle Console-uitvoer, weergegeven de meest recente 100 toepassingslogboeken ook in de pagina Dashboard voor de webtaak, niet op de pagina voor een functie-aanroep.</span><span class="sxs-lookup"><span data-stu-id="67e48-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="67e48-315">Console-uitvoer wordt weergegeven in het Dashboard alleen als het programma wordt uitgevoerd in een Azure-webtaak niet als het programma lokaal wordt uitgevoerd of in sommige andere omgeving.</span><span class="sxs-lookup"><span data-stu-id="67e48-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="67e48-316">Dashboard logboekregistratie voor scenario's met hoge doorvoer uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="67e48-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="67e48-317">Standaard schrijft de logboeken naar de opslag de SDK en deze activiteit kan de prestaties nadelig beïnvloeden tijdens de verwerking van veel berichten.</span><span class="sxs-lookup"><span data-stu-id="67e48-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="67e48-318">Als logboekregistratie wilt uitschakelen, stelt u de verbindingsreeks dashboard op null, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="67e48-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="67e48-319">Het volgende voorbeeld ziet u schrijven logboeken op verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="67e48-319">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="67e48-320">In de WebJobs SDK-Dashboard de uitvoer van de `TextWriter` object wordt wanneer u naar de pagina voor een bepaalde gaat functie aanroepen en klik op **wisselknop uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="67e48-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span></span>

![Klik op de koppeling van de functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Logboeken op de pagina voor functie-aanroep](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="67e48-323">In de WebJobs SDK-Dashboard de meest recente 100 regels van de Console uitvoer weergeven van wanneer u gaat u naar de pagina voor de webtaak (niet voor de functie-aanroep) en klik op **wisselknop uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="67e48-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span></span>

![Klik op de uitvoer in-of uitschakelen](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="67e48-325">In een doorlopende webtaak toepassingslogboeken weergegeven in/data/taken/continue/*{webjobname}*/job_log.txt in het bestandssysteem van de web-app.</span><span class="sxs-lookup"><span data-stu-id="67e48-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="67e48-326">In een Azure blob-de toepassing Logboeken eruit als volgt: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, fout, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="67e48-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="67e48-327">En in een Azure-tabel de `Console.Out` en `Console.Error` logboeken moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="67e48-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span></span>

![Logboek van de gegevens in de tabel](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Foutenlogboek in tabel](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="67e48-330">Als u uw eigen berichtenlogboek aansluit wilt, Zie [in dit voorbeeld](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="67e48-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="67e48-331"><a id="errors"></a>Het afhandelen van fouten en time-outs configureren</span><span class="sxs-lookup"><span data-stu-id="67e48-331"><a id="errors"></a>How to handle errors and configure timeouts</span></span>
<span data-ttu-id="67e48-332">De WebJobs SDK bevat ook een [time-out](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) kenmerk dat u gebruiken kunt om te leiden tot een functie worden geannuleerd als niet voltooid binnen een opgegeven tijdsduur.</span><span class="sxs-lookup"><span data-stu-id="67e48-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="67e48-333">En als u een waarschuwing activeren wilt als er te veel fouten optreden binnen een opgegeven periode, kunt u de `ErrorTrigger` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="67e48-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span></span> <span data-ttu-id="67e48-334">Hier volgt een [ErrorTrigger voorbeeld](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="67e48-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="67e48-335">U kunt ook dynamisch uitschakelen en inschakelen van functies om te bepalen of ze kunnen worden geactiveerd, door middel van een configuratieswitch die een app-instelling of de naam van omgevingsvariabele kan worden.</span><span class="sxs-lookup"><span data-stu-id="67e48-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="67e48-336">Zie voor een voorbeeld van code, de `Disable` kenmerk in [de WebJobs SDK voorbeelden opslagplaats](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="67e48-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="67e48-337"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67e48-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="67e48-338">Deze handleiding is opgegeven codevoorbeelden die laten hoe u veelvoorkomende scenario's zien voor het werken met Azure wachtrijen verwerken.</span><span class="sxs-lookup"><span data-stu-id="67e48-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="67e48-339">Zie voor meer informatie over het gebruik van Azure WebJobs en de WebJobs SDK [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="67e48-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
