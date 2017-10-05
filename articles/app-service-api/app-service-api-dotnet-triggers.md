---
title: App Service API-app-triggers | Microsoft Docs
description: Triggers implementeren in een API-App in Azure App Service
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
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="4d9b7-103">API-app-triggers voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4d9b7-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="4d9b7-104">Deze versie van het artikel is van toepassing op API apps-2014-12-01-preview-schemaversie.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="4d9b7-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4d9b7-105">Overview</span></span>
<span data-ttu-id="4d9b7-106">In dit artikel wordt uitgelegd hoe API app-triggers implementeren en gebruiken van een logische app.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="4d9b7-107">Alle van de codefragmenten in dit onderwerp worden gekopieerd van de [FileWatcher API-App-codevoorbeeld](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="4d9b7-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="4d9b7-108">Merk op dat u wilt downloaden van de volgende nuget-pakket voor de code in dit artikel om te bouwen en uitvoeren: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="4d9b7-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="4d9b7-109">Wat API app-triggers zijn?</span><span class="sxs-lookup"><span data-stu-id="4d9b7-109">What are API app triggers?</span></span>
<span data-ttu-id="4d9b7-110">Het is een veelvoorkomend scenario voor een API-app zodat clients van de API-app de juiste actie in reactie op de gebeurtenis ondernemen kunnen een gebeurtenis wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="4d9b7-111">Het mechanisme voor op basis van REST-API die ondersteuning biedt voor dit scenario wordt een API-app-trigger genoemd.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="4d9b7-112">Bijvoorbeeld, Stel dat uw clientcode maakt gebruik van de [Twitter-Connector-API-app](../connectors/connectors-create-api-twitter.md) en uw code nodig zijn voor een actie die op basis van nieuwe tweets die bepaalde woorden bevatten.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="4d9b7-113">U mogelijk in dit geval een poll of push trigger instellen om deze behoefte.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="4d9b7-114">Poll-trigger versus push-signaal</span><span class="sxs-lookup"><span data-stu-id="4d9b7-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="4d9b7-115">Op dit moment kunnen worden twee soorten triggers ondersteund:</span><span class="sxs-lookup"><span data-stu-id="4d9b7-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="4d9b7-116">Poll-trigger - Client controleert de API-app voor melding van een gebeurtenis die is verwijderd</span><span class="sxs-lookup"><span data-stu-id="4d9b7-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="4d9b7-117">Push-signaal - Client wordt door de API-app geïnformeerd wanneer een gebeurtenis wordt gestart</span><span class="sxs-lookup"><span data-stu-id="4d9b7-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="4d9b7-118">Poll-trigger</span><span class="sxs-lookup"><span data-stu-id="4d9b7-118">Poll trigger</span></span>
<span data-ttu-id="4d9b7-119">Een poll-trigger is geïmplementeerd als een reguliere REST-API en poll-om op te halen van de melding wordt verwacht dat de clients (zoals een logische app).</span><span class="sxs-lookup"><span data-stu-id="4d9b7-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="4d9b7-120">Terwijl de client de status behouden kan, is de poll-trigger zelf staatloze.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="4d9b7-121">De volgende gegevens over de aanvraag en antwoord pakketten illustratie van enkele belangrijke aspecten van het contract van de trigger poll:</span><span class="sxs-lookup"><span data-stu-id="4d9b7-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="4d9b7-122">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="4d9b7-122">Request</span></span>
  * <span data-ttu-id="4d9b7-123">HTTP-methode: ophalen</span><span class="sxs-lookup"><span data-stu-id="4d9b7-123">HTTP method: GET</span></span>
  * <span data-ttu-id="4d9b7-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="4d9b7-124">Parameters</span></span>
    * <span data-ttu-id="4d9b7-125">triggerState - deze optionele parameter kan clients opgeven dat hun status, zodat de poll-trigger goed beslissen om terug te keren melding of niet op basis van de opgegeven status.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="4d9b7-126">API-specifieke parameters</span><span class="sxs-lookup"><span data-stu-id="4d9b7-126">API-specific parameters</span></span>
* <span data-ttu-id="4d9b7-127">Antwoord</span><span class="sxs-lookup"><span data-stu-id="4d9b7-127">Response</span></span>
  * <span data-ttu-id="4d9b7-128">Statuscode **200** - aanvraag geldig is en er is een melding van de trigger.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="4d9b7-129">De inhoud van de melding worden de antwoordtekst.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="4d9b7-130">Een header 'Opnieuw proberen na' in het antwoord geeft aan dat er aanvullende kennisgeving gegevens met een aanroep van de volgende aanvraag moet worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="4d9b7-131">Statuscode **202** - aanvraag is geldig, maar er is geen nieuwe melding van de trigger.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="4d9b7-132">Statuscode **4xx** -aanvraag is niet geldig.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="4d9b7-133">De client moet de aanvraag niet opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="4d9b7-134">Statuscode **5xx** -aanvraag heeft geleid tot een interne serverfout en/of een tijdelijk probleem.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="4d9b7-135">De client moet de aanvraag opnieuw te proberen.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-135">The client should retry the request.</span></span>

<span data-ttu-id="4d9b7-136">Het volgende codefragment is een voorbeeld van het implementeren van een poll-trigger.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="4d9b7-137">Als u wilt testen deze trigger poll, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4d9b7-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="4d9b7-138">Implementeer de API-App met een verificatie-instelling van **openbare anonieme**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="4d9b7-139">Roep de **touch** bewerking touch van een bestand.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="4d9b7-140">De volgende afbeelding toont een voorbeeld van een aanvraag via Postman.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="4d9b7-141">![Touch-bewerking via Postman aanroepen](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="4d9b7-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="4d9b7-142">Roep de poll-trigger met de **triggerState** parameter ingesteld op een tijdstempel vóór stap 2.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="4d9b7-143">De volgende afbeelding toont de voorbeeld-aanvraag via Postman.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="4d9b7-144">![Poll-Trigger via Postman aanroepen](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="4d9b7-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="4d9b7-145">Push-signaal</span><span class="sxs-lookup"><span data-stu-id="4d9b7-145">Push trigger</span></span>
<span data-ttu-id="4d9b7-146">Een push-signaal is geïmplementeerd als een reguliere REST-API die meldingen verstuurd naar clients die zich hebben geregistreerd wilt worden gewaarschuwd als specifieke gebeurtenissen worden gestart.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="4d9b7-147">De volgende gegevens over de aanvraag en antwoord pakketten illustratie van enkele belangrijke aspecten van de push-trigger-contract.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="4d9b7-148">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="4d9b7-148">Request</span></span>
  * <span data-ttu-id="4d9b7-149">HTTP-methode: plaatsen</span><span class="sxs-lookup"><span data-stu-id="4d9b7-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="4d9b7-150">Parameters</span><span class="sxs-lookup"><span data-stu-id="4d9b7-150">Parameters</span></span>
    * <span data-ttu-id="4d9b7-151">triggerId: vereist - ondoorzichtige tekenreeks (zoals een GUID) voor de registratie van een push-trigger.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="4d9b7-152">callbackUrl: vereist - URL van de callback moet worden aangeroepen wanneer de gebeurtenis wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="4d9b7-153">De aanroep is een eenvoudige HTTP POST-aanroep.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="4d9b7-154">API-specifieke parameters</span><span class="sxs-lookup"><span data-stu-id="4d9b7-154">API-specific parameters</span></span>
* <span data-ttu-id="4d9b7-155">Antwoord</span><span class="sxs-lookup"><span data-stu-id="4d9b7-155">Response</span></span>
  * <span data-ttu-id="4d9b7-156">Statuscode **200** -aanvraag voor het registreren van de client is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="4d9b7-157">Statuscode **4xx** -aanvraag is niet geldig.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="4d9b7-158">De client moet de aanvraag niet opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="4d9b7-159">Statuscode **5xx** -aanvraag heeft geleid tot een interne serverfout en/of een tijdelijk probleem.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="4d9b7-160">De client moet de aanvraag opnieuw te proberen.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-160">The client should retry the request.</span></span>
* <span data-ttu-id="4d9b7-161">Terugbellen</span><span class="sxs-lookup"><span data-stu-id="4d9b7-161">Callback</span></span>
  * <span data-ttu-id="4d9b7-162">HTTP-methode: POST</span><span class="sxs-lookup"><span data-stu-id="4d9b7-162">HTTP method: POST</span></span>
  * <span data-ttu-id="4d9b7-163">Aanvraagtekst: berichtinhoud.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-163">Request body: Notification content.</span></span>

<span data-ttu-id="4d9b7-164">Het volgende codefragment is een voorbeeld van het implementeren van een push-signaal:</span><span class="sxs-lookup"><span data-stu-id="4d9b7-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
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
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="4d9b7-165">Als u wilt testen deze trigger poll, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4d9b7-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="4d9b7-166">Implementeer de API-App met een verificatie-instelling van **openbare anonieme**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="4d9b7-167">Blader naar [http://requestb.in/](http://requestb.in/) voor het maken van een RequestBin die als de URL van uw retouraanroep fungeert.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="4d9b7-168">Aanroepen van de push-trigger met een GUID als **triggerId** en de URL RequestBin als **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="4d9b7-169">![Push-signaal via Postman aanroepen](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="4d9b7-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="4d9b7-170">Roep de **touch** bewerking touch van een bestand.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="4d9b7-171">De volgende afbeelding toont een voorbeeld van een aanvraag via Postman.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="4d9b7-172">![Touch-bewerking via Postman aanroepen](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="4d9b7-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="4d9b7-173">Controleer de RequestBin om te bevestigen dat de callback van de trigger push is aangeroepen met de eigenschap uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="4d9b7-174">![Poll-Trigger via Postman aanroepen](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="4d9b7-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="4d9b7-175">Beschrijven triggers in API-definitie</span><span class="sxs-lookup"><span data-stu-id="4d9b7-175">Describe triggers in API definition</span></span>
<span data-ttu-id="4d9b7-176">Nadat de triggers implementeren en uw API-app implementeren naar Azure, gaat u naar de **API-definitie** blade in de Azure preview-portal en u ziet triggers worden automatisch herkend in de gebruikersinterface wordt aangedreven door de Swagger 2.0 API-definitie van de API-app.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![API-definitie-Blade](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="4d9b7-178">Als u op de **downloaden Swagger** knop en opent u het JSON-bestand, ziet u resultaten die vergelijkbaar is met het volgende:</span><span class="sxs-lookup"><span data-stu-id="4d9b7-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

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

<span data-ttu-id="4d9b7-179">De eigenschap extension **x-ms-schedular-trigger** is hoe triggers worden beschreven in de API-definitie en automatisch door de API-app-gateway wordt toegevoegd wanneer u via de gateway van de API-definitie aanvragen als de aanvraag voor een van de de volgende criteria.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="4d9b7-180">(U kunt ook deze eigenschap handmatig toevoegen.)</span><span class="sxs-lookup"><span data-stu-id="4d9b7-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="4d9b7-181">Poll-trigger</span><span class="sxs-lookup"><span data-stu-id="4d9b7-181">Poll trigger</span></span>
  * <span data-ttu-id="4d9b7-182">Als de HTTP-methode is **ophalen**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="4d9b7-183">Als de **operationId** eigenschap bevat de tekenreeks **trigger**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="4d9b7-184">Als de **parameters** eigenschap bevat een parameter met een **naam** eigenschap ingesteld op **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="4d9b7-185">Push-signaal</span><span class="sxs-lookup"><span data-stu-id="4d9b7-185">Push trigger</span></span>
  * <span data-ttu-id="4d9b7-186">Als de HTTP-methode is **plaatsen**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="4d9b7-187">Als de **operationId** eigenschap bevat de tekenreeks **trigger**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="4d9b7-188">Als de **parameters** eigenschap bevat een parameter met een **naam** eigenschap ingesteld op **triggerId**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="4d9b7-189">API app-triggers gebruiken in Logic apps</span><span class="sxs-lookup"><span data-stu-id="4d9b7-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="4d9b7-190">Weergeven en configureren van app-triggers voor API in de ontwerpfunctie voor Logic apps</span><span class="sxs-lookup"><span data-stu-id="4d9b7-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="4d9b7-191">Als u een logische app in dezelfde resourcegroep bevinden als de API-app maakt, kunt u zich kunt toevoegen aan het designer-canvas gewoon door erop te klikken.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="4d9b7-192">De volgende afbeeldingen illustreren dit:</span><span class="sxs-lookup"><span data-stu-id="4d9b7-192">The following images illustrate this:</span></span>

![Triggers in Logic App-ontwerper](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Poll-Trigger in Logic App-ontwerper configureren](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Push-signaal in Logic App-ontwerper configureren](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="4d9b7-196">API-app-triggers voor Logic apps optimaliseren</span><span class="sxs-lookup"><span data-stu-id="4d9b7-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="4d9b7-197">Nadat u triggers aan een API-app toevoegt, zijn er enkele dingen die u doen kunt om de ervaring te verbeteren wanneer u de API-app in een logische app.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="4d9b7-198">Bijvoorbeeld, de **triggerState** parameter voor de poll-triggers moet worden ingesteld op de volgende expressie in de logische app.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="4d9b7-199">Deze expressie moet de laatste aanroep van de trigger van de logische app evalueren en die waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="4d9b7-200">Opmerking: Voor een uitleg van de functies die in de bovenstaande expressie worden gebruikt, Raadpleeg de documentatie op [Logic App werkstroom Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d9b7-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="4d9b7-201">Logic app-gebruikers moeten de expressie hierboven voor de **triggerState** parameter tijdens het gebruik van de trigger.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="4d9b7-202">Het is mogelijk dat deze waarde vooraf ingesteld door de ontwerper Logic app via de eigenschap extension **x-ms-scheduler-aanbeveling**.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="4d9b7-203">De **x-ms-zichtbaarheid** uitbreidingseigenschap kan worden ingesteld op een waarde van *interne* zodat de parameter zelf niet in de ontwerpfunctie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="4d9b7-204">Het volgende fragment illustreert die.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-204">The following snippet illustrates that.</span></span>

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

<span data-ttu-id="4d9b7-205">Voor de push-triggers de **triggerId** parameter moet een unieke identificatie van de logische app.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="4d9b7-206">Aanbevolen wordt deze eigenschap instellen op de naam van de werkstroom met behulp van de volgende expressie:</span><span class="sxs-lookup"><span data-stu-id="4d9b7-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="4d9b7-207">Met behulp van de **x-ms-scheduler-aanbeveling** en **x-ms-zichtbaarheid** eigenschappen van de extensie in de API-definitie, de API-app kunt overbrengen naar de ontwerpfunctie Logic app worden automatisch ingesteld deze expressie voor de de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="4d9b7-208">Eigenschappen van de extensie in API-definition toevoegen</span><span class="sxs-lookup"><span data-stu-id="4d9b7-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="4d9b7-209">Informatie over aanvullende metagegevens - zoals de uitbreidingseigenschappen **x-ms-scheduler-aanbeveling** en **x-ms-zichtbaarheid** -kunnen worden toegevoegd in de API-definition op twee manieren: statisch of dynamisch.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="4d9b7-210">Voor statische metagegevens kunt u direct bewerken de */metadata/apiDefinition.swagger.json* -bestand in uw project en de eigenschappen handmatig toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="4d9b7-211">Voor API-apps met dynamische metagegevens, kunt u het bestand SwaggerConfig.cs voor het toevoegen van een bewerking met het filter dat deze uitbreidingen kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="4d9b7-212">Hier volgt een voorbeeld van hoe deze klasse kan worden geïmplementeerd om te vergemakkelijken van het scenario dynamisch metagegevens.</span><span class="sxs-lookup"><span data-stu-id="4d9b7-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
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
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
