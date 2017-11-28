---
title: aaaApp Service API-app-triggers | Microsoft Docs
description: Hoe tooimplement activeert in een API-App in Azure App Service
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="850da-103">API-app-triggers voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="850da-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="850da-104">Deze versie van Hallo artikel geldt tooAPI apps 2014-12-01-preview-schemaversie.</span><span class="sxs-lookup"><span data-stu-id="850da-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="850da-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="850da-105">Overview</span></span>
<span data-ttu-id="850da-106">Dit artikel wordt uitgelegd hoe tooimplement API app getriggerd en gebruiken van een logische app.</span><span class="sxs-lookup"><span data-stu-id="850da-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="850da-107">Alle Hallo codefragmenten in dit onderwerp worden gekopieerd van Hallo [FileWatcher API-App-codevoorbeeld](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="850da-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="850da-108">Opmerking moet u toodownload Hallo volgende nuget-pakket voor Hallo-code in dit artikel toobuild en voer: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="850da-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="850da-109">Wat API app-triggers zijn?</span><span class="sxs-lookup"><span data-stu-id="850da-109">What are API app triggers?</span></span>
<span data-ttu-id="850da-110">Is een veelvoorkomend scenario voor een API-app toofire een gebeurtenis zodat clients van de API-app Hallo antwoord toohello gebeurtenis Hallo passende maatregelen kunnen nemen.</span><span class="sxs-lookup"><span data-stu-id="850da-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="850da-111">Hallo op basis van REST-API-mechanisme die ondersteuning biedt voor dit scenario wordt een API-app-trigger genoemd.</span><span class="sxs-lookup"><span data-stu-id="850da-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="850da-112">Bijvoorbeeld, Stel dat uw clientcode maakt gebruik van Hallo [Twitter-Connector-API-app](../connectors/connectors-create-api-twitter.md) en uw code moet tooperform een actie op basis van nieuwe tweets die bepaalde woorden bevatten.</span><span class="sxs-lookup"><span data-stu-id="850da-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="850da-113">In dit geval wordt u mogelijk instellen een poll of push trigger toofacilitate deze behoefte.</span><span class="sxs-lookup"><span data-stu-id="850da-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="850da-114">Poll-trigger versus push-signaal</span><span class="sxs-lookup"><span data-stu-id="850da-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="850da-115">Op dit moment kunnen worden twee soorten triggers ondersteund:</span><span class="sxs-lookup"><span data-stu-id="850da-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="850da-116">Poll-trigger - Client worden opgevraagd Hallo API-app voor melding van een gebeurtenis die is verwijderd</span><span class="sxs-lookup"><span data-stu-id="850da-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="850da-117">Push-signaal - Client wordt door Hallo API-app geïnformeerd wanneer een gebeurtenis wordt gestart</span><span class="sxs-lookup"><span data-stu-id="850da-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="850da-118">Poll-trigger</span><span class="sxs-lookup"><span data-stu-id="850da-118">Poll trigger</span></span>
<span data-ttu-id="850da-119">Een poll-trigger is geïmplementeerd als een reguliere REST-API en de toopoll clients (zoals een logische app) verwacht in volgorde tooget melding.</span><span class="sxs-lookup"><span data-stu-id="850da-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="850da-120">Tijdens het Hallo-client kan de status behouden, is Hallo poll trigger zelf staatloze.</span><span class="sxs-lookup"><span data-stu-id="850da-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="850da-121">Hallo volgende informatie met betrekking tot hello-pakketten voor aanvraag- en ziet u enkele belangrijke aspecten van Hallo poll trigger contract:</span><span class="sxs-lookup"><span data-stu-id="850da-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="850da-122">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="850da-122">Request</span></span>
  * <span data-ttu-id="850da-123">HTTP-methode: ophalen</span><span class="sxs-lookup"><span data-stu-id="850da-123">HTTP method: GET</span></span>
  * <span data-ttu-id="850da-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="850da-124">Parameters</span></span>
    * <span data-ttu-id="850da-125">triggerState - deze optionele parameter kan clients toospecify hun status, zodat die poll trigger Hallo goed kunt bepalen of tooreturn melding of niet op basis van Hallo status opgegeven.</span><span class="sxs-lookup"><span data-stu-id="850da-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="850da-126">API-specifieke parameters</span><span class="sxs-lookup"><span data-stu-id="850da-126">API-specific parameters</span></span>
