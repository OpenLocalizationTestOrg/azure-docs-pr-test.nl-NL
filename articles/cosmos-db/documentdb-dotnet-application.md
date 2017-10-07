---
title: 'ASP.NET MVC-zelfstudie voor Azure Cosmos DB: webtoepassingsontwikkeling | Microsoft Docs'
description: ASP.NET MVC zelfstudie toocreate een MVC-webtoepassing met Azure Cosmos DB. JSON opslaan en gegevens benaderen via een takenlijst-app die wordt gehost op Azure Websites - Stapsgewijze zelfstudie voor ASP NET MVC.
keywords: asp.net mvc-zelfstudie, ontwikkelen van webtoepassingen, mvc-webtoepassing, asp net mvc zelfstudie stapsgewijs
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>ASP.NET MVC-zelfstudie: webtoepassingsontwikkeling met Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight hoe efficiënt kunt u gebruikmaken van Azure DB die Cosmos toostore en JSON-documenten opvragen, in dit artikel biedt een end-to-end-procedure die laat zien u hoe een app met behulp van Azure DB die Cosmos toobuild. Hallo-taken worden opgeslagen als JSON-documenten in Azure Cosmos DB.

![Schermopname van het Hallo-takenlijst MVC-webtoepassing die is gemaakt met deze zelfstudie - stapsgewijze voor ASP NET MVC-zelfstudie](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

Deze procedure ziet u hoe toouse hello Azure Cosmos DB service toostore en toegang tot gegevens uit een ASP.NET MVC-webtoepassing gehost op Azure. Als u zoekt naar een zelfstudie is alleen op Azure Cosmos DB gericht en niet hello ASP.NET MVC-onderdelen, Zie [een Azure Cosmos DB C#-consoletoepassing bouwen](documentdb-get-started.md).

> [!TIP]
> Voor deze zelfstudie wordt ervan uitgegaan dat u ervaring hebt met ASP.NET MVC en Azure Websites. Als u nieuwe tooASP.NET of Hallo [vereiste hulpprogramma's](#_Toc395637760), het is raadzaam Hallo volledige voorbeeldproject via downloaden [GitHub] [ GitHub] en het Hallo-instructies in dit voorbeeld. Zodra u klaar hebt, kunt u dit artikel toogain inzicht op Hallo code in de context van project Hallo Hallo bekijken.
> 
> 

## <a name="_Toc395637760"></a>Vereisten voor deze databasezelfstudie
Voordat u Hallo-instructies in dit artikel uitvoert, moet u ervoor zorgen dat u de volgende Hallo hebt:

* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 

    OF

    Een lokale installatie van Hallo [Azure Cosmos DB Emulator](local-emulator.md).
* [Visual Studio 2017](http://www.visualstudio.com/).  
* Microsoft Azure SDK voor .NET voor Visual Studio 2017 beschikbaar via Hallo Visual Studio Installer.

Alle Hallo schermopnamen in dit artikel zijn gemaakt met behulp van Microsoft Visual Studio Community 2017. Als uw systeem is geconfigureerd met een andere versie is het mogelijk dat de schermen en opties niet volledig overeenkomen, maar als u voldoet aan Hallo bovenstaande vereisten moet deze oplossing werken.

## <a name="_Toc395637761"></a>Stap 1: een Azure Cosmos DB-databaseaccount maken
Begin met het maken van een Azure Cosmos DB-account. Als u al een account voor SQL (DocumentDB) voor Azure Cosmos DB hebben of als u Azure Cosmos DB Emulator Hallo voor deze zelfstudie, kunt u overslaan te[Maak een nieuwe ASP.NET MVC-toepassing](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Nu u kunt zien via hoe toocreate een nieuwe ASP.NET MVC-toepassing van Hallo a t/m. 

## <a name="_Toc395637762"></a>Stap 2: Een nieuwe ASP.NET MVC-toepassing maken

1. In Visual Studio op Hallo **bestand** menu te verwijzen**nieuw**, en klik vervolgens op **Project**. Hallo **nieuw Project** dialoogvenster wordt weergegeven.

2. In Hallo **projecttypen** deelvenster Vouw **sjablonen**, **Visual C#**, **Web**, en selecteer vervolgens **ASP.NET-webtoepassing** .

      ![Schermopname van het dialoogvenster Nieuw Project Hallo met Hallo projecttype voor ASP.NET-webtoepassing gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. In Hallo **naam** vak, Hallo-typenaam van Hallo-project. Hallo-naam 'todo' maakt gebruik van deze zelfstudie. Als u toouse iets anders dan dit kiest, waar deze zelfstudie wordt gesproken over Hallo todo-naamruimte, moet u tooadjust Hallo opgegeven code voorbeelden toouse met de naam die uw toepassing. 
4. Klik op **Bladeren** toonavigate toohello map waar u wilt toocreate Hallo-project en klik vervolgens op **OK**.
   
      Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster wordt weergegeven.
   
    ![Schermopname van dialoogvenster Hallo-nieuwe ASP.NET-webtoepassing met Hallo MVC-toepassingssjabloon gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. Selecteer in het deelvenster met sjablonen Hallo **MVC**.

6. Klik op **OK** en bijbehorende dingen rond steigers Hallo lege ASP.NET MVC-sjabloon doen in Visual Studio. 

          
7. Nadat Visual Studio Hallo standaardtekst MVC-toepassing heeft gemaakt hebt u een lege ASP.NET-toepassing die u lokaal kunt uitvoeren.
   
    We zullen uitgevoerd Hallo-project lokaal omdat ik ervoor dat we alle waargenomen Hallo ASP.NET 'Hallo wereld' hebt toepassing. We gaan rechte tooadding Azure Cosmos DB toothis project en onze toepassing bouwen.

## <a name="_Toc395637767"></a>Stap 3: Azure Cosmos DB tooyour MVC-webproject toepassing toevoegen
Nu dat we de meeste Hallo ASP.NET MVC Loodgieterswerk die we nodig hebben voor deze oplossing hebben, krijgen we toohello Werkelijke doel van deze zelfstudie, Azure Cosmos DB tooour MVC-webtoepassing toevoegen.

1. Hello Azure Cosmos DB .NET SDK wordt verpakt en gedistribueerd als een NuGet-pakket. tooget Hallo NuGet-pakket in Visual Studio, Hallo NuGet-Pakketbeheer in Visual Studio gebruiken door met de rechtermuisknop op het Hallo-project in **Solution Explorer** en vervolgens te klikken op **NuGet-pakketten beheren**.
   
    ![Schermopname van het Hallo met de rechtermuisknop op de opties voor het Hallo-webtoepassingsproject in Solution Explorer, met NuGet-pakketten beheren gemarkeerd.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    Hallo **NuGet-pakketten beheren** dialoogvenster wordt weergegeven.
2. In Hallo NuGet **Bladeren** in het vak ***Azure DocumentDB***. (Hallo pakketnaam is geen bijgewerkte tooAzure Cosmos DB.)
   
    Installeren in Hallo resultaten Hallo **Microsoft.Azure.DocumentDB door Microsoft** pakket. Dit zal downloaden en installeren hello Azure Cosmos DB pakket, evenals alle afhankelijkheden, zoals Newtonsoft.Json. Klik op **OK** in Hallo **Preview** venster en **ik ga akkoord** in Hallo **licentie acceptatie** venster toocomplete Hallo installeren.
   
    ![Schermopname van het venster NuGet-pakketten beheren hello, hello Microsoft Azure DocumentDB-clientbibliotheek gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      U kunt ook Hallo Package Manager Console tooinstall Hallo pakket gebruiken. toodo in dat geval op Hallo **extra** menu, klikt u op **NuGet Package Manager**, en klik vervolgens op **Package Manager Console**. Hallo opdrachtprompt, typt u Hallo volgende.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Nadat Hallo-pakket is geïnstalleerd, ziet uw Visual Studio-oplossing Hallo volgende met twee nieuwe verwijzingen Microsoft.Azure.Documents.Client en Newtonsoft.Json.
   
    ![Schermopname van de twee verwijzingen Hallo toegevoegd toohello JSON-gegevensproject in Solution Explorer](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>Stap 4: Hallo ASP.NET MVC-toepassing instellen
Nu gaan we Hallo modellen, weergaven en controllers toothis MVC-toepassing toevoegen:

* [Een model toevoegen](#_Toc395637764).
* [Een controller toevoegen](#_Toc395637765).
* [Weergaven toevoegen](#_Toc395637766).

### <a name="_Toc395637764"></a>Een JSON-gegevensmodel toevoegen
Laten we beginnen met het maken van Hallo **M** in MVC, Hallo model. 

1. In **Solution Explorer**, klik met de rechtermuisknop Hallo **modellen** map, klikt u op **toevoegen**, en klik vervolgens op **klasse**.
   
      Hallo **Add New Item** dialoogvenster wordt weergegeven.
2. Geef een naam op voor uw nieuwe klasse **Item.cs** en klik op **Toevoegen**. 
3. In het nieuwe **Item.cs** bestand, Hallo volgende na Hallo laatste toevoegen *met de instructie*.
   
        using Newtonsoft.Json;
4. Vervang deze code nu 
   
        public class Item
        {
        }
   
    Hello code te volgen.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Alle gegevens in Azure DB die Cosmos is doorgegeven via de kabel Hallo en opgeslagen als JSON. toocontrol hello manier uw objecten worden geserialiseerd/gedeserialiseerd door JSON.NET kunt u Hallo **JsonProperty** kenmerk, zoals wordt beschreven in Hallo **Item** klasse die we zojuist hebben gemaakt. U geen **hebben** toodo dit maar wilt tooensure dat mijn eigenschappen naamgevingsregels van Hallo JSON camelCase volgen. 
   
    Niet alleen kunt u bepalen Hallo-indeling van de naam van de eigenschap Hallo wanneer deze worden opgeslagen in de JSON, maar u uw .NET-eigenschappen volledig wijzigen kunt zoals ik deed met Hallo **beschrijving** eigenschap. 

### <a name="_Toc395637765"></a>Een controller toevoegen
Dat zorgt voor Hallo **M**, nu gaan we maken Hallo **C** in MVC, een controllerklasse.

1. In **Solution Explorer**, klik met de rechtermuisknop Hallo **domeincontrollers** map, klikt u op **toevoegen**, en klik vervolgens op **Controller**.
   
    Hallo **Add Scaffold** dialoogvenster wordt weergegeven.
2. Selecteer **MVC 5 Controller - Empty** (MVC 5-controller - Leeg) en klik vervolgens op **Toevoegen**.
   
    ![Schermopname van dialoogvenster Hallo Add Scaffold met Hallo MVC 5 Controller - leeg optie gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Noem uw nieuwe controller **ItemController**.
   
    ![Schermopname van dialoogvenster Hallo-Controller toevoegen](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Zodra het Hallo-bestand is gemaakt, uw Visual Studio-oplossing moet eruitzien als Hallo volgende met Hallo nieuwe bestand ItemController.cs in **Solution Explorer**. Hallo nieuwe bestand Item.cs file eerder hebt gemaakt, wordt ook weergegeven.
   
    ![Schermopname van Hallo Visual Studio-oplossing - Solution Explorer met het nieuwe bestand ItemController.cs hello en gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    U kunt ItemController.cs sluiten, we je tooit later terugkomen. 

### <a name="_Toc395637766"></a>Weergaven toevoegen
Nu gaan we maken Hallo **V** in MVC, Hallo weergaven:

* [Een weergave toevoegen voor een itemindex ](#AddItemIndexView).
* [Een weergave toevoegen voor nieuwe items](#AddNewIndexView).
* [Een weergave toevoegen voor het bewerken van items](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Een weergave toevoegen voor een itemindex
1. In **Solution Explorer**, vouw Hallo **weergaven** map, klik met de rechtermuisknop Hallo leeg **Item** map die Visual Studio voor u gemaakt bij het toevoegen van Hallo  **ItemController** Klik **toevoegen**, en klik vervolgens op **weergave**.
   
    ![Schermopname van Solution Explorer toont Hallo Item map die Visual Studio hebt gemaakt met Hallo weergave toevoegen opdrachten gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. In Hallo **weergave toevoegen** dialoogvenster vak, Hallo te volgen:
   
   * In Hallo **weergavenaam** in het vak ***Index***.
   * In Hallo **sjabloon** de optie ***lijst***.
   * In Hallo **Modelklasse** de optie ***Item (todo. Modellen)***.
   * Hallo indeling pagina Typ in ***~/Views/Shared/_Layout.cshtml***.
     
   ![Schermopname van Hallo weergave toevoegen voor dialoogvenster scherm](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. Zodra al deze waarden zijn ingesteld, klikt u op **Toevoegen** en wordt er een nieuwe sjabloonweergave in Visual Studio gemaakt. Als deze is voltooid, wordt deze geopend Hallo cshtml-bestand dat is gemaakt. We kunnen dat bestand in Visual Studio kunt sluiten als we zullen tooit later terugkomen.

#### <a name="AddNewIndexView"></a>Een weergave toevoegen voor nieuwe items
Vergelijkbare toohow gemaakt een **itemindex** weergave we gaan nu een nieuwe weergave voor het maken van nieuwe maken **Items**.

1. In **Solution Explorer**, klik met de rechtermuisknop Hallo **Item** map opnieuw in en klikt u op **toevoegen**, en klik vervolgens op **weergave**.
2. In Hallo **weergave toevoegen** dialoogvenster vak, Hallo te volgen:
   
   * In Hallo **weergavenaam** in het vak ***maken***.
   * In Hallo **sjabloon** de optie ***maken***.
   * In Hallo **Modelklasse** de optie ***Item (todo. Modellen)***.
   * Hallo indeling pagina Typ in ***~/Views/Shared/_Layout.cshtml***.
   * Klik op **Add**.
   
#### <a name="_Toc395888515"></a>Een weergave toevoegen voor het bewerken van items
En voeg een weergave voor het bewerken van een **Item** in Hallo dezelfde manier als voorheen.

1. In **Solution Explorer**, klik met de rechtermuisknop Hallo **Item** map opnieuw in en klikt u op **toevoegen**, en klik vervolgens op **weergave**.
2. In Hallo **weergave toevoegen** dialoogvenster vak, Hallo te volgen:
   
   * In Hallo **weergavenaam** in het vak ***bewerken***.
   * In Hallo **sjabloon** de optie ***bewerken***.
   * In Hallo **Modelklasse** de optie ***Item (todo. Modellen)***.
   * Hallo indeling pagina Typ in ***~/Views/Shared/_Layout.cshtml***.
   * Klik op **Add**.

Zodra dit is gebeurd, sluit u alle Hallo cshtml-documenten in Visual Studio als we toothese weergaven later terug.

## <a name="_Toc395637769"></a>Stap 5: Azure Cosmos DB fysiek aansluiten
Nu dat Hallo MVC hebben voltooid is afgehandeld, nu gaan we tooadding Hallo code voor Azure Cosmos DB. 

In deze sectie gaan we de code toohandle Hallo volgende toevoegen:

* [Vermelden van onvolledige items](#_Toc395637770).
* [Items toevoegen](#_Toc395637771).
* [Items bewerken](#_Toc395637772).

### <a name="_Toc395637770"></a>Onvolledige objecten in uw MVC-webtoepassing vermelden
Hallo eerste ding toodo hier is een klasse toevoegen die alle Hallo logica tooconnect tooand gebruik Azure Cosmos DB bevat. Voor deze zelfstudie voegen we alle logica tooa opslagplaatsklasse naam DocumentDBRepository. 

1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project, klik op **toevoegen**, en klik vervolgens op **klasse**. Naam nieuwe klasse Hallo **DocumentDBRepository** en klik op **toevoegen**.
2. In nieuw gemaakte Hallo **DocumentDBRepository** klasse en voeg de volgende Hallo *using-instructies* hierboven Hallo *naamruimte* declaratie
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    Vervang deze code nu 
   
        public class DocumentDBRepository
        {
        }
   
    Hello code te volgen.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. We sommige waarden uit de configuratie van leest, zodat openen Hallo **Web.config** bestand van uw toepassing en voeg de volgende regels onder Hallo Hallo `<AppSettings>` sectie.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. Werk nu Hallo waarden voor *eindpunt* en *authKey* met behulp van de blade van de sleutels Hallo van hello Azure-Portal. Hallo gebruiken **URI** Hallo sleutels blade als Hallo-waarde van Hallo endpoint-instelling en gebruik Hallo **primaire sleutel**, of **secundaire sleutel** van de blade van Hallo sleutels als waarde Hallo Hallo authKey-instelling.

    Dat zorgt voor de bekabeling van de opslagplaats hello Azure Cosmos DB, nu gaan we toepassingslogica toevoegen.

1. Hallo willen eerst te beginnen we toobe kunnen toodo met een takenlijsttoepassing toodisplay Hallo onvolledige items is.  Kopieer en plak de volgende codefragment overal in Hallo Hallo **DocumentDBRepository** klasse.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. Open Hallo **ItemController** we eerder hebt toegevoegd en voeg de volgende Hallo *using-instructies* boven de naamruimtedeclaratie Hallo.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Als uw project niet de naam 'todo', moet u tooupdate met behulp van 'todo. Modellen'; tooreflect Hallo-naam van uw project.
   
    Vervang deze code nu
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    Hello code te volgen.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. Open **Global.asax.cs** en voeg Hallo volgende regel toohello **Application_Start** methode 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

Op dit moment moet uw oplossing kunnen toobuild zonder fouten.

Als u Hallo toepassing nu hebt uitgevoerd, gaat u toohello **HomeController** en Hallo **Index** van die controller. Dit is het standaardgedrag Hallo voor MVC-sjabloonproject Hallo die we aan begin Hallo hebt gekozen, maar we willen dat niet! Laten we Hallo routering op deze MVC-toepassing tooalter dit gedrag wijzigen.

Open ***App\_Start\RouteConfig.cs*** en zoek Hallo regel die begint met "standaardwaarden: ' en wijzigt u tooresemble hello te volgen.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

Hiermee stelt ASP.NET MVC die u hebt een waarde niet opgegeven in Hallo URL toocontrol Hallo routeringsgedrag routeringsgedrag **Start**, gebruik **Item** als Hallo-controller en de gebruiker **Index** als Hallo weergave.

Nu als u de toepassing hello uitvoert, wordt gebeld naar uw **ItemController** die wordt in de opslagplaatsklasse toohello aanroepen en Hallo GetItems methode tooreturn alle Hallo onvolledige items toohello **weergaven** \\ **Item**\\**Index** weergeven. 

Als u dit project nu maakt en uitvoert, ziet u iets dat vergelijkbaar is met het volgende.    

![Schermopname van het Hallo takenlijstwebtoepassing gemaakt met deze databasezelfstudie](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Items toevoegen
Laten we enkele items aan de database zodat we hebben iets meer dan een leeg raster toolook op.

Laten we de code te toevoegen Azure Cosmos DBRepository ItemController toopersist Hallo record in Azure Cosmos DB.

1. Hallo na methode tooyour toevoegen **DocumentDBRepository** klasse.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   Deze methode wordt een tooit doorgegeven object gewoon en deze in Azure Cosmos DB zich blijft voordoen.
2. Hallo ItemController.cs bestand openen en voeg Hallo volgende codefragment in Hallo-klasse. Dit is hoe weet ASP.NET MVC wat toodo voor Hallo **maken** in te grijpen. In dit geval gekoppelde alleen render Hallo Create.cshtml weergave eerder hebt gemaakt.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    Nu moet u meer code in deze controller die Hallo inzending vanuit Hallo accepteert **maken** weergeven.
3. Hallo volgende blok van code toohello klasse ItemController.cs waarmee ASP.NET MVC wat toodo met een form POST voor deze controller toevoegen.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    Deze code roept toohello DocumentDBRepository en Hallo CreateItemAsync methode toopersist Hallo nieuwe todo item toohello database gebruikt. 
   
    **Opmerking over beveiliging**: Hallo **ValidateAntiForgeryToken** kenmerk wordt gebruikt hier toohelp beveiligen voor deze toepassing tegen aanvallen van aanvraagvervalsing op meerdere sites. Er is meer tooit alleen toe te voegen dit kenmerk, uw weergaven moeten toowork met dit anti-vervalsingstoken ook. Voor meer informatie over het Hallo-onderwerp en voorbeelden van hoe tooimplement dit correct Zie [Cross-Site zo wordt voorkomen dat aanvragen vervalsing][Preventing Cross-Site Request Forgery]. broncode op Hallo [GitHub] [ GitHub] beschikt over de volledige implementatie Hallo.
   
    **Opmerking over beveiliging**: We gebruiken ook Hallo **binden** -kenmerk op Hallo methode parameter toohelp beschermen tegen over-postingaanvallen. Zie [Eenvoudige CRUD-bewerkingen in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC] voor meer informatie.

Hiermee is Hallo code vereist tooadd nieuwe Items tooour database.

### <a name="_Toc395637772"></a>Items bewerken
Er is een ding voor ons toodo en dat tooadd Hallo mogelijkheid tooedit **Items** in Hallo-database en toomark als voltooid. Hallo weergave voor bewerken is al toegevoegd toohello project, hoeft daarom alleen tooadd sommige code tooour controller en toohello **DocumentDBRepository** klasse opnieuw.

1. Hallo na toohello toevoegen **DocumentDBRepository** klasse.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    eerste dag van deze methoden Hallo **GetItem** haalt u een Item uit Azure Cosmos-database die wordt doorgegeven back toohello **ItemController** en klik vervolgens op toohello **bewerken** weergeven.
   
    Hallo seconde van Hallo methoden die zojuist is toegevoegd vervangt Hallo **Document** in Azure Cosmos DB met Hallo-versie van Hallo **Document** doorgegeven vanuit Hallo **ItemController**.
2. Hallo na toohello toevoegen **ItemController** klasse.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    Hallo eerste methode verwerkt Hallo Http GET die plaatsvindt wanneer de gebruiker Hallo op Hallo **bewerken** koppeling van Hallo **Index** weergeven. Deze methode haalt een [ **Document** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) van Azure DB die Cosmos en geeft deze door toohello **bewerken** weergeven.
   
    Hallo **bewerken** weergave voert een Http POST-toohello **IndexController**. 
   
    Hallo tweede methode we Hallo bijgewerkt object tooAzure Cosmos DB toobe doorgeven ingangen toegevoegd permanent in Hallo-database.

Dit is alles dat is alles wat we onze toepassing toorun nodig, onvolledige lijst **Items**, nieuwe toevoegen **Items**, en bewerken **Items**.

## <a name="_Toc395637773"></a>Stap 6: Hallo toepassing lokaal uitvoeren
tootest hello toepassing op uw lokale machine Hallo te volgen:

1. Druk op F5 in Visual Studio toobuild Hallo toepassing in de foutopsporingsmodus. Het moet Hallo toepassing bouwen en een browser gestart met de Hallo lege rasterpagina dat we eerder hebben gezien:
   
    ![Schermopname van het Hallo takenlijstwebtoepassing gemaakt met deze databasezelfstudie](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Klik op Hallo **nieuw** koppelen en voeg waarden toohello **naam** en **beschrijving** velden. Hallo laat **voltooid** selectievakje uitgeschakeld anders Hallo nieuwe **Item** worden toegevoegd met een onvoltooide status en wordt niet weergegeven in de initiële lijst Hallo.
   
    ![Schermopname van het Hallo weergave maken](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. Klik op **maken** en u omgeleide back toohello **Index** weergeven en uw **Item** wordt weergegeven in de lijst Hallo.
   
    ![Schermopname van het Hallo weergave Index](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    Kunt u gratis tooadd enkele **Items** tooyour takenlijsten.
    
4. Klik op **bewerken** volgende tooan **Item** op Hallo lijst en u zijn genomen toohello **bewerken** weergave waarin u een eigenschap van het object, met inbegrip van Hallo kunt bijwerken  **Voltooid** vlag. Als u Hallo markeert **Complete** markeert en op **opslaan**, Hallo **Item** wordt verwijderd uit de lijst Hallo met onvolledige taken.
   
    ![Schermopname van het Hallo weergave Index met de selectievakje voltooid Hallo ingeschakeld](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Zodra u Hallo app hebt getest, drukt u op Ctrl + F5 toostop foutopsporing Hallo-app. U bent klaar toodeploy!

## <a name="_Toc395637774"></a>Stap 7: Hallo toepassing tooAzure App Service implementeren 
Nu dat u de volledige toepassing hello hebt gaan correct werkt met Azure Cosmos DB we toodeploy deze web-app tooAzure App Service.  

1. toopublish alle van deze toepassing moet u toodo is met de rechtermuisknop op het Hallo-project in **Solution Explorer** en klik op **publiceren**.
   
    ![Schermopname van het Hallo optie publiceren in Solution Explorer](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. In Hallo **publiceren** in het dialoogvenster klikt u op **Microsoft Azure App Service**, selecteer daarna **nieuw** toocreate een App Service-profiel, of klik op **selecteren Bestaande** toouse een bestaand profiel.

    ![Het dialoogvenster Publish in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. Als u een bestaand Azure App Service-profiel, voert u de abonnementsnaam van uw. Gebruik Hallo **weergave** toosort door resourcegroep of resourcetype filteren en selecteer vervolgens uw Azure App Service. 
   
    ![In het dialoogvenster App Service in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. toocreate een nieuw Azure App Service-profiel, klikt u op **nieuw** in Hallo **publiceren** in het dialoogvenster. In Hallo **Create App Service** dialoogvenster, Voer uw Web-App-naam en de juiste abonnement, de resourcegroep en de App Service-abonnement en klik vervolgens op **maken**.

    ![Het dialoogvenster App Service maken in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

Binnen een paar seconden zal Visual Studio publicatie van uw webtoepassing voltooien en een browser starten waarin u kunt zien uw werk in Azure wordt uitgevoerd!



## <a name="_Toc395637775"></a>Volgende stappen
Gefeliciteerd. U zojuist hebt gemaakt van uw eerste ASP.NET MVC-webtoepassing met Azure Cosmos DB en tooAzure gepubliceerd. Hallo broncode voor de volledige toepassing hello, met inbegrip van Hallo detail functionaliteit en verwijderen die niet zijn opgenomen in deze zelfstudie kan worden gedownload of gekloond van [GitHub][GitHub]. Dus als u geïnteresseerd bent in die app tooyour toe te voegen, halen Hallo code en voeg deze toothis app.

Bekijk Hallo beschikbare API's in Hallo-tooadd aanvullende functionaliteit tooyour toepassing [Azure Cosmos DB .NET-bibliotheek](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) harte gratis toocontribute toohello Azure Cosmos DB .NET-bibliotheek op [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
