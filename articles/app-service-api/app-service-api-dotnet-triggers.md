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
# <a name="azure-app-service-api-app-triggers"></a>API-app-triggers voor Azure App Service
> [!NOTE]
> Deze versie van Hallo artikel geldt tooAPI apps 2014-12-01-preview-schemaversie.
>
>

## <a name="overview"></a>Overzicht
Dit artikel wordt uitgelegd hoe tooimplement API app getriggerd en gebruiken van een logische app.

Alle Hallo codefragmenten in dit onderwerp worden gekopieerd van Hallo [FileWatcher API-App-codevoorbeeld](http://go.microsoft.com/fwlink/?LinkId=534802).

Opmerking moet u toodownload Hallo volgende nuget-pakket voor Hallo-code in dit artikel toobuild en voer: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>Wat API app-triggers zijn?
Is een veelvoorkomend scenario voor een API-app toofire een gebeurtenis zodat clients van de API-app Hallo antwoord toohello gebeurtenis Hallo passende maatregelen kunnen nemen. Hallo op basis van REST-API-mechanisme die ondersteuning biedt voor dit scenario wordt een API-app-trigger genoemd.

Bijvoorbeeld, Stel dat uw clientcode maakt gebruik van Hallo [Twitter-Connector-API-app](../connectors/connectors-create-api-twitter.md) en uw code moet tooperform een actie op basis van nieuwe tweets die bepaalde woorden bevatten. In dit geval wordt u mogelijk instellen een poll of push trigger toofacilitate deze behoefte.

## <a name="poll-trigger-versus-push-trigger"></a>Poll-trigger versus push-signaal
Op dit moment kunnen worden twee soorten triggers ondersteund:

* Poll-trigger - Client worden opgevraagd Hallo API-app voor melding van een gebeurtenis die is verwijderd
* Push-signaal - Client wordt door Hallo API-app geïnformeerd wanneer een gebeurtenis wordt gestart

### <a name="poll-trigger"></a>Poll-trigger
Een poll-trigger is geïmplementeerd als een reguliere REST-API en de toopoll clients (zoals een logische app) verwacht in volgorde tooget melding. Tijdens het Hallo-client kan de status behouden, is Hallo poll trigger zelf staatloze.

Hallo volgende informatie met betrekking tot hello-pakketten voor aanvraag- en ziet u enkele belangrijke aspecten van Hallo poll trigger contract:

* Aanvraag
  * HTTP-methode: ophalen
  * Parameters
    * triggerState - deze optionele parameter kan clients toospecify hun status, zodat die poll trigger Hallo goed kunt bepalen of tooreturn melding of niet op basis van Hallo status opgegeven.
    * API-specifieke parameters
* Antwoord
  * Statuscode **200** - aanvraag geldig is en er is een melding van Hallo-trigger. Hallo-inhoud van het Hallo-melding worden Hallo antwoordtekst. Een header 'Opnieuw proberen na' hello antwoord geeft aan dat er aanvullende kennisgeving gegevens met een aanroep van de volgende aanvraag moet worden opgehaald.
  * Statuscode **202** - aanvraag is geldig, maar er is geen nieuwe melding van Hallo-trigger.
  * Statuscode **4xx** -aanvraag is niet geldig. Hallo-client moet Hallo-aanvraag niet opnieuw proberen.
  * Statuscode **5xx** -aanvraag heeft geleid tot een interne serverfout en/of een tijdelijk probleem. Hallo-client moet Hallo aanvraag opnieuw.

Hallo volgende codefragment is een voorbeeld van hoe een poll tooimplement activeren.

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

tootest deze poll activeert, als volgt te werk:

1. Hallo API App met een verificatie-instelling van implementeren **openbare anonieme**.
2. Hallo aanroepen **touch** bewerking tootouch een bestand. Hallo volgende afbeelding toont een voorbeeld van een aanvraag via Postman.
   ![Touch-bewerking via Postman aanroepen](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Hallo poll trigger Hello aanroepen **triggerState** parameterset tooa tijdstempel voorafgaande tooStep #2. Hallo toont volgende afbeelding Hallo voorbeeld van een aanvraag via Postman.
   ![Poll-Trigger via Postman aanroepen](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Push-signaal
Een push-signaal is geïmplementeerd als een reguliere REST-API die pushes meldingen tooclients die zich hebben geregistreerd toobe een melding wanneer er specifieke gebeurtenissen gestart.

Hallo informatie met betrekking tot hello-pakketten voor aanvraag- en volgende illustratie van enkele belangrijke aspecten van Hallo push trigger contract.

* Aanvraag
  * HTTP-methode: plaatsen
  * Parameters
    * triggerId: vereist - ondoorzichtig tekenreeks (zoals een GUID) dat vertegenwoordigt de registratie van een push-signaal Hallo.
    * callbackUrl: vereist - URL van Hallo callback tooinvoke wanneer Hallo gebeurtenis wordt gestart. Hallo-aanroep is een eenvoudige HTTP POST-aanroep.
    * API-specifieke parameters
* Antwoord
  * Statuscode **200** -aanvraag tooregister client voltooid.
  * Statuscode **4xx** -aanvraag is niet geldig. Hallo-client moet Hallo-aanvraag niet opnieuw proberen.
  * Statuscode **5xx** -aanvraag heeft geleid tot een interne serverfout en/of een tijdelijk probleem. Hallo-client moet Hallo aanvraag opnieuw.
* Terugbellen
  * HTTP-methode: POST
  * Aanvraagtekst: berichtinhoud.

Hallo volgende codefragment is een voorbeeld van hoe een push tooimplement activeren:

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

tootest deze poll activeert, als volgt te werk:

1. Hallo API App met een verificatie-instelling van implementeren **openbare anonieme**.
2. Te bladeren[http://requestb.in/](http://requestb.in/) toocreate een RequestBin die als de URL van uw retouraanroep fungeert.
3. Hallo push trigger met een GUID als aanroepen **triggerId** en RequestBin URL als Hallo **callbackUrl**.
   ![Push-signaal via Postman aanroepen](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Hallo aanroepen **touch** bewerking tootouch een bestand. Hallo volgende afbeelding toont een voorbeeld van een aanvraag via Postman.
   ![Touch-bewerking via Postman aanroepen](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Controleer Hallo RequestBin tooconfirm die Hallo push trigger retouraanroep wordt aangeroepen met de eigenschap uitvoer.
   ![Poll-Trigger via Postman aanroepen](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Beschrijven triggers in API-definitie
Ga na Hallo triggers implementeren en uw tooAzure API-app implementeren, toohello **API-definitie** blade in hello Azure preview-portal en u ziet triggers worden automatisch herkend in Hallo-gebruikersinterface die wordt aangedreven door Hello Swagger 2.0 API-definitie van Hallo API-app.

![API-definitie-Blade](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Als u klikt op Hallo **downloaden Swagger** knop en open Hallo JSON-bestand, ziet u de resultaten vergelijkbare toohello te volgen:

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

Hallo uitbreidingseigenschap **x-ms-schedular-trigger** is hoe triggers worden beschreven in de API-definitie en automatisch door Hallo API app gateway wordt toegevoegd wanneer u Hallo API-definitie via Hallo gateway aanvragen als Hallo tooone van aanvragen Hallo criteria te volgen. (U kunt ook deze eigenschap handmatig toevoegen.)

* Poll-trigger
  * Als HTTP-methode Hallo **ophalen**.
  * Als hello **operationId** eigenschap bevat Hallo tekenreeks **trigger**.
  * Als hello **parameters** eigenschap bevat een parameter met een **naam** eigenschappenset te**triggerState**.
* Push-signaal
  * Als HTTP-methode Hallo **plaatsen**.
  * Als hello **operationId** eigenschap bevat Hallo tekenreeks **trigger**.
  * Als hello **parameters** eigenschap bevat een parameter met een **naam** eigenschappenset te**triggerId**.

## <a name="use-api-app-triggers-in-logic-apps"></a>API app-triggers gebruiken in Logic apps
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Weergeven en configureren van de API app-triggers in Hallo Logic apps ontwerpen
Als u een logische app in Hallo maken dezelfde resourcegroep als Hallo API-app, kunt u zich kunt tooadd het toohello designer-canvas gewoon door erop te klikken. Hallo volgende afbeeldingen illustreren dit:

![Triggers in Logic App-ontwerper](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Poll-Trigger in Logic App-ontwerper configureren](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Push-signaal in Logic App-ontwerper configureren](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>API-app-triggers voor Logic apps optimaliseren
Nadat u triggers tooan API-app toevoegt, zijn er enkele dingen die u kunt tooimprove Hallo ervaring kunt doen wanneer Hallo API-app in een logische app.

Bijvoorbeeld: Hallo **triggerState** parameter voor de poll-triggers toohello na expressie in Hallo logische app moet worden ingesteld. Deze expressie moet evalueren Hallo laatste aanroep van de trigger Hallo van Hallo logische app en dat de waarde retourneren.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Opmerking: Voor een uitleg van Hallo-functies in de bovenstaande Hallo-expressie gebruikt, Raadpleeg de documentatie toohello op [Logic App werkstroom Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Logic app-gebruikers tooprovide Hallo expressie hierboven nodig voor Hallo **triggerState** parameter tijdens het Hallo-trigger gebruikt. Het is mogelijk toohave voorinstelling deze waarde door Hallo Logic app-ontwerper via de eigenschap extension Hallo **x-ms-scheduler-aanbeveling**.  Hallo **x-ms-zichtbaarheid** uitbreidingseigenschap tooa waarde kan worden ingesteld *interne* zodat Hallo parameter zelf niet wordt weergegeven op Hallo designer.  Hallo volgende codefragment ziet u dat.

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

Voor de push-triggers Hallo **triggerId** parameter moet een unieke identificatie Hallo logische app. Een aanbevolen procedure is tooset deze toohello eigenschapsnaam van Hallo werkstroom met behulp van Hallo expressie te volgen:

    @workflow().name

Met behulp van Hallo **x-ms-scheduler-aanbeveling** en **x-ms-zichtbaarheid** eigenschappen van de extensie in de API-definitie, Hallo API-app kunnen overbrengen toohello Logic app designer tooautomatically dit instellen expressie voor het Hallo-gebruiker.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>Eigenschappen van de extensie in API-definition toevoegen
Informatie over aanvullende metagegevens - zoals Hallo uitbreidingseigenschappen **x-ms-scheduler-aanbeveling** en **x-ms-zichtbaarheid** -kunnen worden toegevoegd in Hallo API-definition op twee manieren: statisch of dynamisch.

Voor statische metagegevens kunt u direct Hallo bewerken */metadata/apiDefinition.swagger.json* -bestand in uw project en Hallo eigenschappen handmatig toevoegen.

Voor API-apps met dynamische metagegevens, kunt u Hallo SwaggerConfig.cs bestand tooadd een bewerking met het filter dat deze uitbreidingen kunt toevoegen.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Hallo Hier volgt een voorbeeld van hoe deze klasse geïmplementeerd toofacilitate Hallo dynamische metagegevens scenario kan zijn.

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
