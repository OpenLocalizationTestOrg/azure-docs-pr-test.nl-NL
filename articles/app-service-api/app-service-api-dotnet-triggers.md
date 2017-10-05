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
# <a name="azure-app-service-api-app-triggers"></a>API-app-triggers voor Azure App Service
> [!NOTE]
> Deze versie van het artikel is van toepassing op API apps-2014-12-01-preview-schemaversie.
>
>

## <a name="overview"></a>Overzicht
In dit artikel wordt uitgelegd hoe API app-triggers implementeren en gebruiken van een logische app.

Alle van de codefragmenten in dit onderwerp worden gekopieerd van de [FileWatcher API-App-codevoorbeeld](http://go.microsoft.com/fwlink/?LinkId=534802).

Merk op dat u wilt downloaden van de volgende nuget-pakket voor de code in dit artikel om te bouwen en uitvoeren: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>Wat API app-triggers zijn?
Het is een veelvoorkomend scenario voor een API-app zodat clients van de API-app de juiste actie in reactie op de gebeurtenis ondernemen kunnen een gebeurtenis wordt gestart. Het mechanisme voor op basis van REST-API die ondersteuning biedt voor dit scenario wordt een API-app-trigger genoemd.

Bijvoorbeeld, Stel dat uw clientcode maakt gebruik van de [Twitter-Connector-API-app](../connectors/connectors-create-api-twitter.md) en uw code nodig zijn voor een actie die op basis van nieuwe tweets die bepaalde woorden bevatten. U mogelijk in dit geval een poll of push trigger instellen om deze behoefte.

## <a name="poll-trigger-versus-push-trigger"></a>Poll-trigger versus push-signaal
Op dit moment kunnen worden twee soorten triggers ondersteund:

* Poll-trigger - Client controleert de API-app voor melding van een gebeurtenis die is verwijderd
* Push-signaal - Client wordt door de API-app geïnformeerd wanneer een gebeurtenis wordt gestart

### <a name="poll-trigger"></a>Poll-trigger
Een poll-trigger is geïmplementeerd als een reguliere REST-API en poll-om op te halen van de melding wordt verwacht dat de clients (zoals een logische app). Terwijl de client de status behouden kan, is de poll-trigger zelf staatloze.

De volgende gegevens over de aanvraag en antwoord pakketten illustratie van enkele belangrijke aspecten van het contract van de trigger poll:

* Aanvraag
  * HTTP-methode: ophalen
  * Parameters
    * triggerState - deze optionele parameter kan clients opgeven dat hun status, zodat de poll-trigger goed beslissen om terug te keren melding of niet op basis van de opgegeven status.
    * API-specifieke parameters
* Antwoord
  * Statuscode **200** - aanvraag geldig is en er is een melding van de trigger. De inhoud van de melding worden de antwoordtekst. Een header 'Opnieuw proberen na' in het antwoord geeft aan dat er aanvullende kennisgeving gegevens met een aanroep van de volgende aanvraag moet worden opgehaald.
  * Statuscode **202** - aanvraag is geldig, maar er is geen nieuwe melding van de trigger.
  * Statuscode **4xx** -aanvraag is niet geldig. De client moet de aanvraag niet opnieuw proberen.
  * Statuscode **5xx** -aanvraag heeft geleid tot een interne serverfout en/of een tijdelijk probleem. De client moet de aanvraag opnieuw te proberen.

Het volgende codefragment is een voorbeeld van het implementeren van een poll-trigger.

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

Als u wilt testen deze trigger poll, de volgende stappen uit:

1. Implementeer de API-App met een verificatie-instelling van **openbare anonieme**.
2. Roep de **touch** bewerking touch van een bestand. De volgende afbeelding toont een voorbeeld van een aanvraag via Postman.
   ![Touch-bewerking via Postman aanroepen](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Roep de poll-trigger met de **triggerState** parameter ingesteld op een tijdstempel vóór stap 2. De volgende afbeelding toont de voorbeeld-aanvraag via Postman.
   ![Poll-Trigger via Postman aanroepen](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Push-signaal
Een push-signaal is geïmplementeerd als een reguliere REST-API die meldingen verstuurd naar clients die zich hebben geregistreerd wilt worden gewaarschuwd als specifieke gebeurtenissen worden gestart.

De volgende gegevens over de aanvraag en antwoord pakketten illustratie van enkele belangrijke aspecten van de push-trigger-contract.

* Aanvraag
  * HTTP-methode: plaatsen
  * Parameters
    * triggerId: vereist - ondoorzichtige tekenreeks (zoals een GUID) voor de registratie van een push-trigger.
    * callbackUrl: vereist - URL van de callback moet worden aangeroepen wanneer de gebeurtenis wordt gestart. De aanroep is een eenvoudige HTTP POST-aanroep.
    * API-specifieke parameters
* Antwoord
  * Statuscode **200** -aanvraag voor het registreren van de client is geslaagd.
  * Statuscode **4xx** -aanvraag is niet geldig. De client moet de aanvraag niet opnieuw proberen.
  * Statuscode **5xx** -aanvraag heeft geleid tot een interne serverfout en/of een tijdelijk probleem. De client moet de aanvraag opnieuw te proberen.
* Terugbellen
  * HTTP-methode: POST
  * Aanvraagtekst: berichtinhoud.

Het volgende codefragment is een voorbeeld van het implementeren van een push-signaal:

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

Als u wilt testen deze trigger poll, de volgende stappen uit:

1. Implementeer de API-App met een verificatie-instelling van **openbare anonieme**.
2. Blader naar [http://requestb.in/](http://requestb.in/) voor het maken van een RequestBin die als de URL van uw retouraanroep fungeert.
3. Aanroepen van de push-trigger met een GUID als **triggerId** en de URL RequestBin als **callbackUrl**.
   ![Push-signaal via Postman aanroepen](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Roep de **touch** bewerking touch van een bestand. De volgende afbeelding toont een voorbeeld van een aanvraag via Postman.
   ![Touch-bewerking via Postman aanroepen](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Controleer de RequestBin om te bevestigen dat de callback van de trigger push is aangeroepen met de eigenschap uitvoer.
   ![Poll-Trigger via Postman aanroepen](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Beschrijven triggers in API-definitie
Nadat de triggers implementeren en uw API-app implementeren naar Azure, gaat u naar de **API-definitie** blade in de Azure preview-portal en u ziet triggers worden automatisch herkend in de gebruikersinterface wordt aangedreven door de Swagger 2.0 API-definitie van de API-app.

![API-definitie-Blade](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Als u op de **downloaden Swagger** knop en opent u het JSON-bestand, ziet u resultaten die vergelijkbaar is met het volgende:

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

De eigenschap extension **x-ms-schedular-trigger** is hoe triggers worden beschreven in de API-definitie en automatisch door de API-app-gateway wordt toegevoegd wanneer u via de gateway van de API-definitie aanvragen als de aanvraag voor een van de de volgende criteria. (U kunt ook deze eigenschap handmatig toevoegen.)

* Poll-trigger
  * Als de HTTP-methode is **ophalen**.
  * Als de **operationId** eigenschap bevat de tekenreeks **trigger**.
  * Als de **parameters** eigenschap bevat een parameter met een **naam** eigenschap ingesteld op **triggerState**.
* Push-signaal
  * Als de HTTP-methode is **plaatsen**.
  * Als de **operationId** eigenschap bevat de tekenreeks **trigger**.
  * Als de **parameters** eigenschap bevat een parameter met een **naam** eigenschap ingesteld op **triggerId**.

## <a name="use-api-app-triggers-in-logic-apps"></a>API app-triggers gebruiken in Logic apps
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a>Weergeven en configureren van app-triggers voor API in de ontwerpfunctie voor Logic apps
Als u een logische app in dezelfde resourcegroep bevinden als de API-app maakt, kunt u zich kunt toevoegen aan het designer-canvas gewoon door erop te klikken. De volgende afbeeldingen illustreren dit:

![Triggers in Logic App-ontwerper](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Poll-Trigger in Logic App-ontwerper configureren](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Push-signaal in Logic App-ontwerper configureren](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>API-app-triggers voor Logic apps optimaliseren
Nadat u triggers aan een API-app toevoegt, zijn er enkele dingen die u doen kunt om de ervaring te verbeteren wanneer u de API-app in een logische app.

Bijvoorbeeld, de **triggerState** parameter voor de poll-triggers moet worden ingesteld op de volgende expressie in de logische app. Deze expressie moet de laatste aanroep van de trigger van de logische app evalueren en die waarde retourneren.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Opmerking: Voor een uitleg van de functies die in de bovenstaande expressie worden gebruikt, Raadpleeg de documentatie op [Logic App werkstroom Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Logic app-gebruikers moeten de expressie hierboven voor de **triggerState** parameter tijdens het gebruik van de trigger. Het is mogelijk dat deze waarde vooraf ingesteld door de ontwerper Logic app via de eigenschap extension **x-ms-scheduler-aanbeveling**.  De **x-ms-zichtbaarheid** uitbreidingseigenschap kan worden ingesteld op een waarde van *interne* zodat de parameter zelf niet in de ontwerpfunctie wordt weergegeven.  Het volgende fragment illustreert die.

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

Voor de push-triggers de **triggerId** parameter moet een unieke identificatie van de logische app. Aanbevolen wordt deze eigenschap instellen op de naam van de werkstroom met behulp van de volgende expressie:

    @workflow().name

Met behulp van de **x-ms-scheduler-aanbeveling** en **x-ms-zichtbaarheid** eigenschappen van de extensie in de API-definitie, de API-app kunt overbrengen naar de ontwerpfunctie Logic app worden automatisch ingesteld deze expressie voor de de gebruiker.

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
Informatie over aanvullende metagegevens - zoals de uitbreidingseigenschappen **x-ms-scheduler-aanbeveling** en **x-ms-zichtbaarheid** -kunnen worden toegevoegd in de API-definition op twee manieren: statisch of dynamisch.

Voor statische metagegevens kunt u direct bewerken de */metadata/apiDefinition.swagger.json* -bestand in uw project en de eigenschappen handmatig toevoegen.

Voor API-apps met dynamische metagegevens, kunt u het bestand SwaggerConfig.cs voor het toevoegen van een bewerking met het filter dat deze uitbreidingen kunt toevoegen.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Hier volgt een voorbeeld van hoe deze klasse kan worden geïmplementeerd om te vergemakkelijken van het scenario dynamisch metagegevens.

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
