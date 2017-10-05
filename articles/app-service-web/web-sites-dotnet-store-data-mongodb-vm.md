---
title: Een web-app in Azure maken die verbinding maakt met MongoDB op een virtuele machine
description: Een zelfstudie leert u hoe u een ASP.NET-app in Azure App Service implementeren met Git verbonden met MongoDB op een virtuele Machine van Azure.
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
ms.openlocfilehash: a3f289ed9c764d0859573de4f834e042d0f103c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="59941-103">Een web-app in Azure maken die verbinding maakt met MongoDB op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="59941-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="59941-104">Met Git, kunt u een ASP.NET-toepassing naar Azure App Service Web Apps implementeren.</span><span class="sxs-lookup"><span data-stu-id="59941-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="59941-105">In deze zelfstudie maakt u een eenvoudige ASP.NET-MVC-front-taak lijst toepassing die is verbonden met een MongoDB-database op een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="59941-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="59941-106">[MongoDB] [ MongoDB] is een populaire open-source NoSQL-database voor hoge prestaties.</span><span class="sxs-lookup"><span data-stu-id="59941-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="59941-107">Nadat u hebt uitgevoerd en de ASP.NET-toepassing op uw ontwikkelcomputer testen, gaat u de toepassing naar App Service Web Apps met Git uploaden.</span><span class="sxs-lookup"><span data-stu-id="59941-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="59941-108">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="59941-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="59941-109">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="59941-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="59941-110">Achtergrondkennis</span><span class="sxs-lookup"><span data-stu-id="59941-110">Background knowledge</span></span>
<span data-ttu-id="59941-111">Kennis van de volgende is handig voor deze zelfstudie, hoewel niet vereist:</span><span class="sxs-lookup"><span data-stu-id="59941-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="59941-112">De C# stuurprogramma voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="59941-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="59941-113">Zie voor meer informatie over het C# toepassingen ontwikkelt voor MongoDB, de MongoDB [CSharp taal Center][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="59941-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="59941-114">ASP .NET web application framework.</span><span class="sxs-lookup"><span data-stu-id="59941-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="59941-115">U kunt meer informatie over op de [ASP.net-website][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="59941-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="59941-116">ASP .NET MVC web application framework.</span><span class="sxs-lookup"><span data-stu-id="59941-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="59941-117">U kunt meer informatie over op de [ASP.NET MVC-website][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="59941-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="59941-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="59941-118">Azure.</span></span> <span data-ttu-id="59941-119">U kunt aan de slag lezen op [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="59941-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59941-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="59941-120">Prerequisites</span></span>
* <span data-ttu-id="59941-121">[Visual Studio Express 2013 voor Web] [ VSEWeb] of [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="59941-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="59941-122">Azure-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="59941-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="59941-123">Een actief Microsoft Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="59941-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="59941-124">Een virtuele machine maken en installeer MongoDB</span><span class="sxs-lookup"><span data-stu-id="59941-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="59941-125">Deze zelfstudie wordt ervan uitgegaan dat u een virtuele machine hebt gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="59941-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="59941-126">Na het maken van de virtuele machine moet u MongoDB installeren op de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="59941-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="59941-127">Zie voor het maken van een virtuele Windows-computer en installeer MongoDB, [MongoDB installeren op een virtuele machine Windows Server worden uitgevoerd in Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="59941-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="59941-128">Nadat u hebt gemaakt van de virtuele machine in Azure en MongoDB geïnstalleerd, zorg er dan voor dat de DNS-naam van de virtuele machine ('testlinuxvm.cloudapp.net', bijvoorbeeld) en de externe poort onthouden voor MongoDB die u hebt opgegeven in het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="59941-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="59941-129">U moet deze informatie later in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="59941-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="59941-130">De toepassing maken</span><span class="sxs-lookup"><span data-stu-id="59941-130">Create the application</span></span>
<span data-ttu-id="59941-131">In deze sectie maakt een ASP.NET-toepassing 'Mijn takenlijst' aangeroepen met behulp van Visual Studio en uitvoeren van een aanvankelijke implementatie naar Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="59941-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="59941-132">U wordt de toepassing lokaal uitvoeren, maar wordt verbinding met uw virtuele machine in Azure en er gebruik van het MongoDB-exemplaar dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="59941-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="59941-133">Klik in Visual Studio **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="59941-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Pagina Nieuw Project starten][StartPageNewProject]
2. <span data-ttu-id="59941-135">In de **nieuw Project** venster in het linkerdeelvenster, selecteer **Visual C#**, en selecteer vervolgens **Web**.</span><span class="sxs-lookup"><span data-stu-id="59941-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="59941-136">Selecteer in het middelste deelvenster **ASP.NET-webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="59941-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="59941-137">Aan de onderkant uw project een naam 'MyTaskListApp' en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="59941-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Het dialoogvenster Nieuw project][NewProjectMyTaskListApp]
3. <span data-ttu-id="59941-139">In de **nieuw ASP.NET-Project** dialoogvenster, **MVC**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="59941-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![MVC-sjabloon selecteren][VS2013SelectMVCTemplate]
4. <span data-ttu-id="59941-141">Als u nog niet hebt aangemeld bij Microsoft Azure, wordt u gevraagd aan te melden.</span><span class="sxs-lookup"><span data-stu-id="59941-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="59941-142">Volg de aanwijzingen om aan te melden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="59941-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="59941-143">Wanneer u bent aangemeld, kunt u beginnen met het configureren van uw App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="59941-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="59941-144">Geef de **Web-App-naam**, **App Service-abonnement**, **resourcegroep**, en **regio**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="59941-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="59941-145">Nadat het maken van het project is voltooid, wacht u totdat de web-app in Azure App Service worden gemaakt, zoals aangegeven in de **Azure App Service-activiteit** venster.</span><span class="sxs-lookup"><span data-stu-id="59941-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="59941-146">Klik vervolgens op **MyTaskListApp publiceren naar deze Web-App nu**.</span><span class="sxs-lookup"><span data-stu-id="59941-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="59941-147">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="59941-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="59941-148">Als de standaard-ASP.NET-toepassing is gepubliceerd naar Azure App Service Web Apps, wordt deze gestart in de browser.</span><span class="sxs-lookup"><span data-stu-id="59941-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="59941-149">Installeer het stuurprogramma MongoDB C#</span><span class="sxs-lookup"><span data-stu-id="59941-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="59941-150">MongoDB biedt client-side '-ondersteuning voor C#-toepassingen via een stuurprogramma, moet u installeren op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="59941-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="59941-151">De C#-stuurprogramma is beschikbaar via NuGet.</span><span class="sxs-lookup"><span data-stu-id="59941-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="59941-152">Het MongoDB-C#-stuurprogramma installeren:</span><span class="sxs-lookup"><span data-stu-id="59941-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="59941-153">In **Solution Explorer**, met de rechtermuisknop op de **MyTaskListApp** project en selecteer **NuGetPackages beheren**.</span><span class="sxs-lookup"><span data-stu-id="59941-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![NuGet-pakketten beheren][VS2013ManageNuGetPackages]
2. <span data-ttu-id="59941-155">In de **NuGet-pakketten beheren** venster in het linkerdeelvenster klikt u op **Online**.</span><span class="sxs-lookup"><span data-stu-id="59941-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="59941-156">In de **Online zoeken** vak aan de rechterkant, typt u 'mongodb.driver'.</span><span class="sxs-lookup"><span data-stu-id="59941-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="59941-157">Klik op **installeren** het stuurprogramma te installeren.</span><span class="sxs-lookup"><span data-stu-id="59941-157">Click **Install** to install the driver.</span></span>
   
    ![Zoeken naar MongoDB C# stuurprogramma][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="59941-159">Klik op **ik ga akkoord** de 10gen, Inc. licentievoorwaarden te accepteren.</span><span class="sxs-lookup"><span data-stu-id="59941-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="59941-160">Klik op **sluiten** nadat het stuurprogramma is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="59941-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="59941-161">![MongoDB C# stuurprogramma geïnstalleerd][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="59941-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="59941-162">Het MongoDB-C#-stuurprogramma is nu geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="59941-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="59941-163">Verwijzingen naar de **MongoDB.Bson**, **MongoDB.Driver**, en **MongoDB.Driver.Core** bibliotheken zijn toegevoegd aan het project.</span><span class="sxs-lookup"><span data-stu-id="59941-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![MongoDB C# stuurprogramma verwijzingen][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="59941-165">Een model toevoegen</span><span class="sxs-lookup"><span data-stu-id="59941-165">Add a model</span></span>
<span data-ttu-id="59941-166">In **Solution Explorer**, met de rechtermuisknop op de *modellen* map en **toevoegen** een nieuwe **klasse** en noem deze *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="59941-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="59941-167">In *TaskModel.cs*, vervangt de bestaande code door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="59941-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-the-data-access-layer"></a><span data-ttu-id="59941-168">De data access-laag toevoegen</span><span class="sxs-lookup"><span data-stu-id="59941-168">Add the data access layer</span></span>
<span data-ttu-id="59941-169">In **Solution Explorer**, met de rechtermuisknop op de *MyTaskListApp* project en **toevoegen** een **nieuwe map** met de naam *DAL*.</span><span class="sxs-lookup"><span data-stu-id="59941-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="59941-170">Met de rechtermuisknop op de *DAL* map en **toevoegen** een nieuwe **klasse**.</span><span class="sxs-lookup"><span data-stu-id="59941-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="59941-171">Noem het klassebestand *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="59941-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="59941-172">In *Dal.cs*, vervangt de bestaande code door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="59941-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

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

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

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

## <a name="add-a-controller"></a><span data-ttu-id="59941-173">Een controller toevoegen</span><span class="sxs-lookup"><span data-stu-id="59941-173">Add a controller</span></span>
<span data-ttu-id="59941-174">Open de *Controllers\HomeController.cs* bestanden per **Solution Explorer** en vervang de bestaande code door het volgende:</span><span class="sxs-lookup"><span data-stu-id="59941-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

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

## <a name="set-up-the-styles"></a><span data-ttu-id="59941-175">De stijlen instellen</span><span class="sxs-lookup"><span data-stu-id="59941-175">Set up the styles</span></span>
<span data-ttu-id="59941-176">De titel boven aan de pagina wilt wijzigen, opent u de *Views\Shared\\_Layout.cshtml* bestanden per **Solution Explorer** en vervang 'Application name' in de navigatiebalk header door 'mijn takenlijst Application' zodat deze er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="59941-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="59941-177">Om het menu takenlijst instelt, opent u de *\Views\Home\Index.cshtml* -bestand en de bestaande code te vervangen door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="59941-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

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


<span data-ttu-id="59941-178">Als u wilt toevoegen de mogelijkheid om een nieuwe taak te maken, met de rechtermuisknop op de *Views\Home\\*  map en **toevoegen** een **weergave**.</span><span class="sxs-lookup"><span data-stu-id="59941-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="59941-179">Naam van de weergave *maken*.</span><span class="sxs-lookup"><span data-stu-id="59941-179">Name the view *Create*.</span></span> <span data-ttu-id="59941-180">Vervang de code door het volgende:</span><span class="sxs-lookup"><span data-stu-id="59941-180">Replace the code with the following:</span></span>

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

<span data-ttu-id="59941-181">**Solution Explorer** ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="59941-181">**Solution Explorer** should look like this:</span></span>

![Solution Explorer][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="59941-183">De MongoDB-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="59941-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="59941-184">In **Solution Explorer**, open de *DAL/Dal.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="59941-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="59941-185">De volgende coderegel vinden:</span><span class="sxs-lookup"><span data-stu-id="59941-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="59941-186">Vervang `<vm-dns-name>` met de DNS-naam van de virtuele machine met MongoDB die u hebt gemaakt in de [maken van een virtuele machine en installeer MongoDB] [ Create a virtual machine and install MongoDB] stap van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="59941-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="59941-187">De DNS-naam van uw virtuele machine vindt u bij de Azure-Portal, selecteer **virtuele Machines**, en zoek **DNS-naam**.</span><span class="sxs-lookup"><span data-stu-id="59941-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="59941-188">Als de DNS-naam van de virtuele machine 'testlinuxvm.cloudapp.net' en MongoDB op de standaardpoort 27017 luistert, kan de verbinding tekenreeks coderegel, ziet er als:</span><span class="sxs-lookup"><span data-stu-id="59941-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="59941-189">Als het eindpunt van de virtuele machine Hiermee geeft u een andere externe poort voor MongoDB, kunt u de poort in de verbindingsreeks door:</span><span class="sxs-lookup"><span data-stu-id="59941-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="59941-190">Zie voor meer informatie over verbindingsreeksen MongoDB [verbindingen][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="59941-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="59941-191">De lokale implementatie testen</span><span class="sxs-lookup"><span data-stu-id="59941-191">Test the local deployment</span></span>
<span data-ttu-id="59941-192">Als u wilt uw toepassing uitvoeren op uw ontwikkelcomputer, **foutopsporing starten** van de **fouten opsporen in** menu of hits **F5**.</span><span class="sxs-lookup"><span data-stu-id="59941-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="59941-193">IIS Express wordt gestart en een browser wordt geopend en de startpagina van de toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="59941-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="59941-194">U kunt een nieuwe taak die wordt toegevoegd aan de MongoDB-database op de virtuele machine in Azure kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="59941-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![Mijn taak lijst-toepassing][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="59941-196">Publiceren naar Azure App Service WebApps</span><span class="sxs-lookup"><span data-stu-id="59941-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="59941-197">In deze sectie kunt u uw wijzigingen wilt publiceren naar Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="59941-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="59941-198">Klik in Solution Explorer met de rechtermuisknop op **MyTaskListApp** opnieuw en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="59941-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="59941-199">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="59941-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="59941-200">U ziet nu uw web-app uitgevoerd in Azure App Service en toegang tot de MongoDB-database in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="59941-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="59941-201">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="59941-201">Summary</span></span>
<span data-ttu-id="59941-202">U hebt nu uw ASP.NET-toepassing naar Azure App Service Web Apps is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="59941-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="59941-203">De web-app weergeven:</span><span class="sxs-lookup"><span data-stu-id="59941-203">To view the web app:</span></span>

1. <span data-ttu-id="59941-204">Meld u aan bij de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="59941-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="59941-205">Klik op **Web-apps**.</span><span class="sxs-lookup"><span data-stu-id="59941-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="59941-206">Selecteer uw web-app in de **Web-Apps** lijst.</span><span class="sxs-lookup"><span data-stu-id="59941-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="59941-207">Zie voor meer informatie over het C# toepassingen ontwikkelt voor MongoDB [CSharp taal Center][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="59941-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp
