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
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a>Een web-app in Azure maken die verbinding maakt met MongoDB op een virtuele machine
Met Git, kunt u een ASP.NET-toepassing naar Azure App Service Web Apps implementeren. In deze zelfstudie maakt u een eenvoudige ASP.NET-MVC-front-taak lijst toepassing die is verbonden met een MongoDB-database op een virtuele machine in Azure.  [MongoDB] [ MongoDB] is een populaire open-source NoSQL-database voor hoge prestaties. Nadat u hebt uitgevoerd en de ASP.NET-toepassing op uw ontwikkelcomputer testen, gaat u de toepassing naar App Service Web Apps met Git uploaden.

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="background-knowledge"></a>Achtergrondkennis
Kennis van de volgende is handig voor deze zelfstudie, hoewel niet vereist:

* De C# stuurprogramma voor MongoDB. Zie voor meer informatie over het C# toepassingen ontwikkelt voor MongoDB, de MongoDB [CSharp taal Center][MongoC#LangCenter]. 
* ASP .NET web application framework. U kunt meer informatie over op de [ASP.net-website][ASP.NET].
* ASP .NET MVC web application framework. U kunt meer informatie over op de [ASP.NET MVC-website][MVCWebSite].
* Azure. U kunt aan de slag lezen op [Azure][WindowsAzure].

