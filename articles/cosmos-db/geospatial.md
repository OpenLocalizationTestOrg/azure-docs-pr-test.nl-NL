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
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="30007-103">Werken met georuimtelijke en GeoJSON locatiegegevens in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="30007-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="30007-104">Dit artikel bevat een inleiding toohello georuimtelijke functionaliteit in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="30007-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="30007-105">Na het lezen van dit, kunt u zich kunt tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="30007-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="30007-106">Hoe kan ik ruimtelijke gegevens opslaan in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="30007-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="30007-107">Hoe kan ik een query over gegevens in Azure Cosmos-database in SQL- en LINQ georuimtelijke?</span><span class="sxs-lookup"><span data-stu-id="30007-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="30007-108">Hoe ik in- of uitschakelen ruimtelijke indexeren in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="30007-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="30007-109">Dit artikel laat zien hoe toowork met ruimtelijke gegevens met DocumentDB API Hallo.</span><span class="sxs-lookup"><span data-stu-id="30007-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="30007-110">Raadpleeg dit [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) voor codevoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="30007-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="30007-111">Inleiding toospatial gegevens</span><span class="sxs-lookup"><span data-stu-id="30007-111">Introduction toospatial data</span></span>
<span data-ttu-id="30007-112">Ruimtelijke gegevens beschrijft Hallo positie en vorm van objecten in de ruimte.</span><span class="sxs-lookup"><span data-stu-id="30007-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="30007-113">In de meeste toepassingen deze komen overeen met tooobjects op Hallo aarde, dat wil zeggen georuimtelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="30007-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="30007-114">Ruimtelijke gegevens kunnen worden gebruikt toorepresent Hallo locatie van een persoon, een plaats van belang of Hallo grens van een stad of een meer.</span><span class="sxs-lookup"><span data-stu-id="30007-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="30007-115">Algemene gebruiksvoorbeelden inhouden vaak nabijheid query's voor bijvoorbeeld 'vinden alle in internetcafés in de buurt van mijn huidige locatie'.</span><span class="sxs-lookup"><span data-stu-id="30007-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="30007-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="30007-116">GeoJSON</span></span>
<span data-ttu-id="30007-117">Azure Cosmos-DB biedt ondersteuning voor indexering en query's naar georuimtelijke punt gegevens die worden weergegeven met behulp van Hallo [GeoJSON-specificatie](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="30007-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="30007-118">GeoJSON gegevensstructuren zijn altijd geldig JSON-objecten, zodat ze kunnen worden opgeslagen en opgevraagd met Azure Cosmos DB zonder speciale hulpprogramma's of bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="30007-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="30007-119">Hello Azure Cosmos DB SDK's bieden helperklassen en methoden waarmee u eenvoudig toowork met ruimtelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="30007-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="30007-120">Punten, multipoint en Veelhoek</span><span class="sxs-lookup"><span data-stu-id="30007-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="30007-121">Een **punt** wordt bepaald door een enkele positie in de ruimte.</span><span class="sxs-lookup"><span data-stu-id="30007-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="30007-122">Een punt vertegenwoordigt georuimtelijke gegevens, de exacte locatie hello, wat erop kan een adres van een winkelketen, een kiosk, een auto of een plaats.</span><span class="sxs-lookup"><span data-stu-id="30007-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="30007-123">GeoJSON (en Azure Cosmos DB) met behulp van de coördinaat paar of de lengte en de breedte van een punt wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="30007-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="30007-124">Hier volgt een voorbeeld van JSON voor een punt.</span><span class="sxs-lookup"><span data-stu-id="30007-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="30007-125">**Punten in Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="30007-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="30007-126">Hallo GeoJSON-specificatie bevat lengtegraad eerste en breedtegraad tweede.</span><span class="sxs-lookup"><span data-stu-id="30007-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="30007-127">Net als in andere toepassingen toewijzing breedtegraad worden hoeken en vertegenwoordigd in termen van graden.</span><span class="sxs-lookup"><span data-stu-id="30007-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="30007-128">Lengtegraadwaarden worden gemeten vanaf Hallo nulmeridiaan en zijn tussen-180 en 180.0 graden en breedtegraad waarden worden gemeten vanaf Hallo evenaar en zijn tussen-90.0 en 90.0 graden.</span><span class="sxs-lookup"><span data-stu-id="30007-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="30007-129">Azure Cosmos DB interpreteert coördinaten, zoals wordt weergegeven per Hallo WGS 84 referentiesysteem.</span><span class="sxs-lookup"><span data-stu-id="30007-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="30007-130">Zie hieronder voor meer informatie over coördinaat referentiesystemen.</span><span class="sxs-lookup"><span data-stu-id="30007-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="30007-131">Dit kan worden ingesloten in een document Azure Cosmos DB zoals in dit voorbeeld van een gebruikersprofiel met locatiegegevens:</span><span class="sxs-lookup"><span data-stu-id="30007-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="30007-132">**Gebruik het profiel met locatie opgeslagen in Azure Cosmos-DB**</span><span class="sxs-lookup"><span data-stu-id="30007-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="30007-133">Daarnaast ondersteunt toopoints, GeoJSON ook multipoint en veelhoek.</span><span class="sxs-lookup"><span data-stu-id="30007-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="30007-134">**Multipoint** Hallo lijnsegmenten waarmee ze verbinding maken en een reeks van twee of meer punten in de ruimte vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="30007-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="30007-135">In georuimtelijke gegevens zijn multipoint veelgebruikte toorepresent wegen of rivieren.</span><span class="sxs-lookup"><span data-stu-id="30007-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="30007-136">Een **veelhoek** is een grens verbonden punten die een gesloten LineString vormt.</span><span class="sxs-lookup"><span data-stu-id="30007-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="30007-137">Veelhoek zijn vaak gebruikte toorepresent natuurlijke formaties zoals meren of politieke rechtsgebieden zoals steden en statussen.</span><span class="sxs-lookup"><span data-stu-id="30007-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="30007-138">Hier volgt een voorbeeld van een Polygoon in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="30007-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="30007-139">**Veelhoek in GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="30007-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="30007-140">Hallo GeoJSON specificatie moet voor geldige veelhoek hello laatste coördinaat paar opgegeven Hallo dezelfde als Hallo eerst toocreate een gesloten vorm.</span><span class="sxs-lookup"><span data-stu-id="30007-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="30007-141">Punten in een Polygoon moeten worden opgegeven in rechtsom volgorde.</span><span class="sxs-lookup"><span data-stu-id="30007-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="30007-142">Een veelhoek in rechtsom order opgegeven vertegenwoordigt Hallo inverse van Hallo regio erin.</span><span class="sxs-lookup"><span data-stu-id="30007-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="30007-143">In aanvulling tooPoint, LineString en Veelhoek, GeoJSON ook Hiermee geeft u Hallo weergave voor het toogroup meerdere georuimtelijke locaties, en hoe tooassociate willekeurige eigenschappen met geolocatie als een **functie**.</span><span class="sxs-lookup"><span data-stu-id="30007-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="30007-144">Aangezien deze objecten geldige JSON zijn, kunnen ze alle worden opgeslagen en verwerkt in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="30007-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="30007-145">Maar Azure Cosmos DB biedt alleen ondersteuning voor automatisch indexeren van punten.</span><span class="sxs-lookup"><span data-stu-id="30007-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="30007-146">Coördinaat referentiesystemen</span><span class="sxs-lookup"><span data-stu-id="30007-146">Coordinate reference systems</span></span>
<span data-ttu-id="30007-147">Omdat Hallo vorm van Hallo earth onregelmatige is, wordt veel coördinaat referentiesystemen (CRS), elk met hun eigen frames van verwijzing en maateenheden coördinaten van georuimtelijke gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="30007-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="30007-148">Hallo 'National raster van-Brittannië' is bijvoorbeeld een referentiesysteem is zeer nauwkeurig voor Hallo Verenigd Koninkrijk, maar niet buiten.</span><span class="sxs-lookup"><span data-stu-id="30007-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="30007-149">Hallo populairste CRS in gebruik is vandaag de dag Hallo wereld geodetisch systeem [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="30007-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="30007-150">Gebruik WGS 84 GPS-apparaten en veel toewijzing services, met inbegrip van Google-kaarten en Bing kaarten-API's.</span><span class="sxs-lookup"><span data-stu-id="30007-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="30007-151">Azure Cosmos DB ondersteunt indexeren en query's naar georuimtelijke gegevens met behulp van Hallo WGS 84 CRS alleen.</span><span class="sxs-lookup"><span data-stu-id="30007-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="30007-152">Maken van documenten met ruimtelijke gegevens</span><span class="sxs-lookup"><span data-stu-id="30007-152">Creating documents with spatial data</span></span>
<span data-ttu-id="30007-153">Bij het maken van documenten die GeoJSON-waarden bevatten, worden ze automatisch geïndexeerd met een ruimtelijke index in overeenstemming toohello indexeringsbeleid van Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="30007-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="30007-154">Als u met een Azure-SDK Cosmos-database in een dynamisch getypeerde taal zoals Python of Node.js werkt, moet u geldige GeoJSON maken.</span><span class="sxs-lookup"><span data-stu-id="30007-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="30007-155">**Document maken met georuimtelijke gegevens in Node.js**</span><span class="sxs-lookup"><span data-stu-id="30007-155">**Create Document with Geospatial data in Node.js**</span></span>

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

<span data-ttu-id="30007-156">Als u met DocumentDB APIs hello werkt, kunt u Hallo `Point` en `Polygon` klassen in Hallo `Microsoft.Azure.Documents.Spatial` naamruimte tooembed locatiegegevens binnen uw toepassingsobjecten.</span><span class="sxs-lookup"><span data-stu-id="30007-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="30007-157">Deze klassen vereenvoudigen Hallo serialisatie en deserialisatie van ruimtelijke gegevens in GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="30007-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="30007-158">**Document met georuimtelijke gegevens in .NET maken**</span><span class="sxs-lookup"><span data-stu-id="30007-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="30007-159">Als u niet beschikt over de breedtegraad en lengtegraad informatie Hallo maar Hallo fysieke adressen of de naam van de locatie zoals plaats of land hebt, kunt u de werkelijke coördinaten Hallo opzoeken met behulp van een geocodering service, zoals Bing Maps REST-Services.</span><span class="sxs-lookup"><span data-stu-id="30007-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="30007-160">Meer informatie over geocodering van Bing Maps [hier](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="30007-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="30007-161">Spatiale typen opvragen</span><span class="sxs-lookup"><span data-stu-id="30007-161">Querying spatial types</span></span>
<span data-ttu-id="30007-162">Nu dat we kijken hoe hebt genomen tooinsert georuimtelijke gegevens, eens kijken hoe tooquery deze gegevens met behulp van Azure Cosmos DB met SQL en LINQ.</span><span class="sxs-lookup"><span data-stu-id="30007-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="30007-163">Ruimtelijke ingebouwde SQL-functies</span><span class="sxs-lookup"><span data-stu-id="30007-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="30007-164">Azure Cosmos DB ondersteunt Hallo Open georuimtelijke Consortium (OGC) ingebouwde functies voor georuimtelijke query's te volgen.</span><span class="sxs-lookup"><span data-stu-id="30007-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="30007-165">Voor meer informatie over de volledige reeks ingebouwde functies in SQL-taal Hallo Hallo Raadpleeg te[Query Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="30007-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="30007-166"><strong>Gebruik</strong></span><span class="sxs-lookup"><span data-stu-id="30007-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="30007-167"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="30007-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="30007-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="30007-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="30007-169">Retourneert Hallo afstand tussen twee Hallo GeoJSON punt, Polygon of LineString expressies.</span><span class="sxs-lookup"><span data-stu-id="30007-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="30007-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="30007-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="30007-171">Retourneert een Booleaanse expressie die aangeeft of Hallo eerste GeoJSON-object (punt, Polygon of LineString) binnen Hallo tweede GeoJSON-object (punt, Polygon of LineString).</span><span class="sxs-lookup"><span data-stu-id="30007-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="30007-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="30007-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="30007-173">Retourneert een Booleaanse expressie die aangeeft of Hallo twee opgegeven GeoJSON-objecten (punt, Polygon of LineString) intersect.</span><span class="sxs-lookup"><span data-stu-id="30007-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="30007-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="30007-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="30007-175">Retourneert een Booleaanse waarde die aangeeft of Hallo opgegeven GeoJSON punt, Polygon of LineString expressie is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="30007-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="30007-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="30007-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="30007-177">Retourneert een JSON-waarde met een Boolean-waarde als Hallo GeoJSON punt, Polygon of LineString expressie opgegeven geldig is en als ongeldig, bovendien Hallo reden als een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="30007-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="30007-178">Ruimtelijke functies kunnen worden gebruikt tooperform nabijheid query's op ruimtelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="30007-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="30007-179">Hier is bijvoorbeeld een query waarmee alle familie documenten dat binnen 30 km Hallo opgegeven locatie Hallo ST_DISTANCE ingebouwde functie gebruikt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="30007-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="30007-180">**Query**</span><span class="sxs-lookup"><span data-stu-id="30007-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="30007-181">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="30007-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="30007-182">Als u ruimtelijke indexeren in uw indexeringsbeleid opneemt, kunnen klikt u vervolgens 'afstand query's ' worden geleverd efficiënt via Hallo index.</span><span class="sxs-lookup"><span data-stu-id="30007-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="30007-183">Zie voor meer informatie over het ruimtelijke indexeren Hallo hieronder.</span><span class="sxs-lookup"><span data-stu-id="30007-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="30007-184">Als u een ruimtelijke hebt index voor Hallo paden die is opgegeven, kunt u nog steeds ruimtelijke query's uitvoeren door te geven `x-ms-documentdb-query-enable-scan` aanvraag-header met waarde hello te 'true' ingesteld.</span><span class="sxs-lookup"><span data-stu-id="30007-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="30007-185">In .NET, kunt dit doen door de optionele Hallo doorgeven **FeedOptions** argument tooqueries met [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) tootrue ingesteld.</span><span class="sxs-lookup"><span data-stu-id="30007-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="30007-186">ST_WITHIN zijn gebruikte toocheck als een punt binnen een Polygoon ligt.</span><span class="sxs-lookup"><span data-stu-id="30007-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="30007-187">Veelhoek zijn vaak gebruikte toorepresent grenzen zoals zip-codes, status grenzen of natuurlijke formaties.</span><span class="sxs-lookup"><span data-stu-id="30007-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="30007-188">Opnieuw als u ruimtelijke indexeren in uw indexeringsbeleid opneemt, klikt u vervolgens 'in' query's kunnen worden geleverd efficiënt via Hallo index.</span><span class="sxs-lookup"><span data-stu-id="30007-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="30007-189">Argumenten van de veelhoek in ST_WITHIN mag slechts één keer, dat wil zeggen Hallo veelhoek mag geen gaten in deze.</span><span class="sxs-lookup"><span data-stu-id="30007-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="30007-190">**Query**</span><span class="sxs-lookup"><span data-stu-id="30007-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="30007-191">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="30007-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="30007-192">Soortgelijke toohow verkeerde werkt in Azure Cosmos DB-query als Hallo locatiewaarde opgegeven een argument is onjuist gevormd of ongeldig, deze te evalueren**niet-gedefinieerde** en Hallo geëvalueerd document toobe van Hallo overgeslagen de resultaten van de query.</span><span class="sxs-lookup"><span data-stu-id="30007-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="30007-193">Als de query geen resultaten oplevert, voert u ST_ISVALIDDETAILED toodebug waarom Hallo spatail type ongeldig is.</span><span class="sxs-lookup"><span data-stu-id="30007-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="30007-194">Azure Cosmos DB biedt ook ondersteuning voor inverse query's uitvoeren, dat wil zeggen u kunt indexeren Multilinestring of regels in een Azure Cosmos DB en vervolgens zoeken naar Hallo gebieden die een opgegeven punt bevatten.</span><span class="sxs-lookup"><span data-stu-id="30007-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="30007-195">Dit patroon wordt vaak gebruikt in logistiek tooidentify bijvoorbeeld wanneer een vrachtwagen binnengaat of verlaat een aangewezen gebied.</span><span class="sxs-lookup"><span data-stu-id="30007-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="30007-196">**Query**</span><span class="sxs-lookup"><span data-stu-id="30007-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="30007-197">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="30007-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="30007-198">ST_ISVALID en ST_ISVALIDDETAILED kunnen gebruikte toocheck zich als een ruimtelijke object geldig is.</span><span class="sxs-lookup"><span data-stu-id="30007-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="30007-199">Hallo na query controleert bijvoorbeeld Hallo geldigheid van een punt met een out-of breedtegraad bereikwaarde (-132.8).</span><span class="sxs-lookup"><span data-stu-id="30007-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="30007-200">ST_ISVALID alleen een Booleaanse waarde retourneert en ST_ISVALIDDETAILED retourneert Hallo Booleaanse waarde en een tekenreeks met Hallo reden waarom het wordt als ongeldig beschouwd.</span><span class="sxs-lookup"><span data-stu-id="30007-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="30007-201">** Query **</span><span class="sxs-lookup"><span data-stu-id="30007-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="30007-202">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="30007-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="30007-203">Deze functies kunnen ook worden gebruikt toovalidate veelhoek.</span><span class="sxs-lookup"><span data-stu-id="30007-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="30007-204">Bijvoorbeeld, hier gebruiken we ST_ISVALIDDETAILED toovalidate een Polygoon die niet wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="30007-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="30007-205">**Query**</span><span class="sxs-lookup"><span data-stu-id="30007-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="30007-206">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="30007-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="30007-207">LINQ een query uitvoert op Hallo .NET SDK</span><span class="sxs-lookup"><span data-stu-id="30007-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="30007-208">Hallo DocumentDB .NET SDK ook providers stub-methoden `Distance()` en `Within()` voor gebruik in een LINQ-expressies.</span><span class="sxs-lookup"><span data-stu-id="30007-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="30007-209">Hallo DocumentDB LINQ-provider vertaalt deze methode aanroepen toohello gelijkwaardige SQL ingebouwde functieaanroepen (ST_DISTANCE en ST_WITHIN respectievelijk).</span><span class="sxs-lookup"><span data-stu-id="30007-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="30007-210">Hier volgt een voorbeeld van een LINQ-query waarmee wordt gezocht naar alle documenten in hello Azure Cosmos DB verzameling waarvan de waarde 'locatie' wordt binnen een straal van 30km Hallo opgegeven verwijzen met behulp van LINQ.</span><span class="sxs-lookup"><span data-stu-id="30007-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="30007-211">**LINQ-query voor afstand**</span><span class="sxs-lookup"><span data-stu-id="30007-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="30007-212">Hier is ook een query voor het zoeken naar alle Hallo documenten waarvan 'locatie' binnen Hallo valt vak/veelhoek opgegeven.</span><span class="sxs-lookup"><span data-stu-id="30007-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="30007-213">**LINQ-query voor binnen**</span><span class="sxs-lookup"><span data-stu-id="30007-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="30007-214">Nu dat we kijken hoe hebt genomen tooquery documenten met behulp van LINQ en SQL, eens kijken hoe tooconfigure Azure Cosmos DB voor ruimtelijke indexeren.</span><span class="sxs-lookup"><span data-stu-id="30007-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="30007-215">Indexeren</span><span class="sxs-lookup"><span data-stu-id="30007-215">Indexing</span></span>
<span data-ttu-id="30007-216">Zoals wordt beschreven in Hallo [Schema Networkdirect indexering met Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papier we Azure Cosmos DB database-engine toobe ontworpen echt schema networkdirect en eerste-klas ondersteuning bieden voor JSON.</span><span class="sxs-lookup"><span data-stu-id="30007-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="30007-217">Hallo schrijven die zijn geoptimaliseerd voor database-engine van Azure DB die Cosmos begrijpt systeemeigen ruimtelijke gegevens (points, Multilinestring en regels) in Hallo GeoJSON standaard weergegeven.</span><span class="sxs-lookup"><span data-stu-id="30007-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="30007-218">Kortom, Hallo geometrie wordt geprojecteerd van geodetisch coördinaten op een 2D vlak vervolgens geleidelijk onderverdeeld in de cellen met behulp van een **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="30007-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="30007-219">Deze cellen zijn toegewezen too1D op basis van locatie Hallo van Hallo cel binnen een **Hilbert ruimte vullen curve**, die de plaats van punten behouden blijft.</span><span class="sxs-lookup"><span data-stu-id="30007-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="30007-220">Bovendien wanneer locatiegegevens wordt geïndexeerd, wordt er een proces genaamd **mozaïekpatroon**, dat wil zeggen alle Hallo cellen die een locatie intersect worden geïdentificeerd en opgeslagen als sleutels in hello Azure Cosmos DB index.</span><span class="sxs-lookup"><span data-stu-id="30007-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="30007-221">Op het moment dat de query, argumenten zoals punten en Veelhoek ook representatie mozaïekpatroon tooextract zijn Hallo relevante cel ID bereiken en vervolgens tooretrieve gegevens van de index Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="30007-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="30007-222">Als u een indexeringsbeleid met ruimtelijke index voor / * (alle paden) en vervolgens alle punten gevonden binnen de verzameling Hallo worden geïndexeerd voor efficiënte ruimtelijke query's (ST_WITHIN en ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="30007-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="30007-223">Ruimtelijke indexen niet hebben een precisiewaarde, en gebruik altijd een standaardwaarde precisie.</span><span class="sxs-lookup"><span data-stu-id="30007-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="30007-224">Azure Cosmos DB biedt ondersteuning voor automatisch indexeren van punten, Multilinestring en multipoint</span><span class="sxs-lookup"><span data-stu-id="30007-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="30007-225">Hallo volgende JSON-fragment toont een indexeringsbeleid met ruimtelijke indexeren is ingeschakeld, dat wil zeggen indexnummer nergens GeoJSON gevonden binnen documenten ruimtelijke query's.</span><span class="sxs-lookup"><span data-stu-id="30007-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="30007-226">Als u indexeren met behulp van Azure Portal Hallo Hallo wijzigt, kunt u Hallo JSON volgen voor indexeren beleid tooenable ruimtelijke indexeren op uw verzameling opgeven.</span><span class="sxs-lookup"><span data-stu-id="30007-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="30007-227">**Verzameling indexeren JSON met Spatial ingeschakeld voor punten en Veelhoek beleid**</span><span class="sxs-lookup"><span data-stu-id="30007-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="30007-228">Hier volgt een codefragment in .NET die laat hoe een verzameling zien met ruimtelijke indexeren toocreate ingeschakeld voor alle paden die punten bevat.</span><span class="sxs-lookup"><span data-stu-id="30007-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="30007-229">**Maak een verzameling met ruimtelijke indexeren**</span><span class="sxs-lookup"><span data-stu-id="30007-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="30007-230">En hier ziet u hoe u een bestaande verzameling tootake voordeel van het ruimtelijke indexeren via alle punten die zijn opgeslagen in de documenten kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="30007-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="30007-231">**Een bestaande verzameling met ruimtelijke indexeren wijzigen**</span><span class="sxs-lookup"><span data-stu-id="30007-231">**Modify an existing collection with spatial indexing**</span></span>

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
> <span data-ttu-id="30007-232">Als Hallo locatie GeoJSON-waarde in het document Hallo onjuist gevormd of ongeldig is, wordt klikt u vervolgens het niet geïndexeerd ruimtelijke query's.</span><span class="sxs-lookup"><span data-stu-id="30007-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="30007-233">U kunt de locatie van waarden met ST_ISVALID en ST_ISVALIDDETAILED valideren.</span><span class="sxs-lookup"><span data-stu-id="30007-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="30007-234">Als de definitie van de verzameling een partitiesleutel bevat, is indexeren voortgang van de transformatie niet gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="30007-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="30007-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="30007-235">Next steps</span></span>
<span data-ttu-id="30007-236">Nu dat u hebt vernomen over hoe tooget met ondersteuning voor georuimtelijke in Azure Cosmos DB gestart, kunt u:</span><span class="sxs-lookup"><span data-stu-id="30007-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="30007-237">Gaan coderen Hello [georuimtelijke .NET-codevoorbeelden op GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="30007-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="30007-238">U handen op waarop het georuimtelijke opvragen op Hallo [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="30007-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="30007-239">Meer informatie over [Azure Cosmos DB-Query](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="30007-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="30007-240">Meer informatie over [Azure Cosmos DB indexeren beleid](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="30007-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

