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
# <a name="using-net-class-libraries-with-azure-functions"></a>Met behulp van .NET-klassebibliotheken met Azure Functions

Tooscript bestanden, Azure Functions ondersteunt tevens een class-bibliotheek publiceren als Hallo-implementatie voor een of meer functies. Het is raadzaam dat u Hallo [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).

## <a name="prerequisites"></a>Vereisten 

In dit artikel heeft Hallo volgende vereisten:

- [Visual Studio 2017 15,3 Preview](https://www.visualstudio.com/vs/preview/). Hallo werkbelastingen installeren **ASP.NET en web ontwikkeling** en **ontwikkelen van Azure**.
- [Azure-functie hulpprogramma's voor Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a>Functies class library-project

Vanuit Visual Studio een nieuw Azure Functions-project te maken. Hallo-nieuw project-sjabloon maakt Hallo bestanden *host.json* en *local.settings.json*. U kunt [aanpassen van Azure Functions-runtime-instellingen in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json). 

Hallo bestand *local.settings.json* app-instellingen, verbindingsreeksen en instellingen voor Azure Functions Core hulpprogramma's worden opgeslagen. toolearn meer informatie over de structuur, Zie [Code en testen van Azure functions lokaal](functions-run-local.md#local-settings).

### <a name="functionname-attribute"></a>Functienaam kenmerk

Hallo-kenmerk [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) markeert een methode als een functie-ingangspunt. Deze moet worden gebruikt met exact één trigger en 0 of meer invoer en uitvoer bindingen.

### <a name="conversion-toofunctionjson"></a>Conversie toofunction.json

Wanneer u een Azure Functions-project is gebouwd, maakt het bestand `function.json` in Hallo directory gedefinieerd die overeenkomt met de naam van de functie Hallo door `[FunctionName]`. Geeft aan van triggers en bindingen en punten toohello projectbestand assembly.

Deze conversie wordt uitgevoerd door de NuGet-pakket Hallo [Microsoft\.NET\.Sdk\.functies](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions). Hallo-bron is beschikbaar in de GitHub-repo-Hallo [azure\-functies\-tegenover\-bouwen\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## <a name="triggers-and-bindings"></a>Triggers en bindingen

Hallo volgende tabel bevat Hallo triggers en bindingen die beschikbaar in een Azure Functions class library-project zijn. Alle kenmerken zijn in de naamruimte Hallo `Microsoft.Azure.WebJobs`.

| Binding | Kenmerk | NuGet-pakket |
|------   | ------    | ------        |
| [BLOB storage trigger, invoer, uitvoer](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [Blobopslag] |
| [Cosmos DB invoer en uitvoer van de binding](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [Event Hubs-trigger en uitvoer](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [Bestand met externe invoer en uitvoer](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [HTTP- en webhook trigger](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Mobile Apps-invoer en uitvoer](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [Notification Hubs-uitvoer](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [Queue storage trigger en uitvoer](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [SendGrid-uitvoer](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [Service Bus-trigger en uitvoer](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [Table storage invoer en uitvoer](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Timertrigger](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Twilio-uitvoer](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>BLOB storage trigger, invoer en uitvoer bindingen

Azure Functions ondersteunt worden geactiveerd, invoer en uitvoer van de bindingen voor Azure Blob-opslag. Zie voor meer informatie over expressies voor gegevensbinding en metagegevens [bindingen van Azure Functions Blob storage](functions-bindings-storage-blob.md).

Een blob-trigger is gedefinieerd met Hallo `[BlobTrigger]` kenmerk. U kunt Hallo kenmerk `[StorageAccount]` toodefine Hallo storage-account dat wordt gebruikt door een hele functie of de klasse.

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

BLOB invoer en uitvoer worden gedefinieerd met behulp van Hallo `[Blob]` kenmerk toe, samen met een `FileAccess` parameter die aangeeft lezen of schrijven. Hallo volgende voorbeeld maakt gebruik van een blob-trigger en blob-uitvoer binding.

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

### <a name="cosmos-db-input-and-output-bindings"></a>Cosmos DB invoer en uitvoer bindingen

Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Cosmos-DB. toolearn meer informatie over het Hallo-functies van de binding van de Cosmos-DB hello, Zie [bindingen van Azure Functions Cosmos DB](functions-bindings-documentdb.md).

toobind tooa Cosmos-DB-document Hallo kenmerk gebruiken `[DocumentDB]` in NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.DocumentDB]. Hallo volgende voorbeeld heeft de trigger van een wachtrij en een DocumentDB-API binding uitvoer:

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

### <a name="event-hubs-trigger-and-output"></a>Event Hubs-trigger en uitvoer

Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Event Hubs. Zie voor meer informatie [bindingen van Azure Functions Event Hub](functions-bindings-event-hubs.md).

Hallo typen `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` en `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` zijn gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.ServiceBus]. 

Hallo wordt volgende voorbeeld een Event Hub-trigger.

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Hallo heeft volgende voorbeeld een Event Hub uitvoer met behulp van de retourwaarde van de methode Hallo als Hallo uitvoer:

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

### <a name="external-file-input-and-output"></a>Bestand met externe invoer en uitvoer

Azure Functions ondersteunt trigger, invoer en uitvoer bindingen voor externe bestanden, zoals Google Drive, Dropbox en OneDrive. toolearn meer, Zie [bindingen van Azure Functions-bestand met externe](functions-bindings-external-file.md). Hallo kenmerken `[ExternalFileTrigger]` en `[ExternalFile]` zijn gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.ApiHub].

Hallo volgende C#-voorbeeld demonstreert een extern bestand invoer en uitvoer van de binding. Hallo code kopieën Hallo invoerbestand toohello-uitvoerbestand.

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

### <a name="http-and-webhooks"></a>HTTP en webhooks

Gebruik Hallo `HttpTrigger` kenmerk toodefine een HTTP-trigger of webhook. Dit kenmerk wordt gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.Http]. U kunt aanpassen autorisatieniveau hello, webhook type route en methoden. Hallo volgende voorbeeld definieert een HTTP-trigger met anonieme verificatie en _genericJson_ webhook-type.

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Mobile Apps-invoer en uitvoer

Azure Functions ondersteunt invoer en uitvoer van de bindingen voor mobiele Apps. toolearn meer, Zie [mobiele Apps van Azure Functions bindingen](functions-bindings-mobile-apps.md). Hallo-kenmerk `[MobileTable]` is gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.MobileApps].

Hallo volgende voorbeeld toont een Mobile Apps binding uitvoer:

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>Notification Hubs-uitvoer

Azure Functions ondersteunt een uitvoer-binding voor Notification Hubs. toolearn meer, Zie [Azure Functions Notification Hub uitvoer binding](functions-bindings-notification-hubs.md). Hallo-kenmerk `[NotificationHub]` is gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>Queue storage trigger en uitvoer

Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Azure wachtrijen. Zie voor meer informatie [bindingen van Azure Functions Queue Storage](functions-bindings-storage-queue.md).

Hallo volgende voorbeeld laat zien hoe toouse Hallo functie retourtype met de uitvoer van een wachtrij binding, met behulp van Hallo `[Queue]` kenmerk. een trigger wachtrij toodefine gebruiken Hallo `[QueueTrigger]` kenmerk.

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

### <a name="sendgrid-output"></a>SendGrid-uitvoer

Azure Functions ondersteunt een SendGrid-uitvoer binding voor het programmatisch verzenden van e-mail. toolearn meer, Zie [bindingen van Azure Functions SendGrid](functions-bindings-sendgrid.md).

Hallo-kenmerk `[SendGrid]` is gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.Extensions.SendGrid].

Hallo Hieronder volgt een voorbeeld van een Service Bus-wachtrij-trigger gebruikt en een SendGrid uitvoer binding met `SendGridMessage`:

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

### <a name="service-bus-trigger-and-output"></a>Service Bus-trigger en uitvoer

Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Service Bus-wachtrijen en onderwerpen. Zie voor meer informatie over het configureren van bindingen [bindingen van Azure Functions Service Bus](functions-bindings-service-bus.md).

Hallo kenmerken `[ServiceBusTrigger]` en `[ServiceBus]` zijn gedefinieerd in de NuGet-pakket Hallo [Microsoft.Azure.WebJobs.ServiceBus]. 

Hallo Hieronder volgt een voorbeeld van een Service Bus-wachtrij trigger:

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

Hallo Hier volgt een voorbeeld van een Service Bus-uitvoer binding, met behulp van Hallo methode retourtype als Hallo uitvoer:

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

### <a name="table-storage-input-and-output"></a>Table storage invoer en uitvoer

Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Azure Table storage. toolearn meer, Zie [bindingen van Azure Functions Table storage](functions-bindings-storage-table.md).

Hallo is volgende voorbeeld een klasse met twee functies, tabeluitvoer van opslag en invoer bindingen te demonstreren. 

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

### <a name="timer-trigger"></a>Timertrigger

Azure Functions heeft een timer trigger binding waarmee u de functiecode op basis van een ingesteld schema uitvoeren. toolearn meer informatie over het Hallo-functies van de binding hello, Zie [plannen van de uitvoering van code met Azure Functions](functions-bindings-timer.md).

Op Hallo verbruik plan, kunt u schema's met een [CRON expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression). Als u een App Service-abonnement, kunt u ook een TimeSpan-tekenreeks. 

Hallo volgende voorbeeld definieert een timertrigger die wordt uitgevoerd om de 5 minuten:

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Twilio-uitvoer

Azure Functions ondersteunt Twilio uitvoer van de SMS-berichten van functies toosend tooenable bindingen. toolearn meer, Zie [verzenden SMS-berichten van Azure Functions Hallo Twilio met uitvoer binding](functions-bindings-twilio.md). 

Hallo-kenmerk `[TwilioSms]` is gedefinieerd in Hallo pakket [Microsoft.Azure.WebJobs.Extensions.Twilio].

Hallo volgende C#-voorbeeld maakt gebruik van een wachtrij trigger en een Twilio binding uitvoer:

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

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van Azure Functions in C# scripting [Azure Functions C\# referentie voor ontwikkelaars script](functions-reference-csharp.md).

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
