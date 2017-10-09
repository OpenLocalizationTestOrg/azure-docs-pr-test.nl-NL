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
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Een REST-service met ASP.NET Web API- en SQL-Database in Azure App Service maken
Deze zelfstudie laat zien hoe toodeploy een ASP.NET web-app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) met Hallo webpublicatie wizard in Visual Studio 2013 of Visual Studio 2013 Community Edition. 

U kunt gratis een Azure-account openen en als u nog geen Visual Studio 2013 hebt, Hallo SDK installeert automatisch Visual Studio 2013 Express Web. U kunt dus gaan ontwikkelen voor Azure volledig voor gratis.

Deze zelfstudie wordt ervan uitgegaan dat u hebt geen ervaring met Azure. Op het voltooien van deze zelfstudie hebt u een eenvoudige web-app up en wordt uitgevoerd in de cloud Hallo.

U leert het volgende:

* Hoe tooenable computer klaarmaken voor het ontwikkelen van Azure door het installeren van hello Azure SDK.
* Hoe toocreate een ASP.NET MVC 5 voor Visual Studio-project en publiceer deze tooan Apps van Azure.
* Hoe toouse Hallo ASP.NET Web API tooenable Restful-API aanroept.
* Hoe toouse een SQL-database toostore gegevens in Azure.
* Hoe werkt toopublish toepassing tooAzure.

U moet een eenvoudige lijst met contactpersonen-webtoepassing die is gebouwd op ASP.NET MVC 5 bouwen en maakt gebruik van hello ADO.NET Entity Framework voor toegang tot de database. Hallo volgende afbeelding toont Hallo voltooid toepassing:

