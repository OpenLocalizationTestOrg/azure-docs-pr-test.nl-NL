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
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>Een web-app maken in Azure die verbinding maakt tooMongoDB uitgevoerd op een virtuele machine
Met Git, kunt u een ASP.NET-toepassing tooAzure App Service Web Apps implementeren. In deze zelfstudie maakt u een eenvoudige ASP.NET-MVC-front-taak lijst toepassing die verbinding maakt tooa MongoDB-database op een virtuele machine in Azure.  [MongoDB] [ MongoDB] is een populaire open-source NoSQL-database voor hoge prestaties. Na het uitgevoerd en ASP.NET-toepassing hello op uw ontwikkelcomputer testen, gaat uploaden Hallo toepassing tooApp Service Web Apps met Git.

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="background-knowledge"></a>Achtergrondkennis
Kennis van de volgende Hallo is handig voor deze zelfstudie, hoewel niet vereist:

* Hallo C#-stuurprogramma voor MongoDB. Zie voor meer informatie over het ontwikkelen van C#-toepassingen op basis van MongoDB hello MongoDB [CSharp taal Center][MongoC#LangCenter]. 
* Hallo ASP .NET web application framework. U kunt meer informatie over op het Hallo [ASP.net-website][ASP.NET].
* Hallo ASP .NET MVC web application framework. U kunt meer informatie over op het Hallo [ASP.NET MVC-website][MVCWebSite].
* Azure. U kunt aan de slag lezen op [Azure][WindowsAzure].

