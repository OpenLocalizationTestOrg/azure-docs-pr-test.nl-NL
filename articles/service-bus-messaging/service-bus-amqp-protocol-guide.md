---
title: aaaAMQP 1.0 in Azure Service Bus en Event Hubs protocol handleiding | Microsoft Docs
description: Protocol handleiding tooexpressions en beschrijving van AMQP 1.0 in Azure Service Bus en Event Hubs
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# AMQP 1.0 in Azure Service Bus en Event Hubs-protocol-handleiding

Hallo is geavanceerde Message Queueing Protocol 1.0 een gestandaardiseerde framing en transfer protocol voor het asynchroon, veilig en betrouwbaar berichten over te brengen tussen twee partijen. Is het primaire protocol Hallo van Azure Service Bus-berichtenservice en Azure Event Hubs. Beide services bieden ook ondersteuning voor HTTPS. Hallo bedrijfseigen SBMP protocol dat wordt ook ondersteund wordt door de AMQP geleidelijk stopgezet.

AMQP 1.0 is Hallo resultaat van brede bedrijfstak samenwerking die middleware leveranciers, zoals Microsoft en Red Hat met veel messaging middleware gebruikers zoals JP Morgan Chase Hallo financiële diensten bedrijfstak die bij elkaar gebracht. Hallo technische normalisatie-forum voor Hallo AMQP-protocol en de extensie specificaties OASIS is en deze formele goedkeuring als een internationale standaard als ISO/IEC 19494 heeft bereikt.

## Doelstellingen

In dit artikel bevat een overzicht van Hallo belangrijkste concepten van messaging Hallo AMQP 1.0-specificatie samen met een kleine set ontwerpspecificaties voor uitbreiding die momenteel nog in Hallo OASIS AMQP technisch comité gewerkt wordt kort en wordt uitgelegd hoe Azure Servicebus implementeert en bouwt voort op deze specificaties.

Hallo-doel is voor ontwikkelaars met behulp van een bestaande AMQP 1.0-client-stack op elk platform toobe toointeract kunnen met Azure Service Bus via AMQP 1.0.

Algemene algemene AMQP 1.0-stacks, zoals Apache Proton of AMQP.NET Lite, worden al alle core AMQP 1.0-gebaren implementeren. Deze fundamentele gebaren zijn soms verpakt met een hoger niveau API; Apache Proton zelfs biedt twee, Hallo imperatieve Messenger-API en Hallo reactieve Reactor API.

In de Hallo bespreking van de volgende, gaan we ervan uit dat Hallo beheer van AMQP-verbindingen, sessies en koppelingen en Hallo verwerking van het frame overschrijvingen en datatransportbesturing worden verwerkt door de respectieve Hallo-stack (zoals Apache Proton-C) en hoeven niet veel eventuele specifieke de aandacht van ontwikkelaars van toepassingen. Abstract Aannemende Hallo bestaan van een paar API primitieven zoals Hallo mogelijkheid tooconnect en toocreate een vorm van *afzender* en *ontvanger* abstractie-objecten, die u enige vorm van hebt`send()`en `receive()` bewerkingen, respectievelijk.

Wanneer u geavanceerde mogelijkheden van Azure Service Bus, zoals bericht bladeren of beheer van sessies, worden deze functies worden beschreven in AMQP voorwaarden, maar ook als de implementatie van een gelaagd pseudo boven deze aangenomen API abstractie op.

## Wat is AMQP?

AMQP is een protocol framing en de overdracht. Framing betekent dat deze structuur biedt voor binaire gegevensstromen die in beide richtingen van een netwerkverbinding stromen. Hallo-structuur biedt begrenzing voor afzonderlijke blokken met gegevens, aangeroepen *frames*, toobe uitgewisseld tussen Hallo verbonden partijen. Hallo-overdrachtmogelijkheden Zorg ervoor dat beide communicerende partijen tot stand brengen een gedeelde kennis over wanneer frames worden overgedragen, en wanneer overdrachten worden beschouwd voltooid.

In tegenstelling tot eerdere verlopen conceptversies die wordt geproduceerd door Hallo AMQP werkgroep die nog in gebruik door een enkele bericht beleggingsmakelaars, schrijven Hallo van de werkgroep final en gestandaardiseerde AMQP 1.0-protocol niet Hallo aanwezigheid van een bericht broker of een bepaalde topologie voor entiteiten in een bericht broker.

Hallo-protocol kan worden gebruikt voor symmetrische peer-to-peer-communicatie voor interactie met bericht beleggingsmakelaars die ondersteuning bieden voor wachtrijen en entiteiten publiceren/abonneren, zoals Azure Service Bus biedt. Het kan ook worden gebruikt voor interactie met berichteninfrastructuur waar Hallo interactie patronen verschillen van reguliere wachtrijen, zoals Hallo geval met Azure Event Hubs. Een Event Hub fungeert als een wachtrij wanneer gebeurtenissen tooit worden verzonden, maar meer fungeert als een seriële opslagservice wanneer gebeurtenissen worden gelezen uit het lijkt erg op een tapestation. Hallo client haalt een offset Hallo beschikbare gegevens stroom en vervolgens alle gebeurtenissen uit dat offset toohello meest recente beschikbare worden geleverd.

