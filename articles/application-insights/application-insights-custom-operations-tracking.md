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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="4091f-103">Bijhouden van aangepaste bewerkingen met Application Insights-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="4091f-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="4091f-104">Azure Application Insights-SDK's automatisch bijhouden binnenkomende HTTP-aanvragen en roept toodependent services, zoals HTTP-aanvragen en SQL-query's.</span><span class="sxs-lookup"><span data-stu-id="4091f-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="4091f-105">Bijhouden en correlatie van aanvragen en afhankelijkheden bieden u inzicht in de reactietijd en betrouwbaarheid Hallo gehele toepassing op alle microservices met een combinatie van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="4091f-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="4091f-106">Er is een klasse die van toepassing patronen die algemeen kan niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4091f-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="4091f-107">Goede bewaking van deze patronen vereist handmatige code instrumentation.</span><span class="sxs-lookup"><span data-stu-id="4091f-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="4091f-108">In dit artikel bevat informatie over een paar patronen die mogelijk handmatige instrumentation, zoals aangepaste wachtrij verwerken en langlopende achtergrondtaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4091f-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="4091f-109">Dit document biedt richtlijnen voor hoe tootrack aangepaste bewerkingen met Application Insights-SDK Hallo.</span><span class="sxs-lookup"><span data-stu-id="4091f-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="4091f-110">Deze documentatie is relevant voor:</span><span class="sxs-lookup"><span data-stu-id="4091f-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="4091f-111">Application Insights voor .NET (ook wel bekend als Base SDK) versie 2.4 +.</span><span class="sxs-lookup"><span data-stu-id="4091f-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="4091f-112">Application Insights voor web-toepassingen (met ASP.NET) versie 2.4 +.</span><span class="sxs-lookup"><span data-stu-id="4091f-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="4091f-113">Application Insights voor ASP.NET Core versie 2.1 +.</span><span class="sxs-lookup"><span data-stu-id="4091f-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="4091f-114">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4091f-114">Overview</span></span>
<span data-ttu-id="4091f-115">Een bewerking is een logische werk uitgevoerd door een toepassing.</span><span class="sxs-lookup"><span data-stu-id="4091f-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="4091f-116">Een naam, de starttijd, duur, resultaat en een context van de uitvoering zoals gebruikersnaam, eigenschappen en resultaat heeft.</span><span class="sxs-lookup"><span data-stu-id="4091f-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="4091f-117">Als een bewerking is gestart door de bewerking B, wordt bewerking B ingesteld als een bovenliggend element van A. Een bewerking kan slechts één bovenliggend hebben, maar er veel onderliggende bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="4091f-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="4091f-118">Zie voor meer informatie over bewerkingen en telemetrie correlatie [Azure Application Insights telemetrie correlatie](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="4091f-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="4091f-119">In Application Insights-SDK voor .NET hello, Hallo-bewerking is beschreven door Hallo abstracte klasse [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) en afgeleiden [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) en [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="4091f-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="4091f-120">Binnenkomende operations bijhouden</span><span class="sxs-lookup"><span data-stu-id="4091f-120">Incoming operations tracking</span></span> 
<span data-ttu-id="4091f-121">Hallo Application Insights web die SDK verzamelt automatisch HTTP-aanvragen voor ASP.NET-toepassingen die worden uitgevoerd in een IIS-pijplijn en alle toepassingen die ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4091f-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="4091f-122">Er zijn oplossingen voor andere platforms en frameworks community ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4091f-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="4091f-123">Echter, als de toepassing hello niet wordt ondersteund door een van de Hallo standard of oplossingen community ondersteund, u kunt softwareontwikkelaars deze handmatig.</span><span class="sxs-lookup"><span data-stu-id="4091f-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="4091f-124">Een ander voorbeeld waarvoor aangepaste bijhouden is Hallo werknemer die items uit de wachtrij Hallo ontvangt.</span><span class="sxs-lookup"><span data-stu-id="4091f-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="4091f-125">Voor sommige wachtrijen aanroepen Hallo tooadd een bericht toothis wachtrij wordt bijgehouden als een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="4091f-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="4091f-126">Hallo op hoog niveau bewerking die berichtverwerking beschrijft is echter niet automatisch verzameld.</span><span class="sxs-lookup"><span data-stu-id="4091f-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="4091f-127">Laten we zien hoe deze bewerkingen kunnen worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="4091f-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="4091f-128">Op hoog niveau is Hallo taak toocreate `RequestTelemetry` en bekende eigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="4091f-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="4091f-129">Nadat het Hallo-bewerking is voltooid, kunt u bijhouden Hallo telemetrie.</span><span class="sxs-lookup"><span data-stu-id="4091f-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="4091f-130">Hallo volgende voorbeeld ziet u deze taak.</span><span class="sxs-lookup"><span data-stu-id="4091f-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="4091f-131">HTTP-aanvraag in host zichzelf Owin-app</span><span class="sxs-lookup"><span data-stu-id="4091f-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="4091f-132">In dit voorbeeld volgt we Hallo [HTTP-Protocol voor correlatie](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="4091f-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="4091f-133">Houd rekening met tooreceive headers die er worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="4091f-133">You should expect tooreceive headers that are described there.</span></span>

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

<span data-ttu-id="4091f-134">Hallo HTTP-Protocol voor correlatie declareert ook Hallo `Correlation-Context` header.</span><span class="sxs-lookup"><span data-stu-id="4091f-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="4091f-135">Echter, dit wordt weggelaten hier voor eenvoud.</span><span class="sxs-lookup"><span data-stu-id="4091f-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="4091f-136">Wachtrij instrumentation</span><span class="sxs-lookup"><span data-stu-id="4091f-136">Queue instrumentation</span></span>
<span data-ttu-id="4091f-137">Voor HTTP-communicatie, er is een protocol toopass correlatie details gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4091f-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="4091f-138">Met de sommige wachtrijen protocollen, kunt u aanvullende metagegevens samen met het Hallo-bericht en met anderen die u niet doorgeven.</span><span class="sxs-lookup"><span data-stu-id="4091f-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="4091f-139">Service Bus-wachtrij</span><span class="sxs-lookup"><span data-stu-id="4091f-139">Service Bus queue</span></span>
<span data-ttu-id="4091f-140">Hello Azure [Service Bus-wachtrij](../service-bus-messaging/index.md), kunt u een eigenschappenverzameling samen met het Hallo-bericht doorgeven.</span><span class="sxs-lookup"><span data-stu-id="4091f-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="4091f-141">We gebruiken deze toopass Hallo correlatie-ID.</span><span class="sxs-lookup"><span data-stu-id="4091f-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="4091f-142">Hallo Service Bus-wachtrij maakt gebruik van TCP-protocollen.</span><span class="sxs-lookup"><span data-stu-id="4091f-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="4091f-143">Application Insights niet automatisch bijgehouden voor bewerkingen van de wachtrij, zodat we ze handmatig bijhouden.</span><span class="sxs-lookup"><span data-stu-id="4091f-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="4091f-144">Hallo in wachtrij bewerking is een push-stijl-API en dit niet kan tootrack deze.</span><span class="sxs-lookup"><span data-stu-id="4091f-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="4091f-145">In de wachtrij plaatsen</span><span class="sxs-lookup"><span data-stu-id="4091f-145">Enqueue</span></span>

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

#### <a name="process"></a><span data-ttu-id="4091f-146">Proces</span><span class="sxs-lookup"><span data-stu-id="4091f-146">Process</span></span>
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

### <a name="azure-storage-queue"></a><span data-ttu-id="4091f-147">Azure Storage-wachtrij</span><span class="sxs-lookup"><span data-stu-id="4091f-147">Azure Storage queue</span></span>
<span data-ttu-id="4091f-148">Hallo volgende voorbeeld wordt getoond hoe tootrack hello [Azure Storage-wachtrij](../storage/queues/storage-dotnet-how-to-use-queues.md) bewerkingen en vergelijken telemetrie tussen Hallo producent, Hallo consumer en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4091f-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="4091f-149">Hallo-opslagwachtrij heeft een HTTP-API.</span><span class="sxs-lookup"><span data-stu-id="4091f-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="4091f-150">Alle aanroepen toohello wachtrij bijgehouden door Hallo Application Insights afhankelijkheid Collector voor HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4091f-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="4091f-151">Zorg ervoor dat u hebt `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="4091f-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="4091f-152">Als u dit niet hebt u deze toevoegen via een programma zoals beschreven in [filteren en voorverwerking in hello Azure Application Insights-SDK](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="4091f-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="4091f-153">Als u de Application Insights handmatig configureert, moet u maken en initialiseren `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` als:</span><span class="sxs-lookup"><span data-stu-id="4091f-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="4091f-154">Ook kunt u toocorrelate Hallo Application Insights bewerkings-ID met Hallo opslag aanvraag-ID.</span><span class="sxs-lookup"><span data-stu-id="4091f-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="4091f-155">Zie voor informatie over hoe tooset en get opslaggroep client en de aanvraag-ID van een server aanvragen, [Monitor, vaststellen en oplossen van Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="4091f-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="4091f-156">In de wachtrij plaatsen</span><span class="sxs-lookup"><span data-stu-id="4091f-156">Enqueue</span></span>
<span data-ttu-id="4091f-157">Omdat opslagwachtrijen Hallo HTTP API ondersteunt, worden alle bewerkingen met Hallo wachtrij automatisch bijgehouden door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4091f-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="4091f-158">In veel gevallen kan moeten deze instrumentation voldoende.</span><span class="sxs-lookup"><span data-stu-id="4091f-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="4091f-159">Echter toocorrelate traceert Hallo consumer zijde met producent traceringen, moet u alle context correlatie doorgeven op dezelfde manier toohow we dit doen in Hallo HTTP-Protocol voor correlatie.</span><span class="sxs-lookup"><span data-stu-id="4091f-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="4091f-160">In dit voorbeeld die we volgen Hallo optionele `Enqueue` bewerking.</span><span class="sxs-lookup"><span data-stu-id="4091f-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="4091f-161">U kunt:</span><span class="sxs-lookup"><span data-stu-id="4091f-161">You can:</span></span>

 - <span data-ttu-id="4091f-162">**Nieuwe pogingen correleren (indien aanwezig)**: alle moeten één gemeenschappelijk bovenliggend niveau die Hallo `Enqueue` bewerking.</span><span class="sxs-lookup"><span data-stu-id="4091f-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="4091f-163">Ze zijn anders als onderliggende elementen van de binnenkomende aanvraag Hallo bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="4091f-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="4091f-164">Als er meerdere logische aanvragen toohello wachtrij, is mogelijk moeilijk toofind welke aanroep nieuwe pogingen heeft.</span><span class="sxs-lookup"><span data-stu-id="4091f-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="4091f-165">**Opslag logboeken correleren (of en wanneer nodig)**: ze zijn gecorreleerd met Application Insights telemetrie.</span><span class="sxs-lookup"><span data-stu-id="4091f-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="4091f-166">Hallo `Enqueue` bewerking is Hallo onderliggend element van een bovenliggende-bewerking (bijvoorbeeld, een binnenkomende HTTP-aanvraag).</span><span class="sxs-lookup"><span data-stu-id="4091f-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="4091f-167">Hallo HTTP afhankelijkheidsaanroep is Hallo onderliggende Hallo `Enqueue` bewerking en Hallo onderliggend voor inkomende hello-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="4091f-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

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

<span data-ttu-id="4091f-168">rapporten van tooreduce Hallo hoeveelheid telemetrie uw toepassing of als u niet dat tootrack hello wilt `Enqueue` bewerking om andere redenen gebruik Hallo `Activity` rechtstreeks API:</span><span class="sxs-lookup"><span data-stu-id="4091f-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="4091f-169">Maak (en start) een nieuwe `Activity` in plaats van Hallo Application Insights-bewerking wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4091f-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="4091f-170">U doet *niet* tooassign moet alle eigenschappen behalve Hallo bewerkingsnaam.</span><span class="sxs-lookup"><span data-stu-id="4091f-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="4091f-171">Serialiseren `yourActivity.Id` in Hallo-bericht nettolading in plaats van `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="4091f-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="4091f-172">U kunt ook `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="4091f-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="4091f-173">In wachtrij</span><span class="sxs-lookup"><span data-stu-id="4091f-173">Dequeue</span></span>
<span data-ttu-id="4091f-174">Op dezelfde manier te`Enqueue`, een wachtrij toohello-opslag voor werkelijke HTTP-aanvragen is automatisch bijgehouden door de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4091f-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="4091f-175">Hallo echter `Enqueue` -bewerking wordt waarschijnlijk uitgevoerd in de context van het Hallo bovenliggende, zoals de aanvraagcontext van een binnenkomende.</span><span class="sxs-lookup"><span data-stu-id="4091f-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="4091f-176">Application Insights-SDK's correleren automatisch dergelijke bewerking (en het onderdeel HTTP) met Hallo bovenliggende aanvraag en andere telemetrie die is gerapporteerd in Hallo dat dezelfde scope.</span><span class="sxs-lookup"><span data-stu-id="4091f-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="4091f-177">Hallo `Dequeue` bewerking is lastig.</span><span class="sxs-lookup"><span data-stu-id="4091f-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="4091f-178">Hallo Application Insights-SDK HTTP-aanvragen automatisch worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="4091f-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="4091f-179">Maar weet niet Hallo correlatie context totdat het Hallo-bericht wordt geparseerd.</span><span class="sxs-lookup"><span data-stu-id="4091f-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="4091f-180">Het is niet mogelijk toocorrelate Hallo HTTP tooget Hallo aanvraagbericht met rest Hallo Hallo telemetrie.</span><span class="sxs-lookup"><span data-stu-id="4091f-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="4091f-181">In veel gevallen kan het nuttig toocorrelate Hallo HTTP-aanvraag toohello wachtrij met andere traceringen ook zijn.</span><span class="sxs-lookup"><span data-stu-id="4091f-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="4091f-182">Hallo volgende voorbeeld laat zien hoe toodo het:</span><span class="sxs-lookup"><span data-stu-id="4091f-182">hello following example demonstrates how toodo it:</span></span>

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

#### <a name="process"></a><span data-ttu-id="4091f-183">Proces</span><span class="sxs-lookup"><span data-stu-id="4091f-183">Process</span></span>

<span data-ttu-id="4091f-184">In de Hallo voorbeeld te volgen, traceren we een binnenkomend bericht op een manier op dezelfde manier toohow we een binnenkomende HTTP trace-aanvragen:</span><span class="sxs-lookup"><span data-stu-id="4091f-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

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

<span data-ttu-id="4091f-185">Op dezelfde manier kunnen andere bewerkingen wachtrij worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4091f-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="4091f-186">Een bewerking peek moet geïnstrumenteerd op een vergelijkbare manier als een bewerking van de wachtrij halen.</span><span class="sxs-lookup"><span data-stu-id="4091f-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="4091f-187">Wachtrij-beheerbewerkingen instrumenteren is niet nodig.</span><span class="sxs-lookup"><span data-stu-id="4091f-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="4091f-188">Application Insights houdt bewerkingen zoals HTTP en in de meeste gevallen is voldoende.</span><span class="sxs-lookup"><span data-stu-id="4091f-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="4091f-189">Wanneer u softwareontwikkelaars verwijdering van berichten, zorg er dan voor dat u Hallo bewerking-id's (correlatie) instellen.</span><span class="sxs-lookup"><span data-stu-id="4091f-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="4091f-190">U kunt ook hello gebruiken `Activity` API.</span><span class="sxs-lookup"><span data-stu-id="4091f-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="4091f-191">Vervolgens hoeft u niet tooset bewerking-id's op Hallo telemetrie-items omdat Application Insights dit gebeurt:</span><span class="sxs-lookup"><span data-stu-id="4091f-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="4091f-192">Maak een nieuwe `Activity` nadat u hebt een item uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="4091f-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="4091f-193">Gebruik `Activity.SetParentId(message.ParentId)` toocorrelate consumer en producent Logboeken.</span><span class="sxs-lookup"><span data-stu-id="4091f-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="4091f-194">Hallo Start `Activity`.</span><span class="sxs-lookup"><span data-stu-id="4091f-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="4091f-195">Bijhouden in wachtrij, verwerken en verwijderen van bewerkingen met behulp van `Start/StopOperation` helpers.</span><span class="sxs-lookup"><span data-stu-id="4091f-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="4091f-196">Dit doen vanaf Hallo dezelfde asynchrone transportbesturing (uitvoeringscontext).</span><span class="sxs-lookup"><span data-stu-id="4091f-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="4091f-197">Op deze manier bent ze gecorreleerde goed.</span><span class="sxs-lookup"><span data-stu-id="4091f-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="4091f-198">Stop Hallo `Activity`.</span><span class="sxs-lookup"><span data-stu-id="4091f-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="4091f-199">Gebruik `Start/StopOperation`, of bel `Track` telemetrie handmatig.</span><span class="sxs-lookup"><span data-stu-id="4091f-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="4091f-200">Batchverwerking</span><span class="sxs-lookup"><span data-stu-id="4091f-200">Batch processing</span></span>
<span data-ttu-id="4091f-201">Sommige wachtrijen, kunt u meerdere berichten met één aanvraag in wachtrij.</span><span class="sxs-lookup"><span data-stu-id="4091f-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="4091f-202">Dergelijke berichten worden verwerkt, is waarschijnlijk onafhankelijk en verschillende logische bewerkingen toohello behoort.</span><span class="sxs-lookup"><span data-stu-id="4091f-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="4091f-203">In dit geval wordt het is niet mogelijk toocorrelate hello `Dequeue` bewerking tooparticular berichtverwerking.</span><span class="sxs-lookup"><span data-stu-id="4091f-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="4091f-204">Elk bericht moet worden verwerkt in de eigen asynchrone Controlestroom.</span><span class="sxs-lookup"><span data-stu-id="4091f-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="4091f-205">Zie voor meer informatie, Hallo [uitgaande afhankelijkheden bijhouden](#outgoing-dependencies-tracking) sectie.</span><span class="sxs-lookup"><span data-stu-id="4091f-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="4091f-206">Achtergrondtaken langlopende</span><span class="sxs-lookup"><span data-stu-id="4091f-206">Long-running background tasks</span></span>
<span data-ttu-id="4091f-207">Sommige toepassingen starten langlopende bewerkingen die kunnen worden veroorzaakt door het aanvragen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4091f-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="4091f-208">Vanuit het perspectief van de tracering/instrumentation hello, van verschilt niet van de aanvraag of een afhankelijkheid instrumentation:</span><span class="sxs-lookup"><span data-stu-id="4091f-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

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

<span data-ttu-id="4091f-209">In dit voorbeeld gebruiken we `telemetryClient.StartOperation` toocreate `RequestTelemetry` en opvulling Hallo correlatie context.</span><span class="sxs-lookup"><span data-stu-id="4091f-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="4091f-210">Stel dat u hebt een bovenliggende-bewerking die is gemaakt door de inkomende aanvragen dat Hallo-bewerking geplande.</span><span class="sxs-lookup"><span data-stu-id="4091f-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="4091f-211">Zolang `BackgroundTask` gestart in Hallo dezelfde asynchrone Controlestroom als een inkomende aanvraag, deze worden gecorreleerd met die bovenliggende voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="4091f-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="4091f-212">`BackgroundTask`en alle geneste telemetrie-items automatisch worden gecorreleerd met Hallo-aanvraag, waardoor er, zelfs nadat het Hallo-aanvraag wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="4091f-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="4091f-213">Wanneer Hallo-taak wordt gestart van Hallo achtergrondthread dat geen bewerkingen (`Activity`) gekoppeld, `BackgroundTask` heeft een bovenliggende geen.</span><span class="sxs-lookup"><span data-stu-id="4091f-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="4091f-214">Echter, het kan hebben genest bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="4091f-214">However, it can have nested operations.</span></span> <span data-ttu-id="4091f-215">Alle telemetrie-items van de taak Hallo gerapporteerd zijn gecorreleerde toohello `RequestTelemetry` gemaakt in `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="4091f-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="4091f-216">Uitgaande afhankelijkheden bijhouden</span><span class="sxs-lookup"><span data-stu-id="4091f-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="4091f-217">U kunt uw eigen soort afhankelijkheid of een bewerking die niet wordt ondersteund door de Application Insights bijhouden.</span><span class="sxs-lookup"><span data-stu-id="4091f-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="4091f-218">Hallo `Enqueue` methode in de Service Bus-wachtrij Hallo of Hallo opslagwachtrij kan fungeren als voorbeelden van dergelijke aangepaste bijhouden.</span><span class="sxs-lookup"><span data-stu-id="4091f-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="4091f-219">Hallo algemeen de aanpak voor het bijhouden van aangepaste afhankelijkheid is:</span><span class="sxs-lookup"><span data-stu-id="4091f-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="4091f-220">Hallo aanroepen `TelemetryClient.StartOperation` (extensie)-methode die wordt gevuld Hallo `DependencyTelemetry` eigenschappen die nodig zijn voor correlatie en andere eigenschappen (begintijd stempel, duur).</span><span class="sxs-lookup"><span data-stu-id="4091f-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="4091f-221">Andere aangepaste eigenschappen worden ingesteld op Hallo `DependencyTelemetry`, zoals het Hallo-naam en een andere context die u nodig.</span><span class="sxs-lookup"><span data-stu-id="4091f-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="4091f-222">Controleer een afhankelijkheid bellen en een ogenblik geduld.</span><span class="sxs-lookup"><span data-stu-id="4091f-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="4091f-223">Hallo-bewerking met stoppen `StopOperation` wanneer deze voltooid.</span><span class="sxs-lookup"><span data-stu-id="4091f-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="4091f-224">Uitzonderingen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4091f-224">Handle exceptions.</span></span>

<span data-ttu-id="4091f-225">`StopOperation`alleen gestopt Hallo die is gestart.</span><span class="sxs-lookup"><span data-stu-id="4091f-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="4091f-226">Als de huidige actieve bewerking Hallo komt niet overeen met de Hallo een gewenste toostop, `StopOperation` , gebeurt er niets.</span><span class="sxs-lookup"><span data-stu-id="4091f-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="4091f-227">Deze situatie kan gebeuren als u meerdere bewerkingen parallel in Hallo start dezelfde uitvoeringscontext:</span><span class="sxs-lookup"><span data-stu-id="4091f-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

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

<span data-ttu-id="4091f-228">Zorg ervoor dat u altijd aanroepen `StartOperation` en voert u de taak in een eigen context:</span><span class="sxs-lookup"><span data-stu-id="4091f-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="4091f-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4091f-229">Next steps</span></span>

- <span data-ttu-id="4091f-230">Leer de basisbeginselen Hallo van [telemetrie correlatie](application-insights-correlation.md) in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4091f-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="4091f-231">Zie Hallo [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.</span><span class="sxs-lookup"><span data-stu-id="4091f-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="4091f-232">Aangepast rapport [gebeurtenissen en metrische gegevens](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="4091f-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="4091f-233">Bekijk standaard [configuratie](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) voor context eigenschappen verzameling.</span><span class="sxs-lookup"><span data-stu-id="4091f-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="4091f-234">Controleer Hallo [System.Diagnostics.Activity gebruikershandleiding](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee hoe we telemetrie correleren.</span><span class="sxs-lookup"><span data-stu-id="4091f-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
