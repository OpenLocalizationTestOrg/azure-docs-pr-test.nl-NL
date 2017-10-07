---
title: aaaAzure Cosmos DB Python API SDK & Resources | Microsoft Docs
description: Meer informatie over Hallo Python-API en SDK, inclusief release datums, buiten gebruik stellen datums en wijzigingen die zijn aangebracht tussen elke versie van hello Azure Cosmos DB Python SDK.
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>Azure DB Cosmos Python SDK: Releaseopmerkingen en resources
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET-Feed van wijzigen](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [REST-resourceprovider](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**SDK downloaden**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**API-documentatie**</td><td>[Python-API-naslagdocumentatie](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**SDK-installatie-instructies**</td><td>[Python SDK installatie-instructies](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Bijdragen tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Aan de slag**</td><td>[Aan de slag met Hallo Python SDK](documentdb-python-application.md)</td></tr>

<tr><td>**Huidige ondersteund platform**</td><td>[Python 2.7](https://www.python.org/downloads/) en [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Releaseopmerkingen
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Ondersteuning toegevoegd voor een nieuwe consistentieniveau ConsistentPrefix genoemd.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Ondersteuning toegevoegd voor aggregatie van query's (COUNT, MIN, MAX, SUM en Gem).
* Een optie voor het uitschakelen van SSL-verificatie bij het uitvoeren in Cosmos DB Emulator toegevoegd.
* Hallo-beperking van de afhankelijke aanvragen module toobe exact 2.10.0 verwijderd.
* Minimaal doorvoer voor gepartitioneerde verzamelingen uit 10,100 RU/s too2500 RU/s verlaagd.
* Ondersteuning toegevoegd voor het inschakelen van logboekregistratie script tijdens het uitvoeren van de opgeslagen procedure.
* REST-API-versie tegenaan te ' 2017-01-19' in deze versie.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Redactionele wijzigingen aangebracht in toodocumentation opmerkingen.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Ondersteuning toegevoegd voor Python 3.5.
* Ondersteuning toegevoegd voor verbindingsgroepering met een module aanvragen.
* Ondersteuning toegevoegd voor sessieconsistentie.
* Ondersteuning toegevoegd voor TOP/ORDERBY-query's voor gepartitioneerde verzamelingen.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Toegevoegde opnieuw Beleidsondersteuning voor beperkte aanvragen. (Beperkte aanvragen ontvangen van een aanvraag snelheid te groot uitzondering, foutcode 429.) Standaard Azure Cosmos DB pogingen negen keer voor elke aanvraag wanneer foutcode 429 is opgetreden, Hallo retryAfter tijd in Hallo antwoordheader naleven. Een vaste opnieuw tijdsinterval kan nu worden ingesteld als onderdeel van Hallo RetryOptions-eigenschap op Hallo ConnectionPolicy object als u wilt dat tooignore hello retryAfter tijd geretourneerd door server tussen nieuwe pogingen Hallo. Azure Cosmos-DB wordt nu gewacht op maximaal 30 seconden voor elke aanvraag die wordt beperkt (ongeacht het aantal pogingen) en het Hallo-antwoord met foutcode 429 retourneert. Deze tijd kan ook worden onderdrukt in Hallo RetryOptions-eigenschap op ConnectionPolicy-object.
* Cosmos DB retourneert nu x-ms-versnelling-aantal nieuwe pogingen en x-ms-throttle-retry-wait-time-ms Hallo antwoordheaders in elke aanvraag toodenote Hallo versnelling probeer telling en het Hallo cummulative keer Hallo gewacht tussen pogingen Hallo.
* Verwijderde Hallo RetryPolicy klasse en bijbehorende Hallo-eigenschap (retry_policy) op Hallo document_client klasse worden weergegeven en in plaats daarvan een RetryOptions klasse blootstellen Hallo RetryOptions eigenschap voor ConnectionPolicy-klasse die gebruikt toooverride worden kan geïntroduceerd Sommige van de standaard Hallo opties voor nieuw pogingen.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Hallo toegevoegde ondersteuning voor meerdere landen/regio database accounts.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Toegevoegde Hallo ondersteuning voor de functie voor tooLive(TTL) voor documenten.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Oplossingen voor problemen die betrekking tooserver side tooallow speciale tekens in pad partitionkey partitioneren.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Geïmplementeerd [gepartitioneerde verzamelingen](partition-data.md) en [prestatieniveaus die door de gebruiker gedefinieerde](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Toevoegen van hash- & bereik partitie resolvers tooassist met sharding-toepassingen op verschillende partities.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Upsert implementeren. Nieuwe UpsertXXX methoden toosupport Upsert functie toegevoegd.
* ID gebaseerde routering wordt geïmplementeerd. Er zijn geen openbare API-wijzigingen, worden alle wijzigingen interne.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Ondersteunt georuimtelijke index.
* De eigenschap id voor alle resources valideert. Kunnen geen id's voor bronnen bevatten?, /, #, \, tekens of eindigen met een spatie.
* Voegt nieuwe header 'index transformatie uitgevoerd' tooResourceResponse.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* V2-indexeringsbeleid implementeert.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Ondersteunt proxyverbinding.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK.

## <a name="release--retirement-dates"></a>Release & buiten gebruik stellen datums
Microsoft biedt melding ten minste **12 maanden** voordat het buiten gebruik stellen van een SDK in de volgorde toosmooth Hallo overgang tooa nieuwere/ondersteunde versie.

Nieuwe functies en functionaliteit en optimalisaties worden alleen toegevoegd toohello huidige SDK als zodanig verdient het voorkeur dat u altijd upgrade toohello nieuwste SDK versie zo spoedig mogelijk. 

Een aanvraag tooCosmos DB met een buiten gebruik gestelde SDK worden geweigerd door Hallo-service.

> [!WARNING]
> Alle versies van hello Azure DocumentDB SDK voor Python voorafgaande tooversion **1.0.0** wordt buiten gebruik worden gesteld op **29 februari 2016**. 
> 
> 

<br/>

| Versie | Releasedatum | Vervaldatum |
| --- | --- | --- |
| [2.2.0](#2.2.0) |10 mei 2017 |--- |
| [2.1.0](#2.1.0) |01 mei 2017 |--- |
| [2.0.1](#2.0.1) |30 oktober 2016 |--- |
| [2.0.0](#2.0.0) |29 september 2016 |--- |
| [1.9.0](#1.9.0) |07 juli 2016 |--- |
| [1.8.0](#1.8.0) |14 juni 2016 |--- |
| [1.7.0](#1.7.0) |26 april 2016 |--- |
| [1.6.1](#1.6.1) |08 april 2016 |--- |
| [1.6.0](#1.6.0) |29 maart 2016 |--- |
| [1.5.0](#1.5.0) |03 januari 2016 |--- |
| [1.4.2](#1.4.2) |06 oktober 2015 |--- |
| [1.4.1](#1.4.1) |06 oktober 2015 |--- |
| [1.2.0](#1.2.0) |06 augustus 2015 |--- |
| [1.1.0](#1.1.0) |09 juli 2015 |--- |
| [1.0.1](#1.0.1) |25 mei 2015 |--- |
| [1.0.0](#1.0.0) |07 april 2015 |--- |
| 0.9.4-prelease |14 januari 2015 |29 februari 2016 |
| 0.9.3-prelease |09 december 2014 |29 februari 2016 |
| 0.9.2-prelease |25 november 2014 |29 februari 2016 |
| 0.9.1-prelease |23 september 2014 |29 februari 2016 |
| 0.9.0-prelease |21 augustus 2014 |29 februari 2016 |

## <a name="faq"></a>Veelgestelde vragen
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Zie ook
Zie toolearn meer informatie over de Cosmos-DB [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) pagina van de service. 

