---
title: aaaAzure Cosmos DB indexering beleid | Microsoft Docs
description: Begrijpen hoe indexeren werkt in Azure Cosmos DB. Meer informatie over hoe tooconfigure en wijzig Hallo indexeringsbeleid voor automatisch indexeren en betere prestaties.
keywords: hoe indexeren werkt, automatische indexeren, database indexeren
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Hoe biedt Azure Cosmos DB indexgegevens?

Standaard worden alle gegevens van Azure DB die Cosmos wordt geïndexeerd. En hoewel veel klanten tevreden toolet Azure Cosmos DB verwerken automatisch alle aspecten van het indexeren, Azure Cosmos DB biedt ook ondersteuning voor het opgeven van een aangepaste **beleid indexeren** voor verzamelingen tijdens het maken van. Indexing-beleid in Azure Cosmos DB zijn flexibelere en krachtigere dan secundaire indexen aangeboden op andere databaseplatforms,, omdat ze u ontwerpen en Hallo vorm van Hallo-index kunnen zonder verlies van schemaflexibiliteit aanpassen. toolearn indexeren werking in Azure Cosmos DB, moet u begrijpen dat door het indexeringsbeleid beheer, kunt u fijnmazig balans vinden tussen opslagoverhead voor indexering-, schrijf- en doorvoer van de query- en consistentie van de query.  

In dit artikel we Bekijk sluiten Azure Cosmos DB beleidsregels indexeren, hoe u kunt indexeringsbeleid aanpassen en Hallo-en nadelen gekoppeld. 

Na het lezen van dit artikel, moet u kunnen tooanswer Hallo vragen te volgen:

* Hoe kan ik Hallo eigenschappen tooinclude overschrijven of uitsluiten van het indexeren?
* Hoe kan ik Hallo index voor eventuele updates configureren?
* Hoe kan ik indexering tooperform Order By of bereik query's configureren?
* Hoe maak ik wijzigingen tooa verzameling indexeringsbeleid
* Hoe vergelijk ik opslag en prestaties van verschillende beleidsregels voor indexering

## <a id="CustomizingIndexingPolicy"></a>Hallo indexeringsbeleid van een verzameling aanpassen
Ontwikkelaars kunnen Hallo verschillen tussen de opslag, schrijven/queryprestaties en consistentie van de query, aanpassen door Hallo standaard indexering beleid op een verzameling Azure Cosmos DB en het configureren van Hallo aspecten te volgen.

* **Inclusief/exclusief paden naar/van de index en documenten**. Ontwikkelaars kunnen bepaalde documenten toobe uitgesloten of opgenomen in Hallo index bij Hallo invoegen of vervangen van toohello verzameling kiezen. Ontwikkelaars kunnen ook tooinclude kiezen of bepaalde JSON-eigenschappen ook uitsluiten paden (inclusief jokertekenpatronen) toobe geïndexeerd op documenten die zijn opgenomen in een index.
* **Configureren van verschillende typen Index**. Voor elk Hallo opgenomen paden, kunnen ontwikkelaars ook Hallo type index die ze nodig over een verzameling op basis van hun gegevens en de werkbelasting query verwacht en Hallo numerieke tekenreeks 'precisie' voor elk pad hebben opgeven.
* **Configureren van Index Update modi**. Azure Cosmos DB ondersteunt drie indexering modi die kunnen worden geconfigureerd via Hallo-beleid op een verzameling Azure Cosmos DB indexeren: Consistent Lazy en er is geen. 

Hallo .NET code codefragment wordt getoond hoe na een aangepast indexeringsbeleid tijdens het maken van een verzameling Hallo tooset. We instellen hier Hallo beleid met een bereikindex voor tekenreeksen en getallen op Hallo maximumprecisie. Dit beleid kunt ons Order By-query's uitvoeren op tekenreeksen.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> Hallo JSON-schema voor het indexeringsbeleid is gewijzigd met Hallo-release van REST-API-versie 2015-06-03 toosupport bereik indexen op tekenreeksen. Ondersteuning voor het nieuwe beleid schema Hallo .NET SDK 1.2.0 en Java, Python en Node.js SDK's 1.1.0. Oudere SDK's Hallo REST API-versie 2015-04-08 gebruiken en ondersteunen Hallo oudere schema van het beleid te indexeren.
> 
> Standaard indexeert Azure Cosmos DB numerieke eigenschappen en alle eigenschappen van een verbindingsreeks in documenten consistent met een hashindex met de bereikindex van een.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Hallo indexeringsbeleid met Hallo portal aanpassen

U kunt indexeren beleid van een verzameling met behulp van Azure-portal Hallo Hallo wijzigen. Open uw Azure DB die Cosmos-account in hello Azure-portal, selecteer uw verzameling in hello linkernavigatievenster menu klikt u op **instellingen**, en klik vervolgens op **indexeren beleid**. In Hallo **indexeren beleid** blade gewenste indexeringsbeleid wijzigen en klik vervolgens op **OK** toosave uw wijzigingen. 

### <a id="indexing-modes"></a>Database indexing-modi
Azure Cosmos DB ondersteunt drie indexering modi die kunnen worden geconfigureerd via Hallo-beleid op een verzameling Azure Cosmos DB – indexeren consistente, Lazy en geen.

**Consistente**: als een Azure DB die Cosmos-verzameling beleid is aangewezen als 'consistent', Hallo-query's in een bepaald Azure Cosmos DB verzameling Volg dezelfde consistentieniveau zoals gespecificeerd voor punt-leesbewerkingen hello (dat wil zeggen sterk, gebonden-verouderd, Hallo sessie of uiteindelijke). Hallo-index wordt synchroon als onderdeel van Hallo document update (dat wil zeggen invoegen, vervangen, bijwerken en verwijderen van een document in een verzameling Azure Cosmos DB) bijgewerkt.  Consistente indexeren biedt ondersteuning voor consistente query's op Hallo kosten van mogelijke vermindering in doorvoer van schrijfbewerkingen. Deze verlaging is een functie van Hallo unieke paden die toobe geïndexeerd moeten en Hallo 'consistentieniveau'. Consistente indexering modus is ontworpen voor werkbelastingen 'snel query schrijven onmiddellijk'.

**Vertraagde**: tooallow maximale document opname doorvoer, een verzameling Azure Cosmos DB kan worden geconfigureerd met de vertraagde consistentie; betekenis query's zijn uiteindelijk consistent is. Hallo-index wordt asynchroon bijgewerkt wanneer een verzameling Azure Cosmos DB is quiescent dat wil zeggen de doorvoercapaciteit van Hallo verzameling is niet volledig gebruikte tooserve gebruikersaanvragen. 'Opnemen nu query later' werkbelastingen vereisen concurrerende document opname zijn 'vertraagde' indexering modus afgestemd.

**Geen**: een verzameling die is gemarkeerd met Indexmodus van 'None' heeft geen index die is gekoppeld. Dit wordt vaak gebruikt als Azure Cosmos DB die wordt gebruikt als een sleutel / waarde-opslag en documenten zijn alleen toegankelijk met de ID-eigenschap. 

> [!NOTE]
> Configureren Hallo indexeren beleid met 'Geen' heeft hello neveneffect van het verwijderen van een bestaande index. Gebruik deze optie als de toegangspatronen zijn alleen nodig 'id' en/of 'Self link-element'.
> 
> 

Hallo volgen voorbeelden tonen hoe maken een Azure DB die Cosmos-verzameling Hallo .NET SDK met consistente automatisch indexeren op alle document invoegingen.

Hallo volgende tabel ziet u Hallo consistentie voor query's op basis van Hallo indexing-modus (consistente en Lazy) geconfigureerd voor Hallo verzameling en Hallo consistentieniveau opgegeven voor het Hallo-aanvraag. Dit geldt tooqueries gemaakt met behulp van een interface - REST-API SDK's of vanuit opgeslagen procedures en triggers. 

|Consistentie|Indexeren van modus: Consistent|Indexeren van modus: vertraagde|
|---|---|---|
|Sterk|Sterk|Mogelijk|
|Gebonden veroudering|Gebonden veroudering|Mogelijk|
|Sessie|Sessie|Mogelijk|
|Mogelijk|Mogelijk|Mogelijk|

Azure Cosmos DB foutmelding een voor query's die zijn aangebracht op verzamelingen geen modus te indexeren. Query's kunnen nog steeds worden uitgevoerd als scans via Hallo expliciete `x-ms-documentdb-enable-scan` header in Hallo REST-API of Hallo `EnableScanInQuery` aanvraag met behulp van optie Hallo .NET SDK. Sommige query-functies zoals ORDER BY worden niet ondersteund als scans met `EnableScanInQuery`.

