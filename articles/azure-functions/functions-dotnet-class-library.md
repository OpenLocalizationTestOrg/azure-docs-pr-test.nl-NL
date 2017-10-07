---
title: klasse aaaUsing .NET-bibliotheken met Azure Functions | Microsoft Docs
description: Meer informatie over hoe tooauthor .NET-klassebibliotheken voor gebruiken met Azure Functions
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="8d884-104">Met behulp van .NET-klassebibliotheken met Azure Functions</span><span class="sxs-lookup"><span data-stu-id="8d884-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="8d884-105">Tooscript bestanden, Azure Functions ondersteunt tevens een class-bibliotheek publiceren als Hallo-implementatie voor een of meer functies.</span><span class="sxs-lookup"><span data-stu-id="8d884-105">In addition tooscript files, Azure Functions supports publishing a class library as hello implementation for one or more functions.</span></span> <span data-ttu-id="8d884-106">Het is raadzaam dat u Hallo [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="8d884-106">We recommend that you use hello [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d884-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d884-107">Prerequisites</span></span> 

<span data-ttu-id="8d884-108">In dit artikel heeft Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="8d884-108">This article has hello following prerequisites:</span></span>

- <span data-ttu-id="8d884-109">[Visual Studio 2017 15,3 Preview](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="8d884-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="8d884-110">Hallo werkbelastingen installeren **ASP.NET en web ontwikkeling** en **ontwikkelen van Azure**.</span><span class="sxs-lookup"><span data-stu-id="8d884-110">Install hello workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="8d884-111">Azure-functie hulpprogramma's voor Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8d884-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="8d884-112">Functies class library-project</span><span class="sxs-lookup"><span data-stu-id="8d884-112">Functions class library project</span></span>

<span data-ttu-id="8d884-113">Vanuit Visual Studio een nieuw Azure Functions-project te maken.</span><span class="sxs-lookup"><span data-stu-id="8d884-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="8d884-114">Hallo-nieuw project-sjabloon maakt Hallo bestanden *host.json* en *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="8d884-114">hello new project template creates hello files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="8d884-115">U kunt [aanpassen van Azure Functions-runtime-instellingen in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="8d884-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="8d884-116">Hallo bestand *local.settings.json* app-instellingen, verbindingsreeksen en instellingen voor Azure Functions Core hulpprogramma's worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8d884-116">hello file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="8d884-117">toolearn meer informatie over de structuur, Zie [Code en testen van Azure functions lokaal](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="8d884-117">toolearn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="8d884-118">Functienaam kenmerk</span><span class="sxs-lookup"><span data-stu-id="8d884-118">FunctionName attribute</span></span>

<span data-ttu-id="8d884-119">Hallo-kenmerk [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) markeert een methode als een functie-ingangspunt.</span><span class="sxs-lookup"><span data-stu-id="8d884-119">hello attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="8d884-120">Deze moet worden gebruikt met exact één trigger en 0 of meer invoer en uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="8d884-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-toofunctionjson"></a><span data-ttu-id="8d884-121">Conversie toofunction.json</span><span class="sxs-lookup"><span data-stu-id="8d884-121">Conversion toofunction.json</span></span>

<span data-ttu-id="8d884-122">Wanneer u een Azure Functions-project is gebouwd, maakt het bestand `function.json` in Hallo directory gedefinieerd die overeenkomt met de naam van de functie Hallo door `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="8d884-122">When an Azure Functions project is built, it produces a file `function.json` in hello directory matching hello function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="8d884-123">Geeft aan van triggers en bindingen en punten toohello projectbestand assembly.</span><span class="sxs-lookup"><span data-stu-id="8d884-123">It specifies triggers and bindings and points toohello project assembly file.</span></span>

<span data-ttu-id="8d884-124">Deze conversie wordt uitgevoerd door de NuGet-pakket Hallo [Microsoft\.NET\.Sdk\.functies](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="8d884-124">This conversion is performed by hello NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="8d884-125">Hallo-bron is beschikbaar in de GitHub-repo-Hallo [azure\-functies\-tegenover\-bouwen\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="8d884-125">hello source is available in hello GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="8d884-126">Triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="8d884-126">Triggers and bindings</span></span>

<span data-ttu-id="8d884-127">Hallo volgende tabel bevat Hallo triggers en bindingen die beschikbaar in een Azure Functions class library-project zijn.</span><span class="sxs-lookup"><span data-stu-id="8d884-127">hello following table lists hello triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="8d884-128">Alle kenmerken zijn in de naamruimte Hallo `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="8d884-128">All attributes are in hello namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="8d884-129">Binding</span><span class="sxs-lookup"><span data-stu-id="8d884-129">Binding</span></span> | <span data-ttu-id="8d884-130">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="8d884-130">Attribute</span></span> | <span data-ttu-id="8d884-131">NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="8d884-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="8d884-132">BLOB storage trigger, invoer, uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="8d884-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="8d884-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="8d884-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="8d884-135">[Blobopslag]</span><span class="sxs-lookup"><span data-stu-id="8d884-135">[Blob storage]</span></span> |
| [<span data-ttu-id="8d884-136">Cosmos DB invoer en uitvoer van de binding</span><span class="sxs-lookup"><span data-stu-id="8d884-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="8d884-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="8d884-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="8d884-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="8d884-139">Event Hubs-trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="8d884-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="8d884-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="8d884-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="8d884-142">Bestand met externe invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="8d884-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="8d884-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="8d884-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="8d884-145">HTTP- en webhook trigger</span><span class="sxs-lookup"><span data-stu-id="8d884-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="8d884-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="8d884-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="8d884-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="8d884-148">Mobile Apps-invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="8d884-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="8d884-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="8d884-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="8d884-151">Notification Hubs-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="8d884-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="8d884-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="8d884-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="8d884-154">Queue storage trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="8d884-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="8d884-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="8d884-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="8d884-157">SendGrid-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="8d884-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-158">[SendGridAttribute]</span></span> | <span data-ttu-id="8d884-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="8d884-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="8d884-160">Service Bus-trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="8d884-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="8d884-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="8d884-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="8d884-163">Table storage invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="8d884-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="8d884-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="8d884-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="8d884-166">Timertrigger</span><span class="sxs-lookup"><span data-stu-id="8d884-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="8d884-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="8d884-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="8d884-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="8d884-169">Twilio-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="8d884-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="8d884-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="8d884-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="8d884-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="8d884-172">BLOB storage trigger, invoer en uitvoer bindingen</span><span class="sxs-lookup"><span data-stu-id="8d884-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="8d884-173">Azure Functions ondersteunt worden geactiveerd, invoer en uitvoer van de bindingen voor Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="8d884-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="8d884-174">Zie voor meer informatie over expressies voor gegevensbinding en metagegevens [bindingen van Azure Functions Blob storage](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="8d884-175">Een blob-trigger is gedefinieerd met Hallo `[BlobTrigger]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8d884-175">A blob trigger is defined with hello `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="8d884-176">U kunt Hallo kenmerk `[StorageAccount]` toodefine Hallo storage-account dat wordt gebruikt door een hele functie of de klasse.</span><span class="sxs-lookup"><span data-stu-id="8d884-176">You can use hello attribute `[StorageAccount]` toodefine hello storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="8d884-177">BLOB invoer en uitvoer worden gedefinieerd met behulp van Hallo `[Blob]` kenmerk toe, samen met een `FileAccess` parameter die aangeeft lezen of schrijven.</span><span class="sxs-lookup"><span data-stu-id="8d884-177">Blob input and output are defined using hello `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="8d884-178">Hallo volgende voorbeeld maakt gebruik van een blob-trigger en blob-uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="8d884-178">hello following example uses a blob trigger and blob output binding.</span></span>

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="8d884-179">Cosmos DB invoer en uitvoer bindingen</span><span class="sxs-lookup"><span data-stu-id="8d884-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="8d884-180">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="8d884-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="8d884-181">toolearn meer informatie over het Hallo-functies van de binding van de Cosmos-DB hello, Zie [bindingen van Azure Functions Cosmos DB](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-181">toolearn more about hello features of hello Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="8d884-182">toobind tooa Cosmos-DB-document Hallo kenmerk gebruiken `[DocumentDB]` in NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="8d884-182">toobind tooa Cosmos DB document, use hello attribute `[DocumentDB]` in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="8d884-183">Hallo volgende voorbeeld heeft de trigger van een wachtrij en een DocumentDB-API binding uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8d884-183">hello following example has a queue trigger and a DocumentDB API output binding:</span></span>

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="8d884-184">Event Hubs-trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="8d884-185">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8d884-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="8d884-186">Zie voor meer informatie [bindingen van Azure Functions Event Hub](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="8d884-187">Hallo typen `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` en `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` zijn gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="8d884-187">hello types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="8d884-188">Hallo wordt volgende voorbeeld een Event Hub-trigger.</span><span class="sxs-lookup"><span data-stu-id="8d884-188">hello following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="8d884-189">Hallo heeft volgende voorbeeld een Event Hub uitvoer met behulp van de retourwaarde van de methode Hallo als Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8d884-189">hello following example has an Event Hub output, using hello method return value as hello output:</span></span>

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a><span data-ttu-id="8d884-190">Bestand met externe invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-190">External file input and output</span></span>

<span data-ttu-id="8d884-191">Azure Functions ondersteunt trigger, invoer en uitvoer bindingen voor externe bestanden, zoals Google Drive, Dropbox en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="8d884-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="8d884-192">toolearn meer, Zie [bindingen van Azure Functions-bestand met externe](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-192">toolearn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="8d884-193">Hallo kenmerken `[ExternalFileTrigger]` en `[ExternalFile]` zijn gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="8d884-193">hello attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="8d884-194">Hallo volgende C#-voorbeeld demonstreert een extern bestand invoer en uitvoer van de binding.</span><span class="sxs-lookup"><span data-stu-id="8d884-194">hello following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="8d884-195">Hallo code kopieën Hallo invoerbestand toohello-uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="8d884-195">hello code copies hello input file toohello output file.</span></span>

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a><span data-ttu-id="8d884-196">HTTP en webhooks</span><span class="sxs-lookup"><span data-stu-id="8d884-196">HTTP and webhooks</span></span>

<span data-ttu-id="8d884-197">Gebruik Hallo `HttpTrigger` kenmerk toodefine een HTTP-trigger of webhook.</span><span class="sxs-lookup"><span data-stu-id="8d884-197">Use hello `HttpTrigger` attribute toodefine an HTTP trigger or webhook.</span></span> <span data-ttu-id="8d884-198">Dit kenmerk wordt gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="8d884-198">This attribute is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="8d884-199">U kunt aanpassen autorisatieniveau hello, webhook type route en methoden.</span><span class="sxs-lookup"><span data-stu-id="8d884-199">You can customize hello authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="8d884-200">Hallo volgende voorbeeld definieert een HTTP-trigger met anonieme verificatie en _genericJson_ webhook-type.</span><span class="sxs-lookup"><span data-stu-id="8d884-200">hello following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="8d884-201">Mobile Apps-invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-201">Mobile Apps input and output</span></span>

<span data-ttu-id="8d884-202">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor mobiele Apps.</span><span class="sxs-lookup"><span data-stu-id="8d884-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="8d884-203">toolearn meer, Zie [mobiele Apps van Azure Functions bindingen](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-203">toolearn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="8d884-204">Hallo-kenmerk `[MobileTable]` is gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="8d884-204">hello attribute `[MobileTable]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="8d884-205">Hallo volgende voorbeeld toont een Mobile Apps binding uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8d884-205">hello following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="8d884-206">Notification Hubs-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-206">Notification Hubs output</span></span>

<span data-ttu-id="8d884-207">Azure Functions ondersteunt een uitvoer-binding voor Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="8d884-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="8d884-208">toolearn meer, Zie [Azure Functions Notification Hub uitvoer binding](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-208">toolearn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="8d884-209">Hallo-kenmerk `[NotificationHub]` is gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="8d884-209">hello attribute `[NotificationHub]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="8d884-210">Queue storage trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-210">Queue storage trigger and output</span></span>

<span data-ttu-id="8d884-211">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Azure wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="8d884-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="8d884-212">Zie voor meer informatie [bindingen van Azure Functions Queue Storage](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="8d884-213">Hallo volgende voorbeeld laat zien hoe toouse Hallo functie retourtype met de uitvoer van een wachtrij binding, met behulp van Hallo `[Queue]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8d884-213">hello following example shows how toouse hello function return type with a queue output binding, using hello `[Queue]` attribute.</span></span> <span data-ttu-id="8d884-214">een trigger wachtrij toodefine gebruiken Hallo `[QueueTrigger]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8d884-214">toodefine a queue trigger, use hello `[QueueTrigger]` attribute.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a><span data-ttu-id="8d884-215">SendGrid-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-215">SendGrid output</span></span>

<span data-ttu-id="8d884-216">Azure Functions ondersteunt een SendGrid-uitvoer binding voor het programmatisch verzenden van e-mail.</span><span class="sxs-lookup"><span data-stu-id="8d884-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="8d884-217">toolearn meer, Zie [bindingen van Azure Functions SendGrid](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-217">toolearn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="8d884-218">Hallo-kenmerk `[SendGrid]` is gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="8d884-218">hello attribute `[SendGrid]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="8d884-219">Hallo Hieronder volgt een voorbeeld van een Service Bus-wachtrij-trigger gebruikt en een SendGrid uitvoer binding met `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="8d884-219">hello following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="8d884-220">Service Bus-trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-220">Service Bus trigger and output</span></span>

<span data-ttu-id="8d884-221">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Service Bus-wachtrijen en onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="8d884-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="8d884-222">Zie voor meer informatie over het configureren van bindingen [bindingen van Azure Functions Service Bus](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="8d884-223">Hallo kenmerken `[ServiceBusTrigger]` en `[ServiceBus]` zijn gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="8d884-223">hello attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="8d884-224">Hallo Hieronder volgt een voorbeeld van een Service Bus-wachtrij trigger:</span><span class="sxs-lookup"><span data-stu-id="8d884-224">hello following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="8d884-225">Hallo Hier volgt een voorbeeld van een Service Bus-uitvoer binding, met behulp van Hallo methode retourtype als Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8d884-225">hello following is an example of a Service Bus output binding, using hello method return type as hello output:</span></span>

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a><span data-ttu-id="8d884-226">Table storage invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-226">Table storage input and output</span></span>

<span data-ttu-id="8d884-227">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="8d884-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="8d884-228">toolearn meer, Zie [bindingen van Azure Functions Table storage](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-228">toolearn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="8d884-229">Hallo is volgende voorbeeld een klasse met twee functies, tabeluitvoer van opslag en invoer bindingen te demonstreren.</span><span class="sxs-lookup"><span data-stu-id="8d884-229">hello following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="8d884-230">Timertrigger</span><span class="sxs-lookup"><span data-stu-id="8d884-230">Timer trigger</span></span>

<span data-ttu-id="8d884-231">Azure Functions heeft een timer trigger binding waarmee u de functiecode op basis van een ingesteld schema uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8d884-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="8d884-232">toolearn meer informatie over het Hallo-functies van de binding hello, Zie [plannen van de uitvoering van code met Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-232">toolearn more about hello features of hello binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="8d884-233">Op Hallo verbruik plan, kunt u schema's met een [CRON expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="8d884-233">On hello Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="8d884-234">Als u een App Service-abonnement, kunt u ook een TimeSpan-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="8d884-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="8d884-235">Hallo volgende voorbeeld definieert een timertrigger die wordt uitgevoerd om de 5 minuten:</span><span class="sxs-lookup"><span data-stu-id="8d884-235">hello following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="8d884-236">Twilio-uitvoer</span><span class="sxs-lookup"><span data-stu-id="8d884-236">Twilio output</span></span>

<span data-ttu-id="8d884-237">Azure Functions ondersteunt Twilio uitvoer van de SMS-berichten van functies toosend tooenable bindingen.</span><span class="sxs-lookup"><span data-stu-id="8d884-237">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages.</span></span> <span data-ttu-id="8d884-238">toolearn meer, Zie [verzenden SMS-berichten van Azure Functions Hallo Twilio met uitvoer binding](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-238">toolearn more, see [Send SMS messages from Azure Functions using hello Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="8d884-239">Hallo-kenmerk `[TwilioSms]` is gedefinieerd in Hallo pakket [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="8d884-239">hello attribute `[TwilioSms]` is defined in hello package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="8d884-240">Hallo volgende C#-voorbeeld maakt gebruik van een wachtrij trigger en een Twilio binding uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8d884-240">hello following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="8d884-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d884-241">Next steps</span></span>

<span data-ttu-id="8d884-242">Zie voor meer informatie over het gebruik van Azure Functions in C# scripting [Azure Functions C\# referentie voor ontwikkelaars script](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="8d884-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
