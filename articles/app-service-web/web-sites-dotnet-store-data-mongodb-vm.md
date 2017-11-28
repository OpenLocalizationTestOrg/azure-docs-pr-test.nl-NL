---
title: aaaCreate een web-app in Azure die verbinding maakt tooMongoDB uitgevoerd op een virtuele machine
description: Een zelfstudie over hoe toouse Git toodeploy een ASP.NET-app tooAzure App Service met elkaar verbonden tooMongoDB op een virtuele Machine van Azure.
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="4cd0b-103">Een web-app maken in Azure die verbinding maakt tooMongoDB uitgevoerd op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="4cd0b-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="4cd0b-104">Met Git, kunt u een ASP.NET-toepassing tooAzure App Service Web Apps implementeren.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="4cd0b-105">In deze zelfstudie maakt u een eenvoudige ASP.NET-MVC-front-taak lijst toepassing die verbinding maakt tooa MongoDB-database op een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="4cd0b-106">[MongoDB] [ MongoDB] is een populaire open-source NoSQL-database voor hoge prestaties.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="4cd0b-107">Na het uitgevoerd en ASP.NET-toepassing hello op uw ontwikkelcomputer testen, gaat uploaden Hallo toepassing tooApp Service Web Apps met Git.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="4cd0b-108">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4cd0b-109">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="4cd0b-110">Achtergrondkennis</span><span class="sxs-lookup"><span data-stu-id="4cd0b-110">Background knowledge</span></span>
<span data-ttu-id="4cd0b-111">Kennis van de volgende Hallo is handig voor deze zelfstudie, hoewel niet vereist:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="4cd0b-112">Hallo C#-stuurprogramma voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="4cd0b-113">Zie voor meer informatie over het ontwikkelen van C#-toepassingen op basis van MongoDB hello MongoDB [CSharp taal Center][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="4cd0b-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="4cd0b-114">Hallo ASP .NET web application framework.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="4cd0b-115">U kunt meer informatie over op het Hallo [ASP.net-website][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="4cd0b-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="4cd0b-116">Hallo ASP .NET MVC web application framework.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="4cd0b-117">U kunt meer informatie over op het Hallo [ASP.NET MVC-website][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="4cd0b-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="4cd0b-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-118">Azure.</span></span> <span data-ttu-id="4cd0b-119">U kunt aan de slag lezen op [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="4cd0b-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cd0b-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4cd0b-120">Prerequisites</span></span>
* <span data-ttu-id="4cd0b-121">[Visual Studio Express 2013 voor Web] [ VSEWeb] of [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="4cd0b-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="4cd0b-122">Azure-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="4cd0b-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="4cd0b-123">Een actief Microsoft Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="4cd0b-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="4cd0b-124">Een virtuele machine maken en installeer MongoDB</span><span class="sxs-lookup"><span data-stu-id="4cd0b-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="4cd0b-125">Deze zelfstudie wordt ervan uitgegaan dat u een virtuele machine hebt gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="4cd0b-126">Na het maken van Hallo virtuele machine moet u tooinstall MongoDB op Hallo virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="4cd0b-127">toocreate een virtuele Windows-computer en installeer MongoDB, Zie [MongoDB installeren op een virtuele machine Windows Server worden uitgevoerd in Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="4cd0b-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="4cd0b-128">Nadat u hebt gemaakt Hallo virtuele machine in Azure en MongoDB geïnstalleerd, worden ervoor tooremember Hallo DNS-naam van Hallo virtuele machine ('testlinuxvm.cloudapp.net', bijvoorbeeld) en de externe poort Hallo voor MongoDB die u hebt opgegeven in het Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="4cd0b-129">U moet deze informatie later in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="4cd0b-130">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="4cd0b-130">Create hello application</span></span>
<span data-ttu-id="4cd0b-131">In deze sectie maakt een ASP.NET-toepassing 'Mijn takenlijst' aangeroepen met behulp van Visual Studio en uitvoeren van een aanvankelijke implementatie tooAzure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="4cd0b-132">U Hallo toepassing lokaal wordt uitgevoerd, maar wordt verbinding tooyour virtuele machine in Azure maken en er gebruik van Hallo MongoDB-exemplaar dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="4cd0b-133">Klik in Visual Studio **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Pagina Nieuw Project starten][StartPageNewProject]
2. <span data-ttu-id="4cd0b-135">In Hallo **nieuw Project** venster in Hallo linkerdeelvenster Selecteer **Visual C#**, en selecteer vervolgens **Web**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="4cd0b-136">Selecteer in het middelste deelvenster Hallo **ASP.NET-webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="4cd0b-137">Naam van uw project 'MyTaskListApp' hello onderin, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Het dialoogvenster Nieuw project][NewProjectMyTaskListApp]
3. <span data-ttu-id="4cd0b-139">In Hallo **nieuw ASP.NET-Project** dialoogvenster, **MVC**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![MVC-sjabloon selecteren][VS2013SelectMVCTemplate]
4. <span data-ttu-id="4cd0b-141">Als u nog niet hebt aangemeld bij Microsoft Azure, kunt u zich na vragen aan gebruiker toosign in.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="4cd0b-142">Ga als volgt Hallo prompts toosign in Azure.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="4cd0b-143">Wanneer u bent aangemeld, kunt u beginnen met het configureren van uw App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="4cd0b-144">Geef Hallo **Web-App-naam**, **App Service-abonnement**, **resourcegroep**, en **regio**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="4cd0b-145">Nadat het Hallo-project maken is voltooid, wachten totdat Hallo web app toobe gemaakt in Azure App Service, zoals aangegeven in Hallo **Azure App Service-activiteit** venster.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="4cd0b-146">Klik vervolgens op **MyTaskListApp publiceren toothis Web-App nu**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="4cd0b-147">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="4cd0b-148">Zodra de standaard-ASP.NET-toepassing gepubliceerd tooAzure App Service Web Apps is, wordt deze in de browser Hallo gestart.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="4cd0b-149">Hallo MongoDB C#-stuurprogramma installeren</span><span class="sxs-lookup"><span data-stu-id="4cd0b-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="4cd0b-150">MongoDB biedt client-side '-ondersteuning voor C#-toepassingen via een stuurprogramma, u moet tooinstall op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="4cd0b-151">Hallo C#-stuurprogramma is beschikbaar via NuGet.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="4cd0b-152">tooinstall hello MongoDB C#-stuurprogramma:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="4cd0b-153">In **Solution Explorer**, klik met de rechtermuisknop Hallo **MyTaskListApp** project en selecteer **NuGetPackages beheren**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![NuGet-pakketten beheren][VS2013ManageNuGetPackages]
2. <span data-ttu-id="4cd0b-155">In Hallo **NuGet-pakketten beheren** venster in het linkerdeelvenster hello, klikt u op **Online**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="4cd0b-156">In Hallo **Online zoeken** vak op de juiste hello, typt u 'mongodb.driver'.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="4cd0b-157">Klik op **installeren** tooinstall Hallo stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![Zoeken naar MongoDB C# stuurprogramma][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="4cd0b-159">Klik op **ik ga akkoord** tooaccept hello 10gen, Inc. licentievoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="4cd0b-160">Klik op **sluiten** nadat het Hallo-stuurprogramma is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="4cd0b-161">![MongoDB C# stuurprogramma geïnstalleerd][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="4cd0b-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="4cd0b-162">Hallo MongoDB C#-stuurprogramma is nu geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="4cd0b-163">Verwijzingen toohello **MongoDB.Bson**, **MongoDB.Driver**, en **MongoDB.Driver.Core** bibliotheken toohello project zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![MongoDB C# stuurprogramma verwijzingen][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="4cd0b-165">Een model toevoegen</span><span class="sxs-lookup"><span data-stu-id="4cd0b-165">Add a model</span></span>
<span data-ttu-id="4cd0b-166">In **Solution Explorer**, klik met de rechtermuisknop Hallo *modellen* map en **toevoegen** een nieuwe **klasse** en noem deze *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="4cd0b-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="4cd0b-167">In *TaskModel.cs*, Hallo bestaande code te vervangen door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="4cd0b-168">Hallo gegevenstoegangslaag toevoegen</span><span class="sxs-lookup"><span data-stu-id="4cd0b-168">Add hello data access layer</span></span>
<span data-ttu-id="4cd0b-169">In **Solution Explorer**, klik met de rechtermuisknop Hallo *MyTaskListApp* project en **toevoegen** een **nieuwe map** met de naam *DAL*.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="4cd0b-170">Klik met de rechtermuisknop Hallo *DAL* map en **toevoegen** een nieuwe **klasse**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="4cd0b-171">Bestand met de klasse Hallo *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="4cd0b-172">In *Dal.cs*, Hallo bestaande code te vervangen door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

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
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
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
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a><span data-ttu-id="4cd0b-173">Een controller toevoegen</span><span class="sxs-lookup"><span data-stu-id="4cd0b-173">Add a controller</span></span>
<span data-ttu-id="4cd0b-174">Open Hallo *Controllers\HomeController.cs* bestanden per **Solution Explorer** en vervang de bestaande code Hallo door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-hello-styles"></a><span data-ttu-id="4cd0b-175">Hallo stijlen instellen</span><span class="sxs-lookup"><span data-stu-id="4cd0b-175">Set up hello styles</span></span>
<span data-ttu-id="4cd0b-176">toochange hello titel bovenaan Hallo Hallo pagina, open Hallo *Views\Shared\\_Layout.cshtml* bestanden per **Solution Explorer** en 'Application name' in de navigatiebalk-header Hallo vervangen door "Mijn taak Een overzicht van toepassing"zodat het lijkt erop dat dit:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="4cd0b-177">Open in de volgorde tooset Hallo takenlijst menu, Hallo *\Views\Home\Index.cshtml* bestands- en Hallo bestaande code te vervangen door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


<span data-ttu-id="4cd0b-178">tooadd hello mogelijkheid toocreate een nieuwe taak met de rechtermuisknop op Hallo *Views\Home\\*  map en **toevoegen** een **weergave**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="4cd0b-179">Hallo weergave naam *maken*.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-179">Name hello view *Create*.</span></span> <span data-ttu-id="4cd0b-180">Hallo code vervangen door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-180">Replace hello code with hello following:</span></span>

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

<span data-ttu-id="4cd0b-181">**Solution Explorer** ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-181">**Solution Explorer** should look like this:</span></span>

![Solution Explorer][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="4cd0b-183">Hallo MongoDB-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="4cd0b-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="4cd0b-184">In **Solution Explorer**Open Hallo *DAL/Dal.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="4cd0b-185">Hallo volgende coderegel zoeken:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="4cd0b-186">Vervang `<vm-dns-name>` met Hallo DNS-naam van Hallo virtuele machine MongoDB die u hebt gemaakt in Hallo [maken van een virtuele machine en installeer MongoDB] [ Create a virtual machine and install MongoDB] stap van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="4cd0b-187">toofind hello DNS-naam van uw virtuele machine, gaat u Azure Portal, selecteer toohello **virtuele Machines**, en zoek **DNS-naam**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="4cd0b-188">Als MongoDB luistert op Hallo standaardpoort 27017 Hallo DNS-naam van Hallo virtuele machine is 'testlinuxvm.cloudapp.net' eruit hello connection string-coderegel:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="4cd0b-189">Als het eindpunt van de virtuele machine Hallo Hiermee geeft u een andere externe poort voor MongoDB, kunt u door Hallo poort in de verbindingsreeks Hallo:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="4cd0b-190">Zie voor meer informatie over verbindingsreeksen MongoDB [verbindingen][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="4cd0b-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="4cd0b-191">Hallo lokale implementatie testen</span><span class="sxs-lookup"><span data-stu-id="4cd0b-191">Test hello local deployment</span></span>
<span data-ttu-id="4cd0b-192">selecteert u uw toepassing op uw ontwikkelcomputer toorun **foutopsporing starten** van Hallo **fouten opsporen in** menu of hits **F5**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="4cd0b-193">IIS Express wordt gestart en een browser wordt geopend en de startpagina van de toepassing hello wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="4cd0b-194">Een nieuwe taak toohello MongoDB-database op de virtuele machine in Azure wordt toegevoegd, kunt u toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![Mijn taak lijst-toepassing][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="4cd0b-196">TooAzure App Service Web Apps publiceren</span><span class="sxs-lookup"><span data-stu-id="4cd0b-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="4cd0b-197">In deze sectie kunt u uw wijzigingen tooAzure App Service Web Apps wilt publiceren.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="4cd0b-198">Klik in Solution Explorer met de rechtermuisknop op **MyTaskListApp** opnieuw en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="4cd0b-199">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="4cd0b-200">U ziet nu uw web-app uitgevoerd in Azure App Service en toegang tot Hallo MongoDB-database in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="4cd0b-201">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="4cd0b-201">Summary</span></span>
<span data-ttu-id="4cd0b-202">U hebt nu uw ASP.NET-toepassing tooAzure App Service Web Apps is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="4cd0b-203">tooview hello web-app:</span><span class="sxs-lookup"><span data-stu-id="4cd0b-203">tooview hello web app:</span></span>

1. <span data-ttu-id="4cd0b-204">Meld u aan bij hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="4cd0b-205">Klik op **Web-apps**.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="4cd0b-206">Selecteer uw web-app in Hallo **Web-Apps** lijst.</span><span class="sxs-lookup"><span data-stu-id="4cd0b-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="4cd0b-207">Zie voor meer informatie over het C# toepassingen ontwikkelt voor MongoDB [CSharp taal Center][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="4cd0b-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
