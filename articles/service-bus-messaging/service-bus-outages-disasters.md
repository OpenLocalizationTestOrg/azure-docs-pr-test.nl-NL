---
title: Azure Service Bus-toepassingen aaaInsulating tegen storingen en noodsituaties | Microsoft Docs
description: Hierin wordt beschreven technieken die u kunt toepassingen tooprotect tegen een mogelijke onderbreking van de Service Bus gebruiken.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>Aanbevolen procedures voor de isolatie van toepassingen tegen storingen van de Service Bus en noodsituaties
Bedrijfskritieke toepassingen moeten continu, zelfs in Hallo aanwezigheid van niet-geplande storingen of noodsituaties werken. Dit onderwerp wordt beschreven technieken kunt u tooprotect Service Bus-toepassingen op basis van een mogelijke onderbreking van deze service of na noodgevallen.

Een storing wordt gedefinieerd als Hallo tijdelijke onbeschikbaarheid van Azure Service Bus. Hallo storing, kan sommige onderdelen van Service Bus, zoals een berichten-store of zelfs Hallo gehele datacenter beïnvloeden. Nadat het Hallo-probleem is verholpen, weer Service Bus beschikbaar is. Normaal gesproken veroorzaakt een storing geen verlies van berichten of andere gegevens. Een voorbeeld van een onderdeelfout is Hallo ontbreken van een bepaalde berichten-store. Een voorbeeld van een onderbreking van de hele datacenter is een stroomstoring van Hallo datacenter of een netwerkswitch defecte datacenter. Een storing kan de laatste van een paar minuten tooa paar dagen.

Een noodgeval wordt gedefinieerd als Hallo permanent verlies van een Service Bus-schaaleenheid of datacenter. Hallo datacenter kan of kan niet weer beschikbaar. Doorgaans verloren een noodgeval enkele of alle berichten of andere gegevens. Voorbeelden van noodsituaties zijn gestart, die het overspoelen of aardbeving.

## <a name="current-architecture"></a>Huidige architectuur
Service Bus maakt gebruik van meerdere messaging winkels toostore-berichten dat tooqueues of onderwerpen worden verzonden. Een niet-gepartitioneerde wachtrij of onderwerp toegewezen tooone messaging-store. Als deze berichten-store niet beschikbaar is, mislukt de alle bewerkingen voor de wachtrij of onderwerp.

Alle Service Bus messaging-entiteiten (wachtrijen, onderwerpen, relays) zich bevinden in een service-naamruimte die is gekoppeld aan een datacenter. Service Bus kunnen niet automatisch geo-replicatie van gegevens, noch het staat een naamruimte toospan meerdere datacenters.

## <a name="protecting-against-acs-outages"></a>Bescherming tegen storingen van ACS
Als u van referenties voor ACS gebruikmaakt en ACS niet meer beschikbaar is, kunnen clients niet langer tokens verkrijgen. Clients die een token hebt gelijktijdig Hallo die ACS uitvalt kunnen toouse Service Bus blijven totdat Hallo tokens verlopen. token standaardlevensduur Hallo is drie uur.

tooprotect tegen storingen is ACS gebruikt Shared Access Signature (SAS)-tokens. In dit geval verifieert Hallo client rechtstreeks met Service Bus met een zelf minted token-ondertekening met een geheime sleutel. Aanroepen tooACS zijn niet langer vereist. Zie voor meer informatie over SAS-tokens [Service Bus verificatie][Service Bus authentication].

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>Beveiligen van wachtrijen en onderwerpen tegen storingen store messaging
Een niet-gepartitioneerde wachtrij of onderwerp toegewezen tooone messaging-store. Als deze berichten-store niet beschikbaar is, mislukt de alle bewerkingen voor de wachtrij of onderwerp. Een wachtrij op Hallo daarentegen gepartitioneerd, bestaat uit meerdere fragmenten. Elke fragment wordt opgeslagen in een andere berichten-store. Wanneer een bericht wordt verzonden tooa gepartitioneerde wachtrij of onderwerp, toegewezen Service Bus Hallo-bericht tooone van Hallo fragmenten. Hallo bijbehorende berichten-store niet beschikbaar is, Service Bus schrijft Hallo-bericht tooa verschillende fragment, indien mogelijk. Zie voor meer informatie over gepartitioneerde entiteiten [gepartitioneerde berichtentiteiten][Partitioned messaging entities].

