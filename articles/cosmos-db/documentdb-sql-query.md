---
title: aaaSQL query's voor Azure Cosmos DB DocumentDB-API | Microsoft Docs
description: Meer informatie over SQL-syntaxis, database-concepten en SQL-query's voor Azure Cosmos DB. SQL kan worden gebruikt als een JSON-querytaal in Azure Cosmos DB.
keywords: SQL-syntaxis, sql-query, sql-query's, json-querytaal, database-concepten en sql-query's, statistische functies
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="ab5c6-105">SQL-query's voor Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="ab5c6-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="ab5c6-106">Microsoft Azure Cosmos DB biedt ondersteuning voor documentquery's die gebruikmaken van SQL (Structured Query Language) als een JSON-querytaal.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="ab5c6-107">Cosmos DB is volledig zonder schema.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="ab5c6-108">Doordat de streven toohello JSON-gegevensmodel rechtstreeks in de database-engine hello biedt deze automatische indexering van JSON-documenten zonder expliciet schema of het maken van secundaire indexen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="ab5c6-109">Tijdens het Hallo-querytaal ontwerpen voor Cosmos DB, zijn twee drie doelen voor ogen:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="ab5c6-110">In plaats van een nieuwe JSON-querytaal vruchtbare, maar we wilden toosupport SQL.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="ab5c6-111">SQL is een van de talen voor Hallo bekend en meest populaire query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="ab5c6-112">Cosmos DB SQL biedt een formele programmeermodel voor uitgebreide query's via JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="ab5c6-113">Als een JSON-document-database kan worden uitgevoerd van JavaScript rechtstreeks in de database-engine Hallo wilden we van toouse JavaScript-programmeermodel Hallo basis voor onze querytaal.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="ab5c6-114">Hallo DocumentDB API SQL verankerd ligt in de JavaScript-typesysteem, evaluatie van expressies en functieaanroep.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="ab5c6-115">Deze beurt biedt een natuurlijke programmeermodel voor projecties relationele, hiërarchische navigatie in JSON-documenten, self joins, ruimtelijke query's en aanroep van de gebruiker gedefinieerde functies (UDF's) geschreven volledig in JavaScript, onder andere functies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="ab5c6-116">We zijn ervan overtuigd dat deze mogelijkheden belangrijke tooreducing Hallo wrijving tussen Hallo-toepassing en Hallo-database zijn en essentieel voor de productiviteit van ontwikkelaars zijn.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="ab5c6-117">We raden aan de slag door bekijkt hello volgende video Aravind Ramachandran toont waar opvragen mogelijkheden Cosmos-database, en in via onze [Queryspeelplaats](http://www.documentdb.com/sql/demo), waarbij u kunt Cosmos-database uitproberen en SQL-query's op uitvoeren onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="ab5c6-118">Keer vervolgens terug toothis artikel, waar u begint met een SQL-query-zelfstudie die u bij enkele eenvoudige JSON-documenten en de SQL-opdrachten helpt.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="ab5c6-119"><a id="GettingStarted"></a>Aan de slag met SQL-opdrachten in een Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="ab5c6-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="ab5c6-120">toosee Cosmos DB SQL op werken, laten we beginnen met een paar eenvoudige JSON-documenten en enkele eenvoudige query's op deze doorlopen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="ab5c6-121">U kunt deze twee JSON-documenten over twee families.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="ab5c6-122">Met Cosmos DB hoeven we geen toocreate geen schema's of secundaire indexen expliciet.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="ab5c6-123">Er hoeft alleen maar tooinsert Hallo JSON-documenten tooa Cosmos DB verzameling en vervolgens een query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="ab5c6-124">Hier hebben we een eenvoudige JSON Documenteer voor Hallo Andersen family, Hallo ouders, onderliggende elementen (en hun huisdieren), adres en registratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="ab5c6-125">Hallo document heeft tekenreeksen, getallen, Booleaanse waarden, matrices en geneste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="ab5c6-126">**Document**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-126">**Document**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="ab5c6-127">Hier volgt een tweede document een subtiele verschil – `givenName` en `familyName` worden gebruikt in plaats van `firstName` en `lastName`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="ab5c6-128">**Document**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-128">**Document**</span></span>  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

<span data-ttu-id="ab5c6-129">Nu gaan we proberen enkele query's op basis van deze gegevens toounderstand aantal Hallo aspecten van DocumentDB API SQL sleutel.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="ab5c6-130">Bijvoorbeeld, Hallo volgende query retourneert Hallo documenten waarbij veld Hallo-id overeenkomt met `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="ab5c6-131">Omdat het een `SELECT *`, Hallo-uitvoer van Hallo query Hallo voltooid JSON-document is:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="ab5c6-132">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ab5c6-133">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-133">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


<span data-ttu-id="ab5c6-134">Bekijk nu Hallo geval waar we tooreformat Hallo JSON-uitvoer in een andere vorm moeten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="ab5c6-135">Deze query projecten een nieuwe JSON object met twee geselecteerde velden naam en plaats, wanneer Hallo plaats Hallo dezelfde naam heeft als Hallo status.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="ab5c6-136">In dit geval 'NY, NY' komt overeen met.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="ab5c6-137">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="ab5c6-138">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="ab5c6-139">de volgende query Hallo retourneert alle Hallo opgegeven namen van kinderen in Hallo familie-id die overeenkomt met `WakefieldFamily` Hallo plaats waar je woont geordend.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="ab5c6-140">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="ab5c6-141">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="ab5c6-142">Willen we graag toodraw aandacht tooa enkele opmerkelijk aspecten van Hallo Cosmos DB querytaal via Hallo voorbeelden die we tot nu toe hebt gezien:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="ab5c6-143">Aangezien DocumentDB API SQL op JSON-waarden werkt, behandelt structuur in de vorm van entiteiten in plaats van rijen en kolommen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="ab5c6-144">Daarom Hallo taal kunt u toonodes van Hallo structuur op elke willekeurige diepte zoals verwijzen `Node1.Node2.Node3…..Nodem`, vergelijkbare toorelational SQL verwijzende toohello Twee onderdeelverwijzing van `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="ab5c6-145">Hallo structured query language werkt met schema minder gegevens.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="ab5c6-146">Daarom dynamisch Hallo type system behoeften toobe gebonden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="ab5c6-147">Hallo kan dezelfde expressie resulteert in verschillende typen op verschillende documenten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="ab5c6-148">Hallo-resultaat van een query is een geldige JSON-waarde, maar toobe van een vast schema kan niet worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="ab5c6-149">Cosmos DB ondersteunt alleen strikte JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="ab5c6-150">Dit betekent dat Hallo typesysteem en expressies zijn beperkt toodeal alleen met JSON-typen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="ab5c6-151">Raadpleeg toohello [JSON-specificatie](http://www.json.org/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="ab5c6-152">Een Cosmos-DB-verzameling is een container zonder schema van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="ab5c6-153">Hallo-relaties in gegevensentiteiten binnen en tussen documenten in een verzameling worden impliciet door containment en niet door de primaire sleutel en refererende sleutels relaties vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="ab5c6-154">Dit is een belangrijk aspect waard wijzen op in het licht Hallo intra-document joins verderop in dit artikel wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="ab5c6-155"><a id="Indexing"></a>Cosmos DB indexeren</span><span class="sxs-lookup"><span data-stu-id="ab5c6-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="ab5c6-156">Voordat we Hallo DocumentDB API SQL-syntaxis krijgen, is het waard Hallo ontwerp in Cosmos DB te indexeren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="ab5c6-157">Hallo-doel van de indexen van de database is tooserve query's in hun diverse vormen en vormen met minimale brongebruik (zoals CPU en input/output) terwijl er goed doorvoer en lage latentie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="ab5c6-158">Vaak vereist Hallo keuze van de juiste index Hallo voor query's in een database veel planning en experimenteren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="ab5c6-159">Deze aanpak vormt een uitdaging voor schema-minder databases waar de Hallo gegevens voldoen niet tooa strikte schema en snel ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="ab5c6-160">Wanneer we Hallo Cosmos DB indexering subsysteem ontworpen, instellen wij daarom Hallo doelstellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="ab5c6-161">Documenten te indexeren zonder schema: Hallo indexeren subsysteem geen vereist een schema-informatie of veronderstellingen over schema van Hallo documenten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="ab5c6-162">Ondersteuning voor efficiënte, geavanceerde hiërarchische en relationele query's: Hallo index ondersteunt Hallo Cosmos-DB-querytaal efficiënt, inclusief ondersteuning voor hiërarchische en relationele projecties.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="ab5c6-163">Ondersteuning voor consistente query's in face of een volgehouden volume van schrijfbewerkingen: voor schrijven met hoge doorvoer werkbelastingen met consistente query's, Hallo index incrementeel efficiënt en online in Hallo face van een duurzame volume van schrijfbewerkingen wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="ab5c6-164">Hallo consistent index-update is cruciaal tooserve Hallo query's op Hallo consistentieniveau in welke service Hallo gebruiker geconfigureerd Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="ab5c6-165">Ondersteuning voor multitenancy: gegeven Hallo reservering gebaseerde model voor de resource governance tussen tenants, index-updates worden uitgevoerd binnen het budget Hallo van systeemresources (CPU, geheugen en input/output-bewerkingen per seconde) die per replica worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="ab5c6-166">Opslagruimte: voor de kosteneffectiviteit, Hallo op schijf opslag overhead van Hallo index is gebonden en voorspelbaar.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="ab5c6-167">Dit is cruciaal omdat Cosmos DB Hallo developer toomake op basis van kosten wisselwerking tussen de overhead van de index in de relatie toohello queryprestaties kunt.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="ab5c6-168">Raadpleeg toohello [Azure Cosmos DB voorbeelden](https://github.com/Azure/azure-documentdb-net) op MSDN voor voorbeelden die laat zien hoe tooconfigure Hallo indexeringsbeleid voor een verzameling.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="ab5c6-169">Laten we nu krijgen Hallo details van hello Azure Cosmos DB SQL-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="ab5c6-170"><a id="Basics"></a>Basisprincipes van een Azure Cosmos DB SQL-query</span><span class="sxs-lookup"><span data-stu-id="ab5c6-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="ab5c6-171">Elke query bestaat uit een SELECT-component en een optionele FROM en WHERE-componenten per ANSI SQL-standaarden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="ab5c6-172">Normaal gesproken voor elke query moet Hallo-bron in de component FROM Hallo is geïnventariseerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="ab5c6-173">Hallo filter vervolgens in de WHERE-component wordt toegepast op Hallo bron tooretrieve Hallo een subset van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="ab5c6-174">Ten slotte Hallo SELECT-component wordt gebruikt tooproject Hallo aangevraagd JSON-waarden in Hallo lijst selecteren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="ab5c6-175"><a id="FromClause"></a>FROM-component</span><span class="sxs-lookup"><span data-stu-id="ab5c6-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="ab5c6-176">Hallo `FROM <from_specification>` component is optioneel tenzij Hallo-bron is gefilterd of later in de query Hallo geprojecteerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="ab5c6-177">Hallo-doel van deze component is toospecify Hallo-gegevensbron bij welke Hallo query moet functioneren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="ab5c6-178">Meestal de volledige verzameling Hallo Hallo-bron is, maar een kunt in plaats daarvan een subset van Hallo verzameling opgeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="ab5c6-179">Een query, zoals `SELECT * FROM Families` geeft aan dat het volledige verzameling worden Families Hallo Hallo bron via welke tooenumerate.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="ab5c6-180">Een speciale ROOT-id kan gebruikte toorepresent Hallo verzameling in plaats van met de naam van de verzameling Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="ab5c6-181">Hallo bevat volgende lijst Hallo-regels die per query worden afgedwongen:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="ab5c6-182">Hallo-verzameling kan worden alias hebben, zoals `SELECT f.id FROM Families AS f` of gewoon `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="ab5c6-183">Hier `f` is Hallo equivalent van `Families`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="ab5c6-184">`AS`is een optioneel trefwoord tooalias Hallo-id.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="ab5c6-185">Eenmaal alias Hallo oorspronkelijke bron kan niet worden gebonden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="ab5c6-186">Bijvoorbeeld: `SELECT Families.id FROM Families f` syntaxis is ongeldig omdat het Hallo-id 'Families' kan niet meer worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="ab5c6-187">Alle eigenschappen die toobe waarnaar wordt verwezen moeten moet volledig gekwalificeerd zijn.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="ab5c6-188">In de Hallo afwezigheid van de toepassing van de strikte schema, is dit afgedwongen tooavoid geen niet-eenduidige bindingen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="ab5c6-189">Daarom `SELECT id FROM Families f` syntaxis is ongeldig omdat de eigenschap Hallo `id` niet is gebonden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="ab5c6-190">Subdocumenten</span><span class="sxs-lookup"><span data-stu-id="ab5c6-190">Subdocuments</span></span>
<span data-ttu-id="ab5c6-191">Hallo-bron kan ook worden verlaagd tooa kleinere subset.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="ab5c6-192">Bijvoorbeeld tooenumerating alleen een substructuur in elk document, Hallo subroot kan vervolgens worden Hallo bron, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="ab5c6-193">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="ab5c6-194">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-194">**Results**</span></span>  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="ab5c6-195">Hallo hierboven voorbeeld gebruikt een matrix als Hallo bron, een object kan ook worden gebruikt als bron hello, dit is wat wordt weergegeven in het volgende voorbeeld Hallo: een geldige JSON-waarde (geen niet-gedefinieerd) die kan worden gevonden in bron hello wordt beschouwd als voor insluiting in Hallo resultaat van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="ab5c6-196">Als sommige families beschikt niet over een `address.state` waarde, in het queryresultaat Hallo worden uitgesloten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="ab5c6-197">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="ab5c6-198">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="ab5c6-199"><a id="WhereClause"></a>WHERE-component</span><span class="sxs-lookup"><span data-stu-id="ab5c6-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="ab5c6-200">WHERE-component Hallo (**`WHERE <filter_condition>`**) is optioneel.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="ab5c6-201">Deze geeft Hallo voorwaarde(n) dat Hallo JSON-documenten geleverd door het Hallo-bron moeten voldoen aan volgorde toobe opgenomen als onderdeel van Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="ab5c6-202">Elk JSON-document moet worden geëvalueerd Hallo opgegeven voorwaarden te 'true' toobe in aanmerking voor Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="ab5c6-203">Hallo waar component wordt gebruikt door Hallo index laag in volgorde toodetermine Hallo absolute kleinste subset van brondocumenten die deel van Hallo resultaat uitmaken kunnen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="ab5c6-204">Hallo volgende query haalt u documenten met een eigenschap name waarvan de waarde `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="ab5c6-205">Elk document dat u beschikt niet over een eigenschap name of waar Hallo waarde komt niet overeen met `AndersenFamily` is uitgesloten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="ab5c6-206">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ab5c6-207">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="ab5c6-208">Hallo vorige voorbeeld blijkt een eenvoudige gelijkheid-query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="ab5c6-209">DocumentDB-API SQL ondersteunt ook een groot aantal scalaire expressies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="ab5c6-210">Hallo meest gebruikte binaire bestanden en unaire expressies zijn.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="ab5c6-211">Eigenschap verwijzingen uit Hallo bron JSON-object zijn ook geldig expressies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="ab5c6-212">binaire operators na Hallo worden momenteel ondersteund en kan worden gebruikt in query's, zoals wordt weergegeven in Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="ab5c6-213">Rekenkundige bewerking</span><span class="sxs-lookup"><span data-stu-id="ab5c6-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="ab5c6-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="ab5c6-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ab5c6-215">Bitsgewijs</span><span class="sxs-lookup"><span data-stu-id="ab5c6-215">Bitwise</span></span></td>    
<td><span data-ttu-id="ab5c6-216">|, &, ^, <<>>,, >>> (nul opvulling rechts verplaatsen)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ab5c6-217">Logische</span><span class="sxs-lookup"><span data-stu-id="ab5c6-217">Logical</span></span></td>
<td><span data-ttu-id="ab5c6-218">EN, OF NIET</span><span class="sxs-lookup"><span data-stu-id="ab5c6-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ab5c6-219">Vergelijking</span><span class="sxs-lookup"><span data-stu-id="ab5c6-219">Comparison</span></span></td>    
<td><span data-ttu-id="ab5c6-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="ab5c6-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ab5c6-221">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ab5c6-221">String</span></span></td>    
<td><span data-ttu-id="ab5c6-222">|| (samenvoegen)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="ab5c6-223">We gaan verdiepen in enkele query's met behulp van de binaire operators.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="ab5c6-224">unaire operators Hallo +,-, ~ worden ook ondersteund, en niet kan worden gebruikt in query's, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="ab5c6-225">Bovendien toobinary en unaire operators, eigenschap verwijzingen zijn ook toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="ab5c6-226">Bijvoorbeeld: `SELECT * FROM Families f WHERE f.isRegistered` retourneert Hallo JSON-document met de eigenschap Hallo `isRegistered` waarbij de waarde van eigenschap Hallo gelijk toohello JSON is `true` waarde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="ab5c6-227">Andere waarden (false, null, niet-gedefinieerde, `<number>`, `<string>`, `<object>`, `<array>`, enzovoort) toohello brondocument wordt uitgesloten van Hallo resultaat leidt.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="ab5c6-228">Gelijkheid en het vergelijkingstype operators</span><span class="sxs-lookup"><span data-stu-id="ab5c6-228">Equality and comparison operators</span></span>
<span data-ttu-id="ab5c6-229">Hallo volgende tabel toont Hallo resultaat van de gelijkheid vergelijkingen in DocumentDB API SQL tussen twee typen die JSON.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="ab5c6-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ab5c6-231">
            <strong>Niet-gedefinieerd</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ab5c6-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ab5c6-233">
            <strong>Booleaanse waarde</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ab5c6-234">
            <strong>Aantal</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ab5c6-235">
            <strong>Tekenreeks</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ab5c6-236">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ab5c6-237">
            <strong>Matrix</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ab5c6-238">
            <strong>Niet-gedefinieerd<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-239">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-240">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-241">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-242">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-243">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-244">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-245">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ab5c6-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-247">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ab5c6-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-249">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-250">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-251">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-252">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-253">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ab5c6-254">
            <strong>Booleaanse waarde<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-255">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-256">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ab5c6-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-258">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-259">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-260">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-261">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ab5c6-262">
            <strong>Aantal<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-263">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-264">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-265">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ab5c6-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-267">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-268">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-269">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ab5c6-270">
            <strong>Tekenreeks<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-271">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-272">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-273">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-274">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ab5c6-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-276">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-277">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ab5c6-278">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-279">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-280">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-281">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-282">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-283">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ab5c6-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-285">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ab5c6-286">
            <strong>Matrix<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ab5c6-287">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-288">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-289">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-290">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-291">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ab5c6-292">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ab5c6-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ab5c6-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="ab5c6-294">Voor andere vergelijkingsoperators zoals >, > =,! =, < en < =, hello volgende regels zijn van toepassing:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="ab5c6-295">Vergelijking van verschillende typen resulteert in Undefined.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="ab5c6-296">Vergelijking tussen de twee objecten of twee matrices resulteert in een Undefined.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="ab5c6-297">Als Hallo resultaat van de scalaire expressie Hallo in Hallo-filter is niet is gedefinieerd, Hallo bijbehorende document zou niet opgenomen in Hallo resultaat, aangezien Undefined logisch te 'true' niet vergelijken.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="ab5c6-298">TUSSEN sleutelwoord</span><span class="sxs-lookup"><span data-stu-id="ab5c6-298">BETWEEN keyword</span></span>
<span data-ttu-id="ab5c6-299">U kunt ook Hallo BETWEEN sleutelwoord tooexpress query's op bereiken met waarden zoals in de ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="ab5c6-300">TUSSEN kan worden gebruikt met tekenreeksen of getallen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="ab5c6-301">Deze query retourneert bijvoorbeeld alle familie documenten in welke Hallo is het eerste onderliggende hoogwaardige tussen 1-5 (zowel liggen).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="ab5c6-302">In tegenstelling tot in de ANSI-SQL, kunt u ook gebruiken Hallo BETWEEN component in hello FROM-component zoals in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="ab5c6-303">Voor snellere tijden in uitvoering, houd er rekening mee toocreate een indexeringsbeleid die gebruikmaakt van een type bereik index op basis van een numerieke eigenschappen/paden die zijn gefilterd in Hallo BETWEEN-component.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="ab5c6-304">Hallo belangrijkste verschil tussen het gebruik van BETWEEN in DocumentDB-API en ANSI SQL is dat u kunt snelle bereik een query uitgevoerd naar eigenschappen van gemengde gegevenstypen: bijvoorbeeld wellicht 'hoogwaardige' is geen getal (5) in een aantal documenten en tekenreeksen in andere gevallen ('grade4').</span><span class="sxs-lookup"><span data-stu-id="ab5c6-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="ab5c6-305">In dergelijke gevallen, wordt zoals in JavaScript, een vergelijking tussen de twee verschillende typen resulteert in een 'niet-gedefinieerde' en het Hallo-document overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="ab5c6-306">Logische (AND, OR en NOT) operators</span><span class="sxs-lookup"><span data-stu-id="ab5c6-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="ab5c6-307">Logische operators bewerken Boole-waarden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="ab5c6-308">Hallo logische waarheid tabellen voor deze operators worden weergegeven in Hallo tabellen te volgen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="ab5c6-309">OF</span><span class="sxs-lookup"><span data-stu-id="ab5c6-309">OR</span></span> | <span data-ttu-id="ab5c6-310">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-310">True</span></span> | <span data-ttu-id="ab5c6-311">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-311">False</span></span> | <span data-ttu-id="ab5c6-312">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ab5c6-313">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-313">True</span></span> |<span data-ttu-id="ab5c6-314">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-314">True</span></span> |<span data-ttu-id="ab5c6-315">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-315">True</span></span> |<span data-ttu-id="ab5c6-316">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-316">True</span></span> |
| <span data-ttu-id="ab5c6-317">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-317">False</span></span> |<span data-ttu-id="ab5c6-318">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-318">True</span></span> |<span data-ttu-id="ab5c6-319">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-319">False</span></span> |<span data-ttu-id="ab5c6-320">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-320">Undefined</span></span> |
| <span data-ttu-id="ab5c6-321">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-321">Undefined</span></span> |<span data-ttu-id="ab5c6-322">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-322">True</span></span> |<span data-ttu-id="ab5c6-323">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-323">Undefined</span></span> |<span data-ttu-id="ab5c6-324">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-324">Undefined</span></span> |

| <span data-ttu-id="ab5c6-325">EN</span><span class="sxs-lookup"><span data-stu-id="ab5c6-325">AND</span></span> | <span data-ttu-id="ab5c6-326">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-326">True</span></span> | <span data-ttu-id="ab5c6-327">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-327">False</span></span> | <span data-ttu-id="ab5c6-328">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ab5c6-329">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-329">True</span></span> |<span data-ttu-id="ab5c6-330">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-330">True</span></span> |<span data-ttu-id="ab5c6-331">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-331">False</span></span> |<span data-ttu-id="ab5c6-332">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-332">Undefined</span></span> |
| <span data-ttu-id="ab5c6-333">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-333">False</span></span> |<span data-ttu-id="ab5c6-334">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-334">False</span></span> |<span data-ttu-id="ab5c6-335">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-335">False</span></span> |<span data-ttu-id="ab5c6-336">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-336">False</span></span> |
| <span data-ttu-id="ab5c6-337">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-337">Undefined</span></span> |<span data-ttu-id="ab5c6-338">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-338">Undefined</span></span> |<span data-ttu-id="ab5c6-339">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-339">False</span></span> |<span data-ttu-id="ab5c6-340">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-340">Undefined</span></span> |

| <span data-ttu-id="ab5c6-341">NIET</span><span class="sxs-lookup"><span data-stu-id="ab5c6-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="ab5c6-342">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-342">True</span></span> |<span data-ttu-id="ab5c6-343">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-343">False</span></span> |
| <span data-ttu-id="ab5c6-344">False</span><span class="sxs-lookup"><span data-stu-id="ab5c6-344">False</span></span> |<span data-ttu-id="ab5c6-345">True</span><span class="sxs-lookup"><span data-stu-id="ab5c6-345">True</span></span> |
| <span data-ttu-id="ab5c6-346">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-346">Undefined</span></span> |<span data-ttu-id="ab5c6-347">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="ab5c6-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="ab5c6-348">TREFWOORD</span><span class="sxs-lookup"><span data-stu-id="ab5c6-348">IN keyword</span></span>
<span data-ttu-id="ab5c6-349">Hallo sleutelwoord kan gebruikte toocheck zijn of een opgegeven waarde komt overeen met elke waarde in een lijst.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="ab5c6-350">Bijvoorbeeld, retourneert deze query alle familie documenten waar Hallo-id van 'WakefieldFamily' of 'AndersenFamily'.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="ab5c6-351">In dit voorbeeld retourneert alle documenten waar Hallo status is Hallo opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="ab5c6-352">Ternair (?) en operators Coalesce (?)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="ab5c6-353">Hallo Ternair en Coalesce operators kunnen worden gebruikt toobuild voorwaardelijke expressies, vergelijkbare toopopular programmeertalen zoals C# en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="ab5c6-354">Hallo Ternair (?) operator is erg handig als maken nieuwe JSON-eigenschappen op Hallo vliegen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="ab5c6-355">Bijvoorbeeld, kunt nu u query's tooclassify Hallo klasse niveaus in een menselijke leesbare vorm zoals beginnende/tussenliggende/Geavanceerd zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="ab5c6-356">U kunt ook Hallo aanroepen toohello operator zoals in de onderstaande Hallo query nesten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="ab5c6-357">Als met andere operators query zijn als hello waarnaar wordt verwezen eigenschappen in Hallo voorwaardelijke expressies ontbreken in elk document of als het Hallo-typen worden vergeleken zijn verschillend zijn, klikt u vervolgens die documenten uitgesloten in Hallo queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="ab5c6-358">Hallo Coalesce (?) operator kan worden tooefficiently selectievakje (ook gebruikt voor de aanwezigheid van een eigenschap Hallo</span><span class="sxs-lookup"><span data-stu-id="ab5c6-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="ab5c6-359">is gedefinieerd) in een document.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-359">is defined) in a document.</span></span> <span data-ttu-id="ab5c6-360">Dit is handig wanneer een query op semi-gestructureerde of gegevens van gemengde typen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="ab5c6-361">Bijvoorbeeld, retourneert deze query Hallo 'lastName' indien aanwezig, of Hallo 'Achternaam' als dit niet aanwezig.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="ab5c6-362"><a id="EscapingReservedKeywords"></a>Tussen aanhalingstekens eigenschapsaccessor</span><span class="sxs-lookup"><span data-stu-id="ab5c6-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="ab5c6-363">U kunt ook toegang tot eigenschappen met Hallo tussen aanhalingstekens eigenschap operator `[]`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="ab5c6-364">Bijvoorbeeld: `SELECT c.grade` en `SELECT c["grade"]` equivalent zijn.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="ab5c6-365">Deze syntaxis is nuttig wanneer u een eigenschap die spaties, speciale tekens bevat of gebeurt tooshare Hallo dezelfde naam als een SQL-sleutelwoord of een gereserveerd woord tooescape nodig.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="ab5c6-366"><a id="SelectClause"></a>SELECT-component</span><span class="sxs-lookup"><span data-stu-id="ab5c6-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="ab5c6-367">Hallo SELECT-component (**`SELECT <select_list>`**) is verplicht en Hiermee geeft u de waarden die worden opgehaald uit Hallo query, net zoals in de ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="ab5c6-368">Hallo subset die boven op Hallo brondocumenten zijn gefilterd worden doorgegeven naar Hallo Projectiefase, waarbij Hallo opgegeven JSON-waarden worden opgehaald en een nieuwe JSON-object voor elke doorgegeven op deze invoer is samengesteld.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="ab5c6-369">Hallo volgende voorbeeld toont een typische SELECT-query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="ab5c6-370">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ab5c6-371">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="ab5c6-372">Geneste eigenschappen</span><span class="sxs-lookup"><span data-stu-id="ab5c6-372">Nested properties</span></span>
<span data-ttu-id="ab5c6-373">In de Hallo voorbeeld te volgen, we twee geneste eigenschappen projecteert `f.address.state` en `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="ab5c6-374">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ab5c6-375">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="ab5c6-376">Projectie biedt ook ondersteuning voor JSON-expressies, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="ab5c6-377">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ab5c6-378">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="ab5c6-379">Bekijk Hallo-rol van `$1` hier.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="ab5c6-380">Hallo `SELECT` component moet een JSON-object toocreate en omdat er geen sleutel is opgegeven, gebruiken we de impliciete argument variabele namen die beginnen met `$1`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="ab5c6-381">Deze query retourneert bijvoorbeeld twee impliciete argumentvariabelen, met het label `$1` en `$2`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="ab5c6-382">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ab5c6-383">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="ab5c6-384">Aliasing</span><span class="sxs-lookup"><span data-stu-id="ab5c6-384">Aliasing</span></span>
<span data-ttu-id="ab5c6-385">Nu gaan we uitbreiden Hallo voorbeeld hierboven expliciete aliasing van waarden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="ab5c6-386">Hallo-sleutelwoord gebruikt voor aliasing is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="ab5c6-387">Dit is optioneel, zoals wordt weergegeven tijdens het projecteren Hallo tweede waarde als `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="ab5c6-388">Als een query over twee eigenschappen met Hallo dezelfde naam aliasing moet gebruikte toorename een of beide eigenschappen Hallo zodat ze ondubbelzinnig zijn gemaakt in Hallo geprojecteerd resultaat.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="ab5c6-389">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ab5c6-390">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="ab5c6-391">Scalaire expressies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-391">Scalar expressions</span></span>
<span data-ttu-id="ab5c6-392">Bovendien tooproperty verwijst naar, Hallo SELECT-component biedt ook ondersteuning voor scalaire expressies zoals constanten, aritmetische expressies, logische expressies, enzovoort. Hier is bijvoorbeeld een eenvoudige 'Hallo wereld'-query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="ab5c6-393">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="ab5c6-394">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="ab5c6-395">Hier volgt een voorbeeld van een complexere die gebruikmaakt van een scalaire expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="ab5c6-396">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="ab5c6-397">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="ab5c6-398">In Hallo voorbeeld te volgen, is Hallo resultaat van de scalaire expressie Hallo het een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="ab5c6-399">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="ab5c6-400">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="ab5c6-401">Maken van het object en array</span><span class="sxs-lookup"><span data-stu-id="ab5c6-401">Object and array creation</span></span>
<span data-ttu-id="ab5c6-402">Een andere belangrijke functie van DocumentDB API SQL is array-object maken.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="ab5c6-403">In het vorige voorbeeld hello, houd er rekening mee dat er een nieuwe JSON-object gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="ab5c6-404">Op deze manier kunt een ook matrices maken zoals in Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="ab5c6-405">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="ab5c6-406">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-406">**Results**</span></span>  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <span data-ttu-id="ab5c6-407"><a id="ValueKeyword"></a>WAARDE sleutelwoord</span><span class="sxs-lookup"><span data-stu-id="ab5c6-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="ab5c6-408">Hallo **waarde** sleutelwoord biedt een manier tooreturn JSON-waarde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="ab5c6-409">Bijvoorbeeld Hallo query retourneert Hallo scalaire hieronder `"Hello World"` in plaats van `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="ab5c6-410">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="ab5c6-411">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="ab5c6-412">Hallo volgende query retourneert Hallo JSON-waarde zonder Hallo `"address"` label in Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="ab5c6-413">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="ab5c6-414">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-414">**Results**</span></span>  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

<span data-ttu-id="ab5c6-415">Hallo volgende voorbeeld breidt deze tooshow hoe tooreturn JSON primitieve waarden (knooppuntniveau van JSON-structuur Hallo Hallo).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="ab5c6-416">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="ab5c6-417">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="ab5c6-418">* Operator</span><span class="sxs-lookup"><span data-stu-id="ab5c6-418">* Operator</span></span>
<span data-ttu-id="ab5c6-419">Hallo speciale operator (*) is ondersteunde tooproject Hallo-document als-is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="ab5c6-420">Wanneer gebruikt, moet dit Hallo geprojecteerd alleen veld.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="ab5c6-421">Terwijl een query zoals `SELECT * FROM Families f` geldig is, `SELECT VALUE * FROM Families f ` en `SELECT *, f.id FROM Families f ` zijn niet geldig.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="ab5c6-422">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ab5c6-423">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-423">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <span data-ttu-id="ab5c6-424"><a id="TopKeyword"></a>Operator TOP</span><span class="sxs-lookup"><span data-stu-id="ab5c6-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="ab5c6-425">Hallo bovenste sleutelwoord kan worden gebruikt toolimit Hallo aantal waarden dat door een query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="ab5c6-426">Als eerste wordt gebruikt in combinatie met Hallo ORDER BY-component, is Hallo resultatenset beperkt toohello eerste N aantal geordende waarden; Anders retourneert het Hallo eerste N aantal resultaten in een niet-gedefinieerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="ab5c6-427">Als een best practice in een instructie SELECT gebruik altijd een component ORDER BY met Hallo TOP-component.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="ab5c6-428">Dit is de enige manier Hallo toopredictably aangeven welke rijen zijn beïnvloed door boven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="ab5c6-429">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="ab5c6-430">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-430">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

<span data-ttu-id="ab5c6-431">TOP kan worden gebruikt met een constante waarde (zoals hierboven) of met de waarde van een variabele query's met parameters.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="ab5c6-432">Zie geparameteriseerde query's hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="ab5c6-433"><a id="Aggregates"></a>Statistische functies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="ab5c6-434">U kunt ook aggregaties uitvoeren in Hallo `SELECT` component.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="ab5c6-435">Statistische functies uitvoeren van een berekening op een set waarden en één waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="ab5c6-436">Bijvoorbeeld: hello volgende query retourneert Hallo telling van familie documenten binnen Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="ab5c6-437">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="ab5c6-438">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="ab5c6-439">U kunt de scalaire waarde Hallo Hallo cumulatieve ook met behulp van Hallo retourneren `VALUE` sleutelwoord.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="ab5c6-440">Bijvoorbeeld retourneert hello volgende query het aantal waarden Hallo als een enkel getal:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="ab5c6-441">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="ab5c6-442">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="ab5c6-443">U kunt ook statistische functies uitvoeren in combinatie met filters.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="ab5c6-444">Bijvoorbeeld retourneert hello volgende query het aantal documenten met Hallo adres Hallo in Hallo staat Washington.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="ab5c6-445">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="ab5c6-446">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="ab5c6-447">Hallo volgende tabel toont Hallo lijst met ondersteunde statistische functies in DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="ab5c6-448">`SUM`en `AVG` via numerieke waarden worden uitgevoerd terwijl `COUNT`, `MIN`, en `MAX` via getallen, tekenreeksen, Booleaanse waarden en null-waarden kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="ab5c6-449">Gebruik</span><span class="sxs-lookup"><span data-stu-id="ab5c6-449">Usage</span></span> | <span data-ttu-id="ab5c6-450">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ab5c6-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="ab5c6-451">AANTAL</span><span class="sxs-lookup"><span data-stu-id="ab5c6-451">COUNT</span></span> | <span data-ttu-id="ab5c6-452">Retourneert Hallo het aantal items in de expressie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="ab5c6-453">SOM</span><span class="sxs-lookup"><span data-stu-id="ab5c6-453">SUM</span></span>   | <span data-ttu-id="ab5c6-454">Retourneert Hallo som van alle Hallo-waarden in Hallo-expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="ab5c6-455">MIN</span><span class="sxs-lookup"><span data-stu-id="ab5c6-455">MIN</span></span>   | <span data-ttu-id="ab5c6-456">Retourneert Hallo minimumwaarde in het Hallo-expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="ab5c6-457">MAXIMUM AANTAL</span><span class="sxs-lookup"><span data-stu-id="ab5c6-457">MAX</span></span>   | <span data-ttu-id="ab5c6-458">Retourneert Hallo maximumwaarde in het Hallo-expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="ab5c6-459">GEM.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-459">AVG</span></span>   | <span data-ttu-id="ab5c6-460">Retourneert Hallo gemiddelde van waarden in de expressie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="ab5c6-461">Statistische functies kunnen ook worden uitgevoerd via Hallo resultaten van een matrix herhaling.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="ab5c6-462">Zie voor meer informatie [herhaling van de matrix in query's](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="ab5c6-463">Wanneer met behulp van Azure portal Queryverkenner hello, houd er rekening mee dat aggregatie van query's kunnen worden geretourneerd Hallo gedeeltelijk cumulatieve resultaten gedurende een querypagina.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="ab5c6-464">Hallo SDK's produceert één cumulatieve waarde op alle pagina's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="ab5c6-465">In volgorde tooperform aggregatie van query's met code, moet u .NET SDK 1.12.0, .NET Core SDK 1.1.0 of Java SDK 1.9.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="ab5c6-466"><a id="OrderByClause"></a>ORDER BY-component</span><span class="sxs-lookup"><span data-stu-id="ab5c6-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="ab5c6-467">Zoals in de ANSI-SQL, u een optionele component Order By tijdens het opvragen opnemen kunt.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="ab5c6-468">Hallo-component kan bestaan uit een optionele ASC/DESC argument toospecify Hallo volgorde waarin de resultaten moeten worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="ab5c6-469">Hier is bijvoorbeeld een query waarmee families in volgorde van de naam van Hallo residente stad opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="ab5c6-470">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="ab5c6-471">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-471">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

<span data-ttu-id="ab5c6-472">En hier is een query waarmee families in volgorde van de aanmaakdatum, dat is opgeslagen, zoals een Hallo epoche tijd, Internet Explorer, verstreken tijd sinds 1 januari 1970 in seconden worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="ab5c6-473">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="ab5c6-474">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-474">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <span data-ttu-id="ab5c6-475"><a id="Advanced"></a>Concepten van geavanceerde database en SQL-query 's</span><span class="sxs-lookup"><span data-stu-id="ab5c6-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="ab5c6-476"><a id="Iteration"></a>Herhaling</span><span class="sxs-lookup"><span data-stu-id="ab5c6-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="ab5c6-477">Een nieuwe constructie is toegevoegd via Hallo **IN** -sleutelwoord in DocumentDB API SQL tooprovide ondersteuning voor iteratie van JSON-matrices.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="ab5c6-478">Hallo FROM bron biedt ondersteuning voor herhaling.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="ab5c6-479">U begint met het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-479">Let's start with hello following example:</span></span>

<span data-ttu-id="ab5c6-480">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="ab5c6-481">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-481">**Results**</span></span>  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="ab5c6-482">Nu we bekijken een andere query die herhaling via onderliggende elementen in de verzameling Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="ab5c6-483">Houd er rekening mee Hallo verschil in Hallo uitvoermatrix.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="ab5c6-484">In dit voorbeeld wordt gesplitst `children` en worden samengevoegd Hallo resultaten in een matrix.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="ab5c6-485">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="ab5c6-486">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-486">**Results**</span></span>  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

<span data-ttu-id="ab5c6-487">Dit kan verder gebruikte toofilter op elke afzonderlijke vermelding van de matrix Hallo zoals weergegeven in het volgende voorbeeld Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="ab5c6-488">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="ab5c6-489">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="ab5c6-490">U kunt ook aggregatie uitvoeren via Hallo resultaat van de matrix herhaling.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="ab5c6-491">Bijvoorbeeld: hello volgende query telt Hallo aantal onderliggende items onder alle families.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="ab5c6-492">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="ab5c6-493">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="ab5c6-494"><a id="Joins"></a>Joins</span><span class="sxs-lookup"><span data-stu-id="ab5c6-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="ab5c6-495">In een relationele database Hallo nodig toojoin tussen tabellen, het is belangrijk.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="ab5c6-496">De Hallo logische corollary toodesigning genormaliseerd schema's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="ab5c6-497">Strijdig toothis, DocumentDB API omgaat met de Hallo gedenormaliseerd gegevensmodel zonder schema documenten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="ab5c6-498">Dit is Hallo logische equivalent van een 'self-join'.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="ab5c6-499">Hallo-syntaxis die ondersteuning biedt voor Hallo taal is < from_source1 > JOIN < from_source2 > JOIN... JOIN < from_sourceN >.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="ab5c6-500">Over het algemeen dit retourneert een reeks **N**- tuples (tuple met **N** waarden).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="ab5c6-501">Elke tuple heeft geproduceerd door alle verzameling aliassen iteratie van hun respectieve sets waarden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="ab5c6-502">Dit is met andere woorden, een volledige vectorproduct van Hallo sets die deel uitmaken van Hallo join.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="ab5c6-503">Hallo volgende voorbeelden ziet u de werking van Hallo JOIN-component.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="ab5c6-504">Hallo-resultaat is in Hallo voorbeeld te volgen, leeg omdat hello vectorproduct van elk document van de bron- en een lege set leeg is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="ab5c6-505">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="ab5c6-506">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="ab5c6-507">In Hallo voorbeeld te volgen, is het Hallo-join tussen Hallo webroot en Hallo `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="ab5c6-508">Het is een vectorproduct tussen twee JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="ab5c6-509">Hallo fact dat onderliggende elementen is een matrix is niet effectief in Hallo JOIN Aangezien we werkt met een één hoofdelement die Hallo onderliggende matrix.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="ab5c6-510">Hallo resultaat bevat daarom slechts twee resultaten omdat hello vectorproduct van elk document met Hallo matrix exact slechts één document levert.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="ab5c6-511">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="ab5c6-512">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="ab5c6-513">Hallo volgende voorbeeld ziet u een meer conventionele join:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="ab5c6-514">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="ab5c6-515">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-515">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



<span data-ttu-id="ab5c6-516">Hallo eerst te beginnen toonote is die Hallo `from_source` Hallo **JOIN** component is een iterator.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="ab5c6-517">Dus Hallo stroom is in dit geval als volgt:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="ab5c6-518">Vouw van elk onderliggend element **c** in Hallo matrix.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="ab5c6-519">Toepassen van een vectorproduct met Hallo hoofdmap van document Hallo **f** met elk onderliggend element **c** dat is samengevoegd in de eerste stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="ab5c6-520">Ten slotte project Hallo hoofdobject **f** naameigenschap alleen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="ab5c6-521">eerste Hallo-document (`AndersenFamily`) bevat slechts één onderliggend element zodat Hallo resultatenset alleen een bijbehorende enkel object toothis document bevat.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="ab5c6-522">tweede Hallo-document (`WakefieldFamily`) twee onderliggende items bevat.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="ab5c6-523">Dus produceert hello vectorproduct een afzonderlijk object voor elke onderliggende, waardoor wat resulteert in twee objecten, één voor elke onderliggende bijbehorende toothis document.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="ab5c6-524">Hallo-hoofdmap velden in beide deze documenten zijn Hallo dezelfde zijn, net zoals u in een vectorproduct verwacht.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="ab5c6-525">Hallo echt hulpprogramma Hallo JOIN tooform tuples uit Hallo-vectorproduct in een shape die anders is moeilijk tooproject.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="ab5c6-526">Bovendien zoals we in de onderstaande Hallo-voorbeeld zien, kon u filteren op Hallo combinatie van een tuple waarmee Hallo gebruiker heeft ervoor gekozen een voorwaarde voldaan door Hallo tuples algemene.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="ab5c6-527">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="ab5c6-528">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-528">**Results**</span></span>

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



<span data-ttu-id="ab5c6-529">In dit voorbeeld is een natuurlijke extensie van het voorgaande voorbeeld Hallo en voert een dubbele koppeling.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="ab5c6-530">Dus kan hello vectorproduct worden weergegeven als Hallo pseudo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

<span data-ttu-id="ab5c6-531">`AndersenFamily`heeft één onderliggende die één huisdier heeft.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="ab5c6-532">Dus hello vectorproduct resulteert in een rij is (1\*1\*1) van deze reeks.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="ab5c6-533">WakefieldFamily echter twee onderliggende items heeft, maar slechts één onderliggende 'Jesse' huisdieren heeft.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="ab5c6-534">Jesse heeft echter twee huisdieren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-534">Jesse has two pets though.</span></span> <span data-ttu-id="ab5c6-535">Daarom hello vectorproduct levert 1\*1\*2 = 2 rijen uit deze reeks.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="ab5c6-536">In het volgende voorbeeld hello, er is een extra filter op `pet`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="ab5c6-537">Dit omvat niet alle Hallo tuples indien Hallo bijnaam niet 'Schaduwkopie' is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="ab5c6-538">U ziet dat we kunnen toobuild tuples uit matrices, filter op Hallo-elementen van het Hallo-tuple zijn en een combinatie van elementen Hallo project.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="ab5c6-539">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="ab5c6-540">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="ab5c6-541"><a id="JavaScriptIntegration"></a>Integratie van JavaScript</span><span class="sxs-lookup"><span data-stu-id="ab5c6-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="ab5c6-542">Azure Cosmos DB biedt een programmeermodel voor het uitvoeren op basis van JavaScript-toepassingslogica rechtstreeks op Hallo van verzamelingen in termen van opgeslagen procedures en triggers.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="ab5c6-543">Hiermee kunt u beide:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-543">This allows for both:</span></span>

* <span data-ttu-id="ab5c6-544">Mogelijkheid toodo high-performance transactionele CRUD-bewerkingen en een query uitgevoerd naar documenten in een verzameling grond Hallo diepe integratie van JavaScript-runtime rechtstreeks in de database-engine Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="ab5c6-545">Een natuurlijke modellering van Controlestroom, variabele scopes en -toewijzing en integratie van primitieven met databasetransacties afhandeling van uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="ab5c6-546">Raadpleeg toohello JavaScript-serverzijde programmeerbaarheid documentatie voor meer informatie over Azure DB die Cosmos-ondersteuning voor integratie van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="ab5c6-547"><a id="UserDefinedFunctions"></a>Gebruiker gedefinieerde functies (UDF's)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="ab5c6-548">Samen met de Hallo-typen is al gedefinieerd in dit artikel, biedt DocumentDB API SQL ondersteuning voor gebruiker gedefinieerde functies (UDF).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="ab5c6-549">In het bijzonder wordt scalaire UDF's waar Hallo ontwikkelaars kunnen doorgeven in nul of meerdere argumenten en terug één argument resultaat geretourneerd ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="ab5c6-550">Elk van deze argumenten wordt voor geldige JSON-waarden worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="ab5c6-551">Hallo DocumentDB API SQL-syntaxis wordt uitgebreid aangepaste toepassingslogica toosupport gebruik van deze door de gebruiker gedefinieerde functies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="ab5c6-552">UDF's kunnen worden geregistreerd met DocumentDB-API en vervolgens naar worden verwezen als onderdeel van een SQL-query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="ab5c6-553">Hallo UDF's exquisitely zijn ontworpen in feite toobe aangeroepen door query's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="ab5c6-554">Als een keuze corollary toothis UDF's hebben geen toegang toohello context-object dat andere JavaScript Hallo typen (opgeslagen procedures en triggers) hebben.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="ab5c6-555">Omdat de query's worden uitgevoerd als alleen-lezen, kunnen ze worden uitgevoerd op de primaire of op secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="ab5c6-556">Daarom zijn UDF's ontworpen toorun op secundaire replica's in tegenstelling tot andere typen JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="ab5c6-557">Hieronder volgt een voorbeeld van hoe een UDF op Hallo Cosmos DB database onder een documentverzameling specifiek kan worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

<span data-ttu-id="ab5c6-558">Hallo voorgaande voorbeeld maakt u een UDF met de naam `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="ab5c6-559">Deze twee waarden voor JSON-tekenreeks accepteert `input` en `pattern` en controleert of Hallo eerste komt overeen met patroon Hallo opgegeven in het tweede Hallo van JavaScript string.match() functie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="ab5c6-560">We kunnen deze UDF nu gebruiken in een query in een projectie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="ab5c6-561">UDF's moeten worden gekwalificeerd met Hallo hoofdlettergevoelig voorvoegsel "udf."</span><span class="sxs-lookup"><span data-stu-id="ab5c6-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="ab5c6-562">Wanneer aangeroepen vanuit query's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="ab5c6-563">Eerdere too3-17-2015, Cosmos DB ondersteund UDF aanroepen zonder Hallo 'udf."</span><span class="sxs-lookup"><span data-stu-id="ab5c6-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="ab5c6-564">voorvoegsel zoals REGEX_MATCH() selecteren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="ab5c6-565">Dit patroon van aanroepen is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="ab5c6-566">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="ab5c6-567">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="ab5c6-568">Hallo UDF kan ook worden gebruikt in een filter, zoals weergegeven in Hallo voorbeeld hieronder, ook worden gekwalificeerd met Hallo 'udf."</span><span class="sxs-lookup"><span data-stu-id="ab5c6-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="ab5c6-569">voorvoegsel:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-569">prefix:</span></span>

<span data-ttu-id="ab5c6-570">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="ab5c6-571">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="ab5c6-572">In principe UDF's geldig scalaire expressies zijn en kunnen worden gebruikt in projecties en filters.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="ab5c6-573">tooexpand op Hallo kracht van UDF's, we kijken naar een ander voorbeeld met voorwaardelijke logica:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


<span data-ttu-id="ab5c6-574">Hieronder volgt een voorbeeld dat oefeningen Hallo UDF.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="ab5c6-575">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="ab5c6-576">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-576">**Results**</span></span>

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


<span data-ttu-id="ab5c6-577">Als de voorgaande voorbeelden toepassingen hello, integreren UDF's in Hallo power van JavaScript-taal Hallo DocumentDB API SQL tooprovide een uitgebreide programmeerbare interface toodo complexe procedurele, heeft voorwaardelijke logica met Hallo hulp van de ingebouwde JavaScript-runtime mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="ab5c6-578">DocumentDB API SQL biedt Hallo argumenten toohello UDF's voor elk document in Hallo-bron in Hallo huidige fase (WHERE-component of SELECT-component) verwerking Hallo UDF.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="ab5c6-579">Hallo resultaat opgenomen in algemene pijplijn naadloos Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="ab5c6-580">Als Hallo eigenschappen waarnaar wordt verwezen tooby Hallo UDF-parameters niet beschikbaar in JSON-waarde Hallo hello parameter wordt beschouwd zijn als niet-gedefinieerde en daarom Hallo UDF-aanroep volledig overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="ab5c6-581">Op dezelfde manier als resultaat Hallo Hallo UDF gedefinieerd is, het niet opgenomen in Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="ab5c6-582">Kortom zijn UDF's geweldige tools toodo complexe bedrijfslogica als onderdeel van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="ab5c6-583">Evaluatie van operator</span><span class="sxs-lookup"><span data-stu-id="ab5c6-583">Operator evaluation</span></span>
<span data-ttu-id="ab5c6-584">Cosmos DB, tekent uit hoofde van een JSON-database wordt Hallo werkt hetzelfde als met JavaScript-operators en de semantiek voor evaluatie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="ab5c6-585">Terwijl Cosmos DB toopreserve JavaScript-semantiek in termen van JSON-ondersteuning probeert, afwijkt Hallo bewerking evaluatie in sommige gevallen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="ab5c6-586">In DocumentDB API SQL, zijn in tegenstelling tot in traditionele SQL Hallo typen waarden vaak niet bekend totdat Hallo waarden uit de database zijn opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="ab5c6-587">Query's uitvoeren in de volgorde tooefficiently, de meeste van Hallo operators strikt type vereisten hebben.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="ab5c6-588">DocumentDB-API SQL biedt geen impliciete conversies, in tegenstelling tot JavaScript uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="ab5c6-589">Een query voor het exemplaar, zoals `SELECT * FROM Person p WHERE p.Age = 21` overeenkomt met de documenten met een eigenschap Age waarvan de waarde 21 is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="ab5c6-590">Een ander document waarvan de eigenschap leeftijd overeenkomt met de tekenreeks '21' of andere mogelijk oneindige variaties, zoals '021', '21,0', '0021', '00021', enzovoort worden niet overeen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="ab5c6-591">Dit is daarentegen toohello JavaScript waar Hallo tekenreekswaarden impliciet omgezet toonumbers worden (op basis van de operator ex: ==).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="ab5c6-592">Deze keuze is van cruciaal belang voor efficiënte index zoeken in DocumentDB API SQL.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="ab5c6-593">SQL-query's met parameters</span><span class="sxs-lookup"><span data-stu-id="ab5c6-593">Parameterized SQL queries</span></span>
<span data-ttu-id="ab5c6-594">Cosmos DB ondersteunt query's met parameters worden uitgedrukt Hello bekend zijn @ notatie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="ab5c6-595">Geparameteriseerde SQL biedt robuuste verwerken en de aanhalingstekens van gebruikersinvoer, onbedoeld blootstelling van gegevens via SQL-injectie voorkomen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="ab5c6-596">U kunt bijvoorbeeld een query schrijven waarmee achternaam en status van adres als parameters neemt en vervolgens uitgevoerd voor verschillende waarden van de laatste naam en adres staat op basis van de invoer van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="ab5c6-597">Deze aanvraag kan vervolgens worden verzonden tooCosmos DB een JSON-query met parameters zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="ab5c6-598">Hallo argument tooTOP kan worden ingesteld met query's met parameters, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="ab5c6-599">Parameterwaarden mag geldige JSON (tekenreeksen, cijfers, Booleaanse waarden, null, zelfs als deze matrices of geneste JSON).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="ab5c6-600">Ook omdat Cosmos DB schema minder, zijn parameters niet gevalideerd met elk type.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="ab5c6-601"><a id="BuiltinFunctions"></a>Ingebouwde functies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="ab5c6-602">Cosmos DB ondersteunt ook een aantal ingebouwde functies voor algemene bewerkingen, die kunnen worden gebruikt in query's als de gebruiker gedefinieerde functies (UDF's).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="ab5c6-603">Functie-groep</span><span class="sxs-lookup"><span data-stu-id="ab5c6-603">Function group</span></span>          | <span data-ttu-id="ab5c6-604">Bewerkingen</span><span class="sxs-lookup"><span data-stu-id="ab5c6-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ab5c6-605">Wiskundige functies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-605">Mathematical functions</span></span>  | <span data-ttu-id="ab5c6-606">ABS, maximum, EXP, FLOOR, logboek, LOG10, POWER, ROUND, aanmelding, SQRT, VIERKANT, geheel, BOOGCOS, ASIN, BOOGTAN, ATN2, Cosinus, COT, graden PI, radialen, SIN en TAN</span><span class="sxs-lookup"><span data-stu-id="ab5c6-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="ab5c6-607">Controle van de functies van het type</span><span class="sxs-lookup"><span data-stu-id="ab5c6-607">Type checking functions</span></span> | <span data-ttu-id="ab5c6-608">IS_ARRAY, IS_BOOL IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED en IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="ab5c6-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="ab5c6-609">Tekenreeks-functies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-609">String functions</span></span>        | <span data-ttu-id="ab5c6-610">CONCAT, bevat ENDSWITH, INDEX_OF, links, lengte, kleine, LTRIM, vervangen, REPLICEREN, REVERSE, rechts, RTRIM, STARTSWITH, SUBTEKENREEKS en hoofdletters</span><span class="sxs-lookup"><span data-stu-id="ab5c6-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="ab5c6-611">Matrixfuncties</span><span class="sxs-lookup"><span data-stu-id="ab5c6-611">Array functions</span></span>         | <span data-ttu-id="ab5c6-612">ARRAY_CONCAT, ARRAY_CONTAINS ARRAY_LENGTH en ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="ab5c6-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="ab5c6-613">Ruimtelijke functies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-613">Spatial functions</span></span>       | <span data-ttu-id="ab5c6-614">ST_DISTANCE, ST_WITHIN ST_INTERSECTS, ST_ISVALID en ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ab5c6-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="ab5c6-615">Als u momenteel een gebruiker gedefinieerde functie (UDF) waarvoor een ingebouwde functie nu beschikbaar is, moet u de bijbehorende ingebouwde functie Hallo zoals sneller toorun toobe en meer gaat efficiënt.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="ab5c6-616">Wiskundige functies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-616">Mathematical functions</span></span>
<span data-ttu-id="ab5c6-617">Hallo wiskundige functies elke uitvoeren van een berekening op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="ab5c6-618">Hier volgt een lijst met ondersteunde ingebouwde, rekenkundige functies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="ab5c6-619">Gebruik</span><span class="sxs-lookup"><span data-stu-id="ab5c6-619">Usage</span></span> | <span data-ttu-id="ab5c6-620">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ab5c6-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ab5c6-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="ab5c6-622">Retourneert Hallo absolute (positieve) waarde Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="ab5c6-623">MAXIMUM (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="ab5c6-624">Retourneert Hallo kleinste geheel getal groter dan of gelijk zijn aan om Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="ab5c6-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="ab5c6-626">Retourneert de grootste integer Hallo kleiner dan of gelijk toohello numerieke expressie opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="ab5c6-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="ab5c6-628">Retourneert Hallo exponent Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="ab5c6-629">[LOGBOEK (num_expr [, base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="ab5c6-630">Retourneert Hallo natuurlijke logaritme van Hallo numerieke expressie, of Hallo logaritme Hallo met base opgegeven</span><span class="sxs-lookup"><span data-stu-id="ab5c6-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="ab5c6-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="ab5c6-632">Retourneert Hallo grondtal 10 logaritmische waarde Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="ab5c6-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="ab5c6-634">Retourneert een numerieke waarde afgeronde toohello dichtstbijzijnde integer-waarde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="ab5c6-635">GEHEEL (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="ab5c6-636">Retourneert een numerieke waarde ingekorte toohello dichtstbijzijnde integer-waarde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="ab5c6-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="ab5c6-638">Retourneert de vierkantswortel van Hallo Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="ab5c6-639">Vierkante (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="ab5c6-640">Retourneert Hallo vierkante Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="ab5c6-641">VOEDING (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="ab5c6-642">Retourneert Hallo power Hallo opgegeven numerieke expressie toohello waarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="ab5c6-643">ONDERTEKENEN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="ab5c6-644">Retourneert Hallo aanmelding waarde (-1, 0, 1) Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="ab5c6-645">BOOGCOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="ab5c6-646">Retourneert Hallo hoek in radialen, waarvan de cosinus is Hallo opgegeven numerieke expressie. ook wel de boogcosinus genoemd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="ab5c6-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="ab5c6-648">Retourneert Hallo hoek in radialen, waarvan de sinus Hallo is opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="ab5c6-649">Dit wordt ook boogsinus genoemd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="ab5c6-650">BOOGTAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="ab5c6-651">Retourneert Hallo hoek in radialen, waarvan de tangens Hallo is opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="ab5c6-652">Dit wordt ook arctangens genoemd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="ab5c6-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="ab5c6-654">Retourneert Hallo hoek in radialen tussen Hallo positief x-as en Hallo ray van Hallo oorsprong toohello punt (y, x), waarbij x en y zijn Hallo waarden Hallo twee opgegeven float-expressies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="ab5c6-655">CO (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="ab5c6-656">Retourneert Hallo trigonometrische cosinus van Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="ab5c6-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="ab5c6-658">Retourneert Hallo trigonometrische cotangens van Hallo hoek aangeduid in radialen, opgegeven in Hallo numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="ab5c6-659">GRADEN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="ab5c6-660">Retourneert Hallo bijbehorende hoek in graden voor een hoek aangeduid in radialen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="ab5c6-661">PI)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="ab5c6-662">Retourneert Hallo constante waarde van PI.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="ab5c6-663">RADIALEN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="ab5c6-664">Retourneert radialen wanneer een numerieke expressie, in graden wordt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="ab5c6-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="ab5c6-666">Retourneert Hallo trigonometrische sinus van Hallo hoek aangeduid in radialen, in Hallo opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="ab5c6-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="ab5c6-668">Retourneert Hallo tangens van invoerexpressie Hallo in Hallo opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="ab5c6-669">U kunt nu bijvoorbeeld query's zoals Hallo volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="ab5c6-670">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="ab5c6-671">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-671">**Results**</span></span>

    [4]

<span data-ttu-id="ab5c6-672">Hallo belangrijkste verschil tussen Cosmos-database functies vergeleken tooANSI SQL is dat ze ontworpen toowork goed met schemagegevens zonder schema en een gemengde zijn.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="ab5c6-673">Als u hebt een document waarbij de eigenschap Size Hallo ontbreekt of heeft een niet-numerieke waarde als 'Onbekend' vervolgens Hallo document is overgeslagen, klikt u in plaats van een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="ab5c6-674">Controle van de functies van het type</span><span class="sxs-lookup"><span data-stu-id="ab5c6-674">Type checking functions</span></span>
<span data-ttu-id="ab5c6-675">Hallo type controleren of functies kunnen u toocheck Hallo-type van een expressie in SQL-query's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="ab5c6-676">Type controle functies kunnen worden gebruikt toodetermine Hallo type eigenschappen in een documenten op Hallo snel wanneer het variabele of onbekende.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="ab5c6-677">Hier volgt een lijst met ondersteunde ingebouwde typecontrole functies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="ab5c6-678"><strong>Gebruik</strong></span><span class="sxs-lookup"><span data-stu-id="ab5c6-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="ab5c6-679"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="ab5c6-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ab5c6-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="ab5c6-681">Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een matrix is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ab5c6-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="ab5c6-683">Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een Booleaanse waarde is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ab5c6-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="ab5c6-685">Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo waarde null is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ab5c6-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="ab5c6-687">Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo waarde een getal is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ab5c6-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="ab5c6-689">Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een JSON-object is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ab5c6-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="ab5c6-691">Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een tekenreeks is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ab5c6-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="ab5c6-693">Retourneert een Booleaanse waarde die aangeeft of Hallo eigenschap een waarde is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ab5c6-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="ab5c6-695">Retourneert een Booleaanse waarde die aangeeft of Hallo type Hallo-waarde een tekenreeks, getal, Booleaanse waarde of null zijn is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="ab5c6-696">U kunt nu een query's de volgende Hallo uitvoeren met behulp van deze functies:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="ab5c6-697">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="ab5c6-698">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="ab5c6-699">Tekenreeks-functies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-699">String functions</span></span>
<span data-ttu-id="ab5c6-700">Hallo volgende scalaire functies een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="ab5c6-701">Hier volgt een lijst met ingebouwde tekenreeks-functies:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="ab5c6-702">Gebruik</span><span class="sxs-lookup"><span data-stu-id="ab5c6-702">Usage</span></span> | <span data-ttu-id="ab5c6-703">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ab5c6-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ab5c6-704">LENGTE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="ab5c6-705">Retourneert Hallo aantal tekens Hallo opgegeven tekenreeksexpressie</span><span class="sxs-lookup"><span data-stu-id="ab5c6-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="ab5c6-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="ab5c6-707">Retourneert een tekenreeks die Hallo resultaat is van het samenvoegen van twee of meer tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="ab5c6-708">De SUBTEKENREEKS (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="ab5c6-709">Retourneert deel van een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="ab5c6-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="ab5c6-711">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo tweede eindigt</span><span class="sxs-lookup"><span data-stu-id="ab5c6-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="ab5c6-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="ab5c6-713">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo tweede eindigt</span><span class="sxs-lookup"><span data-stu-id="ab5c6-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="ab5c6-714">BEVAT (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="ab5c6-715">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo op de tweede bevat.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="ab5c6-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="ab5c6-717">Retourneert Hallo beginpositie van de eerste instantie Hallo van tweede tekenreeksexpressie Hallo binnen Hallo eerste opgegeven tekenreeksexpressie of -1 als het Hallo-tekenreeks is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="ab5c6-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="ab5c6-719">Retourneert het linkergedeelte van een tekenreeks Hallo Hello opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="ab5c6-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="ab5c6-721">Hallo rechts deel uit van een tekenreeks retourneert Hello opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="ab5c6-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="ab5c6-723">Retourneert een tekenreeksexpressie na het verwijderen van toonaangevende lege waarden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="ab5c6-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="ab5c6-725">Retourneert een tekenreeksexpressie na het afkappen van alle volgspaties.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="ab5c6-726">KLEINE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="ab5c6-727">Retourneert een tekenreeksexpressie na hoofdletter gegevens toolowercase converteren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="ab5c6-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="ab5c6-729">Retourneert een tekenreeksexpressie na kleine letter gegevens toouppercase converteren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="ab5c6-730">Vervang (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="ab5c6-731">Vervangt alle instanties van een opgegeven string-waarde met de waarde van een andere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="ab5c6-732">REPLICEREN (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="ab5c6-733">Herhaalt een string-waarde van een opgegeven aantal keren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="ab5c6-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="ab5c6-735">Retourneert de omgekeerde volgorde Hallo van een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="ab5c6-736">U kunt nu een query's de volgende Hallo uitvoeren met behulp van deze functies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="ab5c6-737">Bijvoorbeeld, kunt u terugkeren Hallo familienaam in hoofdletters als volgt:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="ab5c6-738">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="ab5c6-739">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="ab5c6-740">Of samenvoegen van strings zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="ab5c6-741">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="ab5c6-742">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="ab5c6-743">Tekenreeksfuncties kunnen ook worden gebruikt in Hallo waar component toofilter resultaten, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="ab5c6-744">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="ab5c6-745">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="ab5c6-746">Matrixfuncties</span><span class="sxs-lookup"><span data-stu-id="ab5c6-746">Array functions</span></span>
<span data-ttu-id="ab5c6-747">Hallo scalaire functies na een bewerking uitvoeren op een matrix invoerwaarde en retourneren numerieke, Booleaanse waarde of een matrix van waarde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="ab5c6-748">Hier volgt een lijst met ingebouwde matrixfuncties:</span><span class="sxs-lookup"><span data-stu-id="ab5c6-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="ab5c6-749">Gebruik</span><span class="sxs-lookup"><span data-stu-id="ab5c6-749">Usage</span></span> | <span data-ttu-id="ab5c6-750">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ab5c6-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ab5c6-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="ab5c6-752">Retourneert Hallo aantal elementen Hallo matrixexpressie opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="ab5c6-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="ab5c6-754">Retourneert een matrix die Hallo resultaat is van het samenvoegen van twee of meer matrixwaarden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="ab5c6-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="ab5c6-756">Retourneert een Booleaanse waarde die aangeeft of de matrix Hallo Hallo bevat een waarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="ab5c6-757">Kunt opgeven als Hallo treffer volledig of gedeeltelijk is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="ab5c6-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="ab5c6-759">Retourneert deel van een matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="ab5c6-760">Matrixfuncties kunnen worden gebruikt toomanipulate matrices in JSON.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="ab5c6-761">Hier is bijvoorbeeld een query die alle documenten retourneert waarbij een van de ouders Hallo 'Robin Wakefield' is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="ab5c6-762">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="ab5c6-763">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="ab5c6-764">U kunt een gedeeltelijke fragment voor overeenkomende elementen binnen de matrix Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="ab5c6-765">Hallo volgende query vindt u alle bovenliggende items Hello `givenName` van `Robin`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="ab5c6-766">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="ab5c6-767">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="ab5c6-768">Hier volgt een voorbeeld met ARRAY_LENGTH tooget Hallo aantal onderliggende items per serie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="ab5c6-769">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="ab5c6-770">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="ab5c6-771">Ruimtelijke functies</span><span class="sxs-lookup"><span data-stu-id="ab5c6-771">Spatial functions</span></span>
<span data-ttu-id="ab5c6-772">Hallo volgende ingebouwde functies voor query's in georuimtelijke Open georuimtelijke Consortium (OGC) biedt ondersteuning voor cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="ab5c6-773"><strong>Gebruik</strong></span><span class="sxs-lookup"><span data-stu-id="ab5c6-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="ab5c6-774"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="ab5c6-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="ab5c6-776">Retourneert Hallo afstand tussen twee Hallo GeoJSON punt, Polygon of LineString expressies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="ab5c6-778">Retourneert een Booleaanse expressie die aangeeft of Hallo eerste GeoJSON-object (punt, Polygon of LineString) binnen Hallo tweede GeoJSON-object (punt, Polygon of LineString).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="ab5c6-780">Retourneert een Booleaanse expressie die aangeeft of Hallo twee opgegeven GeoJSON-objecten (punt, Polygon of LineString) intersect.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="ab5c6-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="ab5c6-782">Retourneert een Booleaanse waarde die aangeeft of Hallo opgegeven GeoJSON punt, Polygon of LineString expressie is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ab5c6-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ab5c6-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="ab5c6-784">Retourneert een JSON-waarde met een Boolean-waarde als Hallo GeoJSON punt, Polygon of LineString expressie opgegeven geldig is en als ongeldig, bovendien Hallo reden als een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="ab5c6-785">Ruimtelijke functies kunnen worden gebruikt tooperform nabijheid query's op ruimtelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="ab5c6-786">Hier is bijvoorbeeld een query waarmee alle familie documenten dat binnen 30 km Hallo opgegeven locatie Hallo ST_DISTANCE ingebouwde functie gebruikt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="ab5c6-787">**Query**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="ab5c6-788">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="ab5c6-789">Zie voor meer informatie over ondersteuning voor Cosmos DB georuimtelijke [werken met gegevens in Azure Cosmos DB georuimtelijke](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="ab5c6-790">Die loopt van ruimtelijke functies en Hallo SQL-syntaxis voor Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="ab5c6-791">Nu eens kijken hoe LINQ-query werkt en hoe deze samenwerkt met de syntaxis van de Hallo we hebt gezien tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="ab5c6-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="ab5c6-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="ab5c6-793">LINQ is een .NET-programmeermodel waarin berekeningen query's voor stromen van objecten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="ab5c6-794">Cosmos DB biedt een toointerface clientzijde bibliotheek met LINQ doordat een conversie tussen JSON en .NET-objecten en een toewijzing voor een subset van LINQ query's tooCosmos DB-query's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="ab5c6-795">Hallo in de volgende afbeelding toont de architectuur Hallo LINQ-query's met behulp van de Cosmos-DB ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="ab5c6-796">Met behulp van Hallo Cosmos DB client kunnen ontwikkelaars maken een **IQueryable** object dat rechtstreeks query's hello Cosmos-DB-provider opvragen, die vervolgens Hallo LINQ-query in een Cosmos-DB-query zet.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="ab5c6-797">Hallo query toohello Cosmos DB server tooretrieve een set resultaten vervolgens doorgegeven in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="ab5c6-798">Hallo geretourneerd resultaten in een stream met .NET-objecten aan de clientzijde Hallo gedeserialiseerd worden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![Architectuur van de LINQ-query's met DocumentDB-API - SQL-syntaxis, JSON-querytaal concepten van de database en SQL-query's ondersteunen][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="ab5c6-800">.NET- en JSON-toewijzing</span><span class="sxs-lookup"><span data-stu-id="ab5c6-800">.NET and JSON mapping</span></span>
<span data-ttu-id="ab5c6-801">Hallo-toewijzing tussen .NET-objecten en JSON-documenten is natuurlijk - elk veld gegevens lid is toegewezen tooa JSON-object, waarbij Hallo veldnaam is toohello 'sleutel' onderdeel zijn van Hallo-object toegewezen en Hallo '' waarde '' onderdeel recursief toegewezen toohello waardedeel uitmaakt van Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="ab5c6-802">Overweeg het volgende voorbeeld Hallo: Hallo familie-object gemaakt is toegewezen toohello JSON-document, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="ab5c6-803">En vice versa Hallo JSON-document is toegewezen back tooa .NET-object.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="ab5c6-804">**C#-klasse**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-804">**C# Class**</span></span>

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


<span data-ttu-id="ab5c6-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-805">**JSON**</span></span>  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a><span data-ttu-id="ab5c6-806">De vertaling van LINQ tooSQL</span><span class="sxs-lookup"><span data-stu-id="ab5c6-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="ab5c6-807">Hallo Cosmos-DB-provider opvragen voert een best effort toewijzing van een LINQ-query naar een Cosmos DB SQL-query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="ab5c6-808">Hallo beschrijving te volgen, veronderstellen we Hallo lezer heeft een elementaire kennis van LINQ.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="ab5c6-809">Eerst ondersteunen Hallo-typesysteem, wij alle JSON primitieve typen – numerieke typen, Booleaanse waarde, tekenreeks en null.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="ab5c6-810">Alleen deze JSON-typen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-810">Only these JSON types are supported.</span></span> <span data-ttu-id="ab5c6-811">Hallo volgende scalaire expressies worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="ab5c6-812">Constante waarden – hierbij constante waarden van de primitieve gegevenstypen Hallo gelijktijdig Hallo Hallo query wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="ab5c6-813">Eigenschappenmatrix/indexexpressies – deze expressies Raadpleeg toohello-eigenschap van een object of een element van de matrix.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="ab5c6-814">familie. ID;    Family.children[0].familyName;    Family.children[0].Grade;    Family.children[n].Grade; n is een int-variabele</span><span class="sxs-lookup"><span data-stu-id="ab5c6-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="ab5c6-815">Aritmetische expressies - deze algemene aritmetische expressies op numerieke en Booleaanse waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="ab5c6-816">Raadpleeg voor de volledige lijst hello, toohello SQL-specificatie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="ab5c6-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="ab5c6-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="ab5c6-818">Vergelijking van tekenreeksexpressie - hierbij een string-waarde toosome constante string-waarde te vergelijken.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="ab5c6-819">mother.familyName == 'Smith';    child.givenName == s; s is een string-variabele</span><span class="sxs-lookup"><span data-stu-id="ab5c6-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="ab5c6-820">Object/matrix maken van expressie - deze expressies return een object van het waardetype van de samengestelde of anoniem type of een matrix van dergelijke objecten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="ab5c6-821">Deze waarden kunnen worden genest.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-821">These values can be nested.</span></span>
  
     <span data-ttu-id="ab5c6-822">nieuwe bovenliggende {familyName = 'Smit', givenName = "Jan"}; nieuwe {eerst = 1, tweede = 2}; een anoniem type met twee velden</span><span class="sxs-lookup"><span data-stu-id="ab5c6-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="ab5c6-823">nieuwe int [] {3, child.grade, 5};</span><span class="sxs-lookup"><span data-stu-id="ab5c6-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="ab5c6-824"><a id="SupportedLinqOperators"></a>Lijst met ondersteunde LINQ-operators</span><span class="sxs-lookup"><span data-stu-id="ab5c6-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="ab5c6-825">Hier volgt een lijst met ondersteunde LINQ-operators in Hallo LINQ-provider is opgenomen in Hallo DocumentDB .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="ab5c6-826">**Selecteer**: projecties toohello Selecteer objectconstructie inclusief SQL vertalen</span><span class="sxs-lookup"><span data-stu-id="ab5c6-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="ab5c6-827">**Waar**: Filters toohello waar SQL vertalen en ondersteuning voor de conversie van & &, || en!</span><span class="sxs-lookup"><span data-stu-id="ab5c6-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="ab5c6-828">toohello SQL-operators</span><span class="sxs-lookup"><span data-stu-id="ab5c6-828">toohello SQL operators</span></span>
* <span data-ttu-id="ab5c6-829">**SelectMany**: kunt ongedaan maken van matrices toohello SQL JOIN-component.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="ab5c6-830">Gebruikte toochain/nest expressies toofilter op matrixelementen kan zijn</span><span class="sxs-lookup"><span data-stu-id="ab5c6-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="ab5c6-831">**OrderBy en OrderByDescending**: zet tooORDER BY oplopend/aflopend</span><span class="sxs-lookup"><span data-stu-id="ab5c6-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="ab5c6-832">**Aantal**, **som**, **Min**, **Max**, en **gemiddelde** operators voor aggregatie en de async-equivalenten **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, en **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="ab5c6-833">**CompareTo**: zet toorange vergelijkingen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="ab5c6-834">Meestal gebruikt voor tekenreeksen omdat ze nog niet vergeleken in .NET</span><span class="sxs-lookup"><span data-stu-id="ab5c6-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="ab5c6-835">**Nemen**: zet toohello SQL TOP voor het beperken van de resultaten van een query</span><span class="sxs-lookup"><span data-stu-id="ab5c6-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="ab5c6-836">**Rekenkundige functies**: de vertaling van ondersteunt. De NET Abs, BOOGCOS, Asin, BOOGTAN, maximum, CO, Exp, Floor, logboek, Log10, Pow, Round, aanmelding, Sin, Sqrt, Tan, toohello gelijkwaardige SQL ingebouwde functies worden afgekapt.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="ab5c6-837">**Functies String**: de vertaling van ondersteunt. NET van Concat, bevat EndsWith, IndexOf, Count, ToLower, TrimStart, vervangen, Reverse, TrimEnd, StartsWith, subtekenreeks ToUpper toohello gelijkwaardige SQL ingebouwde functies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="ab5c6-838">**Matrix van functies**: de vertaling van ondersteunt. NET van Concat bevat en aantal toohello gelijkwaardige SQL ingebouwde functies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="ab5c6-839">**Extensiefuncties georuimtelijke**: ondersteunt de vertaling van stub-methoden afstand binnen IsValid, en IsValidDetailed toohello gelijkwaardige SQL ingebouwde functies.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="ab5c6-840">**Gebruiker gedefinieerde functie extensiefunctie**: ondersteunt de vertaling van Hallo stub-methode UserDefinedFunctionProvider.Invoke toohello overeenkomende gebruiker gedefinieerde functie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="ab5c6-841">**Diverse**: ondersteunt de vertaling van Hallo coalesce en voorwaardelijke operators.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="ab5c6-842">Kan vertalen bevat tooString bevat, ARRAY_CONTAINS of Hallo SQL IN, afhankelijk van de context.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="ab5c6-843">SQL-query-operators</span><span class="sxs-lookup"><span data-stu-id="ab5c6-843">SQL query operators</span></span>
<span data-ttu-id="ab5c6-844">Hier volgen enkele voorbeelden die aangeven hoe sommige Hallo standaard de LINQ-query-operators omlaag tooCosmos DB-query's worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="ab5c6-845">Operator selecteren</span><span class="sxs-lookup"><span data-stu-id="ab5c6-845">Select Operator</span></span>
<span data-ttu-id="ab5c6-846">Hallo-syntaxis is `input.Select(x => f(x))`, waarbij `f` is een scalaire expressie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="ab5c6-847">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="ab5c6-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="ab5c6-849">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="ab5c6-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="ab5c6-851">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="ab5c6-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="ab5c6-853">SelectMany operator</span><span class="sxs-lookup"><span data-stu-id="ab5c6-853">SelectMany operator</span></span>
<span data-ttu-id="ab5c6-854">Hallo-syntaxis is `input.SelectMany(x => f(x))`, waarbij `f` is een scalaire expressie die als resultaat een verzamelingstype geeft.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="ab5c6-855">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="ab5c6-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="ab5c6-857">Waar operator</span><span class="sxs-lookup"><span data-stu-id="ab5c6-857">Where operator</span></span>
<span data-ttu-id="ab5c6-858">Hallo-syntaxis is `input.Where(x => f(x))`, waarbij `f` is een scalaire expressie die een Booleaanse waarde retourneert.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="ab5c6-859">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="ab5c6-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="ab5c6-861">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="ab5c6-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="ab5c6-863">Samengestelde SQL-query 's</span><span class="sxs-lookup"><span data-stu-id="ab5c6-863">Composite SQL queries</span></span>
<span data-ttu-id="ab5c6-864">Hallo hierboven operators samengesteld tooform krachtige query's kan worden.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="ab5c6-865">Aangezien Cosmos DB geneste verzamelingen ondersteunt, kan Hallo samenstelling worden samengevoegd of genest.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="ab5c6-866">Samenvoeging</span><span class="sxs-lookup"><span data-stu-id="ab5c6-866">Concatenation</span></span>
<span data-ttu-id="ab5c6-867">Hallo-syntaxis is `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="ab5c6-868">Een samengevoegde query kunt beginnen met een optionele `SelectMany` query gevolgd door meerdere `Select` of `Where` operators.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="ab5c6-869">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="ab5c6-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="ab5c6-871">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="ab5c6-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="ab5c6-873">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="ab5c6-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="ab5c6-875">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="ab5c6-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="ab5c6-877">Nesten</span><span class="sxs-lookup"><span data-stu-id="ab5c6-877">Nesting</span></span>
<span data-ttu-id="ab5c6-878">Hallo-syntaxis is `input.SelectMany(x=>x.Q())` waarbij Q is een `Select`, `SelectMany`, of `Where` operator.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="ab5c6-879">Hallo binnenste query is in een geneste query, toegepaste tooeach-element van de buitenste verzameling Hallo.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="ab5c6-880">Een belangrijke functie is dat die Hallo binnenste query kunt verwijzen toohello velden van het Hallo-elementen in de buitenste verzameling Hallo zoals zelf-joins.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="ab5c6-881">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="ab5c6-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="ab5c6-883">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="ab5c6-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="ab5c6-885">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="ab5c6-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="ab5c6-887"><a id="ExecutingSqlQueries"></a>SQL-query's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ab5c6-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="ab5c6-888">Cosmos DB Ontsluit resources via een REST-API die kan worden aangeroepen via elke taal waarmee HTTP/HTTPS-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="ab5c6-889">Daarnaast biedt Cosmos DB programmeringsbibliotheken voor verschillende veelgebruikte talen zoals .NET, Node.js, JavaScript en Python.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="ab5c6-890">Hallo REST-API en Hallo ondersteuning voor verschillende bibliotheken alle opvragen via SQL.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="ab5c6-891">Hallo .NET SDK biedt ondersteuning voor LINQ bovendien tooSQL opvragen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="ab5c6-892">Hallo volgen voorbeelden kunt u zien hoe een query toocreate en te verzenden op basis van een Cosmos-DB-databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="ab5c6-893"><a id="RestAPI"></a>REST-API</span><span class="sxs-lookup"><span data-stu-id="ab5c6-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="ab5c6-894">Cosmos DB biedt een open RESTful-programmeermodel via HTTP.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="ab5c6-895">Database-accounts kunnen worden ingericht met behulp van een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="ab5c6-896">Hallo Cosmos DB resourcemodel bestaat uit een set resources onder de databaseaccount van een, die elk opgevraagd met een logische en stabiele-URI is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="ab5c6-897">Een set resources is waarnaar wordt verwezen tooas een feed in dit document.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="ab5c6-898">Een databaseaccount bestaat uit een reeks databases, die elk meerdere verzamelingen met elk van welke beurt documenten, UDF's en andere brontypen bevatten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="ab5c6-899">Hallo basic interactie model met deze resources is via Hallo HTTP-woorden GET, PUT, POST en DELETE met hun standaard interpretatie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="ab5c6-900">Hallo POST term wordt gebruikt voor het maken van een nieuwe resource, voor het uitvoeren van een opgeslagen procedure of voor het uitgeven van een Cosmos-DB-query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="ab5c6-901">Query's zijn altijd alleen-lezen bewerkingen met geen bijwerkingen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="ab5c6-902">Hallo volgende voorbeelden ziet u een POST voor een DocumentDB-API-query ten opzichte van een verzameling met Hallo twee voorbeelddocumenten dat we tot nu toe hebt bekeken.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="ab5c6-903">Hallo-query heeft een eenvoudige filter op Hallo JSON name-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="ab5c6-904">Houd er rekening mee Hallo gebruik van Hallo `x-ms-documentdb-isquery` en Content-Type: `application/query+json` toodenote headers die Hallo bewerking is een query.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="ab5c6-905">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-905">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="ab5c6-906">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-906">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


<span data-ttu-id="ab5c6-907">Hallo tweede voorbeeld ziet u een complexere query die meerdere resultaten uit Hallo join retourneert.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="ab5c6-908">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-908">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="ab5c6-909">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="ab5c6-909">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


<span data-ttu-id="ab5c6-910">Als de queryresultaten niet binnen één pagina van de resultaten passen en vervolgens Hallo REST-API een vervolgtoken via Hallo retourneert `x-ms-continuation-token` antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="ab5c6-911">Clients kunnen resultaten pagineren door Hallo-header in de volgende resultaten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="ab5c6-912">het aantal resultaten per pagina Hallo kan ook worden beheerd via Hallo `x-ms-max-item-count` nummer header.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="ab5c6-913">Als de opgegeven query Hallo een statistische functie zoals heeft `COUNT`, en vervolgens Hallo querypagina een gedeeltelijk cumulatieve waarde kan worden geretourneerd gedurende Hallo pagina met resultaten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="ab5c6-914">Hallo-clients moeten een aggregatie tweede niveau uitvoeren via deze resultaten tooproduce Hallo laatste resultaten, bijvoorbeeld, som is opgegeven via Hallo aantallen geretourneerd in Hallo afzonderlijke pagina's tooreturn Hallo totale aantal.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="ab5c6-915">beleid voor toomanage Hallo gegevens consistentie voor query's, gebruik Hallo `x-ms-consistency-level` header bijvoorbeeld alle aanvragen voor REST-API.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="ab5c6-916">Voor sessieconsistentie, is het vereist tooalso echo hallo nieuwste `x-ms-session-token` Cookie-kop in Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="ab5c6-917">Hallo indexeringsbeleid aangevraagde verzameling kan ook van invloed zijn op Hallo consistentie van de queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="ab5c6-918">Met standaard Hallo indexeren beleidsinstellingen voor verzamelingen Hallo index is altijd met inhoud van het document Hallo en query resultaten overeenkomen met de Hallo consistentie gekozen voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="ab5c6-919">Als Hallo indexeren beleid beperkte tooLazy is, kunnen query's verlopen resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="ab5c6-920">Zie voor meer informatie [Azure Cosmos DB Consistentieniveaus][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="ab5c6-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="ab5c6-921">Als indexeringsbeleid op Hallo verzameling Hallo geconfigureerd Hallo opgegeven query niet ondersteunen kan, retourneert hello Azure Cosmos DB server 400 'onjuiste aanvraag'.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="ab5c6-922">Dit wordt geretourneerd voor bereik query's op paden die zijn geconfigureerd voor lookups op hash (gelijkheid) en voor paden expliciet is uitgesloten van het indexeren.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="ab5c6-923">Hallo `x-ms-documentdb-query-enable-scan` header opgegeven tooallow Hallo query tooperform een scan kan zijn wanneer een index niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="ab5c6-924">U kunt gedetailleerde metrische gegevens over de uitvoering van de query opvragen door in te stellen `x-ms-documentdb-populatequerymetrics` header te`True`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="ab5c6-925">Zie voor meer informatie [SQL query metrische gegevens voor Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ab5c6-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="ab5c6-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="ab5c6-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="ab5c6-927">Hallo .NET SDK biedt ondersteuning voor LINQ- en SQL uitvoeren van query's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="ab5c6-928">Hallo volgende voorbeeld ziet u hoe tooperform Hallo eenvoudige filterquery geïntroduceerd eerder in dit document.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="ab5c6-929">Dit voorbeeld vergelijkt twee eigenschappen op gelijkheid binnen elk document en maakt gebruik van anonieme projecties.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="ab5c6-930">Hallo volgende voorbeeld ziet u joins, die zijn uitgedrukt via LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="ab5c6-931">Hallo .NET-client worden automatisch alle Hallo-pagina's van queryresultaten in Hallo foreach blokken zoals hierboven doorlopen.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="ab5c6-932">Hallo-query die is geïntroduceerd in Hallo REST-API-sectie opties zijn ook beschikbaar in .NET SDK met de Hallo Hallo `FeedOptions` en `FeedResponse` klassen in Hallo CreateDocumentQuery methode.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="ab5c6-933">Hallo aantal pagina's kan worden beheerd met behulp van Hallo `MaxItemCount` instelling.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="ab5c6-934">U kunt ook expliciet paginering bepalen door het maken van `IDocumentQueryable` met Hallo `IQueryable` object, klikt u vervolgens op het lezen van de` ResponseContinuationToken` waarden en deze weer toe als `RequestContinuationToken` in `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="ab5c6-935">`EnableScanInQuery`is set tooenable scans als Hallo query kan niet worden ondersteund door het indexeringsbeleid Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="ab5c6-936">Voor gepartitioneerde verzamelingen kunt u `PartitionKey` toorun Hallo-query op één partitie (Hoewel Cosmos DB dit automatisch uit de querytekst Hallo ophalen kunt), en `EnableCrossPartitionQuery` toorun-query's die toobe mogelijk moet uitvoeren op meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="ab5c6-937">Raadpleeg te[Azure Cosmos DB .NET-voorbeelden](https://github.com/Azure/azure-documentdb-net) voor meer voorbeelden met query's.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="ab5c6-938"><a id="JavaScriptServerSideApi"></a>JavaScript-serverzijde-API</span><span class="sxs-lookup"><span data-stu-id="ab5c6-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="ab5c6-939">Cosmos DB biedt een programmeermodel voor het uitvoeren op basis van JavaScript-toepassingslogica rechtstreeks op Hallo verzamelingen met opgeslagen procedures en triggers.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="ab5c6-940">Hallo JavaScript-logica geregistreerd op het niveau van een verzameling kan databasebewerkingen uitvoeren op Hallo-bewerkingen op Hallo documenten Hallo gegeven verzameling vervolgens uitgeven.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="ab5c6-941">Deze bewerkingen zijn verpakt in een ambient ACID-transactions.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="ab5c6-942">Hallo volgende voorbeeld laat zien hoe toouse hello queryDocuments in Hallo JavaScript-server API toomake van query's binnen opgeslagen procedures en triggers.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="ab5c6-943"><a id="References"></a>Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="ab5c6-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="ab5c6-944">[Inleiding tooAzure Cosmos-DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="ab5c6-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="ab5c6-945">Azure SQL voor Cosmos-DB-specificatie</span><span class="sxs-lookup"><span data-stu-id="ab5c6-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="ab5c6-946">Azure Cosmos DB .NET-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="ab5c6-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="ab5c6-947">[Azure Cosmos DB Consistentieniveaus][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="ab5c6-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="ab5c6-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="ab5c6-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="ab5c6-950">JavaScript-specificatie [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="ab5c6-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="ab5c6-952">Van evaluatietechnieken voor grote databases query [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="ab5c6-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="ab5c6-953">Queryverwerking in parallelle relationele databasesystemen, IEEE Computer samenleving Press, 1994</span><span class="sxs-lookup"><span data-stu-id="ab5c6-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="ab5c6-954">Lu, Ooi, Tan queryverwerking in parallelle relationele databasesystemen, IEEE Computer samenleving Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="ab5c6-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: een niet zodat vreemde taal voor gegevensverwerking, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="ab5c6-956">G.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-956">G.</span></span> <span data-ttu-id="ab5c6-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-957">Graefe.</span></span> <span data-ttu-id="ab5c6-958">Hallo trapsgewijs framework voor queryoptimalisatie.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="ab5c6-959">IEEE-gegevens eng</span><span class="sxs-lookup"><span data-stu-id="ab5c6-959">IEEE Data Eng.</span></span> <span data-ttu-id="ab5c6-960">Bull., 18, lid 3: 1995.</span><span class="sxs-lookup"><span data-stu-id="ab5c6-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md