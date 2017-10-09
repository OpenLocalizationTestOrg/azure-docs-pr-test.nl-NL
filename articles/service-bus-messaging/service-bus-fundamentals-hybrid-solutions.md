---
title: aaaOverview van grondbeginselen van Azure Service Bus | Microsoft Docs
description: Een inleiding toousing Service Bus tooconnect Azure-toepassingen tooother software.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Azure Service Bus

Of een toepassing of service wordt uitgevoerd in Hallo cloud of on-premises, moet deze vaak toointeract met andere toepassingen of services. een veelzijdige, handige manier toodo tooprovide deze, aanbiedingen van Microsoft Azure Service Bus. In dit artikel wordt bekeken deze technologie en wordt beschreven wat is het en waarom u wellicht toouse deze.

## <a name="service-bus-fundamentals"></a>Grondbeginselen van Service Bus

Verschillende situaties vragen om verschillende communicatiemethoden. Soms als toepassingen berichten via een eenvoudige wachtrij verzenden en ontvangen, is de beste oplossing Hallo. In andere gevallen is een gewone wachtrij niet voldoende en voldoet een wachtrij met een mechanisme voor publiceren en abonneren beter. In sommige gevallen is alleen een verbinding tussen toepassingen nodig en is er geen behoefte aan een wachtrij. Service Bus biedt alle drie de opties, waardoor uw toointeract toepassingen op verschillende manieren.

Service Bus is een multitenant-cloudservice, wat betekent dat Hallo-service wordt gedeeld door meerdere gebruikers. Elke gebruiker, zoals een toepassingsontwikkelaar, maakt een *naamruimte*, definieert Hallo communicatie mechanismen nodig binnen deze naamruimte. In afbeelding 1 ziet u hoe deze architectuur eruit ziet.

![][1]

**Afbeelding 1: Servicebus biedt een multitenant-service voor het verbinden van toepassingen via Hallo cloud.**

Binnen een naamruimte kunt u een of meer exemplaren van drie verschillende communicatiemechanismen gebruiken, die toepassingen alle drie op een andere manier verbinden. Hallo-opties zijn:

* *Wachtrijen*, waarmee communicatie in één richting mogelijk is. Elke wachtrij fungeert als intermediaire service (ook wel *broker* genoemd) die de verzonden berichten opslaat totdat ze worden ontvangen. Elk bericht wordt door één ontvanger ontvangen.
* *Onderwerpen*, die communicatie in één richting bieden via *abonnementen*, waarbij een enkel onderwerp meerdere abonnementen kan hebben. Net zoals een wachtrij fungeert een onderwerp als broker, maar elk abonnement kunt optioneel een filter tooreceive alleen berichten die aan bepaalde criteria voldoen.
* *Relays*, die bidirectionele communicatie bieden. In tegenstelling tot wachtrijen en onderwerpen, worden via een relay berichten die onderweg zijn niet opgeslagen. Een relay is geen broker. In plaats daarvan deze berichten worden slechts doorgegeven op de doeltoepassing toohello.

Wanneer u een wachtrij, onderwerp of relay maakt, geeft u deze een naam. Gecombineerd met de naam van uw naamruimte, maakt deze naam een unieke id voor het Hallo-object. Toepassingen kunnen bieden deze naam tooService Bus en vervolgens die wachtrij, onderwerp of relay toocommunicate met elkaar gebruiken. 