## <a name="protecting-against-datacenter-outages-or-disasters"></a>Bescherming tegen storingen van datacenter of rampen
tooallow voor een failover tussen twee datacentra, kunt u een Service Bus-Servicenaamruimte maken in elk datacenter. Bijvoorbeeld, Hallo Service Bus-Servicenaamruimte **contosoPrimary.servicebus.windows.net** zich mogelijk in de regio van de Verenigde Staten Noord/centraal hello, en **contosoSecondary.servicebus.windows.net**zich mogelijk in Hallo ons Zuid/centraal regio. Als een Service Bus-berichtenservice entiteit blijven toegankelijk in Hallo aanwezigheid van een storing in datacenter zijn moet, kunt u die entiteit maken in beide naamruimten.

Zie voor meer informatie, Hallo '-fout van Servicebus binnen een Azure-datacenter in sectie [asynchrone messaging-patronen en hoge beschikbaarheid][Asynchronous messaging patterns and high availability].

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>Beveiligen van eindpunten relay tegen storingen van datacenter of rampen
Geo-replicatie van de relay-eindpunten kan een service waarmee een bereikbaar in Hallo aanwezigheid van uitval van Service Bus relay-eindpunt toobe. tooachieve geo-replicatie, Hallo-service moet twee relay-eindpunten maken in verschillende naamruimten. Hallo-naamruimten moet zich bevinden in verschillende datacenters en de twee eindpunten Hallo moeten verschillende namen hebben. Bijvoorbeeld: een primaire eindpunt kan worden bereikt onder **contosoPrimary.servicebus.windows.net/myPrimaryService**, terwijl het bijbehorende secundaire server kan worden bereikt onder **contosoSecondary.servicebus.windows.net /mySecondaryService**.

Hallo-service vervolgens luistert op beide eindpunten en een client-service op de eindpunten Hallo kunt aanroepen. Een clienttoepassing willekeurig een van de Hallo relays hervat als primaire eindpunt Hallo en stuurt de aanvraag toohello actief eindpunt. Als het Hallo-bewerking is mislukt met foutcode, wordt deze fout geeft aan dat Hallo relay-eindpunt is niet beschikbaar. Hallo-toepassing opent een kanaal toohello back-eindpunt en databasebron moet worden gestuurd Hallo-aanvraag. Op dat moment overschakelen rollen hello active- en back-eindpunten Hallo: Hallo clienttoepassing beschouwt Hallo oude actief eindpunt toobe Hallo nieuwe back-eindpunt en de oude back-upeindpunt toobe Hallo Hallo nieuwe actief eindpunt. Als beide mislukken verzendt, Hallo-rollen van de twee entiteiten Hallo blijven ongewijzigd en wordt een fout geretourneerd.

Hallo [Geo-replicatie met Service Bus relayed berichten] [ Geo-replication with Service Bus relayed Messages] voorbeeld laat zien hoe tooreplicate doorstuurt.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>Wachtrijen en onderwerpen tegen storingen van datacenter of noodsituaties beveiligen
tooachieve herstelmogelijkheden tegen storingen van datacenter wanneer met behulp van brokered messaging, Service Bus ondersteunt twee methoden: *active* en *passieve* replicatie. Voor elke methode als een bepaalde wachtrij of onderwerp toegankelijk in Hallo aanwezigheid van een storing in een datacenter blijven moet, kunt u dit maken in beide naamruimten. Beide entiteiten kunnen Hallo hebben dezelfde naam. Bijvoorbeeld: een primaire wachtrij kan worden bereikt onder **contosoPrimary.servicebus.windows.net/myQueue**, terwijl het bijbehorende secundaire server kan worden bereikt onder **contosoSecondary.servicebus.windows.net/myQueue**.

Als de toepassing hello permanente afzender naar ontvanger communicatie niet vereist, kunt Hallo toepassing een duurzame clientzijde wachtrij tooprevent verlies en tooshield Hallo afzender van een tijdelijke fouten met Service Bus implementeren.

## <a name="active-replication"></a>Actieve replicatie
Actieve replicatie maakt gebruik van entiteiten in beide naamruimten voor elke bewerking. Een client die u een bericht verzendt verzendt twee exemplaren van Hallo hetzelfde bericht. de eerste kopie Hallo toohello primaire entiteit wordt verzonden (bijvoorbeeld **contosoPrimary.servicebus.windows.net/sales**), en Hallo tweede kopie van het Hallo-bericht verzonden toohello secundaire entiteit (bijvoorbeeld  **contosoSecondary.servicebus.windows.net/sales**).

