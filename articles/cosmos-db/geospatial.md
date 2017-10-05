---
title: Werken met gegevens in Azure Cosmos DB georuimtelijke | Microsoft Docs
description: Begrijpen hoe maken, index en query ruimtelijke-objecten met Azure Cosmos DB en de DocumentDB-API.
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
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="e2321-103">Werken met georuimtelijke en GeoJSON locatiegegevens in Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="e2321-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="e2321-104">In dit artikel bevat een inleiding tot de functionaliteit georuimtelijke in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="e2321-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="e2321-105">Na het lezen van dit, kunt u zich de volgende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="e2321-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="e2321-106">Hoe kan ik ruimtelijke gegevens opslaan in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e2321-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="e2321-107">Hoe kan ik een query over gegevens in Azure Cosmos-database in SQL- en LINQ georuimtelijke?</span><span class="sxs-lookup"><span data-stu-id="e2321-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="e2321-108">Hoe ik in- of uitschakelen ruimtelijke indexeren in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e2321-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="e2321-109">Dit artikel laat zien hoe u werkt met ruimtelijke gegevens met de DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="e2321-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="e2321-110">Raadpleeg dit [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) voor codevoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e2321-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="e2321-111">Inleiding tot ruimtelijke gegevens</span><span class="sxs-lookup"><span data-stu-id="e2321-111">Introduction to spatial data</span></span>
<span data-ttu-id="e2321-112">Ruimtelijke gegevens beschrijft de positie en de vorm van objecten in de ruimte.</span><span class="sxs-lookup"><span data-stu-id="e2321-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="e2321-113">In de meeste toepassingen deze komen overeen met objecten op de aarde, dat wil zeggen georuimtelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="e2321-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="e2321-114">Ruimtelijke gegevens kunnen worden gebruikt voor de locatie van een persoon, een plaats van belang of de grens van een stad of een meer.</span><span class="sxs-lookup"><span data-stu-id="e2321-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="e2321-115">Algemene gebruiksvoorbeelden inhouden vaak nabijheid query's voor bijvoorbeeld 'vinden alle in internetcafés in de buurt van mijn huidige locatie'.</span><span class="sxs-lookup"><span data-stu-id="e2321-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="e2321-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="e2321-116">GeoJSON</span></span>
<span data-ttu-id="e2321-117">Azure Cosmos-DB biedt ondersteuning voor indexering en query's naar georuimtelijke gegevens die is weergegeven met behulp van de [GeoJSON-specificatie](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="e2321-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="e2321-118">GeoJSON gegevensstructuren zijn altijd geldig JSON-objecten, zodat ze kunnen worden opgeslagen en opgevraagd met Azure Cosmos DB zonder speciale hulpprogramma's of bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="e2321-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="e2321-119">De Azure Cosmos DB SDK's bieden helperklassen en methoden die gemakkelijk te werken met ruimtelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="e2321-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="e2321-120">Punten, multipoint en Veelhoek</span><span class="sxs-lookup"><span data-stu-id="e2321-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="e2321-121">Een **punt** wordt bepaald door een enkele positie in de ruimte.</span><span class="sxs-lookup"><span data-stu-id="e2321-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="e2321-122">Een punt vertegenwoordigt georuimtelijke gegevens, de exacte locatie, wat erop kan een adres van een winkelketen, een kiosk, een auto of een plaats.</span><span class="sxs-lookup"><span data-stu-id="e2321-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="e2321-123">GeoJSON (en Azure Cosmos DB) met behulp van de coördinaat paar of de lengte en de breedte van een punt wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e2321-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="e2321-124">Hier volgt een voorbeeld van JSON voor een punt.</span><span class="sxs-lookup"><span data-stu-id="e2321-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="e2321-125">**Punten in Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="e2321-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="e2321-126">Het GeoJSON-specificatie bevat lengtegraad eerste en breedtegraad tweede.</span><span class="sxs-lookup"><span data-stu-id="e2321-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="e2321-127">Net als in andere toepassingen toewijzing breedtegraad worden hoeken en vertegenwoordigd in termen van graden.</span><span class="sxs-lookup"><span data-stu-id="e2321-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="e2321-128">Lengtegraadwaarden van de nulmeridiaan worden gemeten en zijn tussen-180 en 180.0 graden en breedtegraad waarden van de evenaar worden gemeten en zijn tussen-90.0 en 90.0 graden.</span><span class="sxs-lookup"><span data-stu-id="e2321-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="e2321-129">Azure Cosmos DB interpreteert coördinaten, zoals wordt weergegeven per het referentiesysteem WGS 84.</span><span class="sxs-lookup"><span data-stu-id="e2321-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="e2321-130">Zie hieronder voor meer informatie over coördinaat referentiesystemen.</span><span class="sxs-lookup"><span data-stu-id="e2321-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="e2321-131">Dit kan worden ingesloten in een document Azure Cosmos DB zoals in dit voorbeeld van een gebruikersprofiel met locatiegegevens:</span><span class="sxs-lookup"><span data-stu-id="e2321-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="e2321-132">**Gebruik het profiel met locatie opgeslagen in Azure Cosmos-DB**</span><span class="sxs-lookup"><span data-stu-id="e2321-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="e2321-133">Naast punten ondersteunt GeoJSON ook multipoint en veelhoek.</span><span class="sxs-lookup"><span data-stu-id="e2321-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="e2321-134">**Multipoint** vertegenwoordigen een reeks van twee of meer punten in de lijnsegmenten waarmee ze verbinding maken en de ruimte.</span><span class="sxs-lookup"><span data-stu-id="e2321-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="e2321-135">In georuimtelijke gegevens wordt multipoint vaak gebruikt om te wegen of rivieren vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="e2321-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="e2321-136">Een **veelhoek** is een grens verbonden punten die een gesloten LineString vormt.</span><span class="sxs-lookup"><span data-stu-id="e2321-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="e2321-137">Veelhoek wordt vaak gebruikt om natuurlijke formaties zoals meren of politieke rechtsgebieden zoals steden en statussen te geven.</span><span class="sxs-lookup"><span data-stu-id="e2321-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="e2321-138">Hier volgt een voorbeeld van een Polygoon in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2321-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="e2321-139">**Veelhoek in GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="e2321-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="e2321-140">De specificatie GeoJSON vereist dat voor geldige veelhoek het laatste coördinaat paar opgegeven moet hetzelfde zijn als de eerste pagina, voor het maken van een gesloten vorm.</span><span class="sxs-lookup"><span data-stu-id="e2321-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="e2321-141">Punten in een Polygoon moeten worden opgegeven in rechtsom volgorde.</span><span class="sxs-lookup"><span data-stu-id="e2321-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="e2321-142">Een Polygoon die is opgegeven in rechtsom volgorde vertegenwoordigt de inverse van de regio binnen deze.</span><span class="sxs-lookup"><span data-stu-id="e2321-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="e2321-143">Naast Point, LineString, en Veelhoek GeoJSON ook Hiermee geeft u de weergave voor het groeperen van meerdere locaties voor georuimtelijke, evenals willekeurige eigenschappen koppelen aan geolocatie als een **functie**.</span><span class="sxs-lookup"><span data-stu-id="e2321-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="e2321-144">Aangezien deze objecten geldige JSON zijn, kunnen ze alle worden opgeslagen en verwerkt in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2321-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="e2321-145">Maar Azure Cosmos DB biedt alleen ondersteuning voor automatisch indexeren van punten.</span><span class="sxs-lookup"><span data-stu-id="e2321-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="e2321-146">Coördinaat referentiesystemen</span><span class="sxs-lookup"><span data-stu-id="e2321-146">Coordinate reference systems</span></span>
<span data-ttu-id="e2321-147">Omdat de vorm van de aarde onregelmatige is, wordt veel coördinaat referentiesystemen (CRS), elk met hun eigen frames van verwijzing en maateenheden coördinaten van georuimtelijke gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e2321-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="e2321-148">Bijvoorbeeld, de 'National raster van-Brittannië' is een referentiesysteem zeer nauwkeurig is voor het Verenigd Koninkrijk, maar niet buiten.</span><span class="sxs-lookup"><span data-stu-id="e2321-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="e2321-149">De meest populaire CRS in gebruik is vandaag de dag de wereld geodetisch systeem [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="e2321-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="e2321-150">Gebruik WGS 84 GPS-apparaten en veel toewijzing services, met inbegrip van Google-kaarten en Bing kaarten-API's.</span><span class="sxs-lookup"><span data-stu-id="e2321-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="e2321-151">Azure Cosmos DB ondersteunt indexeren en query's naar georuimtelijke gegevens met behulp van de WGS 84 CRS alleen.</span><span class="sxs-lookup"><span data-stu-id="e2321-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="e2321-152">Maken van documenten met ruimtelijke gegevens</span><span class="sxs-lookup"><span data-stu-id="e2321-152">Creating documents with spatial data</span></span>
<span data-ttu-id="e2321-153">Bij het maken van documenten die GeoJSON-waarden bevatten, worden ze automatisch geïndexeerd met een ruimtelijke index overeenkomstig het indexeringsbeleid van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="e2321-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="e2321-154">Als u met een Azure-SDK Cosmos-database in een dynamisch getypeerde taal zoals Python of Node.js werkt, moet u geldige GeoJSON maken.</span><span class="sxs-lookup"><span data-stu-id="e2321-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="e2321-155">**Document maken met georuimtelijke gegevens in Node.js**</span><span class="sxs-lookup"><span data-stu-id="e2321-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="e2321-156">Als u met de APIs DocumentDB werkt, kunt u de `Point` en `Polygon` klassen binnen de `Microsoft.Azure.Documents.Spatial` naamruimte voor het insluiten van locatie-informatie in uw toepassingsobjecten.</span><span class="sxs-lookup"><span data-stu-id="e2321-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="e2321-157">Deze klassen vereenvoudigen de serialisatie en deserialisatie van ruimtelijke gegevens in GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="e2321-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="e2321-158">**Document met georuimtelijke gegevens in .NET maken**</span><span class="sxs-lookup"><span data-stu-id="e2321-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="e2321-159">Als u niet beschikt over de breedtegraad en lengtegraad informatie, maar u beschikt over de fysieke adressen of de locatienaam zoals plaats of land, kunt u de werkelijke coördinaten opzoeken met behulp van een geocodering service, zoals Bing Maps REST-Services.</span><span class="sxs-lookup"><span data-stu-id="e2321-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="e2321-160">Meer informatie over geocodering van Bing Maps [hier](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2321-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="e2321-161">Spatiale typen opvragen</span><span class="sxs-lookup"><span data-stu-id="e2321-161">Querying spatial types</span></span>
<span data-ttu-id="e2321-162">Nu dat we kijken hoe georuimtelijke gegevens invoegen, eens kijken hoe deze gegevens met behulp van Azure Cosmos DB met SQL en LINQ query hebt genomen.</span><span class="sxs-lookup"><span data-stu-id="e2321-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="e2321-163">Ruimtelijke ingebouwde SQL-functies</span><span class="sxs-lookup"><span data-stu-id="e2321-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="e2321-164">Azure Cosmos DB ondersteunt de volgende ingebouwde functies voor Open georuimtelijke Consortium (OGC) georuimtelijke query's.</span><span class="sxs-lookup"><span data-stu-id="e2321-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="e2321-165">Raadpleeg voor meer informatie over de volledige reeks ingebouwde functies in de SQL-taal, [Query Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="e2321-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="e2321-166"><strong>Gebruik</strong></span><span class="sxs-lookup"><span data-stu-id="e2321-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="e2321-167"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="e2321-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e2321-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="e2321-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="e2321-169">Retourneert de afstand tussen de twee GeoJSON punt, Polygon of LineString expressies.</span><span class="sxs-lookup"><span data-stu-id="e2321-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e2321-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="e2321-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="e2321-171">Retourneert een Booleaanse expressie die aangeeft of het eerste GeoJSON-object (punt, Polygon of LineString) binnen het tweede GeoJSON-object (punt, Polygon of LineString).</span><span class="sxs-lookup"><span data-stu-id="e2321-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e2321-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="e2321-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="e2321-173">Retourneert een Booleaanse expressie waarmee wordt aangegeven of de twee opgegeven GeoJSON objecten (punt, Polygon of LineString) intersect.</span><span class="sxs-lookup"><span data-stu-id="e2321-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e2321-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="e2321-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="e2321-175">Retourneert een Booleaanse waarde die aangeeft of de opgegeven expressie voor GeoJSON punt, Polygon of LineString ongeldig is.</span><span class="sxs-lookup"><span data-stu-id="e2321-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="e2321-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="e2321-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="e2321-177">Retourneert een JSON-waarde met een Booleaanse waarde als de opgegeven expressie voor GeoJSON punt, Polygon of LineString is geldig, en als ongeldig, ook de reden als een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="e2321-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="e2321-178">Ruimtelijke functies kunnen worden gebruikt om uit te voeren nabijheid query's op ruimtelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="e2321-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="e2321-179">Hier is bijvoorbeeld een query die alle familie documenten die binnen 30 km van de opgegeven locatie met de ingebouwde functie ST_DISTANCE retourneert.</span><span class="sxs-lookup"><span data-stu-id="e2321-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="e2321-180">**Query**</span><span class="sxs-lookup"><span data-stu-id="e2321-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="e2321-181">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="e2321-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="e2321-182">Als u ruimtelijke indexeren in uw indexeringsbeleid opneemt, kunnen klikt u vervolgens 'afstand query's ' worden geleverd efficiënt via de index.</span><span class="sxs-lookup"><span data-stu-id="e2321-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="e2321-183">Zie de sectie hieronder voor meer informatie over het ruimtelijke indexeren.</span><span class="sxs-lookup"><span data-stu-id="e2321-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="e2321-184">Als u een ruimtelijke index voor de opgegeven paden niet hebt, kunt u nog steeds ruimtelijke query's uitvoeren door te geven `x-ms-documentdb-query-enable-scan` aanvraag-header met de waarde ingesteld op 'true'.</span><span class="sxs-lookup"><span data-stu-id="e2321-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="e2321-185">In .NET, kunt dit doen door de optionele **FeedOptions** argument voor query's met [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="e2321-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="e2321-186">ST_WITHIN kan worden gebruikt om te controleren of een punt binnen een Polygoon liggen.</span><span class="sxs-lookup"><span data-stu-id="e2321-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="e2321-187">Veelhoek worden vaak gebruikt om grenzen zoals zip-codes, status grenzen of natuurlijke formaties vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="e2321-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="e2321-188">Opnieuw als u ruimtelijke indexeren in uw indexeringsbeleid opneemt, klikt u vervolgens 'in' query's kunnen worden geleverd efficiënt via de index.</span><span class="sxs-lookup"><span data-stu-id="e2321-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="e2321-189">Argumenten van de veelhoek in ST_WITHIN mag slechts één keer, dat wil zeggen de veelhoek mag geen gaten bevat.</span><span class="sxs-lookup"><span data-stu-id="e2321-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="e2321-190">**Query**</span><span class="sxs-lookup"><span data-stu-id="e2321-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="e2321-191">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="e2321-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="e2321-192">Vergelijkbaar met hoe niet-overeenkomende typen werkt in Azure Cosmos DB-query als de locatiewaarde opgegeven een argument is onjuist gevormd of ongeldig, deze wordt geëvalueerd als **niet-gedefinieerde** en het geëvalueerde document van de query overgeslagen resultaten.</span><span class="sxs-lookup"><span data-stu-id="e2321-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="e2321-193">Als de query geen resultaten oplevert, voert u ST_ISVALIDDETAILED voor foutopsporing waarom het type spatail ongeldig is.</span><span class="sxs-lookup"><span data-stu-id="e2321-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="e2321-194">Azure Cosmos DB biedt ook ondersteuning voor inverse query's uitvoeren, dat wil zeggen u kunt indexeren Multilinestring of regels in een Azure Cosmos DB en vervolgens een query voor de gebieden die een opgegeven punt bevatten.</span><span class="sxs-lookup"><span data-stu-id="e2321-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="e2321-195">Dit patroon wordt meestal gebruikt in logistiek om te identificeren, bijvoorbeeld wanneer een vrachtwagen binnengaat of verlaat een aangewezen gebied.</span><span class="sxs-lookup"><span data-stu-id="e2321-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="e2321-196">**Query**</span><span class="sxs-lookup"><span data-stu-id="e2321-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="e2321-197">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="e2321-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="e2321-198">ST_ISVALID en ST_ISVALIDDETAILED kunnen worden gebruikt om te controleren of een ruimtelijke object geldig is.</span><span class="sxs-lookup"><span data-stu-id="e2321-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="e2321-199">Bijvoorbeeld controleert de volgende query de geldigheid van een punt met een out-of breedtegraad bereikwaarde (-132.8).</span><span class="sxs-lookup"><span data-stu-id="e2321-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="e2321-200">ST_ISVALID alleen een Booleaanse waarde retourneert en ST_ISVALIDDETAILED retourneert de Booleaanse waarde en een tekenreeks met de reden waarom het wordt als ongeldig beschouwd.</span><span class="sxs-lookup"><span data-stu-id="e2321-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="e2321-201">** Query **</span><span class="sxs-lookup"><span data-stu-id="e2321-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="e2321-202">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="e2321-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="e2321-203">Deze functies kunnen ook worden gebruikt voor het valideren van de veelhoek.</span><span class="sxs-lookup"><span data-stu-id="e2321-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="e2321-204">Bijvoorbeeld, hier gebruiken we ST_ISVALIDDETAILED valideren van een Polygoon die niet wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="e2321-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="e2321-205">**Query**</span><span class="sxs-lookup"><span data-stu-id="e2321-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="e2321-206">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="e2321-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="e2321-207">LINQ-query in de .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e2321-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="e2321-208">De DocumentDB .NET SDK ook providers stub-methoden `Distance()` en `Within()` voor gebruik in een LINQ-expressies.</span><span class="sxs-lookup"><span data-stu-id="e2321-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="e2321-209">De DocumentDB LINQ-provider vertaalt deze methodeaanroepen naar de equivalente SQL ingebouwde functieaanroepen (ST_DISTANCE en ST_WITHIN respectievelijk).</span><span class="sxs-lookup"><span data-stu-id="e2321-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="e2321-210">Hier volgt een voorbeeld van een LINQ-query waarmee wordt gezocht naar alle documenten in de Azure DB die Cosmos-verzameling waarvan de waarde 'locatie' wordt binnen een straal van 30km van de opgegeven verwijzen met behulp van LINQ.</span><span class="sxs-lookup"><span data-stu-id="e2321-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="e2321-211">**LINQ-query voor afstand**</span><span class="sxs-lookup"><span data-stu-id="e2321-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="e2321-212">Hier wordt ook een query voor het zoeken naar alle documenten waarvan 'locatie' binnen de opgegeven vak/veelhoek is.</span><span class="sxs-lookup"><span data-stu-id="e2321-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="e2321-213">**LINQ-query voor binnen**</span><span class="sxs-lookup"><span data-stu-id="e2321-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="e2321-214">Nu dat we kijken hoe documenten met behulp van de LINQ- en SQL query hebt gemaakt, gaat u nu een overzicht van het configureren van Azure DB die Cosmos voor ruimtelijke indexeren.</span><span class="sxs-lookup"><span data-stu-id="e2321-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="e2321-215">Indexeren</span><span class="sxs-lookup"><span data-stu-id="e2321-215">Indexing</span></span>
<span data-ttu-id="e2321-216">Zoals wordt beschreven in de [Schema Networkdirect indexering met Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) artikel, dat we Azure Cosmos DB database-engine worden ontworpen echt schema networkdirect en eerste-klas ondersteuning bieden voor JSON.</span><span class="sxs-lookup"><span data-stu-id="e2321-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="e2321-217">De schrijven die zijn geoptimaliseerd voor database-engine van Azure DB die Cosmos begrijpt systeemeigen ruimtelijke gegevens (punten, Multilinestring en regels) weergegeven in de standaard GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="e2321-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="e2321-218">Kortom, de geometrie wordt geprojecteerd van geodetisch coördinaten op een 2D vlak vervolgens geleidelijk onderverdeeld in de cellen met behulp van een **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="e2321-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="e2321-219">Deze cellen zijn toegewezen aan 1D op basis van de locatie van de cel binnen een **Hilbert ruimte vullen curve**, die de plaats van punten behouden blijft.</span><span class="sxs-lookup"><span data-stu-id="e2321-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="e2321-220">Bovendien wanneer locatiegegevens wordt geïndexeerd, wordt er een proces genaamd **mozaïekpatroon**, dat wil zeggen alle cellen met een locatie intersect worden geïdentificeerd en opgeslagen als sleutels in de Azure DB die Cosmos-index.</span><span class="sxs-lookup"><span data-stu-id="e2321-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="e2321-221">Op het moment dat de query, argumenten zoals points en Veelhoek zijn ook representatie mozaïekpatroon om op te halen van de betreffende cel ID bereiken, en vervolgens gebruikt voor het ophalen van gegevens vanaf de index.</span><span class="sxs-lookup"><span data-stu-id="e2321-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="e2321-222">Als u een indexeringsbeleid met ruimtelijke index voor / * (alle paden) en vervolgens alle punten gevonden binnen de verzameling worden geïndexeerd voor efficiënte ruimtelijke query's (ST_WITHIN en ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="e2321-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="e2321-223">Ruimtelijke indexen niet hebben een precisiewaarde, en gebruik altijd een standaardwaarde precisie.</span><span class="sxs-lookup"><span data-stu-id="e2321-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="e2321-224">Azure Cosmos DB biedt ondersteuning voor automatisch indexeren van punten, Multilinestring en multipoint</span><span class="sxs-lookup"><span data-stu-id="e2321-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="e2321-225">Het volgende JSON-fragment toont een indexeringsbeleid met ruimtelijke indexeren is ingeschakeld, dat wil zeggen indexnummer nergens GeoJSON gevonden binnen documenten ruimtelijke query's.</span><span class="sxs-lookup"><span data-stu-id="e2321-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="e2321-226">Als u het indexeringsbeleid met de Azure Portal wijzigt, kunt u de volgende JSON voor indexeringsbeleid om in te schakelen ruimtelijke indexeren op uw verzameling opgeven.</span><span class="sxs-lookup"><span data-stu-id="e2321-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="e2321-227">**Verzameling indexeren JSON met Spatial ingeschakeld voor punten en Veelhoek beleid**</span><span class="sxs-lookup"><span data-stu-id="e2321-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="e2321-228">Hier volgt een codefragment in .NET die laat hoe u een verzameling maken zien met ruimtelijke indexeren is ingeschakeld voor alle paden die punten bevat.</span><span class="sxs-lookup"><span data-stu-id="e2321-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="e2321-229">**Maak een verzameling met ruimtelijke indexeren**</span><span class="sxs-lookup"><span data-stu-id="e2321-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="e2321-230">En hier ziet u hoe u een bestaande verzameling om te profiteren van de ruimtelijke indexeren via alle punten die zijn opgeslagen in de documenten kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e2321-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="e2321-231">**Een bestaande verzameling met ruimtelijke indexeren wijzigen**</span><span class="sxs-lookup"><span data-stu-id="e2321-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="e2321-232">Als de locatie GeoJSON-waarde in het document onjuist gevormd of ongeldig is, wordt klikt u vervolgens het niet geïndexeerd ruimtelijke query's.</span><span class="sxs-lookup"><span data-stu-id="e2321-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="e2321-233">U kunt de locatie van waarden met ST_ISVALID en ST_ISVALIDDETAILED valideren.</span><span class="sxs-lookup"><span data-stu-id="e2321-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="e2321-234">Als de definitie van de verzameling een partitiesleutel bevat, is indexeren voortgang van de transformatie niet gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="e2321-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e2321-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2321-235">Next steps</span></span>
<span data-ttu-id="e2321-236">Nu dat u over het aan de slag met ondersteuning voor georuimtelijke in Azure Cosmos DB vernomen hebt, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e2321-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="e2321-237">Gaan coderen met de [georuimtelijke .NET-codevoorbeelden op GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="e2321-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="e2321-238">U handen op waarop het georuimtelijke uitvoeren van query's op de [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="e2321-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="e2321-239">Meer informatie over [Azure Cosmos DB-Query](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="e2321-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="e2321-240">Meer informatie over [Azure Cosmos DB indexeren beleid](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="e2321-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