Hallo volgende tabel ziet u Hallo consistentie voor query's op basis van Hallo indexering modus (consistente, Lazy en geen) als EnableScanInQuery is opgegeven.

|Consistentie|Indexeren van modus: Consistent|Indexeren van modus: vertraagde|Indexeren van modus: geen|
|---|---|---|---|
|Sterk|Sterk|Mogelijk|Sterk|
|Gebonden veroudering|Gebonden veroudering|Mogelijk|Gebonden veroudering|
|Sessie|Sessie|Mogelijk|Sessie|
|Mogelijk|Mogelijk|Mogelijk|Mogelijk|

Hallo volgen voorbeelden laten zien hoe maken een Azure DB die Cosmos-verzameling Hallo .NET SDK met consistente indexeren op alle document invoegingen.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>Index paden
Azure Cosmos-DB modellen JSON-documenten en Hallo index als structuren en kunt u tootune toopolicies voor paden binnen Hallo-structuur. Binnen documenten, kunt u kiezen welke paden moeten worden opgenomen of uitgesloten van het indexeren. Dit kunt verbeterde schrijfprestaties en lagere opslagkosten voor index voor scenario's bieden Hallo querypatronen vooraf bepaald.

Index paden beginnen met Hallo hoofdmap (/) en meestal eindigen op Hallo? jokertekens-operator, die aangeeft dat er meerdere mogelijke waarden voor Hallo voorvoegsel zijn. Bijvoorbeeld, selecteer tooserve * van Families F waar F.familyName = 'Andersen', moet u een pad van de index voor /familyName/ opnemen? in het beleid van de index van een verzameling Hallo.

Index paden kunt Hallo * jokerteken operator toospecify Hallo gedrag voor paden recursief onder Hallo voorvoegsel. Bijvoorbeeld: / nettolading / * kan worden gebruikt tooexclude alles onder Hallo nettolading eigenschap van het indexeren.

Hier volgen algemene patronen Hallo voor index paden opgeven:

| Pad                | Beschrijving/gebruiksvoorbeeld                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | Het standaardpad voor de verzameling. Recursieve en past de documentstructuur toowhole.                                                                                                                                                                                                                                   |
| / prop /?             | Index pad vereist tooserve query's de volgende hello (met hash- of -bereik van het type respectievelijk):<br><br>Selecteer uit verzameling c WHERE c.prop = '' waarde ''<br><br>Selecteer uit verzameling c WHERE c.prop > 5<br><br>Selecteer in de c verzameling ORDER BY c.prop                                                                       |
| / prop / *             | Pad van de index voor alle paden die onder het opgegeven label Hallo. Werkt met query's volgen Hallo<br><br>Selecteer uit verzameling c WHERE c.prop = '' waarde ''<br><br>Selecteer uit verzameling c WHERE c.prop.subprop > 5<br><br>Selecteer uit verzameling c WHERE c.prop.subprop.nextprop = '' waarde ''<br><br>Selecteer in de c verzameling ORDER BY c.prop         |
| Eigenschappen / [] /?         | Index pad vereist tooserve iteratie en JOIN-query's op matrices met scalaire waarden zoals ["a", "b", "c"]:<br><br>Selecteer label van de tag IN collection.props waar tag = '' waarde ''<br><br>Selecteer tag uit verzameling c JOIN-tag IN c.props waar tag > 5                                                                         |
| /props/ [] /subprop/? | Index pad vereist tooserve herhaling en JOIN-query's op matrices van objecten, zoals [{subprop: "a"}, {subprop: "b"}]:<br><br>Selecteer label van de tag IN collection.props waar tag.subprop '' waarde '' =<br><br>Selecteer labelen van verzameling c JOIN-tag IN c.props waar tag.subprop '' waarde '' =                                  |
| / prop/subprop /?     | Index pad vereist tooserve query's (met hash- of -bereik van het type respectievelijk):<br><br>Selecteer uit verzameling c WHERE c.prop.subprop = '' waarde ''<br><br>Selecteer uit verzameling c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> Tijdens het instellen van aangepaste index paden, bent u vereiste toospecify Hallo indexering standaardregel voor Hallo hele documentstructuur aangegeven met Hallo speciale pad ' / * '. 
> 
> 

