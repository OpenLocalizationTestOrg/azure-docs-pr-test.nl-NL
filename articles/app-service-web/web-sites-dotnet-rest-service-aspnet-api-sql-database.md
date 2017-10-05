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
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Een REST-service met ASP.NET Web API- en SQL-Database in Azure App Service maken
Deze zelfstudie laat zien hoe u een ASP.NET-web-app te implementeren een [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) met behulp van de wizard webpublicatie in Visual Studio 2013 of Visual Studio 2013 Community Edition. 

U kunt gratis een Azure-account openen en als u nog geen Visual Studio 2013 hebt, de SDK installeert automatisch Visual Studio 2013 Express Web. U kunt dus gaan ontwikkelen voor Azure volledig voor gratis.

Deze zelfstudie wordt ervan uitgegaan dat u hebt geen ervaring met Azure. Op het voltooien van deze zelfstudie hebt u een eenvoudige web-app up en wordt uitgevoerd in de cloud.

U leert het volgende:

* De computer klaarmaken voor het ontwikkelen van Azure door de Azure SDK te installeren.
* Het maken van een Visual Studio ASP.NET MVC 5-project en deze publiceren naar een Azure-app.
* Het gebruik van de ASP.NET-Web-API om in te schakelen van Restful-API-aanroepen.
* Het gebruik van een SQL-database voor het opslaan van gegevens in Azure.
* Hoe om toepassingsupdates te publiceren naar Azure.

U moet een eenvoudige lijst met contactpersonen van een webtoepassing die is gebaseerd op ASP.NET MVC 5 en ADO.NET Entity Framework wordt gebruikt voor toegang tot de database maken. In de volgende afbeelding wordt de voltooide toepassing weergegeven:

