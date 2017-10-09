---
title: aaaMonitor Node.js services met Azure Application Insights | Microsoft Docs
description: Prestaties bewaken en problemen detecteren in Node.js-services met Application Insights.
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="44ffb-103">Node.js-services en -apps bewaken met Application Insights</span><span class="sxs-lookup"><span data-stu-id="44ffb-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="44ffb-104">[Azure Application Insights](app-insights-overview.md) bewaakt uw back-end-services en onderdelen nadat u ze toohelp implementeert u [detecteren en onderzoeken van prestaties en andere problemen met snel](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="44ffb-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="44ffb-105">Gebruik het voor Node.js-services die overal worden gehost: uw datacenter, Azure VM's en web-apps en zelfs andere openbare clouds.</span><span class="sxs-lookup"><span data-stu-id="44ffb-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="44ffb-106">tooreceive, opslaan, en Verken uw gegevens bewaking, volg Hallo instructies tooinclude een agent in uw code te volgen en een bijbehorende Application Insights-resource in Azure instellen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="44ffb-107">Hallo-agent verzendt gegevens toothat resource voor verdere analyse en te verkennen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="44ffb-108">Hallo Node.js agent kunt automatisch bewaken binnenkomende en uitgaande HTTP-aanvragen, verschillende system metrische gegevens en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="44ffb-109">Vanaf v0.20 kan het ook sommige algemene pakketten van derden bewaken, zoals `mongodb`, `mysql` en `redis`.</span><span class="sxs-lookup"><span data-stu-id="44ffb-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="44ffb-110">Alle gebeurtenissen met betrekking tooan inkomende HTTP-aanvraag zijn gecorreleerd voor sneller probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="44ffb-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="44ffb-111">U kunt meer aspecten van uw app bewaken en system door ze handmatig instrumenteren Hallo verderop agent-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44ffb-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Voorbeeld van grafieken met prestatiebewaking](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="44ffb-113">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="44ffb-113">Getting Started</span></span>

