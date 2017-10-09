---
title: aaaCreate een REST-API in Azure met ASP.NET en SQL-database | Microsoft Docs
description: Een zelfstudie die leert u hoe toodeploy een app die gebruikmaakt van ASP.NET Web API tooan Azure-web-app Hallo met behulp van Visual Studio.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="c4456-103">Een REST-service met ASP.NET Web API- en SQL-Database in Azure App Service maken</span><span class="sxs-lookup"><span data-stu-id="c4456-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="c4456-104">Deze zelfstudie laat zien hoe toodeploy een ASP.NET web-app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) met Hallo webpublicatie wizard in Visual Studio 2013 of Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="c4456-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="c4456-105">U kunt gratis een Azure-account openen en als u nog geen Visual Studio 2013 hebt, Hallo SDK installeert automatisch Visual Studio 2013 Express Web.</span><span class="sxs-lookup"><span data-stu-id="c4456-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="c4456-106">U kunt dus gaan ontwikkelen voor Azure volledig voor gratis.</span><span class="sxs-lookup"><span data-stu-id="c4456-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="c4456-107">Deze zelfstudie wordt ervan uitgegaan dat u hebt geen ervaring met Azure.</span><span class="sxs-lookup"><span data-stu-id="c4456-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="c4456-108">Op het voltooien van deze zelfstudie hebt u een eenvoudige web-app up en wordt uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="c4456-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="c4456-109">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="c4456-109">You'll learn:</span></span>

* <span data-ttu-id="c4456-110">Hoe tooenable computer klaarmaken voor het ontwikkelen van Azure door het installeren van hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="c4456-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="c4456-111">Hoe toocreate een ASP.NET MVC 5 voor Visual Studio-project en publiceer deze tooan Apps van Azure.</span><span class="sxs-lookup"><span data-stu-id="c4456-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="c4456-112">Hoe toouse Hallo ASP.NET Web API tooenable Restful-API aanroept.</span><span class="sxs-lookup"><span data-stu-id="c4456-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="c4456-113">Hoe toouse een SQL-database toostore gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4456-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="c4456-114">Hoe werkt toopublish toepassing tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c4456-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="c4456-115">U moet een eenvoudige lijst met contactpersonen-webtoepassing die is gebouwd op ASP.NET MVC 5 bouwen en maakt gebruik van hello ADO.NET Entity Framework voor toegang tot de database.</span><span class="sxs-lookup"><span data-stu-id="c4456-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="c4456-116">Hallo volgende afbeelding toont Hallo voltooid toepassing:</span><span class="sxs-lookup"><span data-stu-id="c4456-116">hello following illustration shows hello completed application:</span></span>

