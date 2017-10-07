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
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Azure DB Cosmos programmeren-server: opgeslagen procedures, databasetriggers en UDF's
Meer informatie over hoe Azure Cosmos DB taal geïntegreerd, transactionele uitvoering van JavaScript kan ontwikkelaars schrijven **opgeslagen procedures**, **triggers** en **de gebruiker gedefinieerde functies (UDF's)** systeemeigen in een [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript. Hiermee kunt u toowrite database programma toepassingslogica die kan worden verzonden en rechtstreeks uitgevoerd op Hallo database opslag partities. 

We raden aan ophalen gestart door kijken Hallo volgende video waar Andrew Liu biedt voor een korte inleiding tooCosmos DB van server-side '-database-programmeermodel. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

Keer vervolgens terug toothis artikel, waarin u leert Hallo-antwoorden toohello vragen te volgen:  

* Hoe schrijf ik een een opgeslagen procedure, trigger of UDF met JavaScript?
* Hoe garandeert Cosmos DB ACID
* Hoe werken transacties in Cosmos-database?
* Wat zijn vooraf activeert en na activeert en hoe schrijf ik een?
* Hoe ik registreren en uitvoeren van een opgeslagen procedure, trigger of UDF in een RESTful manier met behulp van HTTP?
* Cosmos DB SDK's zijn beschikbaar toocreate en uitvoeren van opgeslagen procedures, triggers en UDF's?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>Inleiding tooStored Procedure en UDF programmeren
Deze benadering van *'JavaScript als een moderne dag T-SQL'* toepassingsontwikkelaars van Hallo complexiteit van het systeem niet-overeenkomende typen en -technologieën voor object-relationele gegevens maakt. Er wordt ook een aantal ingebouwde voordelen die gebruikte toobuild uitgebreide toepassingen worden kunnen:  

* **Procedurele logica:** JavaScript als een hoog niveau programmeertaal biedt een uitgebreide en vertrouwd interface tooexpress bedrijfsregels in te schakelen. U kunt complexe reeksen operations dichter toohello gegevens kunt uitvoeren.
* **Atomische transacties:** Cosmos DB wordt gegarandeerd dat de bewerkingen die worden uitgevoerd binnen een enkele opgeslagen procedure of trigger database atomic zijn. Hiermee kunt een toepassing gerelateerde bewerkingen in één batch combineren zodat ze allemaal slagen of geen van beide slagen. 
* **Prestaties:** Hallo feit JSON typesysteem voor intrinsiek toegewezen toohello Javascript-taal is en is ook Hallo basic-eenheid voor opslag in Cosmos DB kunt u een aantal optimalisaties zoals vertraagde materialisatie van JSON-documenten in Hallo buffer toepassingen en zodat ze beschikbaar op aanvraag toohello code wordt uitgevoerd. Er zijn meer prestatievoordelen die zijn gekoppeld aan back-upfunctie zakelijke logica toohello database:
  
  * Batchverwerking: ontwikkelaars kunnen groep bewerkingen zoals ingevoegd en deze bulksgewijs te verzenden. Hallo verkeer netwerklatentie kosten en Hallo store overhead toocreate afzonderlijke transacties aanzienlijk worden verminderd. 
  * Vooraf compilatie – Cosmos DB precompiles opgeslagen procedures, triggers en door de gebruiker gedefinieerde functies (UDF's) tooavoid JavaScript compilatie kosten voor elke aanroep. Hallo overhead van het bouwen van Hallo byte code voor Hallo procedurele logica is afgelost tooa minimale waarde.
  * Sequentiëren – veel bewerkingen moet een neveneffect ('trigger') die mogelijk het uitvoeren van een of meer secundaire store-bewerkingen. Behalve atomisch, is dit meer zodat als de toohello server verplaatst. 
* **Inkapseling:** opgeslagen procedures kunnen worden gebruikt toogroup bedrijfsregels in te schakelen op één plek. Dit heeft twee voordelen:
  * Een abstractielaag boven op Hallo onbewerkte gegevens, zodat gegevens architecten tooevolve hun toepassingen onafhankelijk van Hallo gegevens wordt toegevoegd. Dit is vooral nuttig wanneer Hallo gegevens schema minder vanwege toohello brosse veronderstellingen die toobe standaard uitbreidbaar in toepassing hello wellicht als ze rechtstreeks toodeal met gegevens hebben.  
  * Deze abstractie kan bedrijven hun gegevens beveiligen door af te stroomlijnen Hallo toegang via Hallo-scripts.  

Hallo maken en de uitvoering van de databasetriggers, opgeslagen procedure en aangepaste query's wordt ondersteund door Hallo [REST-API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), en [client-SDK's](documentdb-sdk-dotnet.md) op verschillende platforms, waaronder .NET, Node.js en JavaScript.

Deze zelfstudie wordt gebruikgemaakt van Hallo [Node.js-SDK met Q](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntaxis en het gebruik van opgeslagen procedures, triggers en UDF's.   

## <a name="stored-procedures"></a>Opgeslagen procedures
### <a name="example-write-a-simple-stored-procedure"></a>Voorbeeld: Een eenvoudige opgeslagen procedure schrijven
Laten we beginnen met een eenvoudige opgeslagen procedure die een antwoord 'Hallo wereld' geretourneerd.

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


Opgeslagen procedures worden geregistreerd per verzameling en kunnen worden uitgevoerd op een document en bijlage aanwezig zijn in die verzameling. Hallo volgende fragment toont hoe tooregister Hallo helloWorld opgeslagen procedure met een verzameling. 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


Zodra Hallo opgeslagen procedure is geregistreerd, kunnen we uitgevoerd op Hallo verzameling en gelezen Hallo resultaten terug op het Hallo-client. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


Hallo context-object biedt toegang tooall bewerkingen die kunnen worden uitgevoerd op Cosmos databaseopslag, evenals toegang tot toohello aanvraag en antwoord-objecten. In dit geval gebruikt we Hallo object tooset Hallo antwoordtekst van Hallo-antwoord dat back toohello client is verzonden. Raadpleeg voor meer informatie, toohello [Azure Cosmos DB JavaScript server SDK-documentatie](http://azure.github.io/azure-documentdb-js-server/).  

Laat het ons uitvouwt op dit voorbeeld en voeg meer verwante functionaliteit database toohello opgeslagen procedure. Opgeslagen procedures kunnen maken, bijwerken, lezen, opvragen en documenten en bijlagen binnen Hallo verzameling verwijderen.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>Voorbeeld: Een document een opgeslagen procedure toocreate schrijft
Hallo volgende fragment toont hoe toouse Hallo context-object toointeract met Cosmos-DB-resources.

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


Deze opgeslagen procedure neemt als invoer documentToCreate, Hallo hoofdtekst van een document toobe gemaakt in de huidige verzameling Hallo. Alle dergelijke bewerkingen zijn asynchroon en zijn afhankelijk van retouraanroepen van JavaScript-functie. Hallo-callback-functie heeft twee parameters, één voor Hallo foutobject geval Hallo-bewerking is mislukt en één voor Hallo-object gemaakt. Binnen het Hallo-callback kunnen gebruikers Hallo uitzondering verwerken of een fout. Als een retouraanroep niet opgegeven is en er een fout is, hello Azure Cosmos DB runtime een fout genereert.   

Hallo-callback genereert een fout in Hallo bovenstaande voorbeeld als Hallo-bewerking is mislukt. Anders wordt Hallo-id van Hallo document gemaakt als de berichttekst Hallo van Hallo antwoord toohello client ingesteld. Hier ziet u hoe u deze opgeslagen procedure uitvoeren met de invoerparameters.

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


Opmerking dat deze procedure opgeslagen kan worden gewijzigd tootake een matrix van document instanties als invoer en maken ze allemaal in dezelfde opgeslagen Hallo procedure kan worden uitgevoerd in plaats van meerdere netwerk toocreate ze afzonderlijk aanvragen. Dit kan gebruikte tooimplement een efficiënte bulksgewijs importfunctie voor Cosmos-DB (Zie verderop in deze zelfstudie) zijn.   

Hallo-voorbeeld beschreven gedemonstreerd hoe toouse opgeslagen procedures. We hebben later in Hallo zelfstudie triggers en door de gebruiker gedefinieerde functies (UDF's).

## <a name="database-program-transactions"></a>Programma databasetransacties
Transactie in een typische database kan worden gedefinieerd als een reeks bewerkingen die worden uitgevoerd als één logische eenheid van het werk. Elke transactie biedt **ACID garanties**. ACID is een bekende acroniem die voor de vier eigenschappen - atomisch, consistentie, isolatie en duurzaamheid staat.  

Kort samengevat kunt atomisch zorgt ervoor dat alle Hallo werk binnen een transactie wordt behandeld als één eenheid waar beide alles is doorgevoerd of none. Consistentie zorgt ervoor dat gegevens Hallo altijd in goede staat verkeren interne over transacties is. Isolatie zorgt ervoor dat geen twee transacties verstoren elkaar – algemeen, de meeste commerciële systemen Geef meerdere isolatieniveaus die kunnen worden gebruikt op basis van de behoeften van de toepassing hello. Duurzaamheid zorgt ervoor dat elke wijziging die vastgelegd in de database Hallo altijd aanwezig zijn.   

In de Cosmos-DB JavaScript wordt gehost in Hallo geheugenruimte Hallo-database. Daarom verzoeken in opgeslagen procedures en triggers uitvoeren in Hallo hetzelfde bereik van een databasesessie. Hierdoor Cosmos DB tooguarantee ACID voor alle bewerkingen die deel van één opgeslagen procedure/trigger uitmaken. Houd rekening met de volgende Hallo opgeslagen proceduredefinitie:

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

Deze opgeslagen procedure maakt gebruik van transacties binnen een gaming-app tootrade items tussen twee spelers in één bewerking. Hallo opgeslagen procedure pogingen tooread twee documenten die elke overeenkomende id's van de toohello-speler als argument wordt doorgegeven. Als beide player-documenten zijn gevonden, updates Hallo opgeslagen procedure Hallo documenten door hun items wisselen. Als er fouten op Hallo pad optreden, genereert het een JavaScript-uitzondering die impliciet Hallo transactie afgebroken.

Als hello verzameling Hallo opgeslagen procedure is geregistreerd op basis van een verzameling van één partitie, wordt hello transactie is binnen het bereik tooall Hallo documenten binnen Hallo verzameling. Als Hallo verzameling is gepartitioneerd, worden de opgeslagen procedures uitgevoerd in transactiebereik Hallo van een sleutel met één partitie. Elke opgeslagen procedure-uitvoering moet een waarde voor de partitiesleutel corresponderende toohello bereik Hallo transactie moet worden uitgevoerd onder vervolgens bevatten. Zie voor meer informatie [Azure Cosmos DB partitioneren](partition-data.md).

### <a name="commit-and-rollback"></a>Commit- en rollback
Transacties zijn systeemeigen en nauw geïntegreerd in Cosmos-database JavaScript-programmeermodel. Binnen een JavaScript-functie, worden alle bewerkingen automatisch ingepakt onder één transactie. Als hello JavaScript is voltooid zonder een uitzondering, Hallo operations toohello-database zijn doorgevoerd. Hallo 'BEGIN TRANSACTION' en 'COMMIT TRANSACTION' instructies in relationele databases zijn in feite impliciete in Cosmos-database.  

Als er een uitzondering die wordt doorgegeven vanuit de Hallo script, wordt JavaScript-runtime Cosmos-database teruggedraaid Hallo hele transactie. Zoals in Hallo eerder is bijvoorbeeld uitzondering opgetreden effectief gelijkwaardige tooa 'ROLLBACK TRANSACTION' in Cosmos-database.

### <a name="data-consistency"></a>Gegevensconsistentie
Opgeslagen procedures en triggers worden altijd uitgevoerd op de primaire replica Hallo van hello Azure DB die Cosmos-container. Dit zorgt ervoor dat leesbewerkingen van binnen procedures aanbieding sterke consistentie opgeslagen. Query's op basis van de gebruiker gedefinieerde functies kunnen worden uitgevoerd op de primaire hello of een secundaire replica, maar wij niet garanderen toomeet hello consistentieniveau aangevraagd door de juiste replica Hallo kiezen.

## <a name="bounded-execution"></a>Begrensde uitvoering
Alle bewerkingen van de Cosmos-DB moeten voltooid binnen de opgegeven Hallo-server aanvragen van de time-outduur. Deze beperking geldt ook tooJavaScript functies (opgeslagen procedures, triggers en gebruiker gedefinieerde functies). Als een bewerking niet wordt voltooid met deze termijn, Hallo transactie wordt teruggedraaid. JavaScript-functies moeten worden voltooid binnen de tijdslimiet Hallo of implementeren van een voortzetting op basis van model toobatch/hervatten uitvoering.  

In de volgorde toosimplify ontwikkeling van opgeslagen procedures en triggers toohandle tijdslimiet, alle functies onder Hallo verzamelingsobject (voor het maken, lezen, vervangen en verwijderen van documenten en bijlagen) retourneren een Booleaanse waarde die aangeeft of die bewerking wordt voltooid. Als deze waarde false is, is het een indicatie dat de tijdslimiet Hallo over tooexpire en die procedure Hallo van uitvoering inpakken moet.  Bewerkingen in de wachtrij voorafgaande toohello eerste niet-geaccepteerde store bewerking zijn toocomplete gegarandeerd als Hallo opgeslagen procedure is voltooid in de tijd en geen aanvullende aanvragen niet in de wachtrij.  

JavaScript-functies worden ook begrensd op resourceverbruik. Cosmos DB reserveert doorvoer per verzameling op basis van de grootte van een databaseaccount Hallo ingericht. Doorvoer wordt uitgedrukt in termen van genormaliseerde eenheid van de CPU, geheugen en i/o-verbruik aanvraageenheden of RUs genoemd. JavaScript-functies kunnen gebruiken om een groot aantal RUs binnen een korte periode en mogelijk ophalen snelheid beperkte als Hallo collector is bereikt. In quarantaine geplaatste tooensure beschikbaarheid van primitieve databasebewerkingen kunnen ook een resource intensieve opgeslagen procedures zijn.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>Voorbeeld: Bulksgewijs importeren van gegevens in een database-programma
Hieronder volgt een voorbeeld van een opgeslagen procedure die documenten toobulk importeren in een verzameling is geschreven. Opmerking hoe Hallo opgeslagen procedure ingangen begrensd worden uitgevoerd door te controleren Hallo Booleaanse waarde retourneren vanuit createDocument en vervolgens maakt gebruik van het aantal documenten in elke aanroep van Hallo opgeslagen procedure tootrack en hervatten voortgang wordt ingevoegd in batches Hallo.

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

## <a id="trigger"></a>Databasetriggers
### <a name="database-pre-triggers"></a>Vooraf databasetriggers
Cosmos DB biedt triggers die zijn uitgevoerd of geactiveerd door een bewerking op een document. U kunt bijvoorbeeld een vooraf trigger opgeven wanneer u bij het maken van een document: deze vooraf trigger wordt uitgevoerd voordat het Hallo-document wordt gemaakt. Hallo Hieronder volgt een voorbeeld van hoe vooraf triggers mag gebruikte toovalidate Hallo eigenschappen van een document dat wordt gemaakt:

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


En bijbehorende clientzijde registratie van Node.js-code voor de trigger Hallo Hallo:

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


Vooraf triggers kunnen geen invoer parameters hebben. Hallo request-object kan aanvraagbericht voor gebruikte toomanipulate Hallo Hallo bewerking gekoppeld zijn. Hier Hallo vooraf trigger wordt uitgevoerd met het maken van een document Hallo en Hallo-bericht aanvraagtekst Hallo document toobe gemaakt in JSON-indeling bevat.   

Wanneer triggers zijn geregistreerd, kunnen gebruikers Hallo-bewerkingen die kan worden uitgevoerd met opgeven. Deze trigger is gemaakt met TriggerOperation.Create, wat betekent dat de volgende Hallo is niet toegestaan.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>Na databasetriggers
Na triggers, zoals pre triggers zijn gekoppeld aan een bewerking op een document en geen invoerparameters bevatten geen onderneemt. Ze worden uitgevoerd **nadat** Hallo-bewerking is voltooid, en hebben toegang tot toohello response-bericht dat toohello client wordt verzonden.   

Hallo volgende voorbeeld ziet u na triggers in actie:

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


Hallo trigger kan worden geregistreerd, zoals wordt weergegeven in Hallo voorbeeld te volgen.

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


Deze trigger Hallo metagegevensdocument opgevraagd en bijgewerkt met informatie over Hallo nieuw gemaakte document.  

Één ding dat is het belangrijk toonote hello **transactionele** uitvoering van triggers in Cosmos-database. Deze na trigger wordt uitgevoerd als onderdeel van Hallo dezelfde transactie als Hallo maken van het originele document Hallo. Dus als we Veroorzaak een exception van Hallo na trigger (zeg als we document kan niet tooupdate Hallo-metagegevens zijn), de hele transactie Hallo zal mislukken en worden teruggedraaid. Er is geen document wordt gemaakt en wordt een uitzondering geretourneerd.  

## <a id="udf"></a>Gebruiker gedefinieerde functies
Gebruiker gedefinieerde functies (UDF's) zijn gebruikte tooextend hello DocumentDB API SQL query language-grammatica en aangepaste bedrijfslogica implementeren. Ze kunnen alleen worden aangeroepen vanuit in query's. Ze hebben geen toegang tot toohello context-object en toobe gebruikt als alleen-compute JavaScript zijn bedoeld. Daarom kunnen UDF's worden uitgevoerd op secundaire replica's van Hallo Cosmos-DB-service.  

Hallo volgende voorbeeld maakt een UDF toocalculate inkomstenbelasting op basis van de tarieven voor verschillende inkomsten vierkante haken, en gebruikt vervolgens het binnen een toofind query alle mensen die meer dan 20.000 $ betaald belastingen.

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


Hallo UDF kan vervolgens worden gebruikt in query's zoals in Hallo voorbeeld te volgen:

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

## <a name="javascript-language-integrated-query-api"></a>JavaScript-taal geïntegreerd query API
Bovendien tooissuing query met behulp van de DocumentDB SQL-grammatica's hello serverzijde SDK kunt u tooperform geoptimaliseerde query's op basis van een beheersen JavaScript-interface zonder dat daarvoor kennis van SQL. Hallo JavaScript query die API u tooprogrammatically build-query's kunt door een predikaat functies wordt doorgegeven in de chainable functie aanroept met een syntaxis bekend-tooECMAScript5 matrix dient te worden en populaire JavaScript-bibliotheken zoals lodash. Query's worden geparseerd door Hallo JavaScript-runtime toobe efficiënt met behulp van Azure Cosmos DB indices uitgevoerd.

> [!NOTE]
> `__`(double liggend streepje) is een alias te`getContext().getCollection()`.
> <br/>
> Met andere woorden, u kunt `__` of `getContext().getCollection()` tooaccess Hallo API JavaScript-query.
> 
> 

Ondersteunde functies omvatten:

<ul>
<li>
<b>... chain(). waarde ([retouraanroep] [, opties])</b>
<ul>
<li>
Start een keten-aanroep die moet worden afgesloten met value().
</li>
</ul>
</li>
<li>
<b>filter (predicateFunction [, opties] [, callback])</b>
<ul>
<li>
Voer met behulp van een predicaatfunctie die resulteert in waar/onwaar in volgorde toofilter in/out invoerdocumenten in de resulterende set Hallo Hallo filtert. Dit gedrag vergelijkbaar tooa WHERE-component in SQL.
</li>
</ul>
</li>
<li>
<b>kaart (transformationFunction [, opties] [, callback])</b>
<ul>
<li>
Van toepassing is een projectie krijgt een transformatiefunctie waarbij elke invoer item tooa JavaScript-object of een waarde toegewezen. Dit is het gedrag vergelijkbaar tooa component SELECT van SQL.
</li>
</ul>
</li>
<li>
<b>pluck ([propertyName] [, opties] [, callback])</b>
<ul>
<li>
Dit is een snelkoppeling naar een kaart die uit elk item invoer Hallo-waarde van één eigenschap haalt.
</li>
</ul>
</li>
<li>
<b>plat ([isShallow] [, opties] [, callback])</b>
<ul>
<li>
Combineert en matrices van elk item invoer in één matrix tooa worden samengevoegd. Dit is het gedrag vergelijkbaar tooSelectMany in LINQ.
</li>
</ul>
</li>
<li>
<b>sortBy ([predicate] [, opties] [, callback])</b>
<ul>
<li>
Levert een nieuwe reeks documenten Hallo documenten in Hallo invoerdocument stream in oplopende volgorde met Hallo predicaat gegeven wordt gesorteerd. Dit is het gedrag vergelijkbaar tooa ORDER BY-component in SQL.
</li>
</ul>
</li>
<li>
<b>sortByDescending ([predicate] [, opties] [, callback])</b>
<ul>
<li>
Levert een nieuwe set van documenten Hallo documenten in Hallo invoerdocument stream in aflopende volgorde met Hallo predicaat gegeven wordt gesorteerd. Dit is het gedrag vergelijkbaar tooa x DESC ORDER BY-component in SQL.
</li>
</ul>
</li>
</ul>


Als opgenomen binnen een predikaat en/of selector-functies, opvragen hello volgende JavaScript-constructs automatisch geoptimaliseerde toorun rechtstreeks op Azure Cosmos DB indexen:

* Eenvoudige operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* Letterlijke waarden, met inbegrip van Hallo object letterlijke: {}
* var, return

Hallo volgende JavaScript-constructs komen niet ophalen geoptimaliseerd voor Azure Cosmos DB indexen:

* Transportbesturing (bijvoorbeeld als, terwijl)
* Functieaanroepen

Zie voor meer informatie onze [serverzijde JSDocs](http://azure.github.io/azure-documentdb-js-server/).

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>Voorbeeld: Een opgeslagen procedure met behulp van API-Hallo JavaScript query schrijven
Hallo volgende codevoorbeeld is een voorbeeld van hoe Hallo API JavaScript-Query kan worden gebruikt in de context van een opgeslagen procedure Hallo. Hallo opgeslagen procedure voegt een document, dat is opgegeven door een invoerparameter en updates van met een metagegevensdocument, Hallo `__.filter()` methode met minimaal, maxSize en totalSize op basis van de eigenschap size Hallo invoer van het document.

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

## <a name="sql-toojavascript-cheat-sheet"></a>SQL tooJavascript referentieoverzicht
Hallo geeft volgende tabel verschillende SQL-query's en Hallo bijbehorende JavaScript-query's.

Als het document sleutels met SQL-query's (bijvoorbeeld `doc.id`) zijn hoofdlettergevoelig.

|SQL| Query die JavaScript API|Onderstaande beschrijving|
|---|---|---|
|SELECTEER *<br>VAN documenten| {__.map(Function(doc) <br>&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc;<br>});|1|
|Selecteer docs.id, docs.message als gegevenstarieven in rekening, docs.actions <br>VAN documenten|{__.map(Function(doc)<br>&nbsp;&nbsp;&nbsp;&nbsp;{retourneren<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ID: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bericht: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Actions:doc.Actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|SELECTEER *<br>VAN documenten<br>WAAR docs.id="X998_Y998 '|{__.filter(Function(doc)<br>&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc.id === 'X998_Y998';<br>});|3|
|SELECTEER *<br>VAN documenten<br>WAAR ARRAY_CONTAINS (documenten. Tags, 123)|{__.filter(Function(x)<br>&nbsp;&nbsp;&nbsp;&nbsp;retourneren van x.Tags & & x.Tags.indexOf(123) > -1;<br>});|4|
|Selecteer docs.id, docs.message als bericht<br>VAN documenten<br>WAAR docs.id="X998_Y998 '|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;{.filter(function(doc)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc.id === 'X998_Y998';<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;{.map(function(doc)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{retourneren<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ID: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bericht: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.Value();|5|
|De SELECT VALUE-tag<br>VAN documenten<br>Voeg de tag IN documenten. Labels<br>ORDER BY docs._ts|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;{.filter(function(doc)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc retourneren. Labels & & Array.isArray (doc. Tags);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;{.sortBy(function(doc)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retourneren van doc._ts;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.Value()|6|

Hallo volgende beschrijvingen uitgelegd elke query Hallo bovenstaande tabel.
1. Resultaten in alle documenten (gepagineerd met vervolgtoken) als is.
2. Projecten Hallo-id, bericht (alias toomsg) en van alle documenten in te grijpen.
3. Query's voor documenten met Hallo predicaat: id = 'X998_Y998'.
4. Query's voor documenten die een eigenschap voor Tags en labels hebben, is een matrix met Hallo waarde 123.
5. Query's voor documenten met een predicaat id = "X998_Y998" en vervolgens projecten Hallo-id en -berichten (alias toomsg).
6. Filters voor documenten die een matrixeigenschap, Tags, hebben en resulterende documenten Hallo sorteren op Hallo _ts system tijdstempeleigenschap, en vervolgens projecteert + Hallo labels matrix worden samengevoegd.


## <a name="runtime-support"></a>Runtime-ondersteuning
[DocumentDB-JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) biedt ondersteuning voor Hallo HALLO de meeste functies van JavaScript-taal als gestandaardiseerde door gangbare [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

### <a name="security"></a>Beveiliging
JavaScript opgeslagen procedures en triggers zijn sandbox zodat Hallo gevolgen van een script niet toohello andere gelekt kunnen zonder tussenkomst van Hallo snapshot-isolatie voor transactie op databaseniveau Hallo. Hallo-runtime-omgevingen zijn gegroepeerd maar gereinigd van Hallo context na elke uitvoering. Ze zijn daarom toobe gegarandeerd veilig van onbedoelde nadelen van elkaar.

### <a name="pre-compilation"></a>Vooraf compileren
Opgeslagen procedures, triggers en UDF's zijn impliciet vooraf gecompileerde toohello byte notatie in volgorde tooavoid compilatie kosten gelijktijdig Hallo met elke aanroep van het script. Dit zorgt ervoor dat de aanroepen van opgeslagen procedures zijn snel en een lage footprint hebben.

## <a name="client-sdk-support"></a>Ondersteuning voor client-SDK
In aanvulling toohello DocumentDB-API voor [Node.js](documentdb-sdk-node.md) Azure DB die Cosmos-client heeft [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), en [Python SDK's](documentdb-sdk-python.md) voor Hallo DocumentDB-API. Opgeslagen procedures, triggers en UDF's kunnen worden gemaakt en wordt uitgevoerd met een van deze SDK's ook. Hallo volgende voorbeeld wordt getoond hoe toocreate en een opgeslagen procedure met behulp van Hallo .NET-client wordt uitgevoerd. Opmerking hoe Hallo .NET-typen worden doorgegeven in Hallo opgeslagen procedure als JSON en terug te lezen.

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


In dit voorbeeld laat zien hoe toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate een vooraf trigger en een document te maken met de Hallo trigger is ingeschakeld. 

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


En Hallo volgende voorbeeld ziet u hoe toocreate een gebruiker gedefinieerde functie (UDF) en deze gebruiken in een [DocumentDB API SQL-query](documentdb-sql-query.md).

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

## <a name="rest-api"></a>REST API
Alle Azure DB die Cosmos-bewerkingen kunnen worden uitgevoerd op een RESTful manier. Opgeslagen procedures, triggers en de gebruiker gedefinieerde functies kunnen worden geregistreerd in een verzameling met behulp van HTTP POST. Hallo Hieronder volgt een voorbeeld van hoe u een opgeslagen procedure tooregister:

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


Hallo opgeslagen procedure is geregistreerd door het uitvoeren van een POST-aanvraag tegen Hallo URI Hallo databases/testdb/colls/testColl/sprocs met Hallo hoofdtekst die toocreate opgeslagen procedure. Triggers en UDF's kunnen op dezelfde manier worden geregistreerd door uitgifte van een POST tegen/triggers en /udfs respectievelijk.
Deze opgeslagen procedure kan vervolgens worden uitgevoerd door uitgifte van een POST-aanvraag tegen de resourcekoppeling:

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


Hier wordt Hallo invoer toohello opgeslagen procedure doorgegeven in de aanvraagtekst Hallo. Houd er rekening mee dat Hallo-invoer is doorgegeven als een JSON-matrix van invoerparameters. Hallo opgeslagen procedure vergt Hallo eerste invoer als een document dat een antwoordtekst. Hallo-antwoord die is ontvangen, is als volgt:

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


In tegenstelling tot opgeslagen procedures, triggers kunnen niet rechtstreeks worden uitgevoerd. In plaats daarvan worden uitgevoerd als onderdeel van een bewerking op een document. We kunnen Hallo triggers toorun opgeven met een aanvraag met behulp van HTTP-headers. Hallo volgt aanvraag toocreate een document.

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


Hier is Hallo vooraf trigger toobe uitvoeren met Hallo-aanvraag opgegeven in x-ms-documentdb-pre-trigger-include Hallo-header. Navenant, eventuele na triggers zijn opgegeven in x-ms-documentdb-post-trigger-include Hallo-header. Houd er rekening mee dat zowel vóór en na triggers kunnen worden opgegeven voor een bepaalde aanvraag.

## <a name="sample-code"></a>Voorbeeldcode
U vindt meer serverzijde codevoorbeelden (inclusief [bulk verwijderen](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), en [bijwerken](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) op onze [GitHub-opslagplaats](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).

Wilt u uw geweldig opgeslagen procedure tooshare? Stuur ons een pull-aanvraag. 

## <a name="next-steps"></a>Volgende stappen
Zodra u hebt een of meer opgeslagen procedures, triggers en gebruiker gedefinieerde functies die zijn gemaakt, kunt u ze laden en ze weergeven in Azure portal met behulp van Data Explorer Hallo.

Wellicht vindt u ook de volgende Hallo verwijzingen en bronnen die nuttig zijn bij uw pad toolearn meer informatie over Azure Cosmos dB programmeren-server:

* [Azure Cosmos DB SDK 's](documentdb-sdk-dotnet.md)
* [DocumentDB-Studio](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [Veilige en draagbare Database uitbreidbaarheid](http://dl.acm.org/citation.cfm?id=276339) 
* [Service Oriented Architecture van de Database](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Hallo .NET Runtime in Microsoft SQL server die als host fungeert](http://dl.acm.org/citation.cfm?id=1007669)