Een client ontvangt berichten van beide wachtrijen. Hallo ontvanger processen Hallo eerste kopie van een bericht en de tweede kopie Hallo wordt onderdrukt. dubbele berichten toosuppress Hallo afzender moet elk bericht met een unieke identificatie labelen. Beide kopieën van het Hallo-bericht moeten worden gemarkeerd met Hallo dezelfde id. U kunt Hallo [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] of [BrokeredMessage.Label] [ BrokeredMessage.Label] eigenschappen of een aangepaste eigenschap tootag Hallo Bericht. Hallo ontvanger moet een lijst met berichten die al zijn ontvangen onderhouden.

Hallo [Geo-replicatie met Service Bus Brokered berichten] [ Geo-replication with Service Bus Brokered Messages] ziet u het actieve replicatie van berichtentiteiten.

> [!NOTE]
> Hallo actieve replicatie benadering wordt het aantal bewerkingen Hallo verdubbeld, dus deze benadering toohigher kosten kan leiden.
> 
> 

## <a name="passive-replication"></a>Passieve replicatie
In geval veroorzaakt gratis Hallo passieve replicatie maakt gebruik van slechts één van de twee berichtentiteiten Hallo. Een client verzendt Hallo-bericht toohello active entiteit. Als het Hallo-bewerking op de actieve entiteit Hallo mislukt met de foutcode die aangeeft Hallo datacenter hosts Hallo active entiteit mogelijk niet beschikbaar, verzendt Hallo-client een kopie van het Hallo-bericht toohello back-entiteit. Op dat moment overschakelen rollen hello active- en back-upentiteiten Hallo: Hallo verzendende client beschouwt Hallo oude active entiteit toobe Hallo nieuwe back-entiteit en Hallo oude back-entiteit is hello nieuwe active entiteit. Als beide mislukken verzendt, Hallo-rollen van de twee entiteiten Hallo blijven ongewijzigd en wordt een fout geretourneerd.

Een client ontvangt berichten van beide wachtrijen. Omdat er een kans is die ontvanger Hallo twee kopieën van dezelfde-, Hallo bericht Hallo ontvangt ontvanger dubbele berichten moet onderdrukken. U kunt onderdrukken dubbele items in Hallo dezelfde manier zoals beschreven voor actieve replicatie.

Passieve replicatie is in het algemeen goedkoper dan actieve replicatie omdat in de meeste gevallen slechts één bewerking wordt uitgevoerd. Latentie, doorvoer en kosten zijn identiek toohello niet-gerepliceerde scenario.

Als u passieve replicatie gebruikt, in Hallo kunnen volgende scenario's berichten zoekraken of worden twee keer ontvangen:

* **Bericht vertraging of verlies**: wordt ervan uitgegaan dat Hallo afzender een m1 toohello primaire berichtenwachtrij verzonden en vervolgens Hallo wachtrij uitvalt voordat Hallo ontvanger m1 ontvangt. Hallo afzender verzendt een daaropvolgende m2 toohello secundaire berichtenwachtrij. Als de primaire wachtrij Hallo tijdelijk niet beschikbaar is is, ontvangt Hallo ontvanger m1 nadat Hallo wachtrij weer beschikbaar is. Als er een ramp optreedt ontvangt Hallo ontvanger mogelijk nooit m1.
* **Dubbele ontvangst**: wordt ervan uitgegaan dat Hallo afzender verzendt een m toohello primaire berichtenwachtrij. Service Bus m verwerkt is, maar toosend een antwoord is mislukt. Nadat Hallo verzenden time-out bij bewerking, stuurt Hallo afzender een identieke kopie van m toohello secundaire wachtrij. Als ontvanger Hallo kunnen tooreceive Hallo eerste kopie van m voordat Hallo primaire wachtrij niet meer beschikbaar is, Hallo ontvanger beide kopieën van m op ongeveer Hallo ontvangt hetzelfde moment. Als Hallo ontvanger niet kunnen tooreceive Hallo eerste kopie van m voordat Hallo primaire wachtrij niet meer beschikbaar is, worden Hallo ontvanger in eerste instantie ontvangt alleen Hallo tweede kopie van m, maar ontvangt vervolgens een tweede exemplaar van m zodra Hallo primaire wachtrij beschikbaar is.

Hallo [Geo-replicatie met Service Bus brokered berichten] [ Geo-replication with Service Bus Brokered Messages] voorbeeld demonstreert passieve replicatie van berichtentiteiten.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over herstel na noodgevallen, Zie de volgende artikelen:

* [Azure SQL Database Business Continuity][Azure SQL Database Business Continuity]
* [Robuuste toepassingen voor Azure ontwerpen][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
