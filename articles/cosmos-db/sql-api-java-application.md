---
title: Zelfstudie over het ontwikkelen van Java-toepassingen met Azure Cosmos DB | Microsoft Docs
description: Deze zelfstudie over Java-webtoepassingen ziet u het gebruik van de Cosmos Azure DB en de SQL-API voor het opslaan van en toegang tot gegevens uit een Java-toepassing gehost op Azure Websites.
keywords: Toepassingsontwikkeling, zelfstudie, java-toepassing, zelfstudie over java-webtoepassingen, azure, Microsoft azure
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
ms.openlocfilehash: 8507b772c537ac50bd40367fbde260a8d72375ca
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/18/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-sql-api"></a>Een Java-webtoepassing met behulp van Azure DB die Cosmos en de SQL-API bouwen
> [!div class="op_single_selector"]
> * [.NET](sql-api-dotnet-application.md)
> * [Node.js](sql-api-nodejs-application.md)
> * [Java](sql-api-java-application.md)
> * [Python](sql-api-python-application.md)
> 
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Deze zelfstudie over Java-webtoepassingen, leest u hoe u de [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service voor het opslaan en toegang tot gegevens van een Java-toepassing die worden gehost op Azure App Service Web Apps. In dit onderwerp leert u het volgende:

* Het bouwen van een eenvoudige toepassing Java Server Pages (JSP) in Eclipse.
* Werken met de Azure Cosmos DB-service met behulp van de [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).

In deze zelfstudie over het maken van een Java-toepassing wordt uitgelegd hoe u een webtoepassing voor taakbeheer maakt waarmee u taken kunt maken, ophalen en als voltooid kunt markeren, zoals in de volgende afbeelding. Alle taken in de ToDo-lijst worden als JSON-documenten opgeslagen in Azure Cosmos DB.

![De Java-toepassing My ToDo List](./media/sql-api-java-application/image1.png)

> [!TIP]
> In deze zelfstudie voor het ontwikkelen van toepassingen wordt ervan uitgegaan dat u ervaring met Java hebt. Als u niet bekend bent met Java of de [vereiste hulpprogramma's](#Prerequisites), is het raadzaam het volledige [todo](https://github.com/Azure-Samples/documentdb-java-todo-app)-project via GitHub te downloaden. Vervolgens kunt u [de instructies aan het eind van dit artikel gebruiken](#GetProject) om het project op te bouwen. Zodra u klaar bent, kunt u het artikel lezen voor meer informatie over de code in de context van het project.  
> 
> 

## <a id="Prerequisites"></a>Vereisten voor deze zelfstudie over Java-webtoepassingen
Voordat u met deze zelfstudie over het ontwikkelen van toepassingen aan de slag gaat, moet u beschikken over het volgende:

*  Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint. 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Eclipse IDE voor Java EE-ontwikkelaars.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Een Azure-website met een Java runtime environment (bijvoorbeeld Tomcat of Jetty) is ingeschakeld.](../app-service/app-service-web-get-started-java.md)

Als u deze hulpprogramma's voor het eerst installeert, kunt u op coreservlets.com in de Quick Start-sectie van het artikel[Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) (Zelfstudie: TomCat7 installeren en gebruiken met Eclipse) een overzicht van het installatieproces vinden.

## <a id="CreateDB"></a>Stap 1: Een Azure DB die Cosmos-account maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account hebt of de Azure Cosmos DB-emulator gebruikt voor deze zelfstudie, kunt u direct doorgaan naar [Stap 2: de Java JSP-toepassing maken](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Stap 2: De Java JSP-toepassing maken
De JSP-toepassing maken:

1. Als eerste moet u een Java-project maken. Start Eclipse en klik achtereenvolgens op **File** (Bestand), **New** (Nieuw) en **Dynamic Web Project** (Dynamisch webproject). Als er geen **dynamisch webproject** beschikbaar is, gaat u als volg te werk: klik achtereenvolgens op **File** (Bestand), **New** (Nieuw), **Project**, vouw **Web** uit en klik op **Dynamic Web Project** (Dynamische webproject) en **Next** (Volgende).
   
    ![JSP Java-toepassing ontwikkelen](./media/sql-api-java-application/image10.png)
2. Voer in het vak **Project name** (Projectnaam) een projectnaam in en selecteer in de vervolgkeuzelijst **Target Runtime** (Doelruntime) eventueel een waarde (bijvoorbeeld Apache Tomcat v7.0) en klik vervolgens op **Finish** (Voltooien). Door een doelruntime te selecteren, kunt u het project lokaal via Eclipse uitvoeren.
3. Vouw in de weergave Project Explorer (Projectverkenner) van Eclipse uw project uit. Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).
4. Geef in het dialoogvenster **New JSP File** (Nieuw JSP-bestand) de naam **index.jsp** voor het bestand op. Bewaar de bovenliggende map als **WebContent**, zoals weergegeven in de volgende afbeelding, en klik vervolgens op **Next** (Volgende).
   
    ![Een nieuw JSP-bestand maken - Zelfstudie Java-webtoepassing](./media/sql-api-java-application/image11.png)
