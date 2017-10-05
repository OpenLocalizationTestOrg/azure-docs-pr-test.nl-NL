---
title: SQL-query's voor Azure Cosmos DB DocumentDB API | Microsoft Docs
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
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="11203-105">SQL-query's voor Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="11203-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="11203-106">Microsoft Azure Cosmos DB biedt ondersteuning voor documentquery's die gebruikmaken van SQL (Structured Query Language) als een JSON-querytaal.</span><span class="sxs-lookup"><span data-stu-id="11203-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="11203-107">Cosmos DB is volledig zonder schema.</span><span class="sxs-lookup"><span data-stu-id="11203-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="11203-108">Doordat het gebied van de JSON-gegevensmodel rechtstreeks in de database-engine biedt deze automatische indexering van JSON-documenten zonder expliciet schema of het maken van secundaire indexen.</span><span class="sxs-lookup"><span data-stu-id="11203-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="11203-109">Tijdens het ontwerpen van de query language voor Cosmos DB, zijn twee drie doelen voor ogen:</span><span class="sxs-lookup"><span data-stu-id="11203-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="11203-110">We wilden in plaats van een nieuwe JSON-querytaal vruchtbare, ter ondersteuning van SQL.</span><span class="sxs-lookup"><span data-stu-id="11203-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="11203-111">SQL is een van de bekend en meest populaire querytalen.</span><span class="sxs-lookup"><span data-stu-id="11203-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="11203-112">Cosmos DB SQL biedt een formele programmeermodel voor uitgebreide query's via JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="11203-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="11203-113">We wilden van JavaScript-programmeermodel gebruikt als basis voor de querytaal als een JSON-document-database kan worden uitgevoerd van JavaScript rechtstreeks in de database-engine.</span><span class="sxs-lookup"><span data-stu-id="11203-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="11203-114">De API DocumentDB SQL verankerd ligt in de JavaScript-typesysteem, evaluatie van expressies en functieaanroep.</span><span class="sxs-lookup"><span data-stu-id="11203-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="11203-115">Deze beurt biedt een natuurlijke programmeermodel voor projecties relationele, hiërarchische navigatie in JSON-documenten, self joins, ruimtelijke query's en aanroep van de gebruiker gedefinieerde functies (UDF's) geschreven volledig in JavaScript, onder andere functies.</span><span class="sxs-lookup"><span data-stu-id="11203-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="11203-116">We zijn ervan overtuigd dat deze mogelijkheden essentieel zijn voor het reduceren van de wrijving tussen de toepassing en de database en essentieel voor de productiviteit van ontwikkelaars zijn.</span><span class="sxs-lookup"><span data-stu-id="11203-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="11203-117">We raden aan de slag door het bekijken van de volgende video, Aravind Ramachandran waar de Cosmos-DB querymogelijkheden toont, en in via onze [Queryspeelplaats](http://www.documentdb.com/sql/demo), waarbij u kunt Cosmos-database uitproberen en SQL-query's op onze gegevensset uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="11203-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="11203-118">Keer vervolgens terug naar dit artikel, waar u begint met een SQL-query-zelfstudie die u bij enkele eenvoudige JSON-documenten en de SQL-opdrachten helpt.</span><span class="sxs-lookup"><span data-stu-id="11203-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="11203-119"><a id="GettingStarted"></a>Aan de slag met SQL-opdrachten in een Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="11203-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="11203-120">Als u Cosmos DB SQL op het werk, laten we beginnen met een paar eenvoudige JSON-documenten en enkele eenvoudige query's op deze doorlopen.</span><span class="sxs-lookup"><span data-stu-id="11203-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="11203-121">U kunt deze twee JSON-documenten over twee families.</span><span class="sxs-lookup"><span data-stu-id="11203-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="11203-122">Met Cosmos-DB hoeft we niet expliciet een schema's of secundaire indexen maken.</span><span class="sxs-lookup"><span data-stu-id="11203-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="11203-123">Moet u de JSON-documenten aan een verzameling Cosmos DB invoegen en vervolgens een query.</span><span class="sxs-lookup"><span data-stu-id="11203-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="11203-124">Hier hebben we een eenvoudige JSON-document voor de Andersen family, de bovenliggende items, onderliggende elementen (en hun huisdieren), adres en registratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="11203-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="11203-125">Het document heeft tekenreeksen, getallen, Booleaanse waarden, matrices en geneste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="11203-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="11203-126">**Document**</span><span class="sxs-lookup"><span data-stu-id="11203-126">**Document**</span></span>  

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

<span data-ttu-id="11203-127">Hier volgt een tweede document een subtiele verschil – `givenName` en `familyName` worden gebruikt in plaats van `firstName` en `lastName`.</span><span class="sxs-lookup"><span data-stu-id="11203-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="11203-128">**Document**</span><span class="sxs-lookup"><span data-stu-id="11203-128">**Document**</span></span>  

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

<span data-ttu-id="11203-129">Nu gaan we enkele query's op deze gegevens om een idee van de belangrijkste aspecten van DocumentDB API SQL te proberen.</span><span class="sxs-lookup"><span data-stu-id="11203-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="11203-130">De volgende query retourneert bijvoorbeeld de documenten waarbij het veld id overeenkomt met `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="11203-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="11203-131">Omdat het een `SELECT *`, de uitvoer van de query is de volledige JSON-document:</span><span class="sxs-lookup"><span data-stu-id="11203-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="11203-132">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="11203-133">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-133">**Results**</span></span>

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


<span data-ttu-id="11203-134">Bekijk nu het geval waar moeten we opnieuw indelen van de JSON-uitvoer in een andere vorm.</span><span class="sxs-lookup"><span data-stu-id="11203-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="11203-135">Deze query projecteert een nieuwe JSON-object met twee geselecteerde velden naam en plaats, wanneer het adres stad dezelfde naam als de status heeft.</span><span class="sxs-lookup"><span data-stu-id="11203-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="11203-136">In dit geval 'NY, NY' komt overeen met.</span><span class="sxs-lookup"><span data-stu-id="11203-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="11203-137">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="11203-138">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="11203-139">De volgende query retourneert de opgegeven namen van onderliggende items in de familie-id die overeenkomt met `WakefieldFamily` geordend op de plaats waar je woont.</span><span class="sxs-lookup"><span data-stu-id="11203-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="11203-140">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="11203-141">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="11203-142">Wij willen graag aandacht te vestigen op enkele opmerkelijk aspecten van de Cosmos-DB-querytaal via de voorbeelden die we tot nu toe hebt gezien:</span><span class="sxs-lookup"><span data-stu-id="11203-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="11203-143">Aangezien DocumentDB API SQL op JSON-waarden werkt, behandelt structuur in de vorm van entiteiten in plaats van rijen en kolommen.</span><span class="sxs-lookup"><span data-stu-id="11203-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="11203-144">De taal kunt u knooppunten van de structuur op elke willekeurige diepte zoals Raadpleeg daarom `Node1.Node2.Node3…..Nodem`, vergelijkbaar met relationele SQL verwijst naar de twee onderdeelverwijzing van `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="11203-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="11203-145">De structured query language werkt met schema minder gegevens.</span><span class="sxs-lookup"><span data-stu-id="11203-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="11203-146">Daarom moet het typesysteem dynamisch worden gebonden.</span><span class="sxs-lookup"><span data-stu-id="11203-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="11203-147">Verschillende typen op verschillende documenten kan resulteert in dezelfde expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="11203-148">Het resultaat van een query is een geldige JSON-waarde, maar van een vast schema kan niet worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="11203-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="11203-149">Cosmos DB ondersteunt alleen strikte JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="11203-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="11203-150">Dit betekent dat de systeem- en expressies zijn beperkt tot alleen met JSON-typen zijn getroffen.</span><span class="sxs-lookup"><span data-stu-id="11203-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="11203-151">Raadpleeg de [JSON-specificatie](http://www.json.org/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="11203-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="11203-152">Een Cosmos-DB-verzameling is een container zonder schema van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="11203-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="11203-153">De relaties in gegevensentiteiten binnen en tussen documenten in een verzameling worden impliciet door containment en niet door de primaire sleutel en refererende sleutels relaties vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="11203-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="11203-154">Dit is een belangrijk aspect waard wijzen op in het licht de intra-document wordt besproken verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="11203-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="11203-155"><a id="Indexing"></a>Cosmos DB indexeren</span><span class="sxs-lookup"><span data-stu-id="11203-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="11203-156">Voordat we in de DocumentDB API SQL-syntaxis ophalen, is het waard het ontwerp van de indexering in Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="11203-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="11203-157">Het doel van de indexen van de database is voor het uitvoeren van query's in hun diverse vormen en vormen met minimale brongebruik (zoals CPU en input/output) en tegelijkertijd goede doorvoer en lage latentie.</span><span class="sxs-lookup"><span data-stu-id="11203-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="11203-158">Vaak is de keuze van de juiste index voor query's in een database vereist veel planning en experimenteren.</span><span class="sxs-lookup"><span data-stu-id="11203-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="11203-159">Deze aanpak vormt een uitdaging voor schema-minder databases waarin de gegevens voldoen niet aan een strikte schema en snel ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="11203-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="11203-160">Wanneer we de Cosmos-DB indexering subsysteem ontworpen, instellen wij daarom de volgende doelen:</span><span class="sxs-lookup"><span data-stu-id="11203-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="11203-161">Documenten te indexeren zonder schema: het subsysteem voor indexering geen vereist een schema-informatie of veronderstellingen over schema van de documenten.</span><span class="sxs-lookup"><span data-stu-id="11203-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="11203-162">Ondersteuning voor efficiënte, geavanceerde hiërarchische en relationele query's: de index ondersteunt de Cosmos-DB-querytaal efficiënt, inclusief ondersteuning voor hiërarchische en relationele projecties.</span><span class="sxs-lookup"><span data-stu-id="11203-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="11203-163">Ondersteuning voor consistente query's in face of een volgehouden volume van schrijfbewerkingen: voor schrijven met hoge doorvoer werkbelastingen met consistente query's, de index incrementeel efficiënt en online met betrekking tot een continue volume van schrijfbewerkingen wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="11203-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="11203-164">De consistente index-update is van cruciaal belang om te dienen als de query's op het consistentieniveau van de waarin de gebruiker het documentservice hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="11203-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="11203-165">Ondersteuning voor multitenancy: gegeven het model op basis van een reservering voor de resource governance tussen tenants, index-updates worden uitgevoerd binnen het budget van systeembronnen (CPU, geheugen en input/output-bewerkingen per seconde) die per replica worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="11203-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="11203-166">Opslagruimte: voor de kosteneffectiviteit, de schijfopslag op overhead van de index is gebonden en voorspelbaar.</span><span class="sxs-lookup"><span data-stu-id="11203-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="11203-167">Dit is cruciaal omdat Cosmos DB kan de ontwikkelaar maken op basis van kosten-en nadelen tussen index overhead ten opzichte van de prestaties van query's.</span><span class="sxs-lookup"><span data-stu-id="11203-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="11203-168">Raadpleeg de [Azure Cosmos DB voorbeelden](https://github.com/Azure/azure-documentdb-net) op MSDN voor voorbeelden waarin wordt getoond hoe het indexeringsbeleid voor een verzameling configureren.</span><span class="sxs-lookup"><span data-stu-id="11203-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="11203-169">Laten we nu krijgen tot de details van de Azure Cosmos DB SQL-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="11203-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="11203-170"><a id="Basics"></a>Basisprincipes van een Azure Cosmos DB SQL-query</span><span class="sxs-lookup"><span data-stu-id="11203-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="11203-171">Elke query bestaat uit een SELECT-component en een optionele FROM en WHERE-componenten per ANSI SQL-standaarden.</span><span class="sxs-lookup"><span data-stu-id="11203-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="11203-172">Normaal gesproken voor elke query moet de bron in de component FROM is geïnventariseerd.</span><span class="sxs-lookup"><span data-stu-id="11203-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="11203-173">Het filter in de component WHERE wordt vervolgens toegepast op de bron voor het ophalen van een subset van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="11203-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="11203-174">Ten slotte wordt de SELECT-component gebruikt om de aangevraagde JSON-waarden in de select-lijst.</span><span class="sxs-lookup"><span data-stu-id="11203-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="11203-175"><a id="FromClause"></a>FROM-component</span><span class="sxs-lookup"><span data-stu-id="11203-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="11203-176">De `FROM <from_specification>` component is optioneel tenzij de bron is gefilterd of geprojecteerd verderop in de query.</span><span class="sxs-lookup"><span data-stu-id="11203-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="11203-177">Het doel van deze component is om op te geven van de gegevensbron waarop de query moet functioneren.</span><span class="sxs-lookup"><span data-stu-id="11203-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="11203-178">De volledige verzameling is vaak de bron, maar een kunt in plaats daarvan een subset van de verzameling opgeven.</span><span class="sxs-lookup"><span data-stu-id="11203-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="11203-179">Een query, zoals `SELECT * FROM Families` geeft aan dat de volledige verzameling worden Families de bron via die u wilt inventariseren.</span><span class="sxs-lookup"><span data-stu-id="11203-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="11203-180">Een speciale ROOT-id kan worden gebruikt voor de verzameling in plaats van met de naam van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="11203-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="11203-181">De volgende lijst bevat de regels die per query worden afgedwongen:</span><span class="sxs-lookup"><span data-stu-id="11203-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="11203-182">De verzameling mag alias hebben, zoals `SELECT f.id FROM Families AS f` of gewoon `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="11203-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="11203-183">Hier `f` is het equivalent van `Families`.</span><span class="sxs-lookup"><span data-stu-id="11203-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="11203-184">`AS`is een optioneel trefwoord tot de alias van de id.</span><span class="sxs-lookup"><span data-stu-id="11203-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="11203-185">Eenmaal alias hebben, de oorspronkelijke bron kan niet worden gebonden.</span><span class="sxs-lookup"><span data-stu-id="11203-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="11203-186">Bijvoorbeeld: `SELECT Families.id FROM Families f` syntaxis is ongeldig omdat de id 'Families' kan niet meer worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="11203-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="11203-187">Alle eigenschappen die moeten worden verwezen moet volledig gekwalificeerd zijn.</span><span class="sxs-lookup"><span data-stu-id="11203-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="11203-188">Dit wordt afgedwongen in het ontbreken van de toepassing van de strikte schema om te voorkomen dat geen bindingen niet eenduidig.</span><span class="sxs-lookup"><span data-stu-id="11203-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="11203-189">Daarom `SELECT id FROM Families f` syntaxis is ongeldig omdat de eigenschap `id` niet is gebonden.</span><span class="sxs-lookup"><span data-stu-id="11203-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="11203-190">Subdocumenten</span><span class="sxs-lookup"><span data-stu-id="11203-190">Subdocuments</span></span>
<span data-ttu-id="11203-191">De bron kan ook worden teruggebracht naar een kleinere subset.</span><span class="sxs-lookup"><span data-stu-id="11203-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="11203-192">Voor het exemplaar voor het inventariseren van alleen een substructuur in elk document kan de subroot dan de bron, zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11203-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="11203-193">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="11203-194">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-194">**Results**</span></span>  

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

<span data-ttu-id="11203-195">Het bovenstaande voorbeeld wordt een matrix als bron gebruikt, een object kan ook worden gebruikt als bron is wat wordt weergegeven in het volgende voorbeeld: een geldige JSON-waarde (geen niet-gedefinieerd) die kan worden gevonden in de bron wordt beschouwd als voor opname in het resultaat van de query.</span><span class="sxs-lookup"><span data-stu-id="11203-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="11203-196">Als sommige families beschikt niet over een `address.state` waarde, in de resultaten worden uitgesloten.</span><span class="sxs-lookup"><span data-stu-id="11203-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="11203-197">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="11203-198">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="11203-199"><a id="WhereClause"></a>WHERE-component</span><span class="sxs-lookup"><span data-stu-id="11203-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="11203-200">De WHERE-component (**`WHERE <filter_condition>`**) is optioneel.</span><span class="sxs-lookup"><span data-stu-id="11203-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="11203-201">Hiermee geeft u de voorwaarden die de JSON-documenten die zijn opgegeven door de bron moet voldoen om te worden opgenomen als onderdeel van het resultaat.</span><span class="sxs-lookup"><span data-stu-id="11203-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="11203-202">De opgegeven voorwaarden op "true" worden beschouwd voor het resultaat moet worden geëvalueerd door elk JSON-document.</span><span class="sxs-lookup"><span data-stu-id="11203-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="11203-203">De WHERE-component wordt gebruikt door de laag index om te bepalen van de absolute kleinste subset van de brondocumenten die deel van het resultaat uitmaken kunnen.</span><span class="sxs-lookup"><span data-stu-id="11203-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="11203-204">De volgende query aanvragen documenten met een eigenschap name waarvan de waarde `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="11203-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="11203-205">Elk document dat u beschikt niet over een eigenschap name of waar de waarde komt niet overeen met `AndersenFamily` is uitgesloten.</span><span class="sxs-lookup"><span data-stu-id="11203-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="11203-206">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="11203-207">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="11203-208">Het vorige voorbeeld blijkt een eenvoudige gelijkheid-query.</span><span class="sxs-lookup"><span data-stu-id="11203-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="11203-209">DocumentDB-API SQL ondersteunt ook een groot aantal scalaire expressies.</span><span class="sxs-lookup"><span data-stu-id="11203-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="11203-210">De meest gebruikte zijn binaire bestanden en unaire expressies.</span><span class="sxs-lookup"><span data-stu-id="11203-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="11203-211">Eigenschap verwijzingen van de bron JSON-object zijn ook geldig expressies.</span><span class="sxs-lookup"><span data-stu-id="11203-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="11203-212">De volgende binaire operators worden momenteel ondersteund en kunnen worden gebruikt in query's, zoals wordt weergegeven in de volgende voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="11203-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="11203-213">Rekenkundige bewerking</span><span class="sxs-lookup"><span data-stu-id="11203-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="11203-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="11203-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="11203-215">Bitsgewijs</span><span class="sxs-lookup"><span data-stu-id="11203-215">Bitwise</span></span></td>    
<td><span data-ttu-id="11203-216">|, &, ^, <<>>,, >>> (nul opvulling rechts verplaatsen)</span><span class="sxs-lookup"><span data-stu-id="11203-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="11203-217">Logische</span><span class="sxs-lookup"><span data-stu-id="11203-217">Logical</span></span></td>
<td><span data-ttu-id="11203-218">EN, OF NIET</span><span class="sxs-lookup"><span data-stu-id="11203-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="11203-219">Vergelijking</span><span class="sxs-lookup"><span data-stu-id="11203-219">Comparison</span></span></td>    
<td><span data-ttu-id="11203-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="11203-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="11203-221">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="11203-221">String</span></span></td>    
<td><span data-ttu-id="11203-222">|| (samenvoegen)</span><span class="sxs-lookup"><span data-stu-id="11203-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="11203-223">We gaan verdiepen in enkele query's met behulp van de binaire operators.</span><span class="sxs-lookup"><span data-stu-id="11203-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="11203-224">De unaire operators +,-, ~ worden ook ondersteund, en niet kan worden gebruikt in query's, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11203-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="11203-225">Naast de binaire bestanden en unaire operators, zijn ook verwijzingen van de eigenschap toegestaan.</span><span class="sxs-lookup"><span data-stu-id="11203-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="11203-226">Bijvoorbeeld: `SELECT * FROM Families f WHERE f.isRegistered` retourneert het JSON-document met de eigenschap `isRegistered` waarvoor de eigenschap waarde gelijk is aan de JSON `true` waarde.</span><span class="sxs-lookup"><span data-stu-id="11203-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="11203-227">Alle overige waarden (false, null, niet-gedefinieerde, `<number>`, `<string>`, `<object>`, `<array>`, enzovoort) leidt tot het brondocument wordt uitgesloten van het resultaat.</span><span class="sxs-lookup"><span data-stu-id="11203-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="11203-228">Gelijkheid en het vergelijkingstype operators</span><span class="sxs-lookup"><span data-stu-id="11203-228">Equality and comparison operators</span></span>
<span data-ttu-id="11203-229">De volgende tabel ziet het resultaat van de gelijkheid vergelijkingen in DocumentDB API SQL tussen twee typen die JSON.</span><span class="sxs-lookup"><span data-stu-id="11203-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="11203-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="11203-231">
            <strong>Niet-gedefinieerd</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="11203-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="11203-233">
            <strong>Booleaanse waarde</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="11203-234">
            <strong>Aantal</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="11203-235">
            <strong>Tekenreeks</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="11203-236">
            <strong>Object</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="11203-237">
            <strong>Matrix</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="11203-238">
            <strong>Niet-gedefinieerd<strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-239">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-240">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-241">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-242">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-243">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-244">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-245">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="11203-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-247">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="11203-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-249">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-250">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-251">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-252">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-253">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="11203-254">
            <strong>Booleaanse waarde<strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-255">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-256">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="11203-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-258">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-259">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-260">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-261">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="11203-262">
            <strong>Aantal<strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-263">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-264">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-265">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="11203-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-267">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-268">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-269">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="11203-270">
            <strong>Tekenreeks<strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-271">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-272">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-273">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-274">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="11203-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-276">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-277">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="11203-278">
            <strong>Object<strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-279">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-280">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-281">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-282">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-283">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="11203-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-285">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="11203-286">
            <strong>Matrix<strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="11203-287">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-288">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-289">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-290">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-291">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="11203-292">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="11203-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="11203-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="11203-294">Voor andere vergelijkingsoperators zoals >, > =,! =, < en < =, de volgende regels toepassen:</span><span class="sxs-lookup"><span data-stu-id="11203-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="11203-295">Vergelijking van verschillende typen resulteert in Undefined.</span><span class="sxs-lookup"><span data-stu-id="11203-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="11203-296">Vergelijking tussen de twee objecten of twee matrices resulteert in een Undefined.</span><span class="sxs-lookup"><span data-stu-id="11203-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="11203-297">Als het resultaat van de scalaire expressie die in het filter is niet gedefinieerd, het bijbehorende document zou niet opgenomen in het resultaat, aangezien Undefined niet logisch neer op 'true'.</span><span class="sxs-lookup"><span data-stu-id="11203-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="11203-298">TUSSEN sleutelwoord</span><span class="sxs-lookup"><span data-stu-id="11203-298">BETWEEN keyword</span></span>
<span data-ttu-id="11203-299">U kunt ook het sleutelwoord BETWEEN op query's op bereiken met waarden zoals in de ANSI SQL express gebruiken.</span><span class="sxs-lookup"><span data-stu-id="11203-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="11203-300">TUSSEN kan worden gebruikt met tekenreeksen of getallen.</span><span class="sxs-lookup"><span data-stu-id="11203-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="11203-301">Deze query retourneert bijvoorbeeld alle familie documenten waarmee het eerste onderliggende klasse tussen de 1-5 (zowel liggen is).</span><span class="sxs-lookup"><span data-stu-id="11203-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="11203-302">In tegenstelling tot in de ANSI-SQL kun je de BETWEEN-component in de component FROM zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="11203-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="11203-303">Houd er rekening mee voor snellere tijden in uitvoering, voor het maken van een indexeringsbeleid die gebruikmaakt van een type bereik index op basis van een numerieke eigenschappen/paden die in de component BETWEEN zijn gefilterd.</span><span class="sxs-lookup"><span data-stu-id="11203-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="11203-304">Het belangrijkste verschil tussen het gebruik van BETWEEN in DocumentDB-API en ANSI SQL is dat u kunt snelle bereik een query uitgevoerd naar eigenschappen van gemengde gegevenstypen: bijvoorbeeld wellicht 'hoogwaardige' is geen getal (5) in een aantal documenten en tekenreeksen in andere gevallen ('grade4').</span><span class="sxs-lookup"><span data-stu-id="11203-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="11203-305">In dergelijke gevallen, wordt zoals in JavaScript, een vergelijking tussen twee verschillende typen resulteert in een 'niet-gedefinieerde' en het document overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="11203-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="11203-306">Logische (AND, OR en NOT) operators</span><span class="sxs-lookup"><span data-stu-id="11203-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="11203-307">Logische operators bewerken Boole-waarden.</span><span class="sxs-lookup"><span data-stu-id="11203-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="11203-308">De logische waarheid tabellen voor deze operators worden weergegeven in de volgende tabellen.</span><span class="sxs-lookup"><span data-stu-id="11203-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="11203-309">OF</span><span class="sxs-lookup"><span data-stu-id="11203-309">OR</span></span> | <span data-ttu-id="11203-310">True</span><span class="sxs-lookup"><span data-stu-id="11203-310">True</span></span> | <span data-ttu-id="11203-311">False</span><span class="sxs-lookup"><span data-stu-id="11203-311">False</span></span> | <span data-ttu-id="11203-312">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="11203-313">True</span><span class="sxs-lookup"><span data-stu-id="11203-313">True</span></span> |<span data-ttu-id="11203-314">True</span><span class="sxs-lookup"><span data-stu-id="11203-314">True</span></span> |<span data-ttu-id="11203-315">True</span><span class="sxs-lookup"><span data-stu-id="11203-315">True</span></span> |<span data-ttu-id="11203-316">True</span><span class="sxs-lookup"><span data-stu-id="11203-316">True</span></span> |
| <span data-ttu-id="11203-317">False</span><span class="sxs-lookup"><span data-stu-id="11203-317">False</span></span> |<span data-ttu-id="11203-318">True</span><span class="sxs-lookup"><span data-stu-id="11203-318">True</span></span> |<span data-ttu-id="11203-319">False</span><span class="sxs-lookup"><span data-stu-id="11203-319">False</span></span> |<span data-ttu-id="11203-320">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-320">Undefined</span></span> |
| <span data-ttu-id="11203-321">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-321">Undefined</span></span> |<span data-ttu-id="11203-322">True</span><span class="sxs-lookup"><span data-stu-id="11203-322">True</span></span> |<span data-ttu-id="11203-323">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-323">Undefined</span></span> |<span data-ttu-id="11203-324">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-324">Undefined</span></span> |

| <span data-ttu-id="11203-325">EN</span><span class="sxs-lookup"><span data-stu-id="11203-325">AND</span></span> | <span data-ttu-id="11203-326">True</span><span class="sxs-lookup"><span data-stu-id="11203-326">True</span></span> | <span data-ttu-id="11203-327">False</span><span class="sxs-lookup"><span data-stu-id="11203-327">False</span></span> | <span data-ttu-id="11203-328">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="11203-329">True</span><span class="sxs-lookup"><span data-stu-id="11203-329">True</span></span> |<span data-ttu-id="11203-330">True</span><span class="sxs-lookup"><span data-stu-id="11203-330">True</span></span> |<span data-ttu-id="11203-331">False</span><span class="sxs-lookup"><span data-stu-id="11203-331">False</span></span> |<span data-ttu-id="11203-332">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-332">Undefined</span></span> |
| <span data-ttu-id="11203-333">False</span><span class="sxs-lookup"><span data-stu-id="11203-333">False</span></span> |<span data-ttu-id="11203-334">False</span><span class="sxs-lookup"><span data-stu-id="11203-334">False</span></span> |<span data-ttu-id="11203-335">False</span><span class="sxs-lookup"><span data-stu-id="11203-335">False</span></span> |<span data-ttu-id="11203-336">False</span><span class="sxs-lookup"><span data-stu-id="11203-336">False</span></span> |
| <span data-ttu-id="11203-337">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-337">Undefined</span></span> |<span data-ttu-id="11203-338">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-338">Undefined</span></span> |<span data-ttu-id="11203-339">False</span><span class="sxs-lookup"><span data-stu-id="11203-339">False</span></span> |<span data-ttu-id="11203-340">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-340">Undefined</span></span> |

| <span data-ttu-id="11203-341">NIET</span><span class="sxs-lookup"><span data-stu-id="11203-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="11203-342">True</span><span class="sxs-lookup"><span data-stu-id="11203-342">True</span></span> |<span data-ttu-id="11203-343">False</span><span class="sxs-lookup"><span data-stu-id="11203-343">False</span></span> |
| <span data-ttu-id="11203-344">False</span><span class="sxs-lookup"><span data-stu-id="11203-344">False</span></span> |<span data-ttu-id="11203-345">True</span><span class="sxs-lookup"><span data-stu-id="11203-345">True</span></span> |
| <span data-ttu-id="11203-346">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-346">Undefined</span></span> |<span data-ttu-id="11203-347">Niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="11203-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="11203-348">TREFWOORD</span><span class="sxs-lookup"><span data-stu-id="11203-348">IN keyword</span></span>
<span data-ttu-id="11203-349">Het sleutelwoord kan worden gebruikt om te controleren of een opgegeven waarde komt overeen met elke waarde in een lijst.</span><span class="sxs-lookup"><span data-stu-id="11203-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="11203-350">Deze query retourneert bijvoorbeeld alle familie documenten waar de id van 'WakefieldFamily' of 'AndersenFamily' is.</span><span class="sxs-lookup"><span data-stu-id="11203-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="11203-351">In dit voorbeeld retourneert alle documenten waarin de status is een van de opgegeven waarden.</span><span class="sxs-lookup"><span data-stu-id="11203-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="11203-352">Ternair (?) en operators Coalesce (?)</span><span class="sxs-lookup"><span data-stu-id="11203-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="11203-353">De operators Ternair en Coalesce kunnen worden gebruikt voor het bouwen van voorwaardelijke expressies, vergelijkbaar met populaire programmeertalen, zoals C# en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="11203-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="11203-354">De operator Ternair (?) is heel handig bij het maken van nieuwe JSON-eigenschappen op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="11203-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="11203-355">Bijvoorbeeld, kunt nu u query's voor het classificeren van het niveau van de klasse in een menselijke leesbare vorm zoals beginnende/tussenliggende/Geavanceerd zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="11203-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="11203-356">U kunt ook het aanroepen van de operator zoals in de onderstaande query nesten.</span><span class="sxs-lookup"><span data-stu-id="11203-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="11203-357">Als met andere operators query als de eigenschappen waarnaar wordt verwezen in de conditionele expressie ontbreken in elk document of als de typen worden vergeleken verschillen, vervolgens die documenten worden niet opgenomen in de queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="11203-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="11203-358">De operator Coalesce (?) kan worden gebruikt voor het efficiënt controleren op de aanwezigheid van een eigenschap (ook</span><span class="sxs-lookup"><span data-stu-id="11203-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="11203-359">is gedefinieerd) in een document.</span><span class="sxs-lookup"><span data-stu-id="11203-359">is defined) in a document.</span></span> <span data-ttu-id="11203-360">Dit is handig wanneer een query op semi-gestructureerde of gegevens van gemengde typen.</span><span class="sxs-lookup"><span data-stu-id="11203-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="11203-361">Bijvoorbeeld, retourneert deze query 'Achternaam' indien aanwezig, of de 'Achternaam' als dit niet aanwezig.</span><span class="sxs-lookup"><span data-stu-id="11203-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="11203-362"><a id="EscapingReservedKeywords"></a>Tussen aanhalingstekens eigenschapsaccessor</span><span class="sxs-lookup"><span data-stu-id="11203-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="11203-363">U kunt ook toegang tot eigenschappen met behulp van de operator tussen aanhalingstekens eigenschap `[]`.</span><span class="sxs-lookup"><span data-stu-id="11203-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="11203-364">Bijvoorbeeld: `SELECT c.grade` en `SELECT c["grade"]` equivalent zijn.</span><span class="sxs-lookup"><span data-stu-id="11203-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="11203-365">Deze syntaxis is handig wanneer u een eigenschap die spaties, speciale tekens bevat, of er gebeurt moet met dezelfde naam als een SQL-sleutelwoord of een gereserveerd woord escape.</span><span class="sxs-lookup"><span data-stu-id="11203-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="11203-366"><a id="SelectClause"></a>SELECT-component</span><span class="sxs-lookup"><span data-stu-id="11203-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="11203-367">De component SELECT (**`SELECT <select_list>`**) is verplicht en Hiermee geeft u de waarden die worden opgehaald uit de query, net zoals in ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="11203-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="11203-368">De subset die boven op de brondocumenten zijn gefilterd op de Projectiefase, waarbij de opgegeven JSON-waarden worden opgehaald en een nieuwe JSON-object is samengesteld, voor elke doorgegeven op deze invoer worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="11203-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="11203-369">Het volgende voorbeeld toont een typische SELECT-query.</span><span class="sxs-lookup"><span data-stu-id="11203-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="11203-370">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="11203-371">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="11203-372">Geneste eigenschappen</span><span class="sxs-lookup"><span data-stu-id="11203-372">Nested properties</span></span>
<span data-ttu-id="11203-373">In het volgende voorbeeld we twee geneste eigenschappen projecteert `f.address.state` en `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="11203-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="11203-374">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="11203-375">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="11203-376">Projectie biedt ook ondersteuning voor JSON-expressies, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11203-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="11203-377">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="11203-378">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="11203-379">Bekijk de rol van `$1` hier.</span><span class="sxs-lookup"><span data-stu-id="11203-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="11203-380">De `SELECT` component moet een JSON-object maken en omdat er geen sleutel is opgegeven, gebruiken we de impliciete argument variabele namen die beginnen met `$1`.</span><span class="sxs-lookup"><span data-stu-id="11203-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="11203-381">Deze query retourneert bijvoorbeeld twee impliciete argumentvariabelen, met het label `$1` en `$2`.</span><span class="sxs-lookup"><span data-stu-id="11203-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="11203-382">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="11203-383">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="11203-384">Aliasing</span><span class="sxs-lookup"><span data-stu-id="11203-384">Aliasing</span></span>
<span data-ttu-id="11203-385">Nu gaan we het bovenstaande voorbeeld expliciete aliasing waarden uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="11203-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="11203-386">Het sleutelwoord gebruikt voor aliasing is.</span><span class="sxs-lookup"><span data-stu-id="11203-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="11203-387">Dit is optioneel, zoals wordt weergegeven tijdens het projecteren van de tweede waarde als `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="11203-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="11203-388">Als een query twee eigenschappen met dezelfde naam heeft, moet aliasing om de naam van een of beide van de eigenschappen, zodat ze ondubbelzinnig zijn gemaakt in het verwachte resultaat te worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="11203-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="11203-389">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="11203-390">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="11203-391">Scalaire expressies</span><span class="sxs-lookup"><span data-stu-id="11203-391">Scalar expressions</span></span>
<span data-ttu-id="11203-392">Naast de verwijzingen van de eigenschap ondersteunt de component SELECT ook scalaire expressies zoals constanten, aritmetische expressies, logische expressies, enzovoort. Hier is bijvoorbeeld een eenvoudige 'Hallo wereld'-query.</span><span class="sxs-lookup"><span data-stu-id="11203-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="11203-393">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="11203-394">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="11203-395">Hier volgt een voorbeeld van een complexere die gebruikmaakt van een scalaire expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="11203-396">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="11203-397">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="11203-398">In het volgende voorbeeld is het resultaat van de scalaire expressie die een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="11203-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="11203-399">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="11203-400">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="11203-401">Maken van het object en array</span><span class="sxs-lookup"><span data-stu-id="11203-401">Object and array creation</span></span>
<span data-ttu-id="11203-402">Een andere belangrijke functie van DocumentDB API SQL is array-object maken.</span><span class="sxs-lookup"><span data-stu-id="11203-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="11203-403">In het vorige voorbeeld, houd er rekening mee dat er een nieuwe JSON-object gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11203-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="11203-404">Op deze manier kan een ook matrices samenstellen zoals weergegeven in de volgende voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="11203-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="11203-405">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="11203-406">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-406">**Results**</span></span>  

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

### <span data-ttu-id="11203-407"><a id="ValueKeyword"></a>WAARDE sleutelwoord</span><span class="sxs-lookup"><span data-stu-id="11203-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="11203-408">De **waarde** sleutelwoord biedt een manier om JSON-waarde te retourneren.</span><span class="sxs-lookup"><span data-stu-id="11203-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="11203-409">De onderstaande query retourneert bijvoorbeeld scalaire `"Hello World"` in plaats van `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="11203-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="11203-410">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="11203-411">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="11203-412">De volgende query retourneert de waarde van de JSON zonder de `"address"` label in de resultaten.</span><span class="sxs-lookup"><span data-stu-id="11203-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="11203-413">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="11203-414">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-414">**Results**</span></span>  

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

<span data-ttu-id="11203-415">Het volgende voorbeeld breidt deze optie als u wilt laten zien hoe u JSON primitieve waarden (het knooppuntniveau van de JSON-structuur) retourneren.</span><span class="sxs-lookup"><span data-stu-id="11203-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="11203-416">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="11203-417">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="11203-418">* Operator</span><span class="sxs-lookup"><span data-stu-id="11203-418">* Operator</span></span>
<span data-ttu-id="11203-419">De speciale operator (*) wordt ondersteund voor het document als project-is.</span><span class="sxs-lookup"><span data-stu-id="11203-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="11203-420">Wanneer gebruikt, moet dit het enige verwachte veld.</span><span class="sxs-lookup"><span data-stu-id="11203-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="11203-421">Terwijl een query zoals `SELECT * FROM Families f` geldig is, `SELECT VALUE * FROM Families f ` en `SELECT *, f.id FROM Families f ` zijn niet geldig.</span><span class="sxs-lookup"><span data-stu-id="11203-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="11203-422">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="11203-423">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-423">**Results**</span></span>

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

### <span data-ttu-id="11203-424"><a id="TopKeyword"></a>Operator TOP</span><span class="sxs-lookup"><span data-stu-id="11203-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="11203-425">Het sleutelwoord TOP kan worden gebruikt om te beperken het aantal waarden van een query.</span><span class="sxs-lookup"><span data-stu-id="11203-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="11203-426">Als eerste wordt gebruikt in combinatie met de component ORDER BY, is de resultatenset beperkt tot de eerste N aantal geordende waarden; anders wordt het eerste N aantal resultaten in een niet-gedefinieerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="11203-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="11203-427">Als een best practice in een instructie SELECT gebruik altijd een component ORDER BY met de TOP-component.</span><span class="sxs-lookup"><span data-stu-id="11203-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="11203-428">Dit is de enige manier om voorspelbare aangeven welke rijen zijn beïnvloed door boven.</span><span class="sxs-lookup"><span data-stu-id="11203-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="11203-429">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="11203-430">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-430">**Results**</span></span>

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

<span data-ttu-id="11203-431">TOP kan worden gebruikt met een constante waarde (zoals hierboven) of met de waarde van een variabele query's met parameters.</span><span class="sxs-lookup"><span data-stu-id="11203-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="11203-432">Zie geparameteriseerde query's hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="11203-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="11203-433"><a id="Aggregates"></a>Statistische functies</span><span class="sxs-lookup"><span data-stu-id="11203-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="11203-434">U kunt ook uitvoeren aggregaties in de `SELECT` component.</span><span class="sxs-lookup"><span data-stu-id="11203-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="11203-435">Statistische functies uitvoeren van een berekening op een set waarden en één waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="11203-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="11203-436">Bijvoorbeeld retourneert de volgende query de telling van familie documenten binnen de verzameling.</span><span class="sxs-lookup"><span data-stu-id="11203-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="11203-437">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="11203-438">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="11203-439">U kunt ook de scalaire waarde van de statistische functie retourneren met behulp van de `VALUE` sleutelwoord.</span><span class="sxs-lookup"><span data-stu-id="11203-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="11203-440">De volgende query retourneert bijvoorbeeld het aantal waarden als een enkel getal:</span><span class="sxs-lookup"><span data-stu-id="11203-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="11203-441">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="11203-442">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="11203-443">U kunt ook statistische functies uitvoeren in combinatie met filters.</span><span class="sxs-lookup"><span data-stu-id="11203-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="11203-444">De volgende query retourneert bijvoorbeeld het aantal documenten met het adres in de staat Washington.</span><span class="sxs-lookup"><span data-stu-id="11203-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="11203-445">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="11203-446">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="11203-447">De volgende tabel bevat de lijst met ondersteunde statistische functies in DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="11203-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="11203-448">`SUM`en `AVG` via numerieke waarden worden uitgevoerd terwijl `COUNT`, `MIN`, en `MAX` via getallen, tekenreeksen, Booleaanse waarden en null-waarden kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11203-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="11203-449">Gebruik</span><span class="sxs-lookup"><span data-stu-id="11203-449">Usage</span></span> | <span data-ttu-id="11203-450">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="11203-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="11203-451">AANTAL</span><span class="sxs-lookup"><span data-stu-id="11203-451">COUNT</span></span> | <span data-ttu-id="11203-452">Retourneert het aantal items in de expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="11203-453">SOM</span><span class="sxs-lookup"><span data-stu-id="11203-453">SUM</span></span>   | <span data-ttu-id="11203-454">Retourneert de som van alle waarden in de expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="11203-455">MIN</span><span class="sxs-lookup"><span data-stu-id="11203-455">MIN</span></span>   | <span data-ttu-id="11203-456">Retourneert de minimale waarde in de expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="11203-457">MAXIMUM AANTAL</span><span class="sxs-lookup"><span data-stu-id="11203-457">MAX</span></span>   | <span data-ttu-id="11203-458">Retourneert de maximumwaarde in de expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="11203-459">GEM.</span><span class="sxs-lookup"><span data-stu-id="11203-459">AVG</span></span>   | <span data-ttu-id="11203-460">Retourneert het gemiddelde van de waarden in de expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="11203-461">Statistische functies kunnen ook worden uitgevoerd via de resultaten van een matrix herhaling.</span><span class="sxs-lookup"><span data-stu-id="11203-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="11203-462">Zie voor meer informatie [herhaling van de matrix in query's](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="11203-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="11203-463">Wanneer u de Azure portal Queryverkenner, houd er rekening mee dat aggregatie van query's kunnen het resultaat gedeeltelijk geaggregeerde via een querypagina.</span><span class="sxs-lookup"><span data-stu-id="11203-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="11203-464">De SDK's produceert één cumulatieve waarde op alle pagina's.</span><span class="sxs-lookup"><span data-stu-id="11203-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="11203-465">Als u wilt uitvoeren met code aggregatie-query's, moet u de .NET SDK 1.12.0, .NET Core SDK 1.1.0 of Java SDK 1.9.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="11203-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="11203-466"><a id="OrderByClause"></a>ORDER BY-component</span><span class="sxs-lookup"><span data-stu-id="11203-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="11203-467">Zoals in de ANSI-SQL, u een optionele component Order By tijdens het opvragen opnemen kunt.</span><span class="sxs-lookup"><span data-stu-id="11203-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="11203-468">De component kan bevatten een optioneel argument ASC/DESC de volgorde waarin de resultaten moeten worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="11203-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="11203-469">Hier is bijvoorbeeld een query waarmee families in volgorde van de residente plaatsnaam opgehaald.</span><span class="sxs-lookup"><span data-stu-id="11203-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="11203-470">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="11203-471">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-471">**Results**</span></span>

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

<span data-ttu-id="11203-472">En een query waarmee opgehaald families in volgorde van de aanmaakdatum, die wordt opgeslagen als een getal dat de epoche tijd, Internet Explorer, verstreken tijd sinds 1 januari 1970 in seconden voor hier.</span><span class="sxs-lookup"><span data-stu-id="11203-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="11203-473">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="11203-474">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-474">**Results**</span></span>

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

## <span data-ttu-id="11203-475"><a id="Advanced"></a>Concepten van geavanceerde database en SQL-query 's</span><span class="sxs-lookup"><span data-stu-id="11203-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="11203-476"><a id="Iteration"></a>Herhaling</span><span class="sxs-lookup"><span data-stu-id="11203-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="11203-477">Een nieuwe constructie is toegevoegd de **IN** -sleutelwoord in DocumentDB API SQL ter ondersteuning van iteratie van JSON-matrices.</span><span class="sxs-lookup"><span data-stu-id="11203-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="11203-478">De FROM-bron biedt ondersteuning voor herhaling.</span><span class="sxs-lookup"><span data-stu-id="11203-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="11203-479">Laten we beginnen met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11203-479">Let's start with the following example:</span></span>

<span data-ttu-id="11203-480">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="11203-481">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-481">**Results**</span></span>  

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

<span data-ttu-id="11203-482">Nu we bekijken een andere query die herhaling via onderliggende elementen in de verzameling uitvoert.</span><span class="sxs-lookup"><span data-stu-id="11203-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="11203-483">Noteer het verschil in de uitvoermatrix.</span><span class="sxs-lookup"><span data-stu-id="11203-483">Note the difference in the output array.</span></span> <span data-ttu-id="11203-484">In dit voorbeeld wordt gesplitst `children` en worden de resultaten samengevoegd in één array.</span><span class="sxs-lookup"><span data-stu-id="11203-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="11203-485">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="11203-486">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-486">**Results**</span></span>  

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

<span data-ttu-id="11203-487">Dit kan verder worden gebruikt om te filteren op elke afzonderlijke vermelding van de matrix, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11203-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="11203-488">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="11203-489">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="11203-490">U kunt ook aggregatie uitvoeren via het resultaat van de matrix herhaling.</span><span class="sxs-lookup"><span data-stu-id="11203-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="11203-491">Bijvoorbeeld telt de volgende query het aantal onderliggende items onder alle families.</span><span class="sxs-lookup"><span data-stu-id="11203-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="11203-492">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="11203-493">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="11203-494"><a id="Joins"></a>Joins</span><span class="sxs-lookup"><span data-stu-id="11203-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="11203-495">In een relationele database is de noodzaak om toe te voegen tussen de tabellen belangrijk.</span><span class="sxs-lookup"><span data-stu-id="11203-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="11203-496">Het is het gevolg van logische ontwerpen genormaliseerde schema's.</span><span class="sxs-lookup"><span data-stu-id="11203-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="11203-497">In tegenstelling tot dit omgaat DocumentDB API met het gedenormaliseerd gegevensmodel zonder schema documenten.</span><span class="sxs-lookup"><span data-stu-id="11203-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="11203-498">Dit is het logische equivalent van een 'self-join'.</span><span class="sxs-lookup"><span data-stu-id="11203-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="11203-499">De syntaxis die ondersteuning biedt voor de taal is < from_source1 > JOIN < from_source2 > JOIN... JOIN < from_sourceN >.</span><span class="sxs-lookup"><span data-stu-id="11203-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="11203-500">Over het algemeen dit retourneert een reeks **N**- tuples (tuple met **N** waarden).</span><span class="sxs-lookup"><span data-stu-id="11203-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="11203-501">Elke tuple heeft geproduceerd door alle verzameling aliassen iteratie van hun respectieve sets waarden.</span><span class="sxs-lookup"><span data-stu-id="11203-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="11203-502">Dit is met andere woorden, een volledige vectorproduct van de sets die deel uitmaken van de join.</span><span class="sxs-lookup"><span data-stu-id="11203-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="11203-503">De volgende voorbeelden ziet de werking van de JOIN-component.</span><span class="sxs-lookup"><span data-stu-id="11203-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="11203-504">In het volgende voorbeeld wordt het resultaat is leeg omdat het vectorproduct van elk document van de bron en een lege set is leeg.</span><span class="sxs-lookup"><span data-stu-id="11203-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="11203-505">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="11203-506">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="11203-507">In het volgende voorbeeld wordt de join is tussen de hoofdmap van het document en de `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="11203-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="11203-508">Het is een vectorproduct tussen twee JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="11203-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="11203-509">Het feit dat onderliggende elementen is een matrix is niet effectief in de JOIN omdat we werkt met een enkele basis die de onderliggende matrix is.</span><span class="sxs-lookup"><span data-stu-id="11203-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="11203-510">Het resultaat bevat daarom slechts twee resultaten, omdat het vectorproduct van elk document met de matrix exact slechts één document geeft.</span><span class="sxs-lookup"><span data-stu-id="11203-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="11203-511">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="11203-512">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="11203-513">Het volgende voorbeeld ziet u een meer conventionele join:</span><span class="sxs-lookup"><span data-stu-id="11203-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="11203-514">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="11203-515">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-515">**Results**</span></span>

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



<span data-ttu-id="11203-516">Het eerste dat te weten is dat de `from_source` van de **JOIN** component is een iterator.</span><span class="sxs-lookup"><span data-stu-id="11203-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="11203-517">Ja, de stroom in dit geval is als volgt:</span><span class="sxs-lookup"><span data-stu-id="11203-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="11203-518">Vouw van elk onderliggend element **c** in de matrix.</span><span class="sxs-lookup"><span data-stu-id="11203-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="11203-519">Toepassen van een vectorproduct met de hoofdmap van het document **f** met elk onderliggend element **c** dat is samengevoegd in de eerste stap.</span><span class="sxs-lookup"><span data-stu-id="11203-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="11203-520">Ten slotte het hoofdobject project **f** naameigenschap alleen.</span><span class="sxs-lookup"><span data-stu-id="11203-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="11203-521">Het eerste document (`AndersenFamily`) bevat slechts één onderliggend element, zodat de resultatenset bevat slechts één object hoort bij dit document.</span><span class="sxs-lookup"><span data-stu-id="11203-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="11203-522">Het tweede document (`WakefieldFamily`) twee onderliggende items bevat.</span><span class="sxs-lookup"><span data-stu-id="11203-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="11203-523">Het vectorproduct produceert dus een afzonderlijke object voor elke onderliggende, waardoor wat resulteert in twee objecten, één voor elke onderliggende overeenkomt met dit document.</span><span class="sxs-lookup"><span data-stu-id="11203-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="11203-524">De basis-velden in beide deze documenten zijn hetzelfde, net zoals u in een vectorproduct verwacht.</span><span class="sxs-lookup"><span data-stu-id="11203-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="11203-525">Het echte hulpprogramma van de JOIN is van het vectorproduct in een shape die anders moeilijk te project naar formulier tuples.</span><span class="sxs-lookup"><span data-stu-id="11203-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="11203-526">Bovendien ziet u in het onderstaande voorbeeld kon u filteren op de combinatie van een tuple dat kiest, kunnen de gebruiker heeft ervoor gekozen een voorwaarde voldaan door de tuples algemene.</span><span class="sxs-lookup"><span data-stu-id="11203-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="11203-527">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="11203-528">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-528">**Results**</span></span>

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



<span data-ttu-id="11203-529">In dit voorbeeld is een natuurlijke extensie van het vorige voorbeeld en voert een dubbele koppeling.</span><span class="sxs-lookup"><span data-stu-id="11203-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="11203-530">Het vectorproduct kan dus worden weergegeven als de volgende pseudo code:</span><span class="sxs-lookup"><span data-stu-id="11203-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

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

<span data-ttu-id="11203-531">`AndersenFamily`heeft één onderliggende die één huisdier heeft.</span><span class="sxs-lookup"><span data-stu-id="11203-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="11203-532">Dus het vectorproduct resulteert in een rij is (1\*1\*1) van deze reeks.</span><span class="sxs-lookup"><span data-stu-id="11203-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="11203-533">WakefieldFamily echter twee onderliggende items heeft, maar slechts één onderliggende 'Jesse' huisdieren heeft.</span><span class="sxs-lookup"><span data-stu-id="11203-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="11203-534">Jesse heeft echter twee huisdieren.</span><span class="sxs-lookup"><span data-stu-id="11203-534">Jesse has two pets though.</span></span> <span data-ttu-id="11203-535">Daarom het vectorproduct 1 levert\*1\*2 = 2 rijen uit deze reeks.</span><span class="sxs-lookup"><span data-stu-id="11203-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="11203-536">In het volgende voorbeeld, er is een extra filter op `pet`.</span><span class="sxs-lookup"><span data-stu-id="11203-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="11203-537">Dit omvat niet alle tuples waar de pet-naam geen is 'Schaduwkopie'.</span><span class="sxs-lookup"><span data-stu-id="11203-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="11203-538">U ziet dat we kunnen bouwen tuples uit matrices, filter op een van de elementen van de tuple en een combinatie van de elementen project.</span><span class="sxs-lookup"><span data-stu-id="11203-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="11203-539">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="11203-540">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="11203-541"><a id="JavaScriptIntegration"></a>Integratie van JavaScript</span><span class="sxs-lookup"><span data-stu-id="11203-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="11203-542">Azure Cosmos DB biedt een programmeermodel voor het uitvoeren op basis van JavaScript-toepassingslogica rechtstreeks op de verzamelingen in termen van opgeslagen procedures en triggers.</span><span class="sxs-lookup"><span data-stu-id="11203-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="11203-543">Hiermee kunt u beide:</span><span class="sxs-lookup"><span data-stu-id="11203-543">This allows for both:</span></span>

* <span data-ttu-id="11203-544">Mogelijkheid tot high-performance transactionele CRUD-bewerkingen en een query uitgevoerd naar documenten in een verzameling doordat de diepe integratie van JavaScript-runtime rechtstreeks in de database-engine.</span><span class="sxs-lookup"><span data-stu-id="11203-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="11203-545">Een natuurlijke modellering van Controlestroom, variabele scopes en -toewijzing en integratie van primitieven met databasetransacties afhandeling van uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="11203-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="11203-546">Raadpleeg de JavaScript-serverzijde programmeerbaarheid-documentatie voor meer informatie over Azure DB die Cosmos-ondersteuning voor integratie van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="11203-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="11203-547"><a id="UserDefinedFunctions"></a>Gebruiker gedefinieerde functies (UDF's)</span><span class="sxs-lookup"><span data-stu-id="11203-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="11203-548">Samen met de typen die al is gedefinieerd in dit artikel biedt DocumentDB API SQL ondersteuning voor gebruiker gedefinieerde functies (UDF).</span><span class="sxs-lookup"><span data-stu-id="11203-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="11203-549">In het bijzonder wordt scalaire UDF's waar de ontwikkelaars kunnen doorgeven in nul of meerdere argumenten en terug één argument resultaat geretourneerd ondersteund.</span><span class="sxs-lookup"><span data-stu-id="11203-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="11203-550">Elk van deze argumenten wordt voor geldige JSON-waarden worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="11203-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="11203-551">De DocumentDB API SQL-syntaxis wordt uitgebreid ter ondersteuning van aangepaste toepassingslogica gebruik van deze door de gebruiker gedefinieerde functies.</span><span class="sxs-lookup"><span data-stu-id="11203-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="11203-552">UDF's kunnen worden geregistreerd met DocumentDB-API en vervolgens naar worden verwezen als onderdeel van een SQL-query.</span><span class="sxs-lookup"><span data-stu-id="11203-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="11203-553">De UDF's zijn in feite exquisitely ontworpen om te worden aangeroepen door query's.</span><span class="sxs-lookup"><span data-stu-id="11203-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="11203-554">Als gevolg van deze keuze hebt UDF's geen toegang tot het contextobject met de andere JavaScript typen (opgeslagen procedures en triggers).</span><span class="sxs-lookup"><span data-stu-id="11203-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="11203-555">Omdat de query's worden uitgevoerd als alleen-lezen, kunnen ze worden uitgevoerd op de primaire of op secundaire replica's.</span><span class="sxs-lookup"><span data-stu-id="11203-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="11203-556">Daarom zijn UDF's ontworpen om uit te voeren op secundaire replica's in tegenstelling tot andere typen JavaScript.</span><span class="sxs-lookup"><span data-stu-id="11203-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="11203-557">Hieronder volgt een voorbeeld van hoe een UDF kan worden geregistreerd bij de database Cosmos DB specifiek onder een documentverzameling.</span><span class="sxs-lookup"><span data-stu-id="11203-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="11203-558">Het voorgaande voorbeeld maakt een UDF met de naam `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="11203-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="11203-559">Deze twee waarden voor JSON-tekenreeks accepteert `input` en `pattern` en controleert of het eerste overeenkomt met het patroon die zijn opgegeven in de tweede van JavaScript string.match() functie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="11203-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="11203-560">We kunnen deze UDF nu gebruiken in een query in een projectie.</span><span class="sxs-lookup"><span data-stu-id="11203-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="11203-561">UDF's moeten worden gekwalificeerd met de hoofdlettergevoelige voorvoegsel "udf."</span><span class="sxs-lookup"><span data-stu-id="11203-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="11203-562">Wanneer aangeroepen vanuit query's.</span><span class="sxs-lookup"><span data-stu-id="11203-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="11203-563">Voorafgaand aan 3-17-2015 ondersteund Cosmos DB UDF aanroepen zonder de 'udf."</span><span class="sxs-lookup"><span data-stu-id="11203-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="11203-564">voorvoegsel zoals REGEX_MATCH() selecteren.</span><span class="sxs-lookup"><span data-stu-id="11203-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="11203-565">Dit patroon van aanroepen is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="11203-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="11203-566">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="11203-567">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="11203-568">De UDF kan ook worden gebruikt in een filter, zoals wordt weergegeven in het onderstaande voorbeeld ook gekwalificeerd met de 'udf."</span><span class="sxs-lookup"><span data-stu-id="11203-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="11203-569">voorvoegsel:</span><span class="sxs-lookup"><span data-stu-id="11203-569">prefix:</span></span>

<span data-ttu-id="11203-570">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="11203-571">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="11203-572">In principe UDF's geldig scalaire expressies zijn en kunnen worden gebruikt in projecties en filters.</span><span class="sxs-lookup"><span data-stu-id="11203-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="11203-573">Als op de kracht van UDF's wilt uitbreiden, bekijken we een ander voorbeeld met voorwaardelijke logica:</span><span class="sxs-lookup"><span data-stu-id="11203-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="11203-574">Hieronder volgt een voorbeeld waarin de UDF oefeningen.</span><span class="sxs-lookup"><span data-stu-id="11203-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="11203-575">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="11203-576">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-576">**Results**</span></span>

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


<span data-ttu-id="11203-577">Als de voorgaande voorbeelden presenteren, UDF's de kracht van JavaScript-taal geïntegreerd met de API DocumentDB SQL biedt een uitgebreide programmeerbare interface hiervoor complexe procedurele, heeft voorwaardelijke logica met behulp van de ingebouwde mogelijkheden voor JavaScript-runtime.</span><span class="sxs-lookup"><span data-stu-id="11203-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="11203-578">DocumentDB-API SQL biedt de argumenten voor de UDF's voor elk document in de bron in het huidige stadium (WHERE-component of SELECT-component) van de verwerking van de UDF.</span><span class="sxs-lookup"><span data-stu-id="11203-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="11203-579">Het resultaat is opgenomen in de algehele pijplijn naadloos.</span><span class="sxs-lookup"><span data-stu-id="11203-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="11203-580">Als de eigenschappen waarnaar wordt verwezen door de UDF parameters zijn niet beschikbaar in de JSON-waarde, de parameter wordt beschouwd als niet-gedefinieerde en daarom de UDF-aanroep voor het volledig is overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="11203-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="11203-581">Op dezelfde manier als het resultaat van de UDF gedefinieerd is, het niet opgenomen in het resultaat.</span><span class="sxs-lookup"><span data-stu-id="11203-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="11203-582">Kortom zijn UDF's geweldige tools complexe bedrijfslogica doen als onderdeel van de query.</span><span class="sxs-lookup"><span data-stu-id="11203-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="11203-583">Evaluatie van operator</span><span class="sxs-lookup"><span data-stu-id="11203-583">Operator evaluation</span></span>
<span data-ttu-id="11203-584">Cosmos DB, tekent werkt hetzelfde als met JavaScript-operators en de evaluatie-semantiek ingevolge is een JSON-database.</span><span class="sxs-lookup"><span data-stu-id="11203-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="11203-585">Terwijl Cosmos DB probeert te behouden JavaScript-semantiek in termen van JSON-ondersteuning, wordt de evaluatie van de bewerking in sommige gevallen afwijkt.</span><span class="sxs-lookup"><span data-stu-id="11203-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="11203-586">In DocumentDB API SQL, zijn in tegenstelling tot in traditionele SQL de typen van waarden vaak niet bekend totdat de waarden uit de database zijn opgehaald.</span><span class="sxs-lookup"><span data-stu-id="11203-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="11203-587">Om efficiënt query's worden uitgevoerd, wordt in de meeste van de operators strikt type vereisten hebben.</span><span class="sxs-lookup"><span data-stu-id="11203-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="11203-588">DocumentDB-API SQL biedt geen impliciete conversies, in tegenstelling tot JavaScript uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="11203-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="11203-589">Een query voor het exemplaar, zoals `SELECT * FROM Person p WHERE p.Age = 21` overeenkomt met de documenten met een eigenschap Age waarvan de waarde 21 is.</span><span class="sxs-lookup"><span data-stu-id="11203-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="11203-590">Een ander document waarvan de eigenschap leeftijd overeenkomt met de tekenreeks '21' of andere mogelijk oneindige variaties, zoals '021', '21,0', '0021', '00021', enzovoort worden niet overeen.</span><span class="sxs-lookup"><span data-stu-id="11203-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="11203-591">Zo wordt daarentegen JavaScript waar de tekenreekswaarden impliciet omgezet naar het getallen worden (op basis van de operator ex: ==).</span><span class="sxs-lookup"><span data-stu-id="11203-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="11203-592">Deze keuze is van cruciaal belang voor efficiënte index zoeken in DocumentDB API SQL.</span><span class="sxs-lookup"><span data-stu-id="11203-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="11203-593">SQL-query's met parameters</span><span class="sxs-lookup"><span data-stu-id="11203-593">Parameterized SQL queries</span></span>
<span data-ttu-id="11203-594">Cosmos DB ondersteunt query's met parameters worden uitgedrukt met de vertrouwde @ notatie.</span><span class="sxs-lookup"><span data-stu-id="11203-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="11203-595">Geparameteriseerde SQL biedt robuuste verwerken en de aanhalingstekens van gebruikersinvoer, onbedoeld blootstelling van gegevens via SQL-injectie voorkomen.</span><span class="sxs-lookup"><span data-stu-id="11203-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="11203-596">U kunt bijvoorbeeld een query schrijven waarmee achternaam en status van adres als parameters neemt en vervolgens uitgevoerd voor verschillende waarden van de laatste naam en adres staat op basis van de invoer van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="11203-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="11203-597">Deze aanvraag kan vervolgens worden verzonden aan de Cosmos-database als een JSON-query met parameters zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="11203-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="11203-598">Het argument voor TOP kan worden ingesteld met query's met parameters, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="11203-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="11203-599">Parameterwaarden mag geldige JSON (tekenreeksen, cijfers, Booleaanse waarden, null, zelfs als deze matrices of geneste JSON).</span><span class="sxs-lookup"><span data-stu-id="11203-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="11203-600">Ook omdat Cosmos DB schema minder, zijn parameters niet gevalideerd met elk type.</span><span class="sxs-lookup"><span data-stu-id="11203-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="11203-601"><a id="BuiltinFunctions"></a>Ingebouwde functies</span><span class="sxs-lookup"><span data-stu-id="11203-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="11203-602">Cosmos DB ondersteunt ook een aantal ingebouwde functies voor algemene bewerkingen, die kunnen worden gebruikt in query's als de gebruiker gedefinieerde functies (UDF's).</span><span class="sxs-lookup"><span data-stu-id="11203-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="11203-603">Functie-groep</span><span class="sxs-lookup"><span data-stu-id="11203-603">Function group</span></span>          | <span data-ttu-id="11203-604">Bewerkingen</span><span class="sxs-lookup"><span data-stu-id="11203-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="11203-605">Wiskundige functies</span><span class="sxs-lookup"><span data-stu-id="11203-605">Mathematical functions</span></span>  | <span data-ttu-id="11203-606">ABS, maximum, EXP, FLOOR, logboek, LOG10, POWER, ROUND, aanmelding, SQRT, VIERKANT, geheel, BOOGCOS, ASIN, BOOGTAN, ATN2, Cosinus, COT, graden PI, radialen, SIN en TAN</span><span class="sxs-lookup"><span data-stu-id="11203-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="11203-607">Controle van de functies van het type</span><span class="sxs-lookup"><span data-stu-id="11203-607">Type checking functions</span></span> | <span data-ttu-id="11203-608">IS_ARRAY, IS_BOOL IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED en IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="11203-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="11203-609">Tekenreeks-functies</span><span class="sxs-lookup"><span data-stu-id="11203-609">String functions</span></span>        | <span data-ttu-id="11203-610">CONCAT, bevat ENDSWITH, INDEX_OF, links, lengte, kleine, LTRIM, vervangen, REPLICEREN, REVERSE, rechts, RTRIM, STARTSWITH, SUBTEKENREEKS en hoofdletters</span><span class="sxs-lookup"><span data-stu-id="11203-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="11203-611">Matrixfuncties</span><span class="sxs-lookup"><span data-stu-id="11203-611">Array functions</span></span>         | <span data-ttu-id="11203-612">ARRAY_CONCAT, ARRAY_CONTAINS ARRAY_LENGTH en ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="11203-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="11203-613">Ruimtelijke functies</span><span class="sxs-lookup"><span data-stu-id="11203-613">Spatial functions</span></span>       | <span data-ttu-id="11203-614">ST_DISTANCE, ST_WITHIN ST_INTERSECTS, ST_ISVALID en ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="11203-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="11203-615">Als u een gebruiker gedefinieerde functie (UDF) waarvoor een ingebouwde functie nu beschikbaar is momenteel gebruikt, moet u de bijbehorende ingebouwde functie als is het verstandig om sneller worden uitgevoerd en efficiënter.</span><span class="sxs-lookup"><span data-stu-id="11203-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="11203-616">Wiskundige functies</span><span class="sxs-lookup"><span data-stu-id="11203-616">Mathematical functions</span></span>
<span data-ttu-id="11203-617">De rekenkundige functies elke uitvoeren van een berekening op basis van de invoerwaarden die zijn opgegeven als argumenten en een numerieke waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="11203-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="11203-618">Hier volgt een lijst met ondersteunde ingebouwde, rekenkundige functies.</span><span class="sxs-lookup"><span data-stu-id="11203-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="11203-619">Gebruik</span><span class="sxs-lookup"><span data-stu-id="11203-619">Usage</span></span> | <span data-ttu-id="11203-620">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="11203-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="11203-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="11203-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="11203-622">Retourneert de absolute (positieve) waarde van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="11203-623">MAXIMUM (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="11203-624">Retourneert de kleinste waarde van geheel getal groter dan of gelijk zijn aan de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="11203-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="11203-626">Retourneert het grootste gehele getal kleiner dan of gelijk zijn aan de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="11203-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="11203-628">Retourneert de exponent van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="11203-629">[LOGBOEK (num_expr [, base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="11203-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="11203-630">Retourneert de natuurlijke logaritme van de opgegeven numerieke expressie, of de logaritme met behulp van het opgegeven grondtal</span><span class="sxs-lookup"><span data-stu-id="11203-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="11203-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="11203-632">Retourneert de logaritmische waarde grondtal 10 van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="11203-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="11203-634">Retourneert een numerieke waarde, op het dichtstbijzijnde gehele getal afgerond.</span><span class="sxs-lookup"><span data-stu-id="11203-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="11203-635">GEHEEL (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="11203-636">Retourneert een numerieke waarde, afgekapt tot het dichtstbijzijnde gehele getal.</span><span class="sxs-lookup"><span data-stu-id="11203-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="11203-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="11203-638">Retourneert de vierkantswortel van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="11203-639">Vierkante (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="11203-640">Retourneert het kwadraat van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="11203-641">VOEDING (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="11203-642">Retourneert de kracht van de opgegeven numerieke expressie voor de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="11203-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="11203-643">ONDERTEKENEN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="11203-644">Retourneert de waarde teken (-1, 0, 1) van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="11203-645">BOOGCOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="11203-646">Retourneert de hoek in radialen, waarvan de cosinus de opgegeven numerieke expressie is. ook wel de boogcosinus genoemd.</span><span class="sxs-lookup"><span data-stu-id="11203-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="11203-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="11203-648">Retourneert de hoek in radialen, waarvan de sinus de opgegeven numerieke expressie is.</span><span class="sxs-lookup"><span data-stu-id="11203-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="11203-649">Dit wordt ook boogsinus genoemd.</span><span class="sxs-lookup"><span data-stu-id="11203-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="11203-650">BOOGTAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="11203-651">Retourneert de hoek in radialen, waarvan de tangens de opgegeven numerieke expressie is.</span><span class="sxs-lookup"><span data-stu-id="11203-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="11203-652">Dit wordt ook arctangens genoemd.</span><span class="sxs-lookup"><span data-stu-id="11203-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="11203-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="11203-654">Als resultaat geeft de hoek in radialen tussen de positieve x-as en de ray vanuit de oorsprong naar het punt (y, x), waarbij x en y zijn de waarden van de twee opgegeven float-expressies.</span><span class="sxs-lookup"><span data-stu-id="11203-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="11203-655">CO (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="11203-656">Retourneert de trigonometrische cosinus van de opgegeven hoek in radialen in de opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="11203-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="11203-658">Retourneert de trigonometrische cotangens van de opgegeven hoek in radialen in het opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="11203-659">GRADEN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="11203-660">Retourneert de overeenkomstige hoek in graden voor een hoek aangeduid in radialen.</span><span class="sxs-lookup"><span data-stu-id="11203-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="11203-661">PI)</span><span class="sxs-lookup"><span data-stu-id="11203-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="11203-662">Retourneert de constante waarde van PI.</span><span class="sxs-lookup"><span data-stu-id="11203-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="11203-663">RADIALEN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="11203-664">Retourneert radialen wanneer een numerieke expressie, in graden wordt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="11203-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="11203-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="11203-666">Retourneert de trigonometrische sinus van de opgegeven hoek in radialen in de opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="11203-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="11203-668">Retourneert de tangens van de invoer expressie in de opgegeven expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="11203-669">U kunt nu bijvoorbeeld query's als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="11203-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="11203-670">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="11203-671">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-671">**Results**</span></span>

    [4]

<span data-ttu-id="11203-672">Het belangrijkste verschil tussen Cosmos-database functies ten opzichte van ANSI SQL is dat ze zijn ontworpen om te werken goed met schemagegevens zonder schema en een gemengde.</span><span class="sxs-lookup"><span data-stu-id="11203-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="11203-673">Als u hebt een document waarbij de eigenschap Size ontbreekt of heeft een niet-numerieke waarde, zoals 'Onbekend' vervolgens het document is overgeslagen, klikt u in plaats van een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="11203-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="11203-674">Controle van de functies van het type</span><span class="sxs-lookup"><span data-stu-id="11203-674">Type checking functions</span></span>
<span data-ttu-id="11203-675">Het type controleren of functies kunnen u om te controleren van het type van een expressie in SQL-query's.</span><span class="sxs-lookup"><span data-stu-id="11203-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="11203-676">Type controleren of functies kunnen worden gebruikt om te bepalen het type van de eigenschappen in een-documenten wanneer deze variabele of een onbekend.</span><span class="sxs-lookup"><span data-stu-id="11203-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="11203-677">Hier volgt een lijst met ondersteunde ingebouwde typecontrole functies.</span><span class="sxs-lookup"><span data-stu-id="11203-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="11203-678"><strong>Gebruik</strong></span><span class="sxs-lookup"><span data-stu-id="11203-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="11203-679"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="11203-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="11203-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="11203-681">Retourneert een Booleaanse waarde die aangeeft of het type van de waarde een matrix is.</span><span class="sxs-lookup"><span data-stu-id="11203-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="11203-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="11203-683">Retourneert een Booleaanse waarde die aangeeft of het type van de waarde een Booleaanse waarde is.</span><span class="sxs-lookup"><span data-stu-id="11203-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="11203-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="11203-685">Retourneert een Booleaanse waarde die aangeeft of het type van de waarde null is.</span><span class="sxs-lookup"><span data-stu-id="11203-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="11203-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="11203-687">Retourneert een Booleaanse waarde die aangeeft of het type van de waarde een getal is.</span><span class="sxs-lookup"><span data-stu-id="11203-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="11203-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="11203-689">Retourneert een Booleaanse waarde die aangeeft of het type van de waarde een JSON-object is.</span><span class="sxs-lookup"><span data-stu-id="11203-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="11203-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="11203-691">Retourneert een Booleaanse waarde die aangeeft of het type van de waarde een tekenreeks is.</span><span class="sxs-lookup"><span data-stu-id="11203-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="11203-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="11203-693">Retourneert een Booleaanse waarde die aangeeft of de eigenschap een waarde is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="11203-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="11203-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="11203-695">Retourneert een Booleaanse waarde die aangeeft of het type van de waarde een tekenreeks, getal, Booleaanse waarde of null zijn is.</span><span class="sxs-lookup"><span data-stu-id="11203-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="11203-696">U kunt nu een query's als volgt uitvoeren met behulp van deze functies:</span><span class="sxs-lookup"><span data-stu-id="11203-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="11203-697">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="11203-698">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="11203-699">Tekenreeks-functies</span><span class="sxs-lookup"><span data-stu-id="11203-699">String functions</span></span>
<span data-ttu-id="11203-700">De volgende scalaire functies een bewerking uitvoeren op een tekenreekswaarde van de invoer en een tekenreeks, numerieke of Booleaanse waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="11203-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="11203-701">Hier volgt een lijst met ingebouwde tekenreeks-functies:</span><span class="sxs-lookup"><span data-stu-id="11203-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="11203-702">Gebruik</span><span class="sxs-lookup"><span data-stu-id="11203-702">Usage</span></span> | <span data-ttu-id="11203-703">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="11203-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="11203-704">LENGTE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="11203-705">Retourneert het aantal tekens van de opgegeven tekenreeksexpressie</span><span class="sxs-lookup"><span data-stu-id="11203-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="11203-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="11203-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="11203-707">Retourneert een tekenreeks die het resultaat van het samenvoegen van twee of meer tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="11203-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="11203-708">De SUBTEKENREEKS (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="11203-709">Retourneert deel van een tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="11203-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="11203-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="11203-711">Retourneert een Boolean die aangeeft of de eerste tekenreeksexpressie eindigt op de tweede</span><span class="sxs-lookup"><span data-stu-id="11203-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="11203-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="11203-713">Retourneert een Boolean die aangeeft of de eerste tekenreeksexpressie eindigt op de tweede</span><span class="sxs-lookup"><span data-stu-id="11203-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="11203-714">BEVAT (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="11203-715">Retourneert een Boolean die aangeeft of de eerste expressie tekenreeks de tweede bevat.</span><span class="sxs-lookup"><span data-stu-id="11203-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="11203-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="11203-717">Retourneert de beginpositie van het eerste exemplaar van de tweede tekenreeksexpressie binnen de eerste expressie in de opgegeven tekenreeks is of -1 als de tekenreeks is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="11203-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="11203-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="11203-719">Retourneert het linkergedeelte van een tekenreeks zijn met het opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="11203-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="11203-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="11203-721">Retourneert de juiste deel van een tekenreeks zijn met het opgegeven aantal tekens.</span><span class="sxs-lookup"><span data-stu-id="11203-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="11203-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="11203-723">Retourneert een tekenreeksexpressie na het verwijderen van toonaangevende lege waarden.</span><span class="sxs-lookup"><span data-stu-id="11203-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="11203-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="11203-725">Retourneert een tekenreeksexpressie na het afkappen van alle volgspaties.</span><span class="sxs-lookup"><span data-stu-id="11203-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="11203-726">KLEINE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="11203-727">Retourneert een tekenreeksexpressie na hoofdletter gegevens converteren naar kleine letters.</span><span class="sxs-lookup"><span data-stu-id="11203-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="11203-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="11203-729">Retourneert een tekenreeksexpressie na kleine letter gegevens converteren naar hoofdletters.</span><span class="sxs-lookup"><span data-stu-id="11203-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="11203-730">Vervang (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="11203-731">Vervangt alle instanties van een opgegeven string-waarde met de waarde van een andere tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="11203-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="11203-732">REPLICEREN (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="11203-733">Herhaalt een string-waarde van een opgegeven aantal keren.</span><span class="sxs-lookup"><span data-stu-id="11203-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="11203-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="11203-735">Retourneert de omgekeerde volgorde van een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="11203-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="11203-736">U kunt nu een query's als volgt uitvoeren met behulp van deze functies.</span><span class="sxs-lookup"><span data-stu-id="11203-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="11203-737">U kunt bijvoorbeeld de familienaam in hoofdletters als volgt:</span><span class="sxs-lookup"><span data-stu-id="11203-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="11203-738">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="11203-739">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="11203-740">Of samenvoegen van strings zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11203-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="11203-741">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="11203-742">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="11203-743">Tekenreeks-functies kunnen ook worden gebruikt in de component WHERE om resultaten te filteren, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11203-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="11203-744">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="11203-745">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="11203-746">Matrixfuncties</span><span class="sxs-lookup"><span data-stu-id="11203-746">Array functions</span></span>
<span data-ttu-id="11203-747">De volgende scalaire functies een bewerking uitvoeren op een matrix invoerwaarde en retourneren numerieke, Booleaanse waarde of een matrix van waarde.</span><span class="sxs-lookup"><span data-stu-id="11203-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="11203-748">Hier volgt een lijst met ingebouwde matrixfuncties:</span><span class="sxs-lookup"><span data-stu-id="11203-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="11203-749">Gebruik</span><span class="sxs-lookup"><span data-stu-id="11203-749">Usage</span></span> | <span data-ttu-id="11203-750">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="11203-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="11203-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="11203-752">Retourneert het aantal elementen van de opgegeven matrix-expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="11203-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="11203-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="11203-754">Retourneert een matrix die het resultaat van het samenvoegen van twee of meer matrixwaarden.</span><span class="sxs-lookup"><span data-stu-id="11203-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="11203-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="11203-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="11203-756">Retourneert een Booleaanse waarde die aangeeft of de matrix bevat met de opgegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="11203-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="11203-757">Kunnen opgeven als overeenkomst met de volledige of gedeeltelijke.</span><span class="sxs-lookup"><span data-stu-id="11203-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="11203-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="11203-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="11203-759">Retourneert deel van een matrixexpressie.</span><span class="sxs-lookup"><span data-stu-id="11203-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="11203-760">Matrixfuncties kunnen worden gebruikt voor het bewerken van matrices in JSON.</span><span class="sxs-lookup"><span data-stu-id="11203-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="11203-761">Hier is bijvoorbeeld een query die alle documenten retourneert waarbij een van de ouders 'Robin Wakefield' is.</span><span class="sxs-lookup"><span data-stu-id="11203-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="11203-762">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="11203-763">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="11203-764">U kunt opgeven dat een gedeeltelijke fragment voor overeenkomende elementen binnen de matrix.</span><span class="sxs-lookup"><span data-stu-id="11203-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="11203-765">De volgende query vindt alle bovenliggende items met de `givenName` van `Robin`.</span><span class="sxs-lookup"><span data-stu-id="11203-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="11203-766">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="11203-767">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="11203-768">Hier volgt een voorbeeld waarin ARRAY_LENGTH wordt gebruikt voor het aantal onderliggende items per serie.</span><span class="sxs-lookup"><span data-stu-id="11203-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="11203-769">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="11203-770">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="11203-771">Ruimtelijke functies</span><span class="sxs-lookup"><span data-stu-id="11203-771">Spatial functions</span></span>
<span data-ttu-id="11203-772">De volgende ingebouwde functies voor Open georuimtelijke Consortium (OGC) biedt ondersteuning voor cosmos DB georuimtelijke query's.</span><span class="sxs-lookup"><span data-stu-id="11203-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="11203-773"><strong>Gebruik</strong></span><span class="sxs-lookup"><span data-stu-id="11203-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="11203-774"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="11203-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="11203-776">Retourneert de afstand tussen de twee GeoJSON punt, Polygon of LineString expressies.</span><span class="sxs-lookup"><span data-stu-id="11203-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="11203-778">Retourneert een Booleaanse expressie die aangeeft of het eerste GeoJSON-object (punt, Polygon of LineString) binnen het tweede GeoJSON-object (punt, Polygon of LineString).</span><span class="sxs-lookup"><span data-stu-id="11203-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="11203-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="11203-780">Retourneert een Booleaanse expressie waarmee wordt aangegeven of de twee opgegeven GeoJSON objecten (punt, Polygon of LineString) intersect.</span><span class="sxs-lookup"><span data-stu-id="11203-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="11203-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="11203-782">Retourneert een Booleaanse waarde die aangeeft of de opgegeven expressie voor GeoJSON punt, Polygon of LineString ongeldig is.</span><span class="sxs-lookup"><span data-stu-id="11203-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="11203-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="11203-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="11203-784">Retourneert een JSON-waarde met een Booleaanse waarde als de opgegeven expressie voor GeoJSON punt, Polygon of LineString is geldig, en als ongeldig, ook de reden als een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="11203-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="11203-785">Ruimtelijke functies kunnen worden gebruikt om uit te voeren nabijheid query's op ruimtelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="11203-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="11203-786">Hier is bijvoorbeeld een query die alle familie documenten die binnen 30 km van de opgegeven locatie met de ingebouwde functie ST_DISTANCE retourneert.</span><span class="sxs-lookup"><span data-stu-id="11203-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="11203-787">**Query**</span><span class="sxs-lookup"><span data-stu-id="11203-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="11203-788">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="11203-789">Zie voor meer informatie over ondersteuning voor Cosmos DB georuimtelijke [werken met gegevens in Azure Cosmos DB georuimtelijke](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="11203-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="11203-790">Die loopt van ruimtelijke functies en de SQL-syntaxis voor Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="11203-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="11203-791">Nu eens kijken hoe LINQ-query werkt en hoe deze samenwerkt met de syntaxis we hebt gezien tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="11203-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="11203-792"><a id="Linq"></a>LINQ to SQL voor DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="11203-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="11203-793">LINQ is een .NET-programmeermodel waarin berekeningen query's voor stromen van objecten.</span><span class="sxs-lookup"><span data-stu-id="11203-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="11203-794">Cosmos DB biedt een client-side '-bibliotheek voor LINQ-interface doordat een conversie tussen JSON en .NET-objecten en een toewijzing van een subset van LINQ-query's aan Cosmos-DB-query's.</span><span class="sxs-lookup"><span data-stu-id="11203-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="11203-795">De volgende afbeelding toont de architectuur van LINQ-query's met behulp van de Cosmos-DB ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="11203-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="11203-796">Met behulp van de Cosmos-DB-client kunnen ontwikkelaars maken een **IQueryable** object waarmee een query rechtstreeks op de Cosmos-DB-provider opvragen, die vervolgens de LINQ-query in een Cosmos-DB-query zet.</span><span class="sxs-lookup"><span data-stu-id="11203-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="11203-797">De query wordt vervolgens doorgegeven aan de Cosmos-databaseserver voor het ophalen van een set resultaten in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="11203-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="11203-798">De geretourneerde resultaten worden in een stream met .NET-objecten aan de clientzijde gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="11203-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![Architectuur van de LINQ-query's met DocumentDB-API - SQL-syntaxis, JSON-querytaal concepten van de database en SQL-query's ondersteunen][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="11203-800">.NET- en JSON-toewijzing</span><span class="sxs-lookup"><span data-stu-id="11203-800">.NET and JSON mapping</span></span>
<span data-ttu-id="11203-801">De toewijzing tussen .NET-objecten en JSON-documenten is natuurlijk - elk veld gegevens lid is toegewezen aan een JSON-object, waarbij de veldnaam is toegewezen aan het gedeelte 'sleutel' van het object en het onderdeel '' waarde '' recursief toegewezen aan de waarde van het object.</span><span class="sxs-lookup"><span data-stu-id="11203-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="11203-802">Bekijk het volgende voorbeeld: de familie-object gemaakt is toegewezen aan het JSON-document, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="11203-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="11203-803">En omgekeerd, het JSON-document is toegewezen aan een .NET-object.</span><span class="sxs-lookup"><span data-stu-id="11203-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="11203-804">**C#-klasse**</span><span class="sxs-lookup"><span data-stu-id="11203-804">**C# Class**</span></span>

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


<span data-ttu-id="11203-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="11203-805">**JSON**</span></span>  

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



### <a name="linq-to-sql-translation"></a><span data-ttu-id="11203-806">LINQ SQL vertaling</span><span class="sxs-lookup"><span data-stu-id="11203-806">LINQ to SQL translation</span></span>
<span data-ttu-id="11203-807">De Cosmos-DB-provider opvragen voert een best effort toewijzing van een LINQ-query naar een Cosmos DB SQL-query.</span><span class="sxs-lookup"><span data-stu-id="11203-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="11203-808">In de volgende beschrijving gaan we ervan uit dat de lezer heeft een elementaire kennis van LINQ.</span><span class="sxs-lookup"><span data-stu-id="11203-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="11203-809">Voor het typesysteem ondersteunen we eerst alle JSON primitieve typen – numerieke typen, Booleaanse waarde, tekenreeks en null.</span><span class="sxs-lookup"><span data-stu-id="11203-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="11203-810">Alleen deze JSON-typen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="11203-810">Only these JSON types are supported.</span></span> <span data-ttu-id="11203-811">De volgende scalaire expressies worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="11203-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="11203-812">Constante waarden – hierbij constante waarden van de primitieve gegevenstypen op het moment dat de query wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="11203-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="11203-813">Eigenschappenmatrix/indexexpressies – deze expressies verwijzen naar de eigenschap van een object of een element van de matrix.</span><span class="sxs-lookup"><span data-stu-id="11203-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="11203-814">familie. ID;    Family.children[0].familyName;    Family.children[0].Grade;    Family.children[n].Grade; n is een int-variabele</span><span class="sxs-lookup"><span data-stu-id="11203-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="11203-815">Aritmetische expressies - deze algemene aritmetische expressies op numerieke en Booleaanse waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="11203-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="11203-816">Raadpleeg de SQL-specificatie voor de volledige lijst.</span><span class="sxs-lookup"><span data-stu-id="11203-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="11203-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="11203-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="11203-818">Vergelijking van tekenreeksexpressie - hierbij een string-waarde naar een constante string-waarde te vergelijken.</span><span class="sxs-lookup"><span data-stu-id="11203-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="11203-819">mother.familyName == 'Smith';    child.givenName == s; s is een string-variabele</span><span class="sxs-lookup"><span data-stu-id="11203-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="11203-820">Object/matrix maken van expressie - deze expressies return een object van het waardetype van de samengestelde of anoniem type of een matrix van dergelijke objecten.</span><span class="sxs-lookup"><span data-stu-id="11203-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="11203-821">Deze waarden kunnen worden genest.</span><span class="sxs-lookup"><span data-stu-id="11203-821">These values can be nested.</span></span>
  
     <span data-ttu-id="11203-822">nieuwe bovenliggende {familyName = 'Smit', givenName = "Jan"}; nieuwe {eerst = 1, tweede = 2}; een anoniem type met twee velden</span><span class="sxs-lookup"><span data-stu-id="11203-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="11203-823">nieuwe int [] {3, child.grade, 5};</span><span class="sxs-lookup"><span data-stu-id="11203-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="11203-824"><a id="SupportedLinqOperators"></a>Lijst met ondersteunde LINQ-operators</span><span class="sxs-lookup"><span data-stu-id="11203-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="11203-825">Hier volgt een lijst met ondersteunde LINQ-operators in de LINQ-provider die deel uitmaakt van de DocumentDB .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="11203-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="11203-826">**Selecteer**: projecties vertalen naar de SQL SELECT-objectconstructie inclusief</span><span class="sxs-lookup"><span data-stu-id="11203-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="11203-827">**Waar**: Filters vertalen naar SQL WHERE en ondersteuning voor de conversie van & &, || en!</span><span class="sxs-lookup"><span data-stu-id="11203-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="11203-828">aan de SQL-operators</span><span class="sxs-lookup"><span data-stu-id="11203-828">to the SQL operators</span></span>
* <span data-ttu-id="11203-829">**SelectMany**: kunt ongedaan maken van matrices voor de SQL-JOIN-component.</span><span class="sxs-lookup"><span data-stu-id="11203-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="11203-830">Kan worden gebruikt voor expressies kunt u filteren op matrixelementen keten/nest</span><span class="sxs-lookup"><span data-stu-id="11203-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="11203-831">**OrderBy en OrderByDescending**: vertaalt in ORDER BY oplopend/aflopend</span><span class="sxs-lookup"><span data-stu-id="11203-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="11203-832">**Aantal**, **som**, **Min**, **Max**, en **gemiddelde** operators voor aggregatie en de async-equivalenten **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, en **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="11203-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="11203-833">**CompareTo**: wordt omgezet in bereik vergelijkingen.</span><span class="sxs-lookup"><span data-stu-id="11203-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="11203-834">Meestal gebruikt voor tekenreeksen omdat ze nog niet vergeleken in .NET</span><span class="sxs-lookup"><span data-stu-id="11203-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="11203-835">**Nemen**: kan het aan de BOVENKANT SQL voor het beperken van de resultaten van een query</span><span class="sxs-lookup"><span data-stu-id="11203-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="11203-836">**Rekenkundige functies**: de vertaling van ondersteunt. De NET Abs, BOOGCOS, Asin, BOOGTAN, maximum, CO, Exp, Floor, logboek, Log10, Pow, Round, aanmelding, Sin, Sqrt, Tan, Truncate aan de gelijkwaardige ingebouwde functies van SQL.</span><span class="sxs-lookup"><span data-stu-id="11203-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="11203-837">**Functies String**: de vertaling van ondersteunt. NET van Concat, bevat EndsWith, IndexOf, Count, ToLower, TrimStart, vervangen, Reverse, TrimEnd, StartsWith, subtekenreeks, ToUpper aan de gelijkwaardige ingebouwde functies van SQL.</span><span class="sxs-lookup"><span data-stu-id="11203-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="11203-838">**Matrix van functies**: de vertaling van ondersteunt. NET van Concat, bevat en aantal voor de equivalente ingebouwde SQL-functies.</span><span class="sxs-lookup"><span data-stu-id="11203-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="11203-839">**Extensiefuncties georuimtelijke**: vertaling van stub-methoden afstand binnen IsValid en IsValidDetailed naar de equivalente ingebouwde SQL-functies ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="11203-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="11203-840">**Gebruiker gedefinieerde functie extensiefunctie**: ondersteunt de vertaling van de stubmethode UserDefinedFunctionProvider.Invoke naar de bijbehorende door de gebruiker gedefinieerde functie.</span><span class="sxs-lookup"><span data-stu-id="11203-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="11203-841">**Diverse**: biedt ondersteuning voor omzetting van de coalesce en voorwaardelijke operators.</span><span class="sxs-lookup"><span data-stu-id="11203-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="11203-842">Bevat tekenreeks bevat, ARRAY_CONTAINS of de SQL-IN, afhankelijk van de context kunnen worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="11203-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="11203-843">SQL-query-operators</span><span class="sxs-lookup"><span data-stu-id="11203-843">SQL query operators</span></span>
<span data-ttu-id="11203-844">Hier volgen enkele voorbeelden die aangeven hoe sommige van de standaard LINQ-query's worden omgezet naar beneden Cosmos-DB-query's.</span><span class="sxs-lookup"><span data-stu-id="11203-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="11203-845">Operator selecteren</span><span class="sxs-lookup"><span data-stu-id="11203-845">Select Operator</span></span>
<span data-ttu-id="11203-846">De syntaxis is `input.Select(x => f(x))`, waarbij `f` is een scalaire expressie.</span><span class="sxs-lookup"><span data-stu-id="11203-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="11203-847">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="11203-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="11203-849">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="11203-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="11203-851">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="11203-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="11203-853">SelectMany operator</span><span class="sxs-lookup"><span data-stu-id="11203-853">SelectMany operator</span></span>
<span data-ttu-id="11203-854">De syntaxis is `input.SelectMany(x => f(x))`, waarbij `f` is een scalaire expressie die als resultaat een verzamelingstype geeft.</span><span class="sxs-lookup"><span data-stu-id="11203-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="11203-855">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="11203-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="11203-857">Waar operator</span><span class="sxs-lookup"><span data-stu-id="11203-857">Where operator</span></span>
<span data-ttu-id="11203-858">De syntaxis is `input.Where(x => f(x))`, waarbij `f` is een scalaire expressie die een Booleaanse waarde retourneert.</span><span class="sxs-lookup"><span data-stu-id="11203-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="11203-859">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="11203-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="11203-861">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="11203-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="11203-863">Samengestelde SQL-query 's</span><span class="sxs-lookup"><span data-stu-id="11203-863">Composite SQL queries</span></span>
<span data-ttu-id="11203-864">De bovenstaande operators kunnen worden samengesteld om krachtige query's.</span><span class="sxs-lookup"><span data-stu-id="11203-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="11203-865">Aangezien Cosmos DB geneste verzamelingen ondersteunt, kan de samenstelling worden samengevoegd of genest.</span><span class="sxs-lookup"><span data-stu-id="11203-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="11203-866">Samenvoeging</span><span class="sxs-lookup"><span data-stu-id="11203-866">Concatenation</span></span>
<span data-ttu-id="11203-867">De syntaxis is `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="11203-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="11203-868">Een samengevoegde query kunt beginnen met een optionele `SelectMany` query gevolgd door meerdere `Select` of `Where` operators.</span><span class="sxs-lookup"><span data-stu-id="11203-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="11203-869">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="11203-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="11203-871">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="11203-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="11203-873">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="11203-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="11203-875">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="11203-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="11203-877">Nesten</span><span class="sxs-lookup"><span data-stu-id="11203-877">Nesting</span></span>
<span data-ttu-id="11203-878">De syntaxis is `input.SelectMany(x=>x.Q())` waarbij Q is een `Select`, `SelectMany`, of `Where` operator.</span><span class="sxs-lookup"><span data-stu-id="11203-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="11203-879">In een geneste query, wordt de interne query toegepast op elk element van de buitenste verzameling.</span><span class="sxs-lookup"><span data-stu-id="11203-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="11203-880">Een belangrijk onderdeel is dat de interne query naar de velden van de elementen in de buitenste verzameling zoals verwijzen kunt zelf-joins.</span><span class="sxs-lookup"><span data-stu-id="11203-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="11203-881">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="11203-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="11203-883">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="11203-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="11203-885">**LINQ lambda-expressie**</span><span class="sxs-lookup"><span data-stu-id="11203-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="11203-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="11203-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="11203-887"><a id="ExecutingSqlQueries"></a>SQL-query's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="11203-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="11203-888">Cosmos DB Ontsluit resources via een REST-API die kan worden aangeroepen via elke taal waarmee HTTP/HTTPS-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="11203-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="11203-889">Daarnaast biedt Cosmos DB programmeringsbibliotheken voor verschillende veelgebruikte talen zoals .NET, Node.js, JavaScript en Python.</span><span class="sxs-lookup"><span data-stu-id="11203-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="11203-890">De REST-API en de verschillende bibliotheken ondersteuning voor het uitvoeren van query's via SQL.</span><span class="sxs-lookup"><span data-stu-id="11203-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="11203-891">De .NET SDK biedt ondersteuning voor LINQ-query naast SQL.</span><span class="sxs-lookup"><span data-stu-id="11203-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="11203-892">De volgende voorbeelden laten zien hoe u een query maken en te verzenden op basis van een Cosmos-DB-databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="11203-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="11203-893"><a id="RestAPI"></a>REST-API</span><span class="sxs-lookup"><span data-stu-id="11203-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="11203-894">Cosmos DB biedt een open RESTful-programmeermodel via HTTP.</span><span class="sxs-lookup"><span data-stu-id="11203-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="11203-895">Database-accounts kunnen worden ingericht met behulp van een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="11203-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="11203-896">Het model van de resource Cosmos DB bestaat uit een set resources onder de databaseaccount van een, die elk opgevraagd met een logische en stabiele-URI is.</span><span class="sxs-lookup"><span data-stu-id="11203-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="11203-897">Een set resources wordt aangeduid als een feed in dit document.</span><span class="sxs-lookup"><span data-stu-id="11203-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="11203-898">Een databaseaccount bestaat uit een reeks databases, die elk meerdere verzamelingen met elk van welke beurt documenten, UDF's en andere brontypen bevatten.</span><span class="sxs-lookup"><span data-stu-id="11203-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="11203-899">Het model basic interactie met deze resources is via de HTTP-woorden GET, PUT, POST en DELETE met hun standaard interpretatie.</span><span class="sxs-lookup"><span data-stu-id="11203-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="11203-900">De POST-bewerking wordt gebruikt voor het maken van een nieuwe resource, voor het uitvoeren van een opgeslagen procedure of voor het uitgeven van een Cosmos-DB-query.</span><span class="sxs-lookup"><span data-stu-id="11203-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="11203-901">Query's zijn altijd alleen-lezen bewerkingen met geen bijwerkingen.</span><span class="sxs-lookup"><span data-stu-id="11203-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="11203-902">De volgende voorbeelden ziet een POST voor een DocumentDB-API-query ten opzichte van een verzameling met de twee voorbeelddocumenten dat we tot nu toe hebt bekeken.</span><span class="sxs-lookup"><span data-stu-id="11203-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="11203-903">De query heeft een eenvoudige filter op de naameigenschap JSON.</span><span class="sxs-lookup"><span data-stu-id="11203-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="11203-904">Let op het gebruik van de `x-ms-documentdb-isquery` en Content-Type: `application/query+json` headers om aan te geven dat de bewerking een query wordt.</span><span class="sxs-lookup"><span data-stu-id="11203-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="11203-905">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="11203-905">**Request**</span></span>

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


<span data-ttu-id="11203-906">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-906">**Results**</span></span>

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


<span data-ttu-id="11203-907">Het tweede voorbeeld ziet u een complexere query die meerdere resultaten uit de join retourneert.</span><span class="sxs-lookup"><span data-stu-id="11203-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="11203-908">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="11203-908">**Request**</span></span>

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


<span data-ttu-id="11203-909">**Resultaten**</span><span class="sxs-lookup"><span data-stu-id="11203-909">**Results**</span></span>

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


<span data-ttu-id="11203-910">Als de queryresultaten niet binnen één pagina met resultaten passen, wordt de REST-API een vervolgtoken via retourneert de `x-ms-continuation-token` antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="11203-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="11203-911">Clients kunnen resultaten pagineren door de header in de volgende resultaten.</span><span class="sxs-lookup"><span data-stu-id="11203-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="11203-912">Het aantal resultaten per pagina kan ook worden beheerd via de `x-ms-max-item-count` nummer header.</span><span class="sxs-lookup"><span data-stu-id="11203-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="11203-913">Als de opgegeven query een statistische functie zoals heeft `COUNT`, en vervolgens de querypagina een gedeeltelijk cumulatieve waarde kan worden geretourneerd gedurende de pagina met resultaten.</span><span class="sxs-lookup"><span data-stu-id="11203-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="11203-914">De clients moeten een aggregatie tweede niveau uitvoeren via deze resultaten met het uiteindelijke resultaat, bijvoorbeeld, som is opgegeven via de tellingen geretourneerd in de afzonderlijke pagina's om de totale telling te retourneren.</span><span class="sxs-lookup"><span data-stu-id="11203-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="11203-915">Gebruik het beleid voor de consistentie van gegevens voor query's beheren de `x-ms-consistency-level` header bijvoorbeeld alle aanvragen voor REST-API.</span><span class="sxs-lookup"><span data-stu-id="11203-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="11203-916">Voor sessieconsistentie, is het vereist ook de meest recente echo `x-ms-session-token` Cookie-kop in de queryaanvraag.</span><span class="sxs-lookup"><span data-stu-id="11203-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="11203-917">De aangevraagde verzameling indexeringsbeleid kan ook invloed hebben op de consistentie van de queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="11203-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="11203-918">Met de standaard beleidsinstellingen indexeren, voor verzamelingen de index is altijd de meest recente inhoud van het document en queryresultaten overeenkomen met de consistentiecontrole gekozen voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="11203-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="11203-919">Als het indexeringsbeleid is versoepeld naar Lazy, kunnen query's verlopen resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="11203-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="11203-920">Zie voor meer informatie [Azure Cosmos DB Consistentieniveaus][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="11203-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="11203-921">Als de opgegeven query kan niet worden ondersteund door het geconfigureerde indexeringsbeleid voor de verzameling, retourneert de server Azure Cosmos DB 400 'onjuiste aanvraag'.</span><span class="sxs-lookup"><span data-stu-id="11203-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="11203-922">Dit wordt geretourneerd voor bereik query's op paden die zijn geconfigureerd voor lookups op hash (gelijkheid) en voor paden expliciet is uitgesloten van het indexeren.</span><span class="sxs-lookup"><span data-stu-id="11203-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="11203-923">De `x-ms-documentdb-query-enable-scan` header kan worden opgegeven waarmee de query voor een scan uitvoeren als een index niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="11203-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="11203-924">U kunt gedetailleerde metrische gegevens over de uitvoering van de query opvragen door in te stellen `x-ms-documentdb-populatequerymetrics` koptekst tot `True`.</span><span class="sxs-lookup"><span data-stu-id="11203-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="11203-925">Zie voor meer informatie [SQL query metrische gegevens voor Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="11203-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="11203-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="11203-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="11203-927">De .NET SDK biedt ondersteuning voor LINQ- en SQL uitvoeren van query's.</span><span class="sxs-lookup"><span data-stu-id="11203-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="11203-928">Het volgende voorbeeld ziet hoe u de eenvoudige filterquery geïntroduceerd eerder in dit document uitvoert.</span><span class="sxs-lookup"><span data-stu-id="11203-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="11203-929">Dit voorbeeld vergelijkt twee eigenschappen op gelijkheid binnen elk document en maakt gebruik van anonieme projecties.</span><span class="sxs-lookup"><span data-stu-id="11203-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="11203-930">Het volgende voorbeeld toont joins, die zijn uitgedrukt via LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="11203-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="11203-931">De .NET-client worden automatisch alle pagina's van de resultaten van de query in de foreach-blokken zoals hierboven doorlopen.</span><span class="sxs-lookup"><span data-stu-id="11203-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="11203-932">De query-opties die zijn geïntroduceerd in de REST-API-sectie zijn ook beschikbaar in de .NET SDK met de `FeedOptions` en `FeedResponse` klassen in de methode CreateDocumentQuery.</span><span class="sxs-lookup"><span data-stu-id="11203-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="11203-933">Het aantal pagina's kan worden beheerd met behulp van de `MaxItemCount` instelling.</span><span class="sxs-lookup"><span data-stu-id="11203-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="11203-934">U kunt ook expliciet paginering bepalen door het maken van `IDocumentQueryable` met behulp van de `IQueryable` object, klikt u vervolgens op het lezen van de` ResponseContinuationToken` waarden en deze weer toe als `RequestContinuationToken` in `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="11203-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="11203-935">`EnableScanInQuery`kan worden ingesteld voor het inschakelen van scans als de query kan niet worden ondersteund door het geconfigureerde indexeringsbeleid.</span><span class="sxs-lookup"><span data-stu-id="11203-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="11203-936">Voor gepartitioneerde verzamelingen kunt u `PartitionKey` aan de query uitvoeren voor één partitie (Hoewel Cosmos DB dit automatisch uit de querytekst ophalen kunt), en `EnableCrossPartitionQuery` query's uitvoeren die mogelijk moet worden uitgevoerd tegen meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="11203-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="11203-937">Raadpleeg [Azure Cosmos DB .NET-voorbeelden](https://github.com/Azure/azure-documentdb-net) voor meer voorbeelden met query's.</span><span class="sxs-lookup"><span data-stu-id="11203-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="11203-938"><a id="JavaScriptServerSideApi"></a>JavaScript-serverzijde-API</span><span class="sxs-lookup"><span data-stu-id="11203-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="11203-939">Cosmos DB biedt een programmeermodel voor het uitvoeren op basis van JavaScript-toepassingslogica rechtstreeks op de verzamelingen met opgeslagen procedures en triggers.</span><span class="sxs-lookup"><span data-stu-id="11203-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="11203-940">De JavaScript-logica geregistreerd op het niveau van een verzameling kan databasebewerkingen uitvoeren op de bewerkingen op de documenten van de opgegeven verzameling vervolgens uitgeven.</span><span class="sxs-lookup"><span data-stu-id="11203-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="11203-941">Deze bewerkingen zijn verpakt in een ambient ACID-transactions.</span><span class="sxs-lookup"><span data-stu-id="11203-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="11203-942">Het volgende voorbeeld laat zien hoe de queryDocuments op de server in JavaScript API gebruiken om te maken van query's van binnen opgeslagen procedures en triggers.</span><span class="sxs-lookup"><span data-stu-id="11203-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

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

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="11203-943"><a id="References"></a>Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="11203-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="11203-944">[Inleiding tot Azure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="11203-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="11203-945">Azure SQL voor Cosmos-DB-specificatie</span><span class="sxs-lookup"><span data-stu-id="11203-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="11203-946">Azure Cosmos DB .NET-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="11203-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="11203-947">[Azure Cosmos DB Consistentieniveaus][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="11203-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="11203-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="11203-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="11203-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="11203-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="11203-950">JavaScript-specificatie [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="11203-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="11203-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="11203-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="11203-952">Van evaluatietechnieken voor grote databases query [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="11203-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="11203-953">Queryverwerking in parallelle relationele databasesystemen, IEEE Computer samenleving Press, 1994</span><span class="sxs-lookup"><span data-stu-id="11203-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="11203-954">Lu, Ooi, Tan queryverwerking in parallelle relationele databasesystemen, IEEE Computer samenleving Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="11203-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="11203-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: een niet zodat vreemde taal voor gegevensverwerking, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="11203-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="11203-956">G.</span><span class="sxs-lookup"><span data-stu-id="11203-956">G.</span></span> <span data-ttu-id="11203-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="11203-957">Graefe.</span></span> <span data-ttu-id="11203-958">Het framework trapsgewijs voor queryoptimalisatie.</span><span class="sxs-lookup"><span data-stu-id="11203-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="11203-959">IEEE-gegevens eng</span><span class="sxs-lookup"><span data-stu-id="11203-959">IEEE Data Eng.</span></span> <span data-ttu-id="11203-960">Bull., 18, lid 3: 1995.</span><span class="sxs-lookup"><span data-stu-id="11203-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md