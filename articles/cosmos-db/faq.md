---
title: aaaAzure Cosmos DB Veelgestelde vragen | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over Azure Cosmos DB, een globaal gedistribueerd en modellen database-service ophalen. Meer informatie over de capaciteit, prestatieniveaus en schalen.
keywords: Databasevragen, veelgestelde vragen, documentdb, azure, Microsoft azure
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Veelgestelde vragen over Azure Cosmos DB
## <a name="azure-cosmos-db-fundamentals"></a>Grondbeginselen van Azure DB Cosmos
### <a name="what-is-azure-cosmos-db"></a>Wat is Azure Cosmos DB?
Azure Cosmos-database is een wereldwijd gerepliceerde en modellen database-service waarmee die biedt uitgebreide query over gegevens zonder schema configureerbare en betrouwbare prestaties leveren en maakt snelle ontwikkeling. Dit wordt bereikt door middel van een beheerd platform dat wordt ondersteund door power Hallo en bereik van Microsoft Azure. 

Azure Cosmos-database is de juiste oplossing Hallo voor web-, gaming en IoT-toepassingen wanneer voorspelbare doorvoer, hoge beschikbaarheid, lage latentie en een gegevensmodel zonder schema belangrijke vereisten zijn. Levert schemaflexibiliteit en geavanceerde indexeren en transactionele ondersteuning voor meerdere documenten met geïntegreerde JavaScript bevat. 