## <a name="prerequisites"></a>Vereisten
* [Visual Studio Express 2013 voor Web] [ VSEWeb] of [Visual Studio 2013][VSUlt]
* [Azure-SDK voor .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Een actief Microsoft Azure-abonnement

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Een virtuele machine maken en installeer MongoDB
Deze zelfstudie wordt ervan uitgegaan dat u een virtuele machine hebt gemaakt in Azure. Na het maken van Hallo virtuele machine moet u tooinstall MongoDB op Hallo virtuele machine:

* toocreate een virtuele Windows-computer en installeer MongoDB, Zie [MongoDB installeren op een virtuele machine Windows Server worden uitgevoerd in Azure][InstallMongoOnWindowsVM].

Nadat u hebt gemaakt Hallo virtuele machine in Azure en MongoDB geïnstalleerd, worden ervoor tooremember Hallo DNS-naam van Hallo virtuele machine ('testlinuxvm.cloudapp.net', bijvoorbeeld) en de externe poort Hallo voor MongoDB die u hebt opgegeven in het Hallo-eindpunt.  U moet deze informatie later in de zelfstudie Hallo.

<a id="createapp"></a>

## <a name="create-hello-application"></a>Hallo-toepassing maken
In deze sectie maakt een ASP.NET-toepassing 'Mijn takenlijst' aangeroepen met behulp van Visual Studio en uitvoeren van een aanvankelijke implementatie tooAzure App Service Web Apps. U Hallo toepassing lokaal wordt uitgevoerd, maar wordt verbinding tooyour virtuele machine in Azure maken en er gebruik van Hallo MongoDB-exemplaar dat u hebt gemaakt.

1. Klik in Visual Studio **nieuw Project**.
   
    ![Pagina Nieuw Project starten][StartPageNewProject]
2. In Hallo **nieuw Project** venster in Hallo linkerdeelvenster Selecteer **Visual C#**, en selecteer vervolgens **Web**. Selecteer in het middelste deelvenster Hallo **ASP.NET-webtoepassing**. Naam van uw project 'MyTaskListApp' hello onderin, en klik vervolgens op **OK**.
   
    ![Het dialoogvenster Nieuw project][NewProjectMyTaskListApp]
3. In Hallo **nieuw ASP.NET-Project** dialoogvenster, **MVC**, en klik vervolgens op **OK**.
   
    ![MVC-sjabloon selecteren][VS2013SelectMVCTemplate]
4. Als u nog niet hebt aangemeld bij Microsoft Azure, kunt u zich na vragen aan gebruiker toosign in. Ga als volgt Hallo prompts toosign in Azure.
5. Wanneer u bent aangemeld, kunt u beginnen met het configureren van uw App Service-web-app. Geef Hallo **Web-App-naam**, **App Service-abonnement**, **resourcegroep**, en **regio**, klikt u vervolgens op **maken**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Nadat het Hallo-project maken is voltooid, wachten totdat Hallo web app toobe gemaakt in Azure App Service, zoals aangegeven in Hallo **Azure App Service-activiteit** venster. Klik vervolgens op **MyTaskListApp publiceren toothis Web-App nu**.
7. Klik op **Publish**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Zodra de standaard-ASP.NET-toepassing gepubliceerd tooAzure App Service Web Apps is, wordt deze in de browser Hallo gestart.

## <a name="install-hello-mongodb-c-driver"></a>Hallo MongoDB C#-stuurprogramma installeren
MongoDB biedt client-side '-ondersteuning voor C#-toepassingen via een stuurprogramma, u moet tooinstall op de lokale computer. Hallo C#-stuurprogramma is beschikbaar via NuGet.

tooinstall hello MongoDB C#-stuurprogramma:

1. In **Solution Explorer**, klik met de rechtermuisknop Hallo **MyTaskListApp** project en selecteer **NuGetPackages beheren**.
   
    ![NuGet-pakketten beheren][VS2013ManageNuGetPackages]
2. In Hallo **NuGet-pakketten beheren** venster in het linkerdeelvenster hello, klikt u op **Online**. In Hallo **Online zoeken** vak op de juiste hello, typt u 'mongodb.driver'.  Klik op **installeren** tooinstall Hallo stuurprogramma.
   
    ![Zoeken naar MongoDB C# stuurprogramma][SearchforMongoDBCSharpDriver]
3. Klik op **ik ga akkoord** tooaccept hello 10gen, Inc. licentievoorwaarden.
4. Klik op **sluiten** nadat het Hallo-stuurprogramma is geïnstalleerd.
    ![MongoDB C# stuurprogramma geïnstalleerd][MongoDBCsharpDriverInstalled]

Hallo MongoDB C#-stuurprogramma is nu geïnstalleerd.  Verwijzingen toohello **MongoDB.Bson**, **MongoDB.Driver**, en **MongoDB.Driver.Core** bibliotheken toohello project zijn toegevoegd.

![MongoDB C# stuurprogramma verwijzingen][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Een model toevoegen
In **Solution Explorer**, klik met de rechtermuisknop Hallo *modellen* map en **toevoegen** een nieuwe **klasse** en noem deze *TaskModel.cs* .  In *TaskModel.cs*, Hallo bestaande code te vervangen door Hallo code te volgen:

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

## <a name="add-hello-data-access-layer"></a>Hallo gegevenstoegangslaag toevoegen
In **Solution Explorer**, klik met de rechtermuisknop Hallo *MyTaskListApp* project en **toevoegen** een **nieuwe map** met de naam *DAL*.  Klik met de rechtermuisknop Hallo *DAL* map en **toevoegen** een nieuwe **klasse**. Bestand met de klasse Hallo *Dal.cs*.  In *Dal.cs*, Hallo bestaande code te vervangen door Hallo code te volgen:

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

## <a name="add-a-controller"></a>Een controller toevoegen
Open Hallo *Controllers\HomeController.cs* bestanden per **Solution Explorer** en vervang de bestaande code Hallo door Hallo volgende:

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

## <a name="set-up-hello-styles"></a>Hallo stijlen instellen
toochange hello titel bovenaan Hallo Hallo pagina, open Hallo *Views\Shared\\_Layout.cshtml* bestanden per **Solution Explorer** en 'Application name' in de navigatiebalk-header Hallo vervangen door "Mijn taak Een overzicht van toepassing"zodat het lijkt erop dat dit:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

Open in de volgorde tooset Hallo takenlijst menu, Hallo *\Views\Home\Index.cshtml* bestands- en Hallo bestaande code te vervangen door Hallo code te volgen:

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


tooadd hello mogelijkheid toocreate een nieuwe taak met de rechtermuisknop op Hallo *Views\Home\\*  map en **toevoegen** een **weergave**.  Hallo weergave naam *maken*. Hallo code vervangen door de volgende Hallo:

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

## <a name="set-hello-mongodb-connection-string"></a>Hallo MongoDB-verbindingsreeks instellen
In **Solution Explorer**Open Hallo *DAL/Dal.cs* bestand. Hallo volgende coderegel zoeken:

    private string connectionString = "mongodb://<vm-dns-name>";

Vervang `<vm-dns-name>` met Hallo DNS-naam van Hallo virtuele machine MongoDB die u hebt gemaakt in Hallo [maken van een virtuele machine en installeer MongoDB] [ Create a virtual machine and install MongoDB] stap van deze zelfstudie.  toofind hello DNS-naam van uw virtuele machine, gaat u Azure Portal, selecteer toohello **virtuele Machines**, en zoek **DNS-naam**.

Als MongoDB luistert op Hallo standaardpoort 27017 Hallo DNS-naam van Hallo virtuele machine is 'testlinuxvm.cloudapp.net' eruit hello connection string-coderegel:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Als het eindpunt van de virtuele machine Hallo Hiermee geeft u een andere externe poort voor MongoDB, kunt u door Hallo poort in de verbindingsreeks Hallo:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Zie voor meer informatie over verbindingsreeksen MongoDB [verbindingen][MongoConnectionStrings].

## <a name="test-hello-local-deployment"></a>Hallo lokale implementatie testen
selecteert u uw toepassing op uw ontwikkelcomputer toorun **foutopsporing starten** van Hallo **fouten opsporen in** menu of hits **F5**. IIS Express wordt gestart en een browser wordt geopend en de startpagina van de toepassing hello wordt gestart.  Een nieuwe taak toohello MongoDB-database op de virtuele machine in Azure wordt toegevoegd, kunt u toevoegen.

![Mijn taak lijst-toepassing][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>TooAzure App Service Web Apps publiceren
In deze sectie kunt u uw wijzigingen tooAzure App Service Web Apps wilt publiceren.

1. Klik in Solution Explorer met de rechtermuisknop op **MyTaskListApp** opnieuw en klik op **publiceren**.
2. Klik op **Publish**.
   
    U ziet nu uw web-app uitgevoerd in Azure App Service en toegang tot Hallo MongoDB-database in Azure Virtual Machines.

## <a name="summary"></a>Samenvatting
U hebt nu uw ASP.NET-toepassing tooAzure App Service Web Apps is geïmplementeerd. tooview hello web-app:

1. Meld u aan bij hello Azure-Portal.
2. Klik op **Web-apps**. 
3. Selecteer uw web-app in Hallo **Web-Apps** lijst.

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
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
