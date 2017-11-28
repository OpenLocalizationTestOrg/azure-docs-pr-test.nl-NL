---
title: aaaServer-JavaScript programmeren voor Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe toouse Azure Cosmos DB toowrite opgeslagen procedures, databasetriggers en de gebruiker gedefinieerde functies (UDF's) in JavaScript. Gebruik database programing tips en meer.
keywords: Databasetriggers, opgeslagen procedure, opgeslagen procedure, database-programma, sproc, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="5a57c-105">Azure DB Cosmos programmeren-server: opgeslagen procedures, databasetriggers en UDF's</span><span class="sxs-lookup"><span data-stu-id="5a57c-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="5a57c-106">Meer informatie over hoe Azure Cosmos DB taal geïntegreerd, transactionele uitvoering van JavaScript kan ontwikkelaars schrijven **opgeslagen procedures**, **triggers** en **de gebruiker gedefinieerde functies (UDF's)** systeemeigen in een [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5a57c-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="5a57c-107">Hiermee kunt u toowrite database programma toepassingslogica die kan worden verzonden en rechtstreeks uitgevoerd op Hallo database opslag partities.</span><span class="sxs-lookup"><span data-stu-id="5a57c-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="5a57c-108">We raden aan ophalen gestart door kijken Hallo volgende video waar Andrew Liu biedt voor een korte inleiding tooCosmos DB van server-side '-database-programmeermodel.</span><span class="sxs-lookup"><span data-stu-id="5a57c-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="5a57c-109">Keer vervolgens terug toothis artikel, waarin u leert Hallo-antwoorden toohello vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a57c-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="5a57c-110">Hoe schrijf ik een een opgeslagen procedure, trigger of UDF met JavaScript?</span><span class="sxs-lookup"><span data-stu-id="5a57c-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="5a57c-111">Hoe garandeert Cosmos DB ACID</span><span class="sxs-lookup"><span data-stu-id="5a57c-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="5a57c-112">Hoe werken transacties in Cosmos-database?</span><span class="sxs-lookup"><span data-stu-id="5a57c-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="5a57c-113">Wat zijn vooraf activeert en na activeert en hoe schrijf ik een?</span><span class="sxs-lookup"><span data-stu-id="5a57c-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="5a57c-114">Hoe ik registreren en uitvoeren van een opgeslagen procedure, trigger of UDF in een RESTful manier met behulp van HTTP?</span><span class="sxs-lookup"><span data-stu-id="5a57c-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="5a57c-115">Cosmos DB SDK's zijn beschikbaar toocreate en uitvoeren van opgeslagen procedures, triggers en UDF's?</span><span class="sxs-lookup"><span data-stu-id="5a57c-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="5a57c-116">Inleiding tooStored Procedure en UDF programmeren</span><span class="sxs-lookup"><span data-stu-id="5a57c-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="5a57c-117">Deze benadering van *'JavaScript als een moderne dag T-SQL'* toepassingsontwikkelaars van Hallo complexiteit van het systeem niet-overeenkomende typen en -technologieën voor object-relationele gegevens maakt.</span><span class="sxs-lookup"><span data-stu-id="5a57c-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="5a57c-118">Er wordt ook een aantal ingebouwde voordelen die gebruikte toobuild uitgebreide toepassingen worden kunnen:</span><span class="sxs-lookup"><span data-stu-id="5a57c-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="5a57c-119">**Procedurele logica:** JavaScript als een hoog niveau programmeertaal biedt een uitgebreide en vertrouwd interface tooexpress bedrijfsregels in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="5a57c-120">U kunt complexe reeksen operations dichter toohello gegevens kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5a57c-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="5a57c-121">**Atomische transacties:** Cosmos DB wordt gegarandeerd dat de bewerkingen die worden uitgevoerd binnen een enkele opgeslagen procedure of trigger database atomic zijn.</span><span class="sxs-lookup"><span data-stu-id="5a57c-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="5a57c-122">Hiermee kunt een toepassing gerelateerde bewerkingen in één batch combineren zodat ze allemaal slagen of geen van beide slagen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="5a57c-123">**Prestaties:** Hallo feit JSON typesysteem voor intrinsiek toegewezen toohello Javascript-taal is en is ook Hallo basic-eenheid voor opslag in Cosmos DB kunt u een aantal optimalisaties zoals vertraagde materialisatie van JSON-documenten in Hallo buffer toepassingen en zodat ze beschikbaar op aanvraag toohello code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="5a57c-124">Er zijn meer prestatievoordelen die zijn gekoppeld aan back-upfunctie zakelijke logica toohello database:</span><span class="sxs-lookup"><span data-stu-id="5a57c-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="5a57c-125">Batchverwerking: ontwikkelaars kunnen groep bewerkingen zoals ingevoegd en deze bulksgewijs te verzenden.</span><span class="sxs-lookup"><span data-stu-id="5a57c-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="5a57c-126">Hallo verkeer netwerklatentie kosten en Hallo store overhead toocreate afzonderlijke transacties aanzienlijk worden verminderd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="5a57c-127">Vooraf compilatie – Cosmos DB precompiles opgeslagen procedures, triggers en door de gebruiker gedefinieerde functies (UDF's) tooavoid JavaScript compilatie kosten voor elke aanroep.</span><span class="sxs-lookup"><span data-stu-id="5a57c-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="5a57c-128">Hallo overhead van het bouwen van Hallo byte code voor Hallo procedurele logica is afgelost tooa minimale waarde.</span><span class="sxs-lookup"><span data-stu-id="5a57c-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="5a57c-129">Sequentiëren – veel bewerkingen moet een neveneffect ('trigger') die mogelijk het uitvoeren van een of meer secundaire store-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="5a57c-130">Behalve atomisch, is dit meer zodat als de toohello server verplaatst.</span><span class="sxs-lookup"><span data-stu-id="5a57c-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="5a57c-131">**Inkapseling:** opgeslagen procedures kunnen worden gebruikt toogroup bedrijfsregels in te schakelen op één plek.</span><span class="sxs-lookup"><span data-stu-id="5a57c-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="5a57c-132">Dit heeft twee voordelen:</span><span class="sxs-lookup"><span data-stu-id="5a57c-132">This has two advantages:</span></span>
  * <span data-ttu-id="5a57c-133">Een abstractielaag boven op Hallo onbewerkte gegevens, zodat gegevens architecten tooevolve hun toepassingen onafhankelijk van Hallo gegevens wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="5a57c-134">Dit is vooral nuttig wanneer Hallo gegevens schema minder vanwege toohello brosse veronderstellingen die toobe standaard uitbreidbaar in toepassing hello wellicht als ze rechtstreeks toodeal met gegevens hebben.</span><span class="sxs-lookup"><span data-stu-id="5a57c-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="5a57c-135">Deze abstractie kan bedrijven hun gegevens beveiligen door af te stroomlijnen Hallo toegang via Hallo-scripts.</span><span class="sxs-lookup"><span data-stu-id="5a57c-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="5a57c-136">Hallo maken en de uitvoering van de databasetriggers, opgeslagen procedure en aangepaste query's wordt ondersteund door Hallo [REST-API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), en [client-SDK's](documentdb-sdk-dotnet.md) op verschillende platforms, waaronder .NET, Node.js en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5a57c-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="5a57c-137">Deze zelfstudie wordt gebruikgemaakt van Hallo [Node.js-SDK met Q](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntaxis en het gebruik van opgeslagen procedures, triggers en UDF's.</span><span class="sxs-lookup"><span data-stu-id="5a57c-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="5a57c-138">Opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="5a57c-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="5a57c-139">Voorbeeld: Een eenvoudige opgeslagen procedure schrijven</span><span class="sxs-lookup"><span data-stu-id="5a57c-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="5a57c-140">Laten we beginnen met een eenvoudige opgeslagen procedure die een antwoord 'Hallo wereld' geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="5a57c-141">Opgeslagen procedures worden geregistreerd per verzameling en kunnen worden uitgevoerd op een document en bijlage aanwezig zijn in die verzameling.</span><span class="sxs-lookup"><span data-stu-id="5a57c-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="5a57c-142">Hallo volgende fragment toont hoe tooregister Hallo helloWorld opgeslagen procedure met een verzameling.</span><span class="sxs-lookup"><span data-stu-id="5a57c-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="5a57c-143">Zodra Hallo opgeslagen procedure is geregistreerd, kunnen we uitgevoerd op Hallo verzameling en gelezen Hallo resultaten terug op het Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="5a57c-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="5a57c-144">Hallo context-object biedt toegang tooall bewerkingen die kunnen worden uitgevoerd op Cosmos databaseopslag, evenals toegang tot toohello aanvraag en antwoord-objecten.</span><span class="sxs-lookup"><span data-stu-id="5a57c-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="5a57c-145">In dit geval gebruikt we Hallo object tooset Hallo antwoordtekst van Hallo-antwoord dat back toohello client is verzonden.</span><span class="sxs-lookup"><span data-stu-id="5a57c-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="5a57c-146">Raadpleeg voor meer informatie, toohello [Azure Cosmos DB JavaScript server SDK-documentatie](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="5a57c-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="5a57c-147">Laat het ons uitvouwt op dit voorbeeld en voeg meer verwante functionaliteit database toohello opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="5a57c-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="5a57c-148">Opgeslagen procedures kunnen maken, bijwerken, lezen, opvragen en documenten en bijlagen binnen Hallo verzameling verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="5a57c-149">Voorbeeld: Een document een opgeslagen procedure toocreate schrijft</span><span class="sxs-lookup"><span data-stu-id="5a57c-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="5a57c-150">Hallo volgende fragment toont hoe toouse Hallo context-object toointeract met Cosmos-DB-resources.</span><span class="sxs-lookup"><span data-stu-id="5a57c-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="5a57c-151">Deze opgeslagen procedure neemt als invoer documentToCreate, Hallo hoofdtekst van een document toobe gemaakt in de huidige verzameling Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a57c-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="5a57c-152">Alle dergelijke bewerkingen zijn asynchroon en zijn afhankelijk van retouraanroepen van JavaScript-functie.</span><span class="sxs-lookup"><span data-stu-id="5a57c-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="5a57c-153">Hallo-callback-functie heeft twee parameters, één voor Hallo foutobject geval Hallo-bewerking is mislukt en één voor Hallo-object gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a57c-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="5a57c-154">Binnen het Hallo-callback kunnen gebruikers Hallo uitzondering verwerken of een fout.</span><span class="sxs-lookup"><span data-stu-id="5a57c-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="5a57c-155">Als een retouraanroep niet opgegeven is en er een fout is, hello Azure Cosmos DB runtime een fout genereert.</span><span class="sxs-lookup"><span data-stu-id="5a57c-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="5a57c-156">Hallo-callback genereert een fout in Hallo bovenstaande voorbeeld als Hallo-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="5a57c-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="5a57c-157">Anders wordt Hallo-id van Hallo document gemaakt als de berichttekst Hallo van Hallo antwoord toohello client ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5a57c-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="5a57c-158">Hier ziet u hoe u deze opgeslagen procedure uitvoeren met de invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="5a57c-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="5a57c-159">Opmerking dat deze procedure opgeslagen kan worden gewijzigd tootake een matrix van document instanties als invoer en maken ze allemaal in dezelfde opgeslagen Hallo procedure kan worden uitgevoerd in plaats van meerdere netwerk toocreate ze afzonderlijk aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="5a57c-160">Dit kan gebruikte tooimplement een efficiënte bulksgewijs importfunctie voor Cosmos-DB (Zie verderop in deze zelfstudie) zijn.</span><span class="sxs-lookup"><span data-stu-id="5a57c-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="5a57c-161">Hallo-voorbeeld beschreven gedemonstreerd hoe toouse opgeslagen procedures.</span><span class="sxs-lookup"><span data-stu-id="5a57c-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="5a57c-162">We hebben later in Hallo zelfstudie triggers en door de gebruiker gedefinieerde functies (UDF's).</span><span class="sxs-lookup"><span data-stu-id="5a57c-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="5a57c-163">Programma databasetransacties</span><span class="sxs-lookup"><span data-stu-id="5a57c-163">Database program transactions</span></span>
<span data-ttu-id="5a57c-164">Transactie in een typische database kan worden gedefinieerd als een reeks bewerkingen die worden uitgevoerd als één logische eenheid van het werk.</span><span class="sxs-lookup"><span data-stu-id="5a57c-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="5a57c-165">Elke transactie biedt **ACID garanties**.</span><span class="sxs-lookup"><span data-stu-id="5a57c-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="5a57c-166">ACID is een bekende acroniem die voor de vier eigenschappen - atomisch, consistentie, isolatie en duurzaamheid staat.</span><span class="sxs-lookup"><span data-stu-id="5a57c-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="5a57c-167">Kort samengevat kunt atomisch zorgt ervoor dat alle Hallo werk binnen een transactie wordt behandeld als één eenheid waar beide alles is doorgevoerd of none.</span><span class="sxs-lookup"><span data-stu-id="5a57c-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="5a57c-168">Consistentie zorgt ervoor dat gegevens Hallo altijd in goede staat verkeren interne over transacties is.</span><span class="sxs-lookup"><span data-stu-id="5a57c-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="5a57c-169">Isolatie zorgt ervoor dat geen twee transacties verstoren elkaar – algemeen, de meeste commerciële systemen Geef meerdere isolatieniveaus die kunnen worden gebruikt op basis van de behoeften van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="5a57c-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="5a57c-170">Duurzaamheid zorgt ervoor dat elke wijziging die vastgelegd in de database Hallo altijd aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="5a57c-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="5a57c-171">In de Cosmos-DB JavaScript wordt gehost in Hallo geheugenruimte Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="5a57c-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="5a57c-172">Daarom verzoeken in opgeslagen procedures en triggers uitvoeren in Hallo hetzelfde bereik van een databasesessie.</span><span class="sxs-lookup"><span data-stu-id="5a57c-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="5a57c-173">Hierdoor Cosmos DB tooguarantee ACID voor alle bewerkingen die deel van één opgeslagen procedure/trigger uitmaken.</span><span class="sxs-lookup"><span data-stu-id="5a57c-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="5a57c-174">Houd rekening met de volgende Hallo opgeslagen proceduredefinitie:</span><span class="sxs-lookup"><span data-stu-id="5a57c-174">Consider hello following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="5a57c-175">Deze opgeslagen procedure maakt gebruik van transacties binnen een gaming-app tootrade items tussen twee spelers in één bewerking.</span><span class="sxs-lookup"><span data-stu-id="5a57c-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="5a57c-176">Hallo opgeslagen procedure pogingen tooread twee documenten die elke overeenkomende id's van de toohello-speler als argument wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="5a57c-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="5a57c-177">Als beide player-documenten zijn gevonden, updates Hallo opgeslagen procedure Hallo documenten door hun items wisselen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="5a57c-178">Als er fouten op Hallo pad optreden, genereert het een JavaScript-uitzondering die impliciet Hallo transactie afgebroken.</span><span class="sxs-lookup"><span data-stu-id="5a57c-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="5a57c-179">Als hello verzameling Hallo opgeslagen procedure is geregistreerd op basis van een verzameling van één partitie, wordt hello transactie is binnen het bereik tooall Hallo documenten binnen Hallo verzameling.</span><span class="sxs-lookup"><span data-stu-id="5a57c-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="5a57c-180">Als Hallo verzameling is gepartitioneerd, worden de opgeslagen procedures uitgevoerd in transactiebereik Hallo van een sleutel met één partitie.</span><span class="sxs-lookup"><span data-stu-id="5a57c-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="5a57c-181">Elke opgeslagen procedure-uitvoering moet een waarde voor de partitiesleutel corresponderende toohello bereik Hallo transactie moet worden uitgevoerd onder vervolgens bevatten.</span><span class="sxs-lookup"><span data-stu-id="5a57c-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="5a57c-182">Zie voor meer informatie [Azure Cosmos DB partitioneren](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="5a57c-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="5a57c-183">Commit- en rollback</span><span class="sxs-lookup"><span data-stu-id="5a57c-183">Commit and rollback</span></span>
<span data-ttu-id="5a57c-184">Transacties zijn systeemeigen en nauw geïntegreerd in Cosmos-database JavaScript-programmeermodel.</span><span class="sxs-lookup"><span data-stu-id="5a57c-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="5a57c-185">Binnen een JavaScript-functie, worden alle bewerkingen automatisch ingepakt onder één transactie.</span><span class="sxs-lookup"><span data-stu-id="5a57c-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="5a57c-186">Als hello JavaScript is voltooid zonder een uitzondering, Hallo operations toohello-database zijn doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="5a57c-187">Hallo 'BEGIN TRANSACTION' en 'COMMIT TRANSACTION' instructies in relationele databases zijn in feite impliciete in Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="5a57c-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="5a57c-188">Als er een uitzondering die wordt doorgegeven vanuit de Hallo script, wordt JavaScript-runtime Cosmos-database teruggedraaid Hallo hele transactie.</span><span class="sxs-lookup"><span data-stu-id="5a57c-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="5a57c-189">Zoals in Hallo eerder is bijvoorbeeld uitzondering opgetreden effectief gelijkwaardige tooa 'ROLLBACK TRANSACTION' in Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="5a57c-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="5a57c-190">Gegevensconsistentie</span><span class="sxs-lookup"><span data-stu-id="5a57c-190">Data consistency</span></span>
<span data-ttu-id="5a57c-191">Opgeslagen procedures en triggers worden altijd uitgevoerd op de primaire replica Hallo van hello Azure DB die Cosmos-container.</span><span class="sxs-lookup"><span data-stu-id="5a57c-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="5a57c-192">Dit zorgt ervoor dat leesbewerkingen van binnen procedures aanbieding sterke consistentie opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="5a57c-193">Query's op basis van de gebruiker gedefinieerde functies kunnen worden uitgevoerd op de primaire hello of een secundaire replica, maar wij niet garanderen toomeet hello consistentieniveau aangevraagd door de juiste replica Hallo kiezen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="5a57c-194">Begrensde uitvoering</span><span class="sxs-lookup"><span data-stu-id="5a57c-194">Bounded execution</span></span>
<span data-ttu-id="5a57c-195">Alle bewerkingen van de Cosmos-DB moeten voltooid binnen de opgegeven Hallo-server aanvragen van de time-outduur.</span><span class="sxs-lookup"><span data-stu-id="5a57c-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="5a57c-196">Deze beperking geldt ook tooJavaScript functies (opgeslagen procedures, triggers en gebruiker gedefinieerde functies).</span><span class="sxs-lookup"><span data-stu-id="5a57c-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="5a57c-197">Als een bewerking niet wordt voltooid met deze termijn, Hallo transactie wordt teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="5a57c-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="5a57c-198">JavaScript-functies moeten worden voltooid binnen de tijdslimiet Hallo of implementeren van een voortzetting op basis van model toobatch/hervatten uitvoering.</span><span class="sxs-lookup"><span data-stu-id="5a57c-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="5a57c-199">In de volgorde toosimplify ontwikkeling van opgeslagen procedures en triggers toohandle tijdslimiet, alle functies onder Hallo verzamelingsobject (voor het maken, lezen, vervangen en verwijderen van documenten en bijlagen) retourneren een Booleaanse waarde die aangeeft of die bewerking wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="5a57c-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="5a57c-200">Als deze waarde false is, is het een indicatie dat de tijdslimiet Hallo over tooexpire en die procedure Hallo van uitvoering inpakken moet.</span><span class="sxs-lookup"><span data-stu-id="5a57c-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="5a57c-201">Bewerkingen in de wachtrij voorafgaande toohello eerste niet-geaccepteerde store bewerking zijn toocomplete gegarandeerd als Hallo opgeslagen procedure is voltooid in de tijd en geen aanvullende aanvragen niet in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5a57c-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="5a57c-202">JavaScript-functies worden ook begrensd op resourceverbruik.</span><span class="sxs-lookup"><span data-stu-id="5a57c-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="5a57c-203">Cosmos DB reserveert doorvoer per verzameling op basis van de grootte van een databaseaccount Hallo ingericht.</span><span class="sxs-lookup"><span data-stu-id="5a57c-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="5a57c-204">Doorvoer wordt uitgedrukt in termen van genormaliseerde eenheid van de CPU, geheugen en i/o-verbruik aanvraageenheden of RUs genoemd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="5a57c-205">JavaScript-functies kunnen gebruiken om een groot aantal RUs binnen een korte periode en mogelijk ophalen snelheid beperkte als Hallo collector is bereikt.</span><span class="sxs-lookup"><span data-stu-id="5a57c-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="5a57c-206">In quarantaine geplaatste tooensure beschikbaarheid van primitieve databasebewerkingen kunnen ook een resource intensieve opgeslagen procedures zijn.</span><span class="sxs-lookup"><span data-stu-id="5a57c-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="5a57c-207">Voorbeeld: Bulksgewijs importeren van gegevens in een database-programma</span><span class="sxs-lookup"><span data-stu-id="5a57c-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="5a57c-208">Hieronder volgt een voorbeeld van een opgeslagen procedure die documenten toobulk importeren in een verzameling is geschreven.</span><span class="sxs-lookup"><span data-stu-id="5a57c-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="5a57c-209">Opmerking hoe Hallo opgeslagen procedure ingangen begrensd worden uitgevoerd door te controleren Hallo Booleaanse waarde retourneren vanuit createDocument en vervolgens maakt gebruik van het aantal documenten in elke aanroep van Hallo opgeslagen procedure tootrack en hervatten voortgang wordt ingevoegd in batches Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a57c-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="5a57c-210"><a id="trigger"></a>Databasetriggers</span><span class="sxs-lookup"><span data-stu-id="5a57c-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="5a57c-211">Vooraf databasetriggers</span><span class="sxs-lookup"><span data-stu-id="5a57c-211">Database pre-triggers</span></span>
<span data-ttu-id="5a57c-212">Cosmos DB biedt triggers die zijn uitgevoerd of geactiveerd door een bewerking op een document.</span><span class="sxs-lookup"><span data-stu-id="5a57c-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="5a57c-213">U kunt bijvoorbeeld een vooraf trigger opgeven wanneer u bij het maken van een document: deze vooraf trigger wordt uitgevoerd voordat het Hallo-document wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a57c-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="5a57c-214">Hallo Hieronder volgt een voorbeeld van hoe vooraf triggers mag gebruikte toovalidate Hallo eigenschappen van een document dat wordt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="5a57c-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="5a57c-215">En bijbehorende clientzijde registratie van Node.js-code voor de trigger Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="5a57c-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="5a57c-216">Vooraf triggers kunnen geen invoer parameters hebben.</span><span class="sxs-lookup"><span data-stu-id="5a57c-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="5a57c-217">Hallo request-object kan aanvraagbericht voor gebruikte toomanipulate Hallo Hallo bewerking gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="5a57c-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="5a57c-218">Hier Hallo vooraf trigger wordt uitgevoerd met het maken van een document Hallo en Hallo-bericht aanvraagtekst Hallo document toobe gemaakt in JSON-indeling bevat.</span><span class="sxs-lookup"><span data-stu-id="5a57c-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="5a57c-219">Wanneer triggers zijn geregistreerd, kunnen gebruikers Hallo-bewerkingen die kan worden uitgevoerd met opgeven.</span><span class="sxs-lookup"><span data-stu-id="5a57c-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="5a57c-220">Deze trigger is gemaakt met TriggerOperation.Create, wat betekent dat de volgende Hallo is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="5a57c-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="5a57c-221">Na databasetriggers</span><span class="sxs-lookup"><span data-stu-id="5a57c-221">Database post-triggers</span></span>
<span data-ttu-id="5a57c-222">Na triggers, zoals pre triggers zijn gekoppeld aan een bewerking op een document en geen invoerparameters bevatten geen onderneemt.</span><span class="sxs-lookup"><span data-stu-id="5a57c-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="5a57c-223">Ze worden uitgevoerd **nadat** Hallo-bewerking is voltooid, en hebben toegang tot toohello response-bericht dat toohello client wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="5a57c-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="5a57c-224">Hallo volgende voorbeeld ziet u na triggers in actie:</span><span class="sxs-lookup"><span data-stu-id="5a57c-224">hello following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="5a57c-225">Hallo trigger kan worden geregistreerd, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="5a57c-226">Deze trigger Hallo metagegevensdocument opgevraagd en bijgewerkt met informatie over Hallo nieuw gemaakte document.</span><span class="sxs-lookup"><span data-stu-id="5a57c-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="5a57c-227">Één ding dat is het belangrijk toonote hello **transactionele** uitvoering van triggers in Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="5a57c-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="5a57c-228">Deze na trigger wordt uitgevoerd als onderdeel van Hallo dezelfde transactie als Hallo maken van het originele document Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a57c-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="5a57c-229">Dus als we Veroorzaak een exception van Hallo na trigger (zeg als we document kan niet tooupdate Hallo-metagegevens zijn), de hele transactie Hallo zal mislukken en worden teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="5a57c-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="5a57c-230">Er is geen document wordt gemaakt en wordt een uitzondering geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="5a57c-231"><a id="udf"></a>Gebruiker gedefinieerde functies</span><span class="sxs-lookup"><span data-stu-id="5a57c-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="5a57c-232">Gebruiker gedefinieerde functies (UDF's) zijn gebruikte tooextend hello DocumentDB API SQL query language-grammatica en aangepaste bedrijfslogica implementeren.</span><span class="sxs-lookup"><span data-stu-id="5a57c-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="5a57c-233">Ze kunnen alleen worden aangeroepen vanuit in query's.</span><span class="sxs-lookup"><span data-stu-id="5a57c-233">They can only be called from inside queries.</span></span> <span data-ttu-id="5a57c-234">Ze hebben geen toegang tot toohello context-object en toobe gebruikt als alleen-compute JavaScript zijn bedoeld.</span><span class="sxs-lookup"><span data-stu-id="5a57c-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="5a57c-235">Daarom kunnen UDF's worden uitgevoerd op secundaire replica's van Hallo Cosmos-DB-service.</span><span class="sxs-lookup"><span data-stu-id="5a57c-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="5a57c-236">Hallo volgende voorbeeld maakt een UDF toocalculate inkomstenbelasting op basis van de tarieven voor verschillende inkomsten vierkante haken, en gebruikt vervolgens het binnen een toofind query alle mensen die meer dan 20.000 $ betaald belastingen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="5a57c-237">Hallo UDF kan vervolgens worden gebruikt in query's zoals in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a57c-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="5a57c-238">JavaScript-taal geïntegreerd query API</span><span class="sxs-lookup"><span data-stu-id="5a57c-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="5a57c-239">Bovendien tooissuing query met behulp van de DocumentDB SQL-grammatica's hello serverzijde SDK kunt u tooperform geoptimaliseerde query's op basis van een beheersen JavaScript-interface zonder dat daarvoor kennis van SQL.</span><span class="sxs-lookup"><span data-stu-id="5a57c-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="5a57c-240">Hallo JavaScript query die API u tooprogrammatically build-query's kunt door een predikaat functies wordt doorgegeven in de chainable functie aanroept met een syntaxis bekend-tooECMAScript5 matrix dient te worden en populaire JavaScript-bibliotheken zoals lodash.</span><span class="sxs-lookup"><span data-stu-id="5a57c-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="5a57c-241">Query's worden geparseerd door Hallo JavaScript-runtime toobe efficiënt met behulp van Azure Cosmos DB indices uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="5a57c-242">`__`(double liggend streepje) is een alias te`getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="5a57c-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="5a57c-243">Met andere woorden, u kunt `__` of `getContext().getCollection()` tooaccess Hallo API JavaScript-query.</span><span class="sxs-lookup"><span data-stu-id="5a57c-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="5a57c-244">Ondersteunde functies omvatten:</span><span class="sxs-lookup"><span data-stu-id="5a57c-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="5a57c-245">
<b>... chain(). waarde ([retouraanroep] [, opties])</b>
</span><span class="sxs-lookup"><span data-stu-id="5a57c-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="5a57c-246">Start een keten-aanroep die moet worden afgesloten met value().</span><span class="sxs-lookup"><span data-stu-id="5a57c-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5a57c-247">
<b>filter (predicateFunction [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5a57c-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5a57c-248">Voer met behulp van een predicaatfunctie die resulteert in waar/onwaar in volgorde toofilter in/out invoerdocumenten in de resulterende set Hallo Hallo filtert.</span><span class="sxs-lookup"><span data-stu-id="5a57c-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="5a57c-249">Dit gedrag vergelijkbaar tooa WHERE-component in SQL.</span><span class="sxs-lookup"><span data-stu-id="5a57c-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5a57c-250">
<b>kaart (transformationFunction [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5a57c-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5a57c-251">Van toepassing is een projectie krijgt een transformatiefunctie waarbij elke invoer item tooa JavaScript-object of een waarde toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="5a57c-252">Dit is het gedrag vergelijkbaar tooa component SELECT van SQL.</span><span class="sxs-lookup"><span data-stu-id="5a57c-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5a57c-253">
<b>pluck ([propertyName] [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5a57c-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5a57c-254">Dit is een snelkoppeling naar een kaart die uit elk item invoer Hallo-waarde van één eigenschap haalt.</span><span class="sxs-lookup"><span data-stu-id="5a57c-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5a57c-255">
<b>plat ([isShallow] [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5a57c-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5a57c-256">Combineert en matrices van elk item invoer in één matrix tooa worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="5a57c-257">Dit is het gedrag vergelijkbaar tooSelectMany in LINQ.</span><span class="sxs-lookup"><span data-stu-id="5a57c-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5a57c-258">
<b>sortBy ([predicate] [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5a57c-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5a57c-259">Levert een nieuwe reeks documenten Hallo documenten in Hallo invoerdocument stream in oplopende volgorde met Hallo predicaat gegeven wordt gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="5a57c-260">Dit is het gedrag vergelijkbaar tooa ORDER BY-component in SQL.</span><span class="sxs-lookup"><span data-stu-id="5a57c-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5a57c-261">
<b>sortByDescending ([predicate] [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5a57c-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5a57c-262">Levert een nieuwe set van documenten Hallo documenten in Hallo invoerdocument stream in aflopende volgorde met Hallo predicaat gegeven wordt gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="5a57c-263">Dit is het gedrag vergelijkbaar tooa x DESC ORDER BY-component in SQL.</span><span class="sxs-lookup"><span data-stu-id="5a57c-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="5a57c-264">Als opgenomen binnen een predikaat en/of selector-functies, opvragen hello volgende JavaScript-constructs automatisch geoptimaliseerde toorun rechtstreeks op Azure Cosmos DB indexen:</span><span class="sxs-lookup"><span data-stu-id="5a57c-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="5a57c-265">Eenvoudige operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="5a57c-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="5a57c-266">Letterlijke waarden, met inbegrip van Hallo object letterlijke: {}</span><span class="sxs-lookup"><span data-stu-id="5a57c-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="5a57c-267">var, return</span><span class="sxs-lookup"><span data-stu-id="5a57c-267">var, return</span></span>

<span data-ttu-id="5a57c-268">Hallo volgende JavaScript-constructs komen niet ophalen geoptimaliseerd voor Azure Cosmos DB indexen:</span><span class="sxs-lookup"><span data-stu-id="5a57c-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="5a57c-269">Transportbesturing (bijvoorbeeld als, terwijl)</span><span class="sxs-lookup"><span data-stu-id="5a57c-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="5a57c-270">Functieaanroepen</span><span class="sxs-lookup"><span data-stu-id="5a57c-270">Function calls</span></span>

<span data-ttu-id="5a57c-271">Zie voor meer informatie onze [serverzijde JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="5a57c-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="5a57c-272">Voorbeeld: Een opgeslagen procedure met behulp van API-Hallo JavaScript query schrijven</span><span class="sxs-lookup"><span data-stu-id="5a57c-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="5a57c-273">Hallo volgende codevoorbeeld is een voorbeeld van hoe Hallo API JavaScript-Query kan worden gebruikt in de context van een opgeslagen procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a57c-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="5a57c-274">Hallo opgeslagen procedure voegt een document, dat is opgegeven door een invoerparameter en updates van met een metagegevensdocument, Hallo `__.filter()` methode met minimaal, maxSize en totalSize op basis van de eigenschap size Hallo invoer van het document.</span><span class="sxs-lookup"><span data-stu-id="5a57c-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="5a57c-275">SQL tooJavascript referentieoverzicht</span><span class="sxs-lookup"><span data-stu-id="5a57c-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="5a57c-276">Hallo geeft volgende tabel verschillende SQL-query's en Hallo bijbehorende JavaScript-query's.</span><span class="sxs-lookup"><span data-stu-id="5a57c-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="5a57c-277">Als het document sleutels met SQL-query's (bijvoorbeeld `doc.id`) zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="5a57c-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="5a57c-278">SQL</span><span class="sxs-lookup"><span data-stu-id="5a57c-278">SQL</span></span>| <span data-ttu-id="5a57c-279">Query die JavaScript API</span><span class="sxs-lookup"><span data-stu-id="5a57c-279">JavaScript Query API</span></span>|<span data-ttu-id="5a57c-280">Onderstaande beschrijving</span><span class="sxs-lookup"><span data-stu-id="5a57c-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="5a57c-281">SELECTEER *</span><span class="sxs-lookup"><span data-stu-id="5a57c-281">SELECT *</span></span><br><span data-ttu-id="5a57c-282">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="5a57c-282">FROM docs</span></span>| <span data-ttu-id="5a57c-283">{__.map(Function(doc)</span><span class="sxs-lookup"><span data-stu-id="5a57c-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="5a57c-284">&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc;</span><span class="sxs-lookup"><span data-stu-id="5a57c-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="5a57c-285">});</span><span class="sxs-lookup"><span data-stu-id="5a57c-285">});</span></span>|<span data-ttu-id="5a57c-286">1</span><span class="sxs-lookup"><span data-stu-id="5a57c-286">1</span></span>|
|<span data-ttu-id="5a57c-287">Selecteer docs.id, docs.message als gegevenstarieven in rekening, docs.actions</span><span class="sxs-lookup"><span data-stu-id="5a57c-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="5a57c-288">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="5a57c-288">FROM docs</span></span>|<span data-ttu-id="5a57c-289">{__.map(Function(doc)</span><span class="sxs-lookup"><span data-stu-id="5a57c-289">__.map(function(doc) {</span></span><br><span data-ttu-id="5a57c-290">&nbsp;&nbsp;&nbsp;&nbsp;{retourneren</span><span class="sxs-lookup"><span data-stu-id="5a57c-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="5a57c-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ID: doc.id,</span><span class="sxs-lookup"><span data-stu-id="5a57c-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="5a57c-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bericht: doc.message,</span><span class="sxs-lookup"><span data-stu-id="5a57c-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="5a57c-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Actions:doc.Actions</span><span class="sxs-lookup"><span data-stu-id="5a57c-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="5a57c-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="5a57c-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="5a57c-295">});</span><span class="sxs-lookup"><span data-stu-id="5a57c-295">});</span></span>|<span data-ttu-id="5a57c-296">2</span><span class="sxs-lookup"><span data-stu-id="5a57c-296">2</span></span>|
|<span data-ttu-id="5a57c-297">SELECTEER *</span><span class="sxs-lookup"><span data-stu-id="5a57c-297">SELECT *</span></span><br><span data-ttu-id="5a57c-298">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="5a57c-298">FROM docs</span></span><br><span data-ttu-id="5a57c-299">WAAR docs.id="X998_Y998 '</span><span class="sxs-lookup"><span data-stu-id="5a57c-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="5a57c-300">{__.filter(Function(doc)</span><span class="sxs-lookup"><span data-stu-id="5a57c-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="5a57c-301">&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc.id === 'X998_Y998';</span><span class="sxs-lookup"><span data-stu-id="5a57c-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="5a57c-302">});</span><span class="sxs-lookup"><span data-stu-id="5a57c-302">});</span></span>|<span data-ttu-id="5a57c-303">3</span><span class="sxs-lookup"><span data-stu-id="5a57c-303">3</span></span>|
|<span data-ttu-id="5a57c-304">SELECTEER *</span><span class="sxs-lookup"><span data-stu-id="5a57c-304">SELECT *</span></span><br><span data-ttu-id="5a57c-305">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="5a57c-305">FROM docs</span></span><br><span data-ttu-id="5a57c-306">WAAR ARRAY_CONTAINS (documenten. Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="5a57c-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="5a57c-307">{__.filter(Function(x)</span><span class="sxs-lookup"><span data-stu-id="5a57c-307">__.filter(function(x) {</span></span><br><span data-ttu-id="5a57c-308">&nbsp;&nbsp;&nbsp;&nbsp;retourneren van x.Tags & & x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="5a57c-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="5a57c-309">});</span><span class="sxs-lookup"><span data-stu-id="5a57c-309">});</span></span>|<span data-ttu-id="5a57c-310">4</span><span class="sxs-lookup"><span data-stu-id="5a57c-310">4</span></span>|
|<span data-ttu-id="5a57c-311">Selecteer docs.id, docs.message als bericht</span><span class="sxs-lookup"><span data-stu-id="5a57c-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="5a57c-312">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="5a57c-312">FROM docs</span></span><br><span data-ttu-id="5a57c-313">WAAR docs.id="X998_Y998 '</span><span class="sxs-lookup"><span data-stu-id="5a57c-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="5a57c-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="5a57c-314">__.chain()</span></span><br><span data-ttu-id="5a57c-315">&nbsp;&nbsp;&nbsp;&nbsp;{.filter(function(doc)</span><span class="sxs-lookup"><span data-stu-id="5a57c-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="5a57c-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc.id === 'X998_Y998';</span><span class="sxs-lookup"><span data-stu-id="5a57c-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="5a57c-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5a57c-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5a57c-318">&nbsp;&nbsp;&nbsp;&nbsp;{.map(function(doc)</span><span class="sxs-lookup"><span data-stu-id="5a57c-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="5a57c-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{retourneren</span><span class="sxs-lookup"><span data-stu-id="5a57c-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="5a57c-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ID: doc.id,</span><span class="sxs-lookup"><span data-stu-id="5a57c-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="5a57c-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bericht: doc.message</span><span class="sxs-lookup"><span data-stu-id="5a57c-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="5a57c-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="5a57c-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="5a57c-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5a57c-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5a57c-324">.Value();</span><span class="sxs-lookup"><span data-stu-id="5a57c-324">.value();</span></span>|<span data-ttu-id="5a57c-325">5</span><span class="sxs-lookup"><span data-stu-id="5a57c-325">5</span></span>|
|<span data-ttu-id="5a57c-326">De SELECT VALUE-tag</span><span class="sxs-lookup"><span data-stu-id="5a57c-326">SELECT VALUE tag</span></span><br><span data-ttu-id="5a57c-327">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="5a57c-327">FROM docs</span></span><br><span data-ttu-id="5a57c-328">Voeg de tag IN documenten. Labels</span><span class="sxs-lookup"><span data-stu-id="5a57c-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="5a57c-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="5a57c-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="5a57c-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="5a57c-330">__.chain()</span></span><br><span data-ttu-id="5a57c-331">&nbsp;&nbsp;&nbsp;&nbsp;{.filter(function(doc)</span><span class="sxs-lookup"><span data-stu-id="5a57c-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="5a57c-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc retourneren. Labels & & Array.isArray (doc. Tags);</span><span class="sxs-lookup"><span data-stu-id="5a57c-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="5a57c-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5a57c-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5a57c-334">&nbsp;&nbsp;&nbsp;&nbsp;{.sortBy(function(doc)</span><span class="sxs-lookup"><span data-stu-id="5a57c-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="5a57c-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc._ts;</span><span class="sxs-lookup"><span data-stu-id="5a57c-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="5a57c-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5a57c-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5a57c-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("tags")</span><span class="sxs-lookup"><span data-stu-id="5a57c-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="5a57c-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="5a57c-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="5a57c-339">&nbsp;&nbsp;&nbsp;&nbsp;.Value()</span><span class="sxs-lookup"><span data-stu-id="5a57c-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="5a57c-340">6</span><span class="sxs-lookup"><span data-stu-id="5a57c-340">6</span></span>|

<span data-ttu-id="5a57c-341">Hallo volgende beschrijvingen uitgelegd elke query Hallo bovenstaande tabel.</span><span class="sxs-lookup"><span data-stu-id="5a57c-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="5a57c-342">Resultaten in alle documenten (gepagineerd met vervolgtoken) als is.</span><span class="sxs-lookup"><span data-stu-id="5a57c-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="5a57c-343">Projecten Hallo-id, bericht (alias toomsg) en van alle documenten in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="5a57c-344">Query's voor documenten met Hallo predicaat: id = 'X998_Y998'.</span><span class="sxs-lookup"><span data-stu-id="5a57c-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="5a57c-345">Query's voor documenten die een eigenschap voor Tags en labels hebben, is een matrix met Hallo waarde 123.</span><span class="sxs-lookup"><span data-stu-id="5a57c-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="5a57c-346">Query's voor documenten met een predicaat id = "X998_Y998" en vervolgens projecten Hallo-id en -berichten (alias toomsg).</span><span class="sxs-lookup"><span data-stu-id="5a57c-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="5a57c-347">Filters voor documenten die een matrixeigenschap, Tags, hebben en resulterende documenten Hallo sorteren op Hallo _ts system tijdstempeleigenschap, en vervolgens projecteert + Hallo labels matrix worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="5a57c-348">Runtime-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="5a57c-348">Runtime support</span></span>
<span data-ttu-id="5a57c-349">[DocumentDB-JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) biedt ondersteuning voor Hallo HALLO de meeste functies van JavaScript-taal als gestandaardiseerde door gangbare [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="5a57c-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="5a57c-350">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="5a57c-350">Security</span></span>
<span data-ttu-id="5a57c-351">JavaScript opgeslagen procedures en triggers zijn sandbox zodat Hallo gevolgen van een script niet toohello andere gelekt kunnen zonder tussenkomst van Hallo snapshot-isolatie voor transactie op databaseniveau Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a57c-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="5a57c-352">Hallo-runtime-omgevingen zijn gegroepeerd maar gereinigd van Hallo context na elke uitvoering.</span><span class="sxs-lookup"><span data-stu-id="5a57c-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="5a57c-353">Ze zijn daarom toobe gegarandeerd veilig van onbedoelde nadelen van elkaar.</span><span class="sxs-lookup"><span data-stu-id="5a57c-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="5a57c-354">Vooraf compileren</span><span class="sxs-lookup"><span data-stu-id="5a57c-354">Pre-compilation</span></span>
<span data-ttu-id="5a57c-355">Opgeslagen procedures, triggers en UDF's zijn impliciet vooraf gecompileerde toohello byte notatie in volgorde tooavoid compilatie kosten gelijktijdig Hallo met elke aanroep van het script.</span><span class="sxs-lookup"><span data-stu-id="5a57c-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="5a57c-356">Dit zorgt ervoor dat de aanroepen van opgeslagen procedures zijn snel en een lage footprint hebben.</span><span class="sxs-lookup"><span data-stu-id="5a57c-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="5a57c-357">Ondersteuning voor client-SDK</span><span class="sxs-lookup"><span data-stu-id="5a57c-357">Client SDK support</span></span>
<span data-ttu-id="5a57c-358">In aanvulling toohello DocumentDB-API voor [Node.js](documentdb-sdk-node.md) Azure DB die Cosmos-client heeft [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), en [Python SDK's](documentdb-sdk-python.md) voor Hallo DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="5a57c-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="5a57c-359">Opgeslagen procedures, triggers en UDF's kunnen worden gemaakt en wordt uitgevoerd met een van deze SDK's ook.</span><span class="sxs-lookup"><span data-stu-id="5a57c-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="5a57c-360">Hallo volgende voorbeeld wordt getoond hoe toocreate en een opgeslagen procedure met behulp van Hallo .NET-client wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="5a57c-361">Opmerking hoe Hallo .NET-typen worden doorgegeven in Hallo opgeslagen procedure als JSON en terug te lezen.</span><span class="sxs-lookup"><span data-stu-id="5a57c-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="5a57c-362">In dit voorbeeld laat zien hoe toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate een vooraf trigger en een document te maken met de Hallo trigger is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5a57c-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="5a57c-363">En Hallo volgende voorbeeld ziet u hoe toocreate een gebruiker gedefinieerde functie (UDF) en deze gebruiken in een [DocumentDB API SQL-query](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="5a57c-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="5a57c-364">REST API</span><span class="sxs-lookup"><span data-stu-id="5a57c-364">REST API</span></span>
<span data-ttu-id="5a57c-365">Alle Azure DB die Cosmos-bewerkingen kunnen worden uitgevoerd op een RESTful manier.</span><span class="sxs-lookup"><span data-stu-id="5a57c-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="5a57c-366">Opgeslagen procedures, triggers en de gebruiker gedefinieerde functies kunnen worden geregistreerd in een verzameling met behulp van HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="5a57c-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="5a57c-367">Hallo Hieronder volgt een voorbeeld van hoe u een opgeslagen procedure tooregister:</span><span class="sxs-lookup"><span data-stu-id="5a57c-367">hello following is an example of how tooregister a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="5a57c-368">Hallo opgeslagen procedure is geregistreerd door het uitvoeren van een POST-aanvraag tegen Hallo URI Hallo databases/testdb/colls/testColl/sprocs met Hallo hoofdtekst die toocreate opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="5a57c-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="5a57c-369">Triggers en UDF's kunnen op dezelfde manier worden geregistreerd door uitgifte van een POST tegen/triggers en /udfs respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="5a57c-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="5a57c-370">Deze opgeslagen procedure kan vervolgens worden uitgevoerd door uitgifte van een POST-aanvraag tegen de resourcekoppeling:</span><span class="sxs-lookup"><span data-stu-id="5a57c-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="5a57c-371">Hier wordt Hallo invoer toohello opgeslagen procedure doorgegeven in de aanvraagtekst Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a57c-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="5a57c-372">Houd er rekening mee dat Hallo-invoer is doorgegeven als een JSON-matrix van invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="5a57c-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="5a57c-373">Hallo opgeslagen procedure vergt Hallo eerste invoer als een document dat een antwoordtekst.</span><span class="sxs-lookup"><span data-stu-id="5a57c-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="5a57c-374">Hallo-antwoord die is ontvangen, is als volgt:</span><span class="sxs-lookup"><span data-stu-id="5a57c-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="5a57c-375">In tegenstelling tot opgeslagen procedures, triggers kunnen niet rechtstreeks worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a57c-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="5a57c-376">In plaats daarvan worden uitgevoerd als onderdeel van een bewerking op een document.</span><span class="sxs-lookup"><span data-stu-id="5a57c-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="5a57c-377">We kunnen Hallo triggers toorun opgeven met een aanvraag met behulp van HTTP-headers.</span><span class="sxs-lookup"><span data-stu-id="5a57c-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="5a57c-378">Hallo volgt aanvraag toocreate een document.</span><span class="sxs-lookup"><span data-stu-id="5a57c-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="5a57c-379">Hier is Hallo vooraf trigger toobe uitvoeren met Hallo-aanvraag opgegeven in x-ms-documentdb-pre-trigger-include Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="5a57c-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="5a57c-380">Navenant, eventuele na triggers zijn opgegeven in x-ms-documentdb-post-trigger-include Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="5a57c-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="5a57c-381">Houd er rekening mee dat zowel vóór en na triggers kunnen worden opgegeven voor een bepaalde aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5a57c-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="5a57c-382">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="5a57c-382">Sample code</span></span>
<span data-ttu-id="5a57c-383">U vindt meer serverzijde codevoorbeelden (inclusief [bulk verwijderen](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), en [bijwerken](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) op onze [GitHub-opslagplaats](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="5a57c-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="5a57c-384">Wilt u uw geweldig opgeslagen procedure tooshare?</span><span class="sxs-lookup"><span data-stu-id="5a57c-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="5a57c-385">Stuur ons een pull-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5a57c-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5a57c-386">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a57c-386">Next steps</span></span>
<span data-ttu-id="5a57c-387">Zodra u hebt een of meer opgeslagen procedures, triggers en gebruiker gedefinieerde functies die zijn gemaakt, kunt u ze laden en ze weergeven in Azure portal met behulp van Data Explorer Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a57c-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="5a57c-388">Wellicht vindt u ook de volgende Hallo verwijzingen en bronnen die nuttig zijn bij uw pad toolearn meer informatie over Azure Cosmos dB programmeren-server:</span><span class="sxs-lookup"><span data-stu-id="5a57c-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="5a57c-389">Azure Cosmos DB SDK 's</span><span class="sxs-lookup"><span data-stu-id="5a57c-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="5a57c-390">DocumentDB-Studio</span><span class="sxs-lookup"><span data-stu-id="5a57c-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="5a57c-391">JSON</span><span class="sxs-lookup"><span data-stu-id="5a57c-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="5a57c-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="5a57c-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="5a57c-393">Veilige en draagbare Database uitbreidbaarheid</span><span class="sxs-lookup"><span data-stu-id="5a57c-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="5a57c-394">Service Oriented Architecture van de Database</span><span class="sxs-lookup"><span data-stu-id="5a57c-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="5a57c-395">Hallo .NET Runtime in Microsoft SQL server die als host fungeert</span><span class="sxs-lookup"><span data-stu-id="5a57c-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