Voor meer databasevragen, antwoorden en instructies voor het implementeren en het gebruik van deze service, raadpleegt u Hallo [documentatiepagina voor Azure Cosmos DB](https://azure.microsoft.com/documentation/services/cosmos-db/).

### <a name="what-happened-toodocumentdb"></a>Welke happened tooDocumentDB?
Hallo DocumentDB API is een van de API's en -gegevens modellen Hallo ondersteund voor Azure Cosmos DB. Bovendien ondersteunt Azure Cosmos DB u met Graph API (Preview), tabel-API (Preview) en MongoDB-API. Zie voor meer informatie [vragen van klanten DocumentDB](#moving-to-cosmos-db).

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>Hoe krijg toomy DocumentDB-account in hello Azure-portal?
Klik in hello Azure-portal, op Hallo Azure Cosmos DB pictogram in het linkerdeelvenster Hallo. Als u een DocumentDB-account voordat had, hebt u nu een account Azure Cosmos DB met geen wijziging tooyour facturering.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>Wat zijn typische gebruiksvoorbeelden van Hallo voor Azure Cosmos DB?
Azure Cosmos-database is een goede keuze voor nieuwe web, mobiel, games, en IoT-toepassingen waarbij automatisch schalen, voorspelbare prestaties, snelle volgorde van milliseconde responstijden en mogelijkheid tooquery Hallo via schemavrije gegevens is belangrijk. Azure Cosmos DB gepaard toorapid ontwikkelen en Hallo continue herhaling van toepassingsgegevensmodellen. Toepassingen die door gebruikers gegenereerde inhoud en gegevens beheren zijn [algemene gebruiksvoorbeelden voor Azure Cosmos DB](use-cases.md). 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Hoe biedt Azure Cosmos DB voorspelbare prestaties?
Een [aanvraag eenheid](request-units.md) (RU) is de meting Hallo doorvoer in Azure Cosmos DB. Een doorvoer 1 RU komt overeen toohello doorvoer van Hallo GET van een document van 1 KB. Elke bewerking in Azure Cosmos DB, met inbegrip van leesbewerkingen, schrijfbewerkingen, SQL-query's en opgeslagen procedure-uitvoeringen, heeft een deterministische RU-waarde die gebaseerd op Hallo doorvoer vereist toocomplete Hallo bewerking. In plaats van het denken over CPU, IO, en geheugen en hoe deze elke doorvoer van uw toepassing beïnvloeden, kunt u denken in termen van een enkele RU-meting.

U kunt elke Azure DB die Cosmos-container met ingerichte doorvoer in termen van RUs aan doorvoer per seconde reserveren. Voor toepassingen van elke schaal, kunt u afzonderlijke aanvragen toomeasure hun waarden RU benchmark en inrichten van een container toohandle Hallo-totale aantal aanvraageenheden voor alle aanvragen. U kunt ook opschalen of terugschroeven doorvoer van de container als Hallo behoeften van uw toepassing veranderen. Voor meer informatie over aanvraageenheden en hulp bij het bepalen van de container moet, Zie [schatten doorvoerbehoeften](request-units.md#estimating-throughput-needs) en probeer het Hallo [doorvoer Rekenmachine](https://www.documentdb.com/capacityplanner). Hallo term *container* verwijst hier toorefers tooa DocumentDB API verzameling, Graph API grafiek, MongoDB-API-verzameling en tabel API-tabel. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>Hoe ondersteunt Azure Cosmos DB verschillende gegevensmodellen zoals sleutel/waarde, kolommen, document en grafiek?

Sleutel/waarde van (tabel), kolommen, documenteren en grafiekgegevens modellen zijn alle standaard ondersteund vanwege Hallo ARS (atomen, registreert en reeksen) die Cosmos Azure DB ontwerp is gebaseerd op. Atomen, records en reeksen kunnen worden toegewezen en eenvoudig verwachte toovarious gegevensmodellen. Hallo API's voor een subset van modellen zijn beschikbaar rechts nu (DocumentDB, MongoDB, tabel en Graph API's) en andere specifieke tooadditional gegevensmodellen is beschikbaar in toekomstige Hallo.

Azure Cosmos DB heeft een schema agnostisch indexing-engine geschikt voor automatisch indexeren alle Hallo gegevens die het zonder dat een schema of secundaire indexen van de ontwikkelaar Hallo opgenomen. Hallo-engine wordt gebruikgemaakt van een set van logische index indelingen (omgekeerde, kolommen, structuur), die ook ontkoppelen opslagindeling Hallo van index Hallo en subsystemen verwerken van query's. Cosmos DB ook Hallo mogelijkheid toosupport een reeks API's en kabel protocollen heeft op een uitbreidbare manier en ze kan vertalen efficiënt toohello core data model (1) en Hallo logische index-indelingen (2) zodat u een unieke kunnen meerdere gegevensmodellen systeemeigen ondersteunen .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Is Azure Cosmos DB HIPAA compatibel?
Ja, Azure Cosmos DB HIPAA-compatibel is. HIPAA stelt vereisten voor hello gebruiken, de openbaarmaking en de beveiliging van individueel identificeerbare gezondheidsinformatie. Zie voor meer informatie, Hallo [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>Wat zijn de opslaglimieten Hallo van Azure DB die Cosmos?
Er is geen limiet toohello totale hoeveelheid gegevens die een container kunt opslaan in Azure Cosmos DB.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>Wat zijn de doorvoerlimieten Hallo van Azure DB die Cosmos?
Er is geen limiet toohello totale hoeveelheid doorvoer die een container in Azure Cosmos DB kan ondersteunen. Hallo sleutel idee wordt toodistribute uw workload ongeveer gelijkmatig tussen een voldoende aantal partitiesleutels.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Wat kost Azure Cosmos DB?
Raadpleeg voor meer informatie, toohello [Azure Cosmos DB prijsinformatie](https://azure.microsoft.com/pricing/details/cosmos-db/) pagina. Azure DB Cosmos gebruikskosten worden bepaald door Hallo aantal ingerichte containers, het aantal uren Hallo Hallo containers zijn online en Hallo ingerichte doorvoer voor elke container. Hallo term *containers* verwijst hier toohello DocumentDB API verzameling, Graph API grafiek, MongoDB-API-verzameling en tabel API tabellen. 

### <a name="is-a-free-account-available"></a>Is een gratis account beschikbaar?
Als u nieuwe tooAzure, kunt u zich aanmelden voor een [gratis Azure-account](https://azure.microsoft.com/free/), u hebt dan 30 dagen en en een tegoed tootry alle hello Azure-services. Als u een Visual Studio-abonnement hebt, bent u ook in aanmerking komen voor [gratis Azure-tegoed](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse voor een Azure-service. 

U kunt ook Hallo [Azure Cosmos DB Emulator](local-emulator.md) toodevelop en test de toepassing lokaal voor vrijmaken, zonder te maken van een Azure-abonnement. Wanneer u tevreden bent over hoe uw toepassing in Azure Cosmos DB Emulator Hallo werkt, kunt u een Azure DB die Cosmos-account in Hallo cloud toousing overschakelen.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Hoe kan ik aanvullende ondersteuning voor Azure Cosmos DB krijgen?
Als u hulp nodig hebt, bereiken op toous [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb) of Hallo [MSDN-forum](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), of een gesprek voert chatten met hello Azure Cosmos DB engineeringteam plannen door het verzenden van e-mail te[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Instellen van Azure DB die Cosmos
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Hoe meld ik me voor Azure Cosmos DB?
Azure Cosmos DB is beschikbaar in hello Azure-portal. Eerst zich registreren voor een Azure-abonnement. Nadat u zich hebt aangemeld, kunt u een DocumentDB-API toevoegen, Graph-API (Preview), tabel-API (Preview) of MongoDB API account tooyour Azure-abonnement.

### <a name="what-is-a-master-key"></a>Wat is een hoofdsleutel?
Een hoofdsleutel is een token tooaccess beveiliging van alle resources voor een account. Personen met Hallo sleutel hebben lees- en schrijftoegang tooall resources in Hallo databaseaccount. Wees voorzichtig met het distribueren van hoofdsleutels. Hallo primaire en secundaire hoofdsleutel zijn beschikbaar op Hallo **sleutels** blade Hallo [Azure-portal][azure-portal]. Zie voor meer informatie over sleutels [weergeven, kopiëren en opnieuw genereren toegangstoetsen](manage-account.md#keys).

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>Wat zijn Hallo-regio's die PreferredLocations kan worden ingesteld op? 
Hallo PreferredLocations waarde kan worden ingesteld op tooany Hallo Azure regio's waarin Cosmos DB beschikbaar is. Zie voor een lijst met beschikbare regio's, [Azure-regio's](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>Is er iets die ik houden moet rekening wanneer u gegevens over Hallo wereld via hello Azure-datacenters verdeeld? 
Azure Cosmos DB aanwezig is in alle regio's Azure als opgegeven op Hallo [Azure-regio's](https://azure.microsoft.com/regions/) pagina. Omdat het Hallo-Kernservice, heeft elke nieuwe datacenter de aanwezigheid van een Azure Cosmos DB. 

Vergeet niet dat Azure Cosmos DB soevereine en government clouds respecteert bij het instellen van een regio. Dat wil zeggen, als u een account in een soevereine regio maken, niet te repliceren buiten die soevereine regio. U kunt replicatie naar andere locaties soevereine van een externe account op deze manier niet inschakelen. 

## <a name="develop-against-hello-documentdb-api"></a>Tegen Hallo DocumentDB API ontwikkelen

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>Hoe start ontwikkelen van toepassingen met DocumentDB API Hallo?
DocumentDB-API van Microsoft is beschikbaar in Hallo [Azure-portal][azure-portal]. Eerst moet u aanmelden voor een Azure-abonnement. Zodra u zich voor een Azure-abonnement aanmelden, kunt u DocumentDB API container tooyour Azure-abonnement toevoegen. Zie voor instructies over het toevoegen van een account voor Azure Cosmos DB [Azure DB die Cosmos-databaseaccount maken](create-documentdb-dotnet.md#create-account). Als u een DocumentDB-account in de afgelopen Hallo had, hebt u nu een Cosmos-DB Azure-account. 

Er zijn [SDK's](documentdb-sdk-dotnet.md) beschikbaar voor .NET, Python, Node.js, JavaScript en Java. Ontwikkelaars kunnen ook gebruik Hallo [RESTful HTTP API's](/rest/api/documentdb/) toointeract met Azure Cosmos DB resources uit verschillende platforms en talen.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>Kan ik een aantal vooraf gedefinieerde voorbeelden tooget een goed uitgangspunt openen?
Voorbeelden voor Hallo DocumentDB API [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), en [Python](documentdb-python-samples.md) SDK's zijn beschikbaar op GitHub.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>Ondersteunt Hallo DocumentDB API-ondersteuning schemavrije gegevens uit een database?
Ja, DocumentDB API Hallo kan toepassingen toostore willekeurige JSON-documenten zonder schemadefinities of hints. Gegevens zijn onmiddellijk beschikbaar voor de query wordt uitgevoerd via hello Azure Cosmos DB SQL-QueryInterface.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>Hallo DocumentDB API biedt ondersteuning voor ACID-transactions?
Ja, Hallo DocumentDB API biedt ondersteuning voor transacties van tussen meerder documenten uitgedrukt in JavaScript opgeslagen procedures en triggers. Transacties zijn binnen het bereik van tooa één partitie binnen elke verzameling en uitgevoerd met ACID-semantiek als 'Alles of niets,' geïsoleerd van andere code en gebruikersaanvragen aanvragen voor het gelijktijdig worden uitgevoerd. Als er uitzonderingen worden veroorzaakt Hallo serverzijde uitvoering van JavaScript-toepassingscode, Hallo hele transactie teruggedraaid. Zie voor meer informatie over transacties [Database programmatransacties](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>Wat is een verzameling?
Een verzameling is een groep van documenten en hun bijbehorende JavaScript-toepassingslogica. Een verzameling is een factureerbare entiteit waar hello [kosten](performance-levels.md) wordt bepaald door Hallo doorvoer en opslag gebruikt. Verzamelingen kunnen een of meer partities of servers omvatten en kunnen worden geschaald toohandle vrijwel onbeperkte hoeveelheid opslag of doorvoer.

Verzamelingen zijn ook Hallo factureringsentiteiten voor Azure Cosmos DB. Elke verzameling wordt per uur gefactureerd op basis van de ingerichte doorvoer Hallo en opslagruimte gebruikt. Zie voor meer informatie [prijzen van Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>Hoe maak ik een database?
U kunt databases maken met behulp van Hallo [Azure-portal](https://portal.azure.com), zoals beschreven in [een verzameling toevoegen](create-documentdb-dotnet.md#create-collection), een Hallo [Azure Cosmos DB SDK's](documentdb-sdk-dotnet.md), of Hallo [REST-API's](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>Hoe stel ik gebruikers en machtigingen in?
U kunt gebruikers en machtigingen maken met behulp van een Hallo [Cosmos DB API SDK's](documentdb-sdk-dotnet.md) of Hallo [REST-API's](/rest/api/documentdb/).  

### <a name="does-hello-documentdb-api-support-sql"></a>Hallo DocumentDB API biedt ondersteuning voor SQL?
Hallo SQL-querytaal is een uitgebreide subset van Hallo queryfunctionaliteit die wordt ondersteund door SQL. Hello Azure Cosmos DB SQL-querytaal biedt geavanceerde hiërarchische en relationele operators en uitbreidingsmogelijkheden via op basis van JavaScript, door gebruiker gedefinieerde functies (UDF's). JSON-grammatica biedt de mogelijkheid voor het JSON-documenten te modelleren als structuren met gelabelde knooppunten, die worden gebruikt door zowel hello Azure Cosmos DB automatische indexering technieken en Hallo SQL-querydialect van Azure Cosmos-database. Zie voor informatie over het gebruik van SQL-grammatica Hallo [QueryDocumentDB] [ query] artikel.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>Hallo DocumentDB API-ondersteuning SQL aggregatiefuncties ondersteunt?
Hallo DocumentDB API ondersteunt lage latentie aggregatie op elke schaal via statistische functies `COUNT`, `MIN`, `MAX`, `AVG`, en `SUM` via Hallo SQL-grammatica. Zie voor meer informatie [statistische functies](documentdb-sql-query.md#Aggregates).

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>Hoe biedt DocumentDB API Hallo gelijktijdigheid?
Hallo DocumentDB API biedt ondersteuning voor Optimistisch gelijktijdigheidbeheer (OCC) via HTTP-entity-tags of ETags. Elke DocumentDB-API-resource heeft een ETag en Hallo ETag is ingesteld op Hallo server telkens wanneer een document wordt bijgewerkt. Hallo ETag-kop en de huidige waarde Hallo worden opgenomen in alle antwoordberichten. ETags kan worden gebruikt met Hallo If-Match-header tooallow Hallo server toodecide of een resource moet worden bijgewerkt. Hallo If-Match-waarde is Hallo ETag-waarde toobe gecontroleerd. Als Hallo ETag-waarde overeenkomt met Hallo server ETag-waarde, wordt Hallo resource bijgewerkt. Als Hallo ETag niet meer actueel is, Hallo-server wordt geweigerd Hallo opnieuw met een ' HTTP 412 Precondition failure ' antwoordcode. Hallo client haalt vervolgens opnieuw Hallo resource tooacquire Hallo huidige ETag-waarde voor Hallo resource. Bovendien kan ETags worden gebruikt met Hallo If-None-Match-header toodetermine, of een opnieuw ophalen van een bron die nodig is.

Optimistische gelijktijdigheid in .NET, gebruik Hallo toouse [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) klasse. Zie voor een voorbeeld .NET [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) in Hallo DocumentManagement voorbeeld op GitHub.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>Hoe voer ik transacties in DocumentDB API Hallo uit?
Hallo DocumentDB API biedt ondersteuning voor taalgeïntegreerde transacties via in JavaScript opgeslagen procedures en triggers. Alle databasebewerkingen in scripts worden uitgevoerd onder snapshot-isolatie. Als dit een verzameling van één partitie is, is Hallo uitvoering binnen het bereik toohello verzameling. Als het Hallo-verzameling is gepartitioneerd, Hallo uitvoering binnen het bereik toodocuments Hello is dezelfde partitiesleutel waarde binnen het Hallo-verzameling. Een momentopname van Hallo documentversies (ETags) is die is genomen op Hallo Hallo transactie is gestart en wordt alleen uitgevoerd als Hallo script kan worden uitgevoerd. Als Hallo JavaScript een fout genereert, Hallo transactie wordt teruggedraaid. Zie voor meer informatie [serverzijde JavaScript programmeren voor Azure Cosmos DB](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Hoe kan ik bulksgewijs invoegen documenten naar Cosmos DB?
U kunt bulksgewijs invoegen documenten naar Azure Cosmos DB op twee manieren:

* Hallo hulpprogramma voor gegevensmigratie, zoals beschreven in [hulpprogramma voor migratie van Database voor Azure Cosmos DB](import-data.md).
* Opgeslagen procedures, zoals beschreven in [serverzijde JavaScript programmeren voor Azure Cosmos DB](programming.md).

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>Hallo DocumentDB API ondersteunt resourcekoppelingen?
Ja, omdat Azure Cosmos DB een RESTful-service, resourcekoppelingen onveranderbaar zijn en kunnen in de cache worden opgeslagen. DocumentDB-API-clients kunnen een header 'If-None-Match' opgeven voor leesbewerkingen voor een resource-achtige document of een verzameling en vervolgens hun lokale kopieën werken nadat Hallo serverversie is gewijzigd.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>Is een lokaal exemplaar van DocumentDB API beschikbaar?
Ja. Hallo [Azure Cosmos DB Emulator](local-emulator.md) biedt een hoogwaardige emulatie van Hallo Cosmos-DB-service. Deze functionaliteit die is identiek tooAzure Cosmos DB, inclusief ondersteuning voor het maken en uitvoeren van query's JSON-documenten, het inrichten van ondersteunt en schalen van verzamelingen en uitvoering van opgeslagen procedures en triggers. U kunt ontwikkelen en testen van toepassingen met behulp van hello Azure Cosmos DB Emulator en deze tooAzure op een wereldwijde schaal implementeren door het maken van een configuratie voor één toohello verbindingseindpunt voor Azure Cosmos DB wijzigen.

## <a name="develop-against-hello-api-for-mongodb"></a>Tegen Hallo API ontwikkelen voor MongoDB
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>Wat is Azure Cosmos DB-API voor MongoDB Hallo?
Hello Azure Cosmos DB-API voor MongoDB is een compatibiliteitslaag dat toepassingen tooeasily toestaat en transparant Hallo systeemeigen Azure Cosmos DB database-engine communiceren via het bestaande, community ondersteund Apache MongoDB APIs en stuurprogramma's. Ontwikkelaars kunnen nu gebruikmaken van bestaande MongoDB hulpprogramma ketens en vaardigheden toobuild toepassingen die van Azure Cosmos-database gebruikmaken. Ontwikkelaars profiteren van Hallo unieke mogelijkheden van Azure Cosmos DB, waaronder onderhoud voor automatisch indexeren, back-up en back-financieel service level agreements (Sla).

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>Hoe kan ik toomy API voor MongoDB-database verbinden?
Hallo snelste manier tooconnect toohello Azure Cosmos DB-API voor MongoDB toohead via toohello is [Azure-portal](https://portal.azure.com). Ga tooyour account en klik vervolgens op Hallo linkernavigatievenster menu **Quick Start**. Snel starten is Hallo aanbevolen manier tooget code codefragmenten tooconnect tooyour-database. 

Azure Cosmos DB zorgt er strenge beveiligingsvereisten en standaarden. Azure DB Cosmos-accounts, verificatie en veilige communicatie via SSL vereisen, dus wees zeker toouse TLSv1.2.

Zie voor meer informatie [tooyour-API voor MongoDB-database verbinding](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>Zijn er extra foutcodes voor een API voor MongoDB-database?
Toevoeging toohello algemene MongoDB foutcodes heeft Hallo MongoDB-API een eigen specifieke foutcodes:


| Fout               | Code  | Beschrijving  | Oplossing  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | Totaal aantal aanvraageenheden verbruikt Hallo Hallo ingerichte aanvraag-eenheid tarief voor de verzameling Hallo heeft overschreden en is beperkt. | Schalen Hallo doorvoer van Hallo-verzameling van hello Azure-portal of u opnieuw probeert te overwegen. |
| ExceededMemoryLimit | 16501 | Als een multitenant-service heeft Hallo bewerking van de client Hallo geheugen aandeel overschreden. | Hallo-bereik van Hallo bewerking via de meest beperkende querycriteria verminderen of neem contact op met ondersteuning van Hallo [Azure-portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>Voorbeeld:  *&nbsp; &nbsp; &nbsp; &nbsp;db.getCollection('users').aggregate ([<br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;{$match: {naam: 'Andy'}}, <br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;{$sort: {leeftijd: -1} }<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Ontwikkelen met Hallo tabel-API (Preview)

### <a name="terms"></a>Voorwaarden 
Hello Azure Cosmos DB: tabel-API (Preview) toohello premium aanbieding door Azure Cosmos DB voor tabel ondersteuning aangekondigd op Build 2017 verwijst. 

Hallo standaardtabel SDK is Hallo bestaande Azure Storage tabel SDK. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>Hoe kan ik de nieuwe tabel-API (Preview) aanbieding hello gebruiken? 
Hello Azure Cosmos DB tabel API is beschikbaar in Hallo [Azure-portal][azure-portal]. Eerst moet u aanmelden voor een Azure-abonnement. Nadat u zich hebt aangemeld, kunt u een tabel-API van Azure Cosmos DB account tooyour Azure-abonnement toevoegen en vervolgens tabellen tooyour account toevoegen. 

Tijdens de evaluatieperiode Hallo wanneer [SDK's](../cosmos-db/table-sdk-dotnet.md) zijn beschikbaar voor .NET, u kunt aan de slag door te voeren Hallo [tabel API](../cosmos-db/create-table-dotnet.md) snel starten-artikel.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>Moet ik een nieuwe SDK toouse Hallo tabel-API (Preview)? 
Ja, Hallo [Windows Azure-opslag Premium Table (Preview) SDK](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) beschikbaar is op NuGet. Aanvullende informatie is beschikbaar op Hallo [Azure Cosmos DB tabel .NET API: downloaden en opmerkingen bij de release](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) pagina. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>Hoe ik feedback geven over Hallo SDK of fouten?
U kunt uw feedback in een van de volgende manieren Hallo delen:

* [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [MSDN-forum](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [StackOverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>Wat is de verbindingsreeks Hallo dat ik toouse tooconnect toohello tabel-API (Preview) nodig?
Hallo-verbindingsreeks is:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
Hallo-verbindingsreeks kunt u krijgen via Hallo sleutels pagina in hello Azure-portal. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>Hoe ik Hallo configuratie-instellingen voor Hallo aanvraag opties in Hallo nieuwe tabel API (Preview) overschrijven?
Zie voor informatie over configuratie-instellingen, [mogelijkheden van Azure DB die Cosmos](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Hallo-instellingen kunt u wijzigen door ze toe te voegen tooapp.config in Hallo appSettings gedeelte op Hallo-clienttoepassing.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>Zijn er wijzigingen voor klanten die Hallo bestaande standaard tabel SDK?
Geen. Er zijn geen wijzigingen voor bestaande of nieuwe klanten die Hallo bestaande standaard tabel SDK gebruiken. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>Hoe kan ik gegevens in een tabel die is opgeslagen in Azure Cosmos DB voor gebruik met tabel-API (revisie) Hallo bekijken? 
U kunt hello Azure portal toobrowse Hallo gegevens gebruiken. U kunt ook Hallo tabel-API (Preview)-code of Hallo-hulpprogramma's die worden vermeld in het volgende antwoord hello gebruiken. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>Welke hulpprogramma's werken met Hallo tabel-API (Preview)? 
U kunt Hallo oudere versie van Azure Explorer (0.8.9) gebruiken.

Hulpprogramma's met Hallo flexibiliteit tootake eerder een verbindingsreeks in de opgegeven indeling Hallo kan ondersteunen Hallo nieuwe tabel-API (Preview). Een lijst met hulpprogramma's voor tabel vindt u op Hallo [hulpprogramma's voor Azure Storage Client](../storage/common/storage-explorers.md) pagina. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>PowerShell of Azure CLI werken met Hallo nieuwe tabel API (Preview)?
We zullen tooadd ondersteuning voor PowerShell en Azure CLI voor tabel-API (Preview). 

### <a name="is-hello-concurrency-on-operations-controlled"></a>Is Hallo gelijktijdigheid van bewerkingen die worden beheerd?
Ja, optimistische gelijktijdigheid wordt opgegeven via Hallo gebruik van Hallo ETag-mechanisme. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>Wordt hello model voor OData-query ondersteund voor entiteiten? 
Ja, ondersteunt Hallo tabel-API (Preview) de OData-query en LINQ-query. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>Kan ik Azure standaardtabel toohello verbinden en hello nieuwe premium tabel-API (Preview) naast elkaar in Hallo dezelfde toepassing? 
Ja, u verbinding kunt maken met het maken van twee afzonderlijke exemplaren van Hallo CloudTableClient, elke wijzen tooits eigenaar URI via Hallo-verbindingsreeks.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>Hoe Migreer ik een bestaande Azure Table storage toepassing toothis nieuwe aanbieding
tootake profiteren van nieuwe tabel API-aanbieding Hallo op uw bestaande opslag tabelgegevens, neem contact op met [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com). 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>Wat Hallo roadmap voor deze service is en wanneer bieden u andere standaard tabel API-functies?
We zullen tooadd ondersteuning voor SAS-tokens, ServiceContext, statistieken, Client side versleuteling, Analytics en andere functies zoals we gaan naar de algemene beschikbaarheid. U kunt feedback op [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api). 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>Hoe wordt uitbreiding van Hallo opslaggrootte gedaan voor deze service, bijvoorbeeld wordt gestart met  *n*  GB aan gegevens en Mijn too1 TB na verloop van tijd zal toenemen? 
Azure Cosmos DB is ontworpen tooprovide onbeperkte opslag via Hallo gebruik van horizontaal schalen. Hallo-service kunt bewaken en effectief meer opslagruimte. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>Hoe bewaak ik Hallo tabel-API (Preview) aanbieding
Hallo tabel-API (Preview) kunt u **metrische gegevens** deelvenster toomonitor aanvragen en opslaggebruik. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>Hoe bereken ik Hallo doorvoer die ik nodig?
U kunt Hallo capaciteit estimator toocalculate hello TableThroughput die zijn voor Hallo-bewerkingen vereist. Zie voor meer informatie [schatting Aanvraageenheden en gegevensopslag](https://www.documentdb.com/capacityplanner). In het algemeen kunt u uw entiteit als JSON vertegenwoordigen en Hallo getallen opgeven voor uw bewerkingen. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>Kan ik gebruiken Hallo nieuwe tabel-API (Preview) SDK lokaal met Hallo-emulator?
Ja, kunt u Hallo tabel-API (Preview) met de lokale emulator Hallo wanneer u nieuwe SDK Hallo. nieuwe toodownload-emulator te gaan[gebruik hello Azure Cosmos DB Emulator voor lokale ontwikkeling en tests](local-emulator.md). Hallo StorageConnectionString waarde in app.config moet toobe:

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>Kan mijn bestaande toepassing Hello tabel-API (Preview) werken? 
Hallo surface area van Hallo nieuwe tabel-API (Preview) is compatibel met bestaande Azure standard-tabel SDK via Hallo maken, verwijderen, bijwerken en bewerkingen in Hallo .NET API query Hallo. Zorg ervoor dat u beschikt over een rijsleutel omdat Hallo tabel-API (Preview) is zowel een partitiesleutel als een rijsleutel vereist. We ook plannen tooadd meer ondersteuning voor SDK als we gaan naar GA van deze serviceaanbieding.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>Heb ik nodig toomigrate mijn bestaande Azure-tabel gebaseerde toepassingen toohello nieuwe SDK als ik wil niet toouse Hallo tabel-API (Preview)-functies?
Nee, kunt u maken en gebruiken van bestaande standaardtabel activa zonder onderbreking van elk type. Echter, als u geen Hallo nieuwe tabel API (Preview) gebruikt, kan niet profiteert u automatische index hello, Hallo aanvullende consistentie optie of distributielijsten. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>Hoe voeg replicatie van gegevens Hallo in Hallo premium, tabel-API (Preview) over meerdere regio's van Azure?
U kunt hello Azure Cosmos DB portal [globale replicatie-instellingen](tutorial-global-distribution-documentdb.md#portal) tooadd regio's die geschikt voor uw toepassing zijn. toodevelop een globaal gedistribueerde toepassing, moet u ook uw toepassing met Hallo PreferredLocation informatie set toohello lokale regio voor het ontwikkelen van de lage latentie voor lezen toevoegen. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>Hoe wijzig ik Hallo primaire schrijven regio voor Hallo-account in Hallo premium tabel-API (Preview)
U kunt gebruiken hello Azure Cosmos DB globale replicatie portal deelvenster tooadd een regio en vervolgens een toohello vereist regio failover. Zie voor instructies [ontwikkelen met meerdere landen/regio Azure Cosmos DB accounts](regional-failover.md). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>Hoe kan ik mijn voorkeur lezen regio's voor de lage latentie configureren wanneer ik mijn gegevens distribueert? 
toohelp lezen van de lokale locatie hello, Hallo PreferredLocation-toets gebruiken in Hallo app.config-bestand. Hallo tabel-API (Preview) genereert een fout voor bestaande toepassingen als LocationMode is ingesteld. Deze code niet verwijderen omdat Hallo premium tabel-API (Preview) neemt over deze informatie uit Hallo app.config-bestand. Zie voor meer informatie [mogelijkheden van Azure DB die Cosmos](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>Hoe moet ik denken dat zij consistentieniveaus in Hallo tabel-API (Preview)? 
Azure Cosmos DB biedt goed gemotiveerd verschillen tussen de consistentie, beschikbaarheid en latentie. Azure Cosmos DB biedt vijf consistentieniveaus tooTable API (Preview) ontwikkelaars, zodat u kunt Hallo rechts consistentie model op tabelniveau Hallo kiezen en afzonderlijke aanvragen maken tijdens het Hallo-gegevens opvragen. Wanneer een client verbinding maakt, kunt het niveau van een consistentiecontrole opgeven. U kunt Hallo niveau via Hallo app.config-instelling voor Hallo-waarde van Hallo TableConsistencyLevel sleutel wijzigen. 

Hallo tabel-API (Preview) biedt lage latentie leest met 'lezen uw eigen schrijfbewerkingen' met sessieconsistentie als Hallo standaard. Zie voor meer informatie [consistentieniveaus](consistency-levels.md). 

Azure Table storage biedt standaard sterke consistentie binnen een regio en Eventual consistentie op Hallo secundaire locaties. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>Biedt Azure Cosmos DB meer consistentieniveaus dan standaardtabellen?
Ja, voor informatie over hoe toobenefit van Hallo aard van Azure Cosmos DB gedistribueerde, Zie [consistentieniveaus](consistency-levels.md). Omdat garanties worden geboden voor consistentieniveaus hello, kunt u ze kunt gebruiken met vertrouwen. Zie voor meer informatie [mogelijkheden van Azure DB die Cosmos](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>Wanneer de algemene distributie is ingeschakeld, hoe lang duurt tooreplicate Hallo gegevens?
We doorvoeren Hallo gegevens blijvend in de lokale regio Hallo en push Hallo gegevensgebieden tooother onmiddellijk binnen een paar milliseconden. Deze replicatie is afhankelijk van de Hallo round trip-tijd (RTT) van Hallo datacenter. Zie toolearn meer informatie over Hallo algemene distributie-mogelijkheden van Azure Cosmos DB [Azure Cosmos DB: een wereldwijd gedistribueerde database-service op Azure](distribute-data-globally.md).

### <a name="can-hello-read-request-consistency-level-be-changed"></a>Kan de Hallo leesaanvraag consistentieniveau gewijzigd?
U kunt met Azure Cosmos DB Hallo consistentieniveau instellen op Hallo container niveau (op Hallo tabel). Hallo SDK gebruikt, kunt u Hallo niveau wijzigen door het Hallo-waarde voor de sleutel TableConsistencyLevel in Hallo app.config-bestand op te geven. Hallo mogelijke waarden zijn: sterk, gebonden veroudering sessie, consistente voorvoegsel en Eventual. Zie voor meer informatie [gegevens instelbare consistentieniveaus in Azure Cosmos DB](consistency-levels.md). Hallo sleutel idee is kan niet op in te stellen Hallo aanvraag consistentie niveau meer zijn dan instelling voor de tabel Hallo Hallo. Bijvoorbeeld, instellen u niet Hallo consistentieniveau voor de tabel op Eventual hello en Hallo aanvraag consistentie op sterke. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>Hoe wordt Hallo premium tabel-API (Preview) account verwerkt failover als een regio uitgeschakeld wordt? 
Hallo premium tabel-API (Preview) voortbouwt op Hallo globaal gedistribueerde platform van Azure Cosmos DB. tooensure dat uw toepassing datacenter uitvaltijd, kan tolereren inschakelen ten minste één meer regio voor Hallo-account in hello Azure Cosmos DB portal [ontwikkelen met meerdere landen/regio Azure Cosmos DB accounts](regional-failover.md). U kunt Hallo prioriteit van Hallo regio instellen met behulp van de portal Hallo [ontwikkelen met meerdere landen/regio Azure Cosmos DB accounts](regional-failover.md). 

U kunt zoveel regio als u wilt gebruiken voor het Hallo-account en bepalen waar deze tooby bieden een failover-prioriteit failover toevoegen. Uiteraard toouse Hallo-database, moet u er een toepassing tooprovide te. Wanneer u doet dit, krijgen uw klanten geen uitvaltijd. Hallo client SDK wordt automatisch homing. Dat wil zeggen, kan het Hallo-regio die niet actief is en automatisch een nieuw gebied toohello failover detecteren.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>Hallo premium tabel-API (Preview) is ingeschakeld voor back-ups
Ja, Hallo premium tabel-API (Preview) voortbouwt op Hallo platform van Azure DB die Cosmos voor back-ups. Back-ups worden automatisch gemaakt. Zie voor meer informatie [Online back-up en herstel met Azure Cosmos DB](online-backup-and-restore.md).

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Hallo tabel-API (Preview) alle kenmerken van een entiteit index standaard
Ja, worden alle kenmerken van een entiteit geïndexeerd standaard. Zie voor meer informatie [Azure Cosmos DB: beleid indexeren](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>Betekent dit dat ik heb geen toocreate meerdere indexen toosatisfy Hallo-query's? 
Ja, biedt Azure Cosmos DB automatische indexeren van alle kenmerken zonder eventuele schemadefinitie. Deze automatisering wordt vrijgemaakt ontwikkelaars toofocus op Hallo-toepassing in plaats van op index maken en beheren. Zie voor meer informatie [Azure Cosmos DB: beleid indexeren](indexing-policies.md).

### <a name="can-i-change-hello-indexing-policy"></a>Kan ik Hallo indexeringsbeleid wijzigen?
Ja, kunt u Hallo indexeringsbeleid dankzij de indexdefinitie Hallo. Zie voor meer informatie [mogelijkheden van Azure DB die Cosmos](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). U moet tooproperly coderen en escape Hallo-instellingen. 

Tekenreeks json-indeling in Hallo app.config-bestand:
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>Azure Cosmos-database als een platform lijkt toohave veel mogelijkheden, zoals sorteren, statistische functies, hiërarchie en andere functionaliteit. U wilt toevoegen deze mogelijkheden toohello tabel API? 
In de preview, Hallo tabel API Hallo biedt dezelfde functionaliteit als Azure Table storage een query. Azure Cosmos DB biedt ook ondersteuning voor sorteren, statistische functies, georuimtelijke query hiërarchie en een groot aantal ingebouwde functies. We bieden aanvullende functionaliteit in Hallo API van de tabel in een toekomstige service-update. Zie voor meer informatie [SQL-query's voor Azure Cosmos DB DocumentDB API](../documentdb/documentdb-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>Wanneer moet ik TableThroughput wijzigen voor Hallo tabel-API (Preview)?
Wanneer een van de volgende voorwaarden Hallo van toepassing is, moet u TableThroughput wijzigen:
* U voert een uitpakken, transformeren en laden (ETL) van gegevens, of het gewenste tooupload grote hoeveelheden gegevens in korte tijd. 
* U moet meer doorvoer van Hallo-container op Hallo back-end. Bijvoorbeeld, ziet u dat Hallo gebruikt doorvoer meer dan Hallo ingerichte doorvoer is en u zijn ophalen beperkt. Zie voor meer informatie [Set doorvoer voor Azure Cosmos DB containers](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>Kan ik opschalen of terugschroeven Hallo doorvoer van mijn tabel tabel-API (Preview)? 
Ja, kunt u hello Azure Cosmos DB portal scale deelvenster tooscale Hallo doorvoer. Zie voor meer informatie [Set doorvoer](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>Is een standaard die tablethroughput voor nieuw ingerichte tabellen ingesteld?
Ja, als u Hallo TableThroughput via app.config niet overschrijven en gebruik niet een vooraf gemaakte container in Azure Cosmos DB, Hallo service maakt een tabel met doorvoersnelheid van 400.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>Is er een wijziging van de prijzen voor bestaande klanten van Hallo standaard tabel API?
Geen. Er is geen wijziging in de prijs voor bestaande klanten die standaard tabel-API. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Hoe wordt Hallo prijs berekend voor Hallo tabel-API (Preview)? 
Hallo prijs is afhankelijk van Hallo TableThroughput toegewezen. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>Hoe u verwerkt beperking op Hallo tabellen in de tabel-API (Preview) biedt? 
Snelheid van aanvragen voor Hallo Hallo capaciteit van Hallo ingerichte doorvoer voor onderliggende container Hallo overschrijdt, ontvangt u een fout als Hallo SDK door het toepassen van beleid voor opnieuw proberen Hallo Hallo aanroep probeert.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>Waarom moet ik een doorvoer naast PartitionKey en RowKey tootake profiteren van Hallo premium tabel-API (Preview) aanbod van Azure DB die Cosmos toochoose?
Als u een in Hallo app.config-bestand niet opgeeft, Azure Cosmos-DB een standaard-doorvoer ingesteld voor de container. 

Azure Cosmos DB biedt garanties voor prestaties en de latentie met bovengrenzen van bewerking. Deze garantie is mogelijk wanneer het Hallo-engine governance op Hallo-tenant bewerkingen kunt afdwingen. TableThroughput instelling zorgt ervoor dat u Hallo gegarandeerd doorvoer en latentie, omdat Hallo platform deze capaciteit gereserveerd en wordt gegarandeerd dat operationele geslaagd. 

Hallo doorvoer specificatie gebruikt, kunt u elastisch toobenefit van Hallo seizoensgebonden van uw toepassing wijzigen, Hallo doorvoer behoeften en kosten besparen.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>Azure-opslag-SDK is zeer goedkope voor mij, omdat ik betaalt u alleen toostore Hallo gegevens en het ik zelden opvragen. Hallo nieuwe Azure Cosmos DB aanbieding lijkt toobe opladen mij ondanks dat ik niet heb één transactie uitgevoerd of iets opgeslagen. Kunt u Leg?

Azure Cosmos DB is ontworpen toobe een globaal gedistribueerd, op basis van SLA-systeem met garanties met betrekking tot beschikbaarheid, latentie en doorvoer. Bij het reserveren van doorvoer in Azure DB die Cosmos is gegarandeerd, in tegenstelling tot Hallo doorvoer van andere systemen. Azure Cosmos DB biedt aanvullende functies die klanten hebt aangevraagd, zoals secundaire indexen en distributielijsten. Tijdens de evaluatieperiode hello, bieden we een model doorvoer is geoptimaliseerd en uiteindelijk we een model opslag geoptimaliseerd toomeet tooprovide behoeften van onze klanten plannen. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>Krijg ik nooit een ' volledige ' quotamelding (waarmee wordt aangegeven dat een partitie vol is) wanneer ik opnemen van gegevens in de Table storage. Met de Hallo tabel-API (Preview) krijg ik dit bericht. Dit biedt mij beperken en dwingen mij toochange mijn bestaande toepassing?

Azure Cosmos-database is een SLA-systeem waarmee onbeperkte scale garanties met betrekking tot latentie, doorvoer, beschikbaarheid en consistentie. premium-prestaties gegarandeerd tooensure Zorg ervoor dat uw gegevensgrootte en een index beheerbare en schaalbare. limiet van 10 GB Hallo voor Hallo aantal entiteiten of items per partitiesleutel is tooensure wij goede zoekopdracht en query-prestaties. tooensure die uw toepassing geschaald ook goed voor Azure Storage, raden we u *niet* een hot partitie maken door alle informatie in een partitie op te slaan en het uitvoeren van query's. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>Dus PartitionKey en RowKey nog steeds met vereist zijn Hallo nieuwe tabel-API (Preview)? 
Ja. Omdat Hallo surface area van Hallo tabel-API (Preview) vergelijkbaar toothat Hallo tabelopslag SDK is, biedt de partitiesleutel Hallo een efficiënte manier toodistribute Hallo-gegevens. Hallo rijsleutel is uniek zijn binnen deze partitie. Hallo rij basisbehoeften toobe aanwezig zijn en mag niet null zijn als in Hallo standaard SDK. Hallo-lengte van RowKey is 255 bytes en Hallo lengte van PartitionKey is 100 bytes (toobe verhoogd snel too1 KB). 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Wat zijn de foutberichten Hallo voor Hallo tabel-API (Preview)?
Omdat deze preview compatibel met de standaardtabel hello is, wordt in de meeste van Hallo fouten toohello fouten van de standaardtabel Hallo toewijzen. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>Waarom ik ophalen beperkte bandbreedte wanneer ik probeer toocreate veel tabellen achter elkaar in Hallo tabel-API (Preview)?
Azure Cosmos-database is een SLA-systeem waarmee latentie, doorvoer, beschikbaarheid en consistentie wordt gegarandeerd. Omdat het een ingerichte systeem, reserveren het van resources tooguarantee deze vereisten. Hallo snelle snelheid van het maken van tabellen is gedetecteerd en beperkt. U wordt aangeraden dat u hello snelheid van het maken van tabellen bekijkt en tooless dan 5 per minuut verlagen. Houd er rekening mee dat Hallo tabel-API (Preview) is een ingerichte systeem. Hallo moment dat u het inrichten, moet u toopay voor begint. 

## <a name="develop-against-hello-graph-api-preview"></a>Ontwikkelen tegen Hallo Graph API (Preview)
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>Hoe kan ik Hallo-functionaliteit van Graph API (Preview) tooAzure Cosmos DB toepassen?
U kunt een uitbreiding bibliotheek tooapply Hallo functionaliteit van Graph API (Preview) kunt gebruiken. Deze bibliotheek Microsoft Azure-grafieken wordt genoemd, en is beschikbaar in NuGet. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Lijkt Hallo Gremlin grafiek traversal taal die u ondersteunt. Bent u van plan tooadd meer vormen van de query?
Ja, plan we tooadd andere mechanismen voor toekomstige Hallo query. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>Hoe kan ik Hallo nieuwe Graph-API (Preview) aanbieding gebruiken? 
tooget gestart en volledige Hallo [Graph API](../cosmos-db/create-graph-dotnet.md) snel starten-artikel.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>Vragen van klanten DocumentDB
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>Waarom verplaatst u tooAzure Cosmos DB? 

Azure Cosmos DB is Hallo volgende big leap globaal gedistribueerde geschaald cloud-databases. Als een DocumentDB-klant hebt u nu toegang toohello innovatieve system en mogelijkheden die worden aangeboden door Azure Cosmos DB.

Azure Cosmos DB gestart als 'Project Florence' in 2010 tooaddress Hallo-knelpunten managementoverhead voor ontwikkelaars bij het bouwen van grootschalige toepassingen binnen Microsoft. Hallo uitdagingen bij het bouwen van globaal gedistribueerde apps zijn niet uniek tooMicrosoft zodat we Hallo eerste generatie van deze technologie beschikbaar gesteld in 2015 tooAzure ontwikkelaars in Hallo vorm van Azure DocumentDB. 

Sinds die tijd hebt we nieuwe functies toegevoegd en belangrijke nieuwe functies geïntroduceerd. Azure Cosmos DB is Hallo resultaat. Als onderdeel van deze release, DocumentDB klanten met hun gegevens automatisch en naadloos worden Azure DB die Cosmos-klanten. Deze mogelijkheden zijn in Hallo gebieden van Hallo core database-engine, evenals globale distribueren, elastische schaalbaarheid en de toonaangevende, uitgebreide Sla's. We hebben in het bijzonder hello Azure Cosmos DB database-engine tooefficiently kaart ontwikkeld alle populaire gegevensmodellen, type-systemen en API's toohello onderliggende data model van Azure Cosmos-database. 

Hallo huidige ontwikkelaars gerichte uiting van dit werk is nieuwe ondersteuning voor Hallo [Gremlin](../cosmos-db/graph-introduction.md) en [Table storage-API's](../cosmos-db/table-introduction.md). En dit is alleen Hallo begin. We zullen tooadd andere populaire API's en nieuwere gegevensmodellen gedurende een periode met meer ontwikkelingen in prestaties en de opslag op globale schaal. 

Het is belangrijk toopoint uit die Hallo DocumentDB [SQL-dialect](../documentdb/documentdb-sql-query.md) is slechts een van de Hallo veel API's die Hallo onderliggende Azure Cosmos DB kan ondersteunen. Voor ontwikkelaars die gebruikmaken van een volledig beheerde service zoals Azure Cosmos DB, hello alleen interface toohello-service is Hallo API's die beschikbaar worden gesteld door Hallo-service. Niets echt voor bestaande DocumentDB-klanten wordt gewijzigd. In Azure Cosmos DB krijgt u precies Hallo die dezelfde SQL-API die DocumentDB biedt. En nu (en in toekomstige Hallo), u toegang hebt tot andere mogelijkheden van eerder niet toegankelijk 

Een ander manifest van onze blijvende werk is uitgebreid Hallo basis voor globale en elastische schaalbaarheid van de doorvoer en opslag. Er zijn verschillende verbeteringen van de fundamentele toohello globale distributie subsysteem aangebracht. Een Hallo veel functies van dergelijke ontwikkelaars gerichte Hallo Consistent voorvoegsel consistentie model, waardoor een totale vijf goed gedefinieerde consistentie modellen is. We brengen veel meer interessante mogelijkheden hun. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>Wat kan ik toodo tooensure dat mijn DocumentDB-resources verder toorun Azure Cosmos DB nodig?

U moet toomake geen wijzigingen aan. Uw DocumentDB-resources zijn nu Azure Cosmos DB bronnen en er is geen serviceonderbreking Hallo bij verplaatsing is opgetreden.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>Wat wijzigingen doen ik toomake nodig voor mijn toowork app met Azure Cosmos DB?

Er zijn geen wijzigingen toomake. Klassen, naamruimten en NuGet-pakketnamen zijn niet gewijzigd. Zoals altijd adviseren we dat u de SDK's van toodate tootake profiteren van Hallo meest recente functies en verbeteringen. 

### <a name="whats-changed-in-hello-azure-portal"></a>Wat er gewijzigd in hello Azure-portal?

DocumentDB wordt niet meer weergegeven in de portal Hallo als een Azure-service. In plaats daarvan wordt een nieuw Azure DB die Cosmos-pictogram zoals weergegeven in Hallo volgende afbeelding. Alle collecties zijn beschikbaar, omdat deze zich vóór en u nog steeds doorvoer, consistentieniveaus wijzigen en monitor Sla's schalen kunt. Hallo-mogelijkheden van Data Explorer (Preview) zijn verbeterd. U kunt nu weergeven en bewerken van documenten, maken en query's uitvoeren en werken met opgeslagen procedures, triggers en UDF van één pagina, zoals wordt weergegeven in Hallo installatiekopie te volgen: 

![Hello Azure Cosmos DB verzamelingen blade](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>Zijn er wijzigingen toopricing?

Hallo kosten van uw app in Azure DB die Cosmos is uitgevoerd kunt u Nee, Hallo op dezelfde zoals deze was voordat.

### <a name="are-there-changes-toohello-slas"></a>Zijn er wijzigingen toohello Sla's?

Nee, Hallo serviceovereenkomsten voor beschikbaarheid, consistentie, latentie en doorvoer blijven ongewijzigd en nog steeds worden weergegeven in het Hallo-portal. Zie voor meer informatie [SLA voor Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/).
   
![To-do-app met voorbeeldgegevens](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
