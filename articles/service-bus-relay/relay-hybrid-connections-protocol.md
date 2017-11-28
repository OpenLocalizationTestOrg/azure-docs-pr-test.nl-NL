---
title: aaaAzure Relay hybride verbindingen protocol handleiding | Microsoft Docs
description: Handleiding voor Azure Relay hybride verbindingen-protocol.
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Protocol voor Azure Relay hybride verbindingen
Azure Relay is een Hallo sleutel mogelijkheid stijlen van hello Azure Service Bus-platform. Hallo nieuwe *hybride verbindingen* mogelijkheid relay is een op basis van HTTP- en WebSockets evolutie van beveiligde, open-protocol. Hallo voormalige, evenredig met de naam die hij vervangt *BizTalk Services* functie die is gebaseerd op een eigen protocol foundation. Hallo-integratie van hybride verbindingen in Azure App Services blijft toofunction als-is.

Hybride verbindingen kunnen in twee richtingen, binaire gegevensstroom communicatie tussen twee netwerktoepassingen waarover een of beide partijen kunnen zich achter een NAT's en firewalls. Dit artikel wordt beschreven Hallo clientzijde interacties met Hallo hybride verbindingen relay voor het verbinden van clients in listener en functies van de afzender en hoe listeners nieuwe verbindingen accepteren.

## Interactie model
Hallo hybride verbindingen relay verbindt twee partijen door een punt rendezvous in hello Azure-cloud die zowel partijen kunnen detecteren en verbinding maken toofrom van hun eigen netwerk perspectief te bieden. Dat punt rendezvous heet 'Hybride verbinding' in dit document en andere documentatie in Hallo API's, en ook in hello Azure-portal. Hallo verwezen hybride verbindingen, service-eindpunt is tooas Hallo 'service' hello rest van dit artikel. Hallo interactie model leans op naamgeving volgt de namen Hallo tot stand gebracht door veel andere netwerk-API's.

Er is een listener die eerst duidt gereedheid toohandle binnenkomende verbindingen en vervolgens accepteert naarmate ze binnenkomen. Hallo op de andere kant, er is een client die verbinding maakt die verbinding naar Hallo listener maakt, verwacht dat connection toobe geaccepteerd voor een pad bidirectionele communicatie tot stand brengen.
"Connect," 'Luisteren,' en 'Accepteren' zijn Hallo dezelfde voorwaarden u in de meeste vindt socket API's.

Een communicatiemodel relayed heeft beide partijen maken van uitgaande verbindingen naar een service-eindpunt dat maakt Hallo 'listener' ook een 'client' gewone gebruikt, en mogelijk ook andere terminologie overloads. Hallo nauwkeurig terminologie die wij daarom voor hybride verbindingen gebruiken is als volgt:

Hallo-programma's aan beide zijden van een verbinding worden 'clients,' genoemd, omdat ze clients toohello service. Hallo deze-client die wordt gewacht en aanvaardt verbindingen is het 'listener' of is toobe in Hallo 'listener rol.' Hallo-client die een nieuwe verbinding naar een listener via Hallo service start Hallo 'afzender' wordt genoemd, of bevindt zich in de 'afzender rol'.

### Listener-interacties
Hallo-listener heeft vier interacties met Hallo service; alle gegevens van de kabel worden verderop in dit artikel in Hallo verwijzing sectie beschreven.

#### Luisteren
gereedheid tooindicate toohello-service dat een listener gereed tooaccept verbindingen is, wordt gemaakt een uitgaande WebSocket-verbinding. handshake van verbinding Hallo voert Hallo-naam van een hybride verbinding geconfigureerd op Hallo Relay-naamruimte en een beveiligingstoken dat Hallo 'Luisteren' recht verleent deze naam.
Wanneer Hallo WebSocket wordt geaccepteerd door de service hello, Hallo-registratie is voltooid en Hallo tot stand gebracht web die websocket in stand, als Hallo 'besturingskanaal gehouden is' voor het inschakelen van alle opeenvolgende interacties. Hallo-service kunnen up too25 gelijktijdige listeners op een hybride verbinding. Als er twee of meer actieve listeners, worden binnenkomende verbindingen verdeeld zijn over ze in willekeurige volgorde; evenredige verdeling kan niet worden gegarandeerd.

#### Accepteren
Wanneer een afzender opent een nieuwe verbinding op Hallo-service, service Hallo kiest en waarschuwt een van de actieve listeners Hallo op Hallo hybride verbinding. Deze melding wordt toohello-listener verzonden via Hallo open besturingskanaal als een JSON-bericht met Hallo-URL van Hallo WebSocket-eindpunt dat Hallo listener moet verbinding maken toofor Hallo verbinding accepteren.

