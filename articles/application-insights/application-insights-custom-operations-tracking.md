---
title: aangepaste bewerkingen met Azure Application Insights-SDK voor .NET aaaTrack | Microsoft Docs
description: Het bijhouden van aangepaste bewerkingen met Azure Application Insights-SDK voor .NET
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>Bijhouden van aangepaste bewerkingen met Application Insights-SDK voor .NET

Azure Application Insights-SDK's automatisch bijhouden binnenkomende HTTP-aanvragen en roept toodependent services, zoals HTTP-aanvragen en SQL-query's. Bijhouden en correlatie van aanvragen en afhankelijkheden bieden u inzicht in de reactietijd en betrouwbaarheid Hallo gehele toepassing op alle microservices met een combinatie van deze toepassing. 

Er is een klasse die van toepassing patronen die algemeen kan niet worden ondersteund. Goede bewaking van deze patronen vereist handmatige code instrumentation. In dit artikel bevat informatie over een paar patronen die mogelijk handmatige instrumentation, zoals aangepaste wachtrij verwerken en langlopende achtergrondtaken uitvoeren.

Dit document biedt richtlijnen voor hoe tootrack aangepaste bewerkingen met Application Insights-SDK Hallo. Deze documentatie is relevant voor:

- Application Insights voor .NET (ook wel bekend als Base SDK) versie 2.4 +.
- Application Insights voor web-toepassingen (met ASP.NET) versie 2.4 +.
- Application Insights voor ASP.NET Core versie 2.1 +.

## <a name="overview"></a>Overzicht
Een bewerking is een logische werk uitgevoerd door een toepassing. Een naam, de starttijd, duur, resultaat en een context van de uitvoering zoals gebruikersnaam, eigenschappen en resultaat heeft. Als een bewerking is gestart door de bewerking B, wordt bewerking B ingesteld als een bovenliggend element van A. Een bewerking kan slechts één bovenliggend hebben, maar er veel onderliggende bewerkingen. Zie voor meer informatie over bewerkingen en telemetrie correlatie [Azure Application Insights telemetrie correlatie](application-insights-correlation.md).