Hallo AMQP 1.0-protocol is ontworpen toobe uitbreidbaar, waardoor verdere specificaties tooenhance mogelijkheden ervan. Hallo drie extensie specificaties in dit document besproken illustratie. Voor communicatie via bestaande HTTPS/WebSockets infrastructuur waar Hallo systeemeigen AMQP TCP-poorten configureren kan lastig zijn, een specificatie voor de binding wordt gedefinieerd hoe toolayer AMQP via WebSockets. Voor interactie met Hallo messaging-infrastructuur in een aanvraag/antwoord definieert wijze voor beheerdoeleinden of tooprovide geavanceerde functionaliteit, Hallo AMQP management specificatie Hallo vereist basic interactie primitieven. Voor federatieve autorisatie model-integratie Hallo AMQP claims-beveiliging op basis van-specificatie definieert hoe tooassociate en autorisatie-tokens die zijn gekoppeld aan de koppelingen te vernieuwen.

## Basic AMQP-scenario 's

Deze sectie wordt uitgelegd Hallo basisgebruik van AMQP 1.0 met Azure Service Bus, waaronder verbindingen, sessies en koppelingen maken en berichten tooand overzetten van Service Bus-entiteiten zoals wachtrijen, onderwerpen en abonnementen.

Hallo gezaghebbende bron toolearn over de werking van AMQP hello AMQP 1.0-specificatie is, maar Hallo specificatie tooprecisely handleiding implementatie en niet tooteach Hallo-protocol is geschreven. Deze sectie richt zich op de introductie van zoveel terminologie zo nodig voor het beschrijven hoe Service Bus maakt gebruik van AMQP 1.0. Raadpleeg voor een uitgebreidere inleiding tooAMQP, evenals een uitgebreidere bespreking van AMQP 1.0, [deze video maatregel][this video course].

### Verbindingen en sessies

AMQP aanroepen Hallo communicatie van programma's *containers*; deze bevatten *knooppunten*, welke Hallo entiteiten binnen deze containers communiceren. Een wachtrij kan deze een knooppunt zijn. AMQP kunt voor multiplex, zodat één verbinding kan worden gebruikt voor veel communicatiepaden tussen knooppunten. bijvoorbeeld, een toepassingsclient gelijktijdig via kan ontvangen van een wachtrij en tooanother verzendwachtrij Hallo dezelfde netwerkverbinding.

![][1]

Hallo-netwerkverbinding is dus verankerd op Hallo-container. Deze is gestart door Hallo-container in Hallo client rol maken van een uitgaande TCP-socket verbinding tooa-container in Hallo ontvanger functie, die luistert naar en binnenkomende TCP-verbindingen accepteert. handshake van verbinding Hallo omvat onderhandelen Hallo-protocolversie, declareren of Hallo gebruik van Transport Level Security (TLS/SSL) en een handshake-verificatie/autorisatie bij Hallo verbindingsbereik dat is gebaseerd op SASL onderhandelen.

Azure Service Bus vereist Hallo gebruik van TLS te allen tijde. Het ondersteunt verbindingen via TCP-poort 5671, waarbij Hallo TCP-verbinding, eerst met TLS heen wordt weergegeven voordat de Hallo AMQP-protocol-handshake en biedt ook ondersteuning voor verbindingen via TCP-poort 5672 waarbij Hallo server direct de upgrade van een verplichte van biedt verbinding tooTLS met Hallo AMQP voorgeschreven model. Hallo AMQP WebSockets binding maakt een tunnel via TCP-poort 443, die vervolgens gelijkwaardige tooAMQP 5671 verbindingen.

Na het instellen van het Hallo-verbinding en TLS, biedt Service Bus twee SASL mechanisme opties:

* SASL zonder opmaak wordt meestal gebruikt voor het doorgeven van de gebruikersnaam en wachtwoord referenties tooa-server. Service Bus heeft geen accounts, maar met de naam [gedeelde toegang beveiligingsregels](service-bus-sas.md), die rechten verlenen en zijn gekoppeld aan een sleutel. Hallo-naam van een regel wordt gebruikt als het Hallo-gebruikersnaam en het Hallo-sleutel (zoals base64-tekst gecodeerde) wordt gebruikt als Hallo wachtwoord. Hallo rechten die zijn gekoppeld aan Hallo gekozen regel betrekking op Hallo-bewerkingen op Hallo verbinding toegestaan.
* ANONIEME SASL wordt gebruikt voor het omzeilen van SASL autorisatie wanneer Hallo client wil toouse Hallo claims-beveiligingsmodel op basis van-(CBS) die verderop wordt beschreven. Met deze optie wordt een client kan verbinding anoniem gedurende een korte periode gedurende welke Hallo alleen client kan communiceren met de Hallo CBS eindpunt en Hallo CBS handshake moet voltooien.

Nadat de transportverbinding Hallo tot stand is gebracht, Hallo containers elk declareren Hallo maximale framegrootte zijn bereid toohandle en na een inactiviteit ze hebt eenzijdig verbreken als er geen activiteit op Hallo-verbinding.

Tevens declareren hoeveel gelijktijdige kanalen worden ondersteund. Een kanaal is een overdracht unidirectioneel, uitgaande, virtuele pad boven op het Hallo-verbinding. Een sessie heeft een kanaal van elk van de Hallo onderling verbonden containers tooform een bidirectionele communicatiepad.

Sessies hebben een model voor het toegangsbeheer op basis van het venster stroom; Wanneer een sessie wordt gemaakt, elke partij wordt aangegeven hoeveel frames is bereid tooaccept in het venster ontvangen. Wanneer hello partijen exchange frames overgedragen frames vullen venster en overdrachten stoppen wanneer Hallo venster vol is en totdat Hallo venster opnieuw wordt ingesteld of uitgebreid met Hallo *stroom performative* (*performative*is Hallo AMQP term voor protocolniveau gebaren uitgewisseld tussen Hallo twee partijen).

