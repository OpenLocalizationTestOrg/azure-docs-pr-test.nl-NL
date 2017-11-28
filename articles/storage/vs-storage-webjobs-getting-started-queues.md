---
title: Aan de slag met de opslag van de wachtrij en Visual Studio verbonden services (webtaak projecten) | Microsoft Docs
description: Hoe u aan de slag met Azure Queue storage in een project webtaak nadat u verbinding met een opslagaccount met Visual Studio hebt verbonden services.
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: abd4814c099620345e04833e14dafd38432064e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="d17eb-103">Aan de slag met Azure Queue storage en Visual Studio verbonden services (webtaak projecten)</span><span class="sxs-lookup"><span data-stu-id="d17eb-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="d17eb-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d17eb-104">Overview</span></span>
<span data-ttu-id="d17eb-105">Dit artikel wordt beschreven hoe aan de slag met Azure Queue storage in een project voor Visual Studio Azure webtaak nadat u hebt gemaakt of een Azure storage-account waarnaar wordt verwezen door het gebruik van de Visual Studio **verbonden Services toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d17eb-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="d17eb-106">Wanneer u een opslagaccount toevoegt aan een project webtaak met behulp van de Visual Studio **verbonden Services toevoegen** dialoogvenster de juiste Azure Storage NuGet-pakketten zijn geïnstalleerd, de juiste .NET-verwijzingen worden toegevoegd aan het project en verbindingsreeksen voor het opslagaccount worden bijgewerkt in het bestand App.config.</span><span class="sxs-lookup"><span data-stu-id="d17eb-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="d17eb-107">Dit artikel vindt u C#-codevoorbeelden die laten zien hoe de Azure WebJobs SDK-versie 1.x met de Azure Queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="d17eb-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="d17eb-108">Azure Queue Storage is een service voor de opslag van grote aantallen berichten die via HTTP of HTTPS overal vandaan kunnen worden opgevraagd met geverifieerde aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="d17eb-109">Een enkel wachtrijbericht mag maximaal 64 KB groot zijn en een wachtrij kan miljoenen berichten bevatten, tot de totale capaciteitslimiet van een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d17eb-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="d17eb-110">Zie [aan de slag met Azure Queue Storage met .NET](storage-dotnet-how-to-use-queues.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d17eb-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="d17eb-111">Zie voor meer informatie over ASP.NET [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="d17eb-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="d17eb-112">Het activeren van een functie wanneer er een wachtrijbericht wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="d17eb-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="d17eb-113">Voor het schrijven van een functie waarmee de WebJobs SDK wordt aangeroepen wanneer een wachtrijbericht wordt ontvangen, gebruik de **QueueTrigger** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="d17eb-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="d17eb-114">De kenmerkconstructor tekenreeksparameter een waarmee de naam van de wachtrij om te pollen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="d17eb-115">Bekijk informatie over het instellen van de wachtrijnaam dynamisch, [het instellen van configuratie-opties](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="d17eb-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="d17eb-116">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="d17eb-116">String queue messages</span></span>
<span data-ttu-id="d17eb-117">In het volgende voorbeeld bevat de wachtrij een string-bericht, dus **QueueTrigger** wordt toegepast op een tekenreeksparameter gebruikt met de naam **logMessage** die de inhoud van het bericht uit de wachtrij bevat.</span><span class="sxs-lookup"><span data-stu-id="d17eb-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="d17eb-118">De functie [een logboekbericht schrijft naar het Dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="d17eb-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="d17eb-119">Naast **tekenreeks**, de parameter is mogelijk een bytematrix een **CloudQueueMessage** object of een POCO die u definieert.</span><span class="sxs-lookup"><span data-stu-id="d17eb-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="d17eb-120">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="d17eb-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d17eb-121">In het volgende voorbeeld bevat de wachtrijbericht JSON voor een **BlobInformation** object waaronder een **BlobName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d17eb-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="d17eb-122">De SDK deserializes automatisch het object.</span><span class="sxs-lookup"><span data-stu-id="d17eb-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="d17eb-123">De SDK gebruikt de [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) voor het serialiseren en deserialiseren van berichten.</span><span class="sxs-lookup"><span data-stu-id="d17eb-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="d17eb-124">Als u berichten in wachtrij plaatsen in een programma dat geen gebruik maakt van de WebJobs SDK maakt, kunt u code op het volgende voorbeeld voor het maken van een wachtrijbericht POCO die kan worden geparseerd met de SDK schrijven.</span><span class="sxs-lookup"><span data-stu-id="d17eb-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="d17eb-125">Async-functies</span><span class="sxs-lookup"><span data-stu-id="d17eb-125">Async functions</span></span>
<span data-ttu-id="d17eb-126">De volgende async-functie [een logboek wordt geschreven naar het Dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="d17eb-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="d17eb-127">Async-functies kunnen duren voordat een [annulering token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), zoals wordt weergegeven in het volgende voorbeeld die een blob kopieert.</span><span class="sxs-lookup"><span data-stu-id="d17eb-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="d17eb-128">(Voor een uitleg van de **queueTrigger** tijdelijke aanduiding, Zie de [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sectie.)</span><span class="sxs-lookup"><span data-stu-id="d17eb-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="d17eb-129">Het kenmerk QueueTrigger met werkt typen</span><span class="sxs-lookup"><span data-stu-id="d17eb-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="d17eb-130">U kunt **QueueTrigger** met de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="d17eb-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="d17eb-131">**tekenreeks**</span><span class="sxs-lookup"><span data-stu-id="d17eb-131">**string**</span></span>
* <span data-ttu-id="d17eb-132">Een POCO-type dat geserialiseerd als JSON</span><span class="sxs-lookup"><span data-stu-id="d17eb-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="d17eb-133">**byte]**</span><span class="sxs-lookup"><span data-stu-id="d17eb-133">**byte[]**</span></span>
* <span data-ttu-id="d17eb-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="d17eb-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="d17eb-135">Polling-algoritme</span><span class="sxs-lookup"><span data-stu-id="d17eb-135">Polling algorithm</span></span>
<span data-ttu-id="d17eb-136">De SDK implementeert een willekeurige exponentiële back-off-algoritme het effect van niet-actieve wachtrij op de opslagkosten transaction polling beperkt.</span><span class="sxs-lookup"><span data-stu-id="d17eb-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="d17eb-137">Wanneer een bericht is gevonden, de SDK Wacht twee seconden en wordt er gecontroleerd of een ander bericht; Wanneer er geen bericht is gevonden wacht ongeveer vier seconden alvorens het opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="d17eb-138">Na meerdere mislukte pogingen om op te halen van een wachtrijbericht blijft de wachttijd verhogen totdat het de maximale wachttijd, die standaard één minuut bereikt.</span><span class="sxs-lookup"><span data-stu-id="d17eb-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="d17eb-139">[De maximale wachttijd is configureerbaar](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="d17eb-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="d17eb-140">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="d17eb-140">Multiple instances</span></span>
<span data-ttu-id="d17eb-141">Als uw web-app wordt uitgevoerd op meerdere exemplaren, een doorlopende webtaken uitvoert op elke machine en elke computer wordt gewacht op triggers en probeert uit te voeren van functies.</span><span class="sxs-lookup"><span data-stu-id="d17eb-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="d17eb-142">In sommige gevallen is die dit kan leiden tot sommige functies die twee keer dezelfde gegevens verwerken, dus functies moet idempotent (geschreven zodat meerdere keren aanroepen met de dezelfde invoergegevens geen dubbele resultaten levert).</span><span class="sxs-lookup"><span data-stu-id="d17eb-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="d17eb-143">Parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="d17eb-143">Parallel execution</span></span>
<span data-ttu-id="d17eb-144">Als er meerdere functies luistert naar verschillende wachtrijen, wordt de SDK aangeroepen ze parallel wanneer berichten tegelijkertijd worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="d17eb-145">Hetzelfde geldt wanneer meerdere berichten worden ontvangen voor een enkele wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d17eb-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="d17eb-146">Standaard is de SDK opgehaald van een batch van 16 Wachtrijberichten tegelijk, en voert de functie die parallel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d17eb-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="d17eb-147">[De batchgrootte is configureerbaar](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="d17eb-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="d17eb-148">Wanneer het aantal verwerkte opgehaald omlaag naar de helft van de batchgrootte van de, wordt de SDK opgehaald van een andere batch en begint met de verwerking van deze berichten.</span><span class="sxs-lookup"><span data-stu-id="d17eb-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="d17eb-149">Daarom is het maximum aantal gelijktijdige berichten worden verwerkt per functie en een half keer de batchgrootte.</span><span class="sxs-lookup"><span data-stu-id="d17eb-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="d17eb-150">Deze limiet is van toepassing afzonderlijk op elke functie die een **QueueTrigger** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="d17eb-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="d17eb-151">Als u geen parallelle uitvoering voor berichten ontvangen voor een wachtrij wilt, moet u de batchgrootte ingesteld op 1.</span><span class="sxs-lookup"><span data-stu-id="d17eb-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="d17eb-152">Wachtrij of wachtrij bericht metagegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="d17eb-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="d17eb-153">U kunt de volgende berichteigenschappen krijgen door parameters toe te voegen aan de methodehandtekening:</span><span class="sxs-lookup"><span data-stu-id="d17eb-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="d17eb-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="d17eb-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="d17eb-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="d17eb-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="d17eb-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="d17eb-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="d17eb-157">**tekenreeks** queueTrigger (de berichttekst bevat)</span><span class="sxs-lookup"><span data-stu-id="d17eb-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="d17eb-158">**tekenreeks** id</span><span class="sxs-lookup"><span data-stu-id="d17eb-158">**string** id</span></span>
* <span data-ttu-id="d17eb-159">**tekenreeks** popReceipt</span><span class="sxs-lookup"><span data-stu-id="d17eb-159">**string** popReceipt</span></span>
* <span data-ttu-id="d17eb-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="d17eb-160">**int** dequeueCount</span></span>

<span data-ttu-id="d17eb-161">Als u samenwerken met de Azure storage-API wilt, u kunt ook toevoegen een **CloudStorageAccount** parameter.</span><span class="sxs-lookup"><span data-stu-id="d17eb-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="d17eb-162">Het volgende voorbeeld worden alle deze metagegevens van een logboek INFO geschreven.</span><span class="sxs-lookup"><span data-stu-id="d17eb-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="d17eb-163">In het voorbeeld bevatten zowel logMessage als queueTrigger de inhoud van het bericht uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d17eb-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="d17eb-164">Hier volgt een voorbeeld-logboekbestanden geschreven door de voorbeeldcode:</span><span class="sxs-lookup"><span data-stu-id="d17eb-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="d17eb-165">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="d17eb-165">Graceful shutdown</span></span>
<span data-ttu-id="d17eb-166">Een functie die wordt uitgevoerd in een doorlopende webtaak kan accepteren een **CancellationToken** parameter waarmee het besturingssysteem naar de functie waarschuwen wanneer de webtaak wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d17eb-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="d17eb-167">U kunt deze melding om ervoor te zorgen dat de functie niet onverwacht beëindigd op een manier die gegevens in een inconsistente status heeft blijven.</span><span class="sxs-lookup"><span data-stu-id="d17eb-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="d17eb-168">Het volgende voorbeeld laat zien hoe om te controleren voor aanstaande webtaak beëindiging in een functie.</span><span class="sxs-lookup"><span data-stu-id="d17eb-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="d17eb-169">**Opmerking:** het Dashboard mogelijk niet correct weergegeven status en de uitvoer van de functies die zijn afgesloten.</span><span class="sxs-lookup"><span data-stu-id="d17eb-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="d17eb-170">Zie voor meer informatie [WebJobs correct afsluiten](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="d17eb-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="d17eb-171">Het maken van een wachtrijbericht tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="d17eb-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="d17eb-172">Voor het schrijven van een functie die een nieuwe wachtrijbericht maakt, gebruikt u de **wachtrij** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="d17eb-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="d17eb-173">Zoals **QueueTrigger**, u doorgeeft in de naam van de wachtrij als een tekenreeks of kunt u [dynamisch naam van de wachtrij ingesteld](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="d17eb-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="d17eb-174">String, Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="d17eb-174">String queue messages</span></span>
<span data-ttu-id="d17eb-175">Het volgende niet-async-codevoorbeeld maakt een nieuwe wachtrijbericht in de wachtrij met de naam 'outputqueue' met dezelfde inhoud als het bericht in de wachtrij ontvangen in de wachtrij met de naam 'inputqueue'.</span><span class="sxs-lookup"><span data-stu-id="d17eb-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="d17eb-176">(Gebruik voor asynchrone functies **IAsyncCollector<T>**  zoals later in deze sectie.)</span><span class="sxs-lookup"><span data-stu-id="d17eb-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="d17eb-177">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="d17eb-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d17eb-178">Voor het maken van een wachtrijbericht met een POCO in plaats van een tekenreeks, geeft u het type POCO als een output-parameter voor de **wachtrij** kenmerkconstructor.</span><span class="sxs-lookup"><span data-stu-id="d17eb-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="d17eb-179">De SDK serialiseert automatisch het object naar JSON.</span><span class="sxs-lookup"><span data-stu-id="d17eb-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="d17eb-180">Een wachtrijbericht is altijd gemaakt, zelfs als het object null is.</span><span class="sxs-lookup"><span data-stu-id="d17eb-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="d17eb-181">Meerdere berichten maken of in een async-functies</span><span class="sxs-lookup"><span data-stu-id="d17eb-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="d17eb-182">Controleer het parametertype voor de wachtrij voor de uitvoer voor het maken van meerdere berichten **ICollector<T>**  of **IAsyncCollector<T>**, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d17eb-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="d17eb-183">Het bericht voor elke wachtrij wordt onmiddellijk gemaakt wanneer de **toevoegen** methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="d17eb-184">Typen die geschikt is voor het kenmerk wachtrij</span><span class="sxs-lookup"><span data-stu-id="d17eb-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="d17eb-185">U kunt de **wachtrij** kenmerk voor de volgende parameter:</span><span class="sxs-lookup"><span data-stu-id="d17eb-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="d17eb-186">**uitgaand tekenreeks** (wachtrijbericht maakt als waarde voor de parameter niet null wanneer de functie eindigt)</span><span class="sxs-lookup"><span data-stu-id="d17eb-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="d17eb-187">**uitgaand byte []** (werkt als **tekenreeks**)</span><span class="sxs-lookup"><span data-stu-id="d17eb-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="d17eb-188">**uitgaand CloudQueueMessage** (werkt als **tekenreeks**)</span><span class="sxs-lookup"><span data-stu-id="d17eb-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="d17eb-189">**uitgaand POCO** (een serialiseerbaar type, maakt u een bericht met een null-object als de parameter is null wanneer de functie wordt beëindigd)</span><span class="sxs-lookup"><span data-stu-id="d17eb-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="d17eb-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="d17eb-190">**ICollector**</span></span>
* <span data-ttu-id="d17eb-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="d17eb-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="d17eb-192">**CloudQueue** (voor het maken van berichten handmatig rechtstreeks met de Azure Storage-API)</span><span class="sxs-lookup"><span data-stu-id="d17eb-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="d17eb-193">Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="d17eb-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="d17eb-194">Als u werken in uw functie wilt voordat u een kenmerk WebJobs SDK, zoals **wachtrij**, **Blob**, of **tabel**, kunt u de **IBinder**interface.</span><span class="sxs-lookup"><span data-stu-id="d17eb-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="d17eb-195">Het volgende voorbeeld wordt een bericht invoerwachtrij en maakt u een nieuw bericht met de inhoud van een wachtrij voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d17eb-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="d17eb-196">De naam van de uitvoer-wachtrij is ingesteld door de code in de hoofdtekst van de functie.</span><span class="sxs-lookup"><span data-stu-id="d17eb-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="d17eb-197">De **IBinder** interface kan ook worden gebruikt met de **tabel** en **Blob** kenmerken.</span><span class="sxs-lookup"><span data-stu-id="d17eb-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="d17eb-198">Hoe kunnen lezen en schrijven van blobs, tabellen en tijdens het verwerken van een wachtrijbericht</span><span class="sxs-lookup"><span data-stu-id="d17eb-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="d17eb-199">De **Blob** en **tabel** kenmerken kunnen u blobs en tabellen lezen en schrijven.</span><span class="sxs-lookup"><span data-stu-id="d17eb-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="d17eb-200">De voorbeelden in deze sectie zijn van toepassing op blobs.</span><span class="sxs-lookup"><span data-stu-id="d17eb-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="d17eb-201">Zie voor codevoorbeelden die laten hoe u zien voor het activeren van processen wanneer BLOB's worden gemaakt of bijgewerkt, [Azure blob storage gebruiken met de WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), en voor codevoorbeelden die lezen en schrijven van tabellen, Zie [het gebruik van Azure-tabel opslag met de WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="d17eb-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="d17eb-202">String, Wachtrijberichten activering van blob-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="d17eb-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="d17eb-203">Voor een wachtrijbericht met een tekenreeks **queueTrigger** is een tijdelijke aanduiding kunt u in de **Blob** van het kenmerk **blobPath** parameter met de inhoud van de Bericht.</span><span class="sxs-lookup"><span data-stu-id="d17eb-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="d17eb-204">Het volgende voorbeeld wordt **stroom** objecten te lezen en schrijven blobs.</span><span class="sxs-lookup"><span data-stu-id="d17eb-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="d17eb-205">Bericht uit de wachtrij is de naam van een blob die zich in de container textblobs.</span><span class="sxs-lookup"><span data-stu-id="d17eb-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="d17eb-206">Een kopie van de blob met '-nieuwe ' toegevoegd aan de naam wordt gemaakt in dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="d17eb-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="d17eb-207">De **Blob** kenmerk constructor heeft een **blobPath** parameter waarmee de container en de blob-naam.</span><span class="sxs-lookup"><span data-stu-id="d17eb-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="d17eb-208">Zie voor meer informatie over deze tijdelijke aanduiding [Azure blob storage gebruiken met de WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="d17eb-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="d17eb-209">Wanneer het kenmerk wordt verfraaid een **stroom** object, een andere constructorparameter geeft u de **FileAccess** modus lezen, schrijven of lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="d17eb-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="d17eb-210">Het volgende voorbeeld wordt een **CloudBlockBlob** object verwijderen van een blob.</span><span class="sxs-lookup"><span data-stu-id="d17eb-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="d17eb-211">Bericht uit de wachtrij is de naam van de blob.</span><span class="sxs-lookup"><span data-stu-id="d17eb-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="d17eb-212">POCO [(Plain oude CLR-Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) berichten in de wachtrij</span><span class="sxs-lookup"><span data-stu-id="d17eb-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="d17eb-213">Voor een POCO opgeslagen als JSON in bericht in de wachtrij, kunt u tijdelijke aanduidingen die eigenschappen van het object in een naam geven de **wachtrij** van het kenmerk **blobPath** parameter.</span><span class="sxs-lookup"><span data-stu-id="d17eb-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="d17eb-214">U kunt ook metagegevens-Eigenschapsnamen wachtrij gebruiken als tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="d17eb-215">Zie [wachtrij of wachtrij bericht metagegevens ophalen](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="d17eb-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="d17eb-216">Het volgende voorbeeld wordt een blob kopieert naar een nieuwe blob met een andere extensie.</span><span class="sxs-lookup"><span data-stu-id="d17eb-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="d17eb-217">Bericht uit de wachtrij is een **BlobInformation** -object met **BlobName** en **BlobNameWithoutExtension** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="d17eb-218">De namen van eigenschappen worden gebruikt als tijdelijke aanduidingen in de blobpad voor de **Blob** kenmerken.</span><span class="sxs-lookup"><span data-stu-id="d17eb-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="d17eb-219">De SDK gebruikt de [Newtonsoft.Json NuGet-pakket](http://www.nuget.org/packages/Newtonsoft.Json) voor het serialiseren en deserialiseren van berichten.</span><span class="sxs-lookup"><span data-stu-id="d17eb-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="d17eb-220">Als u berichten in wachtrij plaatsen in een programma dat geen gebruik maakt van de WebJobs SDK maakt, kunt u code op het volgende voorbeeld voor het maken van een wachtrijbericht POCO die kan worden geparseerd met de SDK schrijven.</span><span class="sxs-lookup"><span data-stu-id="d17eb-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="d17eb-221">Als u werken in de functie wilt voor het binden van een blob naar een object, kunt u het kenmerk in de hoofdtekst van de functie, zoals wordt weergegeven in [WebJobs SDK gebruiken kenmerken in de hoofdtekst van een functie](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="d17eb-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="d17eb-222">U het kenmerk Blob met kunt typen</span><span class="sxs-lookup"><span data-stu-id="d17eb-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="d17eb-223">De **Blob** kenmerk kan worden gebruikt met de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="d17eb-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="d17eb-224">**Stroom** (lezen of schrijven, opgegeven met behulp van de constructorparameter FileAccess)</span><span class="sxs-lookup"><span data-stu-id="d17eb-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="d17eb-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="d17eb-225">**TextReader**</span></span>
* <span data-ttu-id="d17eb-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="d17eb-226">**TextWriter**</span></span>
* <span data-ttu-id="d17eb-227">**tekenreeks** (gelezen)</span><span class="sxs-lookup"><span data-stu-id="d17eb-227">**string** (read)</span></span>
* <span data-ttu-id="d17eb-228">**uitgaand tekenreeks** (schrijven, maakt u een blob alleen als de tekenreeksparameter is een niet-null wanneer de functie retourneert)</span><span class="sxs-lookup"><span data-stu-id="d17eb-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="d17eb-229">POCO (lezen)</span><span class="sxs-lookup"><span data-stu-id="d17eb-229">POCO (read)</span></span>
* <span data-ttu-id="d17eb-230">uitgaand POCO (schrijven; altijd een blob maakt, maakt als null-object als POCO-parameter null is wanneer de functie retourneert)</span><span class="sxs-lookup"><span data-stu-id="d17eb-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="d17eb-231">**CloudBlobStream** (schrijven)</span><span class="sxs-lookup"><span data-stu-id="d17eb-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="d17eb-232">**ICloudBlob** (lezen of schrijven)</span><span class="sxs-lookup"><span data-stu-id="d17eb-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="d17eb-233">**CloudBlockBlob** (lezen of schrijven)</span><span class="sxs-lookup"><span data-stu-id="d17eb-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="d17eb-234">**CloudPageBlob** (lezen of schrijven)</span><span class="sxs-lookup"><span data-stu-id="d17eb-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="d17eb-235">Hoe verontreinigde berichten worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="d17eb-235">How to handle poison messages</span></span>
<span data-ttu-id="d17eb-236">Berichten waarvan de inhoud zorgt ervoor dat een functie mislukken worden genoemd *berichten poison*.</span><span class="sxs-lookup"><span data-stu-id="d17eb-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="d17eb-237">De functie mislukt, bericht uit de wachtrij wordt niet verwijderd als uiteindelijk wordt opgehaald, waardoor de cyclus om te worden herhaald.</span><span class="sxs-lookup"><span data-stu-id="d17eb-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="d17eb-238">De SDK kan automatisch de cyclus worden onderbroken na een beperkt aantal iteraties of u kunt dit handmatig doen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="d17eb-239">Verwerken van verontreinigde berichten automatische</span><span class="sxs-lookup"><span data-stu-id="d17eb-239">Automatic poison message handling</span></span>
<span data-ttu-id="d17eb-240">De SDK worden aanroepen van een functie 5 maal een wachtrijbericht te verwerken.</span><span class="sxs-lookup"><span data-stu-id="d17eb-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="d17eb-241">Als de vijfde poging is mislukt, wordt het bericht wordt verplaatst naar een poison wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d17eb-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="d17eb-242">U kunt zien hoe het configureren van het maximum aantal pogingen in [het instellen van configuratie-opties](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="d17eb-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="d17eb-243">De naam van de wachtrij verontreinigd *{originalqueuename}*-verontreinigd.</span><span class="sxs-lookup"><span data-stu-id="d17eb-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="d17eb-244">U kunt schrijven om een functie verwerken van berichten uit de wachtrij verontreinigd door registratie of het verzenden van een melding dat handmatige aandacht nodig is.</span><span class="sxs-lookup"><span data-stu-id="d17eb-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="d17eb-245">In het volgende voorbeeld de **CopyBlob** functie mislukken wanneer er een wachtrijbericht bevat de naam van een blob die niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="d17eb-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="d17eb-246">Wanneer dit gebeurt, wordt het bericht uit de wachtrij copyblobqueue verplaatst naar de wachtrij copyblobqueue poison.</span><span class="sxs-lookup"><span data-stu-id="d17eb-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="d17eb-247">De **ProcessPoisonMessage** meldt zich dan verontreinigd bericht.</span><span class="sxs-lookup"><span data-stu-id="d17eb-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

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

<span data-ttu-id="d17eb-248">De volgende afbeelding toont console-uitvoer van deze functies bij het verwerken van een poison-bericht.</span><span class="sxs-lookup"><span data-stu-id="d17eb-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![De uitvoer van de console voor het verwerken van verontreinigde berichten](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="d17eb-250">Verwerken van verontreinigde berichten handmatige</span><span class="sxs-lookup"><span data-stu-id="d17eb-250">Manual poison message handling</span></span>
<span data-ttu-id="d17eb-251">U kunt het aantal keren dat een bericht opgepikt voor verwerking ophalen door het toevoegen van een **int** parameter met de naam **dequeueCount** aan de functie.</span><span class="sxs-lookup"><span data-stu-id="d17eb-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="d17eb-252">U kunt controleren van de wachtrij halen telling in functiecode en voer uw eigen verontreinigd bericht verwerkt wanneer meer dan een drempelwaarde, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d17eb-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

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

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="d17eb-253">Het instellen van configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="d17eb-253">How to set configuration options</span></span>
<span data-ttu-id="d17eb-254">U kunt de **JobHostConfiguration** type in te stellen van de volgende configuratieopties:</span><span class="sxs-lookup"><span data-stu-id="d17eb-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="d17eb-255">De SDK-verbindingsreeksen in code instellen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="d17eb-256">Configureer **QueueTrigger** instellingen zoals het maximum aantal in wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d17eb-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="d17eb-257">Wachtrijnamen van de ophalen van configuratie.</span><span class="sxs-lookup"><span data-stu-id="d17eb-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="d17eb-258">SDK-verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="d17eb-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="d17eb-259">Instellen van de SDK-verbindingsreeksen in code kunt u uw eigen namen van de tekenreeks verbindingen in configuratiebestanden of omgevingsvariabelen gebruiken zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d17eb-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="d17eb-260">QueueTrigger instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="d17eb-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="d17eb-261">U kunt de volgende instellingen die betrekking hebben op de berichtverwerking wachtrij configureren:</span><span class="sxs-lookup"><span data-stu-id="d17eb-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="d17eb-262">Het maximum aantal berichten die tegelijkertijd worden opgepikt parallel worden uitgevoerd (de standaardwaarde is 16).</span><span class="sxs-lookup"><span data-stu-id="d17eb-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="d17eb-263">Het maximum aantal pogingen alvorens een wachtrijbericht naar een poison-wachtrij verzonden (de standaardwaarde is 5).</span><span class="sxs-lookup"><span data-stu-id="d17eb-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="d17eb-264">De maximale wachttijd voordat opnieuw polling wanneer een wachtrij leeg is (de standaardwaarde is 1 minuut).</span><span class="sxs-lookup"><span data-stu-id="d17eb-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="d17eb-265">Het volgende voorbeeld ziet u hoe deze instellingen te configureren:</span><span class="sxs-lookup"><span data-stu-id="d17eb-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="d17eb-266">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="d17eb-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="d17eb-267">Soms wilt u de naam van een wachtrij, een blob-naam of -container opgeven of een tabel naam in de code in plaats van harde-code.</span><span class="sxs-lookup"><span data-stu-id="d17eb-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="d17eb-268">Bijvoorbeeld, u wilt mogelijk opgeven de naam van de wachtrij voor **QueueTrigger** in een configuratie-bestand of de omgeving variabele.</span><span class="sxs-lookup"><span data-stu-id="d17eb-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="d17eb-269">U kunt dit doen door doorgeven in een **NameResolver** object toe aan de **JobHostConfiguration** type.</span><span class="sxs-lookup"><span data-stu-id="d17eb-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="d17eb-270">U speciale tijdelijke aanduidingen omgeven door procent (%) tekens in constructorparameters WebJobs SDK-kenmerk, opnemen en uw **NameResolver** code bevat de werkelijke waarden moet worden gebruikt in plaats van de tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="d17eb-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="d17eb-271">Stel dat u wilt gebruiken, een wachtrij met de naam logqueuetest in de testomgeving en een benoemde logqueueprod in productie.</span><span class="sxs-lookup"><span data-stu-id="d17eb-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="d17eb-272">In plaats van een vastgelegde wachtrijnaam, die u wilt opgeven van de naam van een vermelding in de **appSettings** verzameling die de werkelijke wachtrijnaam zou hebben.</span><span class="sxs-lookup"><span data-stu-id="d17eb-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="d17eb-273">Als de **appSettings** sleutel logqueue is, de functie eruit als in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d17eb-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="d17eb-274">Uw **NameResolver** klasse kan vervolgens worden opgehaald uit de naam van de wachtrij **appSettings** zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d17eb-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="d17eb-275">U geeft de **NameResolver** -klasse in voor de **JobHost** object, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d17eb-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="d17eb-276">**Opmerking:** Queue, table en blob-namen zijn opgelost telkens wanneer een functie wordt aangeroepen, maar de namen van de blob-containers zijn opgelost, alleen wanneer de toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d17eb-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="d17eb-277">U kunt de naam van de blob-container niet wijzigen terwijl de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d17eb-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="d17eb-278">Het activeren van een functie handmatig</span><span class="sxs-lookup"><span data-stu-id="d17eb-278">How to trigger a function manually</span></span>
<span data-ttu-id="d17eb-279">Als u wilt een functie handmatig activeren, gebruiken de **aanroepen** of **CallAsync** methode op de **JobHost** object en de **NoAutomaticTrigger** het kenmerk voor de functie, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d17eb-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

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

## <a name="how-to-write-logs"></a><span data-ttu-id="d17eb-280">Het schrijven van Logboeken</span><span class="sxs-lookup"><span data-stu-id="d17eb-280">How to write logs</span></span>
<span data-ttu-id="d17eb-281">Het Dashboard toont de logboeken op twee plaatsen: de pagina voor de webtaak en op de pagina voor een specifieke webtaak-aanroep.</span><span class="sxs-lookup"><span data-stu-id="d17eb-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Logboeken in webtaak pagina](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Logboeken op de pagina voor functie-aanroep](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="d17eb-284">De uitvoer van de Console methoden die u in een functie aanroept of in de **Main()** wordt weergegeven op de pagina Dashboard voor de webtaak, niet op de pagina voor het aanroepen van een bepaalde methode.</span><span class="sxs-lookup"><span data-stu-id="d17eb-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="d17eb-285">De uitvoer van het object TextWriter die u via een parameter in de methodehandtekening wordt weergegeven op de pagina Dashboard voor een methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="d17eb-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="d17eb-286">Console-uitvoer kan niet worden gekoppeld aan een bepaalde methodeaanroep omdat de Console één thread, is terwijl veel functies kunnen worden uitgevoerd op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="d17eb-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="d17eb-287">Daarom is de SDK kunt u elke functieaanroep met een eigen unieke logboek writer-object.</span><span class="sxs-lookup"><span data-stu-id="d17eb-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="d17eb-288">Schrijven van [logboeken voor tracering van toepassing](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), gebruik **Console.Out** (maakt logboeken die zijn gemarkeerd als INFO) en **Console.Error** (logboeken die zijn gemarkeerd als fout maakt).</span><span class="sxs-lookup"><span data-stu-id="d17eb-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="d17eb-289">Een alternatief is [tracering of TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), waarmee u uitgebreid, waarschuwing, en kritieke niveaus naast gegevens en de fout.</span><span class="sxs-lookup"><span data-stu-id="d17eb-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="d17eb-290">Logboeken voor tracering van toepassing worden weergegeven in de logboekbestanden web app, Azure-tabellen, of Azure blobs, afhankelijk van hoe u uw Azure-web-app configureren.</span><span class="sxs-lookup"><span data-stu-id="d17eb-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="d17eb-291">Geldt voor alle Console-uitvoer, weergegeven de meest recente 100 toepassingslogboeken ook in de pagina Dashboard voor de webtaak, niet op de pagina voor een functie-aanroep.</span><span class="sxs-lookup"><span data-stu-id="d17eb-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="d17eb-292">Console-uitvoer wordt weergegeven in het Dashboard alleen als het programma wordt uitgevoerd in een Azure-webtaak niet als het programma lokaal wordt uitgevoerd of in sommige andere omgeving.</span><span class="sxs-lookup"><span data-stu-id="d17eb-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="d17eb-293">U kunt logboekregistratie uitschakelen door de verbindingsreeks Dashboard in te stellen op null.</span><span class="sxs-lookup"><span data-stu-id="d17eb-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="d17eb-294">Zie voor meer informatie [het instellen van configuratie-opties](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="d17eb-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="d17eb-295">Het volgende voorbeeld ziet u schrijven logboeken op verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="d17eb-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="d17eb-296">In de WebJobs SDK-Dashboard de uitvoer van de **TextWriter** object wordt wanneer u naar de pagina voor een bepaalde gaat functie aanroepen en selecteer **wisselknop uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="d17eb-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![Het aanroepen van koppeling](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Logboeken op de pagina voor functie-aanroep](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="d17eb-299">In de WebJobs SDK-Dashboard de meest recente 100 regels van de Console uitvoer weergeven van wanneer u gaat u naar de pagina voor de webtaak (niet voor de functie-aanroep) en selecteer **wisselknop uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="d17eb-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Uitvoer van de in-of uitschakelen](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="d17eb-301">In een doorlopende webtaak toepassingslogboeken weergegeven in/data/taken/continue/*{webjobname}*/job_log.txt in het bestandssysteem van de web-app.</span><span class="sxs-lookup"><span data-stu-id="d17eb-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="d17eb-302">In een Azure blob-de toepassing Logboeken eruit als volgt: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, fout, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="d17eb-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="d17eb-303">En in een Azure-tabel de **Console.Out** en **Console.Error** logboeken moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="d17eb-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![Logboek van de gegevens in de tabel](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Foutenlogboek in tabel](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="d17eb-306">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d17eb-306">Next steps</span></span>
<span data-ttu-id="d17eb-307">In dit artikel is opgegeven codevoorbeelden die laten hoe u veelvoorkomende scenario's zien voor het werken met Azure wachtrijen verwerken.</span><span class="sxs-lookup"><span data-stu-id="d17eb-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="d17eb-308">Zie voor meer informatie over het gebruik van Azure WebJobs en de WebJobs SDK [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d17eb-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