Hallo-URL kan en moet rechtstreeks worden gebruikt door de listener Hallo zonder extra werk.
Hallo gecodeerde gegevens zijn alleen is geldig voor een korte periode, hoofdzakelijk voor zo lang als de afzender Hallo bereid toowait voor Hallo verbinding tot stand gebracht toobe end-to-end, maar up tooa maximaal 30 seconden. Hallo-URL kan alleen worden gebruikt voor een geslaagde verbindingspoging. Zo spoedig Hallo WebSocket-verbinding met de Hallo rendezvous die URL tot stand is gebracht, alle verdere activiteiten op dit WebSocket is doorgegeven van en toohello afzender, zonder tussenkomst van de of interpretatie door Hallo-service.

#### Verlengen
Hallo-beveiligingstoken die moet worden gebruikt tooregister Hallo-listener en onderhouden van dat het besturingskanaal mogelijk verloopt terwijl Hallo listener actief is. Hallo toegangstoken heeft geen invloed op actieve verbindingen, maar dit leidt tot Hallo besturingselement kanaal toobe verwijderd door het Hallo-service op of kort na de verloopdatum Hallo moment. Hallo 'vernieuwen'-bewerking is een JSON-bericht dat Hallo listener tooreplace Hallo token die is gekoppeld aan het besturingskanaal hello, kunt verzenden zodat hello besturingskanaal kan worden beheerd gedurende langere perioden.

#### Ping
Als besturingskanaal Hallo inactief gedurende een lange periode, schakels op Hallo manier blijft, zoals load kunnen balancers of NAT's uitvallen Hallo TCP-verbinding. Hallo 'pingen' bewerking voorkomt dat door het verzenden van een kleine hoeveelheid gegevens op Hallo-kanaal dat iedereen op Hallo netwerkroute eraan herinnert dat connection Hallo is bedoeld als toobe actief is en deze fungeert ook als een 'live' test voor Hallo listener. Hallo pingen mislukt, Hallo besturingskanaal moet worden beschouwd als onbruikbaar als Hallo listener moet opnieuw worden verbonden.

### Interactie van de afzender
Hallo afzender heeft slechts één interactie met Hallo-service: deze verbinding maakt.

#### Verbinding maken
Hallo "connect"-bewerking wordt een beveiligingstoken dat de machtiging 'Verzenden' in de queryreeks Hallo geopend WebSocket op Hallo-service, verstrekken Hallo-naam van hybride verbinding Hallo en (optioneel, maar vereist standaard). Hallo-service communiceert vervolgens met Hallo-listener in Hallo zoals eerder beschreven en Hallo listener maakt een rendezvous-verbinding die wordt samengevoegd met dit WebSocket. Nadat Hallo WebSocket is geaccepteerd, worden alle verdere interacties op die WebSocket met een verbonden listener.

### Interactie van de samenvatting
Hallo-resultaat van dit model interactie is dat die Hallo afzender-client wordt geleverd buiten de handshake met een 'schone' WebSocket, die is verbonden tooa listener en dat er geen verdere preambles of voorbereiding moet. Dit model kunt vrijwel alle bestaande WebSocket-client implementatie tooreadily profiteren van de Hallo hybride verbindingen service door het opgeven van een URL juist samengesteld in hun laag WebSocket-client.

Hallo rendezvous verbinding WebSocket die listener Hallo via de interactie accepteren verkrijgt ook schoon is en kan worden verstrekt tooany bestaande WebSocket-serverimplementatie met een minimale extra abstractie die wordt onderscheid tussen 'accepteren gemaakt' bewerkingen op het lokale netwerk listeners en de hybride verbindingen externe hun framework accepteren' ' bewerkingen.

## Naslaginformatie over het protocol

Deze sectie beschrijft de details op Hallo van Hallo protocol interacties die eerder zijn beschreven.

Alle WebSocket-verbindingen worden uitgevoerd op poort 443 als een upgrade vanaf HTTPS 1.1, die meestal wordt gescheiden door een aantal WebSocket-framework of API. Hier de beschrijving wordt opgeslagen implementatie neutrale, zonder dat een specifiek framework voorstellen.

### Listener-protocol
Hallo-listener protocol bestaat uit twee verbinding gebaren en drie berichtbewerkingen.

#### Listener-kanaal controleverbinding
Hallo-besturingskanaal wordt geopend met het maken van een WebSocket-verbinding met:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

