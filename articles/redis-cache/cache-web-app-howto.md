---
title: aaaHow toocreate een Web-App met Redis-Cache | Microsoft Docs
description: Meer informatie over hoe toocreate een Web-App met Redis-Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>Hoe toocreate een Web-App met Redis-Cache
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Deze zelfstudie laat zien hoe toocreate en implementeren van een ASP.NET web application tooa web-app in Azure App Service met behulp van Visual Studio 2017. Hallo-voorbeeldtoepassing geeft een lijst met teamstatistieken uit een database en toont de verschillende manieren toouse Azure Redis-Cache toostore en gegevens ophalen uit de cache Hallo. Wanneer u Hallo-zelfstudie hebt voltooid hebt u een actieve WebApp die leest en schrijft tooa database geoptimaliseerd met Azure Redis-Cache en wordt gehost in Azure.

U leert het volgende:

* Hoe toocreate een ASP.NET MVC 5-webtoepassing in Visual Studio.
* Hoe tooaccess gegevens uit een database met behulp van Entity Framework.
* Hoe tooimprove gegevensdoorvoer en belasting van de database te verminderen door opslaan en ophalen van gegevens met behulp van Azure Redis-Cache.
* Hoe toouse een in Redis gesorteerde set tooretrieve Hallo bovenste 5 teams.
* Tooprovision Hallo hoe Azure-resources voor Hallo-toepassing met een Resource Manager-sjabloon.
* Hoe Hallo toopublish tooAzure van toepassing met Visual Studio.

## <a name="prerequisites"></a>Vereisten
toocomplete hello zelfstudie, moet u Hallo na vereisten hebben.

