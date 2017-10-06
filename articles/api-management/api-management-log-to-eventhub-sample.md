---
title: API's met Azure API Management, Event Hubs en Runscope aaaMonitor | Microsoft Docs
description: Voorbeeld van een toepassing demonstreren Hallo logboek-eventhub-beleid door het maken van verbinding Azure API Management, Azure Event Hubs en Runscope voor HTTP-logboekregistratie en controle
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>Uw API's met Azure API Management, Event Hubs en Runscope bewaken
Hallo [API Management-service](api-management-key-concepts.md) biedt veel mogelijkheden tooenhance Hallo verwerking van HTTP-aanvragen dat is verzonden tooyour HTTP-API. Hallo echter bestaan Hallo aanvragen en antwoorden zijn tijdelijke. Hallo-aanvraag wordt gedaan en wordt gebruikt door Hallo API Management-service tooyour end-API. Hallo-aanvraag wordt verwerkt door uw API en een antwoord terug via toohello API consumer loopt. Hallo API Management-service houdt een aantal belangrijke statistische gegevens over Hallo API's voor weergave in Hallo Publisher portaldashboard, maar naast, details Hallo zijn verdwenen.

Met behulp van Hallo [logboek voor eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [beleid](api-management-howto-policies.md) in Hallo API Management-service verzendt u details van de aanvraag en -antwoord tooan hello [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md). Er zijn diverse redenen waarom u kunt toogenerate gebeurtenissen van HTTP-berichten worden verzonden tooyour API's. Voorbeelden zijn audittrail van updates, gebruiksanalyse, uitzondering waarschuwingen en 3e integraties van derden.   

In dit artikel laat zien hoe toocapture Hallo gehele HTTP-aanvraag en antwoord-bericht verzenden tooan Event Hub en vervolgens relay-bericht tooa van derden service waarmee HTTP-logboekregistratie en controle van services.

## <a name="why-send-from-api-management-service"></a>Waarom verzenden van API Management-Service?
Het is mogelijk toowrite HTTP middleware waarmee kunt aansluiten op een HTTP-API frameworks toocapture HTTP-aanvragen en antwoorden en ze in logboekregistratie en controle van systemen feed. Hallo neerwaartse toothis aanpak is Hallo HTTP middleware moet toobe geïntegreerd in Hallo-end-API en platform Hallo Hallo API moet overeenkomen. Als er meerdere API's moet elk criterium Hallo middleware implementeren. Er zijn vaak redenen waarom de back-end voor API's kan niet worden bijgewerkt.

Met behulp van hello Azure API Management-service toointegrate met infrastructuur voor logboekregistratie biedt een gecentraliseerd en platformonafhankelijk-oplossing. Het is ook schaalbare gedeeltelijk vanwege toohello [geo-replicatie](api-management-howto-deploy-multi-region.md) mogelijkheden van Azure API Management.

## <a name="why-send-tooan-azure-event-hub"></a>Waarom Azure Event Hub tooan verzenden?
Het is een redelijke tooask, waarom maakt u een beleid dat specifiek tooAzure Event Hubs? Er zijn verschillende plaatsen waar mogelijk wil toolog mijn aanvragen. Waarom niet gewoon verzenden Hallo-aanvragen rechtstreeks toohello eindbestemming?  Dit is een optie. Wanneer u logboekregistratie van aanvragen van een API management-service, is het echter noodzakelijk tooconsider hoe berichtregistratie heeft invloed op prestaties Hallo Hallo API. Geleidelijke toename in belasting kunnen worden verwerkt door het verhogen van de beschikbare exemplaren van de onderdelen van het systeem of door gebruik te maken van geo-replicatie. Korte pieken in het verkeer kunnen echter leiden tot aanvragen toobe aanzienlijk vertraagd als aanvragen toologging infrastructuur tooslow belast wordt gestart.

Hello Azure Event Hubs is ontworpen tooingress grote hoeveelheden gegevens, met capaciteit voor het omgaan met een veel hoger aantal gebeurtenissen dan Hallo aantal HTTP-aanvragen proces voor de meeste API's. Hallo Event Hub fungeert als een soort geavanceerde buffer tussen uw API management-service en Hallo infrastructuur die wordt opgeslagen en Hallo-berichten verwerken. Dit zorgt ervoor dat de prestaties van uw API niet vanwege toohello logboekregistratie infrastructuur afnemen.  

Wanneer gegevens Hallo is verstreken tooan Event Hub worden bewaard en wordt gewacht op Event Hub consumenten tooprocess deze. Hallo Event Hub niets uit hoe deze worden verwerkt, het is net belangrijk ervoor te zorgen dat het Hallo-bericht met succes worden geleverd.     

Event Hubs hebben Hallo mogelijkheid toostream gebeurtenissen toomultiple consumer-groepen. Hiermee worden gebeurtenissen toobe verwerkt door andere systemen. Hierdoor kunnen veel integratiescenario's ondersteunen toevoeging vertragingen zonder op te plaatsen Hallo verwerken van de API-aanvraag Hallo binnen Hallo API Management-service wanneer slechts één gebeurtenis toobe gegenereerd moet.

## <a name="a-policy-toosend-applicationhttp-messages"></a>Een beleid toosend toepassing/HTTP-berichten
Een Event Hub accepteert gebeurtenisgegevens worden opgeslagen als een eenvoudige tekenreeks. Hallo-inhoud van de reeks zijn volledig tooyou. toobe kunnen toopackage-up maken van een HTTP-aanvraag en uit tooEvent Hubs tooformat Hallo tekenreeks met de aanvraag of antwoord informatie Hallo moet verzenden. In dit scenario, als er een bestaande opmaak die kan opnieuw worden gebruikt, vervolgens wordt mogelijk geen toowrite ons eigen bij het parseren van code. In eerste instantie als ik beschouwd met behulp van Hallo [HAR](http://www.softwareishard.com/blog/har-12-spec/) voor het verzenden van HTTP-aanvragen en antwoorden. Deze indeling is echter wel geoptimaliseerd voor het opslaan van een reeks van HTTP-aanvragen in een JSON op basis van indeling. Het bevat een aantal verplichte elementen die onnodige complexiteit voor Hallo scenario Hallo HTTP-bericht om door te geven via de kabel Hallo toegevoegd.  

Een alternatief is toouse hello `application/http` mediatype zoals beschreven in Hallo HTTP-specificatie [RFC 7230](http://tools.ietf.org/html/rfc7230). Dit mediatype gebruikt Hallo exact dezelfde notatie is gebruikte tooactually verzenden HTTP-berichten via de kabel hello, maar de volledige Hallo-bericht in de Hallo hoofdtekst van een andere HTTP-aanvraag kan worden geplaatst. In ons geval gaan NET we toouse Hallo instantie als onze bericht toosend tooEvent Hubs. Gemakkelijk, is er een parser dat voorkomt in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotheken die kunnen parseren deze indeling en deze converteren naar Hallo systeemeigen `HttpRequestMessage` en `HttpResponseMessage` objecten.

toobe kunnen toocreate dit bericht moeten we tootake profiteren van C# [beleidsexpressies](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management. Hier volgt Hallo-beleid waarmee een HTTP-aanvraag bericht tooAzure Event Hubs wordt verzonden.

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a>De declaratie van het beleid
Er enkele bepaalde zaken opgemerkt over dit beleidsexpressie. Hallo-logboek voor eventhub beleid heeft een kenmerk met de naam van logboek-id die verwijst toohello-naam van het logboek dat binnen Hallo API Management-service is gemaakt. meer informatie over hoe toosetup een Event Hub berichtenlogboek in Hallo API Management-service kan worden gevonden in Hallo document Hallo [hoe toolog gebeurtenissen tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md). Hallo tweede kenmerk is een optionele parameter zodat Event Hubs welke partitie toostore Hallo-bericht in. Event Hubs partities tooenable schaalbaarheid gebruiken en een minimum van twee vereisen. Hallo besteld aflevering van berichten is alleen binnen een partitie gegarandeerd. Als we Event Hub niet in welke partitie tooplace Hallo-bericht opdragen doen, wordt een round robin algoritme toodistribute Hallo belasting gebruikt. Echter, die mogelijk enkele van onze berichten toobe volgorde worden verwerkt.  

### <a name="partitions"></a>Partities
tooensure onze berichten worden tooconsumers op volgorde geleverd en te profiteren van Hallo load distributie mogelijkheid van partities, ik heb gekozen toosend HTTP-aanvraag berichten tooone en HTTP-antwoord berichten tooa tweede partitie. Dit zorgt ervoor dat een gelijkmatige verdeling en wij kunnen garanderen dat alle aanvragen worden gebruikt in volgorde en alle antwoorden in volgorde worden gebruikt. Het is mogelijk een antwoord toobe geconsumeerd voor het bijbehorende Hallo-aanvraag, maar omdat die niet is een probleem zoals we hebben een ander mechanisme voor het correleren tooresponses vraagt en we weten dat aanvragen altijd voordat antwoorden afkomstig zijn.

### <a name="http-payloads"></a>HTTP-nettoladingen
Na het bouwen van Hallo `requestLine` we toosee controleren als aanvraagtekst Hallo moet worden afgekapt. Hallo aanvraagtekst is afgekapt tooonly 1024. Dit kan worden verhoogd, afzonderlijke Event Hub berichten zijn echter beperkt too256KB, dus is het waarschijnlijk dat bepaalde HTTP-bericht wordt niet in een enkel bericht passen instanties. Bij het uitvoeren van logboekregistratie en analyse een aanzienlijke hoeveelheid gegevens kunnen worden afgeleid van NET Hallo HTTP-aanvraagregel en -koppen. Ook veel API-aanvragen alleen kleine instanties retourneren en dus Hallo verlies van informatie waarde door af te kappen grote organisaties is vrij minimale vergelijking toohello vermindering van overdracht, verwerking en opslag van kosten tookeep alle inhoud. Een definitieve opmerking over het verwerken van Hallo-instantie is moeten we toopass `true` toohello als<string>()-methode omdat we bij het lezen van de inhoud van hello, maar is ook wilt Hallo-end-API toobe kunnen tooread Hallo hoofdtekst. Door door te geven waar toothis methode hebben we Hallo hoofdtekst toobe gebufferd zodat deze een tweede keer kan worden gelezen. Dit is belangrijk toobe op de hoogte van hebt u een API die geen zeer grote bestanden worden geüpload of lange polling gebruikt. In deze gevallen zou worden aanbevolen tooavoid Hallo hoofdtekst helemaal lezen.   

### <a name="http-headers"></a>HTTP-headers
HTTP-Headers kunnen eenvoudig worden overgedragen via in Hallo berichtindeling in een eenvoudige sleutel/waarde-paar-indeling. We hebben ervoor gekozen toostrip uit bepaalde beveiligings-tijdgevoelige velden, tooavoid onnodig lekken referentie-informatie. Het lijkt onwaarschijnlijk dat API-sleutels en andere referenties zou worden gebruikt voor andere doeleinden analytics. Als we toodo analyse op Hallo gebruiker en Hallo bepaald product wilt ze gebruiken en we die kan verkrijgen van Hallo `context` object en toohello bericht toe te voegen.     

### <a name="message-metadata"></a>De metagegevens van het bericht
Wanneer u Hallo volledige bericht toosend toohello event hub, Hallo eerste regel is niet deel uit van Hallo `application/http` bericht. de eerste regel Hallo is aanvullende metagegevens die bestaan uit of het Hallo-bericht een aanvraag of antwoord-bericht is en een bericht-id die gebruikt toocorrelate is tooresponses aanvragen. Hallo-bericht-id is gemaakt met behulp van een ander beleid dat op dit lijkt:

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

Er kan Hallo-aanvraagbericht dat in een variabele tot Hallo antwoord is geretourneerd en vervolgens gewoon Hallo-aanvraag en -antwoord als een enkel bericht verzonden opgeslagen gemaakt. Hallo echter door Hallo-aanvraag en -antwoord onafhankelijk verzenden en het gebruik van een bericht-id toocorrelate twee, er iets meer flexibiliteit bij het Hallo-berichtgrootte, Hallo mogelijkheid tootake profiteren van meerdere partities ophalen terwijl de volgorde van berichten en Hallo behouden blijven aanvraag wordt weergegeven in het dashboard van onze logboekregistratie sneller. Ook kan er een aantal scenario's waarbij toohello event hub, mogelijk vanwege tooa aanvraag fatale fout in Hallo API Management-service, nooit door een geldig antwoord wordt verzonden, maar we kunnen je wordt nog een record van Hallo-aanvraag.

Hallo beleid toosend Hallo antwoord HTTP-bericht vergelijkbaar toohello aanvraag eruitziet en dus Hallo voltooien beleidsconfiguratie uitziet:

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

Hallo `set-variable` beleid maakt een waarde die toegankelijk is voor beide Hallo `log-to-eventhub` beleid in Hallo `<inbound>` sectie en Hallo `<outbound>` sectie.  

## <a name="receiving-events-from-event-hubs"></a>Ontvangen van gebeurtenissen van Event Hubs
Gebeurtenissen van Azure Event Hub worden ontvangen met Hallo [AMQP-protocol](http://www.amqp.org/). Hallo Microsoft Service Bus-team aangebracht client bibliotheken beschikbaar toomake Hallo gebeurtenissen gemakkelijker verbruikt. Er zijn twee verschillende benaderingen ondersteund, een wordt een *directe Consumer* , en andere Hallo Hallo `EventProcessorHost` klasse. Voorbeelden van deze twee methoden kunnen u vinden in Hallo [Event Hubs-programmeergids](../event-hubs/event-hubs-programming-guide.md). Hallo verkorte versie van Hallo verschillen is, `Direct Consumer` , hebt u volledige controle en Hallo `EventProcessorHost` biedt een aantal Loodgieterswerk Hallo voor u maar kunt u bepaalde veronderstellingen over hoe u deze gebeurtenissen worden verwerkt.  

### <a name="eventprocessorhost"></a>EventProcessorHost
In dit voorbeeld gebruiken we Hallo `EventProcessorHost` voor eenvoud, maar deze kan niet Hallo beste keuze voor dit scenario. `EventProcessorHost`Hallo harde werk waarbij wordt gecontroleerd of er geen tooworry over threading problemen binnen een bepaalde gebeurtenis processor-klasse. In ons scenario zijn er echter gewoon Hallo tooanother berichtindeling converteren en doorgeeft langs tooanother service met behulp van een async-methode. Er is niet nodig voor het bijwerken van de gedeelde status en daarom geen risico bestaat dat threading problemen. Voor de meeste scenario `EventProcessorHost` is waarschijnlijk de beste keuze Hallo en het is gewoon eenvoudiger Hallo-optie.     

### <a name="ieventprocessor"></a>IEventProcessor
Hallo centrale concept bij gebruik van `EventProcessorHost` toocreate is een een implementatie van Hallo `IEventProcessor` interface waarin Hallo methode `ProcessEventAsync`. Hallo essentie van deze methode wordt hier weergegeven:

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

Een lijst met EventData objecten worden doorgegeven aan de methode Hallo en we doorlopen die lijst. Hallo bytes van elke methode worden geparseerd naar een object HttpMessage en dat object tooan exemplaar van IHttpMessageProcessor wordt doorgegeven.

### <a name="httpmessage"></a>HttpMessage
Hallo `HttpMessage` -exemplaar bevat drie soorten gegevens:

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

Hallo `HttpMessage` -exemplaar bevat een `MessageId` GUID waarmee we tooconnect Hallo HTTP-aanvraag toohello bijbehorende HTTP-antwoord en een Booleaanse waarde die aangeeft of het Hallo-object bevat een exemplaar van een HttpRequestMessage en HttpResponseMessage. Met behulp van de ingebouwde HTTP-klassen uit Hallo `System.Net.Http`, ik tootake kunnen profiteren van Hallo is `application/http` bij het parseren van code die is opgenomen in `System.Net.Http.Formatting`.  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
Hallo `HttpMessage` exemplaar wordt vervolgens doorgestuurd tooimplementation van `IHttpMessageProcessor` die ik heb gemaakt toodecouple Hallo ontvangen en interpretatie van Hallo-gebeurtenis uit Azure Event Hub en Hallo daadwerkelijke verwerking van deze interface is.

## <a name="forwarding-hello-http-message"></a>Doorsturen Hallo HTTP-bericht
Voor dit voorbeeld ik besloten zou zijn interessante toopush Hallo HTTP-aanvraag via te[Runscope](http://www.runscope.com). Runscope is een service in de cloud die is gespecialiseerd in HTTP-foutopsporing, logboekregistratie en controle. Ze hebben een gratis laag, dus is het eenvoudig tootry en kunt u ons toosee Hallo HTTP-aanvragen in realtime stromend door onze API Management-service.

Hallo `IHttpMessageProcessor` implementatie uitziet,

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

Ik was tootake kunnen profiteren van een [bestaande-clientbibliotheek voor Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) kunt dan eenvoudig toopush `HttpRequestMessage` en `HttpResponseMessage` up bij hun service-exemplaren. In volgorde Hallo tooaccess Runscope API moet u een account en een API-sleutel. Instructies voor het ophalen van een API-sleutel kunnen worden gevonden in Hallo [toepassingen maken tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.

## <a name="complete-sample"></a>Compleet codevoorbeeld
Hallo [broncode](https://github.com/darrelmiller/ApimEventProcessor) en tests voor Hallo voorbeeld op GitHub. U moet een [API Management-Service](api-management-get-started.md), [een verbonden Event Hub](api-management-howto-log-event-hubs.md), en een [Opslagaccount](../storage/common/storage-create-storage-account.md) toorun Hallo voorbeeld voor uzelf.   

Hallo voorbeeld is alleen een eenvoudige consoletoepassing die luistert naar gebeurtenissen die afkomstig zijn van de Event Hub, converteert u deze in een `HttpRequestMessage` en `HttpResponseMessage` objecten en stuurt ze door op toohello Runscope API.

In Hallo animatie te volgen, ziet u een aanvraag wordt tooan API in Hallo Portal voor ontwikkelaars Hallo Console toepassing waarin Hallo-bericht wordt ontvangen, verwerkt en doorgestuurd en vervolgens Hallo aanvraag en -antwoord weergegeven in de Hallo Runscope verkeer Inspector.

![Demonstratie van de aanvraag doorgestuurd tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>Samenvatting
Azure API Management-service biedt een ideaal plaats toocapture Hallo HTTP-verkeer op reis tooand van uw API's. Azure Event Hubs is een zeer schaalbaar, voordelige oplossing voor het vastleggen van dat verkeer en die deze naar secundaire verwerkingssystemen voor logboekregistratie, bewaken en andere geavanceerde analyses. Verbinding maken met too3rd partij verkeer bewaken Runscope is een eenvoudige als een paar dozijn regels code.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Azure Event Hubs
  * [Aan de slag met Azure Event Hubs](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Berichten ontvangen met EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Programmeerhandleiding voor Event Hubs](../event-hubs/event-hubs-programming-guide.md)
* Meer informatie over de integratie van API Management en Event Hubs
  * [Hoe toolog gebeurtenissen tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md)
  * [Entiteitsverwijzing berichtenlogboek](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [documentatie voor logboek-eventhub-beleid](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