Hallo `namespace-address` Hallo volledig gekwalificeerde domeinnaam van hello Azure Relay naamruimte dat hosts hybride verbinding doorgaans van Hallo formulier Hallo `{myname}.servicebus.windows.net`.

tekenreeks Hallo-parameter queryopties zijn als volgt.

| Parameter | Vereist | Beschrijving |
| --- | --- | --- |
| `sb-hc-action` |Ja |Voor Hallo listener rol Hallo parameter moet **sb-CH-action = luisteren** |
| `{path}` |Ja |Hallo URL-codering naamruimtepad Hallo van de vooraf geconfigureerde hybride verbinding tooregister deze listener op. Deze expressie wordt toegevoegde toohello vaste `$hc/` padgedeelte te hebben. |
| `sb-hc-token` |Ja\* |Hallo listener moet voorzien in een geldige, door de URL-codering Service Bus Shared Access Token Hallo naamruimte of hybride verbinding die Hallo verleent **luisteren** rechts. |
| `sb-hc-id` |Nee |Deze client opgegeven optionele ID kunt diagnostische tracering end-to-end. |

Als Hallo WebSocket-verbinding is mislukt vanwege toohello hybride verbinding pad niet wordt geregistreerd, of een ongeldige of ontbrekende token of een andere fout, wordt de Hallo fout feedback gegeven met Hallo reguliere HTTP 1.1-status feedback model. De beschrijving van status bevat een fout tracerings-id die kan worden doorgegeven aan Azure ondersteuningspersoneel:

| Code | Fout | Beschrijving |
| --- | --- | --- |
| 404 |Niet gevonden |Hallo hybride verbinding pad is ongeldig of Hallo basis-URL heeft onjuiste indeling. |
| 401 |Niet geautoriseerd |Hallo-beveiligingstoken is ontbreken of onjuist gevormd of ongeldig. |
| 403 |Is niet toegestaan |Hallo-beveiligingstoken is niet geldig voor dit pad voor deze actie. |
| 500 |Interne fout |Er is een fout in Hallo-service. |

Als Hallo WebSocket-verbinding opzettelijk door Hallo service afgesloten wordt nadat deze is in eerste instantie hebt ingesteld, Hallo reden voor dit wel doet wordt gecommuniceerd met behulp van een juiste WebSocket-protocol foutcode samen met een beschijvend foutbericht die ook een bijhouden -ID. Hallo-service wordt niet afgesloten het besturingskanaal zonder dat er een fout opgetreden. Geldige afsluiting is de client worden beheerd.

| WS-Status | Beschrijving |
| --- | --- |
| 1001 |Hallo hybride verbinding pad is verwijderd of uitgeschakeld. |
| 1008 |Hello security token is verlopen, daarom Hallo verificatiebeleid wordt geschonden. |
| 1011 |Er is een fout in Hallo-service. |

### Handshake accepteren
Hallo 'accepteren' melding wordt verzonden door Hallo service toohello listener via de eerder vastgestelde besturingskanaal als een JSON-bericht in een WebSocket frame. Er is geen antwoordbericht toothis.

Hallo-bericht bevat een JSON-object met de naam 'accepteren' definieert de volgende eigenschappen op dit moment Hallo:

* **adres** – Hallo URL tekenreeks toobe gebruikt voor het Hallo WebSocket toothe service tooaccept een binnenkomende verbinding tot stand brengen.
* **id** – Hallo unieke id voor deze verbinding. Als Hallo-ID is opgegeven door de afzender-client Hallo Hallo afzender opgegeven waarde is, anders het systeem gegenereerde waarde is.
* **connectHeaders** – alle HTTP-headers die zijn opgegeven toohello Relay eindpunt van de afzender hello, waaronder ook Hallo Sec-WebSocket-Protocol en de seconde-WebSocket-extensies headers.

#### Bericht accepteren

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

Hallo adres URL opgegeven in Hallo JSON bericht wordt gebruikt door de listener Hallo tot stand brengen hello WebSocket voor goedkeuren of weigeren Hallo afzender socket.

#### Acceptatie van Hallo socket
tooaccept, Hallo listener stelt toohello opgegeven adres van een WebSocket-verbinding.

Als Hallo 'accepteren' bericht uitvoert een `Sec-WebSocket-Protocol` koptekst wordt verwacht dat Hallo-listener accepteert alleen Hallo WebSocket als het protocol ondersteunt. Bovendien wordt het Hallo-header ingesteld als Hallo die websocket tot stand is gebracht.

Hallo geldt toohello `Sec-WebSocket-Extensions` header. Als Hallo framework een extensie ondersteunt, moet het Hallo-header toohello serverzijde antwoord Hallo vereist ingesteld `Sec-WebSocket-Extensions` handshake voor Hallo-extensie.

