---
title: uw Azure in Visual Studio code aaaOptimizing | Microsoft Docs
description: Meer informatie over hoe Azure code optimalisatie hulpprogramma's in Visual Studio zorgt u ervoor dat uw code krachtigere en meer.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Optimaliseren van uw Azure-Code
Wanneer u apps die gebruikmaken van Microsoft Azure programmeren, er zijn enkele codering procedures die u moet volgen toohelp voorkoming van problemen met app-schaalbaarheid, werking en prestaties in een cloudomgeving. Microsoft biedt een analyseprogramma Azure Code die wordt herkend en identificeert diverse van deze problemen meestal aangetroffen en kunt u deze kunt oplossen. Hallo-hulpprogramma in Visual Studio via NuGet, kunt u downloaden.

## <a name="azure-code-analysis-rules"></a>Azure Code Analysis-regels
Hello Azure Code analysehulpprogramma gebruikt Hallo volgens de regels voor tooautomatically vlag uw Azure code wanneer er bekende problemen met prestaties beïnvloeden. Gevonden problemen worden weergegeven als een waarschuwingen of compilatiefouten. Code correcties of suggesties tooresolve Hallo waarschuwingen of fouten zijn vaak door een gloeilampje voorzien.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Vermijd het gebruik van standaard (in-process) sessiestatusmodus gebruiken
### <a name="id"></a>Id
AP0000

### <a name="description"></a>Beschrijving
Als u Hallo standaard (in-process) sessiestatusmodus voor cloud-toepassingen gebruikt, kunt u de sessiestatus kunt verliezen.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Hallo sessiestatusmodus in Hallo web.config-bestand opgegeven is in-process standaard. Als er geen vermelding is opgegeven in configuratiebestand hello, standaard Hallo sessiestatus modus tooin-process. Hallo-in-process-modus wordt de sessiestatus opgeslagen in het geheugen op Hallo-webserver. Wanneer een exemplaar opnieuw is opgestart of een nieuw exemplaar wordt gebruikt voor de load balancer of failover-ondersteuning, wordt niet Hallo sessiestatus opgeslagen in het geheugen op de webserver Hallo opgeslagen. Deze situatie wordt voorkomen dat Hallo toepassing wordt schaalbare op Hallo cloud.