* <span data-ttu-id="850da-127">Antwoord</span><span class="sxs-lookup"><span data-stu-id="850da-127">Response</span></span>
  * <span data-ttu-id="850da-128">Statuscode **200** - aanvraag geldig is en er is een melding van Hallo-trigger.</span><span class="sxs-lookup"><span data-stu-id="850da-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="850da-129">Hallo-inhoud van het Hallo-melding worden Hallo antwoordtekst.</span><span class="sxs-lookup"><span data-stu-id="850da-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="850da-130">Een header 'Opnieuw proberen na' hello antwoord geeft aan dat er aanvullende kennisgeving gegevens met een aanroep van de volgende aanvraag moet worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="850da-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="850da-131">Statuscode **202** - aanvraag is geldig, maar er is geen nieuwe melding van Hallo-trigger.</span><span class="sxs-lookup"><span data-stu-id="850da-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="850da-132">Statuscode **4xx** -aanvraag is niet geldig.</span><span class="sxs-lookup"><span data-stu-id="850da-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="850da-133">Hallo-client moet Hallo-aanvraag niet opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="850da-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="850da-134">Statuscode **5xx** -aanvraag heeft geleid tot een interne serverfout en/of een tijdelijk probleem.</span><span class="sxs-lookup"><span data-stu-id="850da-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="850da-135">Hallo-client moet Hallo aanvraag opnieuw.</span><span class="sxs-lookup"><span data-stu-id="850da-135">hello client should retry hello request.</span></span>

<span data-ttu-id="850da-136">Hallo volgende codefragment is een voorbeeld van hoe een poll tooimplement activeren.</span><span class="sxs-lookup"><span data-stu-id="850da-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="850da-137">tootest deze poll activeert, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="850da-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="850da-138">Hallo API App met een verificatie-instelling van implementeren **openbare anonieme**.</span><span class="sxs-lookup"><span data-stu-id="850da-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="850da-139">Hallo aanroepen **touch** bewerking tootouch een bestand.</span><span class="sxs-lookup"><span data-stu-id="850da-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="850da-140">Hallo volgende afbeelding toont een voorbeeld van een aanvraag via Postman.</span><span class="sxs-lookup"><span data-stu-id="850da-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="850da-141">![Touch-bewerking via Postman aanroepen](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="850da-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="850da-142">Hallo poll trigger Hello aanroepen **triggerState** parameterset tooa tijdstempel voorafgaande tooStep #2.</span><span class="sxs-lookup"><span data-stu-id="850da-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="850da-143">Hallo toont volgende afbeelding Hallo voorbeeld van een aanvraag via Postman.</span><span class="sxs-lookup"><span data-stu-id="850da-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="850da-144">![Poll-Trigger via Postman aanroepen](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="850da-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="850da-145">Push-signaal</span><span class="sxs-lookup"><span data-stu-id="850da-145">Push trigger</span></span>
<span data-ttu-id="850da-146">Een push-signaal is geïmplementeerd als een reguliere REST-API die pushes meldingen tooclients die zich hebben geregistreerd toobe een melding wanneer er specifieke gebeurtenissen gestart.</span><span class="sxs-lookup"><span data-stu-id="850da-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="850da-147">Hallo informatie met betrekking tot hello-pakketten voor aanvraag- en volgende illustratie van enkele belangrijke aspecten van Hallo push trigger contract.</span><span class="sxs-lookup"><span data-stu-id="850da-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="850da-148">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="850da-148">Request</span></span>
  * <span data-ttu-id="850da-149">HTTP-methode: plaatsen</span><span class="sxs-lookup"><span data-stu-id="850da-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="850da-150">Parameters</span><span class="sxs-lookup"><span data-stu-id="850da-150">Parameters</span></span>
    * <span data-ttu-id="850da-151">triggerId: vereist - ondoorzichtig tekenreeks (zoals een GUID) dat vertegenwoordigt de registratie van een push-signaal Hallo.</span><span class="sxs-lookup"><span data-stu-id="850da-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="850da-152">callbackUrl: vereist - URL van Hallo callback tooinvoke wanneer Hallo gebeurtenis wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="850da-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="850da-153">Hallo-aanroep is een eenvoudige HTTP POST-aanroep.</span><span class="sxs-lookup"><span data-stu-id="850da-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="850da-154">API-specifieke parameters</span><span class="sxs-lookup"><span data-stu-id="850da-154">API-specific parameters</span></span>