toouse een van deze objecten in Hallo relay scenario, Windows-toepassingen kunnen gebruikmaken van Windows Communication Foundation (WCF). Deze service wordt ook wel [WCF-relay](../service-bus-relay/relay-what-is-it.md). Voor wachtrijen en onderwerpen kunnen Windows-toepassingen door Service Bus gedefinieerde berichtenservice-API's gebruiken. toomake deze objecten gemakkelijker toouse uit niet-Windows-toepassingen, Microsoft biedt SDK's voor Java, Node.js en andere talen. U hebt ook toegang tot wachtrijen en onderwerpen met behulp van [REST-API's](/rest/api/servicebus/) via HTTP(S). 

Het is belangrijk toounderstand dat hoewel Service Bus zelf wordt uitgevoerd in Hallo-cloud (dat wil zeggen, in Azure-datacenters van Microsoft), overal kunnen worden uitgevoerd door toepassingen die worden gebruikt. U kunt Service Bus tooconnect toepassingen die worden uitgevoerd op Azure, bijvoorbeeld of toepassingen die worden uitgevoerd binnen uw eigen datacenter. U kunt deze ook gebruiken tooconnect een toepassing die wordt uitgevoerd op Azure of een ander cloudplatform met een on-premises toepassing of tablets en telefoons. Het is tooconnect zelfs mogelijk huishoudelijke apparaten, sensoren en andere apparaten tooa centrale toepassing of andere tooone. Service Bus is een communicatiemechanisme in Hallo cloud die toegankelijk is vanaf vrijwel elke locatie. Hoe u afhankelijk deze van welke uw toepassingen toodo moeten.

## <a name="queues"></a>Wachtrijen

Stel dat u tooconnect twee toepassingen met behulp van een Service Bus-wachtrij bepalen. In afbeelding 2 ziet u deze situatie.

![][2]

**Afbeelding 2: Service Bus-wachtrijen bieden asynchrone wachtrijservices in één richting.**

Hallo-proces is eenvoudig: een afzender verzendt een bericht tooa Service Bus-wachtrij en een ontvanger neemt dat bericht over op een later tijdstip. Een wachtrij kan slechts één ontvanger, hebben, zoals in afbeelding 2 wordt weergegeven. Of meerdere toepassingen kunnen worden gelezen vanaf Hallo dezelfde wachtrij. In het laatste geval hello wordt elk bericht gelezen door slechts één ontvanger. Voor een multicast-service is het echter beter om een onderwerp te gebruiken.

Elk bericht bestaat uit twee delen: een reeks eigenschappen, elk een sleutel-waardepaar, en een berichtnettolading. Hallo nettolading kan binair, tekst of zelfs XML zijn. Hoe deze worden gebruikt, is afhankelijk van wat een toepassing toodo probeert. Een toepassing verzenden van een bericht over een recente verkoop kan bijvoorbeeld Hallo eigenschappen **verkoper = 'Ava'** en **bedrag = 10000**. Hallo berichttekst kan een gescande afbeelding van Hallo ondertekende verkoopovereenkomst bevatten of als er niet is, leeg blijven.

Een ontvanger kan op twee verschillende manieren een bericht in een Service Bus-wachtrij lezen. eerste optie, Hallo  *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, wordt een bericht uit de wachtrij Hallo en onmiddellijk gewist. Deze optie is eenvoudig, maar als Hallo ontvanger vastloopt voordat het klaar is met het verwerken van het Hallo-bericht, Hallo-bericht is verloren gegaan. Omdat deze wordt verwijderd uit de wachtrij hello, geen andere ontvanger met toegang tot dit. 

tweede optie Hallo  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, toohelp bij dit probleem is bedoeld. Zoals **ReceiveAndDelete**, een **PeekLock** lezen wordt een bericht uit de wachtrij Hallo. Het verwijderen Hallo-bericht echter niet. In plaats daarvan Hiermee vergrendelt u het Hallo-bericht, waardoor het onzichtbaar tooother ontvangers, vervolgens wordt gewacht op een van drie gebeurtenissen:

* Als Hallo ontvanger processen hello bericht is, ontvangt [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete), en Hallo wachtrij verwijdert het Hallo-bericht. 
* Als de ontvanger Hallo beslist dat het Hallo-bericht niet kan verwerken, ontvangt [Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon). Hallo wachtrij vervolgens Hallo vergrendeling verwijdert uit het Hallo-bericht en maakt het beschikbaar tooother ontvangers.
* Als de ontvanger Hallo geen van deze methoden (standaard 60 seconden) binnen een configureerbare periode aanroept, Hallo wachtrij wordt ervan uitgegaan Hallo ontvanger is mislukt. In dit geval het gedraagt zich alsof de ontvanger Hallo had aangeroepen **afbreken**, waardoor het Hallo-bericht beschikbaar tooother ontvangers.

U ziet hier dus: hello hetzelfde bericht mogelijk tweemaal worden geleverd, mogelijk tootwo verschillende ontvangers. Toepassingen die gebruikmaken van Service Bus-wachtrijen, moeten hiermee rekening houden. toomake detectie van duplicaten gemakkelijker, elk bericht heeft een unieke [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) eigenschap die standaard Hallo blijft hetzelfde, ongeacht hoe vaak het Hallo-bericht is gelezen uit een wachtrij. 

Wachtrijen zijn handig in tal van situaties. Ze toepassingen toocommunicate inschakelen, zelfs als beide niet worden uitgevoerd op Hallo dezelfde tijd, iets wat is vooral handig met batch- en mobiele toepassingen. Een wachtrij met meerdere ontvangers biedt ook automatische taakverdeling, aangezien verzonden berichten worden verdeeld over deze ontvangers.

## <a name="topics"></a>Onderwerpen

Hoewel ze handig zijn, zijn wachtrijen niet altijd de juiste oplossing Hallo. Service Bus-onderwerpen komen soms beter van pas. Afbeelding 3 laat dit zien.

![][3]

**Afbeelding 3: Gebaseerd op Hallo-filter die een geabonneerde toepassing bevat, krijgt sommige of alle Hallo-berichten tooa Service Bus-onderwerp.**

Een *onderwerp* lijkt op veel manieren tooa wachtrij. Afzenders verzenden berichten tooa onderwerp in Hallo dezelfde manier die ze berichten tooa wachtrij verzenden, en deze berichten uiterlijk Hallo hetzelfde als bij een wachtrij. Hallo verschil is dat onderwerpen elke ontvangende toepassing toocreate inschakelen eigen *abonnement* door te definiëren die een *filter*. Een abonnee ziet vervolgens alleen Hallo-berichten die met het filter overeenkomen. In afbeelding 3 ziet u bijvoorbeeld een afzender en een onderwerp met drie abonnees, elk met een eigen filter:

* Abonnee 1 ontvangt alleen berichten met de eigenschap Hallo *verkoper = 'Ava'*.
* Abonnee 2 ontvangt berichten met de eigenschap Hallo *verkoper = 'Ruby'* en/of bevatten een *bedrag* eigenschap waarvan de waarde groter dan 100.000 is. Wellicht is Ruby Hallo Verkoopmanager en zodat ze wil toosee zowel haar eigen verkopen als alle grote verkoop ongeacht wie ze tot stand brengt.
* Abonnee 3 heeft het filter te ingesteld*True*, wat betekent dat alle berichten worden ontvangen. Bijvoorbeeld: deze toepassing kan zijn verantwoordelijk voor het onderhouden van een audittrail en moet deze toosee alle Hallo-berichten.

Zoals wachtrijen, abonnees tooa onderwerp berichten lezen met een [ReceiveAndDelete of PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode). In tegenstelling tot wachtrijen, echter verzonden een enkel bericht tooa onderwerp kan worden ontvangen door meerdere abonnementen. Deze benadering, doorgaans aangeduid *publiceren en abonneren* (of *pub subitems*), is nuttig wanneer meerdere toepassingen zijn geïnteresseerd in Hallo dezelfde berichten. Met het juiste filter Hallo definiëren, kunnen abonnees in slechts Hallo deel van de berichtenstroom Hallo dat het toosee moet.

## <a name="relays"></a>Relays

Wachtrijen en onderwerpen bieden allebei asynchrone communicatie in één richting via een broker. Het verkeer stroomt in één richting en er is geen directe verbinding tussen afzenders en ontvangers. Maar wat als u dit niet wilt? Stel dat uw toepassingen moet tooboth verzenden en ontvangen berichten, of misschien u wilt dat een rechtstreekse koppeling tussen en hoeft u geen broker toostore berichten. tooaddress scenario's zoals deze, Service Bus biedt *doorstuurt*, zoals in afbeelding 4 ziet.

![][4]

**Afbeelding 4: Service Bus Relay biedt synchrone communicatie in twee richtingen tussen toepassingen.**

Hallo tooask van de hand liggende vraag over relays is dit: Waarom zou ik die gebruiken? Zelfs als ik geen wachtrijen nodig hebt, waarom zouden toepassingen dan communiceren via een cloudservice in plaats van ze rechtstreeks communiceren? Hallo-antwoord is dat communiceren rechtstreeks lastiger zijn kan dan u denkt.

Stel dat u wilt dat tooconnect twee on-premises toepassingen, zowel uitgevoerd binnen bedrijfsdatacenters. Elk van deze toepassingen bevindt zich achter een firewall en elk datacenter maakt waarschijnlijk gebruik van NAT (netwerkadresomzetting). Hallo firewall blokkeert binnenkomende gegevens op alle maar een paar poorten en NAT impliceert dat elke toepassing wordt uitgevoerd op Hallo-machine beschikt niet over een vaste IP-adres dat u rechtstreeks kunt bereiken buiten Hallo datacenter. Zonder extra hulp, deze toepassingen met elkaar verbinden via Hallo openbare internet is problematisch.

Een Service Bus-relay biedt uitkomst. toocommunicate twee richtingen via een relay, elke toepassing een uitgaande TCP-verbinding maakt met Service Bus en blijft geopend. Alle communicatie tussen de twee toepassingen Hallo via deze verbindingen wordt gezonden. Omdat elke verbinding tot stand is gebracht van binnen Hallo datacenter, Hallo firewall staat binnenkomende verkeer tooeach toepassing zonder nieuwe poorten te openen. Deze benadering wordt ook Hallo NAT-probleem opgelost, omdat elke toepassing een consistent eindpunt in de cloud in de gehele Hallo communicatie Hallo heeft. Door het uitwisselen van gegevens via de relay Hallo Hallo toepassingen te voorkomen dat Hallo problemen die anders communicatie moeilijk zouden. 

toouse Service Bus doorstuurt, toepassingen afhankelijk zijn van Hallo Windows Communication Foundation (WCF). Service Bus biedt WCF-bindingen waarmee Windows-toepassingen toointeract via relays eenvoudig. Toepassingen die al gebruikmaken van WCF kunnen meestal een van deze bindingen opgeven en vervolgens praten tooeach andere via een relay. Relays kunnen worden gebruikt vanuit niet-Windows-toepassingen, maar in tegenstelling tot wachtrijen en onderwerpen vereist dit enige programmering. Er worden geen standaardbibliotheken geleverd.

In tegenstelling tot wachtrijen en onderwerpen, maken toepassingen Relays niet expliciet. In plaats daarvan wanneer een toepassing die u tooreceive berichten wenst TCP-verbinding met een Service Bus maakt, is een relay automatisch gemaakt. Wanneer het Hallo-verbinding wordt verbroken, wordt Hallo relay verwijderd. tooenable een toepassing toofind Hallo relay gemaakt door een specifieke listener, Service Bus voorziet in een register waarmee toepassingen toolocate een specifieke relay op naam.

Relays zijn de juiste oplossing Hallo wanneer u rechtstreekse communicatie tussen toepassingen nodig. Denk bijvoorbeeld aan een reserveringssysteem voor een luchtvaartmaatschappij dat wordt uitgevoerd in een on-premises datacenter en dat toegankelijk moet zijn via incheckbalies, mobiele apparaten en andere computers. Toepassingen die worden uitgevoerd op alle deze systemen kunnen vertrouwen op Service Bus relays in Hallo cloud toocommunicate, waar ze ook worden uitgevoerd.

## <a name="summary"></a>Samenvatting

Het verbinden van toepassingen is altijd onderdeel geweest van het ontwikkelen van complete oplossingen en Hallo scala aan scenario's waarvoor toepassingen en services toocommunicate met elkaar tooincrease is ingesteld als u meer toepassingen en apparaten verbonden toohello zijn internet. Dankzij de cloud-gebaseerde technologieën voor het bereiken van de communicatie via wachtrijen, onderwerpen en relays, Service Bus is erop gericht toomake deze essentiële functie gemakkelijker tooimplement en grotere schaal beschikbaar.

## <a name="next-steps"></a>Volgende stappen

Nu u de basisprincipes van Azure Service Bus Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.

* Hoe toouse [Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)
* Hoe toouse [Service Bus-onderwerpen](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* Hoe toouse [Service Bus relay](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [Voorbeelden van Service Bus](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png