ASP.NET-sessiestatus ondersteunt verschillende verschillende opslagopties voor sessiestatusgegevens: InProc, StateServer, SQL Server, aangepast, en uitgeschakeld. Het verdient aanbeveling dat u aangepaste modus toohost gegevens op een externe sessiestatus-winkel, zoals [Azure Session State-provider voor Redis](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Oplossing
Een aanbevolen oplossing is de sessiestatus toostore op een beheerde cacheservice. Meer informatie over hoe toouse [Azure Session State-provider voor Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore de sessiestatus. U kunt ook de store-sessie aangeven in andere locaties tooensure uw toepassing schaalbare op Hallo cloud. meer informatie over alternatieve oplossingen Lees toolearn [sessie status modi](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>Voer methode mag geen asynchrone
### <a name="id"></a>Id
AP1000

### <a name="description"></a>Beschrijving
Maken van asynchrone methoden (zoals [await](https://msdn.microsoft.com/library/hh156528.aspx)) buiten Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode en vervolgens aanroep Hallo async-methoden van [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Hallo declareren [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode als asynchroon zorgt ervoor dat Hallo worker rol tooenter een lus opnieuw opstarten.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Het aanroepen van asynchrone methoden binnen Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode zorgt ervoor dat Hallo cloud service runtime toorecycle Hallo worker-rol. Wanneer een werkrol wordt gestart, alle programma-uitvoering plaatsvindt binnen Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode. Afgesloten Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode veroorzaakt Hallo worker rol toorestart. Wanneer Hallo worker-rol runtime Hallo async-methode raakt, verzendt alle bewerkingen na Hallo async-methode en vervolgens terugkeert. Dit zorgt ervoor dat Hallo worker rol tooexit van Hallo [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode en start deze opnieuw. In de volgende herhaling van de uitvoering van Hallo treffers in de werkrol Hallo Hallo async-methode opnieuw en opnieuw is opgestart, waardoor Hallo worker rol toorecycle ook opnieuw.

### <a name="solution"></a>Oplossing
Plaats alle asynchrone bewerkingen buiten Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode. Roep vervolgens Hallo geherstructureerd async-methode van binnen Hallo [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode, zoals RunAsync () .wait. Hello Azure Code analysehulpprogramma kunt u kunt dit probleem oplossen.

Hallo volgende codefragment wordt getoond hoe Hallo code oplossing voor dit probleem:

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Service Bus Shared Access Signature-verificatie gebruiken
### <a name="id"></a>Id
AP2000

### <a name="description"></a>Beschrijving
Shared Access Signature (SAS) gebruiken voor verificatie. Access Control Service (ACS) wordt voor service bus-verificatie afgeschaft.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Voor een betere beveiliging vervangt Azure Active Directory authentication ACS door de SAS-verificatie. Zie [Azure Active Directory is Hallo toekomstige van ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) voor informatie over het Hallo overgang plan.

### <a name="solution"></a>Oplossing
De SAS-verificatie gebruiken in uw apps. Hallo volgende voorbeeld ziet u hoe toouse een bestaande SAS-token tooaccess een service bus-naamruimte of entiteit.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Zie Hallo volgende onderwerpen voor meer informatie.

* Zie voor een overzicht [Shared Access Signature-verificatie met Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)
* [Hoe toouse Shared Access Signature-verificatie met Service Bus](https://msdn.microsoft.com/library/dn205161.aspx)
* Zie voor een voorbeeldproject [met behulp van Shared Access Signature (SAS)-verificatie met Service Bus-abonnementen](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>Overweeg het gebruik van OnMessage methode tooavoid 'ontvangen lus'
### <a name="id"></a>Id
AP2002

### <a name="description"></a>Beschrijving
bij een 'ontvangen lus,' tooavoid aanroepen Hallo **OnMessage** methode is een betere oplossing voor het ontvangen van berichten dan aanroepen Hallo **ontvangen** methode. Echter, als u Hallo gebruiken moet **ontvangen** methode en u geeft de wachttijd van een niet-standaard-server, controleert u Hallo server wachttijd is meer dan één minuut.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Bij het aanroepen van **OnMessage**, Hallo-client wordt gestart van een interne bericht pomp die voortdurend worden opgevraagd Hallo wachtrij of abonnement. Deze pomp bericht bevat een oneindige lus die problemen met een aanroep van tooreceive berichten. Als er is een time-out opgetreden bij het Hallo-aanroep, moet deze een nieuwe aanroep uitgeeft. Hallo-time-outinterval wordt bepaald door de waarde Hallo Hallo [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) eigenschap Hallo [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)die wordt gebruikt.

Hallo voordeel van **OnMessage** te vergeleken**ontvangen** is dat gebruikers geen toomanually poll-frequentie voor berichten hoeven, uitzonderingen, meerdere berichten tegelijkertijd verwerken en Hallo voltooien berichten.

Als u aanroept **ontvangen** zonder gebruik van de standaardwaarde worden ervoor Hallo *ServerWaitTime* waarde is meer dan één minuut. Instelling *ServerWaitTime* toomore dan één minuut voorkomt u dat Hallo server een time-out opgetreden voordat het Hallo-bericht volledig is ontvangen.

### <a name="solution"></a>Oplossing
Zie Hallo volgen voorbeelden van code voor het gebruik van aanbevolen. Zie voor meer informatie [QueueClient.OnMessage methode (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)en [QueueClient.Receive methode (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

tooimprove hello prestaties van hello Azure messaging-infrastructuur, Zie Hallo ontwerppatroon [asynchrone Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).

Hallo Hieronder volgt een voorbeeld van het gebruik van **OnMessage** tooreceive berichten.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

Hallo Hieronder volgt een voorbeeld van het gebruik van **ontvangen** met Hallo standaardserver wachttijd.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

Hallo Hieronder volgt een voorbeeld van het gebruik van **ontvangen** met een niet-standaard server wachttijd.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>Overweeg het gebruik van asynchrone Service Bus-methoden
### <a name="id"></a>Id
AP2003

### <a name="description"></a>Beschrijving
Gebruik asynchrone methoden tooimprove-prestaties van Service Bus brokered Messaging.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Met asynchrone methoden kunt toepassing programma gelijktijdigheid omdat elke aanroep uitvoeren Hallo hoofdthread niet blokkeert. Wanneer u Service Bus messaging-methoden, uitvoeren van een bewerking (verzenden, ontvangen, verwijderen, enz.) tijd in beslag neemt. Deze tijd bevat Hallo verwerking van Hallo bewerking door Hallo Service Bus-service in toevoeging toohello latentie van Hallo-aanvraag en Hallo-antwoorden. tooincrease hello aantal bewerkingen per keer, moeten bewerkingen tegelijkertijd uitvoeren. Voor meer informatie raadpleegt u te[aanbevolen procedures voor prestaties verbeteringen met behulp van Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Oplossing
Zie [QueueClient klasse (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) voor meer informatie over hoe toouse Hallo asynchrone methode aanbevolen.

tooimprove hello prestaties van hello Azure messaging-infrastructuur, Zie Hallo ontwerppatroon [asynchrone Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>U kunt partitionering Service Bus-wachtrijen en onderwerpen
### <a name="id"></a>Id
AP2004

### <a name="description"></a>Beschrijving
Partitie Service Bus-wachtrijen en onderwerpen voor betere prestaties bij het Service Bus-berichtenservice.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Service Bus-wachtrijen en onderwerpen partitioneren verhoogt de doorvoer en de service de beschikbaarheid van prestaties omdat hello totale doorvoer van een gepartitioneerde wachtrij of onderwerp is niet langer door Hallo-prestaties van een enkel bericht broker of berichten-store beperkt. Bovendien een tijdelijke onderbreking van berichten-store betekent niet dat een gepartitioneerde wachtrij of onderwerp niet beschikbaar. Zie voor meer informatie [Messaging Entities partitioneren](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Oplossing
Hallo code codefragment wordt getoond hoe na toopartition berichtentiteiten.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Zie voor meer informatie [gepartitioneerd Service Bus-wachtrijen en onderwerpen | Microsoft Azure-Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) en bekijk Hallo [Microsoft Azure Service Bus gepartitioneerd wachtrij](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) voorbeeld.

## <a name="do-not-set-sharedaccessstarttime"></a>Stel geen SharedAccessStartTime
### <a name="id"></a>Id
AP3001

### <a name="description"></a>Beschrijving
Vermijd het gebruik van SharedAccessStartTimeset toohello huidige tijd tooimmediately start Hallo beleid voor gedeelde toegang. U hoeft alleen tooset deze eigenschap als u wilt dat toostart Hallo gedeeld toegangsbeleid op een later tijdstip.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Synchronisatie van computerklok zorgt ervoor dat een lichte tijdsverschil tussen datacenters. U zou bijvoorbeeld logisch instelling Hallo-begintijd van een opslag-SAS-beleid zien als hello huidige tijd met behulp van DateTime.Now of een vergelijkbare manier Hallo SAS beleid tootake effect onmiddellijk zullen. Hallo lichte tijdsverschil tussen datacenters kunnen echter problemen met dit veroorzaken omdat een aantal keren datacenter mogelijk enigszins hoger is dan de begintijd hello, terwijl andere voor het. Als gevolg hiervan Hallo SAS-beleid kunt verloopt snel (of zelfs onmiddellijk) als Hallo beleid levensduur te kort is ingesteld.

Zie voor meer informatie over het gebruik van Shared Access Signature op Azure-opslag [introductie van tabel SAS (Shared Access Signature), wachtrij SAS en update tooBlob SAS - Team Blog van Microsoft Azure Storage - Site-MSDN-Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Oplossing
Hiermee stelt u de begintijd Hallo van Hallo gedeeld toegangsbeleid Hallo-instructie verwijderd. Hello Azure Code analysehulpprogramma biedt een oplossing voor dit probleem. Zie voor meer informatie over beveiligingsbeheer Hallo ontwerppatroon [Valet sleutel patroon](https://msdn.microsoft.com/library/dn568102.aspx).

Hallo volgende codefragment demonstreert Hallo code oplossing voor dit probleem.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>Gedeeld toegangsbeleid verlooptijdstip meer dan vijf minuten moet
### <a name="id"></a>Id
AP3002

### <a name="description"></a>Beschrijving
Er kunnen zich als een vijf minuten verschil in klokken tussen datacenters op verschillende locaties vanwege tooa staat bekend als "tijdsverschil." tooprevent hello SAS beleid-token verloopt ingesteld Hallo verstrijken tijd toobe eerder dan gepland, meer dan vijf minuten.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Datacenters op verschillende locaties Hallo wereld synchroniseren met een kloksignaal. Omdat het duurt voor klok signaal tootravel toodifferent locaties, kan er een verschil tijd tussen datacenters op verschillende geografische locaties Hoewel alles zogenaamd is gesynchroniseerd. Deze tijdsverschil kan invloed hebben op hello toegang tot gedeelde beleid start tijd en verlooptijd-interval. Daarom tooensure gedeeld toegangsbeleid wordt direct van kracht, is geen begintijd Hallo opgeeft. Zorg Daarnaast Hallo verlooptijd is meer dan 5 minuten tooprevent vroege time-out.

Zie voor meer informatie over het gebruik van Shared Access Signature op Azure-opslag [introductie van tabel SAS (Shared Access Signature), wachtrij SAS en update tooBlob SAS - Team Blog van Microsoft Azure Storage - Site-MSDN-Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Oplossing
Zie voor meer informatie over beveiligingsbeheer Hallo ontwerppatroon [Valet sleutel patroon](https://msdn.microsoft.com/library/dn568102.aspx).

Hallo Hier volgt een voorbeeld van een begintijd voor toegang tot gedeelde beleid niet op te geven.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Hallo Hieronder volgt een voorbeeld van het opgeven van een begintijd voor toegang tot gedeelde beleid met een duur van de beleid-vervaldatum langer dan vijf minuten.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Zie voor meer informatie [maken en gebruiken van een Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Gebruik CloudConfigurationManager
### <a name="id"></a>Id
AP4000

### <a name="description"></a>Beschrijving
Met behulp van Hallo [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) klasse voor projecten, zoals Azure-Website en Azure mobile services won't introduceren runtime-problemen. Als een best practice, het is echter een goed idee toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) uniforme wijze van het beheren van configuraties voor alle Azure-Cloud-toepassingen.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
CloudConfigurationManager leest Hallo configuratie bestand juiste toohello toepassing-omgeving.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Oplossing
Uw code toouse Hallo opsplitsen [klasse CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Een code-oplossing voor dit probleem wordt verstrekt door hello Azure Code analysehulpprogramma.

Hallo volgende codefragment demonstreert Hallo code oplossing voor dit probleem. Vervangen

`var settings = ConfigurationManager.AppSettings["mySettings"];`

met

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Hier volgt een voorbeeld van hoe toostore Hallo configuratie-instelling in een App.config- of Web.config-bestand. Hallo instellingen toohello appSettings sectie van het configuratiebestand Hallo toevoegen. Hallo volgt Hallo Web.config-bestand voor het vorige codevoorbeeld Hallo.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Vermijd het gebruik van vastgelegde verbindingsreeksen
### <a name="id"></a>Id
AP4001

### <a name="description"></a>Beschrijving
Als u gebruik verbindingsreeksen met vastgelegde en u tooupdate moet ze later kunt u toomake wijzigingen tooyour broncode hebben en Hallo toepassing opnieuw te compileren. Echter, als u de verbindingstekenreeksen in een configuratiebestand opslaat, u kunt ze later wijzigen door simpelweg bijwerken Hallo-configuratiebestand.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Hard-coding van verbindingsreeksen is een ongeldige procedure omdat hierdoor problemen wanneer verbindingsreeksen moeten toobe snel worden gewijzigd. Bovendien als Hallo project toobe toosource besturingselement ingecheckt moet, vastgelegde verbindingsreeksen leiden tot beveiligingsproblemen omdat Hallo tekenreeksen kunnen worden weergegeven in de broncode Hallo.

### <a name="solution"></a>Oplossing
Verbindingsreeksen opslaan in Hallo-configuratiebestanden of Azure-omgevingen.

* Gebruiken voor zelfstandige toepassingen, instellingen voor app.config toostore verbindingstekenreeks.
* Gebruik web.config toostore verbindingsreeksen voor IIS gehoste webtoepassingen.
* Gebruik voor ASP.NET-toepassingen vNext configuration.json toostore verbindingsreeksen.

Zie voor meer informatie over het gebruik van configuraties bestanden zoals web.config of app.config [ASP.NET Web configuratie-instructies](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Zie voor informatie over hoe Azure-omgeving variabelen werken, [Azure websites: tekenreeksen van toepassingen en verbinding tekenreeksen werken](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Zie voor meer informatie over het opslaan van de verbindingsreeks in broncodebeheer [te voorkomen dat gevoelige informatie zoals verbindingsreeksen in bestanden die zijn opgeslagen in de bron code opslagplaats](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).

## <a name="use-diagnostics-configuration-file"></a>Diagnostische gegevens configuratiebestand gebruiken
### <a name="id"></a>Id
AP5000

### <a name="description"></a>Beschrijving
In plaats van de diagnostische instellingen configureren in uw code zoals met behulp van Hallo Microsoft.WindowsAzure.Diagnostics programming API, moet u de diagnostische instellingen configureren in Hallo diagnostics.wadcfg-bestand. (Of diagnostics.wadcfgx als u gebruikmaakt van Azure SDK 2.5). Op deze manier kunt u instellingen voor diagnostische gegevens zonder toorecompile uw code.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Voordat u Azure SDK 2,5 (die gebruikmaakt van Azure diagnostics 1.3), Azure Diagnostics (af) kan worden geconfigureerd met behulp van verschillende methoden gebruiken: toe te voegen toohello configuratie blob in de opslag, via imperatieve code, declaratieve configuratie of Hallo-standaard de configuratie. Hallo voorkeur echter manier tooconfigure diagnostische gegevens is een XML-configuratiebestand (diagnostics.wadcfg of diagnositcs.wadcfgx voor SDK 2.5 en hoger) in het toepassingsproject Hallo toouse. In deze benadering kan Hallo diagnostics.wadcfg bestand volledig Hallo-configuratie is gedefinieerd en worden bijgewerkt en geïmplementeerd op wordt. Een combinatie van Hallo gebruik van Hallo diagnostics.wadcfg configuratiebestand Hello programmatische methoden voor het instellen van configuraties met behulp van Hallo [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)of [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) klassen kunnen tooconfusion leiden. Zie [initialiseren of Azure Diagnostics-configuratie wijzigen](https://msdn.microsoft.com/library/azure/hh411537.aspx) voor meer informatie.

Beginnend met af 1.3 (opgenomen in de Azure SDK 2.5), is niet meer mogelijk toouse code tooconfigure diagnostische gegevens. Als gevolg hiervan kunt u alleen Hallo configuratie tijdens het toepassen van of bijwerken van Hallo-extensie voor diagnostische gegevens opgeven.

### <a name="solution"></a>Oplossing
Gebruik Hallo diagnostics configuration designer toomove diagnostische instellingen toohello diagnostics configuratiebestand (diagnositcs.wadcfg of diagnositcs.wadcfgx voor SDK 2.5 en hoger). Ook wordt aanbevolen dat u installeert [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) en de meest recente diagnostics functie Hallo gebruiken.

1. Kies Eigenschappen in het snelmenu Hallo voor dat u wilt dat tooconfigure Hallo-rol, en kies vervolgens tabblad Hallo-configuratie.
2. In Hallo **Diagnostics** sectie, zorg ervoor dat Hallo **diagnostische gegevens inschakelen** selectievakje is ingeschakeld.
3. Kies Hallo **configureren** knop.

   ![Toegang tot de optie voor Hallo diagnostische gegevens inschakelen](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Zie [diagnostische gegevens configureren voor Azure Cloud Services en virtuele Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) voor meer informatie.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Vermijd DbContext-objecten als statische declareren
### <a name="id"></a>Id
AP6000

### <a name="description"></a>Beschrijving
toosave geheugen, DBContext-objecten als statische declareren voorkomen.

Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Reden
Objecten van de DBContext houdt Hallo queryresultaten vanuit elke aanroep. Statische DBContext-objecten zijn niet verwijderd totdat Hallo toepassingsdomein verwijderd is. Een statisch DBContext-object kan daarom grote hoeveelheden geheugen gebruiken.

### <a name="solution"></a>Oplossing
DBContext declareren als een lokale variabele of een van de niet-statisch exemplaarveld, gebruiken voor een taak en vervolgens laat u dit na gebruik worden verwijderd.

Hallo volgende voorbeeldklasse MVC-controller ziet u hoe toouse Hallo DBContext-object.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het optimaliseren van en probleemoplossing van apps van Azure, Zie [een web-app in Azure App Service met behulp van Visual Studio oplossen](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).