* <span data-ttu-id="850da-155">Antwoord</span><span class="sxs-lookup"><span data-stu-id="850da-155">Response</span></span>
  * <span data-ttu-id="850da-156">Statuscode **200** -aanvraag tooregister client voltooid.</span><span class="sxs-lookup"><span data-stu-id="850da-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="850da-157">Statuscode **4xx** -aanvraag is niet geldig.</span><span class="sxs-lookup"><span data-stu-id="850da-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="850da-158">Hallo-client moet Hallo-aanvraag niet opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="850da-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="850da-159">Statuscode **5xx** -aanvraag heeft geleid tot een interne serverfout en/of een tijdelijk probleem.</span><span class="sxs-lookup"><span data-stu-id="850da-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="850da-160">Hallo-client moet Hallo aanvraag opnieuw.</span><span class="sxs-lookup"><span data-stu-id="850da-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="850da-161">Terugbellen</span><span class="sxs-lookup"><span data-stu-id="850da-161">Callback</span></span>
  * <span data-ttu-id="850da-162">HTTP-methode: POST</span><span class="sxs-lookup"><span data-stu-id="850da-162">HTTP method: POST</span></span>
  * <span data-ttu-id="850da-163">Aanvraagtekst: berichtinhoud.</span><span class="sxs-lookup"><span data-stu-id="850da-163">Request body: Notification content.</span></span>