Dit model op basis van een venster is grofweg overeen toohello TCP-concept van datatransportbesturing op basis van het venster, maar op Hallo sessie niveau binnen Hallo socket. Hallo ervoor van protocol concept van waardoor meerdere gelijktijdige sessies te zorgen dat verkeer met hoge prioriteit kan worden meest voorbij beperkte normale verkeer, zoals op een snelle lane weg.

Azure Service Bus gebruikt momenteel precies één sessie voor elke verbinding. Hallo Service Bus-frame-maximumgrootte is 262.144 bytes (256 kB) voor Service Bus Standard en Event Hubs. Het is 1.048.576 (1 MB) voor Service Bus Premium. Service Bus een bepaalde sessie-niveau bandbreedteregeling windows niet afdwingen, maar opnieuw instellen van venster regelmatig Hallo als onderdeel van de link-level datatransportbesturing (Zie [Hallo van de volgende sectie](#links)).

Verbindingen, kanalen en sessies zijn kortstondige. Als de onderliggende verbinding Hallo worden samengevouwen, verbindingen, TLS-tunnel, SASL verificatiecontext en sessies moeten opnieuw worden gemaakt.

### Koppelingen

AMQP draagt berichten via koppelingen. Een koppeling is een communicatiepad gemaakt via een sessie waarmee overgebracht berichten in één richting; Hallo overdracht status onderhandeling is via het Hallo-koppeling en twee richtingen tussen Hallo verbonden partijen.

![][2]

Koppelingen kunnen worden gemaakt op de container op elk gewenst moment en via een bestaande sessie, waardoor AMQP verschilt van de vele andere protocollen, met inbegrip van HTTP- en MQTT, waarbij Hallo initiatie van overdrachten en pad van de overdracht is een exclusieve bevoegdheid van Hallo partij maken de socketverbinding Hallo.

Hallo koppeling initiëren container Hallo tegenover container tooaccept wordt gevraagd een koppeling en een rol van de afzender of ontvanger worden gekozen. Daarom een container maken Unidirectioneel kunt starten of bidirectionele communicatiepaden, met de laatste Hallo gemodelleerd als paren van koppelingen.

Koppelingen zijn met de naam en die zijn gekoppeld aan knooppunten. Zoals vermeld in Hallo begin, zijn knooppunten Hallo communiceren entiteiten in een container.

In de Service Bus is een knooppunt rechtstreeks gelijkwaardige tooa wachtrij, een onderwerp, een abonnement of een wachtrij voor onbestelbare subwachtrij van een wachtrij of abonnement. Hallo knooppuntnaam gebruikt in AMQP is daarom Hallo relatieve naam van de entiteit Hallo binnen Hallo Service Bus-naamruimte. Als de naam van een wachtrij **rapportberichten**, is ook de naam van de AMQP-knooppunt. Een onderwerpabonnement volgt Hallo HTTP API convention door wordt gesorteerd in een verzameling van de resource 'abonnementen' en dus een abonnement **sub** of een onderwerp **mytopic** heeft de naam van het knooppunt Hallo AMQP **abonnementen mytopic subitems**.

Hallo client die verbinding maakt, is ook vereist toouse een lokale knooppuntnaam voor het maken van koppelingen; Service Bus is geen richtlijnen over de knooppuntnamen en komt niet interpreteren. AMQP 1.0-client stacks gebruiken doorgaans een schema tooassure dat deze tijdelijke knooppuntnamen uniek binnen het bereik van de client Hallo Hallo zijn.

### Overdrachten

Zodra een koppeling tot stand is gebracht, kunnen berichten worden verzonden via deze koppeling. In AMQP, een overdracht wordt uitgevoerd met een gebaar van de expliciete protocol (Hallo *overdracht* performative) die een bericht verplaatst van afzender tooreceiver via een koppeling. Een overdracht is voltooid als het 'betaald', wat betekent dat beide partijen een gedeelde kennis van Hallo resultaat van deze overdracht hebt gemaakt.

![][3]

In de meest eenvoudige geval Hallo kiezen Hallo afzender toosend berichten 'vooraf afgewikkeld', wat betekent dat Hallo-client niet geïnteresseerd in Hallo uitkomst is en Hallo ontvanger geen opmerkingen of vragen hebt over de uitkomst van Hallo bewerking Hallo biedt. Deze modus wordt ondersteund door Service Bus op Hallo AMQP protocolniveau, maar niet worden weergegeven in een van de Hallo client-API's.

Hallo reguliere geval is dat berichten worden verzonden niet-vereffende en Hallo ontvanger vervolgens betekent acceptatie- of afwijzing Hallo met *toestand* performative. Afwijzing treedt op wanneer Hallo ontvanger het Hallo-bericht niet om welke reden accepteren kan en afwijzing het Hallo-bericht bevat informatie over de reden hello, dit een fout-structuur die is gedefinieerd door AMQP is. Als berichten worden geweigerd vanwege fouten in de Service Bus toointernal, stuurt Hallo service extra informatie in die structuur die kan worden gebruikt voor het ontwikkelen van diagnostische gegevens hints toosupport personeel als u ondersteuningsaanvragen indient. U leert later meer informatie over fouten.

Een speciale vorm van afwijzing is Hallo *uitgebracht* staat, wat aangeeft dat Hallo ontvanger heeft geen technisch bezwaar toohello transfer, maar ook geen belang bij het vereffenen overdracht Hallo. Dat geval bestaat, bijvoorbeeld wanneer een bericht wordt bezorgd tooa Service Bus-clienttoepassing en Hallo client kiest te 'verlaten' Hallo-bericht omdat Hallo werk ten gevolge van het verwerken van het Hallo-bericht; kan niet worden uitgevoerd Hallo berichtbezorging zelf is niet op fouten. Een variant van die status is Hallo *gewijzigd* status heeft waarmee wijzigingen toohello bericht bij de release. Die staat, wordt op dit moment niet door Service Bus gebruikt.

Hallo AMQP 1.0-specificatie definieert een verdere disposition status aangeroepen *ontvangen*, waarmee specifiek toohandle koppeling herstel. Herstel van de koppeling kunt endinfrastructuur Hallo status van een koppeling en in behandeling zijnde leveringen boven op een nieuwe verbinding en -sessie wanneer Hallo eerdere verbinding en sessie verloren gegaan zijn.

Service Bus biedt geen ondersteuning voor herstel van de koppeling; Als client Hallo Hallo verbinding tooService Bus met een niet-vereffende bericht verliest transfer in behandeling, deze overdracht bericht is verloren gegaan en Hallo client moet opnieuw verbinding maken, Hallo koppeling herstellen en probeer Hallo overdracht.

Als zodanig Service Bus en Event Hubs ondersteunen 'ten minste eenmaal' overdrachten waarbij Hallo afzender zeker van kunt zijn voor het Hallo-bericht is opgeslagen en geaccepteerd, maar bieden geen ondersteuning voor 'eenmalige' overdrachten op Hallo AMQP-niveau, waarbij Hallo-systeem toorecover probeert Hallo koppeling en toonegotiate Hallo levering status tooavoid duplicatie van de overdracht van Hallo-bericht door te gaan.

toocompensate voor mogelijke duplicaat verzendt, Service Bus biedt ondersteuning voor detectie van duplicaten als een optionele functie van wachtrijen en onderwerpen. Detectie van dubbele records Hallo bericht-id's van alle inkomende berichten tijdens een door de gebruiker gedefinieerde tijdvenster en vervolgens de achtergrond verwijdert die alle met berichten hetzelfde bericht-id's die dezelfde databaseprestaties Hallo.

### Datatransportbesturing

Bovendien toohello sessie-level datatransportbesturing model dat eerder is besproken, elke koppeling heeft een eigen stroom-model voor toegangsbeheer. Sessie-level datatransportbesturing beveiligt Hallo container opheft toohandle te veel frames aan zodra de link-level datatransportbesturing plaatst het Hallo-toepassing die verantwoordelijk is voor het aantal deze wil toohandle via een koppeling berichten en wanneer.

![][4]

Op een koppeling overdrachten kunnen alleen gebeuren wanneer de hello afzender heeft voldoende *koppelen tegoed*. Link-tegoed is een teller die is ingesteld door Hallo ontvanger met Hallo *stroom* performative, die is afgestemd tooa koppeling. Wanneer Hallo afzender link-tegoed toegewezen is, probeert deze toouse van die credit door het leveren van berichten. Elke message delivery verlaagt Hallo resterende link-tegoed met 1. Wanneer het Hallo-link-tegoed is gebruikt, niet meer leveringen.

Wanneer Service Bus in de rol van Hallo ontvanger, biedt het onmiddellijk Hallo afzender ruime link-tegoed, zodat berichten kunnen direct worden verzonden. Link-tegoed is gebruikt, Service Bus af en toe stuurt een *stroom* saldo performative toohello afzender tooupdate Hallo koppeling.

In de rol van de afzender hello verzendt Service Bus berichten toouse up tegoed openstaande koppeling.

Een aanroep van 'ontvangen' hello API-niveau wordt omgezet in een *stroom* performative verstuurd tooService Bus door Hallo-client en Service Bus verbruikt die eerst door Hallo duurt credit beschikbaar, het bericht uit de wachtrij hello, deze vergrendelen ontgrendeld en overdragen. Als er geen bericht direct beschikbaar is voor de levering van openstaande tegoed door een koppeling tot stand gebracht met dat bepaalde entiteit opgenomen in de volgorde van de aankomst blijft en berichten zijn vergrendeld en overgebracht als ze beschikbaar zijn, toouse openstaande tegoed.

Hallo-vergrendeling voor een bericht wordt opgeheven bij het Hallo-overdracht naar een van de terminal statussen Hallo afrekenen *geaccepteerd*, *afgewezen*, of *uitgebracht*. Hallo-bericht is verwijderd uit de Service Bus als Hallo definitieve status is *geaccepteerd*. Het blijft in Service Bus en volgende ontvanger toohello wordt geleverd als Hallo overdracht van Hallo andere statussen bereikt. Hallo-bericht verplaatst Service Bus automatisch naar een van de entiteit Hallo wachtrij voor onbestelbare berichten wanneer het Hallo levering van het maximum aantal toegestane voor Hallo entiteit vervaldatum toorepeated weigeringen of releases wordt bereikt.

Hoewel Hallo Service Bus-API's die een optie vandaag de dag niet rechtstreeks blootstellen, kunt een lager niveau AMQP-protocol client Hallo link-tegoed model tooturn Hallo 'pull-style' interactie van de uitgifte van één eenheid van het krediet voor elke aanvraag ontvangen in een model 'push-style' gebruiken door uitgifte van een groot aantal koppeling krediet en ontvangt berichten zodra deze beschikbaar zijn zonder verdere tussenkomst. Push wordt ondersteund door Hallo [MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount) of [MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount) eigenschapsinstellingen. Wanneer ze dan nul zijn, Hallo AMQP-client wordt gebruikt als Hallo link-tegoed.

In deze context begint de belangrijke toounderstand die klok voor verloop Hallo Hallo vergrendeling van het Hallo-bericht in de entiteit Hallo Hallo wanneer hello bericht is afkomstig uit Hallo-entiteit niet wanneer het Hallo-bericht wordt geplaatst op Hallo-kabel. Wanneer het Hallo-client geeft gereedheid tooreceive berichten aan door uitgifte van link-tegoed, het is daarom verwachte toobe actief opvragen berichten via Hallo netwerk en gereed toohandle worden ze. Anders mogelijk Hallo-bericht vergrendeling verlopen voordat het Hallo-bericht zelfs wordt geleverd. Hallo gebruik van link-tegoed datatransportbesturing moet rechtstreeks Hallo onmiddellijke gereedheid toodeal met beschikbare berichten verzonden toohello ontvanger overeenkomen.

Kortom, hello volgende secties bevatten een schematische overzicht van Hallo performative stroom tijdens verschillende API interacties. Elke sectie beschrijft een andere logische bewerking. Sommige van deze interacties zijn 'vertraagde,' wat betekent dat ze kunnen alleen worden uitgevoerd wanneer dat nodig. Maken de afzender van een bericht kan niet leiden tot een netwerk interactie totdat het eerste Hallo-bericht is verzonden of aangevraagd.

Hallo pijlen in de volgende tabel Hallo weergeven Hallo performative stroomrichting.

#### Bericht ontvanger maken

| Client | Service Bus |
| --- | --- |
| --> () koppelen<br/>naam = {naam van de koppeling}<br/>verwerken = {numerieke ingang}<br/>rol =**ontvanger**,<br/>bron = {entiteitnaam}<br/>doel = {client koppeling id}<br/>) |Client wordt tooentity als ontvanger |
| Service Bus-antwoorden die het einde van de koppeling Hallo koppelen |<--(koppelen<br/>naam = {naam van de koppeling}<br/>verwerken = {numerieke ingang}<br/>rol =**afzender**,<br/>bron = {entiteitnaam}<br/>doel = {client koppeling id}<br/>) |

#### Maken van de afzender

| Client | Service Bus |
| --- | --- |
| --> () koppelen<br/>naam = {naam van de koppeling}<br/>verwerken = {numerieke ingang}<br/>rol =**afzender**,<br/>bron = {client koppeling id}<br/>doel = {naam van de entiteit}<br/>) |Er is geen actie |
| Er is geen actie |<--(koppelen<br/>naam = {naam van de koppeling}<br/>verwerken = {numerieke ingang}<br/>rol =**ontvanger**,<br/>bron = {client koppeling id}<br/>doel = {naam van de entiteit}<br/>) |

