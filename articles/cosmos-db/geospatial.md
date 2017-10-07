---
title: aaaWorking met georuimtelijke gegevens in Azure Cosmos DB | Microsoft Docs
description: Begrijpt hoe toocreate, index en query ruimtelijke-objecten met Azure Cosmos DB en Hallo DocumentDB-API.
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Werken met georuimtelijke en GeoJSON locatiegegevens in Azure Cosmos-DB
Dit artikel bevat een inleiding toohello georuimtelijke functionaliteit in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). Na het lezen van dit, kunt u zich kunt tooanswer Hallo vragen te volgen:

* Hoe kan ik ruimtelijke gegevens opslaan in Azure Cosmos DB?
* Hoe kan ik een query over gegevens in Azure Cosmos-database in SQL- en LINQ georuimtelijke?
* Hoe ik in- of uitschakelen ruimtelijke indexeren in Azure Cosmos DB?

Dit artikel laat zien hoe toowork met ruimtelijke gegevens met DocumentDB API Hallo. Raadpleeg dit [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) voor codevoorbeelden.

## <a name="introduction-toospatial-data"></a>Inleiding toospatial gegevens
Ruimtelijke gegevens beschrijft Hallo positie en vorm van objecten in de ruimte. In de meeste toepassingen deze komen overeen met tooobjects op Hallo aarde, dat wil zeggen georuimtelijke gegevens. Ruimtelijke gegevens kunnen worden gebruikt toorepresent Hallo locatie van een persoon, een plaats van belang of Hallo grens van een stad of een meer. Algemene gebruiksvoorbeelden inhouden vaak nabijheid query's voor bijvoorbeeld 'vinden alle in internetcafés in de buurt van mijn huidige locatie'. 

### <a name="geojson"></a>GeoJSON
Azure Cosmos-DB biedt ondersteuning voor indexering en query's naar georuimtelijke punt gegevens die worden weergegeven met behulp van Hallo [GeoJSON-specificatie](https://tools.ietf.org/html/rfc7946). GeoJSON gegevensstructuren zijn altijd geldig JSON-objecten, zodat ze kunnen worden opgeslagen en opgevraagd met Azure Cosmos DB zonder speciale hulpprogramma's of bibliotheken. Hello Azure Cosmos DB SDK's bieden helperklassen en methoden waarmee u eenvoudig toowork met ruimtelijke gegevens. 

### <a name="points-linestrings-and-polygons"></a>Punten, multipoint en Veelhoek
Een **punt** wordt bepaald door een enkele positie in de ruimte. Een punt vertegenwoordigt georuimtelijke gegevens, de exacte locatie hello, wat erop kan een adres van een winkelketen, een kiosk, een auto of een plaats.  GeoJSON (en Azure Cosmos DB) met behulp van de coördinaat paar of de lengte en de breedte van een punt wordt weergegeven. Hier volgt een voorbeeld van JSON voor een punt.

**Punten in Azure Cosmos DB**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Hallo GeoJSON-specificatie bevat lengtegraad eerste en breedtegraad tweede. Net als in andere toepassingen toewijzing breedtegraad worden hoeken en vertegenwoordigd in termen van graden. Lengtegraadwaarden worden gemeten vanaf Hallo nulmeridiaan en zijn tussen-180 en 180.0 graden en breedtegraad waarden worden gemeten vanaf Hallo evenaar en zijn tussen-90.0 en 90.0 graden. 
> 
> Azure Cosmos DB interpreteert coördinaten, zoals wordt weergegeven per Hallo WGS 84 referentiesysteem. Zie hieronder voor meer informatie over coördinaat referentiesystemen.
> 
> 

Dit kan worden ingesloten in een document Azure Cosmos DB zoals in dit voorbeeld van een gebruikersprofiel met locatiegegevens:

**Gebruik het profiel met locatie opgeslagen in Azure Cosmos-DB**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

Daarnaast ondersteunt toopoints, GeoJSON ook multipoint en veelhoek. **Multipoint** Hallo lijnsegmenten waarmee ze verbinding maken en een reeks van twee of meer punten in de ruimte vertegenwoordigen. In georuimtelijke gegevens zijn multipoint veelgebruikte toorepresent wegen of rivieren. Een **veelhoek** is een grens verbonden punten die een gesloten LineString vormt. Veelhoek zijn vaak gebruikte toorepresent natuurlijke formaties zoals meren of politieke rechtsgebieden zoals steden en statussen. Hier volgt een voorbeeld van een Polygoon in Azure Cosmos DB. 

