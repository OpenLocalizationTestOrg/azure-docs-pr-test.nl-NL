---
title: Programmeren-server JavaScript voor Azure Cosmos DB | Microsoft Docs
description: Informatie over het gebruik van Azure DB die Cosmos om te schrijven van opgeslagen procedures, databasetriggers en de gebruiker gedefinieerde functies (UDF's) in JavaScript. Gebruik database programing tips en meer.
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
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="19763-105">Azure DB Cosmos programmeren-server: opgeslagen procedures, databasetriggers en UDF's</span><span class="sxs-lookup"><span data-stu-id="19763-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="19763-106">Meer informatie over hoe Azure Cosmos DB taal geïntegreerd, transactionele uitvoering van JavaScript kan ontwikkelaars schrijven **opgeslagen procedures**, **triggers** en **de gebruiker gedefinieerde functies (UDF's)** systeemeigen in een [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="19763-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="19763-107">Hiermee kunt u toepassingslogica van het database-programma dat kan worden verzonden en rechtstreeks uitgevoerd op de database-opslag-partities schrijven.</span><span class="sxs-lookup"><span data-stu-id="19763-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="19763-108">Het is raadzaam om aan de slag door het bekijken van de volgende video, waarbij Andrew Liu een korte inleiding tot programmeermodel Cosmos-database-server-side '-database bevat.</span><span class="sxs-lookup"><span data-stu-id="19763-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="19763-109">Keer vervolgens terug naar dit artikel, waarin u leert de antwoorden op de volgende vragen:</span><span class="sxs-lookup"><span data-stu-id="19763-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="19763-110">Hoe schrijf ik een een opgeslagen procedure, trigger of UDF met JavaScript?</span><span class="sxs-lookup"><span data-stu-id="19763-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="19763-111">Hoe garandeert Cosmos DB ACID</span><span class="sxs-lookup"><span data-stu-id="19763-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="19763-112">Hoe werken transacties in Cosmos-database?</span><span class="sxs-lookup"><span data-stu-id="19763-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="19763-113">Wat zijn vooraf activeert en na activeert en hoe schrijf ik een?</span><span class="sxs-lookup"><span data-stu-id="19763-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="19763-114">Hoe ik registreren en uitvoeren van een opgeslagen procedure, trigger of UDF in een RESTful manier met behulp van HTTP?</span><span class="sxs-lookup"><span data-stu-id="19763-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="19763-115">Wat Cosmos DB SDK's zijn beschikbaar voor het maken en uitvoeren, opgeslagen procedures, triggers en UDF's?</span><span class="sxs-lookup"><span data-stu-id="19763-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="19763-116">Inleiding tot de opgeslagen Procedure en UDF programmering</span><span class="sxs-lookup"><span data-stu-id="19763-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="19763-117">Deze benadering van *'JavaScript als een moderne dag T-SQL'* toepassingsontwikkelaars van de complexiteit van het systeem niet-overeenkomende typen en -technologieën voor object-relationele gegevens maakt.</span><span class="sxs-lookup"><span data-stu-id="19763-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="19763-118">Er wordt ook een aantal ingebouwde voordelen die kunnen worden gebruikt om uitgebreide toepassingen te bouwen:</span><span class="sxs-lookup"><span data-stu-id="19763-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="19763-119">**Procedurele logica:** JavaScript als een hoog niveau programmeertaal biedt een uitgebreide en vertrouwd interface bedrijfslogica Express.</span><span class="sxs-lookup"><span data-stu-id="19763-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="19763-120">U kunt complexe reeksen operations dichter in de gegevens kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19763-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="19763-121">**Atomische transacties:** Cosmos DB wordt gegarandeerd dat de bewerkingen die worden uitgevoerd binnen een enkele opgeslagen procedure of trigger database atomic zijn.</span><span class="sxs-lookup"><span data-stu-id="19763-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="19763-122">Hiermee kunt een toepassing gerelateerde bewerkingen in één batch combineren zodat ze allemaal slagen of geen van beide slagen.</span><span class="sxs-lookup"><span data-stu-id="19763-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="19763-123">**Prestaties:** het feit dat JSON intrinsiek is toegewezen aan het typesysteem Javascript-taal en ook de basiseenheid voor opslag in Cosmos DB is kunt u een aantal optimalisaties zoals vertraagde materialisatie van JSON-documenten in de buffergroep en ze op verzoek beschikbaar voor het uitvoeren van code.</span><span class="sxs-lookup"><span data-stu-id="19763-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="19763-124">Er zijn meer prestatievoordelen die zijn gekoppeld aan back-upfunctie bedrijfsregels in te schakelen naar de database:</span><span class="sxs-lookup"><span data-stu-id="19763-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="19763-125">Batchverwerking: ontwikkelaars kunnen groep bewerkingen zoals ingevoegd en deze bulksgewijs te verzenden.</span><span class="sxs-lookup"><span data-stu-id="19763-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="19763-126">De netwerklatentie verkeer de kosten en de store-overhead voor het maken van afzonderlijke transacties aanzienlijk verminderd.</span><span class="sxs-lookup"><span data-stu-id="19763-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="19763-127">Vooraf compilatie – Cosmos DB precompiles opgeslagen procedures, triggers en door de gebruiker gedefinieerde functies (UDF's) om te voorkomen dat JavaScript compilatie kosten voor elke aanroep.</span><span class="sxs-lookup"><span data-stu-id="19763-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="19763-128">De overhead van het bouwen van de byte-code voor de procedurele logica is afgelost op een minimale waarde.</span><span class="sxs-lookup"><span data-stu-id="19763-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="19763-129">Sequentiëren – veel bewerkingen moet een neveneffect ('trigger') die mogelijk het uitvoeren van een of meer secundaire store-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="19763-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="19763-130">Behalve atomisch, maar dit is meer zodat wanneer verplaatst naar de server.</span><span class="sxs-lookup"><span data-stu-id="19763-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="19763-131">**Inkapseling:** opgeslagen procedures kunnen worden gebruikt voor het groeperen van bedrijfsregels in te schakelen op één plek.</span><span class="sxs-lookup"><span data-stu-id="19763-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="19763-132">Dit heeft twee voordelen:</span><span class="sxs-lookup"><span data-stu-id="19763-132">This has two advantages:</span></span>
  * <span data-ttu-id="19763-133">Een abstractielaag boven op de onbewerkte gegevens, zodat gegevens architecten ontwikkelen hun toepassingen onafhankelijk van de gegevens worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="19763-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="19763-134">Dit is vooral nuttig wanneer de gegevens zonder schema, vanwege de brosse veronderstellingen die worden standaard uitbreidbaar in de toepassing moeten mogelijk als ze hebben om te gaan met de gegevens rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="19763-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="19763-135">Deze abstractie kan bedrijven hun gegevens beveiligen door af te stroomlijnen de toegang van de scripts.</span><span class="sxs-lookup"><span data-stu-id="19763-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="19763-136">Het maken en de uitvoering van de databasetriggers, opgeslagen procedure en aangepaste query's wordt ondersteund door de [REST-API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), en [client-SDK's](documentdb-sdk-dotnet.md) op verschillende platforms, waaronder .NET, Node.js en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="19763-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="19763-137">Deze zelfstudie wordt gebruikgemaakt van de [Node.js-SDK met Q](http://azure.github.io/azure-documentdb-node-q/) ter illustratie van de syntaxis en het gebruik van opgeslagen procedures, triggers en UDF's.</span><span class="sxs-lookup"><span data-stu-id="19763-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="19763-138">Opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="19763-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="19763-139">Voorbeeld: Een eenvoudige opgeslagen procedure schrijven</span><span class="sxs-lookup"><span data-stu-id="19763-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="19763-140">Laten we beginnen met een eenvoudige opgeslagen procedure die een antwoord 'Hallo wereld' geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="19763-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="19763-141">Opgeslagen procedures worden geregistreerd per verzameling en kunnen worden uitgevoerd op een document en bijlage aanwezig zijn in die verzameling.</span><span class="sxs-lookup"><span data-stu-id="19763-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="19763-142">Het volgende fragment toont hoe de helloWorld opgeslagen procedure registreren bij een verzameling.</span><span class="sxs-lookup"><span data-stu-id="19763-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="19763-143">Zodra de opgeslagen procedure is geregistreerd, kunnen we uitgevoerd op de verzameling en bekijk de resultaten weer op de client.</span><span class="sxs-lookup"><span data-stu-id="19763-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="19763-144">Het contextobject biedt toegang tot alle bewerkingen die kunnen worden uitgevoerd op Cosmos databaseopslag, evenals de toegang tot de aanvraag en antwoord-objecten.</span><span class="sxs-lookup"><span data-stu-id="19763-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="19763-145">In dit geval wordt het object response gebruikt om de hoofdtekst van het antwoord dat is verzonden naar de client.</span><span class="sxs-lookup"><span data-stu-id="19763-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="19763-146">Raadpleeg voor meer informatie de [Azure Cosmos DB JavaScript server SDK-documentatie](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="19763-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="19763-147">Laat het ons uitvouwt op dit voorbeeld en voeg dat meer verwante functionaliteit aan de opgeslagen procedure-database.</span><span class="sxs-lookup"><span data-stu-id="19763-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="19763-148">Opgeslagen procedures kunnen maken, bijwerken, lezen, opvragen en verwijderen van documenten en bijlagen binnen de verzameling.</span><span class="sxs-lookup"><span data-stu-id="19763-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="19763-149">Voorbeeld: Een opgeslagen procedure voor het maken van een document schrijven</span><span class="sxs-lookup"><span data-stu-id="19763-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="19763-150">Het volgende fragment toont hoe het context-object gebruiken om te communiceren met de resources van de Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="19763-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

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


<span data-ttu-id="19763-151">Deze opgeslagen procedure neemt als invoer documentToCreate, de hoofdtekst van een document moet worden gemaakt in de huidige verzameling.</span><span class="sxs-lookup"><span data-stu-id="19763-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="19763-152">Alle dergelijke bewerkingen zijn asynchroon en zijn afhankelijk van retouraanroepen van JavaScript-functie.</span><span class="sxs-lookup"><span data-stu-id="19763-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="19763-153">De callbackfunctie heeft twee parameters, één voor het foutobject in geval mislukt de bewerking en één voor het gemaakte object.</span><span class="sxs-lookup"><span data-stu-id="19763-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="19763-154">Binnen de callback kunnen gebruikers de uitzondering verwerken of een fout.</span><span class="sxs-lookup"><span data-stu-id="19763-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="19763-155">Als een retouraanroep niet opgegeven is en er een fout is, wordt in de Azure DB die Cosmos-runtime een fout genereert.</span><span class="sxs-lookup"><span data-stu-id="19763-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="19763-156">De callback genereert een fout opgetreden in het bovenstaande voorbeeld als de bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="19763-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="19763-157">Anders wordt de id van het gemaakte document als de berichttekst van het antwoord op de client ingesteld.</span><span class="sxs-lookup"><span data-stu-id="19763-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="19763-158">Hier ziet u hoe u deze opgeslagen procedure uitvoeren met de invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="19763-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
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


<span data-ttu-id="19763-159">Houd er rekening mee dat deze opgeslagen procedure kan worden aangepast voor het uitvoeren van een matrix van document instanties als invoer en maak ze allemaal in dezelfde opgeslagen procedure uitvoering in plaats van meerdere netwerkaanvragen ze allemaal afzonderlijk maken.</span><span class="sxs-lookup"><span data-stu-id="19763-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="19763-160">Dit kan worden gebruikt voor het implementeren van een efficiënte bulksgewijs importfunctie voor Cosmos-DB (Zie verderop in deze zelfstudie).</span><span class="sxs-lookup"><span data-stu-id="19763-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="19763-161">In het voorbeeld dat wordt beschreven hoe u opgeslagen procedures gedemonstreerd.</span><span class="sxs-lookup"><span data-stu-id="19763-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="19763-162">Wordt uitgelegd triggers en door de gebruiker gedefinieerde functies (UDF's) verderop in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="19763-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="19763-163">Programma databasetransacties</span><span class="sxs-lookup"><span data-stu-id="19763-163">Database program transactions</span></span>
<span data-ttu-id="19763-164">Transactie in een typische database kan worden gedefinieerd als een reeks bewerkingen die worden uitgevoerd als één logische eenheid van het werk.</span><span class="sxs-lookup"><span data-stu-id="19763-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="19763-165">Elke transactie biedt **ACID garanties**.</span><span class="sxs-lookup"><span data-stu-id="19763-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="19763-166">ACID is een bekende acroniem die voor de vier eigenschappen - atomisch, consistentie, isolatie en duurzaamheid staat.</span><span class="sxs-lookup"><span data-stu-id="19763-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="19763-167">Kort samengevat kunt atomisch zorgt ervoor dat alle het werk dat binnen een transactie wordt behandeld als één eenheid waar beide alles is doorgevoerd of none.</span><span class="sxs-lookup"><span data-stu-id="19763-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="19763-168">Consistentie zorgt ervoor dat de gegevens altijd in goede staat verkeren interne over transacties is.</span><span class="sxs-lookup"><span data-stu-id="19763-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="19763-169">Isolatie zorgt ervoor dat geen twee transacties verstoren elkaar – algemeen, de meeste commerciële systemen Geef meerdere isolatieniveaus die kunnen worden gebruikt op basis van de behoeften van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="19763-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="19763-170">Duurzaamheid zorgt ervoor dat elke wijziging die vastgelegd in de database altijd aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="19763-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="19763-171">JavaScript wordt in Cosmos-database gehost in de geheugenruimte als de database.</span><span class="sxs-lookup"><span data-stu-id="19763-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="19763-172">Daarom aanvragen uitgevoerd in opgeslagen procedures en triggers in hetzelfde bereik van een databasesessie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19763-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="19763-173">Hierdoor Cosmos DB ACID voor alle bewerkingen die deel van één opgeslagen procedure/trigger uitmaken te garanderen.</span><span class="sxs-lookup"><span data-stu-id="19763-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="19763-174">Houd rekening met de volgende opgeslagen procedure-definitie:</span><span class="sxs-lookup"><span data-stu-id="19763-174">Consider the following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="19763-175">Deze opgeslagen procedure maakt gebruik van transacties binnen een gaming-app handel items tussen twee spelers in één bewerking.</span><span class="sxs-lookup"><span data-stu-id="19763-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="19763-176">De opgeslagen procedure probeert te lezen van de twee documenten elke overeenkomt met de player-id's als argument doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="19763-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="19763-177">Als beide player-documenten zijn gevonden, werkt de opgeslagen procedure de documenten door hun items wisselen.</span><span class="sxs-lookup"><span data-stu-id="19763-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="19763-178">Als er fouten langs de manier optreden, genereert het een JavaScript-uitzondering die impliciet afbreken van de transactie.</span><span class="sxs-lookup"><span data-stu-id="19763-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="19763-179">Als de verzameling de opgeslagen procedure is geregistreerd op basis van een verzameling van één partitie, wordt de transactie is afgestemd op de documenten binnen de verzameling.</span><span class="sxs-lookup"><span data-stu-id="19763-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="19763-180">Als de verzameling is gepartitioneerd, worden de opgeslagen procedures in het transactiebereik van een enkele partitiesleutel uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="19763-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="19763-181">Elke opgeslagen procedure-uitvoering moet een waarde voor de partitiesleutel overeenkomt met het bereik dat de transactie moet worden uitgevoerd onder vervolgens bevatten.</span><span class="sxs-lookup"><span data-stu-id="19763-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="19763-182">Zie voor meer informatie [Azure Cosmos DB partitioneren](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="19763-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="19763-183">Commit- en rollback</span><span class="sxs-lookup"><span data-stu-id="19763-183">Commit and rollback</span></span>
<span data-ttu-id="19763-184">Transacties zijn systeemeigen en nauw geïntegreerd in Cosmos-database JavaScript-programmeermodel.</span><span class="sxs-lookup"><span data-stu-id="19763-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="19763-185">Binnen een JavaScript-functie, worden alle bewerkingen automatisch ingepakt onder één transactie.</span><span class="sxs-lookup"><span data-stu-id="19763-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="19763-186">Als JavaScript zonder een uitzondering is voltooid, wordt de bewerkingen in de database zijn doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="19763-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="19763-187">De instructies 'BEGIN TRANSACTION' en 'COMMIT TRANSACTION' in relationele databases zijn in feite impliciete in Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="19763-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="19763-188">Als er een uitzondering die wordt doorgegeven vanuit het script, wordt Cosmos-database JavaScript-runtime Draai de hele transactie terug.</span><span class="sxs-lookup"><span data-stu-id="19763-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="19763-189">Zoals u in het vorige voorbeeld, is het effectief gelijk is aan een 'ROLLBACK TRANSACTION' toe aan DB Cosmos om uitzondering opgetreden.</span><span class="sxs-lookup"><span data-stu-id="19763-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="19763-190">Gegevensconsistentie</span><span class="sxs-lookup"><span data-stu-id="19763-190">Data consistency</span></span>
<span data-ttu-id="19763-191">Opgeslagen procedures en triggers worden altijd uitgevoerd op de primaire replica van de Azure DB die Cosmos-container.</span><span class="sxs-lookup"><span data-stu-id="19763-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="19763-192">Dit zorgt ervoor dat leesbewerkingen van binnen procedures aanbieding sterke consistentie opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="19763-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="19763-193">Query's op basis van de gebruiker gedefinieerde functies kunnen worden uitgevoerd op de primaire of elke secundaire replica, maar we ervoor zorgen dat de aangevraagde consistentieniveau te voldoen aan de juiste replica kiezen.</span><span class="sxs-lookup"><span data-stu-id="19763-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="19763-194">Begrensde uitvoering</span><span class="sxs-lookup"><span data-stu-id="19763-194">Bounded execution</span></span>
<span data-ttu-id="19763-195">Alle bewerkingen van de Cosmos-DB moeten voltooid binnen de opgegeven server time-outduur aanvragen.</span><span class="sxs-lookup"><span data-stu-id="19763-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="19763-196">Deze beperking geldt ook voor JavaScript-functies (opgeslagen procedures, triggers en gebruiker gedefinieerde functies).</span><span class="sxs-lookup"><span data-stu-id="19763-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="19763-197">Als een bewerking niet wordt voltooid met deze termijn, de transactie is teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="19763-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="19763-198">JavaScript-functies moeten worden voltooid binnen de tijdslimiet of implementeren van een voortzetting op basis van model voor het uitvoeren van batch/hervatten.</span><span class="sxs-lookup"><span data-stu-id="19763-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="19763-199">Alle functies in het verzamelingsobject (voor het maken, lezen, vervangen en verwijderen van documenten en bijlagen) retourneren om de ontwikkeling van opgeslagen procedures en triggers voor het afhandelen van de tijdslimiet vereenvoudigen, een Booleaanse waarde die aangeeft of die voor deze bewerking wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="19763-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="19763-200">Als deze waarde false is, is het een indicatie dat de tijdslimiet is bijna verlopen en dat de procedure van uitvoering inpakken moet.</span><span class="sxs-lookup"><span data-stu-id="19763-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="19763-201">Bewerkingen in de wachtrij vóór de eerste niet-geaccepteerde-bewerking te voltooien als u de opgeslagen procedure is voltooid in de tijd en niet in een wachtrij geen aanvullende aanvragen meer zijn gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="19763-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="19763-202">JavaScript-functies worden ook begrensd op resourceverbruik.</span><span class="sxs-lookup"><span data-stu-id="19763-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="19763-203">Cosmos DB reserveert doorvoer per verzameling op basis van de ingerichte grootte van een databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="19763-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="19763-204">Doorvoer wordt uitgedrukt in termen van genormaliseerde eenheid van de CPU, geheugen en i/o-verbruik aanvraageenheden of RUs genoemd.</span><span class="sxs-lookup"><span data-stu-id="19763-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="19763-205">JavaScript-functies kunnen gebruiken om een groot aantal RUs binnen een korte periode en mogelijk ophalen snelheid beperkte als de verzameling limiet is bereikt.</span><span class="sxs-lookup"><span data-stu-id="19763-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="19763-206">Resource intensieve opgeslagen procedures kunnen ook in quarantaine zodat de beschikbaarheid van primitieve databasebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="19763-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="19763-207">Voorbeeld: Bulksgewijs importeren van gegevens in een database-programma</span><span class="sxs-lookup"><span data-stu-id="19763-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="19763-208">Hieronder volgt een voorbeeld van een opgeslagen procedure die is geschreven naar bulkimport documenten in een verzameling.</span><span class="sxs-lookup"><span data-stu-id="19763-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="19763-209">Houd er rekening mee hoe de opgeslagen procedure begrensde uitvoering verwerkt door het controleren van de Booleaanse waarde retourneren vanuit createDocument, en gebruikt vervolgens het aantal documenten dat is ingevoegd in elke aanroep van de opgeslagen procedure volgen en voortgang in batches hervatten.</span><span class="sxs-lookup"><span data-stu-id="19763-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="19763-210"><a id="trigger"></a>Databasetriggers</span><span class="sxs-lookup"><span data-stu-id="19763-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="19763-211">Vooraf databasetriggers</span><span class="sxs-lookup"><span data-stu-id="19763-211">Database pre-triggers</span></span>
<span data-ttu-id="19763-212">Cosmos DB biedt triggers die zijn uitgevoerd of geactiveerd door een bewerking op een document.</span><span class="sxs-lookup"><span data-stu-id="19763-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="19763-213">U kunt bijvoorbeeld een vooraf trigger opgeven wanneer u bij het maken van een document: deze vooraf trigger wordt uitgevoerd voordat het document wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19763-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="19763-214">Hier volgt een voorbeeld van hoe vooraf triggers kunnen worden gebruikt voor het valideren van de eigenschappen van een document dat wordt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="19763-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="19763-215">En de bijbehorende Node.js-clientzijde registratiecode voor de trigger:</span><span class="sxs-lookup"><span data-stu-id="19763-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

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


<span data-ttu-id="19763-216">Vooraf triggers kunnen geen invoer parameters hebben.</span><span class="sxs-lookup"><span data-stu-id="19763-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="19763-217">Het request-object kan worden gebruikt voor het bewerken van het aanvraagbericht die zijn gekoppeld aan de bewerking.</span><span class="sxs-lookup"><span data-stu-id="19763-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="19763-218">Hier worden de vooraf trigger wordt uitgevoerd met het maken van een document en de berichttekst van de aanvraag bevat het document moet worden gemaakt in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="19763-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="19763-219">Wanneer triggers zijn geregistreerd, kunnen gebruikers de bewerkingen die kan worden uitgevoerd met opgeven.</span><span class="sxs-lookup"><span data-stu-id="19763-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="19763-220">Deze trigger is gemaakt met TriggerOperation.Create, wat betekent dat het volgende is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="19763-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="19763-221">Na databasetriggers</span><span class="sxs-lookup"><span data-stu-id="19763-221">Database post-triggers</span></span>
<span data-ttu-id="19763-222">Na triggers, zoals pre triggers zijn gekoppeld aan een bewerking op een document en geen invoerparameters bevatten geen onderneemt.</span><span class="sxs-lookup"><span data-stu-id="19763-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="19763-223">Ze worden uitgevoerd **nadat** de bewerking is voltooid en hebben toegang tot het response-bericht dat naar de client wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="19763-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="19763-224">Het volgende voorbeeld ziet u na triggers in actie:</span><span class="sxs-lookup"><span data-stu-id="19763-224">The following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="19763-225">De trigger kan worden geregistreerd, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="19763-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
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


<span data-ttu-id="19763-226">Deze trigger wordt gevraagd om het metagegevensdocument en bijgewerkt met informatie over het zojuist gemaakte document.</span><span class="sxs-lookup"><span data-stu-id="19763-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="19763-227">Één ding dat is belangrijk te weten is de **transactionele** uitvoering van triggers in Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="19763-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="19763-228">Deze na trigger wordt uitgevoerd als onderdeel van de dezelfde transactie als het maken van het originele document.</span><span class="sxs-lookup"><span data-stu-id="19763-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="19763-229">Dus als we Veroorzaak een uitzondering van de na trigger (zeg als we niet bijwerken van het metagegevensdocument), de hele transactie zal mislukken en worden teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="19763-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="19763-230">Er is geen document wordt gemaakt en wordt een uitzondering geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="19763-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="19763-231"><a id="udf"></a>Gebruiker gedefinieerde functies</span><span class="sxs-lookup"><span data-stu-id="19763-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="19763-232">Gebruiker gedefinieerde functies (UDF's) worden gebruikt voor het uitbreiden van de DocumentDB API SQL query language-grammatica en aangepaste bedrijfslogica implementeren.</span><span class="sxs-lookup"><span data-stu-id="19763-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="19763-233">Ze kunnen alleen worden aangeroepen vanuit in query's.</span><span class="sxs-lookup"><span data-stu-id="19763-233">They can only be called from inside queries.</span></span> <span data-ttu-id="19763-234">Ze hebben geen toegang tot het contextobject en zijn bedoeld om te worden gebruikt als JavaScript compute alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="19763-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="19763-235">Daarom kunnen UDF's worden uitgevoerd op secundaire replica's van de Cosmos-DB-service.</span><span class="sxs-lookup"><span data-stu-id="19763-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="19763-236">Het volgende voorbeeld maakt een UDF voor het berekenen van de fiscale op basis van de tarieven voor verschillende inkomsten haken en vervolgens alle mensen die meer dan 20.000 $ betaald belastingen te vinden binnen een query gebruikt.</span><span class="sxs-lookup"><span data-stu-id="19763-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="19763-237">De UDF kan vervolgens worden gebruikt in query's zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="19763-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="19763-238">JavaScript-taal geïntegreerd query API</span><span class="sxs-lookup"><span data-stu-id="19763-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="19763-239">Naast het uitgeven van query's met behulp van de DocumentDB SQL-grammatica, kunt de SDK-serverzijde u uitvoeren geoptimaliseerde query's met een beheersen JavaScript-interface zonder dat daarvoor kennis van SQL.</span><span class="sxs-lookup"><span data-stu-id="19763-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="19763-240">De JavaScript-query die API u programmatisch query's opbouwen kunt door predikaat functies in de chainable functie aanroept met een bekende ECMAScript5 van matrix dient te worden en populaire JavaScript-bibliotheken zoals lodash syntaxis.</span><span class="sxs-lookup"><span data-stu-id="19763-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="19763-241">Query's worden geparseerd door de JavaScript-runtime efficiënt met behulp van Azure Cosmos DB indices worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="19763-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="19763-242">`__`(double liggend streepje) is een alias voor `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="19763-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="19763-243">Met andere woorden, u kunt `__` of `getContext().getCollection()` voor toegang tot de query die JavaScript API.</span><span class="sxs-lookup"><span data-stu-id="19763-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="19763-244">Ondersteunde functies omvatten:</span><span class="sxs-lookup"><span data-stu-id="19763-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="19763-245">
<b>... chain(). waarde ([retouraanroep] [, opties])</b>
</span><span class="sxs-lookup"><span data-stu-id="19763-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="19763-246">Start een keten-aanroep die moet worden afgesloten met value().</span><span class="sxs-lookup"><span data-stu-id="19763-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="19763-247">
<b>filter (predicateFunction [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="19763-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="19763-248">Filtert de invoer met behulp van een predicaatfunctie die resulteert in waar/onwaar om te filteren in/out invoerdocumenten in de resulterende set.</span><span class="sxs-lookup"><span data-stu-id="19763-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="19763-249">Dit is het gedrag vergelijkbaar met een WHERE-component in SQL.</span><span class="sxs-lookup"><span data-stu-id="19763-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="19763-250">
<b>kaart (transformationFunction [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="19763-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="19763-251">Van toepassing is een projectie een transformatiefunctie waarbij elk item invoer wordt toegewezen aan een JavaScript-object of een waarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="19763-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="19763-252">Dit is het gedrag vergelijkbaar met een SELECT-clausule in SQL.</span><span class="sxs-lookup"><span data-stu-id="19763-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="19763-253">
<b>pluck ([propertyName] [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="19763-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="19763-254">Dit is een snelkoppeling naar een kaart waarmee de waarde van één eigenschap worden opgehaald van elk item invoer.</span><span class="sxs-lookup"><span data-stu-id="19763-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="19763-255">
<b>plat ([isShallow] [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="19763-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="19763-256">Combineert en matrices van elk item invoer in op één array worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="19763-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="19763-257">Dit is het gedrag vergelijkbaar met SelectMany in LINQ.</span><span class="sxs-lookup"><span data-stu-id="19763-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="19763-258">
<b>sortBy ([predicate] [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="19763-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="19763-259">Een nieuwe reeks documenten produceren de documenten in de stroom invoerdocument in oplopende volgorde met behulp van het gegeven predicaat wordt gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="19763-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="19763-260">Dit is het gedrag vergelijkbaar met een component ORDER BY van SQL.</span><span class="sxs-lookup"><span data-stu-id="19763-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="19763-261">
<b>sortByDescending ([predicate] [, opties] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="19763-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="19763-262">Een nieuwe reeks documenten produceren de documenten in de stroom invoerdocument in aflopende volgorde, met behulp van het gegeven predicaat wordt gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="19763-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="19763-263">Dit is het gedrag vergelijkbaar met een x DESC ORDER BY-clausule in SQL.</span><span class="sxs-lookup"><span data-stu-id="19763-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="19763-264">Wanneer opgenomen binnen een predikaat en/of selector-functies, krijgen automatisch de volgende JavaScript-constructs geoptimaliseerd direct op Azure Cosmos DB indexen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="19763-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="19763-265">Eenvoudige operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="19763-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="19763-266">Letterlijke waarden, met inbegrip van het object letterlijke: {}</span><span class="sxs-lookup"><span data-stu-id="19763-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="19763-267">var, return</span><span class="sxs-lookup"><span data-stu-id="19763-267">var, return</span></span>

<span data-ttu-id="19763-268">De volgende JavaScript-constructs komen niet ophalen geoptimaliseerd voor Azure Cosmos DB indexen:</span><span class="sxs-lookup"><span data-stu-id="19763-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="19763-269">Transportbesturing (bijvoorbeeld als, terwijl)</span><span class="sxs-lookup"><span data-stu-id="19763-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="19763-270">Functieaanroepen</span><span class="sxs-lookup"><span data-stu-id="19763-270">Function calls</span></span>

<span data-ttu-id="19763-271">Zie voor meer informatie onze [serverzijde JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="19763-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="19763-272">Voorbeeld: Een opgeslagen procedure met behulp van de query die JavaScript API schrijven</span><span class="sxs-lookup"><span data-stu-id="19763-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="19763-273">Het volgende codevoorbeeld is een voorbeeld van hoe de JavaScript-API-Query kan worden gebruikt in de context van een opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="19763-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="19763-274">De opgeslagen procedure voegt een document, dat is opgegeven door een invoerparameter en updates van metagegevens van een document, met behulp van de `__.filter()` methode met minimaal, maxSize en totalSize op basis van de eigenschap size het invoerdocument.</span><span class="sxs-lookup"><span data-stu-id="19763-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="19763-275">SQL voor Javascript-referentieoverzicht</span><span class="sxs-lookup"><span data-stu-id="19763-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="19763-276">De volgende tabel geeft verschillende SQL-query's en de bijbehorende JavaScript-query's.</span><span class="sxs-lookup"><span data-stu-id="19763-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="19763-277">Als het document sleutels met SQL-query's (bijvoorbeeld `doc.id`) zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="19763-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="19763-278">SQL</span><span class="sxs-lookup"><span data-stu-id="19763-278">SQL</span></span>| <span data-ttu-id="19763-279">Query die JavaScript API</span><span class="sxs-lookup"><span data-stu-id="19763-279">JavaScript Query API</span></span>|<span data-ttu-id="19763-280">Onderstaande beschrijving</span><span class="sxs-lookup"><span data-stu-id="19763-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="19763-281">SELECTEER *</span><span class="sxs-lookup"><span data-stu-id="19763-281">SELECT *</span></span><br><span data-ttu-id="19763-282">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="19763-282">FROM docs</span></span>| <span data-ttu-id="19763-283">{__.map(Function(doc)</span><span class="sxs-lookup"><span data-stu-id="19763-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="19763-284">&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc;</span><span class="sxs-lookup"><span data-stu-id="19763-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="19763-285">});</span><span class="sxs-lookup"><span data-stu-id="19763-285">});</span></span>|<span data-ttu-id="19763-286">1</span><span class="sxs-lookup"><span data-stu-id="19763-286">1</span></span>|
|<span data-ttu-id="19763-287">Selecteer docs.id, docs.message als gegevenstarieven in rekening, docs.actions</span><span class="sxs-lookup"><span data-stu-id="19763-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="19763-288">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="19763-288">FROM docs</span></span>|<span data-ttu-id="19763-289">{__.map(Function(doc)</span><span class="sxs-lookup"><span data-stu-id="19763-289">__.map(function(doc) {</span></span><br><span data-ttu-id="19763-290">&nbsp;&nbsp;&nbsp;&nbsp;{retourneren</span><span class="sxs-lookup"><span data-stu-id="19763-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="19763-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ID: doc.id,</span><span class="sxs-lookup"><span data-stu-id="19763-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="19763-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bericht: doc.message,</span><span class="sxs-lookup"><span data-stu-id="19763-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="19763-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Actions:doc.Actions</span><span class="sxs-lookup"><span data-stu-id="19763-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="19763-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="19763-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="19763-295">});</span><span class="sxs-lookup"><span data-stu-id="19763-295">});</span></span>|<span data-ttu-id="19763-296">2</span><span class="sxs-lookup"><span data-stu-id="19763-296">2</span></span>|
|<span data-ttu-id="19763-297">SELECTEER *</span><span class="sxs-lookup"><span data-stu-id="19763-297">SELECT *</span></span><br><span data-ttu-id="19763-298">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="19763-298">FROM docs</span></span><br><span data-ttu-id="19763-299">WAAR docs.id="X998_Y998 '</span><span class="sxs-lookup"><span data-stu-id="19763-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="19763-300">{__.filter(Function(doc)</span><span class="sxs-lookup"><span data-stu-id="19763-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="19763-301">&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc.id === 'X998_Y998';</span><span class="sxs-lookup"><span data-stu-id="19763-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="19763-302">});</span><span class="sxs-lookup"><span data-stu-id="19763-302">});</span></span>|<span data-ttu-id="19763-303">3</span><span class="sxs-lookup"><span data-stu-id="19763-303">3</span></span>|
|<span data-ttu-id="19763-304">SELECTEER *</span><span class="sxs-lookup"><span data-stu-id="19763-304">SELECT *</span></span><br><span data-ttu-id="19763-305">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="19763-305">FROM docs</span></span><br><span data-ttu-id="19763-306">WAAR ARRAY_CONTAINS (documenten. Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="19763-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="19763-307">{__.filter(Function(x)</span><span class="sxs-lookup"><span data-stu-id="19763-307">__.filter(function(x) {</span></span><br><span data-ttu-id="19763-308">&nbsp;&nbsp;&nbsp;&nbsp;retourneren van x.Tags & & x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="19763-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="19763-309">});</span><span class="sxs-lookup"><span data-stu-id="19763-309">});</span></span>|<span data-ttu-id="19763-310">4</span><span class="sxs-lookup"><span data-stu-id="19763-310">4</span></span>|
|<span data-ttu-id="19763-311">Selecteer docs.id, docs.message als bericht</span><span class="sxs-lookup"><span data-stu-id="19763-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="19763-312">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="19763-312">FROM docs</span></span><br><span data-ttu-id="19763-313">WAAR docs.id="X998_Y998 '</span><span class="sxs-lookup"><span data-stu-id="19763-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="19763-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="19763-314">__.chain()</span></span><br><span data-ttu-id="19763-315">&nbsp;&nbsp;&nbsp;&nbsp;{.filter(function(doc)</span><span class="sxs-lookup"><span data-stu-id="19763-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="19763-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc.id === 'X998_Y998';</span><span class="sxs-lookup"><span data-stu-id="19763-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="19763-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="19763-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="19763-318">&nbsp;&nbsp;&nbsp;&nbsp;{.map(function(doc)</span><span class="sxs-lookup"><span data-stu-id="19763-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="19763-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{retourneren</span><span class="sxs-lookup"><span data-stu-id="19763-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="19763-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ID: doc.id,</span><span class="sxs-lookup"><span data-stu-id="19763-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="19763-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bericht: doc.message</span><span class="sxs-lookup"><span data-stu-id="19763-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="19763-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="19763-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="19763-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="19763-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="19763-324">.Value();</span><span class="sxs-lookup"><span data-stu-id="19763-324">.value();</span></span>|<span data-ttu-id="19763-325">5</span><span class="sxs-lookup"><span data-stu-id="19763-325">5</span></span>|
|<span data-ttu-id="19763-326">De SELECT VALUE-tag</span><span class="sxs-lookup"><span data-stu-id="19763-326">SELECT VALUE tag</span></span><br><span data-ttu-id="19763-327">VAN documenten</span><span class="sxs-lookup"><span data-stu-id="19763-327">FROM docs</span></span><br><span data-ttu-id="19763-328">Voeg de tag IN documenten. Labels</span><span class="sxs-lookup"><span data-stu-id="19763-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="19763-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="19763-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="19763-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="19763-330">__.chain()</span></span><br><span data-ttu-id="19763-331">&nbsp;&nbsp;&nbsp;&nbsp;{.filter(function(doc)</span><span class="sxs-lookup"><span data-stu-id="19763-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="19763-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc retourneren. Labels & & Array.isArray (doc. Tags);</span><span class="sxs-lookup"><span data-stu-id="19763-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="19763-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="19763-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="19763-334">&nbsp;&nbsp;&nbsp;&nbsp;{.sortBy(function(doc)</span><span class="sxs-lookup"><span data-stu-id="19763-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="19763-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc._ts;</span><span class="sxs-lookup"><span data-stu-id="19763-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="19763-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="19763-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="19763-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("tags")</span><span class="sxs-lookup"><span data-stu-id="19763-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="19763-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="19763-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="19763-339">&nbsp;&nbsp;&nbsp;&nbsp;.Value()</span><span class="sxs-lookup"><span data-stu-id="19763-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="19763-340">6</span><span class="sxs-lookup"><span data-stu-id="19763-340">6</span></span>|

<span data-ttu-id="19763-341">De volgende beschrijvingen uitgelegd elke query in de bovenstaande tabel.</span><span class="sxs-lookup"><span data-stu-id="19763-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="19763-342">Resultaten in alle documenten (gepagineerd met vervolgtoken) als is.</span><span class="sxs-lookup"><span data-stu-id="19763-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="19763-343">De id, het bericht (alias voor bericht) en de actie van alle documenten projecten.</span><span class="sxs-lookup"><span data-stu-id="19763-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="19763-344">Query's voor documenten met het predicaat: id = 'X998_Y998'.</span><span class="sxs-lookup"><span data-stu-id="19763-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="19763-345">Query's voor documenten die een eigenschap voor Tags en labels hebben, is een matrix met de waarde 123.</span><span class="sxs-lookup"><span data-stu-id="19763-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="19763-346">Query's voor documenten met een predicaat id = "X998_Y998" en vervolgens projecteert de id en het bericht (alias voor bericht).</span><span class="sxs-lookup"><span data-stu-id="19763-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="19763-347">Filters voor documenten met een matrixeigenschap, Tags, en de resulterende documenten door de eigenschap _ts timestamp-systeem en projecten sorteert + de matrix labels worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="19763-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="19763-348">Runtime-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="19763-348">Runtime support</span></span>
<span data-ttu-id="19763-349">[DocumentDB-JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) biedt ondersteuning voor de meeste van de algemene JavaScript-taalfuncties als gestandaardiseerde door [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="19763-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="19763-350">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="19763-350">Security</span></span>
<span data-ttu-id="19763-351">JavaScript opgeslagen procedures en triggers zijn sandbox zodat de gevolgen van een script niet naar het andere gelekt komen zonder tussenkomst van de transactie snapshot-isolatie op databaseniveau.</span><span class="sxs-lookup"><span data-stu-id="19763-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="19763-352">De runtimeomgevingen zijn gegroepeerd, maar na elke uitvoering van de context is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="19763-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="19763-353">Ze zijn daarom gegarandeerd veilig van onbedoelde nadelen van elkaar.</span><span class="sxs-lookup"><span data-stu-id="19763-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="19763-354">Vooraf compileren</span><span class="sxs-lookup"><span data-stu-id="19763-354">Pre-compilation</span></span>
<span data-ttu-id="19763-355">Opgeslagen procedures, triggers en UDF's zijn om te voorkomen dat compilatie kosten op het moment van elke aanroep script impliciet vooraf gecompileerde naar de indeling van de code byte.</span><span class="sxs-lookup"><span data-stu-id="19763-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="19763-356">Dit zorgt ervoor dat de aanroepen van opgeslagen procedures zijn snel en een lage footprint hebben.</span><span class="sxs-lookup"><span data-stu-id="19763-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="19763-357">Ondersteuning voor client-SDK</span><span class="sxs-lookup"><span data-stu-id="19763-357">Client SDK support</span></span>
<span data-ttu-id="19763-358">Naast de DocumentDB-API voor [Node.js](documentdb-sdk-node.md) Azure DB die Cosmos-client heeft [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), en [Python SDK's](documentdb-sdk-python.md) voor de DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="19763-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="19763-359">Opgeslagen procedures, triggers en UDF's kunnen worden gemaakt en wordt uitgevoerd met een van deze SDK's ook.</span><span class="sxs-lookup"><span data-stu-id="19763-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="19763-360">Het volgende voorbeeld laat zien hoe kunnen maken en uitvoeren van een opgeslagen procedure met de .NET-client.</span><span class="sxs-lookup"><span data-stu-id="19763-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="19763-361">Houd er rekening mee hoe de .NET-typen zijn doorgegeven naar de opgeslagen procedure als JSON en de inhoud weer.</span><span class="sxs-lookup"><span data-stu-id="19763-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="19763-362">Dit voorbeeld laat zien hoe u de [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) voor het maken van een vooraf trigger en maken van een document met de trigger is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="19763-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

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


<span data-ttu-id="19763-363">En het volgende voorbeeld laat zien hoe door de gebruiker gedefinieerde functies (UDF) maken en deze gebruiken in een [DocumentDB API SQL-query](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="19763-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="19763-364">REST API</span><span class="sxs-lookup"><span data-stu-id="19763-364">REST API</span></span>
<span data-ttu-id="19763-365">Alle Azure DB die Cosmos-bewerkingen kunnen worden uitgevoerd op een RESTful manier.</span><span class="sxs-lookup"><span data-stu-id="19763-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="19763-366">Opgeslagen procedures, triggers en de gebruiker gedefinieerde functies kunnen worden geregistreerd in een verzameling met behulp van HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="19763-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="19763-367">Hier volgt een voorbeeld van hoe u kunt een opgeslagen procedure registreren:</span><span class="sxs-lookup"><span data-stu-id="19763-367">The following is an example of how to register a stored procedure:</span></span>

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


<span data-ttu-id="19763-368">De opgeslagen procedure wordt geregistreerd door een POST-aanvraag tegen de URI-databases/testdb/colls/testColl/sprocs uitvoeren met de hoofdtekst van de opgeslagen procedure maken.</span><span class="sxs-lookup"><span data-stu-id="19763-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="19763-369">Triggers en UDF's kunnen op dezelfde manier worden geregistreerd door uitgifte van een POST tegen/triggers en /udfs respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="19763-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="19763-370">Deze opgeslagen procedure kan vervolgens worden uitgevoerd door uitgifte van een POST-aanvraag tegen de resourcekoppeling:</span><span class="sxs-lookup"><span data-stu-id="19763-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="19763-371">Hier worden de invoer van de opgeslagen procedure wordt doorgegeven in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="19763-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="19763-372">Houd er rekening mee dat de invoer is doorgegeven als een JSON-matrix van invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="19763-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="19763-373">De opgeslagen procedure wordt de eerste invoer als een document dat een antwoordtekst.</span><span class="sxs-lookup"><span data-stu-id="19763-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="19763-374">Het antwoord dat is ontvangen, is als volgt:</span><span class="sxs-lookup"><span data-stu-id="19763-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="19763-375">In tegenstelling tot opgeslagen procedures, triggers kunnen niet rechtstreeks worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="19763-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="19763-376">In plaats daarvan worden uitgevoerd als onderdeel van een bewerking op een document.</span><span class="sxs-lookup"><span data-stu-id="19763-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="19763-377">We kunt opgeven dat de triggers om uit te voeren met een aanvraag met behulp van HTTP-headers.</span><span class="sxs-lookup"><span data-stu-id="19763-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="19763-378">Hieronder vindt een aanvraag voor het maken van een document.</span><span class="sxs-lookup"><span data-stu-id="19763-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="19763-379">Hier worden de trigger vooraf moeten worden uitgevoerd met de aanvraag is opgegeven in de x-ms-documentdb-pre-trigger-include header.</span><span class="sxs-lookup"><span data-stu-id="19763-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="19763-380">Dienovereenkomstig, eventuele na triggers zijn opgegeven in de x-ms-documentdb-post-trigger-include-header.</span><span class="sxs-lookup"><span data-stu-id="19763-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="19763-381">Houd er rekening mee dat zowel vóór en na triggers kunnen worden opgegeven voor een bepaalde aanvraag.</span><span class="sxs-lookup"><span data-stu-id="19763-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="19763-382">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="19763-382">Sample code</span></span>
<span data-ttu-id="19763-383">U vindt meer serverzijde codevoorbeelden (inclusief [bulk verwijderen](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), en [bijwerken](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) op onze [GitHub-opslagplaats](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="19763-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="19763-384">Wilt u uw geweldig opgeslagen procedure delen?</span><span class="sxs-lookup"><span data-stu-id="19763-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="19763-385">Stuur ons een pull-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="19763-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="19763-386">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19763-386">Next steps</span></span>
<span data-ttu-id="19763-387">Zodra u hebt een of meer opgeslagen procedures, triggers en gebruiker gedefinieerde functies die zijn gemaakt, kunt u ze laden en ze weergeven in de Azure-portal met behulp van Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="19763-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="19763-388">Ook kan nuttig voor u de volgende verwijzingen en resources in het pad voor meer informatie over Azure Cosmos dB programmeren-server:</span><span class="sxs-lookup"><span data-stu-id="19763-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="19763-389">Azure Cosmos DB SDK 's</span><span class="sxs-lookup"><span data-stu-id="19763-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="19763-390">DocumentDB-Studio</span><span class="sxs-lookup"><span data-stu-id="19763-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="19763-391">JSON</span><span class="sxs-lookup"><span data-stu-id="19763-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="19763-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="19763-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="19763-393">Veilige en draagbare Database uitbreidbaarheid</span><span class="sxs-lookup"><span data-stu-id="19763-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="19763-394">Service Oriented Architecture van de Database</span><span class="sxs-lookup"><span data-stu-id="19763-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="19763-395">De .NET Runtime in Microsoft SQL server die als host fungeert</span><span class="sxs-lookup"><span data-stu-id="19763-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