#### Maken van de afzender van bericht (fout)

| Client | Service Bus |
| --- | --- |
| --> () koppelen<br/>naam = {naam van de koppeling}<br/>verwerken = {numerieke ingang}<br/>rol =**afzender**,<br/>bron = {client koppeling id}<br/>doel = {naam van de entiteit}<br/>) |Er is geen actie |
| Er is geen actie |<--(koppelen<br/>naam = {naam van de koppeling}<br/>verwerken = {numerieke ingang}<br/>rol =**ontvanger**,<br/>bron = null,<br/>doel = null<br/>)<br/><br/><--loskoppelen ()<br/>verwerken = {numerieke ingang}<br/>gesloten =**true**,<br/>Fout = {foutgegevens}<br/>) |

#### Afsluitbericht ontvanger/afzender

| Client | Service Bus |
| --- | --- |
| --> loskoppelen ()<br/>verwerken = {numerieke ingang}<br/>gesloten =**true**<br/>) |Er is geen actie |
| Er is geen actie |<--loskoppelen ()<br/>verwerken = {numerieke ingang}<br/>gesloten =**true**<br/>) |

#### Verzenden (geslaagd)

| Client | Service Bus |
| --- | --- |
| overdracht (--><br/>levering-id = {numerieke ingang}<br/>levering-tag = {binaire ingang}<br/>afgewikkeld =**false**,, meer =**false**,<br/>status =**null**,<br/>hervatten =**false**<br/>) |Er is geen actie |
| Er is geen actie |<--toestand (<br/>rol ontvanger =<br/>eerst = {levering van id}<br/>laatste = {levering van id}<br/>afgewikkeld =**true**,<br/>status =**geaccepteerd**<br/>) |

