---
title: .NET-klassebibliotheken gebruiken met Azure Functions | Microsoft Docs
description: Meer informatie over het ontwerpen van .NET-klassebibliotheken voor gebruik met Azure Functions
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
ms.openlocfilehash: 0613bb96d3afb85ff7e684246b128e4eef518d23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="ab4ed-104">Met behulp van .NET-klassebibliotheken met Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ab4ed-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="ab4ed-105">Naast de scriptbestanden, Azure Functions ondersteunt een class-bibliotheek publiceren als de uitvoering voor een of meer functies.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-105">In addition to script files, Azure Functions supports publishing a class library as the implementation for one or more functions.</span></span> <span data-ttu-id="ab4ed-106">Het is raadzaam dat u de [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-106">We recommend that you use the [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab4ed-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ab4ed-107">Prerequisites</span></span> 

<span data-ttu-id="ab4ed-108">In dit artikel heeft de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-108">This article has the following prerequisites:</span></span>

- <span data-ttu-id="ab4ed-109">[Visual Studio 2017 15,3 Preview](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="ab4ed-110">Installeren van de werkbelastingen **ASP.NET en web ontwikkeling** en **ontwikkelen van Azure**.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-110">Install the workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="ab4ed-111">Azure-functie hulpprogramma's voor Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ab4ed-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="ab4ed-112">Functies class library-project</span><span class="sxs-lookup"><span data-stu-id="ab4ed-112">Functions class library project</span></span>

<span data-ttu-id="ab4ed-113">Vanuit Visual Studio een nieuw Azure Functions-project te maken.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="ab4ed-114">Het nieuwe projectsjabloon maakt u de bestanden *host.json* en *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-114">The new project template creates the files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="ab4ed-115">U kunt [aanpassen van Azure Functions-runtime-instellingen in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="ab4ed-116">Het bestand *local.settings.json* app-instellingen, verbindingsreeksen en instellingen voor Azure Functions Core hulpprogramma's worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-116">The file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="ab4ed-117">Zie voor meer informatie over de structuur, [Code en testen van Azure functions lokaal](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-117">To learn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="ab4ed-118">Functienaam kenmerk</span><span class="sxs-lookup"><span data-stu-id="ab4ed-118">FunctionName attribute</span></span>

<span data-ttu-id="ab4ed-119">Het kenmerk [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) markeert een methode als een functie-ingangspunt.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-119">The attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="ab4ed-120">Deze moet worden gebruikt met exact één trigger en 0 of meer invoer en uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-to-functionjson"></a><span data-ttu-id="ab4ed-121">Conversie naar function.json</span><span class="sxs-lookup"><span data-stu-id="ab4ed-121">Conversion to function.json</span></span>

<span data-ttu-id="ab4ed-122">Wanneer u een Azure Functions-project is gebouwd, maakt het bestand `function.json` in de map die overeenkomt met de naam van de functie gedefinieerd door `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-122">When an Azure Functions project is built, it produces a file `function.json` in the directory matching the function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="ab4ed-123">Geeft aan triggers en bindingen en verwijst naar het project assembly-bestand.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-123">It specifies triggers and bindings and points to the project assembly file.</span></span>

<span data-ttu-id="ab4ed-124">Deze conversie wordt uitgevoerd door het NuGet-pakket [Microsoft\.NET\.Sdk\.functies](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-124">This conversion is performed by the NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="ab4ed-125">De bron is beschikbaar in de GitHub-repo [azure\-functies\-tegenover\-bouwen\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-125">The source is available in the GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="ab4ed-126">Triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="ab4ed-126">Triggers and bindings</span></span>

<span data-ttu-id="ab4ed-127">De volgende tabel bevat de triggers en bindingen die beschikbaar in een Azure Functions class library-project zijn.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-127">The following table lists the triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="ab4ed-128">Alle kenmerken zijn in de naamruimte `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-128">All attributes are in the namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="ab4ed-129">Binding</span><span class="sxs-lookup"><span data-stu-id="ab4ed-129">Binding</span></span> | <span data-ttu-id="ab4ed-130">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="ab4ed-130">Attribute</span></span> | <span data-ttu-id="ab4ed-131">NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="ab4ed-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="ab4ed-132">BLOB storage trigger, invoer, uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="ab4ed-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ab4ed-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="ab4ed-135">[Blobopslag]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-135">[Blob storage]</span></span> |
| [<span data-ttu-id="ab4ed-136">Cosmos DB invoer en uitvoer van de binding</span><span class="sxs-lookup"><span data-stu-id="ab4ed-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="ab4ed-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="ab4ed-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="ab4ed-139">Event Hubs-trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="ab4ed-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="ab4ed-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="ab4ed-142">Bestand met externe invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="ab4ed-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="ab4ed-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="ab4ed-145">HTTP- en webhook trigger</span><span class="sxs-lookup"><span data-stu-id="ab4ed-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="ab4ed-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="ab4ed-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="ab4ed-148">Mobile Apps-invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="ab4ed-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="ab4ed-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="ab4ed-151">Notification Hubs-uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="ab4ed-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="ab4ed-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="ab4ed-154">Queue storage trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="ab4ed-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ab4ed-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="ab4ed-157">SendGrid-uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="ab4ed-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-158">[SendGridAttribute]</span></span> | <span data-ttu-id="ab4ed-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="ab4ed-160">Service Bus-trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="ab4ed-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="ab4ed-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="ab4ed-163">Table storage invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="ab4ed-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ab4ed-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="ab4ed-166">Timertrigger</span><span class="sxs-lookup"><span data-stu-id="ab4ed-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="ab4ed-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="ab4ed-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="ab4ed-169">Twilio-uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="ab4ed-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="ab4ed-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="ab4ed-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="ab4ed-172">BLOB storage trigger, invoer en uitvoer bindingen</span><span class="sxs-lookup"><span data-stu-id="ab4ed-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="ab4ed-173">Azure Functions ondersteunt worden geactiveerd, invoer en uitvoer van de bindingen voor Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="ab4ed-174">Zie voor meer informatie over expressies voor gegevensbinding en metagegevens [bindingen van Azure Functions Blob storage](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="ab4ed-175">Een blob-trigger is gedefinieerd met de `[BlobTrigger]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-175">A blob trigger is defined with the `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="ab4ed-176">U kunt het kenmerk `[StorageAccount]` voor het definiëren van het storage-account dat wordt gebruikt door een hele functie of de klasse.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-176">You can use the attribute `[StorageAccount]` to define the storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="ab4ed-177">BLOB-invoer en uitvoer worden gedefinieerd met behulp van de `[Blob]` kenmerk toe, samen met een `FileAccess` parameter die aangeeft lezen of schrijven.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-177">Blob input and output are defined using the `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="ab4ed-178">Het volgende voorbeeld wordt een blob trigger en blob uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-178">The following example uses a blob trigger and blob output binding.</span></span>

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

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="ab4ed-179">Cosmos DB invoer en uitvoer bindingen</span><span class="sxs-lookup"><span data-stu-id="ab4ed-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="ab4ed-180">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="ab4ed-181">Zie voor meer informatie over de functies van de Cosmos-DB-binding, [bindingen van Azure Functions Cosmos DB](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-181">To learn more about the features of the Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="ab4ed-182">Als u wilt koppelen aan een Cosmos-DB-document, gebruikt u het kenmerk `[DocumentDB]` in het NuGet-pakket [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-182">To bind to a Cosmos DB document, use the attribute `[DocumentDB]` in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="ab4ed-183">Het volgende voorbeeld heeft de trigger van een wachtrij en een DocumentDB-API binding uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-183">The following example has a queue trigger and a DocumentDB API output binding:</span></span>

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

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="ab4ed-184">Event Hubs-trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="ab4ed-185">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="ab4ed-186">Zie voor meer informatie [bindingen van Azure Functions Event Hub](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="ab4ed-187">De typen `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` en `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` zijn gedefinieerd in het NuGet-pakket [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-187">The types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="ab4ed-188">Het volgende voorbeeld wordt een Event Hub-trigger:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-188">The following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="ab4ed-189">Het volgende voorbeeld heeft een Event Hub uitvoer met behulp van de geretourneerde waarde van de methode als uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-189">The following example has an Event Hub output, using the method return value as the output:</span></span>

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

### <a name="external-file-input-and-output"></a><span data-ttu-id="ab4ed-190">Bestand met externe invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-190">External file input and output</span></span>

<span data-ttu-id="ab4ed-191">Azure Functions ondersteunt trigger, invoer en uitvoer bindingen voor externe bestanden, zoals Google Drive, Dropbox en OneDrive.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="ab4ed-192">Zie voor meer informatie, [bindingen van Azure Functions-bestand met externe](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-192">To learn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="ab4ed-193">De kenmerken `[ExternalFileTrigger]` en `[ExternalFile]` zijn gedefinieerd in het NuGet-pakket [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-193">The attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="ab4ed-194">De volgende C#-voorbeeld wordt een bestand met externe invoer en uitvoer van de binding.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-194">The following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="ab4ed-195">De code wordt het bestand voor invoer gekopieerd naar het uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-195">The code copies the input file to the output file.</span></span>

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

### <a name="http-and-webhooks"></a><span data-ttu-id="ab4ed-196">HTTP en webhooks</span><span class="sxs-lookup"><span data-stu-id="ab4ed-196">HTTP and webhooks</span></span>

<span data-ttu-id="ab4ed-197">Gebruik de `HttpTrigger` kenmerk voor het definiëren van een HTTP-trigger of webhook.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-197">Use the `HttpTrigger` attribute to define an HTTP trigger or webhook.</span></span> <span data-ttu-id="ab4ed-198">Dit kenmerk wordt gedefinieerd in het NuGet-pakket [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-198">This attribute is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="ab4ed-199">U kunt de autorisatieniveau, webhook-type, route en methoden.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-199">You can customize the authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="ab4ed-200">Het volgende voorbeeld definieert een HTTP-trigger met anonieme verificatie en _genericJson_ webhook-type.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-200">The following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="ab4ed-201">Mobile Apps-invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-201">Mobile Apps input and output</span></span>

<span data-ttu-id="ab4ed-202">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor mobiele Apps.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="ab4ed-203">Zie voor meer informatie, [mobiele Apps van Azure Functions bindingen](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-203">To learn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="ab4ed-204">Het kenmerk `[MobileTable]` is gedefinieerd in het NuGet-pakket [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-204">The attribute `[MobileTable]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="ab4ed-205">Het volgende voorbeeld toont een Mobile Apps binding uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-205">The following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="ab4ed-206">Notification Hubs-uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-206">Notification Hubs output</span></span>

<span data-ttu-id="ab4ed-207">Azure Functions ondersteunt een uitvoer-binding voor Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="ab4ed-208">Zie voor meer informatie, [Azure Functions Notification Hub uitvoer binding](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-208">To learn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="ab4ed-209">Het kenmerk `[NotificationHub]` is gedefinieerd in het NuGet-pakket [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-209">The attribute `[NotificationHub]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="ab4ed-210">Queue storage trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-210">Queue storage trigger and output</span></span>

<span data-ttu-id="ab4ed-211">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Azure wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="ab4ed-212">Zie voor meer informatie [bindingen van Azure Functions Queue Storage](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="ab4ed-213">Het volgende voorbeeld ziet u hoe u het retourtype van functie met de uitvoer van een wachtrij binding, met behulp van de `[Queue]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-213">The following example shows how to use the function return type with a queue output binding, using the `[Queue]` attribute.</span></span> <span data-ttu-id="ab4ed-214">Gebruik het definiëren van een trigger voor de wachtrij de `[QueueTrigger]` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-214">To define a queue trigger, use the `[QueueTrigger]` attribute.</span></span>

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

### <a name="sendgrid-output"></a><span data-ttu-id="ab4ed-215">SendGrid-uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-215">SendGrid output</span></span>

<span data-ttu-id="ab4ed-216">Azure Functions ondersteunt een SendGrid-uitvoer binding voor het programmatisch verzenden van e-mail.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="ab4ed-217">Zie voor meer informatie, [bindingen van Azure Functions SendGrid](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-217">To learn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="ab4ed-218">Het kenmerk `[SendGrid]` is gedefinieerd in het NuGet-pakket [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-218">The attribute `[SendGrid]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="ab4ed-219">Hieronder volgt een voorbeeld van een Service Bus-wachtrij-trigger gebruikt en een SendGrid uitvoer binding met `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-219">The following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

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
    public string To { get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="ab4ed-220">Service Bus-trigger en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-220">Service Bus trigger and output</span></span>

<span data-ttu-id="ab4ed-221">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Service Bus-wachtrijen en onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="ab4ed-222">Zie voor meer informatie over het configureren van bindingen [bindingen van Azure Functions Service Bus](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="ab4ed-223">De kenmerken `[ServiceBusTrigger]` en `[ServiceBus]` zijn gedefinieerd in het NuGet-pakket [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-223">The attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="ab4ed-224">Hier volgt een voorbeeld van een Service Bus-wachtrij trigger:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-224">The following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="ab4ed-225">Hier volgt een voorbeeld van een Service Bus-uitvoer binding, met behulp van het retourtype van methode als uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-225">The following is an example of a Service Bus output binding, using the method return type as the output:</span></span>

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

### <a name="table-storage-input-and-output"></a><span data-ttu-id="ab4ed-226">Table storage invoer en uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-226">Table storage input and output</span></span>

<span data-ttu-id="ab4ed-227">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="ab4ed-228">Zie voor meer informatie, [bindingen van Azure Functions Table storage](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-228">To learn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="ab4ed-229">Het volgende voorbeeld is een klasse met twee functies, tabeluitvoer van opslag en invoer bindingen te demonstreren.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-229">The following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

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

    // use the metadata parameter "queueTrigger" to bind the queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="ab4ed-230">Timertrigger</span><span class="sxs-lookup"><span data-stu-id="ab4ed-230">Timer trigger</span></span>

<span data-ttu-id="ab4ed-231">Azure Functions heeft een timer trigger binding waarmee u de functiecode op basis van een ingesteld schema uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="ab4ed-232">Zie voor meer informatie over de functies van de binding, [plannen van de uitvoering van code met Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-232">To learn more about the features of the binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="ab4ed-233">Op het plan verbruik, kunt u schema's met een [CRON expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-233">On the Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="ab4ed-234">Als u een App Service-abonnement, kunt u ook een TimeSpan-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="ab4ed-235">Het volgende voorbeeld definieert een timertrigger die wordt uitgevoerd om de 5 minuten:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-235">The following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="ab4ed-236">Twilio-uitvoer</span><span class="sxs-lookup"><span data-stu-id="ab4ed-236">Twilio output</span></span>

<span data-ttu-id="ab4ed-237">Azure Functions ondersteunt Twilio uitvoer bindingen zodat uw functies SMS-berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="ab4ed-237">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages.</span></span> <span data-ttu-id="ab4ed-238">Zie voor meer informatie, [verzenden SMS-berichten van de functies van Azure met behulp van de Twilio uitvoer binding](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-238">To learn more, see [Send SMS messages from Azure Functions using the Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="ab4ed-239">Het kenmerk `[TwilioSms]` is gedefinieerd in het pakket [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="ab4ed-239">The attribute `[TwilioSms]` is defined in the package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="ab4ed-240">Het volgende C#-voorbeeld wordt een wachtrij trigger en een Twilio binding uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ab4ed-240">The following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        To = order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="ab4ed-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ab4ed-241">Next steps</span></span>

<span data-ttu-id="ab4ed-242">Zie voor meer informatie over het gebruik van Azure Functions in C# scripting [Azure Functions C\# referentie voor ontwikkelaars script](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="ab4ed-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
<span data-ttu-id="ab4ed-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span></span>
<span data-ttu-id="ab4ed-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span></span>
<span data-ttu-id="ab4ed-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="ab4ed-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span></span>
<span data-ttu-id="ab4ed-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span></span>
<span data-ttu-id="ab4ed-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="ab4ed-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span></span>
<span data-ttu-id="ab4ed-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span></span>
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
<span data-ttu-id="ab4ed-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span><span class="sxs-lookup"><span data-stu-id="ab4ed-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span></span>
<span data-ttu-id="ab4ed-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span></span>
<span data-ttu-id="ab4ed-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="ab4ed-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span></span>


<!-- Links to source --> 
<span data-ttu-id="ab4ed-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span></span>
<span data-ttu-id="ab4ed-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span></span>
<span data-ttu-id="ab4ed-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span></span>
<span data-ttu-id="ab4ed-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span></span>
<span data-ttu-id="ab4ed-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span><span class="sxs-lookup"><span data-stu-id="ab4ed-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span></span>
<span data-ttu-id="ab4ed-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span></span>
<span data-ttu-id="ab4ed-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span></span>
<span data-ttu-id="ab4ed-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span></span>
<span data-ttu-id="ab4ed-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span></span>
<span data-ttu-id="ab4ed-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span></span>
<span data-ttu-id="ab4ed-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span></span>
<span data-ttu-id="ab4ed-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span></span>
<span data-ttu-id="ab4ed-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span></span>
<span data-ttu-id="ab4ed-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span></span>
<span data-ttu-id="ab4ed-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span></span>
<span data-ttu-id="ab4ed-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="ab4ed-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span></span>