<span data-ttu-id="44ffb-114">We gaan het instellen van de bewaking voor een app of service stapsgewijs doornemen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="44ffb-115"><a name="resource"></a> Een App Insights-resource instellen</span><span class="sxs-lookup"><span data-stu-id="44ffb-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="44ffb-116">**Voordat u begint**, moet u ervoor zorgen dat u een Azure-abonnement hebt of moet u [een gratis nieuw abonnement aanvragen][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="44ffb-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="44ffb-117">Als uw organisatie al beschikt over een Azure-abonnement, een beheerder kan volgen [deze instructies] [ add-aad-user] tooadd u tooit.</span><span class="sxs-lookup"><span data-stu-id="44ffb-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="44ffb-118">Toohello zich nu aanmelden [Azure-portal] [ portal] en een Application Insights-resource maken, zoals geïllustreerd in de volgende Hallo - Klik op 'Nieuw' > 'Hulpprogramma's voor ontwikkelaars' > 'Application Insights'.</span><span class="sxs-lookup"><span data-stu-id="44ffb-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="44ffb-119">Hallo-bron bevat een eindpunt voor het ontvangen van telemetriegegevens, opslag voor deze gegevens, rapporten en dashboards, regel en configuratie van de waarschuwing en meer opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Een App Insights-resource maken](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="44ffb-121">Kies op Hallo resource maken pagina 'Node.js-toepassing' hello toepassing type vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="44ffb-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="44ffb-122">Hallo app type bepaalt de standaardset Hallo van dashboards en rapporten voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44ffb-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="44ffb-123">Maakt u zich echter geen zorgen, want elke App Insights-resource kan gegevens verzamelen vanuit elke taal en elk platform.</span><span class="sxs-lookup"><span data-stu-id="44ffb-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Nieuw App Insights-resourceformulier](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="44ffb-125"><a name="agent"></a>Hallo Node.js agent instellen</span><span class="sxs-lookup"><span data-stu-id="44ffb-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="44ffb-126">Het is nu tijd tooinclude Hallo agent in uw app zodat deze gegevens kan verzamelen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="44ffb-127">Start uw resource Instrumentatiesleutel kopiëren (hierna tooas uw `ikey`) vanuit de portal Hallo zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="44ffb-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="44ffb-128">Hallo App Insights gebruikt deze sleutel toomap gegevens tooyour Azure-resource systeem zodat u toospecify moet in een omgevingsvariabele of uw code voor Hallo agent toouse.</span><span class="sxs-lookup"><span data-stu-id="44ffb-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![Instrumentatiesleutel kopiëren](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="44ffb-130">Voeg vervolgens Hallo Node.js agent bibliotheek tooyour van app-afhankelijkheden via package.json.</span><span class="sxs-lookup"><span data-stu-id="44ffb-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="44ffb-131">Voer het volgende uit Hallo hoofdmap van uw app:</span><span class="sxs-lookup"><span data-stu-id="44ffb-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="44ffb-132">Nu moet u tooexplicitly load Hallo bibliotheek in uw code.</span><span class="sxs-lookup"><span data-stu-id="44ffb-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="44ffb-133">Omdat de agent Hallo injects instrumentation in veel andere bibliotheken, u moet deze laden zo spoedig mogelijk zelfs vóór andere `require` instructies.</span><span class="sxs-lookup"><span data-stu-id="44ffb-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="44ffb-134">tooget gestart, boven Hallo van uw eerste .js bestand toevoegen:</span><span class="sxs-lookup"><span data-stu-id="44ffb-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="44ffb-135">Hallo `setup` methode configureert Hallo instrumentatiesleutel (en dus Azure-resource) toobe standaard gebruikt voor alle bijgehouden items.</span><span class="sxs-lookup"><span data-stu-id="44ffb-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="44ffb-136">Roep `start` nadat de configuratie is voltooid toobegin verzamelen en verzenden van telemetriegegevens.</span><span class="sxs-lookup"><span data-stu-id="44ffb-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="44ffb-137">U kunt ook een ikey via Hallo omgevingsvariabele APPINSIGHTS opgeven\_INSTRUMENTATIONKEY in plaats van te handmatig doorgeven `setup()` of `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="44ffb-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="44ffb-138">Hierdoor kunt u houden ikeys buiten doorgevoerd broncode en andere ikeys toospecify voor verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="44ffb-139">Extra configuratieopties worden hieronder gedocumenteerd.</span><span class="sxs-lookup"><span data-stu-id="44ffb-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="44ffb-140">Hallo agent kunt u proberen zonder telemetrie te verzenden door in te stellen Hallo instrumentation sleutel tooany niet-lege tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="44ffb-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="44ffb-141"><a name="monitor"></a> Uw app bewaken</span><span class="sxs-lookup"><span data-stu-id="44ffb-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="44ffb-142">Hallo agent verzamelt automatisch telemetrie over Hallo Node.js-runtime en een aantal algemene van derden-modules.</span><span class="sxs-lookup"><span data-stu-id="44ffb-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="44ffb-143">Gebruik van uw toepassing nu toogenerate sommige van deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="44ffb-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="44ffb-144">Klik op Hallo [Azure-portal] [ portal] bladeren toohello Application Insights-resource u eerder hebt gemaakt en zoekt u naar uw eerste weinig gegevenspunten in Hallo overzicht tijdlijn, zoals in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="44ffb-145">Klik in de grafieken Hallo voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44ffb-145">Click through hello charts for more details.</span></span>

![Eerste gegevenspunten](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="44ffb-147">Klik op Hallo toepassing kaart knop tooview Hallo topologie gedetecteerd voor uw app, zoals in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="44ffb-148">Klik in de onderdelen in kaart Hallo voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44ffb-148">Click through components in hello map for more details.</span></span>

![Eenvoudig app-kaart](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="44ffb-150">Meer informatie over uw app en problemen oplossen van problemen bij het gebruik van Hallo andere weergaven die beschikbaar zijn onder de sectie 'Onderzoeken' Hallo.</span><span class="sxs-lookup"><span data-stu-id="44ffb-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Sectie onderzoeken](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="44ffb-152">Zijn er geen gegevens?</span><span class="sxs-lookup"><span data-stu-id="44ffb-152">No data?</span></span>

<span data-ttu-id="44ffb-153">Omdat Hallo agent gegevens voor de verzending van batches mogelijk zijn er een vertraging optreden voordat items worden weergegeven in het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="44ffb-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="44ffb-154">Als er geen gegevens in uw resource kunt u proberen Hallo oplossingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="44ffb-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="44ffb-155">Sommige meer; Hallo-toepassing gebruiken meer acties toogenerate meer telemetrie duren.</span><span class="sxs-lookup"><span data-stu-id="44ffb-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="44ffb-156">Klik op **vernieuwen** in de portal resourceweergave Hallo.</span><span class="sxs-lookup"><span data-stu-id="44ffb-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="44ffb-157">Grafieken automatisch worden regelmatig vernieuwd, maar deze toohappen onmiddellijk vernieuwen forceert.</span><span class="sxs-lookup"><span data-stu-id="44ffb-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="44ffb-158">Controleer of [benodigde uitgaande poorten](app-insights-ip-addresses.md) open zijn.</span><span class="sxs-lookup"><span data-stu-id="44ffb-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="44ffb-159">Open Hallo [Search](app-insights-diagnostic-search.md) tegel en zoekt u afzonderlijke gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="44ffb-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="44ffb-160">Controleer de Hallo [Veelgestelde vragen over][].</span><span class="sxs-lookup"><span data-stu-id="44ffb-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="44ffb-161">Agentconfiguratie</span><span class="sxs-lookup"><span data-stu-id="44ffb-161">Agent Configuration</span></span>

<span data-ttu-id="44ffb-162">Hieronder vindt u Hallo-agent configuratiemethoden en hun standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="44ffb-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="44ffb-163">toofully vergelijken gebeurtenissen in een service worden ervoor tooset `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="44ffb-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="44ffb-164">Hierdoor kunnen tootrack context Hallo agent bij asynchrone retouraanroepen in Node.js.</span><span class="sxs-lookup"><span data-stu-id="44ffb-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="44ffb-165">Agent-API</span><span class="sxs-lookup"><span data-stu-id="44ffb-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="44ffb-166">Hallo API voor .NET-agent wordt volledig beschreven [hier](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="44ffb-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="44ffb-167">U kunt een aanvraag, gebeurtenis, metriek of uitzondering Hallo Application Insights Node.js-client met bijhouden.</span><span class="sxs-lookup"><span data-stu-id="44ffb-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="44ffb-168">Hallo volgende voorbeeld toont een aantal Hallo beschikbare API's.</span><span class="sxs-lookup"><span data-stu-id="44ffb-168">hello following example demonstrates some of hello available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="44ffb-169">Afhankelijkheden bijhouden</span><span class="sxs-lookup"><span data-stu-id="44ffb-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="44ffb-170">Een aangepaste eigenschap tooall gebeurtenissen toevoegen</span><span class="sxs-lookup"><span data-stu-id="44ffb-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="44ffb-171">HTTP GET-aanvragen traceren</span><span class="sxs-lookup"><span data-stu-id="44ffb-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="44ffb-172">Serveropstarttijd traceren</span><span class="sxs-lookup"><span data-stu-id="44ffb-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="44ffb-173">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="44ffb-173">More resources</span></span>

* [<span data-ttu-id="44ffb-174">Uw telemetrie in Hallo-portal bewaken</span><span class="sxs-lookup"><span data-stu-id="44ffb-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="44ffb-175">Analysequery’s schrijven over uw telemetrie</span><span class="sxs-lookup"><span data-stu-id="44ffb-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[Veelgestelde vragen over]: app-insights-troubleshoot-faq.md
