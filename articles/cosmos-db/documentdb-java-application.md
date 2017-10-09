---
title: aaaJava toepassing zelfstudie over het ontwikkelen met behulp van Azure DB die Cosmos | Microsoft Docs
description: Deze zelfstudie over Java-webtoepassingen ziet u hoe toouse hello Azure Cosmos DB en DocumentDB API toostore Hallo en toegang tot gegevens van een Java-toepassing gehost op Azure Websites.
keywords: Toepassingsontwikkeling, databasezelfstudie, java-toepassing, java-webtoepassing zelfstudie, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Een Java-webtoepassing met behulp van Azure DB die Cosmos en Hallo API DocumentDB bouwen
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Deze zelfstudie over Java-webtoepassingen ziet u hoe toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore en toegang tot gegevens van een Java-toepassing die worden gehost op Azure App Service Web Apps. In dit onderwerp leert u het volgende:

* Hoe toobuild een eenvoudige toepassing Java Server Pages (JSP) in Eclipse.
* Hoe toowork Hello Azure Cosmos DB service met behulp van Hallo [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).

Deze zelfstudie over Java-toepassing ziet u hoe taken van taak-management-toepassing voor een webgebaseerde toocreate waarmee u toocreate, ophalen en markeren als voltooid is, zoals wordt weergegeven in Hallo volgende afbeelding. Hallo-taken in de takenlijst Hallo worden opgeslagen als JSON-documenten in Azure Cosmos DB.

