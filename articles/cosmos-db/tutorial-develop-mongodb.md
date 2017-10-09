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
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="d5370-104">Azure Cosmos DB: Verbinding maken met behulp van .NET-tooa MongoDB app</span><span class="sxs-lookup"><span data-stu-id="d5370-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="d5370-105">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d5370-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d5370-106">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="d5370-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="d5370-107">Deze zelfstudie laat zien hoe toocreate een Cosmos-DB Azure account met behulp van Azure-portal hello, en hoe toocreate een database en verzameling toostore gegevens met behulp van Hallo [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5370-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="d5370-108">Deze zelfstudie behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="d5370-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d5370-109">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="d5370-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="d5370-110">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="d5370-110">Update your connection string</span></span>
> * <span data-ttu-id="d5370-111">Een MongoDB-app op een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="d5370-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="d5370-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="d5370-112">Create a database account</span></span>

<span data-ttu-id="d5370-113">Begint met het maken van een Azure DB die Cosmos-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d5370-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="d5370-114">Hebt u al een Azure DB die Cosmos-account?</span><span class="sxs-lookup"><span data-stu-id="d5370-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="d5370-115">Als dit het geval is, gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="d5370-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="d5370-116">Hebt u een Azure-DocumentDB-account?</span><span class="sxs-lookup"><span data-stu-id="d5370-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="d5370-117">Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d5370-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="d5370-118">Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d5370-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="d5370-119">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="d5370-119">Update your connection string</span></span>

1. <span data-ttu-id="d5370-120">In de Azure-portal, op Hallo Hallo **Azure Cosmos DB** pagina, Hallo-API voor MongoDB-account selecteren.</span><span class="sxs-lookup"><span data-stu-id="d5370-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="d5370-121">Klik in de linkerbalk Hallo van Hallo accountblade op **snel starten**.</span><span class="sxs-lookup"><span data-stu-id="d5370-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="d5370-122">Kies uw platform (*.NET stuurprogramma*, *Node.js stuurprogramma*, *MongoDB-Shell*, *Java stuurprogramma*, *Python stuurprogramma*).</span><span class="sxs-lookup"><span data-stu-id="d5370-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="d5370-123">Als u het hulpprogramma vermeld of niet ziet, maak je geen zorgen, we continu meer verbinding codefragmenten-document.</span><span class="sxs-lookup"><span data-stu-id="d5370-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="d5370-124">Kopieer en plak Hallo codefragment in uw app MongoDB, en u bent klaar toogo.</span><span class="sxs-lookup"><span data-stu-id="d5370-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="d5370-125">Stelt de MongoDB-app</span><span class="sxs-lookup"><span data-stu-id="d5370-125">Set up your MongoDB app</span></span>

<span data-ttu-id="d5370-126">Kunt u Hallo [een web-app maken in Azure die verbinding maakt op een virtuele machine tooMongoDB](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) zelfstudie, met minimale wijziging, tooquickly setup een MongoDB-toepassing (een lokaal of gepubliceerde tooan Azure-web-app) die maakt verbinding tooan API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="d5370-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="d5370-127">Volg de zelfstudie hello, met één wijziging.</span><span class="sxs-lookup"><span data-stu-id="d5370-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="d5370-128">Hallo Dal.cs code vervangen door dit:</span><span class="sxs-lookup"><span data-stu-id="d5370-128">Replace hello Dal.cs code with this:</span></span>

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

2. <span data-ttu-id="d5370-129">Hallo volgende variabelen in Hallo Dal.cs bestand per instellingen van uw account uit Hallo sleutels pagina in hello Azure-portal te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="d5370-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="d5370-130">Hallo-app gebruiken!</span><span class="sxs-lookup"><span data-stu-id="d5370-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d5370-131">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="d5370-131">Clean up resources</span></span>

<span data-ttu-id="d5370-132">Als u deze app niet toocontinue toouse gaat, gebruikt u Hallo stappen toodelete alle resources die zijn gemaakt met deze zelfstudie in hello Azure-portal te volgen.</span><span class="sxs-lookup"><span data-stu-id="d5370-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="d5370-133">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d5370-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="d5370-134">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="d5370-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5370-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d5370-135">Next steps</span></span>

<span data-ttu-id="d5370-136">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="d5370-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d5370-137">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="d5370-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="d5370-138">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="d5370-138">Update your connection string</span></span>
> * <span data-ttu-id="d5370-139">Een MongoDB-app op een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="d5370-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="d5370-140">U kunt gaan van de volgende zelfstudie toohello en uw MongoDB gegevens tooAzure Cosmos-database importeren.</span><span class="sxs-lookup"><span data-stu-id="d5370-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5370-141">MongoDB-gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d5370-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

