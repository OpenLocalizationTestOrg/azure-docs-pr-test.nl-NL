---
title: Een REST-API maken in Azure met ASP.NET en SQL DB | Microsoft Docs
description: Een zelfstudie waarmee u u hoe u een app implementeert die gebruikmaakt van de ASP.NET-Web-API aan een Azure-web-app leert met behulp van Visual Studio.
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
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="0c3ac-103">Een REST-service met ASP.NET Web API- en SQL-Database in Azure App Service maken</span><span class="sxs-lookup"><span data-stu-id="0c3ac-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="0c3ac-104">Deze zelfstudie laat zien hoe u een ASP.NET-web-app te implementeren een [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) met behulp van de wizard webpublicatie in Visual Studio 2013 of Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="0c3ac-105">U kunt gratis een Azure-account openen en als u nog geen Visual Studio 2013 hebt, de SDK installeert automatisch Visual Studio 2013 Express Web.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="0c3ac-106">U kunt dus gaan ontwikkelen voor Azure volledig voor gratis.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="0c3ac-107">Deze zelfstudie wordt ervan uitgegaan dat u hebt geen ervaring met Azure.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="0c3ac-108">Op het voltooien van deze zelfstudie hebt u een eenvoudige web-app up en wordt uitgevoerd in de cloud.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="0c3ac-109">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-109">You'll learn:</span></span>

* <span data-ttu-id="0c3ac-110">De computer klaarmaken voor het ontwikkelen van Azure door de Azure SDK te installeren.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="0c3ac-111">Het maken van een Visual Studio ASP.NET MVC 5-project en deze publiceren naar een Azure-app.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="0c3ac-112">Het gebruik van de ASP.NET-Web-API om in te schakelen van Restful-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="0c3ac-113">Het gebruik van een SQL-database voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="0c3ac-114">Hoe om toepassingsupdates te publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="0c3ac-115">U moet een eenvoudige lijst met contactpersonen van een webtoepassing die is gebaseerd op ASP.NET MVC 5 en ADO.NET Entity Framework wordt gebruikt voor toegang tot de database maken.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="0c3ac-116">In de volgende afbeelding wordt de voltooide toepassing weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-116">The following illustration shows the completed application:</span></span>

