---
title: procedures voor het verbeteren van de prestaties met Azure Service Bus aaaBest | Microsoft Docs
description: Beschrijft hoe Service Bus toooptimize prestaties bij het uitwisselen van toouse brokered berichten.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Aanbevolen procedures voor verbeterde prestaties met behulp van Service Bus-berichtenservice

Dit artikel wordt beschreven hoe toouse [Azure Service Bus-berichtenservice](https://azure.microsoft.com/services/service-bus/) toooptimize prestaties bij het uitwisselen van brokered berichten. Hallo eerste deel van dit onderwerp beschrijft Hallo verschillende mechanismen die de prestaties van toohelp worden aangeboden. het tweede gedeelte Hallo biedt richtlijnen voor hoe toouse Service Bus op een manier die de klant kunt aanbieden Hallo voor optimale prestaties in een bepaald scenario.

In dit onderwerp verwijst de term Hallo 'client' tooany entiteit die toegang heeft tot de Service Bus. Een client kan duren voordat Hallo-rol van een afzender of een ontvanger. Hallo term 'afzender' wordt gebruikt voor een Service Bus-wachtrij of onderwerp client die wordt verzonden berichten tooa Service Bus-wachtrij of onderwerp. Hallo term 'ontvanger' verwijst tooa Service Bus wachtrij of abonnement client die berichten van een Service Bus-wachtrij of abonnement ontvangt.

Deze secties vindt enkele concepten die Service Bus maakt gebruik van toohelp hogere prestaties.

## <a name="protocols"></a>Protocollen
Service Bus kunnen clients toosend en ontvang berichten via een van drie protocollen:

1. Geavanceerde Message Queuing-Protocol (AMQP)
2. Servicebus-berichtenservice Protocol (SBMP)
3. HTTP

AMQP en SBMP zijn efficiënter, omdat ze Hallo verbinding tooService Bus onderhouden zolang Hallo messagingfactory bestaat. Ook wordt batchverwerking en veelgevraagde geïmplementeerd. Tenzij expliciet wordt vermeld, is alle inhoud in dit onderwerp wordt ervan uitgegaan Hallo gebruik van AMQP of SBMP.

## <a name="reusing-factories-and-clients"></a>Hergebruik van de fabrieken en clients
Service Bus-clienttoepassing objecten, zoals [QueueClient] [ QueueClient] of [MessageSender][MessageSender], worden gemaakt via een [ MessagingFactory] [ MessagingFactory] -object, dat ook interne beheer van verbindingen biedt. U moet messaging fabrieken of wachtrij, onderwerp en Abonnementclients niet sluiten nadat u een bericht verzenden en opnieuw maken wanneer u het volgende Hallo-bericht verzenden. Sluiten van een messagingfactory verwijdert Hallo verbinding toohello Service Bus-service en een nieuwe verbinding tot stand is gebracht wanneer Hallo factory opnieuw te maken. Meerdere bewerkingen tot stand brengen van dat een verbinding is een dure bewerking die u kunt voorkomen door opnieuw Hallo dezelfde factory en client objecten. U kunt veilig Hallo [QueueClient] [ QueueClient] -object voor het verzenden van berichten van gelijktijdige asynchrone bewerkingen en meerdere threads. 

## <a name="concurrent-operations"></a>Gelijktijdige bewerkingen
Een bewerking (verzenden, ontvangen, verwijderen, enz.) neemt enige tijd in. Deze tijd bevat Hallo verwerking van Hallo bewerking door Hallo Service Bus-service in toevoeging toohello latentie van Hallo-aanvraag en Hallo-antwoorden. tooincrease hello aantal bewerkingen per keer, moeten bewerkingen tegelijkertijd uitvoeren. U kunt dit op verschillende manieren doen:

* **Asynchrone bewerkingen**: Hallo client plant u bewerkingen door het uitvoeren van asynchrone bewerkingen. de volgende aanvraag Hello wordt gestart voordat de vorige Hallo-aanvraag is voltooid. Hallo Hieronder volgt een voorbeeld van een verzendbewerking asynchroon:
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  Dit is een voorbeeld van een asynchrone bewerking ontvangen:
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **Meerdere fabrieken**: alle clients (afzenders in toevoeging tooreceivers) die zijn gemaakt door Hallo dezelfde factory share een TCP-verbinding. Hallo maximale doorvoer wordt beperkt door Hallo aantal bewerkingen dat deze TCP-verbinding kunt doorlopen. Hallo-doorvoer die kan worden verkregen met een enkele factory varieert aanzienlijk met TCP-inclusief de tijd en de grootte van het bericht. hogere doorvoersnelheden tooobtain, moet u meerdere messaging fabrieken gebruiken.

## <a name="receive-mode"></a>Modus ontvangen
Wanneer u een wachtrij of abonnement client maakt, kunt u een receive-modus: *Peek vergrendeling* of *ontvangt en verwijdert*. Hallo standaard modus ontvangen is [PeekLock][PeekLock]. Als het wordt uitgevoerd in deze modus, Hallo client verzendt een aanvraag tooreceive een bericht uit de Service Bus. Nadat het Hallo-client heeft het Hallo-bericht ontvangen, wordt een aanvraag toocomplete Hallo-bericht verzonden.

Hallo instellen wanneer modus te ontvangen[ReceiveAndDelete][ReceiveAndDelete], beide stappen worden gecombineerd in één aanvraag. Dit vermindert het totale aantal bewerkingen hello, en kunnen verbeteren Hallo totale doorvoer van het bericht. Deze prestatieverbetering wordt geleverd op Hallo risico van het verlies van berichten.

Service Bus biedt geen ondersteuning voor transacties voor ontvangen en delete-bewerkingen. Bovendien peek vergrendeling semantiek zijn vereist voor elk scenario's in welke Hallo client wil toodefer of [onbestelbare](service-bus-dead-letter-queues.md) een bericht.

## <a name="client-side-batching"></a>Batchverwerking aan de clientzijde
Batchverwerking aan de clientzijde, kunt een wachtrij of onderwerp client toodelay Hallo verzenden van een bericht voor een bepaalde periode. Als extra berichten Hallo client tijdens deze periode verzendt, verzendt het Hallo-berichten in één batch. Client-side batchverwerking ook zorgt ervoor dat een client wachtrij of abonnement toobatch meerdere **Complete** aanvragen in één aanvraag. Batchverwerking is alleen beschikbaar voor asynchrone **verzenden** en **Complete** bewerkingen. Synchrone bewerkingen worden onmiddellijk toohello Service Bus-service verzonden. Geen batchverwerking optreden voor peek of ontvangstbewerkingen, noch gebeurt batchverwerking over clients.

Een client gebruikt standaard een batch-interval van 20ms. U kunt hello batch-interval wijzigen door de instelling Hallo [BatchFlushInterval] [ BatchFlushInterval] eigenschap voordat u Hallo messagingfactory. Deze instelling geldt voor alle clients die zijn gemaakt door deze factory.

Hallo toodisable batches, stel [BatchFlushInterval] [ BatchFlushInterval] eigenschap te**TimeSpan.Zero**. Bijvoorbeeld:

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

Batchverwerking heeft geen invloed op Hallo aantal factureerbare messaging-bewerkingen, en is alleen beschikbaar voor Hallo clientprotocol Service Bus. Hallo HTTP-protocol biedt geen ondersteuning voor batchverwerking.

## <a name="batching-store-access"></a>Toegang tot store batchverwerking
tooincrease hello doorvoer van een wachtrij, onderwerp of abonnement, Servicebus batches meerdere berichten wanneer tooits interne store worden geschreven. Als ingeschakeld op een wachtrij of onderwerp, berichten schrijven naar Hallo archief wordt in batch worden opgenomen. Als ingeschakeld op een wachtrij of een abonnement, verwijderen van berichten uit de store hello wordt in batch worden opgenomen. Als toegang tot batch store is ingeschakeld voor een entiteit, Service Bus een schrijfbewerking voor een winkel met betrekking tot die entiteit door up too20ms vertraging. Aanvullende store bewerkingen die zich tijdens dit interval voordoen toegevoegd toohello batch. Batch verwerkt store toegang alleen van invloed op **verzenden** en **Complete** operations; ontvangen bewerkingen worden niet beïnvloed. Toegang tot batch store is een eigenschap van een entiteit. Batchverwerking vindt plaats via alle entiteiten waarmee toegang tot batch store.

Wanneer u een nieuwe wachtrij, onderwerp of abonnement maakt, wordt toegang tot batch store standaard ingeschakeld. toodisable batch verwerkt toegang tot store, set Hallo [EnableBatchedOperations] [ EnableBatchedOperations] eigenschap te**false** voordat het Hallo-entiteit maken. Bijvoorbeeld:

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

Toegang tot batch store heeft geen invloed op Hallo aantal factureerbare messaging-bewerkingen, en is een eigenschap van een wachtrij, onderwerp of abonnement. Het is onafhankelijk van Hallo modus en het Hallo-protocol dat wordt gebruikt tussen een client en het Hallo Service Bus-service ontvangen.

## <a name="prefetching"></a>Veelgevraagde
Veelgevraagde Hallo wachtrij of abonnement client tooload aanvullende berichten kan van Hallo-service tijdens het uitvoeren van een ontvangstbewerking. Hallo client slaat deze berichten in een lokale cache. Hallo-grootte van Hallo-cache wordt bepaald door Hallo [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] of [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] Eigenschappen. Elke client waarmee veelgevraagde onderhoudt een eigen cache. Een cache wordt niet gedeeld door clients. Als Hallo client een ontvangstbewerking initieert en de cache leeg is, verzendt Hallo-service een batch van berichten. Hallo-grootte van Hallo batch is gelijk aan Hallo grootte van het Hallo-cache of 256 KB, afhankelijk van wat kleiner is. Als Hallo client een ontvangstbewerking initieert en Hallo-cache een bericht bevat, wordt het Hallo-bericht opgehaald uit Hallo-cache.

Wanneer een bericht is tabelruimte, Hallo service vergrendelingen Hallo tabelruimte-bericht. Op deze manier kan niet tabelruimte Hallo-bericht worden ontvangen door een andere ontvanger. Als het Hallo-bericht Hallo ontvanger kan niet worden voltooid voordat Hallo vergrendeling verloopt, wordt het Hallo-bericht beschikbaar tooother ontvangers. Hallo tabelruimte kopie van het Hallo-bericht blijft in cache Hallo. Hallo ontvanger die Hallo verbruikt verlopen in de cache opgeslagen kopie een uitzondering ontvangen bij een poging toocomplete bericht. Standaard verloopt Hallo-bericht vergrendelen na 60 seconden. Deze waarde kan uitgebreide too5 minuten zijn. tooprevent hello verbruik van verlopen berichten, Hallo cachegrootte moet altijd kleiner zijn dan Hallo aantal berichten dat kan worden gebruikt door een client binnen de time-outinterval van Hallo-vergrendeling.

Wanneer u Hallo standaard vergrendeling vervaldatum van 60 seconden, een goede waarde voor [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] is 20 keer Hallo maximale verwerkingssnelheid weer van alle ontvangers van het Hallo-factory. Bijvoorbeeld, een factory maakt 3 ontvangers en elke ontvanger too10 berichten per seconde kan verwerken. Hallo prefetch aantal mag niet meer dan 20 X 3 X 10 = 600. Standaard [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] set too0, wat betekent dat er geen berichten meer worden opgehaald van Hallo-service is.

Veelgevraagde toeneemt Hallo totale doorvoer voor een wachtrij of een abonnement, omdat dit het totale aantal berichtbewerkingen of retouren Hallo verlaagt berichten. Ophalen van de eerste Hallo-bericht, maar duurt langer (vervaldatum toohello verhoogd berichtgrootte). Ontvangen van berichten tabelruimte worden sneller omdat deze berichten door de client Hallo al zijn gedownload.

Hallo time to live (TTL)-eigenschap van een bericht wordt gecontroleerd door Hallo-server op Hallo moment Hallo-server Hallo-bericht toohello client stuurt. Hallo-client controleert Hallo-bericht TTL-eigenschap niet wanneer het Hallo-bericht wordt ontvangen. Hallo-bericht kan in plaats daarvan worden ontvangen, zelfs als de TTL Hallo-bericht is verstreken terwijl het Hallo-bericht door Hallo-client in de cache is opgeslagen.

Veelgevraagde heeft geen invloed op Hallo aantal factureerbare messaging-bewerkingen, en is alleen beschikbaar voor Hallo clientprotocol Service Bus. Hallo HTTP-protocol biedt geen ondersteuning voor veelgevraagde. Veelgevraagde is beschikbaar voor synchrone en asynchrone bewerkingen ontvangen.

## <a name="express-queues-and-topics"></a>Wachtrijen en onderwerpen Express

Express-entiteiten hoge doorvoer en lagere latentie scenario's inschakelen en worden alleen ondersteund in Hallo standaardcategorie messaging. Entiteiten die zijn gemaakt [Premium-naamruimten](service-bus-premium-messaging.md) snelle Hallo-optie niet ondersteunen. Met de express-entiteiten als een bericht wordt verzonden tooa wachtrij of onderwerp is Hallo-bericht niet onmiddellijk in opgeslagen Hallo-berichten-store. In plaats daarvan wordt het tijdelijk opgeslagen in het geheugen. Als een bericht in de wachtrij Hallo meer dan een paar seconden blijft, wordt deze automatisch toostable opslag, dus te beveiligen tegen verlies vanwege tooan onderbreking geschreven. Schrijven van het Hallo-bericht in een geheugencache verhoogt de doorvoer en vermindert de latentie omdat er geen toostable toegang tot opslag op Hallo tijd Hallo-bericht verzonden. Berichten die worden gebruikt binnen een paar seconden worden toohello messaging store niet geschreven. Hallo volgende voorbeeld maakt een snelle onderwerp.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Als een bericht weergegeven met essentiële informatie die mag geen verloren wordt verzonden tooan snelle entiteit, Hallo afzender Service Bus kunt afdwingen tooimmediately leggen Hallo-bericht toostable opslag instellen Hallo [ForcePersistence] [ ForcePersistence] eigenschap te**true**.

> [!NOTE]
> Express-entiteiten bieden geen ondersteuning voor transacties.

## <a name="use-of-partitioned-queues-or-topics"></a>Gebruik van gepartitioneerde wachtrijen en onderwerpen
Intern maakt gebruik van Service Bus Hallo hetzelfde knooppunt en messaging store tooprocess en alle berichten voor een Berichtentiteit (wachtrij of onderwerp) op te slaan. Een gepartitioneerde wachtrij of onderwerp op Hallo daarentegen is verdeeld over meerdere knooppunten en berichten-stores. Gepartitioneerde wachtrijen en onderwerpen niet alleen resulteert in een hogere doorvoer dan reguliere wachtrijen en onderwerpen, ze hogere beschikbaarheid vertonen. toocreate een gepartitioneerde entiteit set Hallo [EnablePartitioning] [ EnablePartitioning] eigenschap te**true**, zoals weergegeven in het volgende voorbeeld Hallo. Zie voor meer informatie over gepartitioneerde entiteiten [gepartitioneerde berichtentiteiten][Partitioned messaging entities].

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>Gebruik van meerdere wachtrijen

Als het niet mogelijk toouse die een gepartitioneerde wachtrij of onderwerp of Hallo verwacht belasting kan niet worden afgehandeld door een enkele gepartitioneerde wachtrij of onderwerp, moet u meerdere messaging-entiteiten. Wanneer u meerdere entiteiten, een specifieke client voor elke entiteit maken, in plaats van dezelfde Hallo-client voor alle entiteiten.

## <a name="development-and-testing-features"></a>Ontwikkeling en tests functies

Service Bus is een functie die wordt gebruikt voor het ontwikkeling die **mag nooit worden gebruikt in productie configuraties**: [TopicDescription.EnableFilteringMessagesBeforePublishing][].

Wanneer u filters of nieuwe regels toegevoegd toohello onderwerp, kunt u [TopicDescription.EnableFilteringMessagesBeforePublishing][] tooverify die nieuwe filterexpressie Hallo werkt zoals verwacht.

## <a name="scenarios"></a>Scenario's
Hallo volgende secties beschrijven typische berichtverzending en overzicht Hallo voorkeur Service Bus-instellingen. Doorvoersnelheid (minder dan 1 bericht/seconde) zo klein zijn geclassificeerd, Gemiddeld (bericht per seconde van 1 of groter maar minder dan 100 berichten/seconde) en een hoge (100 berichten/seconde of hoger). Hallo zijn aantal clients geclassificeerd als kleine (5 of minder), Gemiddeld (meer dan 5 maar kleiner dan of gelijk zijn too20), en grote (meer dan 20).

### <a name="high-throughput-queue"></a>Hoge gegevensdoorvoer wachtrij
Doel: Maximaliseren Hallo doorvoer van een enkele wachtrij. Hallo aantal afzenders en ontvangers is klein.

* Een gepartitioneerde wachtrij gebruiken voor betere prestaties en beschikbaarheid.
* tooincrease Hallo algehele verzendsnelheid in wachtrij hello, meerdere fabrieken toocreate berichtverzenders gebruiken. Gebruik voor elke afzender asynchrone bewerkingen of meerdere threads.
* tooincrease hello algehele ontvangstsnelheid uit de wachtrij hello, gebruikt u meerdere bericht fabrieken toocreate ontvangers.
* Asynchrone bewerkingen tootake profiteren van de client-side batchverwerking gebruiken.
* Hallo too50ms tooreduce Hallo Intervalnummer van Service Bus-client protocol verzendingen batchverwerking ingesteld. Als u meerdere afzenders gebruikt, vergroot u Hallo interval too100ms batchverwerking.
* Toegang tot batch store ingeschakeld laten. Dit verhoogt de algehele Hallo frequentie waarmee berichten in wachtrij Hallo kunnen worden geschreven.
* Hallo prefetch aantal too20 tijdstippen Hallo maximale verwerkingssnelheden van alle ontvangers van een fabriek instellen. Dit vermindert het aantal gegevensoverdrachten van Service Bus-client protocol Hallo.

### <a name="multiple-high-throughput-queues"></a>Meerdere hoge gegevensdoorvoer wachtrijen
Doel: Het maximaliseren totale doorvoer van meerdere wachtrijen. Hallo-doorvoer van een afzonderlijke wachtrij is Gemiddeld of hoog.

de maximale doorvoer tooobtain via meerdere wachtrijen, Hallo-instellingen gebruiken die worden beschreven toomaximize Hallo doorvoer van een enkele wachtrij. Bovendien kunt u verschillende fabrieken toocreate clients die verzenden of ontvangen van andere wachtrijen.

### <a name="low-latency-queue"></a>Lage latentie wachtrij
Doel: Latentie van de end-to-end van een wachtrij of onderwerp minimaliseren. Hallo aantal afzenders en ontvangers is klein. Hallo-doorvoer van Hallo wachtrij is klein of Gemiddeld.

* Een gepartitioneerde wachtrij gebruiken voor verbeterde beschikbaarheid.
* Batchverwerking aan de clientzijde niet uitschakelen. Hallo-client onmiddellijk een bericht.
* Batch store toegang uitschakelen. Hallo service schrijft onmiddellijk Hallo toohello berichtenopslag.
* Als een enkele client, stelt u Hallo prefetch aantal too20 keren Hallo verwerkingssnelheid van Hallo ontvanger. Als meerdere in wachtrij op Hallo Hallo dezelfde berichten tijd, Hallo clientprotocol Service Bus verzendt deze alles op Hallo hetzelfde moment. Wanneer Hallo client volgende Hallo-bericht ontvangt, is dat bericht al in de lokale cache Hallo. Hallo-cache moet klein zijn.
* Als meerdere clients, stelt u Hallo prefetch aantal too0. Op deze manier kan Hallo tweede client tijdens de eerste client Hallo eerst het Hallo-bericht steeds verwerkt nog tweede Hallo-bericht ontvangen.

### <a name="queue-with-a-large-number-of-senders"></a>Wachtrij met een groot aantal afzenders
Doel: Het maximaliseren van doorvoer van een wachtrij of onderwerp met een groot aantal afzenders. Elke afzender verzendt berichten met een gemiddeld tarief. het aantal ontvangers Hallo is klein.

Service Bus kunt up too1000 gelijktijdige verbindingen tooa messaging entiteit (of 5000 met AMQP). Deze limiet wordt afgedwongen op het niveau van de naamruimte Hallo en onderwerpen-wachtrijen-abonnementen worden beperkt door het Hallo-limiet van gelijktijdige verbindingen per naamruimte. Voor wachtrijen, wordt dit nummer gedeeld tussen afzenders en ontvangers. Als alle 1000 verbindingen vereist voor afzenders zijn, moet u Hallo wachtrij vervangen door een onderwerp met één abonnement. Een onderwerp accepteert too1000 gelijktijdige verbindingen van afzenders, terwijl het Hallo-abonnement een extra 1000 gelijktijdige verbindingen aanvaardt van ontvangers. Als meer dan 1000 gelijktijdige afzenders vereist zijn, moeten Hallo afzenders berichten toohello Service Bus-protocol via HTTP worden verzonden.

toomaximize doorvoer, Hallo te volgen:

* Een gepartitioneerde wachtrij gebruiken voor betere prestaties en beschikbaarheid.
* Als u elke afzender bevindt zich in een ander proces, gebruikt u dezelfde fabriek per proces.
* Asynchrone bewerkingen tootake profiteren van de client-side batchverwerking gebruiken.
* Hallo standaardwaarde batchverwerking interval van 20ms tooreduce Hallo aantal gegevensoverdrachten van Service Bus-client-protocol gebruiken.
* Toegang tot batch store ingeschakeld laten. Dit verhoogt de algehele Hallo frequentie waarmee berichten kunnen worden geschreven in Hallo wachtrij of onderwerp.
* Hallo prefetch aantal too20 tijdstippen Hallo maximale verwerkingssnelheden van alle ontvangers van een fabriek instellen. Dit vermindert het aantal gegevensoverdrachten van Service Bus-client protocol Hallo.

### <a name="queue-with-a-large-number-of-receivers"></a>Wachtrij met een groot aantal ontvangers
Doel: Maximaliseren Hallo ontvangstsnelheid van een wachtrij of een abonnement met een groot aantal ontvangers. Elke ontvanger ontvangt berichten met een gemiddeld snelheid. het aantal afzenders Hallo is klein.

Service Bus kunt up too1000 gelijktijdige verbindingen tooan entiteit. Als een wachtrij meer dan 1000 ontvangers vereist, moet u Hallo wachtrij vervangen door een onderwerp met meerdere abonnementen. Elk abonnement kan too1000 gelijktijdige verbindingen ondersteunen. U kunt ook ontvangers hebben toegang tot Hallo wachtrij via Hallo HTTP-protocol.

toomaximize doorvoer, Hallo te volgen:

* Een gepartitioneerde wachtrij gebruiken voor betere prestaties en beschikbaarheid.
* Als u elke ontvanger zich bevindt in een ander proces, gebruikt u dezelfde fabriek per proces.
* Ontvangers kunnen synchrone of asynchrone bewerkingen gebruiken. Gegeven Hallo matig ontvangstsnelheid van een afzonderlijke ontvanger, client-side batchverwerking van een volledige aanvraag heeft geen invloed op ontvanger doorvoer.
* Toegang tot batch store ingeschakeld laten. Dit vermindert Hallo algehele belasting van Hallo entiteit. Vermindert ook Hallo snelheid waarmee berichten kunnen worden geschreven in Hallo wachtrij of onderwerp.
* Hallo prefetch aantal tooa kleine waarde ingesteld (bijvoorbeeld PrefetchCount = 10). Dit voorkomt dat ontvangers inactiviteit terwijl andere ontvangers grote aantallen berichten in de cache opgeslagen hebben.

### <a name="topic-with-a-small-number-of-subscriptions"></a>Onderwerp met een klein aantal abonnementen
Doel: Maximaliseren Hallo doorvoer van een onderwerp met een klein aantal abonnementen. Een bericht wordt ontvangen door veel abonnementen, wat betekent dat Hallo gecombineerd ontvangen snelheid via alle abonnementen is groter dan de verzendsnelheid Hallo. het aantal afzenders Hallo is klein. het aantal ontvangers per abonnement Hallo is klein.

toomaximize doorvoer, Hallo te volgen:

* Gebruik een gepartitioneerde onderwerp voor betere prestaties en beschikbaarheid.
* tooincrease hello algehele verzendsnelheid in Hallo onderwerp, gebruikt u meerdere fabrieken toocreate berichtverzenders. Gebruik voor elke afzender asynchrone bewerkingen of meerdere threads.
* tooincrease hello algehele ontvangstsnelheid van een abonnement, gebruikt u meerdere bericht fabrieken toocreate ontvangers. Gebruik voor elke ontvanger asynchrone bewerkingen of meerdere threads.
* Asynchrone bewerkingen tootake profiteren van de client-side batchverwerking gebruiken.
* Hallo standaardwaarde batchverwerking interval van 20ms tooreduce Hallo aantal gegevensoverdrachten van Service Bus-client-protocol gebruiken.
* Toegang tot batch store ingeschakeld laten. Dit verhoogt de algehele Hallo frequentie waarmee berichten kunnen worden geschreven in Hallo onderwerp.
* Hallo prefetch aantal too20 tijdstippen Hallo maximale verwerkingssnelheden van alle ontvangers van een fabriek instellen. Dit vermindert het aantal gegevensoverdrachten van Service Bus-client protocol Hallo.

### <a name="topic-with-a-large-number-of-subscriptions"></a>Onderwerp met een groot aantal abonnementen
Doel: Maximaliseren Hallo doorvoer van een onderwerp met een groot aantal abonnementen. Een bericht wordt ontvangen door veel abonnementen, wat betekent dat Hallo gecombineerd ontvangen snelheid via alle abonnementen is aanzienlijk groter dan de verzendsnelheid Hallo. het aantal afzenders Hallo is klein. het aantal ontvangers per abonnement Hallo is klein.

Onderwerpen met een groot aantal abonnementen wordt doorgaans een lage totale doorvoer blootstellen als er geen alle berichten worden gerouteerd tooall abonnementen zijn. Dit wordt veroorzaakt door Hallo feit dat elk bericht vaak ontvangen wordt en alle berichten die zijn opgenomen in een onderwerp en alle bijbehorende abonnementen worden opgeslagen in Hallo dezelfde opslaan. Ervan wordt uitgegaan dat Hallo aantal afzenders en ontvangers per abonnement aantal klein is. Service Bus biedt ondersteuning voor maximaal too2, 000 abonnementen per onderwerp.

toomaximize doorvoer, Hallo te volgen:

* Gebruik een gepartitioneerde onderwerp voor betere prestaties en beschikbaarheid.
* Asynchrone bewerkingen tootake profiteren van de client-side batchverwerking gebruiken.
* Hallo standaardwaarde batchverwerking interval van 20ms tooreduce Hallo aantal gegevensoverdrachten van Service Bus-client-protocol gebruiken.
* Toegang tot batch store ingeschakeld laten. Dit verhoogt de algehele Hallo frequentie waarmee berichten kunnen worden geschreven in Hallo onderwerp.
* Stel Hallo prefetch aantal too20 keer verwacht Hallo ontvangen frequentie in seconden. Dit vermindert het aantal gegevensoverdrachten van Service Bus-client protocol Hallo.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het optimaliseren van de prestaties van Service Bus, Zie [gepartitioneerde berichtentiteiten][Partitioned messaging entities].

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