![Schermafbeelding van de website][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="c4456-118">Hallo-project maken</span><span class="sxs-lookup"><span data-stu-id="c4456-118">Create hello project</span></span>
1. <span data-ttu-id="c4456-119">Start Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c4456-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="c4456-120">Van Hallo **bestand** muisklik **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="c4456-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="c4456-121">In Hallo **nieuw Project** dialoogvenster Vouw **Visual C#** en selecteer **Web** en selecteer vervolgens **ASP.NET-webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="c4456-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="c4456-122">Naam van de toepassing hello **ContactManager** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4456-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Het dialoogvenster Nieuw project](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="c4456-124">In Hallo **nieuw ASP.NET-Project** dialoogvenster, selecteer Hallo **MVC** sjabloon selectievakje **Web API** en klik vervolgens op **verificatie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="c4456-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="c4456-125">In Hallo **verificatie wijzigen** in het dialoogvenster, klikt u op **geen verificatie**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4456-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Geen verificatie](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="c4456-127">Hallo-voorbeeldtoepassing die u hebt geen functies waarvoor gebruikers toolog in.</span><span class="sxs-lookup"><span data-stu-id="c4456-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="c4456-128">Voor informatie over het tooimplement verificatie en autorisatie Zie Hallo [Vervolgstappen](#nextsteps) sectie op Hallo einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c4456-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="c4456-129">In Hallo **nieuw ASP.NET-Project** dialoogvenster, zorg ervoor dat Hallo **Host in Cloud Hallo** is ingeschakeld en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4456-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="c4456-130">Als u tooAzure eerder niet hebt aangemeld, kunt u zich na vragen aan gebruiker toosign in.</span><span class="sxs-lookup"><span data-stu-id="c4456-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="c4456-131">Hallo-configuratiewizard worden voorgesteld een unieke naam op basis van *ContactManager* (Zie onderstaande Hallo afbeelding).</span><span class="sxs-lookup"><span data-stu-id="c4456-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="c4456-132">Selecteer een regio in de buurt.</span><span class="sxs-lookup"><span data-stu-id="c4456-132">Select a region near you.</span></span> <span data-ttu-id="c4456-133">U kunt [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind Hallo laagste latentie Datacenter.</span><span class="sxs-lookup"><span data-stu-id="c4456-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="c4456-134">Als u een database-server voordat u dit nog niet hebt gemaakt, selecteert u **nieuwe server maken**, een database-gebruikersnaam en wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="c4456-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Azure-Website configureren](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="c4456-136">Als u een database-server hebt, gebruikt u die toocreate een nieuwe database.</span><span class="sxs-lookup"><span data-stu-id="c4456-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="c4456-137">Database-servers zijn een kostbare resource, en u in het algemeen wilt toocreate meerdere databases op Hallo dezelfde server voor testen en ontwikkeling in plaats van een databaseserver per database maken.</span><span class="sxs-lookup"><span data-stu-id="c4456-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="c4456-138">Controleer of uw website en database in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="c4456-138">Make sure your web site and database are in hello same region.</span></span>

![Azure-Website configureren](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="c4456-140">Hallo paginakoptekst of -voettekst instellen</span><span class="sxs-lookup"><span data-stu-id="c4456-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="c4456-141">In **Solution Explorer**, vouw Hallo *Views\Shared* map en open Hallo *_Layout.cshtml* bestand.</span><span class="sxs-lookup"><span data-stu-id="c4456-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml in Solution Explorer][newapp004]
2. <span data-ttu-id="c4456-143">Vervang de inhoud Hallo Hallo *Views\Shared_Layout.cshtml* bestand met de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="c4456-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="c4456-144">Hallo markup hierboven wijzigingen Hallo app-naam van de 'Mijn ASP.NET-App' te ' Contact Manager ', maar verwijdert Hallo koppelingen te**Start**, **over** en **Contact**.</span><span class="sxs-lookup"><span data-stu-id="c4456-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="c4456-145">Hallo-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c4456-145">Run hello application locally</span></span>
1. <span data-ttu-id="c4456-146">Druk op CTRL + F5 toorun Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4456-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="c4456-147">startpagina Hallo-toepassing wordt weergegeven in de standaardbrowser Hallo.</span><span class="sxs-lookup"><span data-stu-id="c4456-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="c4456-148">![tooDo lijst-startpagina](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="c4456-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="c4456-149">Dit is alles wat dat u nodig toodo voor nu toocreate Hallo toepassing dat u tooAzure implementeert.</span><span class="sxs-lookup"><span data-stu-id="c4456-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="c4456-150">U voegt later databasefunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="c4456-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="c4456-151">Hallo toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="c4456-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="c4456-152">In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer** en selecteer **publiceren** in het contextmenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="c4456-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![In het contextmenu project publiceren][PublishVSSolution]
   
    <span data-ttu-id="c4456-154">Hallo **webpublicatie** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c4456-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="c4456-155">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="c4456-155">Click **Publish**.</span></span>

![Tabblad instellingen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="c4456-157">Visual Studio begint Hallo proces van het kopiëren van Hallo bestanden toohello Azure-server.</span><span class="sxs-lookup"><span data-stu-id="c4456-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="c4456-158">Hallo **uitvoer** venster ziet u welke implementatieacties zijn uitgevoerd en rapporteert Hallo-implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c4456-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="c4456-159">Hallo standaardbrowser automatisch geopend toohello URL van de site Hallo geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c4456-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="c4456-160">Hallo-toepassing die u hebt gemaakt, wordt nu uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="c4456-160">hello application you created is now running in hello cloud.</span></span>
   
   ![tooDo lijst-startpagina worden uitgevoerd in Azure][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="c4456-162">Een database toohello toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4456-162">Add a database toohello application</span></span>
<span data-ttu-id="c4456-163">Vervolgens moet u Hallo MVC-toepassing tooadd Hallo mogelijkheid toodisplay bijwerken en contactpersonen bijwerken en Hallo gegevens opslaan in een database.</span><span class="sxs-lookup"><span data-stu-id="c4456-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="c4456-164">Hallo-toepassing hello Entity Framework toocreate Hallo database en tooread gebruikt en gegevens in Hallo-database bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c4456-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="c4456-165">Model gegevensklassen voor Hallo contactpersonen toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4456-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="c4456-166">U begint met het maken van een eenvoudige gegevensmodel in code.</span><span class="sxs-lookup"><span data-stu-id="c4456-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="c4456-167">In **Solution Explorer**, met de rechtermuisknop op de map modellen hello, klik op **toevoegen**, en vervolgens **klasse**.</span><span class="sxs-lookup"><span data-stu-id="c4456-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Klasse in het contextmenu modellen toevoegen][adddb001]
2. <span data-ttu-id="c4456-169">In Hallo **Add New Item** in het dialoogvenster, naam Hallo nieuwe klassebestand *Contact.cs*, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c4456-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Dialoogvenster Nieuw Item toevoegen][adddb002]
3. <span data-ttu-id="c4456-171">Hallo inhoud van Hallo Contacts.cs bestand vervangen door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="c4456-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="c4456-172">Hallo **Neem contact op met** klasse definieert Hallo-gegevens die u voor elke contactpersoon, plus een primaire sleutel, ContactID die nodig is voor het Hallo-database wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="c4456-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="c4456-173">U kunt meer informatie over gegevensmodellen krijgen in Hallo [Vervolgstappen](#nextsteps) sectie op Hallo einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c4456-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="c4456-174">Webpagina's maken die de app gebruikers toowork met Hallo contactpersonen inschakelen</span><span class="sxs-lookup"><span data-stu-id="c4456-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="c4456-175">Hallo ASP.NET MVC Hallo steigers functie kan automatisch code gegenereerd waarmee maken, lezen, bijwerken en verwijderen (CRUD).</span><span class="sxs-lookup"><span data-stu-id="c4456-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="c4456-176">Een domeincontroller en een weergave voor Hallo gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4456-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="c4456-177">In **Solution Explorer**, vouw de map Hallo-Controllers.</span><span class="sxs-lookup"><span data-stu-id="c4456-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="c4456-178">Bouw Hallo project **(Ctrl + Shift + B)**.</span><span class="sxs-lookup"><span data-stu-id="c4456-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="c4456-179">(U moet Hallo project bouwen voordat steigers mechanisme.)</span><span class="sxs-lookup"><span data-stu-id="c4456-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="c4456-180">Met de rechtermuisknop op de map Hallo-Controllers en klik op **toevoegen**, en klik vervolgens op **Controller**.</span><span class="sxs-lookup"><span data-stu-id="c4456-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Controller toevoegen in het contextmenu domeincontrollers][addcode001]
4. <span data-ttu-id="c4456-182">In Hallo **Add Scaffold** dialoogvenster, **MVC-Controller with views, using Entity Framework** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c4456-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Controller toevoegen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="c4456-184">Hallo controllernaam te ingesteld**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="c4456-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="c4456-185">Selecteer **Contact** als uw modelklasse.</span><span class="sxs-lookup"><span data-stu-id="c4456-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="c4456-186">Klik op Hallo **nieuwe gegevenscontext** knop en standaardoptie Hallo 'ContactManager.Models.ContactManagerContext' voor Hallo **nieuwe gegevenscontexttype**.</span><span class="sxs-lookup"><span data-stu-id="c4456-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="c4456-187">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="c4456-187">Click **Add**.</span></span>

    <span data-ttu-id="c4456-188">Een dialoogvenster wordt u gevraagd: 'een bestand met de naam Hallo HomeController al afgesloten.</span><span class="sxs-lookup"><span data-stu-id="c4456-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="c4456-189">Wilt u toch tooreplace deze? '.</span><span class="sxs-lookup"><span data-stu-id="c4456-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="c4456-190">Klik op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c4456-190">Click **Yes**.</span></span> <span data-ttu-id="c4456-191">We wilt Hallo Start de domeincontroller die is gemaakt met de Hallo nieuw project overschrijven.</span><span class="sxs-lookup"><span data-stu-id="c4456-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="c4456-192">We gebruiken Hallo nieuwe start Controller voor onze lijst met contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="c4456-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="c4456-193">Visual Studio maakt de domeincontroller methoden en weergaven voor database-CRUD-bewerkingen voor **Contact** objecten.</span><span class="sxs-lookup"><span data-stu-id="c4456-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="c4456-194">Inschakelen van migraties, het Hallo-database maken, het toevoegen van voorbeeldgegevens en een initialisatiefunctie voor gegevens</span><span class="sxs-lookup"><span data-stu-id="c4456-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="c4456-195">de volgende taak Hallo is tooenable hello [Code First-migraties](http://curah.microsoft.com/55220) functie in volgorde toocreate Hallo database op basis van Hallo-gegevensmodel die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4456-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="c4456-196">In Hallo **extra** selecteert u **Library Package Manager** en vervolgens **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="c4456-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Package Manager-Console in het menu Extra][addcode008]
2. <span data-ttu-id="c4456-198">In Hallo **Package Manager Console** venster Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c4456-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="c4456-199">Hallo **inschakelen migraties** opdracht maakt u een *migraties* map en plaatst het in de map een *Configuration.cs* bestand dat u tooconfigure migraties kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="c4456-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="c4456-200">In Hallo **Package Manager Console** venster Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c4456-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="c4456-201">Hallo **toevoegen migratie initiële** opdracht genereert u een klasse met de naam  **&lt;date_stamp&gt;initiële** die Hallo-database wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4456-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="c4456-202">de eerste parameter Hallo ( *initiële* ) is willekeurig en gebruikte toocreate Hallo-naam van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="c4456-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="c4456-203">U kunt zien Hallo bestanden met betrekking tot een nieuwe klasse in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c4456-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="c4456-204">In Hallo **initiële** klasse hello **Up** methode maakt u tabel Hallo-contactpersonen en Hallo **omlaag** methode (die wordt gebruikt als u wilt dat de vorige status van tooreturn toohello) komt het.</span><span class="sxs-lookup"><span data-stu-id="c4456-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="c4456-205">Open Hallo *Migrations\Configuration.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="c4456-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="c4456-206">Hallo na naamruimten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c4456-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="c4456-207">Vervang Hallo *Seed* methode Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="c4456-207">Replace hello *Seed* method with hello following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="c4456-208">Deze bovenstaande code wordt Hallo-database met contactgegevens Hallo initialiseren.</span><span class="sxs-lookup"><span data-stu-id="c4456-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="c4456-209">Zie voor meer informatie over het Hallo database seeding [foutopsporing Entity Framework (EF) databases](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4456-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="c4456-210">In Hallo **Package Manager Console** Voer Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="c4456-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Opdrachten Package Manager-Console][addcode009]
   
    <span data-ttu-id="c4456-212">Hallo **database bijwerken** wordt uitgevoerd Hallo eerste migratie die Hallo-database wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4456-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="c4456-213">Standaard Hallo-database gemaakt als een SQL Server Express LocalDB-database.</span><span class="sxs-lookup"><span data-stu-id="c4456-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="c4456-214">Druk op CTRL + F5 toorun Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4456-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="c4456-215">Hallo-toepassing hello seedgegevens worden weergegeven en wordt bewerken, details en verwijderkoppelingen.</span><span class="sxs-lookup"><span data-stu-id="c4456-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![MVC-weergave van gegevens][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="c4456-217">Hallo weergave bewerken</span><span class="sxs-lookup"><span data-stu-id="c4456-217">Edit hello View</span></span>
1. <span data-ttu-id="c4456-218">Open Hallo *Views\Home\Index.cshtml* bestand.</span><span class="sxs-lookup"><span data-stu-id="c4456-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="c4456-219">In de volgende stap Hallo we Hallo gegenereerd markup wordt vervangen door de code die wordt gebruikt [jQuery](http://jquery.com/) en [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="c4456-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="c4456-220">Deze nieuwe code haalt Hallo lijst met contactpersonen uit met behulp van web-API en JSON en vervolgens bindingen Hallo contact op met de gegevens toohello UI knockout.js gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c4456-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="c4456-221">Zie voor meer informatie, Hallo [Vervolgstappen](#nextsteps) sectie op Hallo einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c4456-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="c4456-222">Hallo-inhoud van Hallo-bestand met de volgende code Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="c4456-222">Replace hello contents of hello file with hello following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="c4456-223">Met de rechtermuisknop op de map met inhoud Hallo en klik op **toevoegen**, en klik vervolgens op **Nieuw Item...** .</span><span class="sxs-lookup"><span data-stu-id="c4456-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Opmaakmodel toevoegen in de map met inhoud contextmenu][addcode005]
4. <span data-ttu-id="c4456-225">In Hallo **Add New Item** dialoogvenster Voer **stijl** in de bovenste rechts zoekvak Hallo en selecteer vervolgens **opmaakmodel**.</span><span class="sxs-lookup"><span data-stu-id="c4456-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="c4456-226">![Dialoogvenster Nieuw Item toevoegen][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="c4456-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="c4456-227">Bestand met de Hallo *Contacts.css* en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c4456-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="c4456-228">Hallo-inhoud van Hallo-bestand met de volgende code Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="c4456-228">Replace hello contents of hello file with hello following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="c4456-229">We gebruiken deze opmaakmodel voor Hallo opmaak, kleuren en stijlen in Hallo contact manager-app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c4456-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="c4456-230">Open Hallo *App_Start\BundleConfig.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="c4456-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="c4456-231">Toevoegen van de volgende code tooregister Hallo Hallo [uitnemen](http://knockoutjs.com/index.html "KO") invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c4456-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="c4456-232">Dit voorbeeld met uitnemen toosimplify dynamische JavaScript-code die verantwoordelijk is voor Hallo scherm sjablonen.</span><span class="sxs-lookup"><span data-stu-id="c4456-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="c4456-233">Hallo inhoud/css vermelding tooregister Hallo wijzigen *contacts.css* opmaakmodel.</span><span class="sxs-lookup"><span data-stu-id="c4456-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="c4456-234">Hallo volgt regel wijzigen:</span><span class="sxs-lookup"><span data-stu-id="c4456-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="c4456-235">Aan:</span><span class="sxs-lookup"><span data-stu-id="c4456-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="c4456-236">Voer in Hallo Package Manager-Console, Hallo opdracht tooinstall uitname te volgen.</span><span class="sxs-lookup"><span data-stu-id="c4456-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="c4456-237">Een controller voor Web-API Restful Hallo-interface toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4456-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="c4456-238">In **Solution Explorer**, met de rechtermuisknop op domeincontrollers en klik op **toevoegen** en vervolgens **Controller...**</span><span class="sxs-lookup"><span data-stu-id="c4456-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="c4456-239">In Hallo **Add Scaffold** dialoogvenster Voer **Web API 2-Controller met acties, using Entity Framework** en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c4456-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![API-controller toevoegen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="c4456-241">In Hallo **Controller toevoegen** dialoogvenster Voer 'ContactsController' als de naam van uw domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="c4456-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="c4456-242">Selecteer 'Neem contact op met (ContactManager.Models)' voor Hallo **Modelklasse**.</span><span class="sxs-lookup"><span data-stu-id="c4456-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="c4456-243">Hou de standaardwaarde Hallo voor Hallo **Data context class**.</span><span class="sxs-lookup"><span data-stu-id="c4456-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="c4456-244">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="c4456-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="c4456-245">Hallo-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c4456-245">Run hello application locally</span></span>
1. <span data-ttu-id="c4456-246">Druk op CTRL + F5 toorun Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4456-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![De indexpagina][intro001]
2. <span data-ttu-id="c4456-248">Voer een contactpersoon in en klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c4456-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="c4456-249">Hallo app retourneert toohello startpagina en geeft weer Hallo contactpersoon die u hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="c4456-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Indexpagina met lijst taakitems][addwebapi004]
3. <span data-ttu-id="c4456-251">In de browser Hallo toevoegen **/api/contacts** toohello URL.</span><span class="sxs-lookup"><span data-stu-id="c4456-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="c4456-252">Hallo resulterende URL ziet eruit als http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="c4456-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="c4456-253">Hallo RESTful-web-API die u hebt toegevoegd retourneert Hallo opgeslagen contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="c4456-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="c4456-254">Firefox en Chrome weergegeven Hallo gegevens in de XML-indeling.</span><span class="sxs-lookup"><span data-stu-id="c4456-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Indexpagina met lijst taakitems][rxFFchrome]

    <span data-ttu-id="c4456-256">Internet Explorer wordt u tooopen gevraagd of Hallo contactpersonen opslaan.</span><span class="sxs-lookup"><span data-stu-id="c4456-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Web-API dialoogvenster Opslaan][addwebapi006]


    <span data-ttu-id="c4456-258">U kunt Hallo contactpersonen geretourneerd in Kladblok of in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="c4456-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="c4456-259">Deze uitvoer kan worden gebruikt door een andere toepassing, zoals mobiele website of toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4456-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Web-API dialoogvenster Opslaan][addwebapi007]

    <span data-ttu-id="c4456-261">**Beveiligingswaarschuwing**: op dit punt uw toepassing is onveilig en kwetsbaar tooCSRF aanval.</span><span class="sxs-lookup"><span data-stu-id="c4456-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="c4456-262">Verderop in de zelfstudie Hallo wordt deze kwetsbaarheid verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c4456-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="c4456-263">Zie voor meer informatie [aanvallen te voorkomen dat Cross-Site aanvragen kunnen worden vervalst (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="c4456-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="c4456-264">XSRF beveiliging toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4456-264">Add XSRF Protection</span></span>
<span data-ttu-id="c4456-265">Aanvraagvervalsing op meerdere sites (ook wel bekend als XSRF of CSRF) is een aanval tegen web gehoste toepassingen waarbij een schadelijke website Hallo interactie tussen de browser van de client en een website die wordt vertrouwd door de browser kan beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="c4456-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="c4456-266">Deze aanvallen worden mogelijk gemaakt omdat webbrowsers verificatietokens automatisch met elke aanvraag tooa website wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="c4456-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="c4456-267">Hallo canonieke voorbeeld is een verificatiecookie zoals ASP. NET van formulierverificatie ticket.</span><span class="sxs-lookup"><span data-stu-id="c4456-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="c4456-268">Websites die permanente verificatiemechanisme (zoals Windows-verificatie, Basic, enzovoort) te gebruiken kunt echter deze aanvallen zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="c4456-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="c4456-269">Een aanval XSRF verschilt van een phishingaanval.</span><span class="sxs-lookup"><span data-stu-id="c4456-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="c4456-270">Phishingaanvallen vereisen interactie van Hallo slachtoffer.</span><span class="sxs-lookup"><span data-stu-id="c4456-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="c4456-271">Bij een phishingaanval een schadelijke website nabootsen Hallo doelwebsite en Hallo slachtoffer is misleiden in gevoelige informatie toohello aanvaller bieden.</span><span class="sxs-lookup"><span data-stu-id="c4456-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="c4456-272">Bij een aanval XSRF is vaak geen tussenkomst van Hallo slachtoffer nodig.</span><span class="sxs-lookup"><span data-stu-id="c4456-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="c4456-273">In plaats daarvan wordt de aanvaller Hallo vertrouwen op Hallo browser automatisch alle relevante cookies toohello bestemming website wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="c4456-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="c4456-274">Zie voor meer informatie, Hallo [beveiliging Open Webtoepassingsproject](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="c4456-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="c4456-275">In **Solution Explorer**, rechts **ContactManager** project en klik op **toevoegen** en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="c4456-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="c4456-276">Bestand met de Hallo *ValidateHttpAntiForgeryTokenAttribute.cs* en Hallo volgende code toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="c4456-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="c4456-277">Voeg de volgende Hallo *met* instructie toohello contracten controller zodat u toegang tot toohello hebt **[ValidateHttpAntiForgeryToken]** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="c4456-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="c4456-278">Hallo toevoegen **[ValidateHttpAntiForgeryToken]** toohello Post-methoden van Hallo kenmerk **ContactsController** tooprotect uit XSRF bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="c4456-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="c4456-279">U toohello 'PutContact', 'PostContact' wordt toegevoegd en **DeleteContact** actiemethoden.</span><span class="sxs-lookup"><span data-stu-id="c4456-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="c4456-280">Update Hallo *Scripts* sectie Hallo *Views\Home\Index.cshtml* tooinclude code tooget hello XSRF tokens bestand.</span><span class="sxs-lookup"><span data-stu-id="c4456-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="c4456-281">Hallo toepassing update tooAzure en SQL-Database publiceren</span><span class="sxs-lookup"><span data-stu-id="c4456-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="c4456-282">-toepassing hello toopublish u herhalen Hallo procedure die u eerder hebt gevolgd.</span><span class="sxs-lookup"><span data-stu-id="c4456-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="c4456-283">In **Solution Explorer**, klik met de rechtermuisknop op Hallo-project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="c4456-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Publiceren][rxP]
2. <span data-ttu-id="c4456-285">Klik op Hallo **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c4456-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="c4456-286">Onder **ContactsManagerContext(ContactsManagerContext)**, klikt u op Hallo **v** pictogram toochange *externe verbindingsreeks* toohello verbindingsreeks voor Hallo contact op met de database.</span><span class="sxs-lookup"><span data-stu-id="c4456-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="c4456-287">Klik op **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="c4456-287">Click **ContactDB**.</span></span>
   
    ![Instellingen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="c4456-289">Hallo selectievakje voor **uitvoeren Code First-migraties (wordt uitgevoerd op de start van toepassing)**.</span><span class="sxs-lookup"><span data-stu-id="c4456-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="c4456-290">Klik op **volgende** en klik vervolgens op **Preview**.</span><span class="sxs-lookup"><span data-stu-id="c4456-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="c4456-291">Visual Studio geeft een lijst van Hallo-bestanden die worden toegevoegd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c4456-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="c4456-292">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="c4456-292">Click **Publish**.</span></span>
   <span data-ttu-id="c4456-293">Nadat het Hallo-implementatie is voltooid, wordt in het Hallo browser toohello startpagina van de toepassing hello geopend.</span><span class="sxs-lookup"><span data-stu-id="c4456-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Indexpagina met geen contactpersonen][intro001]
   
    <span data-ttu-id="c4456-295">Hallo Visual Studio automatisch geconfigureerd proces Hallo verbindingsreeks publiceren in Hallo geïmplementeerd *Web.config* bestand toopoint toohello SQL-database.</span><span class="sxs-lookup"><span data-stu-id="c4456-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="c4456-296">Deze Code First-migraties tooautomatically upgrade Hallo database toohello meest recente versie Hallo eerste tijd Hallo toepassing toegang heeft tot Hallo database na de implementatie ook geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c4456-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="c4456-297">Als gevolg van deze configuratie Code First Hallo database gemaakt Hallo code wordt uitgevoerd in Hallo **initiële** klasse die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4456-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="c4456-298">Die gold deze Hallo eerste tijd Hallo geprobeerd tooaccess Hallo toepassingsdatabase na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c4456-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="c4456-299">Voer een contactpersoon zoals u deed toen u uitvoerde Hallo app lokaal tooverify die database-implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c4456-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="c4456-300">Als u ziet dat u invoert Hallo-item wordt opgeslagen en wordt weergegeven op de pagina van de contactpersoon manager hello, weet u dat deze is opgeslagen in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="c4456-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Pagina van de index met contactpersonen][addwebapi004]

<span data-ttu-id="c4456-302">Hallo toepassing wordt nu uitgevoerd in de cloud Hallo toostore SQL-Database met de gegevens.</span><span class="sxs-lookup"><span data-stu-id="c4456-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="c4456-303">Nadat u Hallo toepassing testen in Azure, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c4456-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="c4456-304">Hallo toepassing openbaar en heeft geen een mechanisme toolimit toegang.</span><span class="sxs-lookup"><span data-stu-id="c4456-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="c4456-305">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="c4456-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c4456-306">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="c4456-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c4456-307">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4456-307">Next Steps</span></span>
<span data-ttu-id="c4456-308">Een andere manier toostore-gegevens in een Azure-toepassing is toouse Azure-opslag, die niet-relationele gegevensopslag in Hallo vorm van blobs en tabellen bevatten.</span><span class="sxs-lookup"><span data-stu-id="c4456-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="c4456-309">Hallo volgende koppelingen bieden meer informatie op Web-API, ASP.NET MVC en Azure-venster.</span><span class="sxs-lookup"><span data-stu-id="c4456-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="c4456-310">[Aan de slag met Entity Framework met MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="c4456-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="c4456-311">Inleiding tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="c4456-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="c4456-312">Uw eerste ASP.NET-Web-API</span><span class="sxs-lookup"><span data-stu-id="c4456-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="c4456-313">Foutopsporing WAWS</span><span class="sxs-lookup"><span data-stu-id="c4456-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="c4456-314">Deze zelfstudie en Hallo voorbeeldtoepassing is geschreven door [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) met ondersteuning van Tom Dykstra en Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="c4456-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="c4456-315">Geef feedback op wat u beviel of wat u graag verbeterd, niet alleen over Hallo-zelfstudie zelf, maar ook over Hallo producten die laat toosee.</span><span class="sxs-lookup"><span data-stu-id="c4456-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="c4456-316">Uw feedback helpt ons prioriteren verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="c4456-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="c4456-317">We zijn met name geïnteresseerd te komen hoeveel interesse er bevindt zich in meer automatisering voor Hallo proces van het configureren en implementeren van Hallo-lidmaatschapsdatabase.</span><span class="sxs-lookup"><span data-stu-id="c4456-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="c4456-318">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="c4456-318">What's changed</span></span>
* <span data-ttu-id="c4456-319">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c4456-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