**Veelhoek in GeoJSON**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> Hallo GeoJSON specificatie moet voor geldige veelhoek hello laatste coördinaat paar opgegeven Hallo dezelfde als Hallo eerst toocreate een gesloten vorm.
> 
> Punten in een Polygoon moeten worden opgegeven in rechtsom volgorde. Een veelhoek in rechtsom order opgegeven vertegenwoordigt Hallo inverse van Hallo regio erin.
> 
> 

In aanvulling tooPoint, LineString en Veelhoek, GeoJSON ook Hiermee geeft u Hallo weergave voor het toogroup meerdere georuimtelijke locaties, en hoe tooassociate willekeurige eigenschappen met geolocatie als een **functie**. Aangezien deze objecten geldige JSON zijn, kunnen ze alle worden opgeslagen en verwerkt in Azure Cosmos DB. Maar Azure Cosmos DB biedt alleen ondersteuning voor automatisch indexeren van punten.

### <a name="coordinate-reference-systems"></a>Coördinaat referentiesystemen
Omdat Hallo vorm van Hallo earth onregelmatige is, wordt veel coördinaat referentiesystemen (CRS), elk met hun eigen frames van verwijzing en maateenheden coördinaten van georuimtelijke gegevens weergegeven. Hallo 'National raster van-Brittannië' is bijvoorbeeld een referentiesysteem is zeer nauwkeurig voor Hallo Verenigd Koninkrijk, maar niet buiten. 