![De Java-toepassing My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> In deze zelfstudie voor het ontwikkelen van toepassingen wordt ervan uitgegaan dat u ervaring met Java hebt. Als u nieuwe tooJava of Hallo [vereiste hulpprogramma's](#Prerequisites), het is raadzaam downloaden voltooid Hallo [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project van GitHub en bouwen met behulp van [Hallo instructies aan Hallo einde van dit artikel](#GetProject). Zodra u klaar hebt, kunt u Hallo artikel toogain informatie over Hallo-code in de context van project Hallo Hallo bekijken.  
> 
> 

## <a id="Prerequisites"></a>Vereisten voor deze zelfstudie over Java-webtoepassingen
Voordat u deze zelfstudie voor het ontwikkelen van toepassing, moet u de volgende Hallo hebben:

* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie

    OF

    Een lokale installatie van Hallo [Azure Cosmos DB Emulator](local-emulator.md).
* [Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Eclipse IDE voor Java EE-ontwikkelaars.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Een Azure-website met een Java runtime environment (bijvoorbeeld Tomcat of Jetty) is ingeschakeld.](../app-service-web/web-sites-java-get-started.md)

Als u deze hulpprogramma's voor Hallo eerst installeert, coreservlets.com biedt een overzicht van het installatieproces Hallo in Snel starten Hallo-sectie van hun [zelfstudie: TomCat7 installeren en gebruiken met Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) artikel.

## <a id="CreateDB"></a>Stap 1: Een Azure DB die Cosmos-account maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account hebt of als u Azure Cosmos DB Emulator Hallo voor deze zelfstudie, kunt u overslaan te[stap 2: de Java JSP-toepassing hello maken](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Stap 2: De Java JSP-toepassing hello maken
toocreate hello JSP-toepassing:

1. Als eerste moet u een Java-project maken. Start Eclipse en klik achtereenvolgens op **File** (Bestand), **New** (Nieuw) en **Dynamic Web Project** (Dynamisch webproject). Als er geen **dynamisch webproject** wordt aangeduid als een beschikbare project, Hallo te volgen: klik op **bestand**, klikt u op **nieuw**, klikt u op **Project**..., vouw **Web**, klikt u op **dynamisch webproject**, en klik op **volgende**.
   
    ![JSP Java-toepassing ontwikkelen](./media/documentdb-java-application/image10.png)
2. Voer een projectnaam in Hallo **projectnaam** vak en in Hallo **Doelruntime** vervolgkeuzelijst, selecteer desgewenst een waarde (bijvoorbeeld Apache Tomcat v7.0) en klik vervolgens op **voltooien**. Een doelruntime te selecteren, kunt u toorun uw project lokaal via Eclipse.
3. Vouw in de weergave Project Explorer Hallo in Eclipse uw project. Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).
4. In Hallo **nieuw JSP-bestand** in het dialoogvenster, naam Hallo bestand **index.jsp**. Hallo bovenliggende map als houden **WebContent**, zoals weergegeven in Hallo van de volgende afbeelding en klik vervolgens op **volgende**.
   
    ![Een nieuw JSP-bestand maken - Zelfstudie Java-webtoepassing](./media/documentdb-java-application/image11.png)
5. In Hallo **JSP-sjabloon selecteren** in het dialoogvenster voor doel van deze zelfstudie select Hallo **nieuw JSP-bestand (html)**, en klik vervolgens op **voltooien**.
6. Wanneer Hallo index.jsp bestand wordt geopend in Eclipse, voegt u tekst toodisplay **Hello World!** binnen de bestaande Hallo <body> element. Uw bijgewerkte <body> inhoud moet eruitzien als Hallo code te volgen:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Hallo index.jsp bestand opslaan.
8. Als u een doelruntime in stap 2 hebt ingesteld, kunt u **Project** en vervolgens **uitvoeren** toorun uw JSP-toepassing lokaal:
   
    ![Hello World – Zelfstudie Java-toepassing](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>Stap 3: Hallo DocumentDB Java SDK installeren
Hallo gemakkelijkste manier toopull in Hallo DocumentDB Java SDK en de bijbehorende afhankelijkheden is via [Apache Maven](http://maven.apache.org/).

toodo, moet u tooconvert uw project tooa maven-project door Hallo volgende stappen uit te voeren:

1. Met de rechtermuisknop op het project in Hallo Projectverkenner, klikt u op **configureren**, klikt u op **tooMaven Project converteren**.
2. In Hallo **nieuwe POM maken** venster Hallo standaardinstellingen accepteren en op **voltooien**.
3. In **Projectverkenner**Open Hallo pom.xml-bestand.
4. Op Hallo **afhankelijkheden** tabblad in Hallo **afhankelijkheden** deelvenster, klikt u op **toevoegen**.
5. In Hallo **afhankelijkheid selecteren** venster Hallo te volgen:
   
   * In Hallo **groeps-Id** Voer com.microsoft.azure.
   * In Hallo **artefact-Id** Voer azure documentdb.
   * In Hallo **versie** Voer 1.5.1.
     
   ![DocumentDB Java Application SDK installeren](./media/documentdb-java-application/image13.png)
     
   * Of voeg Hallo afhankelijkheids-XML voor de groeps-Id en artefact-Id rechtstreeks toohello pom.xml via een teksteditor:
     
        <dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure documentdb</artifactId> <version>1.9.1</version></dependency>
6. Klik op **OK** en Maven hello DocumentDB Java SDK installeert.
7. Hallo pom.xml-bestand opslaan.

## <a id="UseService"></a>Stap 4: Gebruik hello Azure DB die Cosmos-service in een Java-toepassing
1. Eerst gaan we in TodoItem.java definiëren Hallo TodoItem object:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    In dit project, gebruiken we [Project Lombok](http://projectlombok.org/) toogenerate Hallo constructor, getters, setters en een opbouwfunctie. U kunt ook handmatig schrijven van deze code of hebben Hallo IDE gegenereerd.
2. tooinvoke hello Azure DB die Cosmos-service, moet u instantiëren een nieuwe **DocumentClient**. In het algemeen is het beste tooreuse hello **DocumentClient** - in plaats van te maken van een nieuwe client voor elke volgende aanvraag. Hallo-client kan worden hergebruikt door Hallo-client in een **DocumentClientFactory**. In de DocumentClientFactory.java, moet u toopaste Hallo URI en primaire sleutel waarde opgeslagen van Klembord in tooyour [stap 1](#CreateDB). Vervang [YOUR\_ENDPOINT\_HERE] door de URI en vervang [YOUR\_KEY\_HERE] door uw PRIMAIRE SLEUTEL.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Nu gaan we maken een Data Access-Object (DAO) tooabstract behouden blijven van onze ToDo-items tooAzure Cosmos DB.
   
    In volgorde toosave ToDo-items tooa verzameling, Hallo client moet tooknow welke database en verzameling toopersist te (waarnaar wordt verwezen via Self link-elementen). In het algemeen is het beste toocache Hallo-database en verzameling indien mogelijk tooavoid extra retouren toohello database.
   
    Hallo volgende code laat zien hoe tooretrieve de database en verzameling, als deze bestaat, of een nieuwe maken als deze niet bestaat:
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. de volgende stap Hallo toowrite sommige code toopersist Hallo taken in de verzameling toohello is. In dit voorbeeld gebruiken we [Gson](https://code.google.com/p/google-gson/) tooserialize en TodoItem Plain Old Java Objects (pojo's) tooJSON documenten niet deserialiseren.
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. De verwijzing naar documenten vindt net als bij Azure Cosmos DB-databases en -verzamelingen plaats via self link-elementen. Hallo volgende Help-functie kunt ons documenten ophalen door een ander kenmerk (bijvoorbeeld ' id') in plaats van self link-element:
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. We kunnen Hallo Help-methode in stap 5 tooretrieve een TodoItem JSON-document gebruiken door-id en vervolgens te deserialiseren tooa POJO:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. We kunnen ook Hallo DocumentClient tooget gebruiken een verzameling of lijst met TodoItems met DocumentDB SQL:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Er zijn veel manieren tooupdate een document met Hallo DocumentClient. In onze takenlijsttoepassing willen we toobe kunnen tootoggle of een TodoItem voltooid is. Dit kan worden gerealiseerd door 'complete' Hallo-kenmerk in Hallo document te werken:
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Tot slot willen we Hallo mogelijkheid toodelete een TodoItem uit onze lijst. toodo, kunnen we Hallo eerder geschreven Help-methode gebruiken tooretrieve Hallo Self link-element en vervolgens instrueren Hallo client toodelete het:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>Stap 5: Rest Hallo van project voor de ontwikkeling van Java-toepassing hello samen bekabeling
Nu dat we klaar bent met het Hallo plezier bits - alle die altijd ingeschakeld toobuild is een snelle gebruikersinterface en deze up tooour DAO.

1. Eerst laten we beginnen met het bouwen van een domeincontroller toocall onze DAO:
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    Hallo controller mogelijk gecompliceerde bedrijfslogica boven op Hallo DAO dat in een complexere toepassing.
2. Vervolgens maken we een servlet tooroute HTTP-aanvragen toohello domeincontroller:
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. We hebben een web user interface toodisplay toohello gebruiker nodig. We gaan opnieuw schrijven Hallo index.jsp dat we eerder hebben gemaakt:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. Ten slotte schrijven sommige clientzijde JavaScript tootie Hallo online gebruikersinterface en Hallo servlet samen:
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. Mooi. Alle die altijd ingeschakeld is nu tootest Hallo-toepassing. Hallo-toepassing lokaal uitvoeren en enkele Todo-items toevoegen door te vullen Hallo itemnaam en categorie en te klikken op **taak toevoegen**.
6. Zodra het Hallo-item wordt weergegeven, kunt u bijwerken of deze voltooid is door Hallo selectievakje in te schakelen en te klikken op **taken bijwerken**.

## <a id="Deploy"></a>Stap 6: De Java-toepassing tooAzure websites implementeren
Azure websites kunt u net zo eenvoudig als uw toepassing wordt geëxporteerd als een WAR-bestand en uploaden via broncodebeheer (bijvoorbeeld Git) of FTP-Java-toepassingen implementeren.

1. tooexport uw toepassing als een WAR-bestand met de rechtermuisknop op het project in **Projectverkenner**, klikt u op **exporteren**, en klik vervolgens op **WAR-bestand**.
2. In Hallo **WAR exporteren** venster Hallo te volgen:
   
   * Voer in Hallo vak webproject azure-documentdb-java-sample.
   * Kies een doel toosave Hallo WAR-bestand in Hallo doellocatie.
   * Klik op **Voltooien**.
3. Nu dat u een WAR-bestand in de hand hebt, kunt u gewoon uploaden tooyour Azure-website van **webapps** directory. Zie voor instructies over het Hallo-bestand uploaden [toevoegen van een Java-toepassing tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).
   
    Zodra het Hallo WAR-bestand is geüpload toohello map WebApps, detecteert Hallo runtime-omgeving dat u deze hebt toegevoegd en wordt automatisch geladen.
4. tooview het voltooide product Navigeer toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ en start u uw taken toevoegt.

## <a id="GetProject"></a>Hallo-project ophalen van GitHub
Alle Hallo voorbeelden in deze zelfstudie zijn opgenomen in Hallo [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project op GitHub. tooimport hello todo-project in Eclipse, Controleer of u hebt Hallo software en bronnen in Hallo [vereisten](#Prerequisites) sectie vervolgens Hallo te volgen:

1. Installeer [Project Lombok](http://projectlombok.org/). Lombok is gebruikte toogenerate constructors, getters, setters in Hallo-project. Zodra u Hallo lombok.jar bestand hebt gedownload, dubbelklikt u op het tooinstall het of installeren vanaf de opdrachtregel Hallo.
2. Als Eclipse geopend is, sluit en opnieuw tooload Lombok.
3. In Eclipse op Hallo **bestand** menu, klikt u op **importeren**.
4. In Hallo **importeren** venster, klikt u op **Git**, klikt u op **projecten van Git**, en klik vervolgens op **volgende**.
5. Op Hallo **opslagplaats bron selecteren** scherm, klikt u op **Clone URI**.
6. Op Hallo **bron Git-opslagplaats** scherm in Hallo **URI** vak en klik vervolgens op Voer https://github.com/Azure-Samples/java-todo-app.git **volgende**.
7. Op Hallo **vertakking selectie** scherm **master** is geselecteerd en klik vervolgens op **volgende**.
8. Op Hallo **lokale bestemming** scherm, klikt u op **Bladeren** tooselect een map waar de Hallo opslagplaats kunnen worden gekopieerd en klik vervolgens op **volgende**.
9. Op Hallo **een toouse wizard voor het importeren van de projecten selecteren** scherm **bestaande projecten importeren** is geselecteerd en klik vervolgens op **volgende**.
10. Op Hallo **importeren projecten** scherm, opheffen Hallo **DocumentDB** project en klik vervolgens op **voltooien**. Hallo DocumentDB-project bevat hello Azure Cosmos DB Java SDK, die we als een afhankelijkheid daarvan toevoegen zullen.
11. In **Projectverkenner**, gaat u tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java en Hallo HOST en MASTER_KEY waarden vervangt door Hallo URI en primaire sleutel voor uw Azure DB die Cosmos-account en vervolgens opgeslagen Hallo-bestand. Zie [Stap 1: Een Azure DB die Cosmos-databaseaccount maken](#CreateDB).
12. In **Projectverkenner**, klik met de rechtermuisknop op Hallo **azure-documentdb-java-sample**, klikt u op **pad**, en klik vervolgens op **configureren pad**.
13. Op Hallo **Javabuild-pad** in het rechterdeelvenster hello, selecteer Hallo scherm **bibliotheken** tabblad en klik vervolgens op **externe JARs toevoegen**. Navigeer toohello locatie van Hallo lombok.jar bestand en klik op **Open**, en klik vervolgens op **OK**.
14. Gebruik stap 12 tooopen hello **eigenschappen** venster opnieuw, en klik in het linkerdeelvenster Hallo vervolgens op **Runtimes gericht**.
15. Op Hallo **Runtimes gericht** scherm, klikt u op **nieuw**, selecteer **Apache Tomcat v7.0**, en klik vervolgens op **OK**.
16. Gebruik stap 12 tooopen hello **eigenschappen** venster opnieuw, en klik in het linkerdeelvenster Hallo vervolgens op **Project-facetten**.
17. Op Hallo **Project-facetten** Schakel in het scherm **Dynamic Web Module** en **Java**, en klik vervolgens op **OK**.
18. Op Hallo **Servers** tabblad Hallo welkomstscherm onderaan in, met de rechtermuisknop op **Tomcat v7.0 Server op localhost** en klik vervolgens op **toevoegen en verwijderen**.
19. Op Hallo **toevoegen en verwijderen** venster verplaatsen **azure-documentdb-java-sample** toohello **geconfigureerde** vak en klik vervolgens op **voltooien**.
20. In Hallo **Servers** tabblad, met de rechtermuisknop op **Tomcat v7.0 Server op localhost**, en klik vervolgens op **opnieuw**.
21. Navigeer in een browser toohttp://localhost:8080 / azure-documentdb-java-sample / toe te voegen tooyour takenlijst. Let op: als u standaardpoortwaarden, wijzigt u 8080 toohello waarde die u geselecteerd wijzigen.
22. toodeploy uw project tooan Azure-website, Zie [stap 6. Implementeren van uw toepassing tooAzure websites](#Deploy).

[1]: media/documentdb-java-application/keys.png