![Schermafbeelding van de website][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Hallo-project maken
1. Start Visual Studio 2013.
2. Van Hallo **bestand** muisklik **nieuw Project**.
3. In Hallo **nieuw Project** dialoogvenster Vouw **Visual C#** en selecteer **Web** en selecteer vervolgens **ASP.NET-webtoepassing**. Naam van de toepassing hello **ContactManager** en klik op **OK**.
   
    ![Het dialoogvenster Nieuw project](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. In Hallo **nieuw ASP.NET-Project** dialoogvenster, selecteer Hallo **MVC** sjabloon selectievakje **Web API** en klik vervolgens op **verificatie wijzigen**.
5. In Hallo **verificatie wijzigen** in het dialoogvenster, klikt u op **geen verificatie**, en klik vervolgens op **OK**.
   
    ![Geen verificatie](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    Hallo-voorbeeldtoepassing die u hebt geen functies waarvoor gebruikers toolog in. Voor informatie over het tooimplement verificatie en autorisatie Zie Hallo [Vervolgstappen](#nextsteps) sectie op Hallo einde van deze zelfstudie. 
6. In Hallo **nieuw ASP.NET-Project** dialoogvenster, zorg ervoor dat Hallo **Host in Cloud Hallo** is ingeschakeld en klik op **OK**.

Als u tooAzure eerder niet hebt aangemeld, kunt u zich na vragen aan gebruiker toosign in.

1. Hallo-configuratiewizard worden voorgesteld een unieke naam op basis van *ContactManager* (Zie onderstaande Hallo afbeelding). Selecteer een regio in de buurt. U kunt [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind Hallo laagste latentie Datacenter. 
2. Als u een database-server voordat u dit nog niet hebt gemaakt, selecteert u **nieuwe server maken**, een database-gebruikersnaam en wachtwoord invoeren.
   
    ![Azure-Website configureren](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Als u een database-server hebt, gebruikt u die toocreate een nieuwe database. Database-servers zijn een kostbare resource, en u in het algemeen wilt toocreate meerdere databases op Hallo dezelfde server voor testen en ontwikkeling in plaats van een databaseserver per database maken. Controleer of uw website en database in Hallo dezelfde regio.

![Azure-Website configureren](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Hallo paginakoptekst of -voettekst instellen
1. In **Solution Explorer**, vouw Hallo *Views\Shared* map en open Hallo *_Layout.cshtml* bestand.
   
    ![_Layout.cshtml in Solution Explorer][newapp004]
2. Vervang de inhoud Hallo Hallo *Views\Shared_Layout.cshtml* bestand met de volgende code Hallo:

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

Hallo markup hierboven wijzigingen Hallo app-naam van de 'Mijn ASP.NET-App' te ' Contact Manager ', maar verwijdert Hallo koppelingen te**Start**, **over** en **Contact**.

### <a name="run-hello-application-locally"></a>Hallo-toepassing lokaal uitvoeren
1. Druk op CTRL + F5 toorun Hallo toepassing.
   startpagina Hallo-toepassing wordt weergegeven in de standaardbrowser Hallo.
    ![tooDo lijst-startpagina](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Dit is alles wat dat u nodig toodo voor nu toocreate Hallo toepassing dat u tooAzure implementeert. U voegt later databasefunctionaliteit.

## <a name="deploy-hello-application-tooazure"></a>Hallo toepassing tooAzure implementeren
1. In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer** en selecteer **publiceren** in het contextmenu Hallo.
   
    ![In het contextmenu project publiceren][PublishVSSolution]
   
    Hallo **webpublicatie** wizard wordt geopend.
2. Klik op **Publish**.

![Tabblad instellingen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio begint Hallo proces van het kopiëren van Hallo bestanden toohello Azure-server. Hallo **uitvoer** venster ziet u welke implementatieacties zijn uitgevoerd en rapporteert Hallo-implementatie is voltooid.

1. Hallo standaardbrowser automatisch geopend toohello URL van de site Hallo geïmplementeerd.
   
   Hallo-toepassing die u hebt gemaakt, wordt nu uitgevoerd in de cloud Hallo.
   
   ![tooDo lijst-startpagina worden uitgevoerd in Azure][rxz2]

## <a name="add-a-database-toohello-application"></a>Een database toohello toepassing toevoegen
Vervolgens moet u Hallo MVC-toepassing tooadd Hallo mogelijkheid toodisplay bijwerken en contactpersonen bijwerken en Hallo gegevens opslaan in een database. Hallo-toepassing hello Entity Framework toocreate Hallo database en tooread gebruikt en gegevens in Hallo-database bijwerken.

### <a name="add-data-model-classes-for-hello-contacts"></a>Model gegevensklassen voor Hallo contactpersonen toevoegen
U begint met het maken van een eenvoudige gegevensmodel in code.

1. In **Solution Explorer**, met de rechtermuisknop op de map modellen hello, klik op **toevoegen**, en vervolgens **klasse**.
   
    ![Klasse in het contextmenu modellen toevoegen][adddb001]
2. In Hallo **Add New Item** in het dialoogvenster, naam Hallo nieuwe klassebestand *Contact.cs*, en klik vervolgens op **toevoegen**.
   
    ![Dialoogvenster Nieuw Item toevoegen][adddb002]
3. Hallo inhoud van Hallo Contacts.cs bestand vervangen door Hallo code te volgen.
   
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

Hallo **Neem contact op met** klasse definieert Hallo-gegevens die u voor elke contactpersoon, plus een primaire sleutel, ContactID die nodig is voor het Hallo-database wilt opslaan. U kunt meer informatie over gegevensmodellen krijgen in Hallo [Vervolgstappen](#nextsteps) sectie op Hallo einde van deze zelfstudie.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Webpagina's maken die de app gebruikers toowork met Hallo contactpersonen inschakelen
Hallo ASP.NET MVC Hallo steigers functie kan automatisch code gegenereerd waarmee maken, lezen, bijwerken en verwijderen (CRUD).

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Een domeincontroller en een weergave voor Hallo gegevens toevoegen
1. In **Solution Explorer**, vouw de map Hallo-Controllers.
2. Bouw Hallo project **(Ctrl + Shift + B)**. (U moet Hallo project bouwen voordat steigers mechanisme.) 
3. Met de rechtermuisknop op de map Hallo-Controllers en klik op **toevoegen**, en klik vervolgens op **Controller**.
   
    ![Controller toevoegen in het contextmenu domeincontrollers][addcode001]
4. In Hallo **Add Scaffold** dialoogvenster, **MVC-Controller with views, using Entity Framework** en klik op **toevoegen**.
   
   ![Controller toevoegen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Hallo controllernaam te ingesteld**HomeController**. Selecteer **Contact** als uw modelklasse. Klik op Hallo **nieuwe gegevenscontext** knop en standaardoptie Hallo 'ContactManager.Models.ContactManagerContext' voor Hallo **nieuwe gegevenscontexttype**. Klik op **Add**.

    Een dialoogvenster wordt u gevraagd: 'een bestand met de naam Hallo HomeController al afgesloten. Wilt u toch tooreplace deze? '. Klik op **Ja**. We wilt Hallo Start de domeincontroller die is gemaakt met de Hallo nieuw project overschrijven. We gebruiken Hallo nieuwe start Controller voor onze lijst met contactpersonen.

    Visual Studio maakt de domeincontroller methoden en weergaven voor database-CRUD-bewerkingen voor **Contact** objecten.

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Inschakelen van migraties, het Hallo-database maken, het toevoegen van voorbeeldgegevens en een initialisatiefunctie voor gegevens
de volgende taak Hallo is tooenable hello [Code First-migraties](http://curah.microsoft.com/55220) functie in volgorde toocreate Hallo database op basis van Hallo-gegevensmodel die u hebt gemaakt.

1. In Hallo **extra** selecteert u **Library Package Manager** en vervolgens **Package Manager Console**.
   
    ![Package Manager-Console in het menu Extra][addcode008]
2. In Hallo **Package Manager Console** venster Voer Hallo volgende opdracht:
   
        enable-migrations 
   
    Hallo **inschakelen migraties** opdracht maakt u een *migraties* map en plaatst het in de map een *Configuration.cs* bestand dat u tooconfigure migraties kunt bewerken. 
3. In Hallo **Package Manager Console** venster Voer Hallo volgende opdracht:
   
        add-migration Initial
   
    Hallo **toevoegen migratie initiële** opdracht genereert u een klasse met de naam  **&lt;date_stamp&gt;initiële** die Hallo-database wordt gemaakt. de eerste parameter Hallo ( *initiële* ) is willekeurig en gebruikte toocreate Hallo-naam van Hallo-bestand. U kunt zien Hallo bestanden met betrekking tot een nieuwe klasse in **Solution Explorer**.
   
    In Hallo **initiële** klasse hello **Up** methode maakt u tabel Hallo-contactpersonen en Hallo **omlaag** methode (die wordt gebruikt als u wilt dat de vorige status van tooreturn toohello) komt het.
4. Open Hallo *Migrations\Configuration.cs* bestand. 
5. Hallo na naamruimten toevoegen. 
   
         using ContactManager.Models;
6. Vervang Hallo *Seed* methode Hello code te volgen:
   
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
   
    Deze bovenstaande code wordt Hallo-database met contactgegevens Hallo initialiseren. Zie voor meer informatie over het Hallo database seeding [foutopsporing Entity Framework (EF) databases](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. In Hallo **Package Manager Console** Voer Hallo-opdracht:
   
        update-database
   
    ![Opdrachten Package Manager-Console][addcode009]
   
    Hallo **database bijwerken** wordt uitgevoerd Hallo eerste migratie die Hallo-database wordt gemaakt. Standaard Hallo-database gemaakt als een SQL Server Express LocalDB-database.
8. Druk op CTRL + F5 toorun Hallo toepassing. 

Hallo-toepassing hello seedgegevens worden weergegeven en wordt bewerken, details en verwijderkoppelingen.

![MVC-weergave van gegevens][rxz3]

## <a name="edit-hello-view"></a>Hallo weergave bewerken
1. Open Hallo *Views\Home\Index.cshtml* bestand. In de volgende stap Hallo we Hallo gegenereerd markup wordt vervangen door de code die wordt gebruikt [jQuery](http://jquery.com/) en [Knockout.js](http://knockoutjs.com/). Deze nieuwe code haalt Hallo lijst met contactpersonen uit met behulp van web-API en JSON en vervolgens bindingen Hallo contact op met de gegevens toohello UI knockout.js gebruiken. Zie voor meer informatie, Hallo [Vervolgstappen](#nextsteps) sectie op Hallo einde van deze zelfstudie. 
2. Hallo-inhoud van Hallo-bestand met de volgende code Hallo vervangen.
   
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
3. Met de rechtermuisknop op de map met inhoud Hallo en klik op **toevoegen**, en klik vervolgens op **Nieuw Item...** .
   
    ![Opmaakmodel toevoegen in de map met inhoud contextmenu][addcode005]
4. In Hallo **Add New Item** dialoogvenster Voer **stijl** in de bovenste rechts zoekvak Hallo en selecteer vervolgens **opmaakmodel**.
    ![Dialoogvenster Nieuw Item toevoegen][rxStyle]
5. Bestand met de Hallo *Contacts.css* en klik op **toevoegen**. Hallo-inhoud van Hallo-bestand met de volgende code Hallo vervangen.
   
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
   
    We gebruiken deze opmaakmodel voor Hallo opmaak, kleuren en stijlen in Hallo contact manager-app gebruikt.
6. Open Hallo *App_Start\BundleConfig.cs* bestand.
7. Toevoegen van de volgende code tooregister Hallo Hallo [uitnemen](http://knockoutjs.com/index.html "KO") invoegtoepassing.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Dit voorbeeld met uitnemen toosimplify dynamische JavaScript-code die verantwoordelijk is voor Hallo scherm sjablonen.
8. Hallo inhoud/css vermelding tooregister Hallo wijzigen *contacts.css* opmaakmodel. Hallo volgt regel wijzigen:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Aan:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Voer in Hallo Package Manager-Console, Hallo opdracht tooinstall uitname te volgen.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Een controller voor Web-API Restful Hallo-interface toevoegen
1. In **Solution Explorer**, met de rechtermuisknop op domeincontrollers en klik op **toevoegen** en vervolgens **Controller...** 
2. In Hallo **Add Scaffold** dialoogvenster Voer **Web API 2-Controller met acties, using Entity Framework** en klik vervolgens op **toevoegen**.
   
    ![API-controller toevoegen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. In Hallo **Controller toevoegen** dialoogvenster Voer 'ContactsController' als de naam van uw domeincontroller. Selecteer 'Neem contact op met (ContactManager.Models)' voor Hallo **Modelklasse**.  Hou de standaardwaarde Hallo voor Hallo **Data context class**. 
4. Klik op **Add**.

### <a name="run-hello-application-locally"></a>Hallo-toepassing lokaal uitvoeren
1. Druk op CTRL + F5 toorun Hallo toepassing.
   
    ![De indexpagina][intro001]
2. Voer een contactpersoon in en klikt u op **toevoegen**. Hallo app retourneert toohello startpagina en geeft weer Hallo contactpersoon die u hebt ingevoerd.
   
    ![Indexpagina met lijst taakitems][addwebapi004]
3. In de browser Hallo toevoegen **/api/contacts** toohello URL.
   
    Hallo resulterende URL ziet eruit als http://localhost:1234/api/contacts. Hallo RESTful-web-API die u hebt toegevoegd retourneert Hallo opgeslagen contactpersonen. Firefox en Chrome weergegeven Hallo gegevens in de XML-indeling.
   
    ![Indexpagina met lijst taakitems][rxFFchrome]

    Internet Explorer wordt u tooopen gevraagd of Hallo contactpersonen opslaan.

    ![Web-API dialoogvenster Opslaan][addwebapi006]


    U kunt Hallo contactpersonen geretourneerd in Kladblok of in een browser openen.

    Deze uitvoer kan worden gebruikt door een andere toepassing, zoals mobiele website of toepassing.

    ![Web-API dialoogvenster Opslaan][addwebapi007]

    **Beveiligingswaarschuwing**: op dit punt uw toepassing is onveilig en kwetsbaar tooCSRF aanval. Verderop in de zelfstudie Hallo wordt deze kwetsbaarheid verwijderd. Zie voor meer informatie [aanvallen te voorkomen dat Cross-Site aanvragen kunnen worden vervalst (CSRF)][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>XSRF beveiliging toevoegen
Aanvraagvervalsing op meerdere sites (ook wel bekend als XSRF of CSRF) is een aanval tegen web gehoste toepassingen waarbij een schadelijke website Hallo interactie tussen de browser van de client en een website die wordt vertrouwd door de browser kan beïnvloeden. Deze aanvallen worden mogelijk gemaakt omdat webbrowsers verificatietokens automatisch met elke aanvraag tooa website wordt verzonden. Hallo canonieke voorbeeld is een verificatiecookie zoals ASP. NET van formulierverificatie ticket. Websites die permanente verificatiemechanisme (zoals Windows-verificatie, Basic, enzovoort) te gebruiken kunt echter deze aanvallen zijn gericht.

Een aanval XSRF verschilt van een phishingaanval. Phishingaanvallen vereisen interactie van Hallo slachtoffer. Bij een phishingaanval een schadelijke website nabootsen Hallo doelwebsite en Hallo slachtoffer is misleiden in gevoelige informatie toohello aanvaller bieden. Bij een aanval XSRF is vaak geen tussenkomst van Hallo slachtoffer nodig. In plaats daarvan wordt de aanvaller Hallo vertrouwen op Hallo browser automatisch alle relevante cookies toohello bestemming website wordt verzonden.

Zie voor meer informatie, Hallo [beveiliging Open Webtoepassingsproject](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. In **Solution Explorer**, rechts **ContactManager** project en klik op **toevoegen** en klik vervolgens op **klasse**.
2. Bestand met de Hallo *ValidateHttpAntiForgeryTokenAttribute.cs* en Hallo volgende code toe te voegen:
   
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
3. Voeg de volgende Hallo *met* instructie toohello contracten controller zodat u toegang tot toohello hebt **[ValidateHttpAntiForgeryToken]** kenmerk.
   
        using ContactManager.Filters;
4. Hallo toevoegen **[ValidateHttpAntiForgeryToken]** toohello Post-methoden van Hallo kenmerk **ContactsController** tooprotect uit XSRF bedreigingen. U toohello 'PutContact', 'PostContact' wordt toegevoegd en **DeleteContact** actiemethoden.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Update Hallo *Scripts* sectie Hallo *Views\Home\Index.cshtml* tooinclude code tooget hello XSRF tokens bestand.
   
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

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Hallo toepassing update tooAzure en SQL-Database publiceren
-toepassing hello toopublish u herhalen Hallo procedure die u eerder hebt gevolgd.

1. In **Solution Explorer**, klik met de rechtermuisknop op Hallo-project en selecteer **publiceren**.
   
    ![Publiceren][rxP]
2. Klik op Hallo **instellingen** tabblad.
3. Onder **ContactsManagerContext(ContactsManagerContext)**, klikt u op Hallo **v** pictogram toochange *externe verbindingsreeks* toohello verbindingsreeks voor Hallo contact op met de database. Klik op **ContactDB**.
   
    ![Instellingen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Hallo selectievakje voor **uitvoeren Code First-migraties (wordt uitgevoerd op de start van toepassing)**.
5. Klik op **volgende** en klik vervolgens op **Preview**. Visual Studio geeft een lijst van Hallo-bestanden die worden toegevoegd of bijgewerkt.
6. Klik op **Publish**.
   Nadat het Hallo-implementatie is voltooid, wordt in het Hallo browser toohello startpagina van de toepassing hello geopend.
   
    ![Indexpagina met geen contactpersonen][intro001]
   
    Hallo Visual Studio automatisch geconfigureerd proces Hallo verbindingsreeks publiceren in Hallo geïmplementeerd *Web.config* bestand toopoint toohello SQL-database. Deze Code First-migraties tooautomatically upgrade Hallo database toohello meest recente versie Hallo eerste tijd Hallo toepassing toegang heeft tot Hallo database na de implementatie ook geconfigureerd.
   
    Als gevolg van deze configuratie Code First Hallo database gemaakt Hallo code wordt uitgevoerd in Hallo **initiële** klasse die u eerder hebt gemaakt. Die gold deze Hallo eerste tijd Hallo geprobeerd tooaccess Hallo toepassingsdatabase na de implementatie.
7. Voer een contactpersoon zoals u deed toen u uitvoerde Hallo app lokaal tooverify die database-implementatie is voltooid.

Als u ziet dat u invoert Hallo-item wordt opgeslagen en wordt weergegeven op de pagina van de contactpersoon manager hello, weet u dat deze is opgeslagen in Hallo-database.

![Pagina van de index met contactpersonen][addwebapi004]

Hallo toepassing wordt nu uitgevoerd in de cloud Hallo toostore SQL-Database met de gegevens. Nadat u Hallo toepassing testen in Azure, verwijderen. Hallo toepassing openbaar en heeft geen een mechanisme toolimit toegang.

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Een andere manier toostore-gegevens in een Azure-toepassing is toouse Azure-opslag, die niet-relationele gegevensopslag in Hallo vorm van blobs en tabellen bevatten. Hallo volgende koppelingen bieden meer informatie op Web-API, ASP.NET MVC en Azure-venster.

* [Aan de slag met Entity Framework met MVC][EFCodeFirstMVCTutorial]
* [Inleiding tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Uw eerste ASP.NET-Web-API](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Foutopsporing WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Deze zelfstudie en Hallo voorbeeldtoepassing is geschreven door [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) met ondersteuning van Tom Dykstra en Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Geef feedback op wat u beviel of wat u graag verbeterd, niet alleen over Hallo-zelfstudie zelf, maar ook over Hallo producten die laat toosee. Uw feedback helpt ons prioriteren verbeteringen. We zijn met name geïnteresseerd te komen hoeveel interesse er bevindt zich in meer automatisering voor Hallo proces van het configureren en implementeren van Hallo-lidmaatschapsdatabase. 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

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