![Schermafbeelding van de website][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="0c3ac-118">Het project maken</span><span class="sxs-lookup"><span data-stu-id="0c3ac-118">Create the project</span></span>
1. <span data-ttu-id="0c3ac-119">Start Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="0c3ac-120">Van de **bestand** muisklik **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="0c3ac-121">In de **nieuw Project** dialoogvenster Vouw **Visual C#** en selecteer **Web** en selecteer vervolgens **ASP.NET-webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="0c3ac-122">Naam van de toepassing **ContactManager** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![Het dialoogvenster Nieuw project](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="0c3ac-124">In de **nieuw ASP.NET-Project** selecteert u de **MVC** sjabloon selectievakje **Web API** en klik vervolgens op **verificatie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="0c3ac-125">Klik in het dialoogvenster **Verificatie wijzigen** op **Geen verificatie** en vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Geen verificatie](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="0c3ac-127">De voorbeeldtoepassing die u hebt geen functies waarvoor gebruikers zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="0c3ac-128">Zie voor meer informatie over het implementeren van de functies voor verificatie en autorisatie, de [Vervolgstappen](#nextsteps) sectie aan het einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="0c3ac-129">In de **nieuw ASP.NET-Project** dialoogvenster vak, controleert u of de **Host in de Cloud** is ingeschakeld en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="0c3ac-130">Als u hebt eerder niet aangemeld bij Azure, wordt u gevraagd aan te melden.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="0c3ac-131">Een unieke naam op basis van wordt voorgesteld door de configuratiewizard *ContactManager* (Zie de onderstaande afbeelding).</span><span class="sxs-lookup"><span data-stu-id="0c3ac-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="0c3ac-132">Selecteer een regio in de buurt.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-132">Select a region near you.</span></span> <span data-ttu-id="0c3ac-133">U kunt [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") de laagste latentie datacentrum vinden.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="0c3ac-134">Als u een database-server voordat u dit nog niet hebt gemaakt, selecteert u **nieuwe server maken**, een database-gebruikersnaam en wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Azure-Website configureren](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="0c3ac-136">Als u een database-server hebt, gebruikt u dat een nieuwe database te maken.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="0c3ac-137">Database-servers zijn een kostbare resource en u in het algemeen wilt maken van meerdere databases op dezelfde server voor testen en ontwikkeling in plaats van een databaseserver per database maken.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="0c3ac-138">Zorg ervoor dat uw website en de database zich in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-138">Make sure your web site and database are in the same region.</span></span>

![Azure-Website configureren](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="0c3ac-140">Stel de paginakoptekst of -voettekst</span><span class="sxs-lookup"><span data-stu-id="0c3ac-140">Set the page header and footer</span></span>
1. <span data-ttu-id="0c3ac-141">In **Solution Explorer**, vouw de *Views\Shared* map en open de *_Layout.cshtml* bestand.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml in Solution Explorer][newapp004]
2. <span data-ttu-id="0c3ac-143">Vervang de inhoud van de *Views\Shared_Layout.cshtml* bestand met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="0c3ac-144">De bovenstaande opmaak verandert de naam van de app uit de 'Mijn ASP.NET-App' naar 'Contact Manager' en verwijdert deze de koppelingen naar **Start**, **over** en **Contact**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="0c3ac-145">De toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0c3ac-145">Run the application locally</span></span>
1. <span data-ttu-id="0c3ac-146">Druk op CTRL + F5 om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="0c3ac-147">De startpagina van de toepassing wordt weergegeven in de standaardbrowser.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="0c3ac-148">![Naar de startpagina van de takenlijst](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="0c3ac-148">![To Do List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="0c3ac-149">Dit is alles wat u moet doen nu de toepassing die u naar Azure implementeert te maken.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="0c3ac-150">U voegt later databasefunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="0c3ac-151">De toepassing implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="0c3ac-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="0c3ac-152">In Visual Studio met de rechtermuisknop op het project in **Solution Explorer** en selecteer **publiceren** in het contextmenu.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![In het contextmenu project publiceren][PublishVSSolution]
   
    <span data-ttu-id="0c3ac-154">De **webpublicatie** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="0c3ac-155">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-155">Click **Publish**.</span></span>

![Tabblad instellingen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="0c3ac-157">Visual Studio begint het proces van de bestanden zijn gekopieerd naar de Azure-server.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="0c3ac-158">De **uitvoer** venster ziet u welke implementatieacties zijn uitgevoerd en rapporten van de implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="0c3ac-159">De standaardbrowser automatisch geopend op de URL van de geïmplementeerde site.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="0c3ac-160">De toepassing die u hebt gemaakt, wordt nu uitgevoerd in de cloud.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-160">The application you created is now running in the cloud.</span></span>
   
   ![Naar startpagina takenlijst worden uitgevoerd in Azure][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="0c3ac-162">Een database toevoegen aan de toepassing</span><span class="sxs-lookup"><span data-stu-id="0c3ac-162">Add a database to the application</span></span>
<span data-ttu-id="0c3ac-163">Vervolgens moet u de MVC-toepassing te kunnen weergeven en bijwerken van contactpersonen en opslaan van de gegevens in een database bijwerken.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="0c3ac-164">De toepassing gebruikt de Entity Framework voor het maken van de database en voor het lezen en bijwerken van gegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="0c3ac-165">Model gegevensklassen voor contactpersonen toevoegen</span><span class="sxs-lookup"><span data-stu-id="0c3ac-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="0c3ac-166">U begint met het maken van een eenvoudige gegevensmodel in code.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="0c3ac-167">In **Solution Explorer**, met de rechtermuisknop op de map modellen, klik op **toevoegen**, en vervolgens **klasse**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Klasse in het contextmenu modellen toevoegen][adddb001]
2. <span data-ttu-id="0c3ac-169">In de **Add New Item** in het dialoogvenster de naam van het nieuwe klassebestand *Contact.cs*, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Dialoogvenster Nieuw Item toevoegen][adddb002]
3. <span data-ttu-id="0c3ac-171">De inhoud van het bestand Contacts.cs vervangen door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
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

<span data-ttu-id="0c3ac-172">De **Neem contact op met** klasse definieert de gegevens die u voor elke contactpersoon, plus een primaire sleutel, ContactID die nodig is voor de database wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="0c3ac-173">U kunt meer informatie over gegevensmodellen in krijgen de [Vervolgstappen](#nextsteps) sectie aan het einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="0c3ac-174">Webpagina's maken die app-gebruikers werken met de contactpersonen inschakelen</span><span class="sxs-lookup"><span data-stu-id="0c3ac-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="0c3ac-175">De ASP.NET MVC code die wordt uitgevoerd kan automatisch genereren in de functie steigers maken, lezen, bijwerken en verwijderen (CRUD).</span><span class="sxs-lookup"><span data-stu-id="0c3ac-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="0c3ac-176">Een domeincontroller en een weergave voor de gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="0c3ac-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="0c3ac-177">In **Solution Explorer**, vouw de map domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="0c3ac-178">Bouw het project **(Ctrl + Shift + B)**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="0c3ac-179">(U moet het project bouwen voordat steigers mechanisme.)</span><span class="sxs-lookup"><span data-stu-id="0c3ac-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="0c3ac-180">Met de rechtermuisknop op de map Controllers en klik op **toevoegen**, en klik vervolgens op **Controller**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Controller toevoegen in het contextmenu domeincontrollers][addcode001]
4. <span data-ttu-id="0c3ac-182">In de **Add Scaffold** dialoogvenster, **MVC-Controller with views, using Entity Framework** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Controller toevoegen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="0c3ac-184">Naam van de domeincontroller ingesteld op **HomeController**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="0c3ac-185">Selecteer **Contact** als uw modelklasse.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="0c3ac-186">Klik op de **nieuwe gegevenscontext** knop en accepteer de standaardinstelling 'ContactManager.Models.ContactManagerContext' voor de **nieuwe gegevenscontexttype**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="0c3ac-187">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-187">Click **Add**.</span></span>

    <span data-ttu-id="0c3ac-188">Een dialoogvenster wordt u gevraagd: 'een bestand met de naam HomeController al afgesloten.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="0c3ac-189">Wilt u deze vervangen? '.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-189">Do you want to replace it?".</span></span> <span data-ttu-id="0c3ac-190">Klik op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-190">Click **Yes**.</span></span> <span data-ttu-id="0c3ac-191">We wilt de start-domeincontroller die is gemaakt met het nieuwe project overschrijven.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="0c3ac-192">We gebruiken de nieuwe domeincontroller start voor onze lijst met contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="0c3ac-193">Visual Studio maakt de domeincontroller methoden en weergaven voor database-CRUD-bewerkingen voor **Contact** objecten.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="0c3ac-194">Inschakelen van migraties, maak de database, voorbeeldgegevens en een initialisatiefunctie gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="0c3ac-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="0c3ac-195">De volgende taak is om in te schakelen de [Code First-migraties](http://curah.microsoft.com/55220) functie om de database maken op basis van het gegevensmodel dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="0c3ac-196">In de **extra** selecteert u **Library Package Manager** en vervolgens **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Package Manager-Console in het menu Extra][addcode008]
2. <span data-ttu-id="0c3ac-198">In de **Package Manager Console** venster, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="0c3ac-199">De **inschakelen migraties** opdracht maakt u een *migraties* map en plaatst het in de map een *Configuration.cs* -bestand dat u voor het configureren van migraties kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="0c3ac-200">In de **Package Manager Console** venster, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="0c3ac-201">De **toevoegen migratie initiële** opdracht genereert u een klasse met de naam  **&lt;date_stamp&gt;initiële** die de database wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="0c3ac-202">De eerste parameter ( *initiële* ) is een willekeurige en die wordt gebruikt om de naam van het bestand te maken.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="0c3ac-203">Ziet u de nieuwe klassebestanden op **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="0c3ac-204">In de **initiële** klasse, de **Up** methode maakt u de tabel Contactpersonen en de **omlaag** methode (die wordt gebruikt wanneer u wilt terugkeren naar de vorige status) komt het.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="0c3ac-205">Open de *Migrations\Configuration.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="0c3ac-206">Voeg de volgende naamruimten.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="0c3ac-207">Vervang de *Seed* methode met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-207">Replace the *Seed* method with the following code:</span></span>
   
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
   
    <span data-ttu-id="0c3ac-208">Deze bovenstaande code wordt de database met de contactgegevens worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="0c3ac-209">Zie voor meer informatie over het seeding van de database [foutopsporing Entity Framework (EF) databases](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c3ac-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="0c3ac-210">In de **Package Manager Console** Voer de opdracht:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Opdrachten Package Manager-Console][addcode009]
   
    <span data-ttu-id="0c3ac-212">De **database bijwerken** wordt uitgevoerd van de eerste migratie die de database wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="0c3ac-213">Standaard wordt de database gemaakt als een SQL Server Express LocalDB-database.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="0c3ac-214">Druk op CTRL + F5 om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="0c3ac-215">De toepassing geeft de seedgegevens en koppelingen bewerken, details en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![MVC-weergave van gegevens][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="0c3ac-217">De weergave bewerken</span><span class="sxs-lookup"><span data-stu-id="0c3ac-217">Edit the View</span></span>
1. <span data-ttu-id="0c3ac-218">Open de *Views\Home\Index.cshtml* bestand.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="0c3ac-219">In de volgende stap we de gegenereerde opmaak wordt vervangen door de code die gebruikmaakt van [jQuery](http://jquery.com/) en [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="0c3ac-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="0c3ac-220">Deze nieuwe code haalt de lijst met contactpersonen van het gebruik van web-API en JSON en vervolgens contact op met gegevens gebonden aan de gebruikersinterface met behulp van knockout.js.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="0c3ac-221">Zie voor meer informatie de [Vervolgstappen](#nextsteps) sectie aan het einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="0c3ac-222">Vervang de inhoud van het bestand met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-222">Replace the contents of the file with the following code.</span></span>
   
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
3. <span data-ttu-id="0c3ac-223">Met de rechtermuisknop op de map met inhoud en klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item...** .</span><span class="sxs-lookup"><span data-stu-id="0c3ac-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Opmaakmodel toevoegen in de map met inhoud contextmenu][addcode005]
4. <span data-ttu-id="0c3ac-225">In de **Add New Item** dialoogvenster Voer **stijl** in de linkerbovenhoek rechts het zoekvak en selecteer vervolgens **opmaakmodel**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="0c3ac-226">![Dialoogvenster Nieuw Item toevoegen][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="0c3ac-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="0c3ac-227">Noem het bestand *Contacts.css* en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="0c3ac-228">Vervang de inhoud van het bestand met de volgende code.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-228">Replace the contents of the file with the following code.</span></span>
   
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
   
    <span data-ttu-id="0c3ac-229">We gebruiken deze opmaakmodel voor de indeling, kleuren en stijlen die in de app contactpersonen manager worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="0c3ac-230">Open de *App_Start\BundleConfig.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="0c3ac-231">Voeg de volgende code om te registreren de [uitnemen](http://knockoutjs.com/index.html "KO") invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="0c3ac-232">Dit voorbeeld uitnemen met dynamische JavaScript-code die verantwoordelijk is voor de sjablonen scherm vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="0c3ac-233">Wijzig de vermelding inhoud/css registreren de *contacts.css* opmaakmodel.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="0c3ac-234">Wijzig de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="0c3ac-235">Aan:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="0c3ac-236">Voer de volgende opdracht voor het installeren van uitnemen in de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="0c3ac-237">Een controller voor de Web-API Restful-interface toevoegen</span><span class="sxs-lookup"><span data-stu-id="0c3ac-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="0c3ac-238">In **Solution Explorer**, met de rechtermuisknop op domeincontrollers en klik op **toevoegen** en vervolgens **Controller...**</span><span class="sxs-lookup"><span data-stu-id="0c3ac-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="0c3ac-239">In de **Add Scaffold** dialoogvenster Voer **Web API 2-Controller met acties, using Entity Framework** en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![API-controller toevoegen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="0c3ac-241">In de **Controller toevoegen** dialoogvenster Voer 'ContactsController' als de naam van uw domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="0c3ac-242">Selecteer 'Neem contact op met (ContactManager.Models)' voor de **Modelklasse**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="0c3ac-243">Hou de standaardwaarde voor de **Data context class**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="0c3ac-244">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="0c3ac-245">De toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0c3ac-245">Run the application locally</span></span>
1. <span data-ttu-id="0c3ac-246">Druk op CTRL + F5 om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-246">Press CTRL+F5 to run the application.</span></span>
   
    ![De indexpagina][intro001]
2. <span data-ttu-id="0c3ac-248">Voer een contactpersoon in en klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="0c3ac-249">De app wordt naar de startpagina en wordt de contactpersoon die u hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![Indexpagina met lijst taakitems][addwebapi004]
3. <span data-ttu-id="0c3ac-251">In de browser toevoegen **/api/contacts** naar de URL.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="0c3ac-252">De resulterende URL ziet eruit als http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="0c3ac-253">De RESTful-web-API die u toegevoegd retourneert opgeslagen contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="0c3ac-254">Firefox en Chrome worden de gegevens in XML-indeling weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![Indexpagina met lijst taakitems][rxFFchrome]

    <span data-ttu-id="0c3ac-256">IE wordt u gevraagd om te openen of opslaan van de contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-256">IE will prompt you to open or save the contacts.</span></span>

    ![Web-API dialoogvenster Opslaan][addwebapi006]


    <span data-ttu-id="0c3ac-258">U kunt de geretourneerde contactpersonen openen in Kladblok of in een browser.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="0c3ac-259">Deze uitvoer kan worden gebruikt door een andere toepassing, zoals mobiele website of toepassing.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Web-API dialoogvenster Opslaan][addwebapi007]

    <span data-ttu-id="0c3ac-261">**Beveiligingswaarschuwing**: op dit punt uw toepassing is onveilig en kwetsbaar voor aanvallen CSRF.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="0c3ac-262">Verderop in de zelfstudie wordt deze kwetsbaarheid mogelijk verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="0c3ac-263">Zie voor meer informatie [aanvallen te voorkomen dat Cross-Site aanvragen kunnen worden vervalst (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="0c3ac-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="0c3ac-264">XSRF beveiliging toevoegen</span><span class="sxs-lookup"><span data-stu-id="0c3ac-264">Add XSRF Protection</span></span>
<span data-ttu-id="0c3ac-265">Aanvraagvervalsing op meerdere sites (ook wel bekend als XSRF of CSRF) is een aanval tegen web gehoste toepassingen waarbij een schadelijke website invloed hebben op de interactie tussen de browser van de client en een website die wordt vertrouwd door de browser.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="0c3ac-266">Deze aanvallen worden mogelijk gemaakt omdat webbrowsers verificatietokens automatisch met elke aanvraag naar een website wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="0c3ac-267">Het canonieke voorbeeld is een verificatiecookie zoals ASP. NET van formulierverificatie ticket.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="0c3ac-268">Websites die permanente verificatiemechanisme (zoals Windows-verificatie, Basic, enzovoort) te gebruiken kunt echter deze aanvallen zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="0c3ac-269">Een aanval XSRF verschilt van een phishingaanval.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="0c3ac-270">Phishingaanvallen vereist interactie van het slachtoffer.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="0c3ac-271">Bij een phishingaanval een schadelijke website nabootsen de doelwebsite en het slachtoffer is misleiden in gevoelige informatie opgeeft voor de aanvaller.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="0c3ac-272">Bij een aanval XSRF is vaak geen tussenkomst van het slachtoffer nodig.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="0c3ac-273">In plaats daarvan wordt de aanvaller vertrouwen op de browser alle relevante cookies automatisch wordt verzonden naar de website van de bestemming.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="0c3ac-274">Zie voor meer informatie de [beveiliging Open Webtoepassingsproject](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="0c3ac-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="0c3ac-275">In **Solution Explorer**, rechts **ContactManager** project en klik op **toevoegen** en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="0c3ac-276">Noem het bestand *ValidateHttpAntiForgeryTokenAttribute.cs* en voeg de volgende code:</span><span class="sxs-lookup"><span data-stu-id="0c3ac-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
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
3. <span data-ttu-id="0c3ac-277">Voeg de volgende *met* instructie naar de controller contracten zodat u toegang tot hebt de **[ValidateHttpAntiForgeryToken]** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="0c3ac-278">Voeg de **[ValidateHttpAntiForgeryToken]** kenmerk aan de Post-methoden van de **ContactsController** te beveiligen tegen bedreigingen XSRF.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="0c3ac-279">U gaat deze toevoegen aan de 'PutContact', 'PostContact' en **DeleteContact** actiemethoden.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="0c3ac-280">Update de *Scripts* sectie van de *Views\Home\Index.cshtml* dat moet worden opgenomen code om de XSRF-tokens.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
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

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="0c3ac-281">Het bijwerken van de toepassing publiceren naar Azure en SQL-Database</span><span class="sxs-lookup"><span data-stu-id="0c3ac-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="0c3ac-282">Voor het publiceren van de toepassing, moet u de procedure die u eerder hebt gevolgd herhalen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="0c3ac-283">In **Solution Explorer**, klik met de rechtermuisknop op het project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![Publiceren][rxP]
2. <span data-ttu-id="0c3ac-285">Klik op het tabblad **Settings**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="0c3ac-286">Onder **ContactsManagerContext(ContactsManagerContext)**, klikt u op de **v** pictogram wijzigen *externe verbindingsreeks* de verbindingsreeks voor de database van contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="0c3ac-287">Klik op **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-287">Click **ContactDB**.</span></span>
   
    ![Instellingen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="0c3ac-289">Schakel het selectievakje voor **uitvoeren Code First-migraties (wordt uitgevoerd op de start van toepassing)**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="0c3ac-290">Klik op **volgende** en klik vervolgens op **Preview**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="0c3ac-291">Visual Studio geeft een lijst van de bestanden die worden toegevoegd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="0c3ac-292">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-292">Click **Publish**.</span></span>
   <span data-ttu-id="0c3ac-293">Nadat de implementatie is voltooid, wordt de browser geopend met de startpagina van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Indexpagina met geen contactpersonen][intro001]
   
    <span data-ttu-id="0c3ac-295">De Visual Studio publicatieproces automatisch geconfigureerd van de verbindingsreeks in het geïmplementeerde *Web.config* bestand om te verwijzen naar de SQL-database.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="0c3ac-296">Deze Code First-migraties om automatisch de database bijwerken naar de nieuwste versie de eerste keer dat de toepassing toegang heeft tot de database na de implementatie ook geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="0c3ac-297">Als gevolg van deze configuratie Code First de database is gemaakt door de code in de **initiële** klasse die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="0c3ac-298">Het is dit de eerste keer dat de toepassing heeft geprobeerd toegang tot de database na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="0c3ac-299">Voer een contactpersoon als toen u de app lokaal hebt uitgevoerd om te controleren of de implementatie van de database is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="0c3ac-300">Als u ziet dat het item dat u invoert, wordt opgeslagen en wordt weergegeven op de pagina contact op met manager, weet u dat deze is opgeslagen in de database.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![Pagina van de index met contactpersonen][addwebapi004]

<span data-ttu-id="0c3ac-302">De toepassing wordt nu uitgevoerd in de cloud, met behulp van SQL-Database voor het opslaan van gegevens.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="0c3ac-303">Nadat u de toepassing testen in Azure, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="0c3ac-304">De toepassing openbaar en beschikt niet over een mechanisme om toegang te beperken.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="0c3ac-305">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0c3ac-306">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0c3ac-307">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c3ac-307">Next Steps</span></span>
<span data-ttu-id="0c3ac-308">Gegevens opslaan in een Azure-toepassing op een andere manier is het gebruik van Azure-opslag, die niet-relationele gegevensopslag in de vorm van blobs en tabellen bieden.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-308">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="0c3ac-309">De volgende koppelingen bieden meer informatie op Web-API, ASP.NET MVC en Azure-venster.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-309">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="0c3ac-310">[Aan de slag met Entity Framework met MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="0c3ac-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="0c3ac-311">Inleiding tot de ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="0c3ac-311">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="0c3ac-312">Uw eerste ASP.NET-Web-API</span><span class="sxs-lookup"><span data-stu-id="0c3ac-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="0c3ac-313">Foutopsporing WAWS</span><span class="sxs-lookup"><span data-stu-id="0c3ac-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="0c3ac-314">Deze zelfstudie en de voorbeeldtoepassing is geschreven door [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) met ondersteuning van Tom Dykstra en Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="0c3ac-314">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="0c3ac-315">Neem verbeterd laat feedback over wat u beviel of wat u graag, niet alleen over de zelfstudie zelf, maar ook over de producten die deze laat zien.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-315">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="0c3ac-316">Uw feedback helpt ons prioriteren verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="0c3ac-317">We zijn met name geïnteresseerd te komen hoeveel interesse in meer automation voor het proces van het configureren en implementeren van de lidmaatschapsdatabase.</span><span class="sxs-lookup"><span data-stu-id="0c3ac-317">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="0c3ac-318">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="0c3ac-318">What's changed</span></span>
* <span data-ttu-id="0c3ac-319">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="0c3ac-319">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
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

