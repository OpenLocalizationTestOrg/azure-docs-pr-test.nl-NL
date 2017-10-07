---
title: aaaOverview van AMQP 1.0 in Azure Service Bus | Microsoft Docs
description: Meer informatie over het gebruik van Hallo geavanceerde Message Queuing-Protocol (AMQP) 1.0 in Azure.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>AMQP 1.0-ondersteuning in Service Bus
Beide hello Azure Service Bus-cloudservice en on-premises [Service Bus voor Windows Server (Service Bus 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) ondersteuning Hallo geavanceerde Message Queueing Protocol (AMQP) 1.0. AMQP kunt u toobuild cross-platform, hybride toepassingen met behulp van een open standaard protocol. U kunt opstellen toepassingen met behulp van de onderdelen die zijn gemaakt met behulp van verschillende talen en frameworks en die worden uitgevoerd op verschillende besturingssystemen worden uitgevoerd. Al deze onderdelen kunnen verbinding tooService Bus en naadloos gestructureerde business berichten uitwisselen efficiënt en volledig betrouwbaar.

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>Inleiding: Wat is AMQP 1.0 en waarom is het belangrijk?
Traditioneel bericht georiënteerd middlewareproducten eigen protocollen gebruikt voor communicatie tussen clienttoepassingen en beleggingsmakelaars. Dit betekent dat wanneer u een bepaalde leverancier messaging broker hebt geselecteerd, moet u die leverancier bibliotheken tooconnect uw client toepassingen toothat broker. Dit resulteert in een zekere mate van afhankelijkheid van die leverancier, omdat een ander product van toepassing tooa overdragen codewijzigingen in alle Hallo verbonden toepassingen vereist. 

Bovendien is het lastig berichtenbrokers verbinding te maken van verschillende leveranciers. Dit is doorgaans op toepassingsniveau bridging toomove berichten van een systeem tooanother en tootranslate tussen hun eigen berichtindeling. Dit is een algemene vereiste; bijvoorbeeld, wanneer u moet een nieuwe geïntegreerde interface tooolder bieden verschillende systemen of integreren van IT-systemen na een fusie.

Hallo softwarebranche is een bedrijf snel bewegende; nieuwe programmeertalen en toepassingsframeworks worden soms heel breed tempo geïntroduceerd. Op deze manier ontwikkelaars willen tootake profiteren van de meest recente platformfuncties Hallo en Hallo vereisten van de IT-systemen ontwikkelen gedurende een bepaalde periode. Echter, soms hello geselecteerde messaging leverancier ondersteunt geen deze platforms. Omdat messaging-protocollen eigen zijn, is het niet mogelijk voor anderen tooprovide bibliotheken voor deze nieuwe platforms. Daarom moet u methoden zoals gateways of bruggen waarmee u bouwt toocontinue toouse Hallo messaging product gebruiken.

Hallo-ontwikkeling van Hallo geavanceerde Message Queuing-Protocol (AMQP) 1.0 is gemotiveerd door deze problemen. Deze afkomstig is van JP Morgan Chase die, zoals de meest financiële diensten ondernemingen, zware gebruikers van middleware bericht georiënteerd. Hallo-doel is eenvoudig: toocreate een open standaard messaging protocol waardoor mogelijk toobuild bericht gebaseerde toepassingen met behulp van de onderdelen die zijn gebouwd met behulp van verschillende talen en frameworks besturingssystemen, alles beste van RAS-onderdelen uit met behulp van een bereik van leveranciers.

## <a name="amqp-10-technical-features"></a>Technische AMQP 1.0-functies
AMQP 1.0 is een efficiënte, betrouwbare, wire-niveau messaging protocol waarmee u toobuild robuuste, cross-platform kunt, berichttoepassingen. Hallo-protocol is een eenvoudige doel: toodefine Hallo mechanisme van Hallo veilig, betrouwbaar en efficiënt overdracht van berichten tussen twee partijen. Hallo-berichten zelf zijn gecodeerd met behulp van een draagbare gegevens weergave waarmee heterogene afzenders en ontvangers tooexchange gestructureerd business berichten op volledige betrouwbaarheid. Hallo Hier volgt een samenvatting van de belangrijkste functies Hallo:

* **Efficiënte**: AMQP 1.0 is een protocol verbindings-geörienteerde dat standaard een binaire codering voor Hallo instructies-protocol en Hallo business berichten via het overgedragen. Geavanceerde datatransportbesturing schema's toomaximize Hallo gebruik van het Hallo-netwerk en Hallo verbonden onderdelen opgenomen. Die gezegd, Hallo-protocol is ontworpen toostrike een evenwicht tussen efficiëntie, flexibiliteit en interoperabiliteit zijn.
* **Betrouwbare**: Hallo AMQP 1.0-protocol kunt u berichten toobe uitgewisseld met een bereik van betrouwbaarheid garanties, van brand en vergeet tooreliable exact-levering eenmaal bevestigd.
* **Flexibele**: AMQP 1.0 is een flexibel protocol die gebruikt toosupport verschillende topologieën worden kan. Hallo kan hetzelfde protocol worden gebruikt voor communicatie van client-naar-client, client-naar-broker en broker naar broker.
* **Onafhankelijk van de Broker-model**: Hallo AMQP 1.0-specificatie maakt geen eventuele vereisten op Hallo messaging model gebruikt door een broker. Dit betekent dat het is mogelijk tooeasily AMQP 1.0 ondersteuning tooexisting berichtenbrokers toevoegen.

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>AMQP 1.0 is een standaard (met een hoofdletter ')
AMQP 1.0 is een internationaal standaard goedgekeurd door de ISO en IEC als ISO/IEC 19464:2014.

AMQP 1.0 is in ontwikkeling sinds 2008 door een groep core van meer dan 20 bedrijven, zowel technologie leveranciers en eindgebruikers ondernemingen. Gedurende die tijd gebruiker bedrijven hebben bijgedragen tot de echte zakelijke vereisten en Hallo technologieleveranciers hebt ontwikkeld Hallo protocol toomeet deze vereisten. Tijdens Hallo proces hebben leveranciers deelgenomen aan workshops waarin ze toovalidate Hallo interoperabiliteit tussen hun implementaties samengewerkt.

In oktober 2011 Hallo-projecten is overgegaan tooa technisch comité binnen de organisatie Hallo voor Hallo verschuiving van gestructureerde gegevens Standards (OASIS) en Hallo OASIS AMQP 1.0 standaard werd uitgebracht in oktober 2012. Hallo volgende bedrijven hebben deelgenomen aan Hallo technisch comité tijdens het ontwikkelen van Hallo Hallo standaard:

* **Technologieleveranciers**: Axway Software, Huawei technologieën, vorm Software, INETCO systemen, Kaazing, Microsoft, Mitre Corporation, Primeton technologieën, voortgang van de Software, Red Hat, SITA, Software AG, Solace systemen, VMware, WSO2, Zenika.
* **Gebruiker ondernemingen**: Bank-Amerika, tegoed Zwitserland, Deutsche Boerse, Goldman Sachs, JPMorgan Chase.

Aantal Hallo hierboven vaak voordelen van open standaarden zijn onder andere:

* Minder kans op vaste leverancier
* Interoperabiliteit
* Algemene beschikbaarheid van bibliotheken en tooling
* Bescherming tegen veroudering
* Beschikbaarheid van geïnformeerde personeel
* Lagere en beheerbare risico

## <a name="amqp-10-and-service-bus"></a>AMQP 1.0 en Service Bus
AMQP 1.0-ondersteuning in Azure Service Bus betekent dat u kunt nu gebruikmaken van Hallo Service Bus queuing en publiceren/abonneren brokered messaging-onderdelen uit een reeks met behulp van een efficiënte binaire protocol platforms. Bovendien kunt u toepassingen bestaan uit de onderdelen die zijn gebouwd met behulp van een combinatie van talen en frameworks besturingssystemen maken.

Hallo volgende afbeelding ziet u een voorbeeldimplementatie waarbij Java-clients op Linux, geschreven met behulp van Hallo standard Java bericht Service (JMS) API en de .NET-clients waarop Windows, exchange-berichten via Service Bus met AMQP 1.0.

![][0]

**Afbeelding 1: Implementatie voorbeeldscenario platformonafhankelijke berichten met behulp van Service Bus en AMQP 1.0 wordt weergegeven**

Op dit moment Hallo bekend volgende clientbibliotheken toowork met Service Bus:

| Taal | Bibliotheek |
| --- | --- |
| Java |Apache Qpid Java bericht Service (JMS)-client<br/>VORM Software SwiftMQ Java-client |
| C |Apache Qpid Proton-C |
| PHP |Apache Qpid Proton-PHP |
| Python |Apache Qpid Proton-Python |
| C# |AMQP .net Lite |

**Afbeelding 2: Tabel met AMQP 1.0-clientbibliotheken**

## <a name="summary"></a>Samenvatting
* AMQP 1.0 is een open, betrouwbare messaging-protocol dat u toobuild cross-platform, hybride toepassingen kunt gebruiken. AMQP 1.0 is een standaard OASIS.
* AMQP 1.0-ondersteuning is nu beschikbaar in de Azure Service Bus, evenals een Service Bus voor Windows Server (Service Bus 1.1). Prijzen is dezelfde als voor bestaande protocollen Hallo Hallo.

## <a name="next-steps"></a>Volgende stappen
Gereed toolearn meer? Ga naar Hallo koppelingen te volgen:

* [Met behulp van Servicebus in .NET met AMQP]
* [Met behulp van Servicebus met Java met AMQP]
* [Apache Qpid Proton-C installeren op een Azure Linux VM]
* [AMQP in WindowsServer-Servicebus]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[Met behulp van Servicebus in .NET met AMQP]: service-bus-amqp-dotnet.md
[Met behulp van Servicebus met Java met AMQP]: service-bus-amqp-java.md
[Apache Qpid Proton-C installeren op een Azure Linux VM]: service-bus-amqp-apache.md
[AMQP in WindowsServer-Servicebus]: https://msdn.microsoft.com/library/dn574799.aspx
