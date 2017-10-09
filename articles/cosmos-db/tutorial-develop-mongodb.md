---
title: aaaUse Azure Cosmos DB van API voor MongoDB toobuild een web-app | Microsoft Docs
description: Een Azure DB die Cosmos-zelfstudie waarmee u maakt een online database web-app met behulp van Hallo-API voor MongoDB.
keywords: Voorbeelden van mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a>Azure Cosmos DB: Verbinding maken met behulp van .NET-tooa MongoDB app

Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft. U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren. 

Deze zelfstudie laat zien hoe toocreate een Cosmos-DB Azure account met behulp van Azure-portal hello, en hoe toocreate een database en verzameling toostore gegevens met behulp van Hallo [MongoDB API](mongodb-introduction.md). 

Deze zelfstudie behandelt Hallo taken te volgen:

> [!div class="checklist"]
> * Maak een Azure Cosmos DB-account 
> * Uw verbindingsreeks bijwerken
> * Een MongoDB-app op een virtuele machine maken 


## <a name="create-a-database-account"></a>Een databaseaccount maken

Begint met het maken van een Azure DB die Cosmos-account in hello Azure-portal.  

> [!TIP]
> * Hebt u al een Azure DB die Cosmos-account? Als dit het geval is, gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS)
> * Hebt u een Azure-DocumentDB-account? Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan te[instellen van uw Visual Studio-oplossing](#SetupVS).  
> * Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a>Uw verbindingsreeks bijwerken

1. In de Azure-portal, op Hallo Hallo **Azure Cosmos DB** pagina, Hallo-API voor MongoDB-account selecteren. 
2. Klik in de linkerbalk Hallo van Hallo accountblade op **snel starten**. 
3. Kies uw platform (*.NET stuurprogramma*, *Node.js stuurprogramma*, *MongoDB-Shell*, *Java stuurprogramma*, *Python stuurprogramma*). Als u het hulpprogramma vermeld of niet ziet, maak je geen zorgen, we continu meer verbinding codefragmenten-document. 
4. Kopieer en plak Hallo codefragment in uw app MongoDB, en u bent klaar toogo.

## <a name="set-up-your-mongodb-app"></a>Stelt de MongoDB-app

Kunt u Hallo [een web-app maken in Azure die verbinding maakt op een virtuele machine tooMongoDB](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) zelfstudie, met minimale wijziging, tooquickly setup een MongoDB-toepassing (een lokaal of gepubliceerde tooan Azure-web-app) die maakt verbinding tooan API voor MongoDB-account.  

1. Volg de zelfstudie hello, met één wijziging.  Hallo Dal.cs code vervangen door dit:

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }
   
            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }
   
            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
   
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            # region IDisposable
   
            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }
   
            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. Hallo volgende variabelen in Hallo Dal.cs bestand per instellingen van uw account uit Hallo sleutels pagina in hello Azure-portal te wijzigen:

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. Hallo-app gebruiken!

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app niet toocontinue toouse gaat, gebruikt u Hallo stappen toodelete alle resources die zijn gemaakt met deze zelfstudie in hello Azure-portal te volgen. 

1. Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt. 
2. Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Maak een Azure Cosmos DB-account 
> * Uw verbindingsreeks bijwerken
> * Een MongoDB-app op een virtuele machine maken

U kunt gaan van de volgende zelfstudie toohello en uw MongoDB gegevens tooAzure Cosmos-database importeren.  

> [!div class="nextstepaction"]
> [MongoDB-gegevens importeren in Azure Cosmos DB](mongodb-migrate.md)

