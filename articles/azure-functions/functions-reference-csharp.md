---
title: aaaAzure functies C# Script-referentie voor ontwikkelaars | Microsoft Docs
description: Begrijpen hoe toodevelop Azure Functions met C#.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a>Azure Functions C# script referentie voor ontwikkelaars
> [!div class="op_single_selector"]
> * [C#-script](functions-reference-csharp.md)
> * [F # script](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

Hallo C# script ervaring voor Azure Functions is gebaseerd op Hallo Azure WebJobs SDK. Gegevensstromen in uw C#-functie via argumenten van de methode. Argumentnamen zijn opgegeven in `function.json`, en er zijn vooraf gedefinieerde namen voor toegang tot bepaalde acties Hallo functie berichtenlogboek en annulering tokens.

In dit artikel wordt ervan uitgegaan dat u hebt al Hallo gelezen [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).

Klasse voor informatie over het gebruik van C#-bibliotheken, Zie [met behulp van .NET-klassebibliotheken met Azure Functions](functions-dotnet-class-library.md).

## <a name="how-csx-works"></a>De werking van .csx
Hallo `.csx` notatie kunt u toowrite minder 'standaard' en u richten op het schrijven van slechts een C#-functie. Assembly-verwijzingen en naamruimten aan Hallo begin van Hallo bestand gewoon bevatten. In plaats van dat u alles verpakt in een naamruimte en klassenaam, net definiëren een `Run` methode. Als u nodig hebt tooinclude Hallo alle klassen, voor het exemplaar toodefine zonder opmaak objecten oude CLR-Object (POCO), kunt u een klasse in opnemen hetzelfde bestand.   

## <a name="binding-tooarguments"></a>Binding tooarguments
Hallo verschillende bindingen zijn gebonden tooa C#-functie via Hallo `name` eigenschap in Hallo *function.json* configuratie. Elke binding heeft een eigen ondersteunde typen; een trigger blob kan bijvoorbeeld een tekenreeks, een POCO of een CloudBlockBlob ondersteunen. Hallo ondersteunde typen zijn gedocumenteerd in Hallo-verwijzing voor elke binding. Een POCO-object moet een getter en setter gedefinieerd voor elke eigenschap hebben.

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a>Met behulp van de retourwaarde van de methode voor het binden van uitvoer

Kunt u de geretourneerde waarde van een methode voor een binding uitvoer met de naam Hallo `$return` in *function.json*:

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a>Schrijven van meerdere uitvoerwaarden

toowrite meerdere waarden tooan uitvoer binding, gebruikt u Hallo [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) of [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) typen. Deze typen zijn alleen-schrijven verzamelingen die geschreven toohello uitvoer binding zijn wanneer Hallo-methode is voltooid.

In dit voorbeeld schrijft meerdere Wachtrijberichten met `ICollector`:

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Logboekregistratie
toolog uitvoer tooyour streaminglogboeken in C#, bevatten een argument van het type `TraceWriter`. Het is raadzaam dat u deze de naam `log`. Vermijd het gebruik van `Console.Write` in Azure Functions. 

`TraceWriter`is gedefinieerd in Hallo [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Hallo logboekniveau voor `TraceWriter` kunnen worden geconfigureerd in [host\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Asynchrone
een asynchrone functie toomake hello gebruiken `async` sleutelwoord en retourneren een `Task` object.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>Annulering Token
Bepaalde bewerkingen vereisen correct afsluiten. Het is altijd best toowrite code dat kan worden verwerkt gecrasht in gevallen waar u toohandle correct afsluiten aanvragen, definieert u een [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument opgegeven.  Een `CancellationToken` toosignal dat een afsluiten van de host is geactiveerd is opgegeven.

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a>Naamruimten importeren
Als u tooimport naamruimten moet, kunt u doen gebruikelijke Hello `using` component.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hallo volgende naamruimten automatisch worden geïmporteerd en zijn daarom optioneel:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Verwijzen naar externe assembly 's
Voor de framework-assembly's, voeg verwijzingen toe met behulp van Hallo `#r "AssemblyName"` richtlijn.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hallo worden volgende assembly's automatisch toegevoegd door hello Azure Functions hostomgeving:

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

Hallo volgende assembly's kunnen worden verwezen met eenvoudige naam (bijvoorbeeld `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Aangepaste assembly's die verwijzen naar

een aangepaste assembly tooreference, kunt u ofwel een *gedeelde* assembly of een *persoonlijke* assembly:
- Gedeelde assembly's worden gedeeld door alle functies binnen een functie-app. een aangepaste assembly tooreference uploaden Hallo assembly tooyour functie-app, zoals een `bin` map in Hallo functie app-hoofdmap. 
- Persoonlijke assembly's deel uitmaken van een bepaalde functie context en ondersteuning voor sideloading van verschillende versies. Persoonlijke assembly's moeten worden geüpload een `bin` map in Hallo functie directory. Verwijzing naar het gebruik van Hallo bestandsnaam op, zoals `#r "MyAssembly.dll"`. 

Zie voor informatie over hoe tooupload tooyour functie map bestanden, Hallo volgende sectie op het gebied van pakket.

### <a name="watched-directories"></a>Gecontroleerde mappen

Hallo-map met de Hallo functie scriptbestand wordt automatisch weergegeven voor wijzigingen tooassemblies. toowatch voor assembly-wijzigingen in andere mappen toohello toe te voegen `watchDirectories` in lijst [host\.json].

## <a name="using-nuget-packages"></a>NuGet-pakketten gebruiken
toouse NuGet-pakketten in een C#-functie uploaden een *project.json* bestand van de functie toohello map in Hallo functie app-bestandssysteem. Hier volgt een voorbeeld *project.json* -bestand dat wordt een verwijzing tooMicrosoft.ProjectOxford.Face versie 1.1.0 toegevoegd:

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

Alleen hello .NET Framework 4.6 wordt ondersteund, dus zorg ervoor dat uw *project.json* bestand geeft `net46` zoals hier wordt weergegeven.

Wanneer u uploadt een *project.json* bestand, hello runtime opgehaald hello-pakketten en verwijzingen toohello pakket assembly's worden automatisch toegevoegd. U hoeft niet tooadd `#r "AssemblyName"` richtlijnen. toouse Hallo-typen gedefinieerd in Hallo NuGet-pakketten toevoegen Hallo vereist `using` instructies tooyour *run.csx* bestand 

Hallo runtime van Functions, NuGet terugzetten werkt door te vergelijken `project.json` en `project.lock.json`. Als datum- en tijdstempels van bestanden Hallo Hallo **niet** overeenkomst, een NuGet-herstelbewerking wordt uitgevoerd en NuGet downloads pakketten bijgewerkt. Echter, als hello datum- en tijdstempels van bestanden Hallo **doen** overeenkomen, NuGet voert een terugzetbewerking. Daarom `project.lock.json` moeten niet worden geïmplementeerd omdat het ervoor zorgt NuGet tooskip pakket herstellen dat. Hallo vergrendeling implementeren tooavoid bestand, het toevoegen van Hallo `project.lock.json` toohello `.gitignore` bestand.

een aangepaste NuGet-feed toouse Geef Hallo-kanaal in een *Nuget.Config* bestand in Hallo functie-App-hoofdmap. Zie voor meer informatie [NuGet configureren gedrag](/nuget/consume-packages/configuring-nuget-behavior).

### <a name="using-a-projectjson-file"></a>Met behulp van een bestand project.json
1. Hallo functie openen in hello Azure-portal. Hallo logboeken tabblad geeft Hallo pakket installatie uitvoer.
2. tooupload een bestand project.json gebruik een van de methoden van Hallo Hallo [hoe de app-bestanden voor het functioneren van tooupdate](functions-reference.md#fileupdate) in naslagonderwerp voor hello Azure Functions-ontwikkelaar.
3. Na het Hallo *project.json* bestand wordt geüpload, ziet u uitvoer zoals Hallo voorbeeld in de functie na de streaming-logboek:

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a>Omgevingsvariabelen
tooget een omgevingsvariabele of een app-instelling-waarde gebruiken `System.Environment.GetEnvironmentVariable`, zoals weergegeven in het volgende codevoorbeeld Hallo:

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a>Hergebruik van code .csx
U kunt klassen en methoden die zijn gedefinieerd in andere *.csx* bestanden in uw *run.csx* bestand. toodo die gebruikmaken van `#load` richtlijnen op uw *run.csx* bestand. In de Hallo voorbeeld te volgen, een routine logboekregistratie met de naam `MyLogger` wordt gedeeld *myLogger.csx* en geladen in *run.csx* met Hallo `#load` richtlijn:

Voorbeeld *run.csx*:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

Voorbeeld *mylogger.csx*:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

Met behulp van een gedeelde *.csx* is een algemene patroon als u wilt dat toostrongly uw typeargumenten tussen functies met een POCO-object. In een Hallo vereenvoudigd voorbeeld te volgen, een HTTP-trigger en wachtrij-trigger delen een POCO-object met de naam `Order` toostrongly type Hallo ordenen van gegevens:

Voorbeeld *run.csx* voor HTTP-trigger:

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

Voorbeeld *run.csx* voor wachtrij trigger:

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

Voorbeeld *order.csx*:

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

U kunt een relatief pad Hallo `#load` richtlijn:

* `#load "mylogger.csx"`een bestand in Hallo functie map laadt.
* `#load "loadedfiles\mylogger.csx"`een bestand in een map in Hallo functie map laadt.
* `#load "..\shared\mylogger.csx"`een bestand in een map op hetzelfde niveau als Hallo functie map, dat wil zeggen, Hallo laadt rechtstreeks onder *wwwroot*.

Hallo `#load` richtlijn werkt alleen met *.csx* (C# script)-bestanden, niet bij *.cs* bestanden.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Binding tijdens runtime via imperatieve bindingen

In C# en andere .NET-talen, kunt u een [imperatieve](https://en.wikipedia.org/wiki/Imperative_programming) patroon van de binding, als tegengestelde toohello [ *declaratieve* ](https://en.wikipedia.org/wiki/Declarative_programming) bindingen in *function.json*. Imperatieve binding is handig als bindparameters toobe berekend tijdens runtime in plaats van ontwerp moeten. U kunt met dit patroon binden toosupported invoer en uitvoer van de binding op het moment in uw functiecode.

Definieer een imperatieve binding als volgt:

- **Geen** een vermelding in *function.json* voor uw gewenste imperatieve bindingen.
- Geeft een invoerparameter [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) of [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Gebruik Hallo C# patroon tooperform Hallo gegevensbinding te volgen.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

waar `BindingTypeAttribute` is Hallo .NET-kenmerk dat de binding wordt gedefinieerd en `T` is Hallo invoer- of -type dat wordt ondersteund door deze bindingstype. `T`ook kan niet een `out` parametertype (zoals `out JObject`). Bijvoorbeeld, de tabel Mobile Apps binding ondersteunt uitvoer [zes typen uitvoer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), maar u kunt alleen [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) of [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) voor `T`.

Hallo volgende voorbeeldcode maakt een [Storage-blob uitvoer binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) met blob pad dat gedefinieerd tijdens runtime, schrijft u een tekenreeks toohello blob.

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definieert Hallo [Storage-blob](functions-bindings-storage-blob.md) invoer of uitvoer van de binding en [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is een ondersteunde binding uitvoertype.
Code Hallo Hallo standaard app-instelling voor Hallo verbindingsreeks voor opslag account opgehaald (dit is `AzureWebJobsStorage`). U kunt een aangepaste app-instelling toouse opgeven door toe te voegen de [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) en Hallo kenmerk matrix in doorgeven `BindAsync<T>()`. Bijvoorbeeld:

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

Hallo bevat volgende tabel Hallo .NET kenmerken voor elke binding type hello-pakketten en waarin ze worden gedefinieerd.

> [!div class="mx-codeBreakAll"]
| Binding | Kenmerk | Verwijzing toevoegen |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Event Hubs | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Mobile Apps | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Notification Hubs | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Service Bus | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Storage-wachtrij | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Storage-blob | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Table Storage | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie Hallo resources te volgen:

* [Aanbevolen procedures voor Azure Functions](functions-best-practices.md)
* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)
* [Azure Functions F # referentie voor ontwikkelaars](functions-reference-fsharp.md)
* [Azure Functions NodeJS-referentie voor ontwikkelaars](functions-reference-node.md)
* [Azure Functions-triggers en bindingen](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