#### Verzonden (fout)

| Client | Service Bus |
| --- | --- |
| overdracht (--><br/>levering-id = {numerieke ingang}<br/>levering-tag = {binaire ingang}<br/>afgewikkeld =**false**,, meer =**false**,<br/>status =**null**,<br/>hervatten =**false**<br/>) |Er is geen actie |
| Er is geen actie |<--toestand (<br/>rol ontvanger =<br/>eerst = {levering van id}<br/>laatste = {levering van id}<br/>afgewikkeld =**true**,<br/>status =**afgewezen**()<br/>Fout = {foutgegevens}<br/>)<br/>) |

#### Ontvangen

| Client | Service Bus |
| --- | --- |
| stroom (--><br/>link-tegoed = 1<br/>) |Er is geen actie |
| Er is geen actie |< transfer ()<br/>levering-id = {numerieke ingang}<br/>levering-tag = {binaire ingang}<br/>afgewikkeld =**false**,<br/>meer =**false**,<br/>status =**null**,<br/>hervatten =**false**<br/>) |
| toestand (--><br/>rol =**ontvanger**,<br/>eerst = {levering van id}<br/>laatste = {levering van id}<br/>afgewikkeld =**true**,<br/>status =**geaccepteerd**<br/>) |Er is geen actie |

#### Met meerdere berichten ontvangen