In Application Insights-SDK voor .NET hello, Hallo-bewerking is beschreven door Hallo abstracte klasse [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) en afgeleiden [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) en [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>Binnenkomende operations bijhouden 
Hallo Application Insights web die SDK verzamelt automatisch HTTP-aanvragen voor ASP.NET-toepassingen die worden uitgevoerd in een IIS-pijplijn en alle toepassingen die ASP.NET Core. Er zijn oplossingen voor andere platforms en frameworks community ondersteund. Echter, als de toepassing hello niet wordt ondersteund door een van de Hallo standard of oplossingen community ondersteund, u kunt softwareontwikkelaars deze handmatig.

Een ander voorbeeld waarvoor aangepaste bijhouden is Hallo werknemer die items uit de wachtrij Hallo ontvangt. Voor sommige wachtrijen aanroepen Hallo tooadd een bericht toothis wachtrij wordt bijgehouden als een afhankelijkheid. Hallo op hoog niveau bewerking die berichtverwerking beschrijft is echter niet automatisch verzameld.

Laten we zien hoe deze bewerkingen kunnen worden bijgehouden.

Op hoog niveau is Hallo taak toocreate `RequestTelemetry` en bekende eigenschappen instellen. Nadat het Hallo-bewerking is voltooid, kunt u bijhouden Hallo telemetrie. Hallo volgende voorbeeld ziet u deze taak.

### <a name="http-request-in-owin-self-hosted-app"></a>HTTP-aanvraag in host zichzelf Owin-app
In dit voorbeeld volgt we Hallo [HTTP-Protocol voor correlatie](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md). Houd rekening met tooreceive headers die er worden beschreven.

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

Hallo HTTP-Protocol voor correlatie declareert ook Hallo `Correlation-Context` header. Echter, dit wordt weggelaten hier voor eenvoud.

## <a name="queue-instrumentation"></a>Wachtrij instrumentation
Voor HTTP-communicatie, er is een protocol toopass correlatie details gemaakt. Met de sommige wachtrijen protocollen, kunt u aanvullende metagegevens samen met het Hallo-bericht en met anderen die u niet doorgeven.

### <a name="service-bus-queue"></a>Service Bus-wachtrij
Hello Azure [Service Bus-wachtrij](../service-bus-messaging/index.md), kunt u een eigenschappenverzameling samen met het Hallo-bericht doorgeven. We gebruiken deze toopass Hallo correlatie-ID.

Hallo Service Bus-wachtrij maakt gebruik van TCP-protocollen. Application Insights niet automatisch bijgehouden voor bewerkingen van de wachtrij, zodat we ze handmatig bijhouden. Hallo in wachtrij bewerking is een push-stijl-API en dit niet kan tootrack deze.

#### <a name="enqueue"></a>In de wachtrij plaatsen

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a>Proces
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a>Azure Storage-wachtrij
Hallo volgende voorbeeld wordt getoond hoe tootrack hello [Azure Storage-wachtrij](../storage/queues/storage-dotnet-how-to-use-queues.md) bewerkingen en vergelijken telemetrie tussen Hallo producent, Hallo consumer en Azure Storage. 

Hallo-opslagwachtrij heeft een HTTP-API. Alle aanroepen toohello wachtrij bijgehouden door Hallo Application Insights afhankelijkheid Collector voor HTTP-aanvragen.
Zorg ervoor dat u hebt `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`. Als u dit niet hebt u deze toevoegen via een programma zoals beschreven in [filteren en voorverwerking in hello Azure Application Insights-SDK](app-insights-api-filtering-sampling.md).

Als u de Application Insights handmatig configureert, moet u maken en initialiseren `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` als:
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

Ook kunt u toocorrelate Hallo Application Insights bewerkings-ID met Hallo opslag aanvraag-ID. Zie voor informatie over hoe tooset en get opslaggroep client en de aanvraag-ID van een server aanvragen, [Monitor, vaststellen en oplossen van Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).

#### <a name="enqueue"></a>In de wachtrij plaatsen
Omdat opslagwachtrijen Hallo HTTP API ondersteunt, worden alle bewerkingen met Hallo wachtrij automatisch bijgehouden door de Application Insights. In veel gevallen kan moeten deze instrumentation voldoende. Echter toocorrelate traceert Hallo consumer zijde met producent traceringen, moet u alle context correlatie doorgeven op dezelfde manier toohow we dit doen in Hallo HTTP-Protocol voor correlatie. 

In dit voorbeeld die we volgen Hallo optionele `Enqueue` bewerking. U kunt:

 - **Nieuwe pogingen correleren (indien aanwezig)**: alle moeten één gemeenschappelijk bovenliggend niveau die Hallo `Enqueue` bewerking. Ze zijn anders als onderliggende elementen van de binnenkomende aanvraag Hallo bijgehouden. Als er meerdere logische aanvragen toohello wachtrij, is mogelijk moeilijk toofind welke aanroep nieuwe pogingen heeft.
 - **Opslag logboeken correleren (of en wanneer nodig)**: ze zijn gecorreleerd met Application Insights telemetrie.

Hallo `Enqueue` bewerking is Hallo onderliggend element van een bovenliggende-bewerking (bijvoorbeeld, een binnenkomende HTTP-aanvraag). Hallo HTTP afhankelijkheidsaanroep is Hallo onderliggende Hallo `Enqueue` bewerking en Hallo onderliggend voor inkomende hello-aanvraag:

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

rapporten van tooreduce Hallo hoeveelheid telemetrie uw toepassing of als u niet dat tootrack hello wilt `Enqueue` bewerking om andere redenen gebruik Hallo `Activity` rechtstreeks API:

- Maak (en start) een nieuwe `Activity` in plaats van Hallo Application Insights-bewerking wordt gestart. U doet *niet* tooassign moet alle eigenschappen behalve Hallo bewerkingsnaam.
- Serialiseren `yourActivity.Id` in Hallo-bericht nettolading in plaats van `operation.Telemetry.Id`. U kunt ook `Activity.Current.Id`.


#### <a name="dequeue"></a>In wachtrij
Op dezelfde manier te`Enqueue`, een wachtrij toohello-opslag voor werkelijke HTTP-aanvragen is automatisch bijgehouden door de Application Insights. Hallo echter `Enqueue` -bewerking wordt waarschijnlijk uitgevoerd in de context van het Hallo bovenliggende, zoals de aanvraagcontext van een binnenkomende. Application Insights-SDK's correleren automatisch dergelijke bewerking (en het onderdeel HTTP) met Hallo bovenliggende aanvraag en andere telemetrie die is gerapporteerd in Hallo dat dezelfde scope.

Hallo `Dequeue` bewerking is lastig. Hallo Application Insights-SDK HTTP-aanvragen automatisch worden bijgehouden. Maar weet niet Hallo correlatie context totdat het Hallo-bericht wordt geparseerd. Het is niet mogelijk toocorrelate Hallo HTTP tooget Hallo aanvraagbericht met rest Hallo Hallo telemetrie.

In veel gevallen kan het nuttig toocorrelate Hallo HTTP-aanvraag toohello wachtrij met andere traceringen ook zijn. Hallo volgende voorbeeld laat zien hoe toodo het:

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a>Proces

In de Hallo voorbeeld te volgen, traceren we een binnenkomend bericht op een manier op dezelfde manier toohow we een binnenkomende HTTP trace-aanvragen:

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

Op dezelfde manier kunnen andere bewerkingen wachtrij worden geïmplementeerd. Een bewerking peek moet geïnstrumenteerd op een vergelijkbare manier als een bewerking van de wachtrij halen. Wachtrij-beheerbewerkingen instrumenteren is niet nodig. Application Insights houdt bewerkingen zoals HTTP en in de meeste gevallen is voldoende.

Wanneer u softwareontwikkelaars verwijdering van berichten, zorg er dan voor dat u Hallo bewerking-id's (correlatie) instellen. U kunt ook hello gebruiken `Activity` API. Vervolgens hoeft u niet tooset bewerking-id's op Hallo telemetrie-items omdat Application Insights dit gebeurt:

- Maak een nieuwe `Activity` nadat u hebt een item uit de wachtrij Hallo.
- Gebruik `Activity.SetParentId(message.ParentId)` toocorrelate consumer en producent Logboeken.
- Hallo Start `Activity`.
- Bijhouden in wachtrij, verwerken en verwijderen van bewerkingen met behulp van `Start/StopOperation` helpers. Dit doen vanaf Hallo dezelfde asynchrone transportbesturing (uitvoeringscontext). Op deze manier bent ze gecorreleerde goed.
- Stop Hallo `Activity`.
- Gebruik `Start/StopOperation`, of bel `Track` telemetrie handmatig.

### <a name="batch-processing"></a>Batchverwerking
Sommige wachtrijen, kunt u meerdere berichten met één aanvraag in wachtrij. Dergelijke berichten worden verwerkt, is waarschijnlijk onafhankelijk en verschillende logische bewerkingen toohello behoort. In dit geval wordt het is niet mogelijk toocorrelate hello `Dequeue` bewerking tooparticular berichtverwerking.

Elk bericht moet worden verwerkt in de eigen asynchrone Controlestroom. Zie voor meer informatie, Hallo [uitgaande afhankelijkheden bijhouden](#outgoing-dependencies-tracking) sectie.

## <a name="long-running-background-tasks"></a>Achtergrondtaken langlopende
Sommige toepassingen starten langlopende bewerkingen die kunnen worden veroorzaakt door het aanvragen van gebruikers. Vanuit het perspectief van de tracering/instrumentation hello, van verschilt niet van de aanvraag of een afhankelijkheid instrumentation: 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

In dit voorbeeld gebruiken we `telemetryClient.StartOperation` toocreate `RequestTelemetry` en opvulling Hallo correlatie context. Stel dat u hebt een bovenliggende-bewerking die is gemaakt door de inkomende aanvragen dat Hallo-bewerking geplande. Zolang `BackgroundTask` gestart in Hallo dezelfde asynchrone Controlestroom als een inkomende aanvraag, deze worden gecorreleerd met die bovenliggende voor deze bewerking. `BackgroundTask`en alle geneste telemetrie-items automatisch worden gecorreleerd met Hallo-aanvraag, waardoor er, zelfs nadat het Hallo-aanvraag wordt beëindigd.

Wanneer Hallo-taak wordt gestart van Hallo achtergrondthread dat geen bewerkingen (`Activity`) gekoppeld, `BackgroundTask` heeft een bovenliggende geen. Echter, het kan hebben genest bewerkingen. Alle telemetrie-items van de taak Hallo gerapporteerd zijn gecorreleerde toohello `RequestTelemetry` gemaakt in `BackgroundTask`.

## <a name="outgoing-dependencies-tracking"></a>Uitgaande afhankelijkheden bijhouden
U kunt uw eigen soort afhankelijkheid of een bewerking die niet wordt ondersteund door de Application Insights bijhouden.

Hallo `Enqueue` methode in de Service Bus-wachtrij Hallo of Hallo opslagwachtrij kan fungeren als voorbeelden van dergelijke aangepaste bijhouden.

Hallo algemeen de aanpak voor het bijhouden van aangepaste afhankelijkheid is:

- Hallo aanroepen `TelemetryClient.StartOperation` (extensie)-methode die wordt gevuld Hallo `DependencyTelemetry` eigenschappen die nodig zijn voor correlatie en andere eigenschappen (begintijd stempel, duur).
- Andere aangepaste eigenschappen worden ingesteld op Hallo `DependencyTelemetry`, zoals het Hallo-naam en een andere context die u nodig.
- Controleer een afhankelijkheid bellen en een ogenblik geduld.
- Hallo-bewerking met stoppen `StopOperation` wanneer deze voltooid.
- Uitzonderingen worden verwerkt.

`StopOperation`alleen gestopt Hallo die is gestart. Als de huidige actieve bewerking Hallo komt niet overeen met de Hallo een gewenste toostop, `StopOperation` , gebeurt er niets. Deze situatie kan gebeuren als u meerdere bewerkingen parallel in Hallo start dezelfde uitvoeringscontext:

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

Zorg ervoor dat u altijd aanroepen `StartOperation` en voert u de taak in een eigen context:
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a>Volgende stappen

- Leer de basisbeginselen Hallo van [telemetrie correlatie](application-insights-correlation.md) in Application Insights.
- Zie Hallo [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.
- Aangepast rapport [gebeurtenissen en metrische gegevens](app-insights-api-custom-events-metrics.md) tooApplication Insights.
- Bekijk standaard [configuratie](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) voor context eigenschappen verzameling.
- Controleer Hallo [System.Diagnostics.Activity gebruikershandleiding](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee hoe we telemetrie correleren.