Hallo volgende voorbeeld wordt een specifiek pad met bereik indexeren en de precisiewaarde van een aangepaste van 20 bytes:

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>Gegevenstypen van de index, typen en Precision-systemen
Nu dat we kijken hoe hebt genomen toospecify paden, bekijken we op Hallo-opties gebruiken we Hallo tooconfigure indexeringsbeleid voor een pad. U kunt een of meer indexering definities voor elke pad opgeven:

* Gegevenstype: **tekenreeks**, **getal**, **punt**, **veelhoek**, of **LineString** (kan slechts één vermelding per gegevenstype per pad bevatten)
* Indexeren van type: **Hash** (gelijkheid query's), **bereik** (gelijkheid, bereik of Order By-query's) of **Spatial** (ruimtelijke query's) 
* Precisie: Voor hash-index dit verschilt van 1 too8 voor zowel tekenreeksen en getallen met standaard als 3. Voor bereikindex deze waarde 1 (maximale precisie) en verschillen tussen de 1-100 (maximale precisie) voor de tekenreeks of numerieke waarden.

#### <a name="index-kind"></a>Index-type
Azure Cosmos DB ondersteunt Hash en bereik index soorten voor elk pad (die kunnen worden geconfigureerd voor tekenreeksen, cijfers of beide).

* **Hash** biedt ondersteuning voor efficiënte gelijkheid en JOIN-query's. Voor de meeste gevallen nodig hash-indexen niet een hogere precisie dan de standaardwaarde Hallo van 3 bytes. Gegevenstype is tekenreeks of het getal.
* **Bereik** ondersteunt gelijkheid efficiënt query's, bereik query's (met behulp van >, <>, =, < =,! =), en Order By-query's. Order By-query's standaard moeten echter ook maximumindex precision (-1). Gegevenstype is tekenreeks of het getal.

Azure Cosmos DB ondersteunt ook Hallo ruimtelijke index soort voor elk pad dat kan worden opgegeven voor Hallo punt, Polygon of LineString gegevenstypen. Hallo-waarde op Hallo opgegeven pad moet een geldige GeoJSON-fragment zoals `{"type": "Point", "coordinates": [0.0, 10.0]}`.

* **Ruimtelijke** ondersteunt efficiënt ruimtelijke (binnen en afstand) query's. Gegevenstype mag punt, Polygon of LineString.

> [!NOTE]
> Azure Cosmos DB biedt ondersteuning voor automatisch indexeren van punten, Multilinestring en multipoint.
> 
> 

Hier volgen Hallo ondersteund index soorten en voorbeelden van query's dat ze gebruikte tooserve kunnen worden:

| Index-type | Beschrijving/gebruiksvoorbeeld                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hash       | Hash-via/prop /? (of /) kan worden gebruikt tooserve Hallo de volgende query's efficiënt:<br><br>Selecteer uit verzameling c WHERE c.prop = '' waarde ''<br><br>Hash via Eigenschappen / [] /? (of / of eigenschappen /) kan worden gebruikt tooserve Hallo de volgende query's efficiënt:<br><br>Selecteer labelen van verzameling c JOIN-tag IN c.props waar tag = 5                                                                                                                       |
| bereik      | Bereik via/prop /? (of /) kan worden gebruikt tooserve Hallo de volgende query's efficiënt:<br><br>Selecteer uit verzameling c WHERE c.prop = '' waarde ''<br><br>Selecteer uit verzameling c WHERE c.prop > 5<br><br>Selecteer in de c verzameling ORDER BY c.prop                                                                                                                                                                                                              |
| Ruimtelijk     | Bereik via/prop /? (of /) kan worden gebruikt tooserve Hallo de volgende query's efficiënt:<br><br>Selecteer uit verzameling c<br><br>WAAR ST_DISTANCE (c.prop, {'type': 'Point', 'coördinaten': [0,0, 10.0]}) < 40<br><br>Selecteer uit verzameling c waar ST_WITHIN(c.prop, {"type": "Polygon",...})--met indexeren op punten ingeschakeld<br><br>Selecteer uit verzameling c waar ST_WITHIN({"type": "Point",...}, c.prop)--met indexeren op veelhoek ingeschakeld              |

Standaard wordt een fout geretourneerd voor query's met bereik operators zoals > = als er geen bereikindex (van eventuele precisie is) in de volgorde toosignal een scan mogelijk nodig tooserve Hallo query. Bereik query's kunnen worden uitgevoerd zonder een bereikindex met behulp van Hallo x-ms-documentdb-enable-scan koptekst in Hallo REST-API of Hallo EnableScanInQuery aanvraagoptie Hallo .NET SDK gebruiken. Als er geen andere filters in Hallo-query's met Azure Cosmos DB Hallo index toofilter tegen kunt gebruiken, wordt er geen fout worden geretourneerd.

Hallo dezelfde regels voor ruimtelijke query's gelden. Standaard wordt een fout geretourneerd voor ruimtelijke query's als er geen ruimtelijke index is en er zijn geen filters die worden aangeboden via Hallo index. Ze kunnen worden uitgevoerd als een scan met behulp van de x-ms-documentdb-enable-scan/EnableScanInQuery.

#### <a name="index-precision"></a>Index precisie
Index precisie kunt u een afweging tussen index opslagoverhead en prestaties van query's. Voor getallen, wordt u aangeraden Hallo standaardconfiguratie precisie van-1 ('maximum'). Aangezien getallen 8 bytes in JSON, wordt dit is de configuratie van de equivalente tooa van 8 bytes. Verzamelen van een lagere waarde voor de precisie, zoals 1-7, index betekent dat de waarden binnen enkele kaart bereiken toohello dezelfde vermelding. U wordt daarom verlaagd index opslagruimte, maar queryuitvoering zou kunnen hebben tooprocess meer documenten en als gevolg daarvan dat wil zeggen, verbruikt meer doorvoer aanvraageenheden.

Index precisie configuratie heeft praktischer toepassing met de tekenreeks bereiken. Omdat tekenreeksen kunnen elke willekeurige lengte, kan Hallo keuze van Hallo index precisie invloed hebben op prestaties Hallo van tekenreeks bereik query's en gevolgen Hallo hoeveelheid index opslagruimte vereist. Tekenreeks bereik indexen kunnen worden geconfigureerd met 1-100 of -1 ('maximum'). Als u tooperform Order By-query's op basis van eigenschappen van een verbindingsreeks dat wilt, moet u een precisie van -1 voor de bijbehorende paden Hallo opgeven.

Ruimtelijke indexen worden altijd Hallo standaard index precisie te gebruiken voor alle typen (punten multipoint en Veelhoek) en kunnen niet worden overschreven. 

Hallo volgende voorbeeld ziet u hoe tooincrease Hallo precisie voor bereik worden geïndexeerd in een verzameling met Hallo .NET SDK. 

**Een verzameling met een aangepaste index precisie maken**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Azure Cosmos DB, wordt er een fout geretourneerd als een query maakt gebruik van Order By, maar geen een bereikindex tegen Hallo opgevraagde pad met Hallo maximumprecisie heeft. 
> 
> 

Paden kunnen op dezelfde manier volledig uitgesloten van het indexeren. Hallo volgende voorbeeld ziet u hoe tooexclude een hele sectie Hallo documenten (ook een substructuur) niet kan indexeren met behulp van Hallo ' * ' jokerteken.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>Inschrijving en buiten het indexeren uitschakelen
U kunt kiezen of u wilt dat de verzamelingsindex tooautomatically Hallo alle documenten. Standaard worden alle documenten automatisch geïndexeerd, maar u kunt tooturn uit. Wanneer het indexeren is uitgeschakeld, documenten toegankelijk zijn alleen via hun Self link-elementen of door query's met-id.

Met automatische indexeren uitgeschakeld, kunt u alleen bepaalde documenten toohello index nog steeds selectief toevoegen. Als u daarentegen, kunt u automatische indexering op laat en selectief alleen bepaalde documenten kiezen tooexclude. Indexeren aan/uit-configuraties zijn nuttig wanneer u slechts een subset van documenten die toobe opgevraagd nodig hebt.

Bijvoorbeeld: sample Hallo volgende toont hoe tooinclude een document met expliciet Hallo [DocumentDB API .NET SDK](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) en Hallo [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) eigenschap.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>Hallo indexeringsbeleid van een verzameling wijzigen
Azure Cosmos DB, kunt u toomake wijzigingen toohello indexeringsbeleid van een verzameling op Hallo snel. Een wijziging in het beleid op een verzameling Azure Cosmos DB indexeren kan tooa wijziging in de vorm Hallo van Hallo index inclusief Hallo paden kunnen worden geïndexeerd, de precisie, evenals Hallo consistent model van Hallo index zelf leiden. Effectief vereist een wijziging in indexeringsbeleid, dus een transformatie van Hallo oude index in een nieuwe. 

**Online-Index transformaties**

![Hoe indexeren werkt – Azure Cosmos DB online index transformaties](./media/indexing-policies/index-transformations.png)

Index transformaties online, wat betekent dat Hallo documenten geïndexeerd per Hallo oude beleid efficiënt worden getransformeerd per Hallo nieuw beleid zijn aangebracht **zonder Hallo schrijven beschikbaarheid of ingerichte doorvoer Hallo** van Hallo-verzameling. consistentie van lezen Hallo en schrijfbewerkingen die zijn gemaakt met behulp van Hallo REST-API SDK's of uit binnen de opgeslagen procedures en triggers wordt niet negatief beïnvloed tijdens index transformatie. Dit betekent dat er geen verslechtering of uitvaltijd tooyour apps wanneer u een indexeringsbeleid wijzigen.

Tijdens het Hallo-tijd die index transformatie uitgevoerd is, zijn query's echter uiteindelijk consistent ongeacht Hallo indexeren modus configuratie (consistente of Lazy). Dit ook van toepassing is tooqueries van alle interfaces – REST-API SDK's, en vanuit opgeslagen procedures en triggers. Net als met Lazy indexeren, is index-transformatie uitgevoerd asynchroon op Hallo achtergrond op Hallo replica's met Hallo spare bronnen beschikbaar voor een bepaalde replica. 

Index transformaties worden ook gemaakt **in situ** (in plaats), dat wil zeggen Azure Cosmos DB bewaart geen twee exemplaren van het Hallo-index en wisselen Hallo oude index uit Hello nieuwe. Dit betekent dat er geen extra schijfruimte vereist of in uw verzamelingen gebruikt tijdens het uitvoeren van de index transformaties.

Wanneer u indexeringsbeleid wijzigt, hoe Hallo wijzigingen zijn toegepast toomove van Hallo oude index toohello nieuwe een zijn hoofdzakelijk afhankelijk van Hallo configuraties meer indexeren zodat dan Hallo andere waarden, zoals paden opgenomen/uitgesloten, index-typen en Precision-systemen. Als uw oude en nieuwe beleidsregels consistent indexeren, voert Azure Cosmos DB een transformatie online-index. U kunt een andere indexering beleidswijziging met consistente indexing-modus niet toepassen terwijl Hallo transformatie uitgevoerd wordt.

U kunt echter verplaatsen tooLazy of None indexering modus tijdens een transformatie uitgevoerd wordt. 

* Wanneer u tooLazy verplaatst, Hallo index beleid wordt gewijzigd effectieve onmiddellijk en Azure Cosmos DB begint asynchroon Hallo index opnieuw te maken. 
* Wanneer u tooNone verplaatst, wordt Hallo index weggehaald effectieve onmiddellijk. Het verplaatsen van tooNone is handig als u een onderhanden toocancel wilt transformatie en begin met een ander beleid voor indexering. 

Als u Hallo .NET SDK, kunt u ere van een indexering beleidswijziging met Hallo nieuwe **ReplaceDocumentCollectionAsync** methode en bijhouden Hallo percentage voortgang van Hallo index transformatie Hallo met  **IndexTransformationProgress** antwoord-eigenschap van een **ReadDocumentCollectionAsync** aanroepen. Andere SDK's en de REST-API Hallo ondersteuning voor equivalente eigenschappen en methoden voor het maken van wijzigingen in het indexeren.

Hier volgt een codefragment die laat zien hoe een verzameling toomodify beleid van consistente indexering modus tooLazy het indexeren.

**Beleid indexeren van consistente tooLazy wijzigen**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


U kunt Hallo voortgang van een index transformatie door aanroepen ReadDocumentCollectionAsync, bijvoorbeeld kunt controleren, zoals hieronder wordt weergegeven.

**Voortgang van de Index transformatie volgen**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

U kunt Hallo index voor een verzameling verwijderen door verplaatsen toohello geen modus te indexeren. Dit wordt mogelijk een handig hulpmiddel operationele als u toocancel een transformatie wordt uitgevoerd wilt en een nieuwe onmiddellijk starten.

**Verwijderen van de index Hallo voor een verzameling**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

Wanneer maakt u indexering beleidswijzigingen tooyour Azure Cosmos DB verzamelingen? Hallo hieronder vindt u de meest voorkomende gebruiksvoorbeelden Hallo:

* Consistente resultaten dienen tijdens normale werking, maar terugvallen toolazy tijdens bulkimport gegevens te indexeren
* Start met het gebruik van nieuwe indexering functies op uw huidige Azure Cosmos DB verzamelingen, bijvoorbeeld zoals georuimtelijke uitvoeren van query's die nodig Hallo ruimtelijke index soort of Order By / bereik-query's waarvoor Hallo tekenreeks bereik index type string
* Selecteer Hallo eigenschappen toobe geïndexeerd hand en wijzig ze na verloop van tijd
* Indexering precisie tooimprove query-prestaties afstemmen of opslagruimte is verbruikt verminderen

> [!NOTE]
> toomodify indexeren beleid via ReplaceDocumentCollectionAsync, moet u versie > = 1.3.0 Hallo .NET SDK
> 
> Index transformatie toocomplete is, moet u ervoor zorgen dat er voldoende vrije ruimte beschikbaar op Hallo-verzameling is. Als Hallo verzameling de opslaglimiet bereikt, wordt Hallo index transformatie worden onderbroken. Transformatie van de index wordt automatisch voortgezet zodra opslagruimte beschikbaar is, bijvoorbeeld als u bepaalde documenten verwijdert.
> 
> 

## <a name="performance-tuning"></a>Prestaties afstemmen
Hallo DocumentDB APIs bevatten informatie over de maatstaven voor prestaties, zoals Hallo index opslag gebruikt en Hallo doorvoer (aanvraageenheden) kosten voor elke bewerking. Deze informatie mag gebruikte toocompare verschillende beleidsregels voor indexering en voor prestaties afstemmen.

toocheck hello opslaglimiet en het gebruik van een verzameling, uitvoeren van een HEAD- of GET-aanvraag op Hallo verzamelingsbron en inspecteren Hallo x-ms-aanvraag-quota en Hallo x-ms-aanvraag-gebruik headers. Hallo in Hallo .NET SDK, [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) en [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) eigenschappen in [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) deze bijbehorende waarden bevatten .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


toomeasure hello overhead van het indexeren op elke schrijfbewerking (maken, bijwerken of verwijderen) inspecteren Hallo x-ms-aanvraag-kosten header (of gelijkwaardige Hallo [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) eigenschap in [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) in .NET SDK Hallo) toomeasure Hallo aantal aanvraageenheden verbruikt door deze bewerkingen.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>Wijzigingen toohello indexeren beleidsspecificatie van het
Een wijziging in het schema voor het indexeringsbeleid Hallo is op 7 juli 2015 met de REST API-versie 2015-06-03 geïntroduceerd. Hallo bijbehorende klassen in de SDK-versies Hallo nieuwe implementaties toomatch Hallo schema's zijn. 

Hallo volgende wijzigingen zijn geïmplementeerd in Hallo JSON-specificatie:

* Indexeren van beleid ondersteunt bereik indexen voor tekenreeksen
* Elk pad kan meerdere definities voor index, één voor elk gegevenstype hebben
* Indexeren van precisie ondersteunt 1-8 voor cijfers, 1-100 naar tekenreeksen en -1 (maximumprecisie)
* Paden segmenten vereisen een dubbele aanhalingstekens tooescape niet elk pad. U kunt bijvoorbeeld een pad voor de titel/toevoegen? in plaats van / 'title' /?
* hoofdpad Hallo 'alle paden' die kan worden weergegeven als / * (bovendien te /)

Als u de code die voorziet in verzamelingen met een aangepast indexeringsbeleid geschreven met versie 1.1.0 van hebt Hallo .NET SDK of ouder, moet u toochange uw toepassing code toohandle deze wijzigingen in de volgorde toomove tooSDK versie 1.2.0. Als u geen code die u indexeringsbeleid configureert of toocontinue met behulp van een oudere versie van de SDK van plan bent, zijn geen wijzigingen vereist.

Voor een praktische vergelijking is hier een voorbeeld aangepast indexeringsbeleid geschreven met behulp van Hallo REST API-versie 2015-06-03, evenals Hallo vorige versie 2015-04-08.

**Vorige Indexeringsbeleid JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**Huidige Indexeringsbeleid JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>Volgende stappen
Volg onderstaande Hallo koppelingen voor meer informatie over Azure Cosmos DB querytaal index beleid management voorbeelden en toolearn.

1. [DocumentDB-API .NET indexbeheer-codevoorbeelden](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [DocumentDB API REST-verzameling bewerkingen](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [De query met behulp van SQL](documentdb-sql-query.md)

