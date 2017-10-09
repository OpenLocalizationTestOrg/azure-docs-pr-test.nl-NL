---
title: 'Azure Cosmos DB: DocumentDB-API | Microsoft Docs'
description: Meer informatie over hoe u kunt Azure Cosmos DB toostore en query grote hoeveelheden JSON-documenten met een lage latentie met behulp van SQL en JavaScript.
keywords: json-database, documentdatabase
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>Inleiding tooAzure Cosmos DB: DocumentDB-API

[Azure Cosmos DB](introduction.md) is de wereldwijd gedistribueerde databaseservice met meerdere modellen van Microsoft voor essentiële toepassingen. Biedt Azure Cosmos DB [directe globale distributie](distribute-data-globally.md), [elastisch schalen van doorvoer en opslag](partition-data.md) overal ter wereld, één cijfer milliseconde latenties op Hallo 99th percentiel, [vijf goed gedefinieerde consistentieniveaus](consistency-levels.md), hoge beschikbaarheid, alle back-ups door gegarandeerd [toonaangevende Sla's](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [indexeert automatisch gegevens](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) zonder dat u toodeal met schema- en management. Azure Cosmos DB beschikt over meerdere modellen en ondersteunt modellen voor document-, sleutelwaarde-, grafiek- en kolomgegevens. 

![Azure DocumentDB-API](./media/documentdb-introduction/cosmosdb-documentdb.png) 

Hallo DocumentDB API, Azure Cosmos DB biedt uitgebreide en vertrouwd [SQL querymogelijkheden](documentdb-sql-query.md) met consistente lage latenties via JSON-gegevens zonder schema. In dit artikel bieden we een overzicht van hello Azure Cosmos DB van DocumentDB API en hoe u kunt deze gebruiken toostore grote hoeveelheden JSON-gegevens, in volgorde van milliseconden latentie doorzoeken, en Hallo schema eenvoudig ontwikkelen. 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>Welke mogelijkheden en belangrijke functies biedt Azure Cosmos DB?
Azure Cosmos-DB, via Hallo DocumentDB-API biedt Hallo na de belangrijkste mogelijkheden en voordelen:

* **Elastische schaalbare doorvoer en opslag:** eenvoudig omhoog of omlaag uw JSON-database toomeet schalen van uw toepassing nodig heeft. Uw gegevens worden opgeslagen op SSD-schijven (Solid State Disks) voor lage voorspelbare latenties. Azure Cosmos DB ondersteunt containers voor JSON-gegevens op te slaan verzamelingen die kunnen worden geschaald toovirtually aangeroepen onbeperkte opslaggrootte en ingerichte doorvoer. Naarmate uw toepassing groeit, kunt u Azure Cosmos DB probleemloos elastisch schalen met voorspelbare prestaties. 


* **Meerdere landen/regio-replicatie:** transparant repliceert je je hebt gekoppeld aan uw Azure DB die Cosmos-account, zodat u toodevelop-toepassingen waarvoor globale toegang toodata waarbij tooall regio's Azure Cosmos-DB de wisselwerking tussen de consistentie, beschikbaarheid en prestaties, met bijbehorende garanties. Azure Cosmos DB biedt transparante regionale failover multihoming API's, en Hallo mogelijkheid tooelastically scale doorvoer en opslag van verschillende Hallo wereld. Zie [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md) (Gegevens wereldwijd distribueren met Azure Cosmos DB) voor meer informatie.

* **Ad-hocquery's met bekende SQL-syntaxis:** u kunt heterogene JSON-documenten opslaan en query's op deze documenten uitvoeren via een bekende SQL-syntaxis. Azure Cosmos-database maakt gebruik van een uiterst gelijktijdige, vergrendelingsvrije, logboek gestructureerde indexering technologie tooautomatically index alle documentinhoud. Hierdoor kunnen de uitgebreide realtime query's zonder Hallo nodig toospecify schemahints, secundaire indexen of weergaven. Zie [Query Azure Cosmos DB](documentdb-sql-query.md) (Query's uitvoeren voor Azure Cosmos DB) voor meer informatie. 
* **JavaScript-uitvoering in de database Hallo:** Express-toepassingslogica als opgeslagen procedures, triggers en door de gebruiker gedefinieerde functies (UDF's) met standaard-JavaScript. Hierdoor kan uw toepassing logica toooperate over gegevens zonder dat u de toepassing hello en Hallo-databaseschema komen niet overeen Hallo. Hallo DocumentDB API biedt volledige transactionele uitvoering van JavaScript-toepassingslogica rechtstreeks in de database-engine Hallo. Hallo diepe integratie van JavaScript kan Hallo uitvoering van INSERT, REPLACE, verwijderen en selecteer bewerkingen uit vanuit een JavaScript-programma als geïsoleerde transactie. Zie [Programmeren op de DocumentDB-server](programming.md) voor meer informatie.

* **Instelbare consistentieniveaus:** selecteren uit vijf goed gedefinieerde consistentie niveaus tooachieve optimale balans tussen de consistentie en prestaties. Voor query's en leesbewerkingen biedt Azure Cosmos DB vijf verschillende consistentieniveaus: sterk, gebonden-verouderd, sessie, consistent voorvoegsel en mogelijk. Deze gedetailleerde, goed gedefinieerde consistentieniveaus kunt u toomake geluid verschillen tussen de consistentie, beschikbaarheid en latentie. Meer informatie [met behulp van de consistentie niveaus toomaximize beschikbaarheid en prestaties](consistency-levels.md).

* **Volledig beheerd:** Hallo nodig toomanage database- en machineresources te elimineren. Als een volledig beheerde service voor de Microsoft Azure, u niet nodig toomanage virtuele machines te doen, implementeren en configureren van software, beheren schalen of bekommeren om complexe gegevenslaag upgrades. Er wordt automatisch een back-up van elke database gemaakt en de databases worden automatisch beveiligd tegen regionale fouten. U kunt gemakkelijk een Cosmos-DB Azure-account toevoegen en capaciteit inrichten als u deze nodig hebt, zodat u toofocus op uw toepassing in plaats van het besturingssysteem en het beheren van uw database. 

* **Open ontwerp:** U kunt snel aan de slag door gebruik te maken van bestaande vaardigheden en hulpprogramma's. Programmeren tegen Hallo DocumentDB API een eenvoudige en gebruiksvriendelijke, en geen vereist u nieuwe hulpprogramma's voor tooadopt of toocustom extensies tooJSON of JavaScript voldoen. U kunt toegang tot alle Hallo databasefunctionaliteit inclusief CRUD-, query- en JavaScript-verwerking via een eenvoudige RESTful HTTP-interface. Hallo DocumentDB API hebben bestaande indelingen, talen en standaarden terwijl Daarnaast waardevolle databasemogelijkheden ze.

* **Automatische indexering:** standaard Azure Cosmos DB automatisch alle Hallo documenten in de database Hallo geïndexeerd en niet verwacht of vereisen een schema of het maken van secundaire indexen. Niet wilt dat tooindex alles? Maakt u zich geen zorgen. U kunt ook [paden uitschakelen in uw JSON-bestand](indexing-policies.md).

* **Wijziging feed ondersteuning:** wijziging feed bevat een gesorteerde lijst van documenten binnen een verzameling Azure Cosmos DB in Hallo volgorde waarin ze zijn gewijzigd. Deze feed gebruikte toolisten voor toodata wijzigingen in de volgorde tooreplicate gegevens worden, API-aanroepen activeren of stroom verwerking uitvoeren op updates. Wijziging feed is automatisch ingeschakeld en eenvoudig toouse: [meer informatie over het wijzigen van feed](https://docs.microsoft.com/azure/cosmos-db/change-feed). 

## <a name="data-management"></a>Hoe beheert u gegevens met Hallo DocumentDB API?
Hallo DocumentDB API kan worden beheerd via goed gedefinieerde databaseresources JSON-gegevens. Deze resources worden gerepliceerd voor hoge beschikbaarheid en zijn uniek adresseerbaar op basis van hun logische URI. Hallo DocumentDB API biedt dat een eenvoudige HTTP op basis van RESTful-programmeermodel voor alle resources. 


Hello Azure DB die Cosmos-databaseaccount is een unieke naamruimte waarmee u toegang tot tooAzure Cosmos DB. Voordat u een databaseaccount maken kunt, moet u beschikken over een Azure-abonnement waarmee u toegang tot tooa diverse Azure-services. 

Alle resources binnen Azure Cosmos DB worden gemodelleerd en opgeslagen als JSON-documenten. Resources worden beheerd als items, oftewel JSON-documenten met metagegevens, en als feeds, oftewel verzamelingen items. Sets met items bevinden zich in hun respectieve feeds.

Hallo in onderstaande afbeelding ziet u Hallo relaties tussen hello Azure DB die Cosmos-resources:

![Hallo hiërarchische relatie tussen resources in Azure Cosmos-DB][1] 

Een databaseaccount bestaat uit een set databases die elk meerdere verzamelingen bevatten. Elk verzameling kan opgeslagen procedures, triggers, UDF's, documenten en verwante bijlagen bevatten. Een database ook horen gebruikers, elk met een reeks machtigingen tooaccess verschillende andere verzamelingen, opgeslagen procedures, triggers, UDF's, documenten of bijlagen. Databases, gebruikers, machtigingen en verzamelingen zijn door het systeem gedefinieerde resources met bekende schema's. Documenten, opgeslagen procedures, triggers, UDF's en bijlagen bevatten echter willekeurige, door de gebruiker gedefinieerde JSON-inhoud.  

> [!NOTE]
> Aangezien Hallo DocumentDB API eerder beschikbaar als hello Azure DocumentDB-service is, u kunt doorgaan tooprovision, controleren en beheren van accounts die zijn gemaakt via hello Azure Resource Management REST-API of met behulp van hulpprogramma's hello Azure DocumentDB of Azure Cosmos-DB resourcenamen. We gebruiken door elkaar Hallo namen wanneer toohello Azure DocumentDB APIs wordt verwezen. 

## <a name="develop"></a>Hoe kan ik Hello DocumentDB API-apps ontwikkelen?

Azure Cosmos DB Ontsluit resources via Hallo REST-API's die kunnen worden aangeroepen via elke taal waarmee HTTP/HTTPS-aanvragen. Bovendien bieden wij programmeringsbibliotheken voor verschillende veelgebruikte talen voor Hallo DocumentDB-API. Hallo clientbibliotheken vereenvoudigen veel aspecten van het werken met Hallo API door details zoals adrescaching, Uitzonderingsbeheer, automatische nieuwe pogingen, enzovoort. Bibliotheken zijn momenteel beschikbaar voor Hallo talen en platformen te volgen:  

| Downloaden | Documentatie |
| --- | --- |
| [.NET SDK](http://go.microsoft.com/fwlink/?LinkID=402989) |[.NET-bibliotheek](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [Node.js SDK](http://go.microsoft.com/fwlink/?LinkID=402990) |[Node.js-bibliotheek](http://azure.github.io/azure-documentdb-node/) |
| [Java SDK](http://go.microsoft.com/fwlink/?LinkID=402380) |[Java-bibliotheek](/java/api/com.microsoft.azure.documentdb) |
| [JavaScript SDK](http://go.microsoft.com/fwlink/?LinkID=402991) |[JavaScript-bibliotheek](http://azure.github.io/azure-documentdb-js/) |
| N.v.t. |[JavaScript SDK op de server](http://azure.github.io/azure-documentdb-js-server/) |
| [Python SDK](https://pypi.python.org/pypi/pydocumentdb) |[Python-bibliotheek](http://azure.github.io/azure-documentdb-python/) |
| N.v.t. | [API voor MongoDB](mongodb-introduction.md)


Met behulp van Hallo [Azure Cosmos DB Emulator](local-emulator.md), u kunt ontwikkelen en testen van de toepassing lokaal door hello DocumentDB API, zonder te maken van een Azure-abonnement of mogelijke kosten. Wanneer u tevreden bent over hoe uw toepassing in Hallo-emulator werkt, kunt u een Azure DB die Cosmos-account in Hallo cloud toousing overschakelen.

Afgezien van basic maken, lezen, bijwerken en verwijderen van bewerkingen, Hallo DocumentDB API een uitgebreide SQL-QueryInterface biedt voor het ophalen van JSON-documenten en server side-ondersteuning voor transactionele uitvoering van JavaScript-toepassingslogica. Hallo query's en scripts uitvoeren interfaces zijn beschikbaar via alle platformbibliotheken evenals Hallo REST-API's. 

### <a name="sql-query"></a>SQL-query
Hallo DocumentDB API ondersteunt het uitvoeren van query's documenten met een SQL-taal, die verankerd in Hallo ligt JavaScript typen systeem, en voor expressies met ondersteuning voor relationele, hiërarchische en ruimtelijke query's. Hallo quertytaal is een eenvoudige maar krachtige interface tooquery JSON-documenten. Hallo taal ondersteunt een subset van ANSI SQL-grammatica en diepe integratie van JavaScript-object, matrices objectconstructie en functieaanroep wordt toegevoegd. Hallo API DocumentDB levert het querymodel zonder een expliciet schema of indexeringshints van Hallo-ontwikkelaar.

Gebruiker gedefinieerde functies (UDF's) worden geregistreerd bij Hallo DocumentDB API en waarnaar wordt verwezen als onderdeel van een SQL-query waardoor Hallo grammatica toosupport aangepaste toepassingslogica uitbreiden. Deze UDF zijn geschreven als JavaScript-programma's en worden uitgevoerd binnen een Hallo-database. 

Hallo voor .NET-ontwikkelaars bevat DocumentDB API [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx) biedt ook een LINQ-provider opvragen. 

### <a name="transactions-and-javascript-execution"></a>Transacties en JavaScript uitvoeren
Hallo DocumentDB API kunt u toepassingslogica toowrite als benoemde programma's die zijn geschreven in JavaScript volledig. Deze programma's kunnen zijn geregistreerd voor een verzameling en databasebewerkingen uitvoeren op Hallo documenten binnen een bepaalde verzameling. JavaScript kan worden geregistreerd voor uitvoering als een trigger, opgeslagen procedure of als een door de gebruiker gedefinieerde functie. Triggers en opgeslagen procedures kunnen maken, lezen, bijwerken en verwijderen van documenten, terwijl de gebruiker gedefinieerde functies worden uitgevoerd als onderdeel van Hallo query uitvoeringslogica zonder schrijftoegang toohello verzameling.

JavaScript-uitvoering in Hallo Cosmos DB is gemodelleerd naar Hallo concepten die worden ondersteund door relationele databasesystemen, met JavaScript als een moderne vervanger van Transact-SQL. Alle JavaScript-logica wordt uitgevoerd binnen een ambient ACID-transactie met het isolatieniveau Snapshot. In de loop Hallo van de uitvoering ervan, als JavaScript genereert een uitzondering Hallo Hallo vervolgens hele transactie is afgebroken.

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>Zijn er online cursussen over Azure Cosmos DB?

Ja, er is een [Microsoft Virtual Academy](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847)-cursus over Azure DocumentDB. 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>Volgende stappen
Hebt u al een Azure-account? Vervolgens kunt u aan de slag met Azure Cosmos DB door onze [Quick Starts](../cosmos-db/create-documentdb-dotnet.md) te volgen. Deze bieden informatie over hoe u een account maakt en aan de slag gaat met Cosmos DB.

[1]: ./media/documentdb-introduction/json-database-resources1.png