Hallo populairste CRS in gebruik is vandaag de dag Hallo wereld geodetisch systeem [WGS 84](http://earth-info.nga.mil/GandG/wgs84/). Gebruik WGS 84 GPS-apparaten en veel toewijzing services, met inbegrip van Google-kaarten en Bing kaarten-API's. Azure Cosmos DB ondersteunt indexeren en query's naar georuimtelijke gegevens met behulp van Hallo WGS 84 CRS alleen. 

## <a name="creating-documents-with-spatial-data"></a>Maken van documenten met ruimtelijke gegevens
Bij het maken van documenten die GeoJSON-waarden bevatten, worden ze automatisch geïndexeerd met een ruimtelijke index in overeenstemming toohello indexeringsbeleid van Hallo-verzameling. Als u met een Azure-SDK Cosmos-database in een dynamisch getypeerde taal zoals Python of Node.js werkt, moet u geldige GeoJSON maken.

**Document maken met georuimtelijke gegevens in Node.js**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

Als u met DocumentDB APIs hello werkt, kunt u Hallo `Point` en `Polygon` klassen in Hallo `Microsoft.Azure.Documents.Spatial` naamruimte tooembed locatiegegevens binnen uw toepassingsobjecten. Deze klassen vereenvoudigen Hallo serialisatie en deserialisatie van ruimtelijke gegevens in GeoJSON.

**Document met georuimtelijke gegevens in .NET maken**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

Als u niet beschikt over de breedtegraad en lengtegraad informatie Hallo maar Hallo fysieke adressen of de naam van de locatie zoals plaats of land hebt, kunt u de werkelijke coördinaten Hallo opzoeken met behulp van een geocodering service, zoals Bing Maps REST-Services. Meer informatie over geocodering van Bing Maps [hier](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Spatiale typen opvragen
Nu dat we kijken hoe hebt genomen tooinsert georuimtelijke gegevens, eens kijken hoe tooquery deze gegevens met behulp van Azure Cosmos DB met SQL en LINQ.

### <a name="spatial-sql-built-in-functions"></a>Ruimtelijke ingebouwde SQL-functies
Azure Cosmos DB ondersteunt Hallo Open georuimtelijke Consortium (OGC) ingebouwde functies voor georuimtelijke query's te volgen. Voor meer informatie over de volledige reeks ingebouwde functies in SQL-taal Hallo Hallo Raadpleeg te[Query Azure Cosmos DB](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Gebruik</strong></td>
  <td><strong>Beschrijving</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>Retourneert Hallo afstand tussen twee Hallo GeoJSON punt, Polygon of LineString expressies.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Retourneert een Booleaanse expressie die aangeeft of Hallo eerste GeoJSON-object (punt, Polygon of LineString) binnen Hallo tweede GeoJSON-object (punt, Polygon of LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Retourneert een Booleaanse expressie die aangeeft of Hallo twee opgegeven GeoJSON-objecten (punt, Polygon of LineString) intersect.</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Retourneert een Booleaanse waarde die aangeeft of Hallo opgegeven GeoJSON punt, Polygon of LineString expressie is ongeldig.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Retourneert een JSON-waarde met een Boolean-waarde als Hallo GeoJSON punt, Polygon of LineString expressie opgegeven geldig is en als ongeldig, bovendien Hallo reden als een string-waarde.</td>
</tr>
</table>

Ruimtelijke functies kunnen worden gebruikt tooperform nabijheid query's op ruimtelijke gegevens. Hier is bijvoorbeeld een query waarmee alle familie documenten dat binnen 30 km Hallo opgegeven locatie Hallo ST_DISTANCE ingebouwde functie gebruikt geretourneerd. 

**Query**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Resultaten**

    [{
      "id": "WakefieldFamily"
    }]

Als u ruimtelijke indexeren in uw indexeringsbeleid opneemt, kunnen klikt u vervolgens 'afstand query's ' worden geleverd efficiënt via Hallo index. Zie voor meer informatie over het ruimtelijke indexeren Hallo hieronder. Als u een ruimtelijke hebt index voor Hallo paden die is opgegeven, kunt u nog steeds ruimtelijke query's uitvoeren door te geven `x-ms-documentdb-query-enable-scan` aanvraag-header met waarde hello te 'true' ingesteld. In .NET, kunt dit doen door de optionele Hallo doorgeven **FeedOptions** argument tooqueries met [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) tootrue ingesteld. 

ST_WITHIN zijn gebruikte toocheck als een punt binnen een Polygoon ligt. Veelhoek zijn vaak gebruikte toorepresent grenzen zoals zip-codes, status grenzen of natuurlijke formaties. Opnieuw als u ruimtelijke indexeren in uw indexeringsbeleid opneemt, klikt u vervolgens 'in' query's kunnen worden geleverd efficiënt via Hallo index. 

Argumenten van de veelhoek in ST_WITHIN mag slechts één keer, dat wil zeggen Hallo veelhoek mag geen gaten in deze. 

**Query**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Resultaten**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Soortgelijke toohow verkeerde werkt in Azure Cosmos DB-query als Hallo locatiewaarde opgegeven een argument is onjuist gevormd of ongeldig, deze te evalueren**niet-gedefinieerde** en Hallo geëvalueerd document toobe van Hallo overgeslagen de resultaten van de query. Als de query geen resultaten oplevert, voert u ST_ISVALIDDETAILED toodebug waarom Hallo spatail type ongeldig is.     
> 
> 

Azure Cosmos DB biedt ook ondersteuning voor inverse query's uitvoeren, dat wil zeggen u kunt indexeren Multilinestring of regels in een Azure Cosmos DB en vervolgens zoeken naar Hallo gebieden die een opgegeven punt bevatten. Dit patroon wordt vaak gebruikt in logistiek tooidentify bijvoorbeeld wanneer een vrachtwagen binnengaat of verlaat een aangewezen gebied. 

**Query**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Resultaten**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID en ST_ISVALIDDETAILED kunnen gebruikte toocheck zich als een ruimtelijke object geldig is. Hallo na query controleert bijvoorbeeld Hallo geldigheid van een punt met een out-of breedtegraad bereikwaarde (-132.8). ST_ISVALID alleen een Booleaanse waarde retourneert en ST_ISVALIDDETAILED retourneert Hallo Booleaanse waarde en een tekenreeks met Hallo reden waarom het wordt als ongeldig beschouwd.

** Query **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Resultaten**

    [{
      "$1": false
    }]

Deze functies kunnen ook worden gebruikt toovalidate veelhoek. Bijvoorbeeld, hier gebruiken we ST_ISVALIDDETAILED toovalidate een Polygoon die niet wordt afgesloten. 

**Query**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Resultaten**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>LINQ een query uitvoert op Hallo .NET SDK
Hallo DocumentDB .NET SDK ook providers stub-methoden `Distance()` en `Within()` voor gebruik in een LINQ-expressies. Hallo DocumentDB LINQ-provider vertaalt deze methode aanroepen toohello gelijkwaardige SQL ingebouwde functieaanroepen (ST_DISTANCE en ST_WITHIN respectievelijk). 

Hier volgt een voorbeeld van een LINQ-query waarmee wordt gezocht naar alle documenten in hello Azure Cosmos DB verzameling waarvan de waarde 'locatie' wordt binnen een straal van 30km Hallo opgegeven verwijzen met behulp van LINQ.

**LINQ-query voor afstand**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

Hier is ook een query voor het zoeken naar alle Hallo documenten waarvan 'locatie' binnen Hallo valt vak/veelhoek opgegeven. 

**LINQ-query voor binnen**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


Nu dat we kijken hoe hebt genomen tooquery documenten met behulp van LINQ en SQL, eens kijken hoe tooconfigure Azure Cosmos DB voor ruimtelijke indexeren.

## <a name="indexing"></a>Indexeren
Zoals wordt beschreven in Hallo [Schema Networkdirect indexering met Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papier we Azure Cosmos DB database-engine toobe ontworpen echt schema networkdirect en eerste-klas ondersteuning bieden voor JSON. Hallo schrijven die zijn geoptimaliseerd voor database-engine van Azure DB die Cosmos begrijpt systeemeigen ruimtelijke gegevens (points, Multilinestring en regels) in Hallo GeoJSON standaard weergegeven.

Kortom, Hallo geometrie wordt geprojecteerd van geodetisch coördinaten op een 2D vlak vervolgens geleidelijk onderverdeeld in de cellen met behulp van een **quadtree**. Deze cellen zijn toegewezen too1D op basis van locatie Hallo van Hallo cel binnen een **Hilbert ruimte vullen curve**, die de plaats van punten behouden blijft. Bovendien wanneer locatiegegevens wordt geïndexeerd, wordt er een proces genaamd **mozaïekpatroon**, dat wil zeggen alle Hallo cellen die een locatie intersect worden geïdentificeerd en opgeslagen als sleutels in hello Azure Cosmos DB index. Op het moment dat de query, argumenten zoals punten en Veelhoek ook representatie mozaïekpatroon tooextract zijn Hallo relevante cel ID bereiken en vervolgens tooretrieve gegevens van de index Hallo gebruikt.

Als u een indexeringsbeleid met ruimtelijke index voor / * (alle paden) en vervolgens alle punten gevonden binnen de verzameling Hallo worden geïndexeerd voor efficiënte ruimtelijke query's (ST_WITHIN en ST_DISTANCE). Ruimtelijke indexen niet hebben een precisiewaarde, en gebruik altijd een standaardwaarde precisie.

> [!NOTE]
> Azure Cosmos DB biedt ondersteuning voor automatisch indexeren van punten, Multilinestring en multipoint
> 
> 

Hallo volgende JSON-fragment toont een indexeringsbeleid met ruimtelijke indexeren is ingeschakeld, dat wil zeggen indexnummer nergens GeoJSON gevonden binnen documenten ruimtelijke query's. Als u indexeren met behulp van Azure Portal Hallo Hallo wijzigt, kunt u Hallo JSON volgen voor indexeren beleid tooenable ruimtelijke indexeren op uw verzameling opgeven.

**Verzameling indexeren JSON met Spatial ingeschakeld voor punten en Veelhoek beleid**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

Hier volgt een codefragment in .NET die laat hoe een verzameling zien met ruimtelijke indexeren toocreate ingeschakeld voor alle paden die punten bevat. 

**Maak een verzameling met ruimtelijke indexeren**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

En hier ziet u hoe u een bestaande verzameling tootake voordeel van het ruimtelijke indexeren via alle punten die zijn opgeslagen in de documenten kunt wijzigen.

**Een bestaande verzameling met ruimtelijke indexeren wijzigen**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> Als Hallo locatie GeoJSON-waarde in het document Hallo onjuist gevormd of ongeldig is, wordt klikt u vervolgens het niet geïndexeerd ruimtelijke query's. U kunt de locatie van waarden met ST_ISVALID en ST_ISVALIDDETAILED valideren.
> 
> Als de definitie van de verzameling een partitiesleutel bevat, is indexeren voortgang van de transformatie niet gerapporteerd. 
> 
> 

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt vernomen over hoe tooget met ondersteuning voor georuimtelijke in Azure Cosmos DB gestart, kunt u:

* Gaan coderen Hello [georuimtelijke .NET-codevoorbeelden op GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* U handen op waarop het georuimtelijke opvragen op Hallo [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)
* Meer informatie over [Azure Cosmos DB-Query](documentdb-sql-query.md)
* Meer informatie over [Azure Cosmos DB indexeren beleid](indexing-policies.md)