Hallo-URL moet worden gebruikt als-is voor het tot stand brengen van Hallo socket accepteren, maar bevat de volgende parameters:

| Parameter | Vereist | Beschrijving |
| --- | --- | --- |
| `sb-hc-action` |Ja |Voor het accepteren van een socket moet Hallo-parameter`sb-hc-action=accept` |
| `{path}` |Ja |(Zie volgende alinea Hallo) |
| `sb-hc-id` |Nee |Zie vorige beschrijving van **id**. |

`{path}`is Hallo URL-codering naamruimtepad Hallo vooraf geconfigureerde hybride verbinding op welke tooregister deze listener. Deze expressie wordt toegevoegde toothe vaste `$hc/` padgedeelte te hebben. 

Hallo `path` expressie kan worden uitgebreid met een achtervoegsel en een query-tekenreeksexpressie die volgt op de geregistreerde naam Hallo na een bijbehorende slash. Hierdoor Hallo afzender client toopass dispatch argumenten toohello overnemende listener wanneer het is niet mogelijk tooinclude HTTP-headers. Hallo verwachting is dat Hallo-listener framework parseert Hallo vaste padgedeelte te hebben en Hallo geregistreerde naam van het pad en rest hello, mogelijk maakt zonder query-tekenreeksargumenten voorafgegaan door `sb-`, beschikbare toohello-toepassing voor Gebruik of tooaccept Hallo verbinding.

Zie de volgende sectie "Afzender Protocol" Hallo voor meer informatie.

Als er een fout is, kan Hallo service als volgt beantwoorden:

| Code | Fout | Beschrijving |
| --- | --- | --- |
| 403 |Is niet toegestaan |Hallo-URL is niet geldig. |
| 500 |Interne fout |Er is een fout in Hallo-service |

Hallo-verbinding tot stand is gebracht, Hallo server afgesloten nadat Hallo WebSocket wanneer Hallo afzender WebSocket wordt afgesloten omlaag of Hello status te volgen:

| WS-Status | Beschrijving |
| --- | --- |
| 1001 |Hallo afzender client wordt afgesloten Hallo-verbinding. |
| 1001 |Hallo hybride verbinding pad is verwijderd of uitgeschakeld. |
| 1008 |Hello security token is verlopen, daarom Hallo verificatiebeleid wordt geschonden. |
| 1011 |Er is een fout in Hallo-service. |

#### Hallo socket weigeren
Hallo socket weigert nadat inspecteren Hallo 'accepteren'-bericht een vergelijkbare handshake moet zodat hello statuscode en de beschrijving van status van de reden voor afwijzing Hallo kan stromen communiceren toohello afzender.

Hallo protocol ontwerpkeuze hier is toouse een WebSocket-handshake (dat wil zeggen ontworpen tooend een gedefinieerde foutstatus) zodat listener clientimplementaties toorely op een WebSocket-client kunnen worden voortgezet en niet hoeft te gebruiken van een extra, bare HTTP-client.

tooreject hello socket, Hallo client neemt Hallo adres-URI van het 'accepteren' Hallo-bericht en voegt twee query-tekenreeks parameters tooit, als volgt:

| Param | Vereist | Beschrijving |
| --- | --- | --- |
| statusCode |Ja |Numerieke HTTP-statuscode. |
| StatusDescription |Ja |Menselijke leesbare reden voor Hallo afwijzing. |

vervolgens wordt de resulterende URI Hallo tooestablish WebSocket-verbinding gebruikt.

Wanneer correct is voltooid, wordt deze handshake opzettelijk mislukt met een HTTP-foutcode 410, omdat er geen WebSocket is ingesteld. Als er iets mis gaat beschrijven Hallo codes na Hallo-fout:

| Code | Fout | Beschrijving |
| --- | --- | --- |
| 403 |Is niet toegestaan |Hallo-URL is niet geldig. |
| 500 |Interne fout |Er is een fout in Hallo-service. |

### Vernieuwing van het token listener
Wanneer het Hallo-listener-token is over tooexpire, vervang deze deze door te sturen tekst frame toohello berichtenservice via besturingskanaal Hallo tot stand gebracht. Het bericht bevat een JSON-object aangeroepen `renewToken`, definieert een eigenschap te volgen op dit moment Hallo:

* **token** – een geldige, door de URL-codering Service Bus gedeeld toegangstoken voor de naamruimte of hybride verbinding die Hallo verleent **luisteren** rechts.

#### renewToken bericht

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

