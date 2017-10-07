---
title: aaaAzure opslagwachtrijen en Service Bus-wachtrijen - vergeleken en tegenstelling tot | Microsoft Docs
description: Analyseert verschillen en overeenkomsten tussen de twee typen wachtrijen die door Azure worden aangeboden.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>Opslagwachtrijen en Service Bus-wachtrijen - vergeleken en tegenstelling tot
In dit artikel analyseert Hallo verschillen en overeenkomsten tussen Hallo twee soorten wachtrijen die tegenwoordig worden aangeboden door Microsoft Azure: opslagwachtrijen en Service Bus-wachtrijen. Met behulp van deze informatie kunt u vergelijken en contrast Hallo respectieve technologieën en worden kunnen toomake een meer gefundeerde beslissing over welke oplossing het beste aan uw behoeften voldoet.

## <a name="introduction"></a>Inleiding
Azure ondersteunt twee soorten wachtrij mechanismen: **opslagwachtrijen** en **Service Bus-wachtrijen**.

**Opslagwachtrijen**, die deel uitmaken van Hallo [Azure storage](https://azure.microsoft.com/services/storage/) infrastructuur, functie een eenvoudige interface van de REST gebaseerde GET/PUT/PEEK biedt betrouwbare, permanente messaging binnen en tussen services.

**Service Bus-wachtrijen** deel uitmaken van een breder [Azure messaging](https://azure.microsoft.com/services/service-bus/) infrastructuur die ondersteuning biedt voor queuing evenals publiceren/abonneren en meer geavanceerde integratie patronen. Zie voor meer informatie over Service Bus-onderwerpen-wachtrijen/abonnementen Hallo [overzicht van Service Bus](service-bus-messaging-overview.md).

Hoewel beide queuing technologieën gelijktijdig bestaan, kennisgemaakt opslagwachtrijen eerst als een toegewezen wachtrij opslagmechanisme gebouwd op Azure Storage-services. Service Bus-wachtrijen zijn gebouwd op Hallo breder 'messaging' infrastructuur ontworpen toointegrate toepassingen of de onderdelen van de toepassing die meerdere communicatieprotocollen, gegevenscontracten, vertrouwen domeinen en/of netwerkomgevingen kunnen omvatten.

## <a name="technology-selection-considerations"></a>Overwegingen voor selectie van technologie
Zijn de implementaties van Hallo message Queuing-service dat momenteel wordt aangeboden op Microsoft Azure Storage-wachtrijen en Service Bus-wachtrijen. Elk heeft een iets andere functieset, wat betekent dat Kies een of andere Hallo of beide, afhankelijk van de behoeften van uw bepaalde oplossing of -business-technische probleem, u het oplossen van hello gebruiken.

Bij het bepalen van welke queuing technologie past Hallo doel voor een bepaalde oplossing overwegen oplossingsarchitecten en -ontwikkelaars Hallo onderstaande aanbevelingen. Zie de volgende sectie Hallo voor meer informatie.

Als een oplossing systeemarchitect of ontwikkelaar, **Overweeg het gebruik van opslagwachtrijen** wanneer:

* Uw toepassing moet meer dan 80 GB van berichten opslaan in een wachtrij, waarbij Hallo-berichten een korter zijn dan 7 dagen levensduur hebben.
* Uw toepassing wil tootrack uitgevoerd voor het verwerken van een bericht binnen Hallo wachtrij. Dit is handig als Hallo worker verwerken van een bericht vastloopt. Een daaropvolgende werknemer kunt die informatie toocontinue vanaf waar Hallo voorafgaande worker gebleven was vervolgens gebruiken.
* Gewenste server side-logboeken van alle Hallo transacties die op uw wachtrijen worden uitgevoerd.

Als een oplossing systeemarchitect of ontwikkelaar, **Overweeg het gebruik van Service Bus-wachtrijen** wanneer:

* Uw oplossing moet kunnen tooreceive berichten zonder toopoll Hallo wachtrij. Met Service Bus, kan dit worden bereikt via Hallo gebruik van lange Hallo-polling ontvangstbewerking Hallo TCP-protocollen die ondersteuning biedt voor Service Bus gebruiken.
* Uw oplossing vereist Hallo wachtrij tooprovide een gegarandeerde first-in-first-out (FIFO) besteld levering.
* Wilt u een symmetrische ervaring in Azure en Windows Server (privécloud). Zie voor meer informatie [Service Bus voor Windows Server](https://msdn.microsoft.com/library/dn282144.aspx).
* Uw oplossing moet kunnen toosupport automatische detectie van duplicaten.
* U wilt dat uw toepassing tooprocess berichten als parallelle langlopende gegevensstromen (berichten zijn gekoppeld aan een stream met Hallo [SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) -eigenschap op het Hallo-bericht). In dit model concurreert op elk knooppunt in de toepassing verbruikt Hallo om gegevensstromen, als tegengestelde toomessages. Wanneer een stroom verbruikt knooppunt tooa opgegeven wordt, bekijk Hallo knooppunt Hallo status van Hallo stroom toepassingsstatus met behulp van transacties.
* Uw oplossing is vereist voor transactionele gedrag en atomisch bij het verzenden of ontvangen van meerdere berichten uit een wachtrij.
* Hallo time to live (TTL)-kenmerk van Hallo toepassingsspecifieke werkbelasting kan groter zijn dan 7 dagen Hallo.
* Uw toepassing berichten verwerkt die kunnen groter zijn dan 64 KB, maar wordt niet waarschijnlijk benadering Hallo limiet van 256 KB.
* U werkt met een vereiste tooprovide een toegangsgroepen op basis van model toohello wachtrijen, en andere rechten/machtigingen voor afzenders en ontvangers.
* De wachtrijgrootte van uw groeit niet groter zijn dan 80 GB.
* Wilt u toouse hello AMQP 1.0 op standaarden gebaseerde messaging-protocol. Zie voor meer informatie over AMQP [overzicht van Service Bus-AMQP](service-bus-amqp-overview.md).
* U kunt een uiteindelijke migratie uit op basis van een wachtrij point-to-point communicatie tooa bericht exchange patroon waarmee naadloze integratie van extra ontvangers (abonnees), die elk onafhankelijke kopieën van sommige of alle ontvangt combineren berichten toohello wachtrij. Hallo laatstgenoemde verwijst toohello publiceren/abonneren mogelijkheid systeemeigen geleverd door de Service Bus.
* Uw oplossing voor berichten moet kunnen toosupport Hallo 'in de meeste-eens' levering garantie zonder Hallo nodig is voor u toobuild Hallo extra infrastructuuronderdelen.
* U zou kunnen toopublish toobe zoals en verbruiken batches van berichten.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Vergelijking van opslagwachtrijen en Service Bus-wachtrijen
Hallo tabellen in de volgende secties Hallo bieden een logische groepering van functies van de wachtrij en kunnen u in één oogopslag Hallo mogelijkheden beschikbaar zijn in wachtrijen voor opslag en Service Bus-wachtrijen vergelijken.

## <a name="foundational-capabilities"></a>Fundamentele voorzieningen
Deze sectie worden enkele Hallo fundamentele queuing mogelijkheden van opslagwachtrijen en Service Bus-wachtrijen vergeleken.

| Vergelijkingscriteria | Opslagwachtrijen | Service Bus-wachtrijen |
| --- | --- | --- |
| Ordening garantie |**Nee** <br/><br>Zie Hallo eerste opmerking in de sectie 'Aanvullende informatie' Hallo voor meer informatie.</br> |**Ja - First-In-First-Out (FIFO)**<br/><br>(via Hallo-gebruik van de messaging-sessies) |
| Levering garantie |**Op de minste eenmaal** |**Op de minste eenmaal**<br/><br/>**In de meeste eens** |
| Ondersteuning voor atomic-bewerking |**Nee** |**Ja**<br/><br/> |
| Gedrag ontvangen |**Niet-blokkerende**<br/><br/>(uitgevoerd onmiddellijk als er geen nieuw bericht is gevonden) |**Blokkeren met of zonder time-out**<br/><br/>(biedt lange polling of Hallo ['Komeet techniek'](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**Niet-blokkerende**<br/><br/>(via Hallo gebruik van .NET beheerd API alleen) |
| Push-stijl-API |**Nee** |**Ja**<br/><br/>[OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) en **OnMessage** sessies .NET API. |
| Modus ontvangen |**Inspecteren & Lease** |**Inspecteren & vergrendelen**<br/><br/>**Ontvangen & verwijderen** |
| Modus van exclusieve toegang |**Op basis van de lease** |**Op basis van een vergrendeling** |
| Leasevergrendeling duur |**30 seconden (standaard)**<br/><br/>**7 dagen (maximum)** (u kunt vernieuwen of vrijgeven van de lease van een bericht met Hallo [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API.) |**60 seconden (standaard)**<br/><br/>U kunt een bericht vergrendeling met Hallo verlengen [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API. |
| Leasevergrendeling precisie |**Berichtniveau**<br/><br/>(elk bericht kan hebben een verschillende time-outwaarde, die u vervolgens indien nodig bijwerken kunt tijdens het verwerken van het Hallo-bericht, met behulp van Hallo [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API) |**Wachtrijniveau**<br/><br/>(elke wachtrij heeft een vergrendeling precisie toegepast tooall van de berichten te zien, maar kunt u Hallo vergrendelen met Hallo vernieuwen [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API.) |
| Batch verwerkt ontvangen |**Ja**<br/><br/>(expliciet op te geven aantal berichten bij het ophalen van berichten van tooa maximum van 32 berichten) |**Ja**<br/><br/>(impliciet inschakelen van de eigenschap van een vooraf vastgestelde of expliciet gebruikmaken van transacties via Hallo) |
| Batch verzenden |**Nee** |**Ja**<br/><br/>(via Hallo gebruik van transacties of clientzijde batchverwerking) |

### <a name="additional-information"></a>Aanvullende informatie
* Berichten in de opslagwachtrij worden doorgaans first-in-first-out kunnen, maar soms volgorde; bijvoorbeeld, wanneer een bericht zichtbaarheid time-outduur verloopt (bijvoorbeeld als gevolg van een clienttoepassing gecrasht tijdens de verwerking). Wanneer Hallo zichtbaarheid time-out is verlopen, het Hallo-bericht zichtbaar opnieuw op Hallo wachtrij voor een andere worker toodequeue deze. Op dat moment zojuist zichtbaar het Hallo-bericht kan worden geplaatst in de wachtrij Hallo (toobe uit wachtrij geplaatst opnieuw) na een bericht dat in de wachtrij oorspronkelijk nadat deze.
* Hallo gegarandeerd FIFO-patroon in Service Bus-wachtrijen Hallo gebruik van messaging-sessies vereist. In Hallo gebeurtenis die toepassing hello loopt vast bij het verwerken van een bericht ontvangen in Hallo **inspecteren & vergrendelen** modus, Hallo volgende keer dat de ontvanger van een wachtrij een messaging-sessie accepteert, wordt gestart met mislukte Hallo-bericht na de Time-to-live (TTL) is verlopen.
* Opslagwachtrijen zijn ontworpen toosupport standaard queuing scenario's, zoals ontkoppeling toepassing onderdelen tooincrease schaalbaarheid en tolerantie voor fouten, load leveling en samenstellen van proceswerkstromen.
* Service Bus-wachtrijen ondersteunen Hallo *op in de minste eenmaal* levering van garantie. Bovendien Hallo *in de meeste eens* semantische kan worden ondersteund met behulp van de status toostore Hallo toepassing sessiestatus en berichten ontvangen met behulp van transacties tooatomically en bijwerken van de sessiestatus Hallo.
* Opslagwachtrijen bieden een uniforme en consistente programmeermodel via wachtrijen, tabellen en BLOBs – voor ontwikkelaars en operations-teams.
* Service Bus-wachtrijen bieden ondersteuning voor lokale transacties in Hallo context van een enkele wachtrij.
* Hallo **ontvangt en verwijdert** ondersteund door Service Bus-modus biedt Hallo mogelijkheid tooreduce Hallo messaging bewerking count (en de bijbehorende kosten) voor de levering van verlaagde zekerheid.
* Opslagwachtrijen bieden leases met Hallo mogelijkheid tooextend Hallo leases voor berichten. Hierdoor kunnen toomaintain korte leases Hallo werknemers op berichten. Dus als een werknemer vastloopt, kunt het Hallo-bericht snel opnieuw worden verwerkt door een andere werknemer. Bovendien kan een werknemer Hallo lease op een bericht uitbreiden als deze tijd langer dan de huidige Hallo lease tooprocess.
* Opslagwachtrijen bieden een zichtbaarheid time-out die u kunt instellen op Hallo doelwachtrij plaatsen of waarbij van een bericht. Bovendien kunt u een bericht bijwerken met verschillende lease waarden tijdens runtime en update verschillende waarden voor berichten in Hallo dezelfde wachtrij. Service Bus vergrendeling time-outs zijn gedefinieerd in de metagegevens van de wachtrij Hallo; Hallo lock kunt u echter door de aanroepende Hallo vernieuwen [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) methode.
* Hallo maximale time-out is voor een blokkering ontvangstbewerking in Service Bus-wachtrijen 24 dagen. Time-outs REST gebaseerde hebben echter een maximumwaarde van 55 seconden.
* Client-side batchverwerking geleverd door Service Bus maakt een wachtrij client toobatch meerdere berichten in een enkel verzendbewerking. Batchverwerking is alleen beschikbaar voor verzenden van asynchrone bewerkingen.
* Functies zoals Hallo 200 TB maximum opslagwachtrijen (meer wanneer u accounts virtualiseren) en onbeperkt aantal wachtrijen kunt u een ideaal platform voor SaaS-providers.
* Opslagwachtrijen bieden een flexibele en zodat overgedragen mechanisme voor toegangsbeheer.

## <a name="advanced-capabilities"></a>Geavanceerde mogelijkheden
Deze sectie worden vergeleken geavanceerde mogelijkheden van opslagwachtrijen en Service Bus-wachtrijen.

| Vergelijkingscriteria | Opslagwachtrijen | Service Bus-wachtrijen |
| --- | --- | --- |
| Geplande levering |**Ja** |**Ja** |
| Automatische dode letters |**Nee** |**Ja** |
| Toenemende wachtrij time-to-live-waarde |**Ja**<br/><br/>(via InPlace-update van zichtbaarheid time-out) |**Ja**<br/><br/>(aangeboden via een speciale API-functie) |
| Ondersteuning voor message poison |**Ja** |**Ja** |
| InPlace-update |**Ja** |**Ja** |
| Transactielogboek serverzijde |**Ja** |**Nee** |
| Metrische gegevens Storage |**Ja**<br/><br/>**Minuut van metrische gegevens**: biedt realtime metrische gegevens voor beschikbaarheid, TPS, API aanroepen, tellingen, fout tellingen en meer in realtime (geaggregeerd per minuut en gerapporteerd binnen een paar minuten uit wat net is er gebeurd in productie. Zie voor meer informatie [Storage Analytics Metrics](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics). |**Ja**<br/><br/>(query's door aan te roepen bulksgewijs [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)) |
| Statusbeheer |**Nee** |**Ja**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| Automatisch doorsturen van berichten |**Nee** |**Ja** |
| Wachtrij-functie opschonen |**Ja** |**Nee** |
| Bericht-groepen |**Nee** |**Ja**<br/><br/>(via Hallo-gebruik van de messaging-sessies) |
| De status van de toepassing per groep bericht |**Nee** |**Ja** |
| Detectie van duplicaten |**Nee** |**Ja**<br/><br/>(configureerbaar Hallo afzender-zijde) |
| Bladeren door groepen berichten |**Nee** |**Ja** |
| Bericht-sessies door-ID ophalen |**Nee** |**Ja** |

### <a name="additional-information"></a>Aanvullende informatie
* Beide queuing technologieën kunnen een bericht toobe gepland voor ontvangst op een later tijdstip.
* Automatisch doorsturen van wachtrij kunt duizenden wachtrijen tooauto doorsturen hun berichten tooa enkele wachtrij, bij welke ontvangende toepassing hello Hallo-bericht verbruikt. U kunt dit mechanisme tooachieve beveiliging, Controlestroom en isoleren opslag tussen elke uitgever bericht.
* Opslagwachtrijen bieden ondersteuning voor het bijwerken van de inhoud van het bericht. U kunt deze functionaliteit voor persistent maken informatie over de status en van de incrementele voortgangsupdates gebruiken in het Hallo-bericht zodat deze kan worden verwerkt vanaf Hallo laatste controlepunt, in plaats van vanaf het begin starten. Met Service Bus-wachtrijen, kunt u Hallo hetzelfde scenario via Hallo-berichten uitwisselen. Sessies kunt u toosave en ophalen van de status van de verwerking van toepassing hello (met behulp van [SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) en [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [Dode lettering](service-bus-dead-letter-queues.md), die wordt alleen ondersteund door Service Bus-wachtrijen kan nuttig zijn voor het isoleren van berichten die met succes kunnen niet worden verwerkt door de ontvangende toepassing hello of wanneer berichten hun bestemming vanwege bereiken kunnen tooan verlopen Time-to-live (TTL) eigenschap. Hallo TTL-waarde geeft aan hoe lang een bericht in de wachtrij Hallo blijft. Met Service Bus is het Hallo-bericht verplaatste tooa speciale wachtrij $DeadLetterQueue wordt aangeroepen wanneer de Hallo TTL periode is verstreken.
* toofind 'verontreinigd' berichten in opslagwachtrijen, wanneer waarbij een bericht Hallo toepassing hello onderzoekt  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  eigenschap van het Hallo-bericht. Als **DequeueCount** groter is dan een opgegeven drempelwaarde Hallo toepassing hello bericht tooan toepassingsspecifieke ' ' wachtrij met onbestelde verplaatst.
* Opslagwachtrij kunnen u tooobtain een gedetailleerd logboek van alle transacties Hallo uitgevoerd tegen Hallo wachtrij, evenals metrische gegevens geaggregeerd. Beide opties zijn handig voor foutopsporing en inzicht in hoe uw toepassing gebruikmaakt van opslagwachtrijen. Ze zijn ook nuttig voor uw toepassing prestaties afstemmen en Hallo kosten van het gebruik van wachtrijen.
* Hallo-concept van '-berichten uitwisselen' wordt ondersteund door Service Bus kunt berichten die deel uitmaken van tooa bepaalde logische groep toobe die zijn gekoppeld aan een bepaalde ontvanger die op zijn beurt een sessie-achtige affiniteit tussen berichten en hun respectieve ontvangers maakt. U kunt deze geavanceerde functionaliteit van Service Bus door Hallo instelling inschakelen [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) eigenschap voor een bericht. Ontvangers kunnen luisteren op een bepaalde sessie-ID en ontvangen van berichten die delen van Hallo opgegeven sessie-id.
* Hallo duplicatie detectie functionaliteit automatisch wordt ondersteund door Service Bus-wachtrijen verwijdert dubbele berichten tooa wachtrij of onderwerp, op basis van de Hallo Hallo [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) eigenschap.

## <a name="capacity-and-quotas"></a>Capaciteit en quota 's
Deze sectie vergelijkt opslagwachtrijen en Service Bus-wachtrijen vanuit het oogpunt van Hallo van [capaciteit en quota](service-bus-quotas.md) die mogelijk van toepassing is.

| Vergelijkingscriteria | Opslagwachtrijen | Service Bus-wachtrijen |
| --- | --- | --- |
| Maximale wachtrijgrootte |**500 TB**<br/><br/>(beperkte tooa [opslagaccountcapaciteit eenmalige](../storage/common/storage-introduction.md#queue-storage)) |**1 GB too80 GB**<br/><br/>(gedefinieerd bij het maken van een wachtrij en [inschakelen partitioneren](service-bus-partitioning.md) – Zie de sectie 'Als u meer informatie' Hallo) |
| Maximale berichtgrootte |**64 KB**<br/><br/>(48 KB bij gebruik van **Base64** codering)<br/><br/>Azure biedt ondersteuning voor grote berichten door een combinatie van wachtrijen en blobs – in dat geval u in de wachtrij plaatsen van too200GB voor één item kunt. |**256 KB** of **1 MB**<br/><br/>(met inbegrip van de kop- en hoofdtekst maximale header-grootte: 64 KB).<br/><br/>Afhankelijk van Hallo [servicelaag](service-bus-premium-messaging.md). |
| Maximale bericht TTL |**7 dagen** |**`TimeSpan.Max`** |
| Maximum aantal wachtrijen |**Onbeperkt** |**10,000**<br/><br/>(per naamruimte van de service kan worden verhoogd) |
| Maximum aantal gelijktijdige clients |**Onbeperkt** |**Onbeperkt**<br/><br/>(de limiet van 100 gelijktijdige verbindingen alleen van toepassing tooTCP protocol-communicatie) |

### <a name="additional-information"></a>Aanvullende informatie
* De maximale grootte wachtrij zorgt ervoor dat Service Bus. Maximale wachtrijgrootte voor Hallo is opgegeven bij de aanmaak van Hallo wachtrij en een waarde tussen 1 en 80 GB kan hebben. Als Hallo wachtrij groottewaarde is ingesteld op het maken van de wachtrij Hallo is bereikt, extra binnenkomende berichten geweigerd en wordt een uitzondering ontvangen door Hallo code aanroepen. Zie voor meer informatie over quota in Service Bus [Service Bus quota](service-bus-quotas.md).
* In Hallo [standaardcategorie](service-bus-premium-messaging.md), kunt u Service Bus-wachtrijen in 1, 2, 3, 4 of 5 GB formaten (Hallo standaardwaarde is 1 GB). In de Premium-laag hello, kunt u wachtrijen up too80 GB groot. In de standaard-laag, met partitionering ingeschakeld (dit is Hallo standaardwaarde), Service Bus maakt 16 partities voor elke GB die u opgeeft. Als zodanig als u een wachtrij die 5 GB groot is maken, met 16 partities Hallo Maximale wachtrijgrootte wordt (5 * 16) = 80 GB. U kunt Hallo maximale grootte van uw gepartitioneerde wachtrij of onderwerp zien door te kijken op de vermelding ervan op Hallo [Azure-portal][Azure portal]. Op Hallo Premium-laag, worden alleen 2 partities per wachtrij gemaakt.
* Met opslagwachtrijen, als hello inhoud van het Hallo-bericht is geen XML-veilige, moet deze **Base64** gecodeerd. Als u **Base64**-coderen Hallo-bericht, de nettolading van de gebruiker Hallo kan up too48 KB, in plaats van 64 KB.
* Met Service Bus-wachtrijen wordt elk bericht dat is opgeslagen in een wachtrij bestaat uit twee delen: een header en een hoofdtekst. Hallo totale grootte van het Hallo-bericht mag maximaal Hallo-bericht grootte ondersteund door de servicelaag Hallo niet overschrijden.
* Wanneer clients met Service Bus-wachtrijen via Hallo TCP-protocol communiceren, is Hallo kunt u het maximum aantal gelijktijdige verbindingen tooa één Service Bus-wachtrij beperkt too100. Dit nummer wordt gedeeld tussen afzenders en ontvangers. Als dit quotum is bereikt, worden volgende aanvragen voor aanvullende verbindingen wordt geweigerd en wordt een uitzondering ontvangen door Hallo code aanroepen. Deze limiet is niet ingesteld op clients die verbinding maken met behulp van REST gebaseerde API toohello-wachtrijen.
* Als u meer dan 10.000 wachtrijen in een enkele Service Bus-naamruimte vereist, kunt u contact op met de ondersteuning van Azure-team Hallo en een verhoging aanvragen. tooscale dan 10.000 met Service Bus-wachtrijen, kunt u ook aanvullende naamruimten uitvoeren met Hallo maken [Azure-portal][Azure portal].

## <a name="management-and-operations"></a>Beheer van en bewerkingen
Deze sectie worden vergeleken Hallo management functies van Storage wachtrijen en Service Bus-wachtrijen.

| Vergelijkingscriteria | Opslagwachtrijen | Service Bus-wachtrijen |
| --- | --- | --- |
| Management-protocol |**REST-via HTTP/HTTPS** |**REST-via HTTPS** |
| Runtime-protocol |**REST-via HTTP/HTTPS** |**REST-via HTTPS**<br/><br/>**AMQP 1.0 standaard (TCP-protocol met TLS)** |
| .NET API |**Ja**<br/><br/>(.NET storage Client-API) |**Ja**<br/><br/>(.NET Servicebus API) |
| Native C++ |**Ja** |**Ja** |
| Java-API |**Ja** |**Ja** |
| PHP-API |**Ja** |**Ja** |
| Node.js-API |**Ja** |**Ja** |
| Ondersteuning voor willekeurige metagegevens |**Ja** |**Nee** |
| Wachtrij-naamgevingsregels |**Up too63 tekens bevatten**<br/><br/>(Letters in de naam van een wachtrij moeten kleine letters.) |**Up too260 tekens bevatten**<br/><br/>(Wachtrij paden en namen zijn niet hoofdlettergevoelig). |
| De functie lengte wachtrij ophalen |**Ja**<br/><br/>(Geschatte waarde als berichten na Hallo TTL verlopen zonder te worden verwijderd.) |**Ja**<br/><br/>(Exacte, punt in tijd waarde.) |
| Functie inspecteren |**Ja** |**Ja** |

### <a name="additional-information"></a>Aanvullende informatie
* Opslagwachtrijen bieden ondersteuning voor willekeurige kenmerken die toegepast toohello wachtrij beschrijving, in de vorm Hallo van naam/waarde-paren worden kunnen.
* Beide technologieën wachtrij bieden Hallo mogelijkheid toopeek een bericht zonder toolock it die nuttig zijn kan bij het implementeren van een wachtrij explorer-browser-hulpprogramma.
* Hallo .NET van Service Bus brokered messaging API's gebruiken voor de volledige-duplex TCP-verbindingen voor verbeterde prestaties wanneer tooREST vergeleken via HTTP, en ze standaard Hallo AMQP 1.0-protocol ondersteunen.
* Namen van opslagwachtrijen kan 3-63 tekens lang zijn, kan bestaan uit kleine letters, cijfers en afbreekstreepjes bevatten. Zie voor meer informatie [naamgeving van wachtrijen en metagegevens](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata).
* Namen van de service Bus-wachtrijen kunnen up too260 tekens lang zijn en minder beperkend naamgevingsregels hebben. Namen van de service Bus-wachtrijen kunnen letters, cijfers, punten, afbreekstreepjes en onderstrepingstekens bevatten.

## <a name="authentication-and-authorization"></a>Verificatie en autorisatie
Deze sectie wordt beschreven Hallo-verificatie en autorisatie functies ondersteund door opslagwachtrijen en Service Bus-wachtrijen.

| Vergelijkingscriteria | Opslagwachtrijen | Service Bus-wachtrijen |
| --- | --- | --- |
| Authentication |**Symmetrische sleutel** |**Symmetrische sleutel** |
| Beveiligingsmodel |Gedelegeerde toegang via SAS-tokens. |SAS |
| Provider van identiteitsfederatie |**Nee** |**Ja** |

### <a name="additional-information"></a>Aanvullende informatie
* Elke aanvraag tooeither Hallo queuing technologieën moet worden geverifieerd. Openbare wachtrijen met anonieme toegang worden niet ondersteund. Met behulp van [SAS](service-bus-sas.md), u kunt dit scenario oplossen door het publiceren van een alleen-schrijven SAS, alleen-lezen SAS of zelfs een SAS volledige toegang.
* Hallo verificatieschema opgegeven door de opslag wordt wachtrijen Hallo gebruikgemaakt van een symmetrische sleutel, die een HMAC hash-based Message Authentication Code () is, berekend met Hallo SHA-256-algoritme en gecodeerd als een **Base64** tekenreeks. Zie voor meer informatie over het betreffende protocol Hallo [verificatie voor hello Azure Storage-Services](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services). Service Bus-wachtrijen ondersteunen een vergelijkbaar model met symmetrische sleutels. Zie voor meer informatie [Shared Access Signature-verificatie met Service Bus](service-bus-sas.md).

## <a name="conclusion"></a>Conclusie
U gaat door een beter begrip van Hallo twee technologieën krijgen, kunnen toomake een meer gefundeerde beslissing waarop wachtrij technologie toouse worden, en wanneer. besluit op wanneer de opslagwachtrij toouse of Service Bus duidelijk wachtrijen Hallo afhankelijk is van een aantal factoren. Deze factoren kunnen afhankelijk van geheugenlatentie Hallo specifieke behoeften van uw toepassing en de bijbehorende architectuur. Als uw toepassing al gebruikmaakt van Hallo belangrijkste mogelijkheden van Microsoft Azure, gewenste toochoose opslagwachtrijen, vooral als u nodig hebt basic communicatie en uitwisseling van berichten tussen services of wachtrijen nodig die groter zijn dan 80 GB groot.

Omdat Service Bus-wachtrijen een aantal geavanceerde functies, zoals sessies, transacties bieden, detectie, automatische dubbele mogelijkheden voor verwerking van onbestelbare berichten en duurzame publiceren/abonneren ze kunnen een uitstekende keuze is als u een hybride-toepassing bouwt of als uw toepassing anders deze functies vereist.

## <a name="next-steps"></a>Volgende stappen
Hallo na artikelen bieden meer richtlijnen en informatie over het gebruik van Storage of Service Bus-wachtrijen.

* [Aan de slag met Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)
* [Hoe tooUse Hallo Queue Storage-Service](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Aanbevolen procedures voor verbeterde prestaties met Service Bus brokered messaging](service-bus-performance-improvements.md)
* [Inleiding tot wachtrijen en onderwerpen in de Azure Service Bus (blogbericht)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [Hallo Developer's Guide tooService Bus](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [Gebruik Hallo Queuing-Service in Azure](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

