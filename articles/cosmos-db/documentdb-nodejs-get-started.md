---
title: zelfstudie voor DocumentDB-API voor Azure Cosmos DB Hallo aaaNode.js | Microsoft Docs
description: Een Node.js-zelfstudie waarmee een Cosmos-database met Hallo DocumentDB-API maakt.
keywords: node.js zelfstudie, knooppuntdatabase
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Node.js-zelfstudie: gebruik Hallo DocumentDB API in Azure Cosmos DB toocreate een Node.js-consoletoepassing
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js voor MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Welkom toohello Node.js-zelfstudie voor hello Azure Cosmos DB Node.js SDK. Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.

De volgende onderwerpen komen aan bod:

* Maken en te verbinden tooan Azure DB die Cosmos-account
* Uw toepassing instellen
* Een knooppuntdatabase maken
* Een verzameling maken
* JSON-documenten maken
* Hallo verzameling opvragen
* Een document vervangen
* Een document verwijderen
* Hallo-knooppuntdatabase verwijderen

Hebt u geen tijd? Geen probleem. Hallo volledige oplossing is beschikbaar op [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). Zie [ophalen van de volledige oplossing Hallo](#GetSolution) voor beknopte instructies.

Nadat u Hallo Node.js-zelfstudie hebt voltooid, stemknoppen Controleer gebruik Hallo Hallo boven en onder aan deze pagina toogive ons feedback. Als u graag toocontact u rechtstreeks kunt u gratis tooinclude je e-mailadres in uw opmerkingen.

Tijd om aan de slag te gaan.

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Vereisten voor Hallo Node.js-zelfstudie
Controleer of dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u nog geen abonnement hebt, kunt u zich registreren voor een [gratis Azure-proefversie](https://azure.microsoft.com/pricing/free-trial/).
    * U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie.
* [Node.js](https://nodejs.org/) versie v0.10.29 of hoger.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Stap 1: een Azure Cosmos DB-account maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[uw Node.js-toepassing instellen](#SetupNode). Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[uw Node.js-toepassing instellen](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>Stap 2: Uw Node.js-toepassing instellen
1. Open uw favoriete terminal.
2. Zoek Hallo map of directory waarin u toosave wilt dat uw Node.js-toepassing.
3. Maak twee lege JavaScript-bestanden met Hallo volgende opdrachten:
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Installeer Hallo documentdb-module via npm. Hallo volgende opdracht gebruiken:
   * ```npm install documentdb --save```

Goed gedaan. U bent klaar met het instellen. U gaat nu aan de slag met het schrijven van code.

## <a id="Config"></a>Stap 3: de configuratie van de app instellen
Open ```config.js``` in uw favoriete teksteditor.

Vervolgens, kopiëren en plakken Hallo onderstaande codefragment en eigenschappen instellen ```config.endpoint``` en ```config.primaryKey``` tooyour Azure Cosmos DB eindpunt-uri en primaire sleutel. Deze beide configuraties vindt u in Hallo [Azure-portal](https://portal.azure.com).

![Node.js-zelfstudie - schermopname van het Azure-portal, met een account Azure Cosmos DB met actieve hub Hallo Hallo gemarkeerd, knop Hallo-sleutels gemarkeerd op hello Azure DB die Cosmos-accountblade en Hallo URI, primaire sleutel waarden en secundaire sleutel gemarkeerd op Hallo De blade sleutels - knooppuntdatabase][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Kopieer en plak Hallo ```database id```, ```collection id```, en ```JSON documents``` tooyour ```config``` object waarin u instellen onder uw ```config.endpoint``` en ```config.authKey``` eigenschappen. Als u gegevens die u wilt toostore in de database al hebt, kunt u Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md) in plaats van Hallo documentdefinities toe te voegen.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


Hallo-database, de verzameling en de documentdefinities zal fungeren als uw Azure-Cosmos-DB ```database id```, ```collection id```, documentgegevens.

Ten slotte exporteert uw ```config``` object, zodat u ernaar binnen Hallo verwijzen kunt ```app.js``` bestand.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>Stap 4: Tooan Azure DB die Cosmos-account koppelen
Open uw lege ```app.js``` bestand in de teksteditor Hallo. Kopieer en plak de code Hallo hieronder tooimport hello ```documentdb``` module en de zojuist gemaakte ```config``` module.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Kopieer en plak Hallo code toouse Hallo eerder opgeslagen ```config.endpoint``` en ```config.primaryKey``` toocreate een nieuwe DocumentClient.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Nu dat u Hallo code tooinitialize hello Azure Cosmos DB client hebt, gaat u nu kijken werken met Azure DB die Cosmos-resources.

## <a name="step-5-create-a-node-database"></a>Stap 5: een knooppuntdatabase maken
Kopieer en plak Hallo-code hieronder tooset Hallo HTTP-status voor niet gevonden, Hallo database-url en Hallo verzameling url. Deze URL's zijn hoe hello Azure Cosmos DB client vindt Hallo juiste database en verzameling.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

Een [database](documentdb-resources.md#databases) kunnen worden gemaakt met behulp van Hallo [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) functie Hallo **DocumentClient** klasse. Een database is Hallo logische container voor documentopslag, gepartitioneerd in verzamelingen.

Kopieer en plak Hallo **getDatabase** functie voor het maken van de nieuwe database in Hallo app.js bestand Hello ```id``` opgegeven in Hallo ```config``` object. Hallo functie wordt gecontroleerd of database Hallo Hello dezelfde ```FamilyRegistry``` -id al bestaat niet. Als er al een database met dezelfde id bestaat, wordt die database geretourneerd en wordt er geen nieuwe database gemaakt.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Code kopiëren en plakken Hallo onderstaande waarin het instellen van Hallo **getDatabase** tooadd Hallo Help-functie werken **sluiten** die worden afsluiten het Hallo-bericht en Hallo aanroep te afgedrukt**getDatabase** functie.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```

Gefeliciteerd. U hebt een Azure Cosmos DB-database gemaakt.

## <a id="CreateColl"></a>Stap 6: een verzameling maken
> [!WARNING]
> Met **CreateDocumentCollectionAsync** maakt u een nieuwe verzameling, wat gevolgen heeft voor de kosten. Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.
> 
> 

Een [verzameling](documentdb-resources.md#collections) kunnen worden gemaakt met behulp van Hallo [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) functie Hallo **DocumentClient** klasse. Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.

Kopieer en plak Hallo **getCollection** functie onder Hallo **getDatabase** werken in Hallo app.js bestand toocreate uw nieuwe verzameling Hello ```id``` opgegeven in Hallo ```config```object. Er wordt opnieuw gecontroleerd toomake ervoor dat een verzameling met dezelfde Hallo ```FamilyCollection``` -id al bestaat niet. Als er al een verzameling met dezelfde id bestaat, wordt die verzameling geretourneerd en wordt er geen nieuwe verzameling gemaakt.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Code kopiëren en plakken Hallo onder Hallo aanroep te**getDatabase** tooexecute hello **getCollection** functie.

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```

Gefeliciteerd. U hebt een Azure DB die Cosmos-verzameling gemaakt.

## <a id="CreateDoc"></a>Stap 7: een document maken
Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) functie Hallo **DocumentClient** klasse. Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud. U kunt nu een document invoegen in Azure Cosmos DB.

Kopieer en plak Hallo **getFamilyDocument** functie onder Hallo **getCollection** functie voor het maken van Hallo-documenten met de Hallo JSON-gegevens opgeslagen in Hallo ```config``` object. Er wordt opnieuw gecontroleerd toomake ervoor dat een document met Hallo dezelfde id nog niet bestaat.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

Code kopiëren en plakken Hallo onder Hallo aanroep te**getCollection** tooexecute hello **getFamilyDocument** functie.

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```

Gefeliciteerd. U hebt een Azure DB die Cosmos-document gemaakt.

![Node.js-zelfstudie: Diagram ter illustratie van Hallo hiërarchische relatie tussen Hallo-account, Hallo database Hallo verzameling en Hallo documenten - knooppuntdatabase](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>Stap 8: query's uitvoeren op Azure Cosmos DB-resources
Azure Cosmos DB biedt ondersteuning voor [uitgebreide query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling. Hallo ziet volgende voorbeeldcode u een query die u op Hallo documenten in uw verzameling uitvoeren kunt.

Kopieer en plak Hallo **queryCollection** functie onder Hallo **getFamilyDocument** functie in Hallo app.js-bestand. Azure Cosmos DB ondersteunt SQL-achtige query's, zoals hieronder wordt weergegeven. Bekijk voor meer informatie over het bouwen van complexe query's Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo) en Hallo [querydocumentatie](documentdb-sql-query.md).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


Hallo volgende diagram ziet u hoe u hello Azure Cosmos DB SQL-query syntaxis wordt aangeroepen voor Hallo verzameling gemaakt.

![Node.js-zelfstudie: Diagram ter illustratie van Hallo bereik en de betekenis van Hallo query - knooppuntdatabase](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Hallo [FROM](documentdb-sql-query.md#FromClause) sleutelwoord is optioneel in Hallo query omdat Azure Cosmos DB-query's al één verzameling tooa binnen het bereik zijn. Daarom kan FROM Families f worden ingewisseld door FROM root r, of een andere gewenste variabelenaam. Azure Cosmos DB wordt afgeleid dat Families, root of Hallo variabelenaam u hebt gekozen, verwijzing Hallo huidige verzameling standaard.

Code kopiëren en plakken Hallo onder Hallo aanroep te**getFamilyDocument** tooexecute hello **queryCollection** functie.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```

Gefeliciteerd. U hebt een query uitgevoerd op Azure Cosmos DB-documenten.

## <a id="ReplaceDocument"></a>Stap 9: een document vervangen
Azure Cosmos DB biedt ondersteuning voor het vervangen van JSON-documenten.

Kopieer en plak Hallo **replaceFamilyDocument** functie onder Hallo **queryCollection** functie in Hallo app.js-bestand.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Code kopiëren en plakken Hallo onder Hallo aanroep te**queryCollection** tooexecute hello **replaceDocument** functie. Hallo code toocall ook toe te voegen **queryCollection** opnieuw tooverify dat document Hallo is gewijzigd.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```

Gefeliciteerd. U hebt een Azure Cosmos DB-document vervangen.

## <a id="DeleteDocument"></a>Stap 10: een document verwijderen
Azure Cosmos DB biedt ondersteuning voor het verwijderen van JSON-documenten.

Kopieer en plak Hallo **deleteFamilyDocument** functie onder Hallo **replaceFamilyDocument** functie.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Code kopiëren en plakken Hallo hieronder Hallo aanroep toohello tweede **queryCollection** tooexecute hello **deleteDocument** functie.

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```

Gefeliciteerd. U hebt een Azure Cosmos DB-document verwijderd.

## <a id="DeleteDatabase"></a>Stap 11: Hallo-knooppuntdatabase verwijderen
Verwijderen Hallo gemaakt van de database wordt verwijderd Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).

Kopieer en plak Hallo **opschonen** functie onder Hallo **deleteFamilyDocument** functioneren tooremove Hallo database en alle onderliggende resources van Hallo.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

Code kopiëren en plakken Hallo onder Hallo aanroep te**deleteFamilyDocument** tooexecute hello **opschonen** functie.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>Stap 12: uw Note.js-toepassing uitvoeren
Helemaal er Hallo volgorde voor het aanroepen van uw functies als volgt uit:

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Zoek in de terminal uw ```app.js``` bestand en het Hallo-opdracht uitvoeren:```node app.js```

U ziet de uitvoer Hallo van uw getstarted-app. Hallo-uitvoer moet overeenkomen met de onderstaande Hallo voorbeeldtekst.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

Gefeliciteerd. U hebt gemaakt dat u Hallo Node.js-zelfstudie hebt voltooid en u hebt uw eerste Azure DB die Cosmos-consoletoepassing!

## <a id="GetSolution"></a>Hallo volledige Node.js-zelfstudieoplossing ophalen
Als u geen tijd toocomplete Hallo stappen in deze zelfstudie of gewoon wilt toodownload Hallo code hebt, kunt u het krijgen van [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

toorun hello GetStarted-oplossing die alle Hallo voorbeelden in dit artikel bevat, moet u de volgende Hallo:

* [Azure Cosmos DB-account][create-account].
* Hallo [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) oplossing is beschikbaar op GitHub.

Hallo installeren **documentdb** module via npm. Hallo volgende opdracht gebruiken:

* ```npm install documentdb --save```

Vervolgens gaat u naar Hallo ```config.js``` bestand, Hallo update de waarden config.endpoint en config.authKey zoals beschreven in [stap 3: de configuraties van uw app instellen](#Config). 

Ga vervolgens in de terminal naar uw ```app.js``` -bestand en voert u de opdracht Hallo: ```node app.js```.

Dat is alles, bouw nu de oplossing. Succes! 

## <a name="next-steps"></a>Volgende stappen
* Wilt u een complexer Node.js-voorbeeld? Zie [Een Node.js-webtoepassing bouwen met Azure Cosmos DB](documentdb-nodejs-application.md).
* Meer informatie over hoe te[bewaken van een account voor Azure Cosmos DB](monitor-accounts.md).
* Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).
* Meer informatie over Hallo programmeermodel vindt u in de sectie ontwikkelen van Hallo Hallo [documentatiepagina voor Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