Als Hallo token validatie mislukt, de toegang is geweigerd en Hallo cloudservice gesloten Hallo besturingskanaal WebSocket met een fout. Anders is geen antwoord ontvangen.

| WS-Status | Beschrijving |
| --- | --- |
| 1008 |Hello security token is verlopen, daarom Hallo verificatiebeleid wordt geschonden. |

## Afzender-protocol
Hallo afzender-protocol is effectief identieke toohello manier die een listener tot stand is gebracht.
Hallo-doel is de maximale transparantie voor Hallo end-to-end WebSocket. Hallo-adres voor de verbinding toois Hallo die hetzelfde als die voor de listener hello, maar Hallo "action" verschilt en het token moet een andere machtiging:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

Hallo *naamruimte adres* Hallo volledig gekwalificeerde domeinnaam van hello Azure Relay naamruimte dat hosts hybride verbinding doorgaans van Hallo formulier Hallo `{myname}.servicebus.windows.net`.

Hallo-aanvraag kan willekeurige extra HTTP-headers, met inbegrip van de toepassing gedefinieerde waarden bevatten. Alle headers stroom toohello listener geleverd en kunnen worden gevonden op Hallo `connectHeader` object Hallo **accepteren** bericht besturingselement.

tekenreeks Hallo-parameter queryopties zijn als volgt:

| Param | Vereist? | Beschrijving |
| --- | --- | --- |
| `sb-hc-action` |Ja |Voor de rol van de afzender hello, Hallo-parameter moet `action=connect`. |
| `{path}` |Ja |(Zie volgende alinea Hallo) |
| `sb-hc-token` |Ja\* |Hallo listener moet voorzien in een geldige, door de URL-codering Service Bus Shared Access Token Hallo naamruimte of hybride verbinding die Hallo verleent **verzenden** rechts. |
| `sb-hc-id` |Nee |Een optionele ID die end-to-end-diagnostische tracering en beschikbaar toohello listener is gemaakt tijdens het Hallo handshake accepteren. |

Hallo `{path}` is Hallo URL-codering naamruimtepad Hallo vooraf geconfigureerde hybride verbinding op welke tooregister deze listener. Hallo `path` expressie met een achtervoegsel en een query-tekenreeks expressie toocommunicate verder kan worden uitgebreid. Als Hallo hybride verbinding is geregistreerd onder Hallo pad `hyco`, Hallo `path` expressie kan worden `hyco/suffix?param=value&...` gevolgd door Hallo queryreeksparameters die hier zijn gedefinieerd. Een volledige expressie kan vervolgens als volgt zijn:

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

Hallo `path` expressie toohello-listener in Hallo adres-URI die zijn opgenomen in de besturingselement-bericht met 'accepteren' hello wordt doorgegeven.

Als Hallo WebSocket-verbinding is mislukt vanwege toohello hybride verbinding pad niet wordt geregistreerd, een ongeldige of ontbrekende token of een andere fout, wordt de Hallo fout feedback gegeven met Hallo reguliere HTTP 1.1-status feedback model. De beschrijving van status bevat een fout tracerings-ID die kan worden gecommuniceerd naar Azure ondersteuningspersoneel:

| Code | Fout | Beschrijving |
| --- | --- | --- |
| 404 |Niet gevonden |Hallo hybride verbinding pad is ongeldig of Hallo basis-URL heeft onjuiste indeling. |
| 401 |Niet geautoriseerd |Hallo-beveiligingstoken is ontbreken of onjuist gevormd of ongeldig. |
| 403 |Is niet toegestaan |Hallo beveiligingstoken is niet geldig voor dit pad en voor deze actie. |
| 500 |Interne fout |Er is een fout in Hallo-service. |

Als Hallo WebSocket-verbinding opzettelijk door Hallo service afsluit is nadat deze is in eerste instantie ingesteld, Hallo reden hiervoor dus er wordt gecommuniceerd met behulp van een juiste WebSocket-protocol foutcode samen met een beschijvend foutbericht die ook een tracerings-ID.

| WS-Status | Beschrijving |
| --- | --- |
| 1000 |Hallo-listener is afgesloten van Hallo socket. |
| 1001 |Hallo hybride verbinding pad is verwijderd of uitgeschakeld. |
| 1008 |Hello security token is verlopen, daarom Hallo verificatiebeleid wordt geschonden. |
| 1011 |Er is een fout in Hallo-service. |

## Volgende stappen
* [Veelgestelde vragen over Relay](relay-faq.md)
* [Een naamruimte maken](relay-create-namespace-portal.md)
* [Aan de slag met .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Aan de slag met knooppunten](relay-hybrid-connections-node-get-started.md)