![Schermafbeelding van de website][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a>Het project maken
1. Start Visual Studio 2013.
2. Van de **bestand** muisklik **nieuw Project**.
3. In de **nieuw Project** dialoogvenster Vouw **Visual C#** en selecteer **Web** en selecteer vervolgens **ASP.NET-webtoepassing**. Naam van de toepassing **ContactManager** en klik op **OK**.
   
    ![Het dialoogvenster Nieuw project](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. In de **nieuw ASP.NET-Project** selecteert u de **MVC** sjabloon selectievakje **Web API** en klik vervolgens op **verificatie wijzigen**.
5. Klik in het dialoogvenster **Verificatie wijzigen** op **Geen verificatie** en vervolgens op **OK**.
   
    ![Geen verificatie](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    De voorbeeldtoepassing die u hebt geen functies waarvoor gebruikers zich aanmelden. Zie voor meer informatie over het implementeren van de functies voor verificatie en autorisatie, de [Vervolgstappen](#nextsteps) sectie aan het einde van deze zelfstudie. 
6. In de **nieuw ASP.NET-Project** dialoogvenster vak, controleert u of de **Host in de Cloud** is ingeschakeld en klik op **OK**.

Als u hebt eerder niet aangemeld bij Azure, wordt u gevraagd aan te melden.

1. Een unieke naam op basis van wordt voorgesteld door de configuratiewizard *ContactManager* (Zie de onderstaande afbeelding). Selecteer een regio in de buurt. U kunt [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") de laagste latentie datacentrum vinden. 
2. Als u een database-server voordat u dit nog niet hebt gemaakt, selecteert u **nieuwe server maken**, een database-gebruikersnaam en wachtwoord invoeren.
   
    ![Azure-Website configureren](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Als u een database-server hebt, gebruikt u dat een nieuwe database te maken. Database-servers zijn een kostbare resource en u in het algemeen wilt maken van meerdere databases op dezelfde server voor testen en ontwikkeling in plaats van een databaseserver per database maken. Zorg ervoor dat uw website en de database zich in dezelfde regio.

![Azure-Website configureren](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a>Stel de paginakoptekst of -voettekst
1. In **Solution Explorer**, vouw de *Views\Shared* map en open de *_Layout.cshtml* bestand.
   
    ![_Layout.cshtml in Solution Explorer][newapp004]
2. Vervang de inhoud van de *Views\Shared_Layout.cshtml* bestand met de volgende code:

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

De bovenstaande opmaak verandert de naam van de app uit de 'Mijn ASP.NET-App' naar 'Contact Manager' en verwijdert deze de koppelingen naar **Start**, **over** en **Contact**.

### <a name="run-the-application-locally"></a>De toepassing lokaal uitvoeren
1. Druk op CTRL + F5 om de toepassing uit te voeren.
   De startpagina van de toepassing wordt weergegeven in de standaardbrowser.
    ![Naar de startpagina van de takenlijst](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Dit is alles wat u moet doen nu de toepassing die u naar Azure implementeert te maken. U voegt later databasefunctionaliteit.

## <a name="deploy-the-application-to-azure"></a>De toepassing implementeren in Azure
1. In Visual Studio met de rechtermuisknop op het project in **Solution Explorer** en selecteer **publiceren** in het contextmenu.
   
    ![In het contextmenu project publiceren][PublishVSSolution]
   
    De **webpublicatie** wizard wordt geopend.
2. Klik op **Publish**.

![Tabblad instellingen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio begint het proces van de bestanden zijn gekopieerd naar de Azure-server. De **uitvoer** venster ziet u welke implementatieacties zijn uitgevoerd en rapporten van de implementatie is voltooid.

1. De standaardbrowser automatisch geopend op de URL van de geïmplementeerde site.
   
   De toepassing die u hebt gemaakt, wordt nu uitgevoerd in de cloud.
   
   ![Naar startpagina takenlijst worden uitgevoerd in Azure][rxz2]

## <a name="add-a-database-to-the-application"></a>Een database toevoegen aan de toepassing
Vervolgens moet u de MVC-toepassing te kunnen weergeven en bijwerken van contactpersonen en opslaan van de gegevens in een database bijwerken. De toepassing gebruikt de Entity Framework voor het maken van de database en voor het lezen en bijwerken van gegevens in de database.

### <a name="add-data-model-classes-for-the-contacts"></a>Model gegevensklassen voor contactpersonen toevoegen
U begint met het maken van een eenvoudige gegevensmodel in code.

1. In **Solution Explorer**, met de rechtermuisknop op de map modellen, klik op **toevoegen**, en vervolgens **klasse**.
   
    ![Klasse in het contextmenu modellen toevoegen][adddb001]
2. In de **Add New Item** in het dialoogvenster de naam van het nieuwe klassebestand *Contact.cs*, en klik vervolgens op **toevoegen**.
   
    ![Dialoogvenster Nieuw Item toevoegen][adddb002]
3. De inhoud van het bestand Contacts.cs vervangen door de volgende code.
   
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

De **Neem contact op met** klasse definieert de gegevens die u voor elke contactpersoon, plus een primaire sleutel, ContactID die nodig is voor de database wilt opslaan. U kunt meer informatie over gegevensmodellen in krijgen de [Vervolgstappen](#nextsteps) sectie aan het einde van deze zelfstudie.

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a>Webpagina's maken die app-gebruikers werken met de contactpersonen inschakelen
De ASP.NET MVC code die wordt uitgevoerd kan automatisch genereren in de functie steigers maken, lezen, bijwerken en verwijderen (CRUD).

## <a name="add-a-controller-and-a-view-for-the-data"></a>Een domeincontroller en een weergave voor de gegevens toevoegen
1. In **Solution Explorer**, vouw de map domeincontrollers.
2. Bouw het project **(Ctrl + Shift + B)**. (U moet het project bouwen voordat steigers mechanisme.) 
3. Met de rechtermuisknop op de map Controllers en klik op **toevoegen**, en klik vervolgens op **Controller**.
   
    ![Controller toevoegen in het contextmenu domeincontrollers][addcode001]
4. In de **Add Scaffold** dialoogvenster, **MVC-Controller with views, using Entity Framework** en klik op **toevoegen**.
   
   ![Controller toevoegen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Naam van de domeincontroller ingesteld op **HomeController**. Selecteer **Contact** als uw modelklasse. Klik op de **nieuwe gegevenscontext** knop en accepteer de standaardinstelling 'ContactManager.Models.ContactManagerContext' voor de **nieuwe gegevenscontexttype**. Klik op **Add**.

    Een dialoogvenster wordt u gevraagd: 'een bestand met de naam HomeController al afgesloten. Wilt u deze vervangen? '. Klik op **Ja**. We wilt de start-domeincontroller die is gemaakt met het nieuwe project overschrijven. We gebruiken de nieuwe domeincontroller start voor onze lijst met contactpersonen.

    Visual Studio maakt de domeincontroller methoden en weergaven voor database-CRUD-bewerkingen voor **Contact** objecten.

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a>Inschakelen van migraties, maak de database, voorbeeldgegevens en een initialisatiefunctie gegevens toevoegen
De volgende taak is om in te schakelen de [Code First-migraties](http://curah.microsoft.com/55220) functie om de database maken op basis van het gegevensmodel dat u hebt gemaakt.

1. In de **extra** selecteert u **Library Package Manager** en vervolgens **Package Manager Console**.
   
    ![Package Manager-Console in het menu Extra][addcode008]
2. In de **Package Manager Console** venster, voer de volgende opdracht:
   
        enable-migrations 
   
    De **inschakelen migraties** opdracht maakt u een *migraties* map en plaatst het in de map een *Configuration.cs* -bestand dat u voor het configureren van migraties kunt bewerken. 
3. In de **Package Manager Console** venster, voer de volgende opdracht:
   
        add-migration Initial
   
    De **toevoegen migratie initiële** opdracht genereert u een klasse met de naam  **&lt;date_stamp&gt;initiële** die de database wordt gemaakt. De eerste parameter ( *initiële* ) is een willekeurige en die wordt gebruikt om de naam van het bestand te maken. Ziet u de nieuwe klassebestanden op **Solution Explorer**.
   
    In de **initiële** klasse, de **Up** methode maakt u de tabel Contactpersonen en de **omlaag** methode (die wordt gebruikt wanneer u wilt terugkeren naar de vorige status) komt het.
4. Open de *Migrations\Configuration.cs* bestand. 
5. Voeg de volgende naamruimten. 
   
         using ContactManager.Models;
6. Vervang de *Seed* methode met de volgende code:
   
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
   
    Deze bovenstaande code wordt de database met de contactgegevens worden geïnitialiseerd. Zie voor meer informatie over het seeding van de database [foutopsporing Entity Framework (EF) databases](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. In de **Package Manager Console** Voer de opdracht:
   
        update-database
   
    ![Opdrachten Package Manager-Console][addcode009]
   
    De **database bijwerken** wordt uitgevoerd van de eerste migratie die de database wordt gemaakt. Standaard wordt de database gemaakt als een SQL Server Express LocalDB-database.
8. Druk op CTRL + F5 om de toepassing uit te voeren. 

De toepassing geeft de seedgegevens en koppelingen bewerken, details en verwijderen.

![MVC-weergave van gegevens][rxz3]

## <a name="edit-the-view"></a>De weergave bewerken
1. Open de *Views\Home\Index.cshtml* bestand. In de volgende stap we de gegenereerde opmaak wordt vervangen door de code die gebruikmaakt van [jQuery](http://jquery.com/) en [Knockout.js](http://knockoutjs.com/). Deze nieuwe code haalt de lijst met contactpersonen van het gebruik van web-API en JSON en vervolgens contact op met gegevens gebonden aan de gebruikersinterface met behulp van knockout.js. Zie voor meer informatie de [Vervolgstappen](#nextsteps) sectie aan het einde van deze zelfstudie. 
2. Vervang de inhoud van het bestand met de volgende code.
   
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
3. Met de rechtermuisknop op de map met inhoud en klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item...** .
   
    ![Opmaakmodel toevoegen in de map met inhoud contextmenu][addcode005]
4. In de **Add New Item** dialoogvenster Voer **stijl** in de linkerbovenhoek rechts het zoekvak en selecteer vervolgens **opmaakmodel**.
    ![Dialoogvenster Nieuw Item toevoegen][rxStyle]
5. Noem het bestand *Contacts.css* en klik op **toevoegen**. Vervang de inhoud van het bestand met de volgende code.
   
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
   
    We gebruiken deze opmaakmodel voor de indeling, kleuren en stijlen die in de app contactpersonen manager worden gebruikt.
6. Open de *App_Start\BundleConfig.cs* bestand.
7. Voeg de volgende code om te registreren de [uitnemen](http://knockoutjs.com/index.html "KO") invoegtoepassing.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Dit voorbeeld uitnemen met dynamische JavaScript-code die verantwoordelijk is voor de sjablonen scherm vereenvoudigen.
8. Wijzig de vermelding inhoud/css registreren de *contacts.css* opmaakmodel. Wijzig de volgende regel:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Aan:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Voer de volgende opdracht voor het installeren van uitnemen in de Package Manager-Console.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a>Een controller voor de Web-API Restful-interface toevoegen
1. In **Solution Explorer**, met de rechtermuisknop op domeincontrollers en klik op **toevoegen** en vervolgens **Controller...** 
2. In de **Add Scaffold** dialoogvenster Voer **Web API 2-Controller met acties, using Entity Framework** en klik vervolgens op **toevoegen**.
   
    ![API-controller toevoegen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. In de **Controller toevoegen** dialoogvenster Voer 'ContactsController' als de naam van uw domeincontroller. Selecteer 'Neem contact op met (ContactManager.Models)' voor de **Modelklasse**.  Hou de standaardwaarde voor de **Data context class**. 
4. Klik op **Add**.

### <a name="run-the-application-locally"></a>De toepassing lokaal uitvoeren
1. Druk op CTRL + F5 om de toepassing uit te voeren.
   
    ![De indexpagina][intro001]
2. Voer een contactpersoon in en klikt u op **toevoegen**. De app wordt naar de startpagina en wordt de contactpersoon die u hebt ingevoerd.
   
    ![Indexpagina met lijst taakitems][addwebapi004]
3. In de browser toevoegen **/api/contacts** naar de URL.
   
    De resulterende URL ziet eruit als http://localhost:1234/api/contacts. De RESTful-web-API die u toegevoegd retourneert opgeslagen contactpersonen. Firefox en Chrome worden de gegevens in XML-indeling weergegeven.
   
    ![Indexpagina met lijst taakitems][rxFFchrome]

    IE wordt u gevraagd om te openen of opslaan van de contactpersonen.

    ![Web-API dialoogvenster Opslaan][addwebapi006]


    U kunt de geretourneerde contactpersonen openen in Kladblok of in een browser.

    Deze uitvoer kan worden gebruikt door een andere toepassing, zoals mobiele website of toepassing.

    ![Web-API dialoogvenster Opslaan][addwebapi007]

    **Beveiligingswaarschuwing**: op dit punt uw toepassing is onveilig en kwetsbaar voor aanvallen CSRF. Verderop in de zelfstudie wordt deze kwetsbaarheid mogelijk verwijderd. Zie voor meer informatie [aanvallen te voorkomen dat Cross-Site aanvragen kunnen worden vervalst (CSRF)][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>XSRF beveiliging toevoegen
Aanvraagvervalsing op meerdere sites (ook wel bekend als XSRF of CSRF) is een aanval tegen web gehoste toepassingen waarbij een schadelijke website invloed hebben op de interactie tussen de browser van de client en een website die wordt vertrouwd door de browser. Deze aanvallen worden mogelijk gemaakt omdat webbrowsers verificatietokens automatisch met elke aanvraag naar een website wordt verzonden. Het canonieke voorbeeld is een verificatiecookie zoals ASP. NET van formulierverificatie ticket. Websites die permanente verificatiemechanisme (zoals Windows-verificatie, Basic, enzovoort) te gebruiken kunt echter deze aanvallen zijn gericht.

Een aanval XSRF verschilt van een phishingaanval. Phishingaanvallen vereist interactie van het slachtoffer. Bij een phishingaanval een schadelijke website nabootsen de doelwebsite en het slachtoffer is misleiden in gevoelige informatie opgeeft voor de aanvaller. Bij een aanval XSRF is vaak geen tussenkomst van het slachtoffer nodig. In plaats daarvan wordt de aanvaller vertrouwen op de browser alle relevante cookies automatisch wordt verzonden naar de website van de bestemming.

Zie voor meer informatie de [beveiliging Open Webtoepassingsproject](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. In **Solution Explorer**, rechts **ContactManager** project en klik op **toevoegen** en klik vervolgens op **klasse**.
2. Noem het bestand *ValidateHttpAntiForgeryTokenAttribute.cs* en voeg de volgende code:
   
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
3. Voeg de volgende *met* instructie naar de controller contracten zodat u toegang tot hebt de **[ValidateHttpAntiForgeryToken]** kenmerk.
   
        using ContactManager.Filters;
4. Voeg de **[ValidateHttpAntiForgeryToken]** kenmerk aan de Post-methoden van de **ContactsController** te beveiligen tegen bedreigingen XSRF. U gaat deze toevoegen aan de 'PutContact', 'PostContact' en **DeleteContact** actiemethoden.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Update de *Scripts* sectie van de *Views\Home\Index.cshtml* dat moet worden opgenomen code om de XSRF-tokens.
   
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

## <a name="publish-the-application-update-to-azure-and-sql-database"></a>Het bijwerken van de toepassing publiceren naar Azure en SQL-Database
Voor het publiceren van de toepassing, moet u de procedure die u eerder hebt gevolgd herhalen.

1. In **Solution Explorer**, klik met de rechtermuisknop op het project en selecteer **publiceren**.
   
    ![Publiceren][rxP]
2. Klik op het tabblad **Settings**.
3. Onder **ContactsManagerContext(ContactsManagerContext)**, klikt u op de **v** pictogram wijzigen *externe verbindingsreeks* de verbindingsreeks voor de database van contactpersonen. Klik op **ContactDB**.
   
    ![Instellingen](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Schakel het selectievakje voor **uitvoeren Code First-migraties (wordt uitgevoerd op de start van toepassing)**.
5. Klik op **volgende** en klik vervolgens op **Preview**. Visual Studio geeft een lijst van de bestanden die worden toegevoegd of bijgewerkt.
6. Klik op **Publish**.
   Nadat de implementatie is voltooid, wordt de browser geopend met de startpagina van de toepassing.
   
    ![Indexpagina met geen contactpersonen][intro001]
   
    De Visual Studio publicatieproces automatisch geconfigureerd van de verbindingsreeks in het geïmplementeerde *Web.config* bestand om te verwijzen naar de SQL-database. Deze Code First-migraties om automatisch de database bijwerken naar de nieuwste versie de eerste keer dat de toepassing toegang heeft tot de database na de implementatie ook geconfigureerd.
   
    Als gevolg van deze configuratie Code First de database is gemaakt door de code in de **initiële** klasse die u eerder hebt gemaakt. Het is dit de eerste keer dat de toepassing heeft geprobeerd toegang tot de database na de implementatie.
7. Voer een contactpersoon als toen u de app lokaal hebt uitgevoerd om te controleren of de implementatie van de database is voltooid.

Als u ziet dat het item dat u invoert, wordt opgeslagen en wordt weergegeven op de pagina contact op met manager, weet u dat deze is opgeslagen in de database.

![Pagina van de index met contactpersonen][addwebapi004]

De toepassing wordt nu uitgevoerd in de cloud, met behulp van SQL-Database voor het opslaan van gegevens. Nadat u de toepassing testen in Azure, verwijderen. De toepassing openbaar en beschikt niet over een mechanisme om toegang te beperken.

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Gegevens opslaan in een Azure-toepassing op een andere manier is het gebruik van Azure-opslag, die niet-relationele gegevensopslag in de vorm van blobs en tabellen bieden. De volgende koppelingen bieden meer informatie op Web-API, ASP.NET MVC en Azure-venster.

* [Aan de slag met Entity Framework met MVC][EFCodeFirstMVCTutorial]
* [Inleiding tot de ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Uw eerste ASP.NET-Web-API](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Foutopsporing WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Deze zelfstudie en de voorbeeldtoepassing is geschreven door [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) met ondersteuning van Tom Dykstra en Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Neem verbeterd laat feedback over wat u beviel of wat u graag, niet alleen over de zelfstudie zelf, maar ook over de producten die deze laat zien. Uw feedback helpt ons prioriteren verbeteringen. We zijn met name geïnteresseerd te komen hoeveel interesse in meer automation voor het proces van het configureren en implementeren van de lidmaatschapsdatabase. 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

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