<span data-ttu-id="850da-164">Hallo volgende codefragment is een voorbeeld van hoe een push tooimplement activeren:</span><span class="sxs-lookup"><span data-stu-id="850da-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="850da-165">tootest deze poll activeert, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="850da-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="850da-166">Hallo API App met een verificatie-instelling van implementeren **openbare anonieme**.</span><span class="sxs-lookup"><span data-stu-id="850da-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="850da-167">Te bladeren[http://requestb.in/](http://requestb.in/) toocreate een RequestBin die als de URL van uw retouraanroep fungeert.</span><span class="sxs-lookup"><span data-stu-id="850da-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="850da-168">Hallo push trigger met een GUID als aanroepen **triggerId** en RequestBin URL als Hallo **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="850da-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="850da-169">![Push-signaal via Postman aanroepen](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="850da-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="850da-170">Hallo aanroepen **touch** bewerking tootouch een bestand.</span><span class="sxs-lookup"><span data-stu-id="850da-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="850da-171">Hallo volgende afbeelding toont een voorbeeld van een aanvraag via Postman.</span><span class="sxs-lookup"><span data-stu-id="850da-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="850da-172">![Touch-bewerking via Postman aanroepen](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="850da-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="850da-173">Controleer Hallo RequestBin tooconfirm die Hallo push trigger retouraanroep wordt aangeroepen met de eigenschap uitvoer.</span><span class="sxs-lookup"><span data-stu-id="850da-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="850da-174">![Poll-Trigger via Postman aanroepen](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="850da-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="850da-175">Beschrijven triggers in API-definitie</span><span class="sxs-lookup"><span data-stu-id="850da-175">Describe triggers in API definition</span></span>
<span data-ttu-id="850da-176">Ga na Hallo triggers implementeren en uw tooAzure API-app implementeren, toohello **API-definitie** blade in hello Azure preview-portal en u ziet triggers worden automatisch herkend in Hallo-gebruikersinterface die wordt aangedreven door Hello Swagger 2.0 API-definitie van Hallo API-app.</span><span class="sxs-lookup"><span data-stu-id="850da-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![API-definitie-Blade](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="850da-178">Als u klikt op Hallo **downloaden Swagger** knop en open Hallo JSON-bestand, ziet u de resultaten vergelijkbare toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="850da-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="850da-179">Hallo uitbreidingseigenschap **x-ms-schedular-trigger** is hoe triggers worden beschreven in de API-definitie en automatisch door Hallo API app gateway wordt toegevoegd wanneer u Hallo API-definitie via Hallo gateway aanvragen als Hallo tooone van aanvragen Hallo criteria te volgen.</span><span class="sxs-lookup"><span data-stu-id="850da-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="850da-180">(U kunt ook deze eigenschap handmatig toevoegen.)</span><span class="sxs-lookup"><span data-stu-id="850da-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="850da-181">Poll-trigger</span><span class="sxs-lookup"><span data-stu-id="850da-181">Poll trigger</span></span>
  * <span data-ttu-id="850da-182">Als HTTP-methode Hallo **ophalen**.</span><span class="sxs-lookup"><span data-stu-id="850da-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="850da-183">Als hello **operationId** eigenschap bevat Hallo tekenreeks **trigger**.</span><span class="sxs-lookup"><span data-stu-id="850da-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="850da-184">Als hello **parameters** eigenschap bevat een parameter met een **naam** eigenschappenset te**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="850da-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="850da-185">Push-signaal</span><span class="sxs-lookup"><span data-stu-id="850da-185">Push trigger</span></span>
  * <span data-ttu-id="850da-186">Als HTTP-methode Hallo **plaatsen**.</span><span class="sxs-lookup"><span data-stu-id="850da-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="850da-187">Als hello **operationId** eigenschap bevat Hallo tekenreeks **trigger**.</span><span class="sxs-lookup"><span data-stu-id="850da-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="850da-188">Als hello **parameters** eigenschap bevat een parameter met een **naam** eigenschappenset te**triggerId**.</span><span class="sxs-lookup"><span data-stu-id="850da-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="850da-189">API app-triggers gebruiken in Logic apps</span><span class="sxs-lookup"><span data-stu-id="850da-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="850da-190">Weergeven en configureren van de API app-triggers in Hallo Logic apps ontwerpen</span><span class="sxs-lookup"><span data-stu-id="850da-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="850da-191">Als u een logische app in Hallo maken dezelfde resourcegroep als Hallo API-app, kunt u zich kunt tooadd het toohello designer-canvas gewoon door erop te klikken.</span><span class="sxs-lookup"><span data-stu-id="850da-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="850da-192">Hallo volgende afbeeldingen illustreren dit:</span><span class="sxs-lookup"><span data-stu-id="850da-192">hello following images illustrate this:</span></span>

![Triggers in Logic App-ontwerper](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Poll-Trigger in Logic App-ontwerper configureren](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Push-signaal in Logic App-ontwerper configureren](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="850da-196">API-app-triggers voor Logic apps optimaliseren</span><span class="sxs-lookup"><span data-stu-id="850da-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="850da-197">Nadat u triggers tooan API-app toevoegt, zijn er enkele dingen die u kunt tooimprove Hallo ervaring kunt doen wanneer Hallo API-app in een logische app.</span><span class="sxs-lookup"><span data-stu-id="850da-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="850da-198">Bijvoorbeeld: Hallo **triggerState** parameter voor de poll-triggers toohello na expressie in Hallo logische app moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="850da-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="850da-199">Deze expressie moet evalueren Hallo laatste aanroep van de trigger Hallo van Hallo logische app en dat de waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="850da-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="850da-200">Opmerking: Voor een uitleg van Hallo-functies in de bovenstaande Hallo-expressie gebruikt, Raadpleeg de documentatie toohello op [Logic App werkstroom Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="850da-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="850da-201">Logic app-gebruikers tooprovide Hallo expressie hierboven nodig voor Hallo **triggerState** parameter tijdens het Hallo-trigger gebruikt.</span><span class="sxs-lookup"><span data-stu-id="850da-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="850da-202">Het is mogelijk toohave voorinstelling deze waarde door Hallo Logic app-ontwerper via de eigenschap extension Hallo **x-ms-scheduler-aanbeveling**.</span><span class="sxs-lookup"><span data-stu-id="850da-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="850da-203">Hallo **x-ms-zichtbaarheid** uitbreidingseigenschap tooa waarde kan worden ingesteld *interne* zodat Hallo parameter zelf niet wordt weergegeven op Hallo designer.</span><span class="sxs-lookup"><span data-stu-id="850da-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="850da-204">Hallo volgende codefragment ziet u dat.</span><span class="sxs-lookup"><span data-stu-id="850da-204">hello following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="850da-205">Voor de push-triggers Hallo **triggerId** parameter moet een unieke identificatie Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="850da-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="850da-206">Een aanbevolen procedure is tooset deze toohello eigenschapsnaam van Hallo werkstroom met behulp van Hallo expressie te volgen:</span><span class="sxs-lookup"><span data-stu-id="850da-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="850da-207">Met behulp van Hallo **x-ms-scheduler-aanbeveling** en **x-ms-zichtbaarheid** eigenschappen van de extensie in de API-definitie, Hallo API-app kunnen overbrengen toohello Logic app designer tooautomatically dit instellen expressie voor het Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="850da-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="850da-208">Eigenschappen van de extensie in API-definition toevoegen</span><span class="sxs-lookup"><span data-stu-id="850da-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="850da-209">Informatie over aanvullende metagegevens - zoals Hallo uitbreidingseigenschappen **x-ms-scheduler-aanbeveling** en **x-ms-zichtbaarheid** -kunnen worden toegevoegd in Hallo API-definition op twee manieren: statisch of dynamisch.</span><span class="sxs-lookup"><span data-stu-id="850da-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="850da-210">Voor statische metagegevens kunt u direct Hallo bewerken */metadata/apiDefinition.swagger.json* -bestand in uw project en Hallo eigenschappen handmatig toevoegen.</span><span class="sxs-lookup"><span data-stu-id="850da-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="850da-211">Voor API-apps met dynamische metagegevens, kunt u Hallo SwaggerConfig.cs bestand tooadd een bewerking met het filter dat deze uitbreidingen kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="850da-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="850da-212">Hallo Hier volgt een voorbeeld van hoe deze klasse geïmplementeerd toofacilitate Hallo dynamische metagegevens scenario kan zijn.</span><span class="sxs-lookup"><span data-stu-id="850da-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