* [Azure-account](#azure-account)
* [Visual Studio 2017 Hello Azure SDK voor .NET](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Azure-account
U hebt een Azure-account toocomplete Hallo zelfstudie nodig. U kunt:

* [Gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). U ontvangt tegoed dat gebruikte tootry uit betaald Azure-services worden kunnen. Zelfs nadat Hallo tegoed is gebruikt, kunt u Hallo account houden en gratis Azure-services en functies gebruikt.
* [Uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Via uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Visual Studio 2017 Hello Azure SDK voor .NET
Hallo-zelfstudie is geschreven voor Visual Studio 2017 Hello [Azure SDK voor .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools). Hello Azure SDK 2.9.5 is opgenomen in Visual Studio-installatieprogramma Hallo.

Als u Visual Studio 2015 hebt, kunt u de zelfstudie Hallo Hello [Azure SDK voor .NET](../dotnet-sdk.md) 2.8.2 of hoger. [Download Hallo nieuwste Azure SDK voor Visual Studio 2015 hier](http://go.microsoft.com/fwlink/?linkid=518003). Visual Studio wordt automatisch geïnstalleerd met Hallo SDK als u nog geen hebt. Sommige schermen zien er mogelijk anders uit Hallo illustraties wordt weergegeven in deze zelfstudie.

Als u Visual Studio 2013 hebt, kunt u [downloaden hello nieuwste Azure SDK voor Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322). Sommige schermen zien er mogelijk anders uit Hallo illustraties wordt weergegeven in deze zelfstudie.

## <a name="create-hello-visual-studio-project"></a>Hallo Visual Studio-project maken
1. Open Visual Studio en klik op **File**, **New**, **Project**.
2. Vouw Hallo **Visual C#** knooppunt in Hallo **sjablonen** selecteert **Cloud**, en klik op **ASP.NET-webtoepassing**. Zorg ervoor dat **.NET Framework 4.5.2** of hoger is geselecteerd.  Type **ContosoTeamStats** in Hallo **naam** tekstvak en klik op **OK**.
   
    ![Project maken][cache-create-project]
3. Selecteer **MVC** als Hallo projecttype. 

    Zorg ervoor dat **geen verificatie** is opgegeven voor Hallo **verificatie** instellingen. Afhankelijk van uw versie van Visual Studio kan Hallo standaard toosomething anders worden ingesteld. toochange, klikt u op **verificatie wijzigen** en selecteer **geen verificatie**.

    Als u samen met Visual Studio 2015 volgt, schakelt u Hallo **hosten in de cloud Hallo** selectievakje. U zult [inrichten hello Azure-resources](#provision-the-azure-resources) en [publiceren Hallo toepassing tooAzure](#publish-the-application-to-azure) bij volgende stappen in de zelfstudie Hallo. Voor een voorbeeld van een App Service-web-app vanuit Visual Studio wordt ingericht door **hosten in de cloud Hallo** dit selectievakje inschakelt, Zie [aan de slag met Web-Apps in Azure App Service met ASP.NET en Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
    ![De projectsjabloon selecteren][cache-select-template]
4. Klik op **OK** toocreate Hallo project.

## <a name="create-hello-aspnet-mvc-application"></a>Hallo ASP.NET MVC-toepassing maken
In deze sectie van Hallo zelfstudie maakt u eenvoudige Hallo-toepassing die wordt gelezen en wordt de teamstatistieken uit een database.

* [Hallo Entity Framework NuGet-pakket toevoegen](#add-the-entity-framework-nuget-package)
* [Hallo model toevoegen](#add-the-model)
* [Hallo controller toevoegen](#add-the-controller)
* [Hallo-weergaven configureren](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>Hallo Entity Framework NuGet-pakket toevoegen

1. Klik op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu.
2. Voer hello na de opdracht van Hallo **Package Manager Console** venster.
    
    ```
    Install-Package EntityFramework
    ```

Zie voor meer informatie over dit pakket Hallo [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet-pagina.

### <a name="add-hello-model"></a>Hallo model toevoegen
1. Klik in **Solution Explorer** met de rechtermuisknop op **Models** en kies **Add**, **Class**. 
   
    ![Het model toevoegen][cache-model-add-class]
2. Voer `Team` voor Hallo klassenaam en klik op **toevoegen**.
   
    ![De modelklasse toevoegen][cache-model-add-class-dialog]
3. Vervang Hallo `using` instructies boven Hallo Hallo `Team.cs` bestand met de volgende Hallo `using` instructies.

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. Hallo-definitie Hallo vervangen `Team` klasse met het volgende codefragment bevat een bijgewerkte Hallo `Team` klasse definition, evenals een aantal andere helperklassen van Entity Framework. Zie voor meer informatie over Hallo code eerste benadering tooEntity Framework die wordt gebruikt in deze zelfstudie [Code eerste tooa nieuwe database](https://msdn.microsoft.com/data/jj193542).

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. In **Solution Explorer**, dubbelklikt u op **web.config** tooopen deze.
   
    ![Web.config][cache-web-config]
2. Voeg de volgende Hallo `connectionStrings` sectie. Hallo-naam van de verbindingsreeks Hallo moet overeenkomen met naam van de Hallo Hallo Entity Framework database contextklasse die `TeamContext`.

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    U kunt nieuwe Hallo toevoegen `connectionStrings` sectie zodat het achter `configSections`, zoals weergegeven in het volgende voorbeeld Hallo.

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > De verbindingsreeks kan afwijken, afhankelijk van het Hallo-versie van Visual Studio en SQL Server Express edition toocomplete Hallo zelfstudie gebruikt. Hallo web.config sjabloon moet geconfigureerde toomatch uw installatie, en mogen bevatten `Data Source` vermeldingen, zoals `(LocalDB)\v11.0` (van SQL Server Express 2012) of `Data Source=(LocalDB)\MSSQLLocalDB` (vanuit SQL Server Express 2014 en nieuwer). Zie [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) voor meer informatie over verbindingsreeksen en SQL Express-versies.

### <a name="add-hello-controller"></a>Hallo controller toevoegen
1. Druk op **F6** toobuild Hallo project. 
2. In **Solution Explorer**, klik met de rechtermuisknop Hallo **domeincontrollers** map en kies **toevoegen**, **Controller**.
   
    ![Controller toevoegen][cache-add-controller]
3. Kies **MVC 5 Controller with views, using Entity Framework** en klik op **Add**. Als u een fout optreedt wanneer u op **toevoegen**, zorg ervoor dat u Hallo project eerst hebt gebouwd.
   
    ![Controllerklasse toevoegen][cache-add-controller-class]
4. Selecteer **Team (ContosoTeamStats.Models)** van Hallo **Modelklasse** vervolgkeuzelijst. Selecteer **TeamContext (ContosoTeamStats.Models)** van Hallo **Data context class** vervolgkeuzelijst. Type `TeamsController` in Hallo **Controller** naam textbox (indien dit niet automatisch wordt ingevuld). Klik op **toevoegen** toocreate controllerklasse Hallo en Hallo standaardweergaven toe te voegen.
   
    ![Controller configureren][cache-configure-controller]
5. In **Solution Explorer**, vouw **Global.asax** en dubbelklikt u op **Global.asax.cs** tooopen deze.
   
    ![Global.asax.cs][cache-global-asax]
6. Na twee Hallo toevoegen `using` instructies Hallo boven aan het bestand onder andere Hallo Hallo `using` instructies.

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. Toevoegen van de volgende regel code achter Hallo HALLO hallo `Application_Start` methode.

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. Vouw in **Solution Explorer** `App_Start` uit en dubbelklik op `RouteConfig.cs`.
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. Vervang `controller = "Home"` in de volgende code in Hallo Hallo `RegisterRoutes` methode met `controller = "Teams"` zoals weergegeven in Hallo voorbeeld te volgen.

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>Hallo-weergaven configureren
1. In **Solution Explorer**, vouw Hallo **weergaven** map en klik vervolgens op Hallo **gedeelde** map uit en dubbelklik op **_Layout.cshtml**. 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. Hallo-inhoud van Hallo wijzigen `title` element en vervang `My ASP.NET Application` met `Contoso Team Stats` zoals weergegeven in Hallo voorbeeld te volgen.

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. In Hallo `body` sectie, Hallo eerst bijwerken `Html.ActionLink` -instructie en vervang `Application name` met `Contoso Team Stats` en vervang `Home` met `Teams`.
   
   * Voor: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * Na: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![Codewijzigingen][cache-layout-cshtml-code]
2. Druk op **Ctrl + F5** toobuild en Voer Hallo-toepassing. Deze versie van de toepassing hello leest Hallo resultaten rechtstreeks uit Hallo-database. Opmerking Hallo **nieuw**, **bewerken**, **Details**, en **verwijderen** acties die automatisch zijn toohello toepassing toegevoegd door Hallo **MVC 5 Controller with views, using Entity Framework** scaffold. In de volgende sectie Hallo van Hallo zelfstudie voegt u Redis-Cache toooptimize Hallo gegevens openen en bieden extra functies toohello toepassing.

![Beginnerstoepassing][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>Hallo toepassing toouse Redis-Cache configureren
In deze sectie van de zelfstudie hello, past u Hallo voorbeeld toepassing toostore configureren en ophalen van de Contoso-teamstatistieken uit een Azure Redis-Cache-exemplaar met behulp van Hallo [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cacheclient.

* [Hallo toepassing toouse StackExchange.Redis configureren](#configure-the-application-to-use-stackexchangeredis)
* [Hallo TeamsController klasse tooreturn resultaten uit Hallo cache of Hallo-database bijwerken](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [Hallo maken, bewerken, bijwerken en verwijderen van de methoden toowork met Hallo-cache](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [Hallo Teamindex weergave toowork bijwerken met Hallo-cache](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>Hallo toepassing toouse StackExchange.Redis configureren
1. tooconfigure een clienttoepassing in Visual Studio met Hallo NuGet-pakket StackExchange.Redis, klikt u op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu.
2. Voer hello na de opdracht van Hallo `Package Manager Console` venster.
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    assembly-verwijzingen Hallo NuGet-pakket downloadt en voegt Hallo vereist voor uw client-toepassing tooaccess Azure Redis-Cache met Hallo StackExchange.Redis cacheclient. Als u liever een versie met sterke naam Hallo toouse `StackExchange.Redis` clientbibliotheek, installatie Hallo `StackExchange.Redis.StrongName` pakket.
3. In **Solution Explorer**, vouw Hallo **domeincontrollers** map en dubbelklik op **TeamsController.cs** tooopen deze.
   
    ![TeamsController][cache-teamscontroller]
4. Na twee Hallo toevoegen `using` instructies te**TeamsController.cs**.

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. Toevoegen van de volgende twee eigenschappen toohello Hallo `TeamsController` klasse.

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. Maak een bestand op uw computer met de naam `WebAppPlusCacheAppSecrets.config` en plaats deze in een locatie die niet wordt ingecheckt met Hallo broncode van uw voorbeeldtoepassing, mocht u toocheck besluiten deze ergens in. In dit voorbeeld Hallo `AppSettingsSecrets.config` bestand bevindt zich op `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.
   
    Hallo bewerken `WebAppPlusCacheAppSecrets.config` bestand en voeg Hallo inhoud te volgen. Als u de toepassing hello lokaal uitvoert is deze informatie gebruikt tooconnect tooyour Azure Redis-Cache-exemplaar. Verderop in de zelfstudie Hallo u inrichten van een Azure Redis-Cache-exemplaar en Hallo-cache en het wachtwoord bijwerken. Als u niet van plan toorun Hallo-voorbeeldtoepassing bent lokaal u Hallo maken van dit bestand kunt overslaan en Hallo hierop volgende stappen die verwijzen naar Hallo-bestand, omdat wanneer u tooAzure Hallo toepassing implementeert Hallo cache verbindingsgegevens opgehaald uit Hallo app instelling voor Hallo Web-App en niet uit dit bestand. Sinds Hallo `WebAppPlusCacheAppSecrets.config` niet is geïmplementeerd tooAzure met uw toepassing hoeft tenzij u toorun Hallo toepassing lokaal gaat.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. In **Solution Explorer**, dubbelklikt u op **web.config** tooopen deze.
   
    ![Web.config][cache-web-config]
2. Voeg de volgende Hallo `file` toohello kenmerk `appSettings` element. Als u een andere naam of locatie gebruikt, vervangen door deze waarden Hallo die wordt weergegeven in Hallo voorbeeld.
   
   * Voor: `<appSettings>`
   * Na: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   Hallo ASP.NET-runtime voegt Hallo inhoud van extern bestand met aantekeningen in Hallo HALLO hallo samen `<appSettings>` element. Hallo runtime negeert Hallo file-kenmerk als Hallo opgegeven bestand kan niet worden gevonden. Uw geheimen (Hallo verbinding tooyour tekenreekscache) zijn niet opgenomen als onderdeel van de broncode Hallo voor Hallo-toepassing. Wanneer u uw web-app tooAzure implementeert, Hallo `WebAppPlusCacheAppSecrests.config` bestand niet geïmplementeerd (dat wil zeggen naar wens). Er zijn verschillende manieren toospecify deze geheime gegevens in Azure, en in deze zelfstudie ze zijn geconfigureerd automatisch voor u wanneer u [inrichten hello Azure-resources](#provision-the-azure-resources) in een latere stap van de zelfstudie. Zie voor meer informatie over het werken met geheimen in Azure [aanbevolen procedures voor het implementeren van wachtwoorden en andere gevoelige gegevens tooASP.NET en Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>Hallo TeamsController klasse tooreturn resultaten uit Hallo cache of Hallo-database bijwerken
In dit voorbeeld kunnen teamstatistieken uit de database Hallo of uit de cache Hallo worden opgehaald. Teamstatistieken worden opgeslagen in cache als een geserialiseerde Hallo `List<Team>`, en ook als een gesorteerde set met Redis-gegevenstypen. Bij het ophalen van items uit een gesorteerde set kunt u een query uitvoeren voor sommige items, voor alle items of alleen voor bepaalde items. In dit voorbeeld voert u een query Hallo gesorteerd set voor Hallo bovenste 5 teams door het aantal wins gerangschikt.

> [!NOTE]
> Het is niet vereist toostore hello teamstatistieken in verschillende indelingen in de cache Hallo in volgorde toouse Azure Redis-Cache. Deze zelfstudie wordt gebruikgemaakt van meerdere indelingen toodemonstrate enkele van de verschillende manieren Hallo en verschillende gegevenstypen kunt u toocache gegevens.
> 
> 

1. Voeg de volgende Hallo `using` instructies toohello `TeamsController.cs` bestand boven Hallo Hello andere `using` instructies.

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. Hallo huidige vervangen `public ActionResult Index()` methode-implementatie met Hallo na implementatie.

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. Toevoegen van de volgende drie methoden toohello hello `TeamsController` klasse tooimplement hello `playGames`, `clearCache`, en `rebuildDB` actietypen van Hallo instructie toegevoegd in het vorige codefragment Hallo switch.
   
    Hallo `PlayGames` methode Hallo teamstatistieken bijgewerkt door een seizoen wedstrijden te simuleren, slaat Hallo resultaten toohello database en wist Hallo nu verouderde gegevens uit de cache Hallo.

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hallo `RebuildDB` methode opnieuw Hallo database met Hallo standaardset teams, genereert statistieken voor ze en wist Hallo nu verouderde gegevens uit de cache Hallo.

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hallo `ClearCachedTeams` methode verwijdert opgeslagen teamstatistieken uit de cache Hallo.

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. Toevoegen van de volgende vier methoden toohello hello `TeamsController` klasse tooimplement Hallo verschillende manieren voor het ophalen van teamstatistieken Hallo van Hallo-cache en Hallo-database. Elk van deze methoden retourneert een `List<Team>` die vervolgens door Hallo weergave wordt weergegeven.
   
    Hallo `GetFromDB` methode leest de teamstatistieken Hallo uit Hallo-database.
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    Hallo `GetFromList` methode leest de teamstatistieken Hallo uit de cache als een geserialiseerde `List<Team>`. Als er een cache ontbreekt, worden Hallo teamstatistieken gelezen uit de database Hallo en vervolgens in Hallo cache zijn opgeslagen voor later. In dit voorbeeld we maken gebruik van JSON.NET-serialisatie tooserialize Hallo .NET-objecten tooand uit Hallo-cache. Zie voor meer informatie [hoe toowork met .NET-objecten in Azure Redis-Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    Hallo `GetFromSortedSet` methode leest de teamstatistieken Hallo uit een in cache opgeslagen gesorteerde set. Als er een cache ontbreekt, worden teamstatistieken Hallo Hallo-database niet lezen en opgeslagen in de cache Hallo als een gesorteerde set.

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    Hallo `GetFromSortedSetTop5` methode leest Hallo bovenste 5 teams van Hallo in de cache opgeslagen gesorteerde set. Deze methode begint met het Hallo-cache controleren voor Hallo bestaan Hallo `teamsSortedSet` sleutel. Als deze sleutel niet aanwezig is, Hallo `GetFromSortedSet` methode tooread hello teamstatistieken wordt genoemd en op te slaan in Hallo-cache. Vervolgens hello in de cache opgeslagen gesorteerde set gevraagd voor Hallo bovenste 5 teams die worden geretourneerd.

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>Hallo maken, bewerken, bijwerken en verwijderen van de methoden toowork met Hallo-cache
Hallo ondersteuningscode die is gegenereerd als onderdeel van dit voorbeeld bevat de methoden tooadd, bewerken en verwijderen van teams. Telkens wanneer een team wordt toegevoegd, bewerkt of verwijderd, verouderd Hallo-gegevens in Hallo cache. In deze sectie u bewerkt deze drie methoden tooclear Hallo in cache opgeslagen teams zodat Hallo-cache is niet synchroon met Hallo-database.

1. Blader toohello `Create(Team team)` methode in Hallo `TeamsController` klasse. Voeg een aanroep van toohello `ClearCachedTeams` methode, zoals wordt weergegeven in het volgende voorbeeld Hallo.

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. Blader toohello `Edit(Team team)` methode in Hallo `TeamsController` klasse. Voeg een aanroep van toohello `ClearCachedTeams` methode, zoals wordt weergegeven in het volgende voorbeeld Hallo.

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. Blader toohello `DeleteConfirmed(int id)` methode in Hallo `TeamsController` klasse. Voeg een aanroep van toohello `ClearCachedTeams` methode, zoals wordt weergegeven in het volgende voorbeeld Hallo.

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>Hallo Teamindex weergave toowork bijwerken met Hallo-cache
1. In **Solution Explorer**, vouw Hallo **weergaven** map en klik vervolgens Hallo **Teams** map uit en dubbelklik op **Index.cshtml**.
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. Aan de bovenkant van de Hallo van Hallo-bestand, zoek naar Hallo volgende alinea-element.
   
    ![Actietabel][cache-teams-index-table]
   
    Dit is Hallo koppeling toocreate een nieuw team. Hallo alinea-element met de volgende tabel Hallo vervangen. Deze tabel bevat Actiekoppelingen voor het maken van een nieuw team, een nieuw seizoen wedstrijden, Hallo cache wissen spelen, Hallo teams ophalen uit de cache Hallo in verschillende indelingen, Hallo teams ophalen uit de database Hallo en opnieuw opbouwen van de database met de nieuwe voorbeeldgegevens Hallo.

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. Scroll toohello onderaan Hallo **Index.cshtml** -bestand en voeg de volgende Hallo `tr` element zodat deze de laatste rij Hallo in Hallo laatste tabel in Hallo-bestand.
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    Deze rij geeft de waarde van Hallo `ViewBag.Msg` die een statusrapport over de huidige bewerking Hallo bevat. Hallo `ViewBag.Msg` wanneer u klikt op een van de Actiekoppelingen Hallo van de vorige stap Hallo is ingesteld.   
   
    ![Statusbericht][cache-status-message]
2. Druk op **F6** toobuild Hallo project.

## <a name="provision-hello-azure-resources"></a>Inrichten hello Azure-resources
toohost uw toepassing in Azure, moet u eerst inrichten hello Azure-services die vereist zijn voor uw toepassing. Hallo-voorbeeldtoepassing in deze zelfstudie maakt gebruik van hello Azure-services te volgen.

* Azure Redis-cache
* App Service-web-app
* SQL Database

toodeploy deze services tooa nieuwe of bestaande resourcegroep naar keuze, klikt u op volgende Hallo **tooAzure implementeren** knop.

[! [TooAzure implementeren] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

Dit **implementeren tooAzure** knop gebruikt Hallo [maken van een Web-App plus Redis-Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) sjabloon tooprovision deze services en een set Hallo de verbindingsreeks voor Hallo SQL-Database en Hallo toepassingsinstelling voor hello Azure Redis-Cache-verbindingsreeks.

> [!NOTE]
> Als u geen Azure-account hebt, kunt u binnen een paar minuten [een gratis Azure-account maken](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).
> 
> 

Te klikken op Hallo **tooAzure implementeren** knop gaat u verder toohello Azure-portal en initieert Hallo Hallo resources beschreven door Hallo-sjabloon maken.

![TooAzure implementeren][cache-deploy-to-azure-step-1]

1. In Hallo **basisbeginselen** sectie Selecteer toouse hello Azure-abonnement, en selecteer een bestaande resourcegroep of maak een nieuwe, en geef Hallo locatie voor resourcegroep.
2. In Hallo **instellingen** sectie, geeft u een **aanmeldingsnaam van de beheerder** (gebruik geen **admin**), **beheerderswachtwoord voor aanmelding**, en  **Databasenaam**. Hallo zijn andere parameters geconfigureerd voor een gratis App Service-hostingplan en goedkoper opties voor Hallo SQL-Database en Azure Redis-Cache, die niet geleverd met een gratis laag.

    ![TooAzure implementeren][cache-deploy-to-azure-step-2]

3. Ga na het configureren van instellingen Hallo gewenst toohello einde van de pagina Hallo lezen Hallo en voorwaarden en Hallo controleren **ik ga akkoord toohello voorwaarden bovengenoemde** selectievakje.
4. toobegin inrichting Hallo resources, klikt u op **aankoop**.

tooview hello voortgang van uw implementatie, klik op het pictogram in systeemvak Hallo en op **implementatie gestart**.

![Implementatie gestart][cache-deployment-started]

U kunt Hallo status van uw implementatie bekijken op Hallo **Microsoft.Template** blade.

![TooAzure implementeren][cache-deploy-to-azure-step-3]

Bij het inrichten is voltooid, kunt u uw toepassing tooAzure vanuit Visual Studio kunt publiceren.

> [!NOTE]
> Eventuele fouten die optreden tijdens het inrichtingsproces Hallo worden weergegeven op Hallo **Microsoft.Template** blade. Veelvoorkomende fouten zijn te veel SQL Servers of te veel gratis App Service-hostingplannen per abonnement. Los eventuele fouten en het Hallo-proces opnieuw starten door te klikken op **implementeren** op Hallo **Microsoft.Template** blade of Hallo **tooAzure implementeren** knop in deze zelfstudie.
> 
> 

## <a name="publish-hello-application-tooazure"></a>Hallo toepassing tooAzure publiceren
In deze stap van de zelfstudie Hallo u Hallo toepassing tooAzure publiceren en deze in de cloud Hallo uitvoeren.

1. Klik met de rechtermuisknop Hallo **ContosoTeamStats** in Visual Studio-project en kies **publiceren**.
   
    ![Publiceren][cache-publish-app]
2. Klik op **Microsoft Azure App Service**, kies **Bestaande selecteren** en klik op **Publiceren**.
   
    ![Publiceren][cache-publish-to-app-service]
3. Selecteer Hallo abonnement dat u gebruikt wanneer Hallo resourcegroep die Hallo resources maken hello Azure-resources, uitbreiden, en selecteer Hallo Web-App gewenst. Als u Hallo gebruikt **implementeren tooAzure** knop de naam van uw Web-App met begint **webSite** gevolgd door een aantal extra tekens.
   
    ![Web-app selecteren][cache-select-web-app]
4. Klik op **OK** toobegin Hallo publicatieproces. Na enkele ogenblikken Hallo publicatieproces is voltooid en een browser wordt gestart met Hallo voorbeeldtoepassing wordt uitgevoerd. Als u een DNS-fout tijdens het valideren of publiceren en Hallo inrichtingsproces voor hello Azure-resources voor de toepassing hello is net is voltooid, wacht even en probeer het opnieuw.
   
    ![Cache toegevoegd][cache-added-to-application]

Hallo beschrijft volgende tabel elke actiekoppeling in Hallo-voorbeeldtoepassing.

| Actie | Beschrijving |
| --- | --- |
| Create New |Een nieuw team maken |
| Play Season |Speel een seizoen wedstrijden, update Hallo teamstatistieken bij en wis eventuele team gegevens uit Hallo cache verouderd. |
| Clear Cache |Schakel Hallo teamstatistieken uit de cache Hallo. |
| List from Cache |Haal de teamstatistieken Hallo uit Hallo-cache. Als er een cache ontbreekt, Hallo statistieken uit Hallo database laden en toohello cache opslaan voor later. |
| Sorted Set from Cache |Haal de teamstatistieken Hallo uit Hallo-cache met behulp van een gesorteerde set. Als er een cache ontbreekt, Hallo statistieken uit Hallo database laden en toohello-cache met behulp van een gesorteerde set opslaan. |
| Top 5 Teams from Cache |Top 5 teams Hallo ophalen uit Hallo-cache met behulp van een gesorteerde set. Als er een cache ontbreekt, Hallo statistieken uit Hallo database laden en toohello-cache met behulp van een gesorteerde set opslaan. |
| Load from DB |Haal de teamstatistieken Hallo uit Hallo-database. |
| Rebuild DB |Hallo-database opnieuw en laad deze opnieuw met voorbeeldgegevens van het team. |
| Edit/Details/Delete |Bewerk een team, geef details van een team weer en verwijder een team. |

Klik op een aantal Hallo acties en Experimenteer met het Hallo-gegevens ophalen uit verschillende bronnen Hallo. Geen Hallo verschillen in Hallo duurt toocomplete Hallo verschillende manieren voor het Hallo-gegevens ophalen uit het Hallo-database en Hallo-cache.

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>Hallo-resources verwijderen wanneer u klaar met de toepassing hello bent
Wanneer u klaar met zelfstudie voorbeeldtoepassing hello bent, kunt u hello Azure verwijderen resources die worden gebruikt in de volgorde tooconserve kosten en resources. Als u Hallo **implementeren tooAzure** knop in Hallo [inrichten hello Azure-resources](#provision-the-azure-resources) sectie en al uw resources zijn opgenomen in Hallo dezelfde resourcegroep bevinden, kunt u ze verwijderen samen in één de bewerking is door het verwijderen van resourcegroep Hallo.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) en klik op **resourcegroepen**.
2. Hallo-typenaam van de resourcegroep in Hallo **items filteren...**  textbox.
3. Klik op **...**  toohello rechts van de resourcegroep.
4. Klik op **Verwijderen**.
   
    ![Verwijderen][cache-delete-resource-group]
5. Hallo-typenaam van uw resourcegroep en klik op **verwijderen**.
   
    ![De verwijdering bevestigen][cache-delete-confirm]

Na enkele ogenblikken Hallo resource groep en alle ingesloten bronnen verwijderd.

> [!IMPORTANT]
> Houd er rekening mee dat het verwijderen van een resourcegroep niet ongedaan worden gemaakt en Hallo resourcegroep en alle Hallo resources daarin permanent verwijderd. Zorg ervoor dat u niet per ongeluk Hallo verkeerde resourcegroep of resources verwijdert. Als u Hallo resources voor het hosten van dit voorbeeld in een bestaande resourcegroep hebt gemaakt, kunt u elke resource afzonderlijk verwijderen via hun respectievelijke blades.
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>Hallo-voorbeeldtoepassing uitvoeren op uw lokale computer
toorun hello toepassing lokaal op uw computer, moet u een Azure Redis-Cache-exemplaar in welke toocache uw gegevens. 

* Als u kunt uw toepassing tooAzure hebt gepubliceerd, zoals beschreven in de vorige sectie hello, kunt u hello Azure Redis-Cache-exemplaar dat tijdens die stap is ingericht.
* Als u een ander bestaand exemplaar van Azure Redis-Cache hebt, kunt u die toorun in dit voorbeeld lokaal.
* Als u een Azure Redis-Cache-exemplaar toocreate moet, u kunt stappen Hallo in [een cache maken](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

Zodra u hebt geselecteerd of gemaakt Hallo cache toouse, toohello cache in hello Azure-portal bladeren en ophalen van Hallo [hostnaam](cache-configure.md#properties) en [toegangssleutels](cache-configure.md#access-keys) voor uw cache. Zie [Redis-cache-instellingen configureren](cache-configure.md#configure-redis-cache-settings) voor instructies.

1. Open Hallo `WebAppPlusCacheAppSecrets.config` -bestand dat u hebt gemaakt tijdens het Hallo [Hallo toepassing toouse Redis-Cache configureren](#configure-the-application-to-use-redis-cache) stap van deze zelfstudie met Hallo-editor van uw keuze.
2. Hallo bewerken `value` kenmerk en vervang `MyCache.redis.cache.windows.net` Hello [hostnaam](cache-configure.md#properties) van de cache en Geef ofwel Hallo [primaire of secundaire sleutel](cache-configure.md#access-keys) van de cache als Hallo wachtwoord.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Druk op **Ctrl + F5** toorun Hallo-toepassing.

> [!NOTE]
> Let op: omdat Hallo toepassing, met inbegrip van Hallo-database lokaal wordt uitgevoerd en hello Redis-Cache wordt gehost in Azure, Hallo cache lijkt toounder-Hallo database uitvoeren. Voor de beste prestaties Hallo-clienttoepassing en Azure Redis-Cache-exemplaar moet Hallo dezelfde locatie. 
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [aan de slag met ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) op Hallo [ASP.NET](http://asp.net/) site.
* Zie voor meer voorbeelden van het maken van een ASP.NET-Web-App in App Service [maken en implementeren van een ASP.NET-web-app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) van Hallo [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * Zie voor meer snelstartgidsen van Hallo HealthClinic.biz demo [Azure Developer Tools snelstartgidsen](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
* Meer informatie over Hallo [Code eerste tooa nieuwe database](https://msdn.microsoft.com/data/jj193542) benaderen tooEntity Framework die wordt gebruikt in deze zelfstudie.
* Meer informatie over [web-apps in Azure App Service](../app-service-web/app-service-web-overview.md).
* Meer informatie over hoe te[monitor](cache-how-to-monitor.md) uw cache in hello Azure-portal.
* De premiumfuncties van de Azure Redis-cache verkennen
  
  * [Hoe tooconfigure persistentie voor een Premium Azure Redis-Cache](cache-how-to-premium-persistence.md)
  * [Hoe tooconfigure clustering voor een Premium Azure Redis-Cache](cache-how-to-premium-clustering.md)
  * [Hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache](cache-how-to-premium-vnet.md)
  * Zie Hallo [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) voor meer informatie over de grootte, doorvoer en bandbreedte van premiumcaches.

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