5. Selecteer voor deze zelfstudie in het dialoogvenster **Select JSP Template** (JSP-sjabloon selecteren) de optie **New JSP File (html)** (Nieuw JSP-bestand (html)) en klik vervolgens op **Finish** (Voltooien).
6. Wanneer het bestand index.jsp wordt geopend in Eclipse, voegt u tekst toe om **Hello World!** weer te geven in het bestaande <body>-element. Uw bijgewerkte <body>-inhoud moet eruitzien als de volgende code:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Sla het bestand index.jsp op.
8. Als u een doelruntime in stap 2 hebt ingesteld, kunt u achtereenvolgens op **Project** en **Run** klikken om uw JSP-toepassing lokaal uit te voeren:
   
    ![Hello World – Zelfstudie Java-toepassing](./media/sql-api-java-application/image12.png)

## <a id="InstallSDK"></a>Stap 3: Installeer de SQL-Java SDK
De eenvoudigste manier om op te halen in de SQL-SDK voor Java en de bijbehorende afhankelijkheden is via [Apache Maven](http://maven.apache.org/).

Hiervoor moet u de volgende stappen uitvoeren om het project te converteren naar een Maven-project:

1. Klik met de rechtermuisknop in de Projectverkenner, klik op **Configure** (Configureren) en klik vervolgens op **Convert to Maven Project** (Configureren naar een Maven-project).
2. Accepteer in het venster **Create new POM** (Nieuwe POM maken) de standaardinstellingen en klik op **Finish** (Voltooien).
3. Ga naar de **Projectverkenner** en open het bestand pom.xml.
4. Klik op het tabblad **Dependencies** (Afhankelijkheden) van het deelvenster **Dependencies** (Afhankelijkheden) op **Add** (Toevoegen).
5. Ga in het venster **Select Dependency** (Afhankelijkheid selecteren) als volgt te werk:
   
   * In de **groeps-Id** Voer com.microsoft.azure.
   * In de **artefact-Id** Voer azure documentdb.
   * In de **versie** Voer 1.5.1.
     
   ![SQL Java Application SDK installeren](./media/sql-api-java-application/image13.png)
     
   * Of Voeg de afhankelijkheids-XML voor de groeps-Id en artefact-Id rechtstreeks aan pom.xml via een teksteditor:
     
        <dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure documentdb</artifactId> <version>1.9.1</version></dependency>
6. Klik op **OK** en Maven de SQL Java SDK installeert.
7. Sla het bestand pom.xml op.

## <a id="UseService"></a>Stap 4: de Azure Cosmos DB-service in een Java-toepassing gebruiken
1. Eerst laten we het object TodoItem definiëren in TodoItem.java:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    In dit project, gebruiken we [Project Lombok](http://projectlombok.org/) om de constructor, getters, setters en een opbouwfunctie te genereren. U kunt u deze code eventueel ook handmatig schrijven of door de IDE laten genereren.
2. Als u de Azure Cosmos DB-service wilt aanroepen, moet u een nieuwe **DocumentClient** maken. Doorgaans kunt u de **DocumentClient** het best opnieuw gebruiken, zodat u niet voor elke volgende aanvraag en nieuwe client hoeft te maken. De client kan opnieuw worden gebruikt door deze in een **DocumentClientFactory** te verpakken. In DocumentClientFactory.java, moet u de URI en primaire sleutel waarde die u hebt opgeslagen naar het Klembord in plakken [stap 1](#CreateDB). Vervang [YOUR\_ENDPOINT\_HERE] door de URI en vervang [YOUR\_KEY\_HERE] door uw PRIMAIRE SLEUTEL.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. U kunt nu een Data Access-object (DAO) maken om de ToDo-items naar Azure Cosmos DB te abstraheren.
   
    De client moet weten welke database en verzameling moeten worden gebruikt (waarnaar wordt verwezen via self link-elementen) om de ToDo-items op te kunnen slaan naar een verzameling. Indien mogelijk slaat u de database en verzameling op in het cachegeheugen om extra retouren naar de database te voorkomen.
   
    De volgende code laat zien hoe u de database en verzameling ophaalt, indien de verzameling bestaat, of hoe u een nieuwe verzameling maakt als de verzameling niet bestaat:
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. Vervolgens moet u de code schrijven om de TodoItems door te geven naar de verzameling. In dit voorbeeld gebruiken we [Gson](https://code.google.com/p/google-gson/) om TodoItem POJO's (Plain Old Java Objects) naar JSON-documenten te serialiseren en te deserialiseren.
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. De verwijzing naar documenten vindt net als bij Azure Cosmos DB-databases en -verzamelingen plaats via self link-elementen. Met de volgende Help-functie kunt u documenten ophalen met een ander kenmerk (bijvoorbeeld 'id') in plaats van een self link-element:
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
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
6. We kunnen de Help-methode in stap 5 gebruiken om een TodoItem JSON-document op te halen op basis van de id om het document vervolgens te deserialiseren naar een POJO:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. We kunnen ook de DocumentClient gebruiken om op te halen van een verzameling of lijst met TodoItems met behulp van SQL:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Er zijn verschillende manieren waarop een document kan worden bijgewerkt met de DocumentClient. In onze takenlijsttoepassing moeten we kunnen aangeven of een TodoItem is voltooid of niet. Dit kan worden gerealiseerd door het kenmerk 'complete' in het document bij te werken:
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Tot slot willen we de mogelijkheid hebben om een TodoItem uit onze lijst te verwijderen. Hiervoor kunnen we de eerder geschreven Help-methode gebruiken om het self link-element op te halen en de client vervolgens instrueren dat deze moet worden verwijderd:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>Stap 5: De rest van het project voor de ontwikkeling van een Java-toepassing aaneen koppelen
Nu dat we klaar bent met het leuk bits - alle die altijd ingeschakeld is voor een snelle gebruikersinterface maken en deze maximaal onze DAO.

1. Laten we eerst een controller bouwen waarmee we onze DAO kunnen aanroepen:
   
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
   
    In complexere toepassing is het mogelijk dat de controller naast de DAO gecompliceerde bedrijfslogica bevat.
2. Vervolgens maken we een servlet om HTTP-aanvragen naar de controller te sturen:
   
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
3. We hebben een online gebruikersinterface weer te geven voor de gebruiker nodig. Laten we het bestand index.jsp dat we eerder hebben gemaakt, herschrijven:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
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
   
            <!-- The ToDo List -->
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
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. En schrijf tot slot wat JavaScript aan de clientzijde om de online gebruikersinterface en de servlet met elkaar verbinden:
   
        var todoApp = {
          /*
           * API methods to call Java backend.
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
   
              // Call api to update todo items.
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
           * Install the TodoApp
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
5. Mooi. Nu hoeft de toepassing alleen nog maar te worden getest. Voer de toepassing lokaal uit en voeg enkele Todo-items toe door de itemnaam en categorie in te vullen en op **Taak toevoegen** te klikken.
6. Zodra het item wordt weergegeven, kunt u bijwerken of het item is voltooid door het selectievakje in of uit te schakelen en op **Taken bijwerken** te klikken.

## <a id="Deploy"></a>Stap 6: Implementeer uw Java-toepassing naar Azure websites
Azure websites kunt u net zo eenvoudig als uw toepassing wordt geëxporteerd als een WAR-bestand en uploaden via broncodebeheer (bijvoorbeeld Git) of FTP-Java-toepassingen implementeren.

1. Als u wilt uw toepassing exporteren als een WAR-bestand, met de rechtermuisknop op het project in **Projectverkenner**, klikt u op **exporteren**, en klik vervolgens op **WAR-bestand**.
2. Ga in het venster **WAR exporteren** als volgt te werk:
   
   * Typ in het vak Webproject azure-documentdb-java-sample.
   * Kies in het vak Doel de bestemming waarnaar u het WAR-bestand wilt opslaan.
   * Klik op **Voltooien**.
3. Nu dat u een WAR-bestand in de hand hebt, kunt u gewoon uploaden naar uw Azure-website van **webapps** directory. Zie voor instructies over het uploaden van het bestand [toevoegen van een Java-toepassing naar Azure App Service Web Apps](../app-service/web-sites-java-add-app.md).
   
    Zodra het WAR-bestand is geüpload naar de map webapps, detecteert de runtime-omgeving dat u het bestand hebt toegevoegd en wordt het bestand automatisch geladen.
4. Als u wilt het voltooide product weergeven, navigeert u naar http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ en start u uw taken toevoegt.

## <a id="GetProject"></a>Het project ophalen van GitHub
Alle voorbeelden in deze zelfstudie zijn opgenomen in het [todo](https://github.com/Azure-Samples/documentdb-java-todo-app)-project op GitHub. Als u het todo-project wilt importeren in Eclipse, moet u over de software en resources beschikken die worden vermeld in de sectie [Vereisten](#Prerequisites) en gaat u als volgt te werk:

1. Installeer [Project Lombok](http://projectlombok.org/). Lombok wordt gebruikt om de constructors, getters, setters in het project te genereren. Zodra u het bestand lombok.jar hebt gedownload, dubbelklikt u op het bestand om het te installeren of installeert u het bestand vanaf de opdrachtregel.
2. Als Eclipse is geopend, sluit en opent u Eclipse opnieuw om Lombok te laden.
3. Klik in Eclipse in het menu **File** (Bestand) op **Import** (Importeren).
4. Klik in het venster the **Import** (Importeren) achtereenvolgens op **Git**, **Projects from Git** (Projecten van Git) en **Next** (Volgende).
5. Klik in het venster **Select Repository Source** (Opslagplaatsbron selecteren) op **Clone URI** (URI klonen).
6. Op de **bron Git-opslagplaats** scherm in de **URI** vak en klik vervolgens op Voer https://github.com/Azure-Samples/java-todo-app.git **volgende**.
7. Zorg er in het scherm **Branch Selection** (Vertakking selecteren) voor dat **master** is geselecteerd en klik op **Next** (Volgende).
8. Klik in het scherm **Local Destination** (Lokale bestemming) op **Browse** (Bladeren) om een map te selecteren waarnaar de opslag kan worden gekopieerd en klik op **Next** (Volgende).
9. Zorg er in het scherm **Select a wizard to use for importing projects** (Een wizard selecteren waarmee projecten worden geïmporteerd) voor dat **Import existing projects** (Bestaande projecten selecteren) is geselecteerd en klik op **Next** (Volgende).
10. Schakel in het scherm **Import Projects** (Projecten importeren) het selectievakje uit voor het **DocumentDB-project** en klik op **Finish** (Voltooien). Het DocumentDB-project bevat de Azure Cosmos DB Java SDK, die we als een afhankelijkheid daarvan toevoegen zullen.
11. In **Projectverkenner**, gaat u naar Azure-documentdb-Java-sample\src\com.Microsoft.Azure.documentdb.sample.dao\DocumentClientFactory.Java en vervang de waarden voor HOST en MASTER_KEY door de URI en primaire sleutel voor uw Azure DB van de Cosmos-account en sla het bestand. Zie [Stap 1: Een Azure DB die Cosmos-databaseaccount maken](#CreateDB).
12. Klik in de **Projectverkenner** met de rechtermuisknop op **azure-documentdb-java-sample**, klik op **Build Path** (Opbouwpad) en klik vervolgens op **Configure Build Path** (Opbouwpad configureren).
13. Selecteer in het rechterdeelvenster van het scherm **Java Build Path** (Java-opbouwpad) het tabblad **Libraries** (Bibliotheken) en klik vervolgens op **Add External JARs** (Externe JAR's toevoegen). Navigeer naar de locatie van het bestand lombok.jar en klik op **Open** (Openen) en **OK**.
14. Gebruik stap 12 om het venster **Properties** (Eigenschappen) opnieuw te openen en klik in het linkerdeelvenster vervolgens op **Targeted Runtimes** (Beoogde runtimes).
15. Klik in het scherm **Targeted Runtimes** (Beoogde runtimes) op **New** (Nieuw), selecteer **Apache Tomcat v7.0** en klik vervolgens op **OK**.
16. Gebruik stap 12 om het venster **Properties** (Eigenschappen) opnieuw te openen en klik in het linkerdeelvenster vervolgens op **Project Facets** (Projectfacetten).
17. Selecteer in het scherm **Project Facets** (Projectfacetten) achtereenvolgens **Dynamic Web Module** (Dynamische webmodule) en **Java** en klik vervolgens op **OK**.
18. Klik op het tabblad **Servers** onder aan het scherm met de rechtermuisknop op **Tomcat v7.0 Server at localhost** (Tomcat v7.0 Server op localhost) en klik vervolgens op **Add and Remove** (Toevoegen en verwijderen).
19. Verplaats in het venster **Add and Remove** (Toevoegen en verwijderen) **azure-documentdb-java-sample** naar het vak **Configured** (Geconfigureerd) en klik vervolgens op **Finish** (Voltooien).
20. In de **Servers** tabblad, met de rechtermuisknop op **Tomcat v7.0 Server op localhost**, en klik vervolgens op **opnieuw**.
21. Navigeer in een browser naar http://localhost:8080/azure-documentdb-java-sample/ om taken aan uw takenlijst toe te voegen. Als u de standaardpoortwaarden hebt gewijzigd, wijzigt u 8080 in de waarde die u hebt geselecteerd.
22. Zie [Stap 6: Implementeren van uw toepassing naar Azure websites](#Deploy).

