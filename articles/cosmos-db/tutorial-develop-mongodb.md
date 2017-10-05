---
title: Azure Cosmos DB-API voor MongoDB gebruiken voor het bouwen van een web-app | Microsoft Docs
description: Een Azure DB die Cosmos-zelfstudie waarmee u maakt een online database web-app met behulp van de API voor MongoDB.
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
ms.openlocfilehash: ff277c7f88359cd977424f2e0958c69e2547a2af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-connect-to-a-mongodb-app-using-net"></a><span data-ttu-id="79475-104">Azure Cosmos DB: Verbinding maken met een MongoDB-app met .NET</span><span class="sxs-lookup"><span data-stu-id="79475-104">Azure Cosmos DB: Connect to a MongoDB app using .NET</span></span>

<span data-ttu-id="79475-105">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="79475-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="79475-106">U kunt snel databases maken van documenten, sleutel/waarde-paren en grafen en hier query’s op uitvoeren. Deze databases genieten allemaal het voordeel van de wereldwijde distributie en horizontale schaalmogelijkheden die ten grondslag liggen aan Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79475-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="79475-107">Deze zelfstudie laat zien hoe een Azure DB die Cosmos-account maken met de Azure-portal en het maken van een database en verzameling voor het opslaan van gegevens met behulp van de [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79475-107">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and how to create a database and collection to store data using the [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="79475-108">Deze zelfstudie bevat de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="79475-108">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="79475-109">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="79475-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="79475-110">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="79475-110">Update your connection string</span></span>
> * <span data-ttu-id="79475-111">Een MongoDB-app op een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="79475-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="79475-112">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="79475-112">Create a database account</span></span>

<span data-ttu-id="79475-113">Begint met het maken van een Azure DB die Cosmos-account in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="79475-113">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="79475-114">Hebt u al een Azure DB die Cosmos-account?</span><span class="sxs-lookup"><span data-stu-id="79475-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="79475-115">Als dit het geval is, gaat u verder met [uw Visual Studio-oplossing instellen](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="79475-115">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="79475-116">Hebt u een Azure-DocumentDB-account?</span><span class="sxs-lookup"><span data-stu-id="79475-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="79475-117">Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan naar [instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="79475-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="79475-118">Als u de Emulator Azure Cosmos DB, volgt u de stappen in [Azure Cosmos DB Emulator](local-emulator.md) instellen van de emulator en gaat u verder met [instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="79475-118">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="79475-119">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="79475-119">Update your connection string</span></span>

1. <span data-ttu-id="79475-120">In de Azure-portal in de **Azure Cosmos DB** pagina, selecteert u de API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="79475-120">In the Azure portal, in the **Azure Cosmos DB** page, select the API for MongoDB account.</span></span> 
2. <span data-ttu-id="79475-121">Klik in de linkerbalk van de accountblade op **snel starten**.</span><span class="sxs-lookup"><span data-stu-id="79475-121">In the left bar of the account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="79475-122">Kies uw platform (*.NET stuurprogramma*, *Node.js stuurprogramma*, *MongoDB-Shell*, *Java stuurprogramma*, *Python stuurprogramma*).</span><span class="sxs-lookup"><span data-stu-id="79475-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="79475-123">Als u het hulpprogramma vermeld of niet ziet, maak je geen zorgen, we continu meer verbinding codefragmenten-document.</span><span class="sxs-lookup"><span data-stu-id="79475-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="79475-124">Kopiëren en plakken het codefragment in uw app MongoDB, en u bent klaar om te gaan.</span><span class="sxs-lookup"><span data-stu-id="79475-124">Copy and paste the code snippet into your MongoDB app, and you are ready to go.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="79475-125">Stelt de MongoDB-app</span><span class="sxs-lookup"><span data-stu-id="79475-125">Set up your MongoDB app</span></span>

<span data-ttu-id="79475-126">U kunt de [een web-app maken in Azure die verbinding maakt met MongoDB uitgevoerd op een virtuele machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) zelfstudie, met minimale wijziging, om snel een MongoDB-toepassing in te stellen (een lokaal of gepubliceerd naar een Azure-web-app) die is verbonden aan een API voor MongoDB-account.</span><span class="sxs-lookup"><span data-stu-id="79475-126">You can use the [Create a web app in Azure that connects to MongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, to quickly setup a MongoDB application (either locally or published to an Azure web app) that connects to an API for MongoDB account.</span></span>  

1. <span data-ttu-id="79475-127">Volg de zelfstudie, met één wijziging.</span><span class="sxs-lookup"><span data-stu-id="79475-127">Follow the tutorial, with one modification.</span></span>  <span data-ttu-id="79475-128">Vervang de code Dal.cs dit:</span><span class="sxs-lookup"><span data-stu-id="79475-128">Replace the Dal.cs code with this:</span></span>

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
   
            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from the MongoDB server.        
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
   
            // Creates a Task and inserts it into the collection in MongoDB.
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

2. <span data-ttu-id="79475-129">Wijzig de volgende variabelen in het bestand Dal.cs per de instellingen van uw account via de pagina sleutels in de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="79475-129">Modify the following variables in the Dal.cs file per your account settings from the Keys page in the Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="79475-130">De app gebruiken!</span><span class="sxs-lookup"><span data-stu-id="79475-130">Use the app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="79475-131">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="79475-131">Clean up resources</span></span>

<span data-ttu-id="79475-132">Als u deze app verder niet gaat gebruiken, kunt u met de volgende stappen alle resources verwijderen die met deze zelfstudies in Azure Portal zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="79475-132">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span> 

1. <span data-ttu-id="79475-133">Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="79475-133">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="79475-134">Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="79475-134">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79475-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79475-135">Next steps</span></span>

<span data-ttu-id="79475-136">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="79475-136">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="79475-137">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="79475-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="79475-138">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="79475-138">Update your connection string</span></span>
> * <span data-ttu-id="79475-139">Een MongoDB-app op een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="79475-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="79475-140">U kunt doorgaan met de volgende zelfstudie en uw MongoDB-gegevens importeren in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79475-140">You can proceed to the next tutorial and import your MongoDB data to Azure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="79475-141">MongoDB-gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79475-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

