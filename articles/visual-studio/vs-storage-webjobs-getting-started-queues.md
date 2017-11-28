---
title: aaaGetting gestart met de opslag van de wachtrij en Visual Studio verbonden services (webtaak projecten) | Microsoft Docs
description: Hoe tooget gestart met Azure Queue storage in een project webtaak nadat tooa storage-account met Visual Studio verbinding services verbonden.
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 47a446aa5c6bbf25526339823db4952ac1a8802f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="28afd-103">Aan de slag met Azure Queue storage en Visual Studio verbonden services (webtaak projecten)</span><span class="sxs-lookup"><span data-stu-id="28afd-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="28afd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="28afd-104">Overview</span></span>
<span data-ttu-id="28afd-105">Dit artikel wordt beschreven hoe de slag met Azure Queue storage in een project voor Visual Studio Azure webtaak nadat u hebt gemaakt of waarnaar wordt verwezen Azure storage-account met behulp van Visual Studio Hallo **verbonden Services toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="28afd-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="28afd-106">Wanneer u een project storage account tooa webtaak toevoegen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster Hallo juiste Azure Storage NuGet-pakketten zijn geïnstalleerd, Hallo juiste .NET verwijzingen worden toegevoegd toohello Project en verbindingsreeksen voor Hallo storage-account worden bijgewerkt in Hallo App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="28afd-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="28afd-107">Dit artikel vindt u C#-codevoorbeelden die laten zien hoe toouse hello Azure WebJobs SDK versie 1.x Hello Azure Queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="28afd-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="28afd-108">Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="28afd-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="28afd-109">Een enkel wachtrijbericht mag up too64 KB groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten.</span><span class="sxs-lookup"><span data-stu-id="28afd-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="28afd-110">Zie [aan de slag met Azure Queue Storage met .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="28afd-110">See [Get started with Azure Queue Storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="28afd-111">Zie voor meer informatie over ASP.NET [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="28afd-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="28afd-112">Hoe tootrigger een functie wanneer er een wachtrijbericht wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="28afd-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="28afd-113">toowrite een functie die Hallo WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruikt u Hallo **QueueTrigger** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="28afd-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="28afd-114">Hallo kenmerkconstructor tekenreeksparameter een waarmee Hallo-naam van Hallo wachtrij toopoll.</span><span class="sxs-lookup"><span data-stu-id="28afd-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="28afd-115">toosee hoe tooset Hallo wachtrijnaam dynamisch, Bekijk [hoe tooset configuratieopties](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="28afd-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="28afd-116">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="28afd-116">String queue messages</span></span>
<span data-ttu-id="28afd-117">Hallo voorbeeld te volgen, Hallo wachtrij bevat een Tekenreeksbericht voor de dus **QueueTrigger** toegepaste tooa tekenreeksparameter met de naam is **logMessage** die Hallo inhoud van de wachtrij het Hallo-bericht bevat.</span><span class="sxs-lookup"><span data-stu-id="28afd-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="28afd-118">Hallo functie [schrijft een logboek bericht toohello Dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="28afd-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="28afd-119">Naast **tekenreeks**, Hallo is mogelijk een bytematrix een **CloudQueueMessage** object of een POCO die u definieert.</span><span class="sxs-lookup"><span data-stu-id="28afd-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="28afd-120">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="28afd-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="28afd-121">Hallo voorbeeld te volgen, wachtrij het Hallo-bericht bevat JSON voor een **BlobInformation** object waaronder een **BlobName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="28afd-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="28afd-122">Hallo SDK deserializes automatisch Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="28afd-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="28afd-123">Hallo SDK maakt gebruik van Hallo [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize en deserialiseren van berichten.</span><span class="sxs-lookup"><span data-stu-id="28afd-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="28afd-124">Als u berichten in wachtrij plaatsen in een programma dat Hallo WebJobs SDK maakt geen gebruik maakt, kunt u code zoals het volgende voorbeeld toocreate een wachtrijbericht POCO Hallo schrijven die Hallo die SDK kan worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="28afd-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="28afd-125">Async-functies</span><span class="sxs-lookup"><span data-stu-id="28afd-125">Async functions</span></span>
<span data-ttu-id="28afd-126">Hallo async-functie na [schrijft een logboek toohello Dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="28afd-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="28afd-127">Async-functies kunnen duren voordat een [annulering token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), zoals weergegeven in het volgende voorbeeld die een blob kopieert Hallo.</span><span class="sxs-lookup"><span data-stu-id="28afd-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="28afd-128">(Voor een uitleg van Hallo **queueTrigger** tijdelijke aanduiding, Zie Hallo [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sectie.)</span><span class="sxs-lookup"><span data-stu-id="28afd-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="28afd-129">Typen Hallo QueueTrigger kenmerk werkt met</span><span class="sxs-lookup"><span data-stu-id="28afd-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="28afd-130">U kunt **QueueTrigger** Hello volgende typen:</span><span class="sxs-lookup"><span data-stu-id="28afd-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="28afd-131">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="28afd-131">**string**</span></span>
* <span data-ttu-id="28afd-132">Een POCO-type dat geserialiseerd als JSON</span><span class="sxs-lookup"><span data-stu-id="28afd-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="28afd-133">**byte]**</span><span class="sxs-lookup"><span data-stu-id="28afd-133">**byte[]**</span></span>
* <span data-ttu-id="28afd-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="28afd-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="28afd-135">Polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="28afd-135">Polling algorithm</span></span>
<span data-ttu-id="28afd-136">Hallo SDK implementeert een willekeurige exponentiële back-off algoritme tooreduce Hallo effect van niet-actieve wachtrij polling op de opslagkosten voor transactie.</span><span class="sxs-lookup"><span data-stu-id="28afd-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="28afd-137">Wanneer een bericht is gevonden, Hallo SDK Wacht twee seconden en wordt er gecontroleerd of een ander bericht; Wanneer er geen bericht is gevonden wacht ongeveer vier seconden alvorens het opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="28afd-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="28afd-138">Na meerdere mislukte pogingen tooget een wachtrijbericht, wachttijd Hallo tooincrease voortgezet totdat het Hallo maximale wachttijd, bereikt welke standaardwaarden tooone minuut.</span><span class="sxs-lookup"><span data-stu-id="28afd-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="28afd-139">[Hallo maximale wachttijd is configureerbaar](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="28afd-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="28afd-140">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="28afd-140">Multiple instances</span></span>
<span data-ttu-id="28afd-141">Als uw web-app wordt uitgevoerd op meerdere exemplaren, een doorlopende webtaken uitvoert op elke machine en elke machine wordt gewacht op triggers en probeert toorun functies.</span><span class="sxs-lookup"><span data-stu-id="28afd-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="28afd-142">In sommige gevallen die kan dit leiden toosome functies verwerken Hallo dezelfde gegevens tweemaal functies moeten dus van idempotent (zodat die herhaaldelijk aanroepen Hello dezelfde invoergegevens levert geen resultaten dubbele geschreven).</span><span class="sxs-lookup"><span data-stu-id="28afd-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="28afd-143">Parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="28afd-143">Parallel execution</span></span>
<span data-ttu-id="28afd-144">Als er meerdere functies luistert naar verschillende wachtrijen, wordt Hallo SDK aangeroepen ze parallel wanneer berichten tegelijkertijd worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="28afd-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="28afd-145">Hallo geldt ook wanneer meerdere berichten worden ontvangen voor een enkele wachtrij.</span><span class="sxs-lookup"><span data-stu-id="28afd-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="28afd-146">Standaard Hallo SDK een batch van 16 Wachtrijberichten tegelijk opgehaald en wordt uitgevoerd Hallo-functie die parallel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="28afd-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="28afd-147">[Hallo batchgrootte is configureerbaar](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="28afd-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="28afd-148">Bij het ophalen van Hallo nummer wordt verwerkt omlaag toohalf van batchgrootte hello, hello SDK opgehaald van een andere batch- en begint met de verwerking van deze berichten.</span><span class="sxs-lookup"><span data-stu-id="28afd-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="28afd-149">Maximum aantal gelijktijdige berichten worden verwerkt per functie Hallo is daarom een anderhalf maal Hallo batchgrootte.</span><span class="sxs-lookup"><span data-stu-id="28afd-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="28afd-150">Deze beperking geldt afzonderlijk tooeach-functie die een **QueueTrigger** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="28afd-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="28afd-151">Als u niet dat parallelle uitvoering voor berichten ontvangen voor een wachtrij wilt, stelt u Hallo batch grootte too1.</span><span class="sxs-lookup"><span data-stu-id="28afd-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="28afd-152">Wachtrij of wachtrij bericht metagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="28afd-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="28afd-153">U kunt Hallo berichteigenschappen volgen door toe te voegen parameters toohello methodehandtekening krijgen:</span><span class="sxs-lookup"><span data-stu-id="28afd-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="28afd-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="28afd-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="28afd-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="28afd-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="28afd-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="28afd-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="28afd-157">**tekenreeks** queueTrigger (de berichttekst bevat)</span><span class="sxs-lookup"><span data-stu-id="28afd-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="28afd-158">**tekenreeks** id</span><span class="sxs-lookup"><span data-stu-id="28afd-158">**string** id</span></span>
* <span data-ttu-id="28afd-159">**tekenreeks** popReceipt</span><span class="sxs-lookup"><span data-stu-id="28afd-159">**string** popReceipt</span></span>
* <span data-ttu-id="28afd-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="28afd-160">**int** dequeueCount</span></span>

<span data-ttu-id="28afd-161">Als u wilt dat toowork rechtstreeks met hello Azure storage-API, u kunt ook toevoegen een **CloudStorageAccount** parameter.</span><span class="sxs-lookup"><span data-stu-id="28afd-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="28afd-162">Hallo volgende voorbeeld wordt geschreven alle deze metagegevens tooan INFO-toepassingslogboek.</span><span class="sxs-lookup"><span data-stu-id="28afd-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="28afd-163">In voorbeeld Hallo bevatten zowel logMessage als queueTrigger Hallo inhoud van de wachtrij het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="28afd-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="28afd-164">Hier volgt een voorbeeld-logboekbestanden geschreven door de voorbeeldcode Hallo:</span><span class="sxs-lookup"><span data-stu-id="28afd-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="28afd-165">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="28afd-165">Graceful shutdown</span></span>
<span data-ttu-id="28afd-166">Een functie die wordt uitgevoerd in een doorlopende webtaak kan accepteren een **CancellationToken** parameter waarmee Hallo toonotify Hallo besturingssysteemfunctie wanneer hello webtaak is over toobe beëindigd.</span><span class="sxs-lookup"><span data-stu-id="28afd-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="28afd-167">U kunt deze melding toomake ervoor Hallo-functie niet onverwacht beëindigd op een manier die gegevens in een inconsistente status heeft blijven.</span><span class="sxs-lookup"><span data-stu-id="28afd-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="28afd-168">Hallo volgende voorbeeld wordt getoond hoe toocheck voor aanstaande webtaak beëindiging in een functie.</span><span class="sxs-lookup"><span data-stu-id="28afd-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="28afd-169">**Opmerking:** Hallo Dashboard mogelijk niet correct weergegeven Hallo status en de uitvoer van de functies die zijn afgesloten.</span><span class="sxs-lookup"><span data-stu-id="28afd-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="28afd-170">Zie voor meer informatie [WebJobs correct afsluiten](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="28afd-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="28afd-171">Hoe een wachtrij toocreate bericht tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="28afd-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="28afd-172">een functie die u een nieuw wachtrijbericht, gebruik Hallo maakt toowrite **wachtrij** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="28afd-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="28afd-173">Zoals **QueueTrigger**, u doorgeeft in Hallo wachtrijnaam als een tekenreeks of kunt u [Hallo wachtrijnaam dynamisch ingesteld](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="28afd-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="28afd-174">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="28afd-174">String queue messages</span></span>
<span data-ttu-id="28afd-175">een nieuwe wachtrijbericht in Hallo wachtrij met de naam 'outputqueue' maakt Hello na niet async-codevoorbeeld met dezelfde inhoud als wachtrij het Hallo-bericht in Hallo wachtrij met de naam 'inputqueue ontvangen' Hallo.</span><span class="sxs-lookup"><span data-stu-id="28afd-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="28afd-176">(Gebruik voor asynchrone functies **IAsyncCollector<T>**  zoals later in deze sectie.)</span><span class="sxs-lookup"><span data-stu-id="28afd-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="28afd-177">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="28afd-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="28afd-178">toocreate een wachtrijbericht met een POCO in plaats van een tekenreeks, op te geven Hallo POCO typt als een output-parameter toohello **wachtrij** kenmerkconstructor.</span><span class="sxs-lookup"><span data-stu-id="28afd-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="28afd-179">Hallo SDK serialiseert automatisch Hallo object tooJSON.</span><span class="sxs-lookup"><span data-stu-id="28afd-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="28afd-180">Een wachtrijbericht is altijd gemaakt, zelfs als het Hallo-object is null.</span><span class="sxs-lookup"><span data-stu-id="28afd-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="28afd-181">Meerdere berichten maken of in een async-functies</span><span class="sxs-lookup"><span data-stu-id="28afd-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="28afd-182">toocreate meerdere berichten maken Hallo parametertype voor Hallo uitvoerwachtrij **ICollector<T>**  of **IAsyncCollector<T>**, zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="28afd-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="28afd-183">Het bericht voor elke wachtrij wordt gemaakt bij direct hello **toevoegen** methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="28afd-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="28afd-184">Typen Hallo wachtrij kenmerk werkt met</span><span class="sxs-lookup"><span data-stu-id="28afd-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="28afd-185">U kunt Hallo **wachtrij** -kenmerk op Hallo parametertypen te volgen:</span><span class="sxs-lookup"><span data-stu-id="28afd-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="28afd-186">**uitgaand tekenreeks** (wachtrijbericht maakt als waarde voor de parameter niet null wanneer de functie Hallo eindigt)</span><span class="sxs-lookup"><span data-stu-id="28afd-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="28afd-187">**uitgaand byte []** (werkt als **tekenreeks**)</span><span class="sxs-lookup"><span data-stu-id="28afd-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="28afd-188">**uitgaand CloudQueueMessage** (werkt als **tekenreeks**)</span><span class="sxs-lookup"><span data-stu-id="28afd-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="28afd-189">**uitgaand POCO** (een serialiseerbaar type, maakt u een bericht met een null-object als Hallo-parameter is null wanneer de functie Hallo eindigt)</span><span class="sxs-lookup"><span data-stu-id="28afd-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="28afd-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="28afd-190">**ICollector**</span></span>
* <span data-ttu-id="28afd-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="28afd-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="28afd-192">**CloudQueue** (voor het handmatig maken van berichten met behulp van Hallo API van Azure Storage rechtstreeks)</span><span class="sxs-lookup"><span data-stu-id="28afd-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="28afd-193">Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="28afd-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="28afd-194">Als u toodo moet enkele werken in uw functie voordat u een kenmerk WebJobs SDK, zoals **wachtrij**, **Blob**, of **tabel**, kunt u Hallo **IBinder** interface.</span><span class="sxs-lookup"><span data-stu-id="28afd-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="28afd-195">Hallo volgende voorbeeld wordt een bericht invoerwachtrij en maakt u een nieuw bericht Hello dezelfde inhoud in een wachtrij voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="28afd-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="28afd-196">Hallo uitvoer wachtrijnaam is ingesteld door code in de hoofdtekst van de functie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="28afd-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="28afd-197">Hallo **IBinder** interface kan ook worden gebruikt met Hallo **tabel** en **Blob** kenmerken.</span><span class="sxs-lookup"><span data-stu-id="28afd-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="28afd-198">Hoe tooread en write-blobs en tabellen tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="28afd-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="28afd-199">Hallo **Blob** en **tabel** kenmerken kunt u tooread en blobs en tabellen te schrijven.</span><span class="sxs-lookup"><span data-stu-id="28afd-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="28afd-200">Hallo-voorbeelden in deze sectie tooblobs van toepassing.</span><span class="sxs-lookup"><span data-stu-id="28afd-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="28afd-201">Zie voor codevoorbeelden die laten hoe tootrigger verwerkt zien wanneer BLOB's worden gemaakt of bijgewerkt, [hoe toouse Azure blob-opslag met Hallo WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), en voor codevoorbeelden die lezen en schrijven van tabellen, Zie [hoe toouse Azure-tabel opslag Hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="28afd-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="28afd-202">String, Wachtrijberichten activering van blob-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="28afd-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="28afd-203">Voor een wachtrijbericht met een tekenreeks **queueTrigger** is een tijdelijke aanduiding kunt u in Hallo **Blob** van het kenmerk **blobPath** parameter met inhoud van Hallo Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="28afd-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="28afd-204">Hallo volgende voorbeeld wordt **stroom** tooread en write blobs objecten.</span><span class="sxs-lookup"><span data-stu-id="28afd-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="28afd-205">wachtrij het Hallo-bericht is Hallo-naam van een blob die zich in Hallo textblobs container.</span><span class="sxs-lookup"><span data-stu-id="28afd-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="28afd-206">Een kopie van de blob met Hallo '-nieuwe ' toegevoegde toohello naam wordt gemaakt in Hallo dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="28afd-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="28afd-207">Hallo **Blob** kenmerk constructor heeft een **blobPath** parameter waarmee Hallo-container en de blob-naam.</span><span class="sxs-lookup"><span data-stu-id="28afd-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="28afd-208">Zie voor meer informatie over deze tijdelijke aanduiding [hoe toouse Azure blob-opslag met Hallo WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="28afd-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="28afd-209">Wanneer Hallo kenmerk wordt verfraaid een **stroom** object, een andere constructorparameter geeft u op Hallo **FileAccess** modus lezen, schrijven of lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="28afd-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="28afd-210">Hallo volgende voorbeeld wordt een **CloudBlockBlob** toodelete een blob-object.</span><span class="sxs-lookup"><span data-stu-id="28afd-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="28afd-211">wachtrij het Hallo-bericht is Hallo-naam van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="28afd-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="28afd-212">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="28afd-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="28afd-213">Voor een POCO opgeslagen als JSON in wachtrij het Hallo-bericht, kunt u tijdelijke aanduidingen voor naam van de eigenschappen van het object in Hallo Hallo **wachtrij** van het kenmerk **blobPath** parameter.</span><span class="sxs-lookup"><span data-stu-id="28afd-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="28afd-214">U kunt ook metagegevens-Eigenschapsnamen wachtrij gebruiken als tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="28afd-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="28afd-215">Zie [wachtrij of wachtrij bericht metagegevens ophalen](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="28afd-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="28afd-216">Hallo volgende voorbeeld wordt gekopieerd een blob tooa nieuwe blob met een andere extensie.</span><span class="sxs-lookup"><span data-stu-id="28afd-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="28afd-217">wachtrij het Hallo-bericht is een **BlobInformation** -object met **BlobName** en **BlobNameWithoutExtension** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="28afd-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="28afd-218">eigenschapnamen Hello worden gebruikt als tijdelijke aanduidingen in Hallo blobpad voor Hallo **Blob** kenmerken.</span><span class="sxs-lookup"><span data-stu-id="28afd-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="28afd-219">Hallo SDK maakt gebruik van Hallo [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize en deserialiseren van berichten.</span><span class="sxs-lookup"><span data-stu-id="28afd-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="28afd-220">Als u berichten in wachtrij plaatsen in een programma dat Hallo WebJobs SDK maakt geen gebruik maakt, kunt u code zoals het volgende voorbeeld toocreate een wachtrijbericht POCO Hallo schrijven die Hallo die SDK kan worden geparseerd.</span><span class="sxs-lookup"><span data-stu-id="28afd-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="28afd-221">Als u toodo werken sommige in de functie moet voor het binden van een blob tooan-object, kunt u Hallo kenmerk in de hoofdtekst Hallo van Hallo-functie, zoals wordt weergegeven in [WebJobs SDK gebruiken kenmerken in de hoofdtekst van een functie Hallo](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="28afd-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="28afd-222">Blob-kenmerk met de Hallo kunnen worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="28afd-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="28afd-223">Hallo **Blob** kenmerk kan worden gebruikt met de volgende typen Hallo:</span><span class="sxs-lookup"><span data-stu-id="28afd-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="28afd-224">**Stroom** (lezen of schrijven, opgegeven met behulp van Hallo FileAccess constructorparameter)</span><span class="sxs-lookup"><span data-stu-id="28afd-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="28afd-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="28afd-225">**TextReader**</span></span>
* <span data-ttu-id="28afd-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="28afd-226">**TextWriter**</span></span>
* <span data-ttu-id="28afd-227">**tekenreeks** (gelezen)</span><span class="sxs-lookup"><span data-stu-id="28afd-227">**string** (read)</span></span>
* <span data-ttu-id="28afd-228">**uitgaand tekenreeks** (schrijven, maakt u een blob alleen als Hallo tekenreeksparameter niet-null is bij het Hallo-functie retourneert)</span><span class="sxs-lookup"><span data-stu-id="28afd-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="28afd-229">POCO (lezen)</span><span class="sxs-lookup"><span data-stu-id="28afd-229">POCO (read)</span></span>
* <span data-ttu-id="28afd-230">uitgaand POCO (schrijven; altijd een blob maakt, maakt als null-object als POCO-parameter null is wanneer Hallo functie retourneert)</span><span class="sxs-lookup"><span data-stu-id="28afd-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="28afd-231">**CloudBlobStream** (schrijven)</span><span class="sxs-lookup"><span data-stu-id="28afd-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="28afd-232">**ICloudBlob** (lezen of schrijven)</span><span class="sxs-lookup"><span data-stu-id="28afd-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="28afd-233">**CloudBlockBlob** (lezen of schrijven)</span><span class="sxs-lookup"><span data-stu-id="28afd-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="28afd-234">**CloudPageBlob** (lezen of schrijven)</span><span class="sxs-lookup"><span data-stu-id="28afd-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="28afd-235">Hoe toohandle poison berichten</span><span class="sxs-lookup"><span data-stu-id="28afd-235">How toohandle poison messages</span></span>
<span data-ttu-id="28afd-236">Berichten waarvan de inhoud zorgt ervoor een functie toofail dat worden genoemd *berichten poison*.</span><span class="sxs-lookup"><span data-stu-id="28afd-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="28afd-237">Hallo-functie is mislukt, wachtrij het Hallo-bericht is niet verwijderd als uiteindelijk wordt opgehaald, waardoor Hallo cyclus toobe herhaald.</span><span class="sxs-lookup"><span data-stu-id="28afd-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="28afd-238">Hallo SDK kan automatisch Hallo cyclus worden onderbroken na een beperkt aantal iteraties of u kunt dit handmatig doen.</span><span class="sxs-lookup"><span data-stu-id="28afd-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="28afd-239">Verwerken van verontreinigde berichten automatische</span><span class="sxs-lookup"><span data-stu-id="28afd-239">Automatic poison message handling</span></span>
<span data-ttu-id="28afd-240">Hallo SDK zal een functie van too5 keren tooprocess een wachtrijbericht aanroepen.</span><span class="sxs-lookup"><span data-stu-id="28afd-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="28afd-241">Als de vijfde probeer Hallo mislukt, is het Hallo-bericht verplaatste tooa verontreinigd wachtrij.</span><span class="sxs-lookup"><span data-stu-id="28afd-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="28afd-242">U kunt zien hoe tooconfigure maximum aantal pogingen in Hallo [hoe configuratieopties tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="28afd-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="28afd-243">Hallo verontreinigd wachtrij heet *{originalqueuename}*-verontreinigd.</span><span class="sxs-lookup"><span data-stu-id="28afd-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="28afd-244">U schrijft een functie tooprocess berichten uit Hallo verontreinigd wachtrij registratie of het verzenden van een melding dat handmatige aandacht nodig is.</span><span class="sxs-lookup"><span data-stu-id="28afd-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="28afd-245">In het volgende voorbeeld Hallo Hallo **CopyBlob** functie mislukken wanneer er een wachtrijbericht bevat Hallo-naam van een blob die niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="28afd-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="28afd-246">Wanneer dit gebeurt, wordt het Hallo-bericht wordt verplaatst van Hallo copyblobqueue wachtrij toohello copyblobqueue poison wachtrij.</span><span class="sxs-lookup"><span data-stu-id="28afd-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="28afd-247">Hallo **ProcessPoisonMessage** vervolgens logboeken Hallo verontreinigd bericht.</span><span class="sxs-lookup"><span data-stu-id="28afd-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

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

<span data-ttu-id="28afd-248">Hallo volgende afbeelding ziet u console-uitvoer van deze functies bij het verwerken van een poison-bericht.</span><span class="sxs-lookup"><span data-stu-id="28afd-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![De uitvoer van de console voor het verwerken van verontreinigde berichten](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="28afd-250">Verwerken van verontreinigde berichten handmatige</span><span class="sxs-lookup"><span data-stu-id="28afd-250">Manual poison message handling</span></span>
<span data-ttu-id="28afd-251">U krijgt Hallo aantal keren dat een bericht opgepikt voor verwerking door toe te voegen een **int** parameter met de naam **dequeueCount** tooyour-functie.</span><span class="sxs-lookup"><span data-stu-id="28afd-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="28afd-252">U kunt vervolgens het selectievakje hello telling in functiecode in wachtrij- en uw eigen verontreinigd bericht verwerkt wanneer Hallo nummer een drempelwaarde overschrijdt, zoals wordt weergegeven in het volgende voorbeeld Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="28afd-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="28afd-253">Hoe tooset configuratieopties</span><span class="sxs-lookup"><span data-stu-id="28afd-253">How tooset configuration options</span></span>
<span data-ttu-id="28afd-254">U kunt Hallo **JobHostConfiguration** type tooset Hallo volgende configuratieopties:</span><span class="sxs-lookup"><span data-stu-id="28afd-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="28afd-255">Hallo SDK verbindingsreeksen in code instellen.</span><span class="sxs-lookup"><span data-stu-id="28afd-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="28afd-256">Configureer **QueueTrigger** instellingen zoals het maximum aantal in wachtrij.</span><span class="sxs-lookup"><span data-stu-id="28afd-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="28afd-257">Wachtrijnamen van de ophalen van configuratie.</span><span class="sxs-lookup"><span data-stu-id="28afd-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="28afd-258">SDK-verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="28afd-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="28afd-259">Hallo SDK-verbindingsreeksen instellen in de code kunt u toouse uw eigen namen van de tekenreeks verbindingen in configuratiebestanden of omgevingsvariabelen, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="28afd-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="28afd-260">QueueTrigger instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="28afd-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="28afd-261">U kunt Hallo instellingen die van toepassing toohello wachtrij berichtverwerking volgende configureren:</span><span class="sxs-lookup"><span data-stu-id="28afd-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="28afd-262">maximum aantal berichten die tegelijkertijd toobe parallel uitgevoerd worden opgepikt Hallo (de standaardwaarde is 16).</span><span class="sxs-lookup"><span data-stu-id="28afd-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="28afd-263">Hallo maximum aantal pogingen voordat een wachtrijbericht tooa poison-wachtrij worden verzonden (de standaardwaarde is 5).</span><span class="sxs-lookup"><span data-stu-id="28afd-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="28afd-264">Hallo maximale wachttijd voordat opnieuw polling wanneer een wachtrij leeg is (de standaardwaarde is 1 minuut).</span><span class="sxs-lookup"><span data-stu-id="28afd-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="28afd-265">Hallo volgende voorbeeld wordt getoond hoe tooconfigure deze instellingen:</span><span class="sxs-lookup"><span data-stu-id="28afd-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="28afd-266">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="28afd-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="28afd-267">Soms wilt u toospecify een wachtrijnaam, een blob-naam of de container of een tabel naam in de code in plaats van harde-code.</span><span class="sxs-lookup"><span data-stu-id="28afd-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="28afd-268">U kunt bijvoorbeeld toospecify Hallo wachtrijnaam voor **QueueTrigger** in een configuratie-bestand of de omgeving variabele.</span><span class="sxs-lookup"><span data-stu-id="28afd-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="28afd-269">U kunt dit doen door doorgeven in een **NameResolver** object toohello **JobHostConfiguration** type.</span><span class="sxs-lookup"><span data-stu-id="28afd-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="28afd-270">U speciale tijdelijke aanduidingen omgeven door procent (%) tekens in constructorparameters WebJobs SDK-kenmerk, opnemen en uw **NameResolver** code geeft Hallo werkelijke waarden toobe gebruikt in plaats van de tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="28afd-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="28afd-271">Bijvoorbeeld, Stel dat u wilt dat toouse een wachtrij met de naam logqueuetest in de testomgeving Hallo en één met de naam logqueueprod in productie.</span><span class="sxs-lookup"><span data-stu-id="28afd-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="28afd-272">In plaats van een vastgelegde wachtrijnaam, die u wilt toospecify Hallo-naam van een vermelding in Hallo **appSettings** verzameling die de werkelijke wachtrijnaam Hallo zou hebben.</span><span class="sxs-lookup"><span data-stu-id="28afd-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="28afd-273">Als hello **appSettings** sleutel logqueue is, de functie eruit als Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="28afd-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="28afd-274">Uw **NameResolver** klasse kan vervolgens ophalen Hallo wachtrijnaam van **appSettings** zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="28afd-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="28afd-275">U geeft Hallo **NameResolver** klasse in toohello **JobHost** zoals weergegeven in het volgende voorbeeld Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="28afd-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="28afd-276">**Opmerking:** Queue, table en blob-namen zijn opgelost telkens wanneer een functie wordt aangeroepen, maar de namen van de blob-containers zijn opgelost, alleen wanneer het Hallo-toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="28afd-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="28afd-277">U kunt de naam van de blob-container niet wijzigen terwijl Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="28afd-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="28afd-278">Hoe een functie tootrigger handmatig</span><span class="sxs-lookup"><span data-stu-id="28afd-278">How tootrigger a function manually</span></span>
<span data-ttu-id="28afd-279">een functie tootrigger handmatig hello gebruiken **aanroepen** of **CallAsync** methode op Hallo **JobHost** object en Hallo **NoAutomaticTrigger** het kenmerk op Hallo-functie, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="28afd-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

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

## <a name="how-toowrite-logs"></a><span data-ttu-id="28afd-280">Hoe toowrite registreert</span><span class="sxs-lookup"><span data-stu-id="28afd-280">How toowrite logs</span></span>
<span data-ttu-id="28afd-281">Hallo Dashboard ziet u Logboeken op twee plaatsen: Hallo-pagina voor Hallo webtaak en Hallo-pagina voor een specifieke webtaak-aanroep.</span><span class="sxs-lookup"><span data-stu-id="28afd-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Logboeken in webtaak pagina](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Logboeken op de pagina voor functie-aanroep](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="28afd-284">De uitvoer van de Console-methoden die u in een functie of Hallo aanroepen **Main()** wordt weergegeven in de dashboardpagina Hallo voor Hallo webtaak, niet in Hallo-pagina voor een bepaalde methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="28afd-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="28afd-285">Uitvoer van Hallo TextWriter object die u via een parameter in de methodehandtekening weergegeven in de dashboardpagina Hallo voor een methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="28afd-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="28afd-286">Console-uitvoer kan niet worden bepaald gekoppelde tooa de methodeaanroep omdat Hallo Console één thread, terwijl veel functies kunnen worden uitgevoerd op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="28afd-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="28afd-287">Daarom is Hallo SDK biedt elke functieaanroep met een eigen unieke logboek writer-object.</span><span class="sxs-lookup"><span data-stu-id="28afd-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="28afd-288">toowrite [logboeken voor tracering van toepassing](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), gebruik **Console.Out** (maakt logboeken die zijn gemarkeerd als INFO) en **Console.Error** (logboeken die zijn gemarkeerd als fout maakt).</span><span class="sxs-lookup"><span data-stu-id="28afd-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="28afd-289">Een alternatief is toouse [tracering of TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)en waarmee u uitgebreid, waarschuwing, kritiek niveaus in de toevoeging tooInfo en de fout.</span><span class="sxs-lookup"><span data-stu-id="28afd-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="28afd-290">Logboeken voor tracering van toepassing worden weergegeven in Hallo web app-logboekbestanden, Azure-tabellen, of Azure blobs, afhankelijk van hoe u uw Azure-web-app configureren.</span><span class="sxs-lookup"><span data-stu-id="28afd-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="28afd-291">Geldt voor alle Console-uitvoer, Hallo meest recente 100-toepassingslogboeken ook worden weergegeven in de dashboardpagina Hallo voor Hallo webtaak, niet Hallo pagina voor een functie-aanroep.</span><span class="sxs-lookup"><span data-stu-id="28afd-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="28afd-292">Console-uitvoer wordt weergegeven in Hallo Dashboard alleen als Hallo programma wordt uitgevoerd in een Azure-webtaak niet als Hallo programma lokaal wordt uitgevoerd of in sommige andere omgeving.</span><span class="sxs-lookup"><span data-stu-id="28afd-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="28afd-293">U kunt logboekregistratie uitschakelen door in te stellen Hallo Dashboard connection string toonull.</span><span class="sxs-lookup"><span data-stu-id="28afd-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="28afd-294">Zie voor meer informatie [hoe tooset configuratieopties](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="28afd-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="28afd-295">Hallo volgende voorbeeld ziet u op verschillende manieren toowrite Logboeken:</span><span class="sxs-lookup"><span data-stu-id="28afd-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="28afd-296">Hallo in Hallo WebJobs SDK-Dashboard, uitvoer van Hallo **TextWriter** object wordt wanneer u toohello pagina voor een bepaalde gaat functie aanroepen en selecteer **wisselknop uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="28afd-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![Het aanroepen van koppeling](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Logboeken op de pagina voor functie-aanroep](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="28afd-299">In Hallo WebJobs SDK-Dashboard, Hallo meest recente 100 regels van de Console uitvoer weergeven van wanneer u toohello pagina voor Hallo webtaak (niet voor functie-aanroep Hallo gaat) en selecteer **wisselknop uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="28afd-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![Uitvoer van de in-of uitschakelen](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="28afd-301">In een doorlopende webtaak toepassingslogboeken weergegeven in/data/taken/continue/*{webjobname}*/job_log.txt in Hallo web-app-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="28afd-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="28afd-302">In een Azure blob-toepassing hello logboeken moeten uitzien: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, fout, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="28afd-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="28afd-303">En in een Azure-tabel Hallo **Console.Out** en **Console.Error** logboeken moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="28afd-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![Logboek van de gegevens in de tabel](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Foutenlogboek in tabel](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="28afd-306">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="28afd-306">Next steps</span></span>
<span data-ttu-id="28afd-307">In dit artikel hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="28afd-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="28afd-308">Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="28afd-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