## <a name="prerequisites"></a>Vereisten
* [Visual Studio Express 2013 voor Web] [ VSEWeb] of [Visual Studio 2013][VSUlt]
* [Azure-SDK voor .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Een actief Microsoft Azure-abonnement

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Een virtuele machine maken en installeer MongoDB
Deze zelfstudie wordt ervan uitgegaan dat u een virtuele machine hebt gemaakt in Azure. Na het maken van de virtuele machine moet u MongoDB installeren op de virtuele machine:

* Zie voor het maken van een virtuele Windows-computer en installeer MongoDB, [MongoDB installeren op een virtuele machine Windows Server worden uitgevoerd in Azure][InstallMongoOnWindowsVM].

Nadat u hebt gemaakt van de virtuele machine in Azure en MongoDB geïnstalleerd, zorg er dan voor dat de DNS-naam van de virtuele machine ('testlinuxvm.cloudapp.net', bijvoorbeeld) en de externe poort onthouden voor MongoDB die u hebt opgegeven in het eindpunt.  U moet deze informatie later in de zelfstudie.

<a id="createapp"></a>

## <a name="create-the-application"></a>De toepassing maken
In deze sectie maakt een ASP.NET-toepassing 'Mijn takenlijst' aangeroepen met behulp van Visual Studio en uitvoeren van een aanvankelijke implementatie naar Azure App Service Web Apps. U wordt de toepassing lokaal uitvoeren, maar wordt verbinding met uw virtuele machine in Azure en er gebruik van het MongoDB-exemplaar dat u hebt gemaakt.

1. Klik in Visual Studio **nieuw Project**.
   
    ![Pagina Nieuw Project starten][StartPageNewProject]
2. In de **nieuw Project** venster in het linkerdeelvenster, selecteer **Visual C#**, en selecteer vervolgens **Web**. Selecteer in het middelste deelvenster **ASP.NET-webtoepassing**. Aan de onderkant uw project een naam 'MyTaskListApp' en klik vervolgens op **OK**.
   
    ![Het dialoogvenster Nieuw project][NewProjectMyTaskListApp]
3. In de **nieuw ASP.NET-Project** dialoogvenster, **MVC**, en klik vervolgens op **OK**.
   
    ![MVC-sjabloon selecteren][VS2013SelectMVCTemplate]
4. Als u nog niet hebt aangemeld bij Microsoft Azure, wordt u gevraagd aan te melden. Volg de aanwijzingen om aan te melden bij Azure.
5. Wanneer u bent aangemeld, kunt u beginnen met het configureren van uw App Service-web-app. Geef de **Web-App-naam**, **App Service-abonnement**, **resourcegroep**, en **regio**, klikt u vervolgens op **maken**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Nadat het maken van het project is voltooid, wacht u totdat de web-app in Azure App Service worden gemaakt, zoals aangegeven in de **Azure App Service-activiteit** venster. Klik vervolgens op **MyTaskListApp publiceren naar deze Web-App nu**.
7. Klik op **Publish**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Als de standaard-ASP.NET-toepassing is gepubliceerd naar Azure App Service Web Apps, wordt deze gestart in de browser.

## <a name="install-the-mongodb-c-driver"></a>Installeer het stuurprogramma MongoDB C#
MongoDB biedt client-side '-ondersteuning voor C#-toepassingen via een stuurprogramma, moet u installeren op de lokale computer. De C#-stuurprogramma is beschikbaar via NuGet.

Het MongoDB-C#-stuurprogramma installeren:

1. In **Solution Explorer**, met de rechtermuisknop op de **MyTaskListApp** project en selecteer **NuGetPackages beheren**.
   
    ![NuGet-pakketten beheren][VS2013ManageNuGetPackages]
2. In de **NuGet-pakketten beheren** venster in het linkerdeelvenster klikt u op **Online**. In de **Online zoeken** vak aan de rechterkant, typt u 'mongodb.driver'.  Klik op **installeren** het stuurprogramma te installeren.
   
    ![Zoeken naar MongoDB C# stuurprogramma][SearchforMongoDBCSharpDriver]
3. Klik op **ik ga akkoord** de 10gen, Inc. licentievoorwaarden te accepteren.
4. Klik op **sluiten** nadat het stuurprogramma is geïnstalleerd.
    ![MongoDB C# stuurprogramma geïnstalleerd][MongoDBCsharpDriverInstalled]

Het MongoDB-C#-stuurprogramma is nu geïnstalleerd.  Verwijzingen naar de **MongoDB.Bson**, **MongoDB.Driver**, en **MongoDB.Driver.Core** bibliotheken zijn toegevoegd aan het project.

![MongoDB C# stuurprogramma verwijzingen][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Een model toevoegen
In **Solution Explorer**, met de rechtermuisknop op de *modellen* map en **toevoegen** een nieuwe **klasse** en noem deze *TaskModel.cs*.  In *TaskModel.cs*, vervangt de bestaande code door de volgende code:

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

## <a name="add-the-data-access-layer"></a>De data access-laag toevoegen
In **Solution Explorer**, met de rechtermuisknop op de *MyTaskListApp* project en **toevoegen** een **nieuwe map** met de naam *DAL*.  Met de rechtermuisknop op de *DAL* map en **toevoegen** een nieuwe **klasse**. Noem het klassebestand *Dal.cs*.  In *Dal.cs*, vervangt de bestaande code door de volgende code:

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

## <a name="add-a-controller"></a>Een controller toevoegen
Open de *Controllers\HomeController.cs* bestanden per **Solution Explorer** en vervang de bestaande code door het volgende:

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

## <a name="set-up-the-styles"></a>De stijlen instellen
De titel boven aan de pagina wilt wijzigen, opent u de *Views\Shared\\_Layout.cshtml* bestanden per **Solution Explorer** en vervang 'Application name' in de navigatiebalk header door 'mijn takenlijst Application' zodat deze er als volgt uit:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

Om het menu takenlijst instelt, opent u de *\Views\Home\Index.cshtml* -bestand en de bestaande code te vervangen door de volgende code:

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


Als u wilt toevoegen de mogelijkheid om een nieuwe taak te maken, met de rechtermuisknop op de *Views\Home\\*  map en **toevoegen** een **weergave**.  Naam van de weergave *maken*. Vervang de code door het volgende:

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

**Solution Explorer** ziet er als volgt:

![Solution Explorer][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a>De MongoDB-verbindingsreeks instellen
In **Solution Explorer**, open de *DAL/Dal.cs* bestand. De volgende coderegel vinden:

    private string connectionString = "mongodb://<vm-dns-name>";

Vervang `<vm-dns-name>` met de DNS-naam van de virtuele machine met MongoDB die u hebt gemaakt in de [maken van een virtuele machine en installeer MongoDB] [ Create a virtual machine and install MongoDB] stap van deze zelfstudie.  De DNS-naam van uw virtuele machine vindt u bij de Azure-Portal, selecteer **virtuele Machines**, en zoek **DNS-naam**.

Als de DNS-naam van de virtuele machine 'testlinuxvm.cloudapp.net' en MongoDB op de standaardpoort 27017 luistert, kan de verbinding tekenreeks coderegel, ziet er als:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Als het eindpunt van de virtuele machine Hiermee geeft u een andere externe poort voor MongoDB, kunt u de poort in de verbindingsreeks door:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Zie voor meer informatie over verbindingsreeksen MongoDB [verbindingen][MongoConnectionStrings].

## <a name="test-the-local-deployment"></a>De lokale implementatie testen
Als u wilt uw toepassing uitvoeren op uw ontwikkelcomputer, **foutopsporing starten** van de **fouten opsporen in** menu of hits **F5**. IIS Express wordt gestart en een browser wordt geopend en de startpagina van de toepassing wordt gestart.  U kunt een nieuwe taak die wordt toegevoegd aan de MongoDB-database op de virtuele machine in Azure kunt toevoegen.

![Mijn taak lijst-toepassing][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a>Publiceren naar Azure App Service WebApps
In deze sectie kunt u uw wijzigingen wilt publiceren naar Azure App Service Web Apps.

1. Klik in Solution Explorer met de rechtermuisknop op **MyTaskListApp** opnieuw en klik op **publiceren**.
2. Klik op **Publish**.
   
    U ziet nu uw web-app uitgevoerd in Azure App Service en toegang tot de MongoDB-database in Azure Virtual Machines.

## <a name="summary"></a>Samenvatting
U hebt nu uw ASP.NET-toepassing naar Azure App Service Web Apps is geïmplementeerd. De web-app weergeven:

1. Meld u aan bij de Azure-Portal.
2. Klik op **Web-apps**. 
3. Selecteer uw web-app in de **Web-Apps** lijst.

Zie voor meer informatie over het C# toepassingen ontwikkelt voor MongoDB [CSharp taal Center][MongoC#LangCenter]. 

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