| Client | Service Bus |
| --- | --- |
| stroom (--><br/>link-tegoed = 3<br/>) |Er is geen actie |
| Er is geen actie |< transfer ()<br/>levering-id = {numerieke ingang}<br/>levering-tag = {binaire ingang}<br/>afgewikkeld =**false**,<br/>meer =**false**,<br/>status =**null**,<br/>hervatten =**false**<br/>) |
| Er is geen actie |< transfer ()<br/>levering-id = {numerieke ingang + 1},<br/>levering-tag = {binaire ingang}<br/>afgewikkeld =**false**,<br/>meer =**false**,<br/>status =**null**,<br/>hervatten =**false**<br/>) |
| Er is geen actie |< transfer ()<br/>levering-id = {numerieke ingang + 2},<br/>levering-tag = {binaire ingang}<br/>afgewikkeld =**false**,<br/>meer =**false**,<br/>status =**null**,<br/>hervatten =**false**<br/>) |
| toestand (--><br/>rol ontvanger =<br/>eerst = {levering van id}<br/>laatste = {-id voor levering + 2}<br/>afgewikkeld =**true**,<br/>status =**geaccepteerd**<br/>) |Er is geen actie |

### Berichten

Hallo volgende secties wordt uitgelegd welke eigenschappen van Hallo standaard AMQP bericht secties worden gebruikt door de Service Bus en hoe deze toohello Service Bus-API set worden toegewezen.

#### koptekst

| Veldnaam | Gebruik | API-naam |
| --- | --- | --- |
| duurzame |- |- |
| Prioriteit |- |- |
| TTL |Voor dit bericht toolive tijd |[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| eerste verwerver |- |- |
| levering tellen |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### properties

| Veldnaam | Gebruik | API-naam |
| --- | --- | --- |
| bericht-id |ID voor dit bericht toepassingsspecifieke, vrije vorm. Gebruikt voor detectie van duplicaten. |[MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| gebruikers-id |Toepassingen gedefinieerde gebruiker-id, niet worden geïnterpreteerd door Service Bus. |Niet toegankelijk via Hallo Service Bus-API. |
| te|Bestemming toepassingen gedefinieerde id, niet worden geïnterpreteerd door Service Bus. |[Aan](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| Onderwerp |Bericht toepassingsspecifieke doel-id, niet worden geïnterpreteerd door Service Bus. |[Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| antwoord te|Antwoord-path toepassingsspecifieke indicator, niet worden geïnterpreteerd door Service Bus. |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| correlatie-id |Toepassingsspecifieke correlatie-id, niet worden geïnterpreteerd door Service Bus. |[CorrelationId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| type inhoud |Toepassingsspecifieke inhoudstype indicator voor het Hallo-instantie, niet worden geïnterpreteerd door Service Bus. |[ContentType](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| codering van inhoud |Toepassingsspecifieke indicator codering van inhoud voor het Hallo-instantie, niet worden geïnterpreteerd door Service Bus. |Niet toegankelijk via Hallo Service Bus-API. |
| absolute verlooptijdstip |Verklaart op welke absolute instant Hallo bericht is verlopen. Genegeerd op invoer (koptekst TTL is waargenomen), de gezaghebbende op uitvoer. |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| Aanmaaktijd |Verklaart op welk tijdstip Hallo bericht is gemaakt. Niet gebruikt door de Service Bus |Niet toegankelijk via Hallo Service Bus-API. |
| groep-id |Toepassingen gedefinieerde id voor een bijbehorende set berichten. Gebruikt voor Service Bus-sessies. |[Sessie-id](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| volgorde van de groep |De teller Hallo relatieve volgnummer van het Hallo-bericht in een sessie te identificeren. Door de Servicebus genegeerd. |Niet toegankelijk via Hallo Service Bus-API. |
| antwoord-naar-groep-id |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## Geavanceerde mogelijkheden voor Service Bus

Deze sectie bevat informatie over geavanceerde mogelijkheden van Azure Service Bus die zijn gebaseerd op concept extensies tooAMQP, ontwikkeling in Hallo OASIS technisch comité voor AMQP. Service Bus implementeert Hallo nieuwste versies van deze concepten en wijzigingen die zijn geïntroduceerd als deze concepten worden standaard status bereikt aanneemt.

> [!NOTE]
> Service Bus-berichtenservice geavanceerde bewerkingen worden ondersteund door middel van een aanvraag/antwoord-patroon. Hallo-details van deze bewerkingen worden beschreven in Hallo document [AMQP 1.0 in Service Bus: aanvraag-antwoord-bewerkingen](service-bus-amqp-request-response.md).
> 
> 

### AMQP-management

Hallo AMQP management specificatie is Hallo eerste Hallo concept extensies die hier worden besproken. Deze specificatie definieert een reeks protocol-gebaren gelaagd boven op Hallo AMQP-protocol waarmee beheerinteracties Hello messaging-infrastructuur via AMQP. Hallo-specificatie definieert algemene bewerkingen zoals *maken*, *lezen*, *bijwerken*, en *verwijderen* voor het beheren van entiteiten in een messaging-infrastructuur en een reeks querybewerkingen.

Alle deze gebaren vereisen een aanvraag/antwoord-interactie tussen Hallo-client en Hallo messaging-infrastructuur en daarom Hallo-specificatie definieert hoe toomodel die interactie patroon boven op AMQP: Hallo client verbinding maakt toohello messaging infrastructuur, initieert een sessie en maakt vervolgens een combinatie van koppelingen. Op één koppeling Hallo client fungeert als de afzender en op andere Hallo het fungeert als ontvanger, waardoor een paar koppelingen die als een bidirectioneel kanaal optreden kan.

| Logische-bewerking | Client | Service Bus |
| --- | --- | --- |
| Aanvraag antwoord pad maken |--> () koppelen<br/>naam = {*naam van de koppeling*},<br/>verwerken = {*numerieke ingang*},<br/>rol =**afzender**,<br/>bron =**null**,<br/>target = 'management myentity / $'<br/>) |Er is geen actie |
| Aanvraag antwoord pad maken |Er is geen actie |\<--(koppelen<br/>naam = {*naam van de koppeling*},<br/>verwerken = {*numerieke ingang*},<br/>rol =**ontvanger**,<br/>bron = null,<br/>TARGET = "myentity"<br/>) |
| Aanvraag antwoord pad maken |--> () koppelen<br/>naam = {*naam van de koppeling*},<br/>verwerken = {*numerieke ingang*},<br/>rol =**ontvanger**,<br/>bron = 'myentity / $management',<br/>target = 'id myclient$ '<br/>) | |
| Aanvraag antwoord pad maken |Er is geen actie |\<--(koppelen<br/>naam = {*naam van de koppeling*},<br/>verwerken = {*numerieke ingang*},<br/>rol =**afzender**,<br/>bron = "myentity"<br/>target = 'id myclient$ '<br/>) |

Met deze combinatie van koppelingen in plaats, Hallo aanvraag/antwoord-implementatie is eenvoudig: een verzoek is een bericht verzonden tooan entiteit binnen Hallo messaging-infrastructuur die werkt met dit patroon. In dat aanvraagbericht Hallo *antwoordadres* veld Hallo *eigenschappen* sectie toohello is ingesteld *doel* id voor koppeling naar welke antwoord toodeliver Hallo Hallo. Hallo-aanvraag wordt verwerkt door Hallo afhandeling van entiteit en levert Hallo antwoord via Hallo koppelen waarvan *doel* id komt overeen met de Hallo aangegeven *antwoordadres* id.

Hallo patroon is natuurlijk vereist dat Hallo client container en Hallo client gegenereerde id voor Hallo antwoord bestemming uniek voor alle clients en ook moeilijk toopredict uit veiligheidsoverwegingen zijn.

Hallo-berichtuitwisselingen gebruikt voor Hallo management-protocol en voor alle andere protocollen die gebruik Hallo hetzelfde patroon gebeuren op toepassingsniveau Hallo; ze geen nieuwe AMQP-protocolniveau gebaren gedefinieerd. Dat is opzettelijk, zodat toepassingen kunnen profiteren direct met de volgende extensies met compatibele AMQP 1.0-stacks.

Service Bus momenteel implementeert niet Hallo core functies van de management-specificatie hello, maar Hallo aanvraag/antwoord-patroon gedefinieerd door Hallo management specificatie fundamentele voor Hallo claims-beveiliging op basis van-functie en voor bijna alle is Hallo geavanceerde mogelijkheden besproken in Hallo uit te voeren.

### Claims gebaseerde verificatie

Hallo AMQP Claims-gebaseerde verificatie (CBS) specificatie concept bouwt voort op Hallo management specificatie aanvragen/reacties patroon en een beschrijving van een algemene model voor hoe toouse beveiligingstokens met AMQP federatieve.

Hallo standaard beveiligingsmodel van AMQP besproken in Hallo inleiding is gebaseerd op SASL en kan worden geïntegreerd met de handshake van verbinding AMQP Hallo. Met behulp van SASL heeft Hallo-voordeel die dit een uitbreidbare model waarvoor een reeks mechanismen zijn gedefinieerd biedt uit elk protocol dat voorheen op SASL leans kan profiteren. Deze mechanismen zijn 'PLATTE' voor de overdracht van gebruikersnamen en wachtwoorden, tooTLS beveiligingsniveau toobind 'Extern', 'Anoniem' tooexpress Hallo afwezigheid van expliciete verificatie/autorisatie en tal van aanvullende mechanismen waarmee het doorgeven van referenties voor verificatie en/of de autorisatie of -tokens.

De AMQP SASL integratie heeft twee nadelen:

* Alle referenties en tokens zijn binnen het bereik toohello verbinding. Messaging-infrastructuur kunt tooprovide differentiated toegangsbeheer op basis van het per entiteit; bijvoorbeeld, zodat Hallo bearer van een token toosend tooqueue A, maar niet tooqueue B. Met Hallo autorisatiecontext verankerd op Hallo verbinding is niet mogelijk toouse één verbinding is, en nog andere toegangstokens voor wachtrij A en B. wachtrij gebruiken
* Toegangstokens zijn doorgaans alleen geldig voor een beperkte periode. Deze geldigheid Hallo tooperiodically opnieuw ophalen gebruikerstokens vereist en biedt een kans toohello uitgever beveiligingstoken toorefuse uitgeven van een nieuw token als van de gebruiker van het Hallo-machtigingen zijn gewijzigd. AMQP verbindingen mogelijk langere tijd duren. Hallo SASL model biedt alleen een tooset kans op een token tijdens de verbinding, wat betekent dat berichteninfrastructuur ofwel Hallo toodisconnect Hallo client heeft wanneer Hallo-token is verlopen of moet worden tooaccept Hallo risico toestaan blijvende communicatie met een client die is toegangsrechten is ingetrokken in Hallo tussentijdse.

Hallo-specificatie AMQP CBS geïmplementeerd door de Service Bus, kunt u een elegante tijdelijke oplossing voor beide die problemen: kunt u een client tooassociate toegangstokens met elk knooppunt en tooupdate die tokens voordat ze verlopen, zonder dat de berichtenstroom Hallo worden onderbroken.

CBS definieert een virtuele management-knooppunt, met de naam *$cbs*, toobe geleverd door Hallo messaging-infrastructuur. Hallo knooppunt accepteert tokens namens een andere knooppunten in Hallo messaging-infrastructuur.

Hallo protocol gebaar is een aanvraag/antwoord-uitwisseling zoals gedefinieerd door Hallo management-specificatie. Dat betekent dat de client Hallo stelt een combinatie van koppelingen Hello *$cbs* knooppunt en vervolgens geeft een aanvraag op Hallo uitgaande koppeling en wacht op antwoord Hallo op Hallo inkomende koppeling.

Hallo-bericht van aanvraag heeft Hallo toepassingseigenschappen te volgen:

| Sleutel | Optioneel | Waardetype | De inhoud |
| --- | --- | --- | --- |
| bewerking |Nee |Tekenreeks |**Put-token** |
| type |Nee |Tekenreeks |Hallo type Hallo-token wordt geplaatst. |
| naam |Nee |Tekenreeks |Hallo 'doelgroep' toowhich Hallo token is van toepassing. |
| vervaldatum |Ja |tijdstempel |Het verlooptijdstip Hallo Hallo-token. |

Hallo *naam* eigenschap identificeert Hallo entiteit aan welke Hallo token gekoppeld worden moet. In de Service Bus de Hallo pad toohello wachtrij of onderwerp/abonnement. Hallo *type* eigenschap identificeert Hallo tokentype:

| Type token | Beschrijving van token | Hoofdtekst van Type | Opmerkingen |
| --- | --- | --- | --- |
| amqp:jwt |JSON Web Token (JWT) |AMQP-waarde (tekenreeks) |Nog niet beschikbaar. |
| amqp:SWT |Eenvoudige Web Token (SWT) |AMQP-waarde (tekenreeks) |Alleen ondersteund voor SWT tokens die zijn uitgegeven door AAD/ACS |
| servicebus.Windows.NET:sastoken |Service Bus SAS-Token |AMQP-waarde (tekenreeks) |- |

Tokens verleent rechten. Service Bus op de hoogte van de drie fundamentele rechten: 'Verzenden' kunnen worden verzonden, 'Luisteren' kunt ontvangen en manipuleren entiteiten 'Beheren' maakt. Deze rechten bevatten SWT tokens die zijn uitgegeven door AAD/ACS expliciet als claims. Service Bus SAS-tokens Raadpleeg toorules geconfigureerd op het Hallo-naamruimte of entiteit en deze regels zijn geconfigureerd met rechten. Hallo ondertekeningstoken met Hallo-sleutel die is gekoppeld aan deze regel wordt dus Hallo token snelle Hallo respectieve rechten. Hallo-token die is gekoppeld aan een entiteit met *put-token* kunnen inhoud Hallo verbonden client toointeract met Hallo entiteit per Hallo token rechten. Een koppeling waar Hallo client op Hallo plaatsvindt *afzender* rol is vereist 'Verzenden' hello rechts; op Hallo *ontvanger* rol Hallo 'Luisteren' rechts vereist.

Hallo antwoordbericht heeft Hallo *eigenschappen van application* waarden

| Sleutel | Optioneel | Waardetype | De inhoud |
| --- | --- | --- | --- |
| statuscode in |Nee |int |HTTP-antwoordcode **[RFC2616]**. |
| Beschrijving van status |Ja |Tekenreeks |Beschrijving van status Hallo. |

Hallo-client kunt aanroepen *put-token* herhaaldelijk en voor elke entiteit in Hallo messaging-infrastructuur. Hallo tokens zijn binnen het bereik toohello huidige client en verankerd op de huidige verbinding hello, betekenis Hallo server vallen tot terugkerende tokens wanneer Hallo verbinding uitvalt.

Hallo huidige Service Bus-implementatie kan alleen CBS in combinatie met Hallo SASL-methode 'Anoniem'. SSL/TLS-verbinding moet altijd voorafgaande toohello SASL handshake bestaan.

Hallo anonieme mechanisme moet daarom worden ondersteund door Hallo gekozen AMQP 1.0-client. Anonieme toegang betekent dat de handshake van de eerste verbinding, zoals het maken van de eerste sessie Hallo Hallo gebeurt zonder Service Bus weten wie Hallo verbinding wordt gemaakt.

Zodra het Hallo-verbinding en sessie tot stand is gebracht, Hallo koppelen toohello koppelingen *$cbs* knooppunt en het verzenden van Hallo *put-token* aanvraag Hallo zijn alleen toegestaan bewerkingen. Een geldig token moet worden ingesteld met een *put-token* aanvraag voor een bepaald knooppunt entiteit binnen 20 seconden nadat het Hallo-verbinding tot stand is gebracht, anders Hallo verbinding wordt eenzijdig verbroken door Service Bus.

Hallo-client is vervolgens verantwoordelijk voor het bijhouden van verlopen van het token. Wanneer een token is verlopen, verwijderd Service Bus alle koppelingen onmiddellijk op Hallo verbinding toohello respectieve entiteit. tooprevent deze, Hallo client Hallo token voor Hallo knooppunt kunt vervangen door een nieuwe op elk gewenst moment via virtuele Hallo *$cbs* knooppunt met dezelfde Hallo *put-token* gebaar en zonder opvragen in Hallo manier van Hallo nettolading van het verkeer dat overdrachten op verschillende koppelingen.

## Volgende stappen

toolearn meer informatie over AMQP, gaat u naar Hallo koppelingen te volgen:

* [Service Bus AMQP-overzicht]
* [AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd]
* [AMQP in WindowsServer-Servicebus]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[Service Bus AMQP-overzicht]: service-bus-amqp-overview.md
[AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP in WindowsServer-Servicebus]: https://msdn.microsoft.com/library/dn574799.aspx
