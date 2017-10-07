---
title: een Node.js-web-app voor Azure Cosmos DB aaaBuild | Microsoft Docs
description: Voor deze zelfstudie behandelt hoe toouse Microsoft Azure Cosmos DB toostore en toegang tot gegevens van een Node.js Express-webtoepassing gehost op Azure Websites.
keywords: Toepassingsontwikkeling, zelfstudie, node.js, node.js-zelfstudie leren
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395783175"></a>Een Node.js-webtoepassing bouwen met Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Voor deze zelfstudie ziet u hoe toouse Azure Cosmos DB en DocumentDB API toostore en toegang tot gegevens van een Node.js Express-toepassing hello op Azure Websites gehost. U bouwt een eenvoudige webtoepassing voor taakbeheer, een taken-app, waarmee u taken kunt maken, ophalen en voltooien. Hallo-taken worden opgeslagen als JSON-documenten in Azure Cosmos DB. Deze zelfstudie wordt u begeleid bij Hallo maken en implementeren van Hallo-app en wordt uitgelegd wat er gebeurt in elke codefragment.

![Schermopname van het Hallo toepassing My Todo List die in deze zelfstudie hebt gemaakt](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

Geen tijd toocomplete Hallo zelfstudie hebben en kunnen alleen wilt tooget Hallo volledige oplossing? Geen probleem, kunt u complete Voorbeeldoplossing Hallo van krijgen [GitHub][GitHub]. Hallo lezen alleen [Leesmij](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) -bestand voor instructies over hoe toorun Hallo app.

## <a name="_Toc395783176"></a>Vereisten
> [!TIP]
> Voor deze zelfstudie wordt ervan uitgegaan dat u ervaring hebt met Node.js en Azure Websites
> 
> 

Voordat u Hallo-instructies in dit artikel uitvoert, moet u ervoor zorgen dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.

   OF

   Een lokale installatie van Hallo [Azure Cosmos DB Emulator](local-emulator.md) (alleen Windows).
* [Node.js][Node.js] versie v0.10.29 of hoger.
* [Express generator](http://www.expressjs.com/starter/generator.html) (te installeren via `npm install express-generator -g`)
* [Git][Git].

## <a name="_Toc395637761"></a>Stap 1: een Azure Cosmos DB-databaseaccount maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account hebt of als u Azure Cosmos DB Emulator Hallo voor deze zelfstudie, kunt u overslaan te[stap 2: Maak een nieuwe Node.js-toepassing](#_Toc395783178).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>Stap 2: Maak een nieuwe Node.js-toepassing
Nu gaan we een eenvoudige Hello World Node.js-project met Hallo meer toocreate [Express](http://expressjs.com/) framework.

1. Open uw favoriete terminal, zoals Hallo Node.js-opdrachtprompt.
2. Navigeer toohello directory waarin u toostore Hallo nieuwe toepassing wilt.
3. Hallo express-generator toogenerate aangeroepen voor een nieuwe toepassing gebruiken **todo**.
   
        express todo
4. Open de nieuwe map **todo** en installeer afhankelijkheden.
   
        cd todo
        npm install
5. Voer uw nieuwe toepassing uit.
   
        npm start
6. U kunt uw nieuwe toepassing weergeven door uw browser te navigeren[http://localhost: 3000](http://localhost:3000).
   
    ![Node.js leren - schermopname van de toepassing in een browservenster Hallo wereld Hallo](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    Vervolgens toostop toepassing hello, druk op CTRL + C in Hallo terminalvenster en klik op **y** tooterminate Hallo batchverwerking.

## <a name="_Toc395783179"></a>Stap 3: Aanvullende modules installeren
Hallo **package.json** bestand is een Hallo-bestanden die zijn gemaakt in de hoofdmap Hallo van Hallo-project. Dit bestand bevat een lijst met aanvullende modules die u nodig hebt voor uw Node.js-toepassing. Later, wanneer u deze toepassing tooAzure Websites implementeert, is dit bestand gebruikt toodetermine welke modules moeten toobe geïnstalleerd op Azure toosupport uw toepassing. Er moet nog steeds tooinstall twee pakketten voor deze zelfstudie.

1. Terug in terminal hello, installeert u Hallo **asynchrone** module via npm.
   
        npm install async --save
2. Hallo installeren **documentdb** module via npm. Dit is Hallo module waar alle hello Azure DB die Cosmos-magie plaatsvindt.
   
        npm install documentdb --save
3. Een snelle controle van Hallo **package.json** bestand van de toepassing hello moet worden weergegeven Hallo aanvullende modules. Dit bestand wordt vertelt Azure welke pakketten toodownload en geïnstalleerd wanneer uw toepassing wordt uitgevoerd. Het bestand is vergelijkbaar Hallo in het volgende voorbeeld.
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    Hiermee wordt bij Node (en later bij Azure) aangegeven dat de toepassing afhankelijk is van deze aanvullende modules.

## <a name="_Toc395783180"></a>Stap 4: Hello Azure DB die Cosmos-service in een knooppunttoepassing gebruiken
Dat zorgt voor alle Hallo eerste installatie en configuratie, nu gaan we get omlaag toowhy we, en dat sommige code met behulp van Azure DB die Cosmos toowrite is.

### <a name="create-hello-model"></a>Hallo-model maken
1. In de projectmap hello, maakt u een nieuwe map met de naam **modellen** in Hallo dezelfde directory als Hallo package.json-bestand.
2. In Hallo **modellen** directory, maak een nieuw bestand met de naam **taskDao.js**. Dit bestand bevat Hallo-model voor Hallo-taken die zijn gemaakt door de toepassing.
3. Hallo in dezelfde **modellen** directory, maakt u een ander nieuw bestand met de naam **docdbUtils.js**. Dit bestand bevat enkele handige, opnieuw bruikbare codefragmenten die we voor de hele toepassing zullen gebruiken. 
4. Kopiëren Hallo volgende code te**docdbUtils.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. Opslaan en sluiten Hallo **docdbUtils.js** bestand.
6. Aan begin Hallo Hallo **taskDao.js** bestand, het toevoegen van de volgende code tooreference Hallo Hallo **DocumentDBClient** en Hallo **docdbUtils.js** die eerder is gemaakt:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. Vervolgens moet u code toodefine toevoegen en Hallo taakobject exporteren. Dit is verantwoordelijk voor het taakobject geïnitialiseerd en het instellen van Hallo-Database en verzameling van documenten, zullen worden gebruikt.
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. Voeg vervolgens Hallo code toodefine extra methoden volgen op Hallo taakobject, waardoor er interactie met gegevens die zijn opgeslagen in Azure Cosmos DB.
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. Opslaan en sluiten Hallo **taskDao.js** bestand. 

### <a name="create-hello-controller"></a>Hallo controller maken
1. In Hallo **routes** directory van uw project, maak een nieuw bestand met de naam **tasklist.js**. 
2. Hallo code te volgen toevoegen**tasklist.js**. Dit wordt geladen Hallo DocumentDBClient en async-modules die worden gebruikt door **tasklist.js**. Dit ook Hallo gedefinieerd **TaskList** functie die een exemplaar van Hallo wordt doorgegeven **taak** object eerder:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. Doorgaan met het toevoegen van toohello **tasklist.js** bestand door toe te voegen Hallo methoden te**showTasks, addTask**, en **completeTasks**:
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. Opslaan en sluiten Hallo **tasklist.js** bestand.

### <a name="add-configjs"></a>Config.js toevoegen
1. Maak een nieuw bestand met de naam **config.js** in uw projectmap.
2. Hallo te volgende toevoegen**config.js**. Hiermee definieert u configuratie-instellingen en waarden die nodig zijn voor de toepassing.
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. In Hallo **config.js** -bestand, update Hallo waarden voor HOST en auth_key bij door met behulp van Hallo waarden gevonden in de blade van Hallo-sleutels van uw Azure DB die Cosmos-account op Hallo [Microsoft Azure-portal](https://portal.azure.com).
4. Opslaan en sluiten Hallo **config.js** bestand.

### <a name="modify-appjs"></a>App.js wijzigen
1. Open in de projectmap Hallo Hallo **app.js** bestand. Dit bestand is gemaakt toen de Express-webtoepassing Hallo is gemaakt.
2. Hallo na code toohello bovenaan toevoegen **app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. Deze code definieert Hallo config bestand toobe gebruikt en tooread waarden buiten dit bestand in sommige variabelen we binnenkort gebruiken verloopt.
4. Vervangen van de volgende twee regels in Hallo **app.js** bestand:
   
        app.use('/', index);
        app.use('/users', users); 
   
      Hello codefragment te volgen:
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. Deze regels definiëren een nieuw exemplaar van onze **TaskDao** object met een nieuwe verbinding tooAzure Cosmos-DB (met behulp van Hallo waarden lezen uit Hallo **config.js**), initialiseren Hallo taakobject en bindt de formulieracties toomethods op onze **TaskList** controller. 
6. Ten slotte opslaan en sluiten Hallo **app.js** -bestand, bijna klaar.

## <a name="_Toc395783181"></a>Stap 5: Een gebruikersinterface maken
Nu gaan we onze aandacht toobuilding Hallo-gebruikersinterface, zodat een gebruiker daadwerkelijk communiceren met de toepassing communiceren kan. Express-toepassing die is gemaakt, gebruikt Hallo **Jade** als Hallo weergave-engine. Voor meer informatie over Jade Raadpleeg te[http://jade-lang.com/](http://jade-lang.com/).

1. Hallo **layout.jade** bestand in Hallo **weergaven** directory wordt gebruikt als een algemeen sjabloon voor andere **.jade** bestanden. In deze stap wijzigt u deze toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), dit is een werkset waarmee u eenvoudig toodesign een aantrekkelijk ogende website. 
2. Open Hallo **layout.jade** bestand gevonden in Hallo **weergaven** inhoud in de map en vervang de Hallo met Hallo volgende:

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    Zodoende weet Hallo **Jade** engine toorender HTML-code voor onze toepassing en maakt een **blok** aangeroepen **inhoud** waarmee we Hallo lay-out voor onze inhoud kunt leveren pagina's.

    Sla het bestand **layout.jade** op en sluit het bestand.

3. Open nu Hallo **index.jade** bestand, Hallo weergave die wordt gebruikt door de toepassing en het Hallo-inhoud van Hallo bestand vervangen door de volgende Hallo:
   
        extends layout
        block content
           h1 #{title}
           br
        
           form(action="/completetask", method="post")
             table.table.table-striped.table-bordered
               tr
                 td Name
                 td Category
                 td Date
                 td Complete
               if (typeof tasks === "undefined")
                 tr
                   td
               else
                 each task in tasks
                   tr
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

Dit breidt lay-out en inhoud biedt voor Hallo **inhoud** tijdelijke aanduiding hebt gezien in Hallo **layout.jade** bestand.
   
In deze lay-out hebben we twee HTML-formulieren gemaakt.

Hallo eerste formulier bevat een tabel voor onze gegevens en een knop waarmee we tooupdate items door boeken te**/completetask** methode van de controller.
    
Hallo tweede formulier bevat twee invoervelden en een knop waarmee een nieuw item toocreate door boeken te**/addtask** methode van de controller.

Dit is alles wat we nodig hebben om onze toepassing toowork.

## <a name="_Toc395783181"></a>Stap 6: De toepassing lokaal uitvoeren
1. tootest hello toepassing op uw lokale machine uitgevoerd `npm start` in terminal toostart uw toepassing hello en vernieuw vervolgens de [http://localhost: 3000](http://localhost:3000) browserpagina. Hallo pagina ziet er nu als Hallo in onderstaande afbeelding:
   
    ![Schermafbeelding van de toepassing MyTodo List in een browservenster Hallo](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > Als u een foutbericht over Hallo streepje in Hallo layout.jade hello index.jade bestand of ontvangt, zorg ervoor dat de eerste twee regels Hallo in beide bestanden links gerechtvaardigd is, zonder spaties. Als er spaties vóór de eerste twee regels hello, verwijder ze, beide bestanden opslaan en vernieuw het browservenster. 

2. Hallo-Item, itemnaam en categorie velden tooenter een nieuwe taak en klik vervolgens op **Item toevoegen**. Hiermee maakt u in Azure Cosmos DB een document met deze eigenschappen. 
3. Hallo pagina moet bijwerken toodisplay Hallo nieuw item in de takenlijst Hallo gemaakt.
   
    ![Schermopname van de toepassing hello met een nieuw item in de takenlijst Hallo](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. toocomplete een taak Hallo gewoon selectievakje van in de kolom voor Hallo voltooid en klik vervolgens op **taken bijwerken**. Deze updates Hallo al gemaakte document.

5. toostop hello toepassing, druk op CTRL + C in Hallo terminalvenster en klik vervolgens op **Y** tooterminate Hallo batchverwerking.

## <a name="_Toc395783182"></a>Stap 7: Uw toepassing ontwikkelen project tooAzure Websites implementeren
1. Als dit nog niet hebt gedaan, schakelt u een git-opslagplaats voor uw Azure-website in. U vindt instructies over het toodo dit op Hallo [lokale Git-implementatie tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) onderwerp.
2. Voeg uw Azure-website toe als een externe git.
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. Door te pushen toohello externe implementeren.
   
        git push azure master
4. Binnen een paar seconden zal git publicatie van uw webtoepassing voltooien en een browser starten waarin u kunt zien uw werk in Azure wordt uitgevoerd!

    Gefeliciteerd. U hebt zojuist uw eerste Node.js Express-webtoepassing met behulp van Azure DB die Cosmos gebouwd en gepubliceerd tooAzure Websites.

    Als u wilt dat toodownload of raadpleegt u de volledige referentietoepassing toohello voor deze zelfstudie, kan worden gedownload van [GitHub][GitHub].

## <a name="_Toc395637775"></a>Volgende stappen

* Wilt u tooperform schaal en prestaties testen met Azure Cosmos DB? Zie [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) (Prestaties en schaal testen met Azure Cosmos DB)
* Meer informatie over hoe te[bewaken van een account voor Azure Cosmos DB](monitor-accounts.md).
* Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).
* Hallo verkennen [Azure Cosmos DB documentatie](https://docs.microsoft.com/azure/documentdb/).

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

