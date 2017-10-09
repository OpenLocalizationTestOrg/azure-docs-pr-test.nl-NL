---
title: aaaUsing elastische database-clientbibliotheek met Entity Framework | Microsoft Docs
description: Gebruik van de clientbibliotheek voor elastische Database en Entity Framework voor het coderen van databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>Elastische Database-clientbibliotheek met Entity Framework
Dit document bevat Hallo wijzigingen in een Entity Framework-toepassing die vereiste toointegrate Hello [hulpmiddelen voor elastische databases](sql-database-elastic-scale-introduction.md). Hallo richt zich voornamelijk op het samenstellen van [shard kaart management](sql-database-elastic-scale-shard-map-management.md) en [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) Hello Entity Framework **Code First** benadering. Hallo [Code eerst - nieuwe Database](http://msdn.microsoft.com/data/jj193542.aspx) zelfstudie voor EF fungeert als het actieve voorbeeld in dit hele document. Hallo voorbeeldcode bij dit document is onderdeel van de elastische database tools van de voorbeelden in Visual Studio-codevoorbeelden Hallo ingesteld.

## <a name="downloading-and-running-hello-sample-code"></a>Downloaden en uitvoeren van Hallo voorbeeldcode
toodownload hello code voor dit artikel:

* Visual Studio 2012 of hoger is vereist. 
* Hallo downloaden [elastische DB-hulpprogramma's voor Azure SQL - Entity Framework integratie voorbeeld](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) van MSDN. Pak Hallo voorbeeld tooa locatie van uw keuze.
* Start Visual Studio. 
* In Visual Studio-Selecteer-Bestand > Open Project/oplossing. 
* In Hallo **Project openen** dialoogvenster gaat toohello voorbeeld die u hebt gedownload en selecteert u **EntityFrameworkCodeFirst.sln** tooopen Hallo voorbeeld. 

toorun hello voorbeeld moet u drie toocreate leeg databases in Azure SQL Database:

* Shard-toewijzing Manager-database
* 1 shard-database
* 2 shard-database

Nadat u deze databases hebt gemaakt, vult u Hallo plaats houders in **Program.cs** met de naam van uw Azure SQL DB, Hallo databasenamen en uw referenties tooconnect toohello databases. Hallo-oplossing in Visual Studio maken. Visual Studio downloadt Hallo vereist NuGet-pakketten voor het Hallo-clientbibliotheek voor elastische database Entity Framework en tijdelijke fout verwerken als onderdeel van Hallo buildproces. Zorg ervoor dat het herstellen van NuGet-pakketten is ingeschakeld voor uw oplossing. U kunt deze instelling inschakelen door met de rechtermuisknop op Hallo oplossingsbestand in Visual Studio Solution Explorer Hallo. 

## <a name="entity-framework-workflows"></a>Entity Framework-werkstromen
Entity Framework ontwikkelaars zijn afhankelijk van een van de volgende vier werkstromen toobuild toepassingen en tooensure persistentie voor toepassingsobjecten hello: 

* **Eerste (nieuwe Database) code**: Hallo EF developer maakt Hallo-model in de toepassingscode Hallo en EF genereert vervolgens Hallo database uit. 
* **Eerste (bestaande Database) code**: Hallo developer kunt EF Hallo toepassingscode voor Hallo model genereren vanuit een bestaande database.
* **Eerste model**: Hallo developer Hallo-model in Hallo EF designer maakt en EF maakt vervolgens Hallo database uit Hallo-model.
* **Eerste database**: Hallo developer EF tooinfer Hallo model vanuit een bestaande database tooling gebruikt. 

Alle deze methoden zijn afhankelijk van Hallo DbContext-klasse tootransparently beheren databaseverbindingen en -databaseschema voor een toepassing. Database maken van het uitvoeren van de bootstrap- en schema behandeld in meer detail verderop in document Hallo verschillende constructors op Hallo DbContext-basisklasse voor verschillende niveaus van controle over het maken van de verbinding toestaan. Uitdagingen ontstaan voornamelijk uit Hallo feit dat de polygoonring Hallo database verbinding management via EF met mogelijkheden voor verbinding Hallo Hallo gegevens afhankelijke routeringsinterfaces opgegeven door Hallo-clientbibliotheek voor elastische database. 

## <a name="elastic-database-tools-assumptions"></a>Veronderstellingen voor elastische database-hulpprogramma 's
Zie voor definities van de termijn [verklarende woordenlijst hulpprogramma's van elastische Database](sql-database-elastic-scale-glossary.md).

Met de clientbibliotheek voor elastische databases definiëren u partities van de toepassingsgegevens aangeroepen shardlets. Shardlets worden geïdentificeerd door een sharding-sleutel en zijn toegewezen toospecific databases. Een toepassing kan zo veel databases zo nodig hebt en distribueer Hallo shardlets tooprovide voldoende capaciteit of prestaties gegeven van de huidige zakelijke vereisten. Hallo-toewijzing van sharding sleutelwaarden toohello databases wordt opgeslagen in een shard-toewijzing zoals opgegeven door Hallo elastische databaseclient API's. We noemen deze mogelijkheid **Shard kaart Management**, of SMM kortweg. Hallo shard kaart fungeert ook als Hallo broker databaseverbindingen voor aanvragen die een sharding-sleutel bevatten. We verwijzen toothis mogelijkheden als **gegevensafhankelijke routering**. 

Hallo shard-toewijzing manager beveiligt gebruikers tegen inconsistente weergaven in shardlet gegevens die optreden kunnen wanneer de gelijktijdige shardlet management bewerkingen (zoals het verplaatsen van gegevens uit één shard tooanother) plaatsvinden. toodo Hallo dus shard-kaarten die worden beheerd door Hallo bibliotheek broker Hallo database clientverbindingen voor een toepassing. Hierdoor kan Hallo shard kaart functionaliteit tooautomatically kill een databaseverbinding wanneer shard-beheerbewerkingen kunnen invloed hebben op Hallo shardlet die Hallo verbinding is gemaakt. Deze aanpak moet toointegrate met enkele van de EF-functionaliteit, zoals het maken van nieuwe verbindingen van een bestaande één toocheck database bestaan. In het algemeen onze observatie is dat Hallo standaard DbContext constructors werken alleen op betrouwbare wijze voor gesloten databaseverbindingen die veilig kunnen worden gekloond voor EF werk. Hallo ontwerpprincipe van elastische database is in plaats daarvan tooonly broker geopend verbindingen. Een misschien denkt dat het sluiten van een verbinding die door de clientbibliotheek Hallo brokered voordat het wordt over toohello EF DbContext dit probleem mogelijk oplossen. Hallo-verbinding wordt gesloten en vertrouwen op EF toore-open het, foregoes een echter Hallo validatie en consistentie controles uitgevoerd door het Hallo-bibliotheek. Hallo migraties functionaliteit in EF, gebruikt echter deze verbindingen toomanage Hallo onderliggende databaseschema op een manier die transparant toohello toepassing is. In het ideale geval zouden we tooretain, zoals en alle deze mogelijkheden van zowel Hallo-clientbibliotheek voor elastische database als EF in Hallo combineren dezelfde toepassing. Hallo volgende hoofdstuk beschrijft uitgebreid deze eigenschappen en de vereisten in meer detail. 

## <a name="requirements"></a>Vereisten
Als u werkt met Hallo-clientbibliotheek voor elastische database en Entity Framework-API's, willen we tooretain Hallo volgende eigenschappen: 

* **Scale-out**: tooadd of verwijder databases van de gegevenslaag Hallo van shard toepassing hello die nodig zijn voor Hallo capaciteit eisen van de toepassing hello. Dit betekent dat de controle over Hallo Hallo maken en verwijderen van databases en het gebruik Hallo elastische database shard kaart manager-API's toomanage-databases en toewijzingen van shardlets. 
* **Consistentie**: toepassing hello veiligheidsmaatregelen sharding en maakt gebruik van gegevens afhankelijke routering mogelijkheden van de clientbibliotheek Hallo Hallo. tooavoid beschadigd of verkeerd queryresultaten verbindingen zijn brokered via Hallo shard-toewijzing manager. Dit houdt ook validatie en consistentie.
* **Eerste code**: tooretain Hallo gemak van de EF code eerste paradigma. In de Code First klassen in de toepassing hello transparant zijn toegewezen toohello onderliggende databasestructuren. Hallo-toepassingscode communiceert met DbSets die de meeste aspecten die zijn betrokken bij de verwerking van de database onderliggende hello maskeren.
* **Schema**: Entity Framework initiële database schema maken en latere schema evolutie via migraties worden verwerkt. Als deze mogelijkheden aanhoudt, is het eenvoudig als Hallo gegevens ontwikkeld aanpassing van uw app. 

Hallo volgende hulp ontvangt de instructie hoe toosatisfy deze vereisten voor Code First-toepassingen met hulpprogramma's voor elastische database. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>Gegevens afhankelijke EF DbContext-routering
Databaseverbindingen met Entity Framework worden meestal beheerd via subklassen van **DbContext**. Deze subklassen maken die zijn afgeleid van **DbContext**. U definieert uw **DbSets** die Hallo een back-database verzamelingen van CLR-objecten voor uw toepassing implementeren. In de context van de Hallo van gegevensafhankelijke routering, kunnen we enkele nuttige eigenschappen die niet noodzakelijkerwijs voor andere EF code eerste toepassingsscenario's bewaart identificeren: 

* Hallo-database bestaat al en is geregistreerd in Hallo elastische database shard-toewijzing. 
* Hallo-schema van de toepassing hello is al geïmplementeerde toohello database (Zie hieronder). 
* Gegevensafhankelijke routering verbindingen toohello database zijn geleverd door Hallo shard-toewijzing. 

toointegrate **DbContexts** met gegevensafhankelijke routering voor scale-out:

1. De fysieke databaseverbindingen via Hallo elastische database clientinterfaces van Hallo shard kaart manager maken 
2. Hallo-verbinding met de Hallo teruglopen **DbContext** subklasse
3. Hallo verbinding omlaag binnenkomen Hallo **DbContext** klassen tooensure Hallo verwerking Hallo EF-zijde ook gebeurt baseren. 

Hallo volgende codevoorbeeld ziet u deze methode. (Deze code is ook in Visual Studio-project begeleidende Hallo)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>Belangrijkste punten
* Een nieuwe constructor vervangt de standaardconstructor Hallo in Hallo DbContext-subklasse 
* nieuwe Hallo-constructor heeft Hallo argumenten die vereist zijn voor het afhankelijke doorsturen van gegevens via de clientbibliotheek voor elastische database:
  
  * Hallo shard-toewijzing tooaccess Hallo gegevensafhankelijke routeringsinterfaces,
  * Hallo sharding key tooidentify hello shardlet
  * een verbindingsreeks met het Hallo-referenties voor Hallo gegevensafhankelijke routering verbinding toohello shard. 
* Hallo aanroep toohello basisklassenconstructor werkt een detour in een statische methode waarmee alle Hallo stappen nodig voor het doorsturen van afhankelijk zijn van gegevens. 
  
  * Hallo OpenConnectionForKey aanroep van Hallo elastische database clientinterfaces wordt gebruikt op Hallo shard kaart tooestablish een open verbinding.
  * Hallo shard-toewijzing maakt Hallo open verbinding toohello shard die Hallo shardlet voor Hallo opgegeven sharding-sleutel bevat.
  * Deze verbinding openen wordt back toohello basisklassenconstructor van DbContext tooindicate dat deze verbinding gebruikt door EF in plaats van EF automatisch maken van een nieuwe verbinding laten toobe is doorgegeven. Deze manier Hallo verbinding zijn gelabeld door Hallo elastische databaseclient API zodat zij consistentie onder beheerbewerkingen shard-toewijzing kunt waarborgen.

Gebruik de nieuwe constructor Hallo voor uw DbContext-subklasse in plaats van de standaardconstructor Hallo in uw code. Hier volgt een voorbeeld: 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

nieuwe constructor Hallo opent Hallo verbinding toohello shard dat Hallo-gegevens voor Hallo shardlet geïdentificeerd door de waarde van Hallo bevat **tenantid1**. Hallo-code in Hallo **met** blok blijft ongewijzigd tooaccess hello **DbSet** voor blogs met EF op Hallo shard voor **tenantid1**. Hiermee wijzigt u semantiek voor Hallo-code in Hallo met blok dat alle databasebewerkingen nu worden binnen het bereik van één shard toohello waar **tenantid1** wordt bewaard. Bijvoorbeeld, een LINQ-query via Hallo blogs **DbSet** zou blogs opgeslagen op de huidige shard Hallo alleen worden geretourneerd, maar niet Hallo zijn opgeslagen op andere shards.  

#### <a name="transient-faults-handling"></a>Tijdelijke fouten verwerken
Hallo Microsoft Patterns en procedures in een team gepubliceerde Hallo [Hallo tijdelijke fout afhandeling van Application Block](https://msdn.microsoft.com/library/dn440719.aspx). Hallo tapewisselaar wordt gebruikt met de clientbibliotheek elastisch schalen in combinatie met EF. Er echter voor zorgen dat een tijdelijke uitzondering tooa plaats waar we dat die nieuwe constructor Hallo na een tijdelijke fout wordt gebruikt retourneert kunnen zodat elke nieuwe verbindingspoging wordt gemaakt met behulp van Hallo constructors die we hebt toegepast. Anders wordt een juiste shard kan niet worden gegarandeerd, en er zijn geen garanties Hallo verbinding verbinding toohello bijgehouden als wijzigingen optreden toohello shard-toewijzing. 

Hallo volgende codevoorbeeld ziet u hoe een SQL-beleid voor opnieuw proberen kan worden gebruikt om Hallo nieuwe **DbContext** subklasse constructors: 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** in Hallo bovenstaande code wordt gedefinieerd als een **SqlDatabaseTransientErrorDetectionStrategy** met een aantal nieuwe pogingen van 10 en 5 seconden wachttijd tussen nieuwe pogingen. Deze aanpak is vergelijkbaar toohello richtlijnen voor EF en transacties gebruiker gestart (Zie [beperkingen in de uitvoering van strategieën opnieuw uit te voeren (EF6 en hoger)](http://msdn.microsoft.com/data/dn307226). Beide situaties vereisen dat programma van de toepassing hello bepaalt Hallo bereik toowhich Hallo tijdelijke uitzondering retourneert: tooeither Open Hallo transactie of (zoals) opnieuw wilt maken Hallo context van de juiste constructor Hallo dat wordt gebruikt Hallo elastische database clientbibliotheek.

Hallo nodig toocontrol waar tijdelijke uitzonderingen in beslag terug in bereik ook uitsluit Hallo gebruik van de ingebouwde Hallo **SqlAzureExecutionStrategy** die wordt geleverd met EF. **SqlAzureExecutionStrategy** zou opnieuw een verbinding openen maar niet **OpenConnectionForKey** en daarom omzeilen Hallo validaties die wordt uitgevoerd als onderdeel van Hallo **OpenConnectionForKey** aanroepen. In plaats daarvan Hallo voorbeeldcode maakt gebruik van Hallo ingebouwde **DefaultExecutionStrategy** die wordt geleverd met EF. In plaats van te**SqlAzureExecutionStrategy**, deze correct werkt in combinatie met Hallo-beleid voor opnieuw proberen van afhandeling van tijdelijke fout. Hallo-uitvoeringsbeleid is ingesteld in Hallo **ElasticScaleDbConfiguration** klasse. Opmerking dat we niet toouse besloten **DefaultSqlExecutionStrategy** omdat er wordt verwezen naar toouse **SqlAzureExecutionStrategy** als tijdelijke uitzonderingen optreden - die zouden kunnen leiden toowrong gedrag zoals besproken. Zie voor meer informatie over Hallo verschillende retry-beleid en de EF [Verbindingstolerantie in EF](http://msdn.microsoft.com/data/dn456835.aspx).     

#### <a name="constructor-rewrites"></a>Constructor regeneraties
Hallo codevoorbeelden bovenstaande illustratie Hallo standaard constructor herschrijft vereist is voor uw toepassing in volgorde toouse afhankelijk van de gegevens routering met Hallo Entity Framework. Hallo tabel generaliseert deze benadering tooother constructors. 

| Huidige Constructor | Herschreven Constructor voor gegevens | Base-Constructor | Opmerkingen |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext (ShardMap, TKey) |DbContext (DbConnection, bool) |Hallo verbinding moet een functie van Hallo shard-toewijzing en Hallo gegevensafhankelijke routering sleutel toobe. U moet tooby pass automatisch verbinding maken met EF en in plaats daarvan Hallo shard kaart toobroker Hallo verbinding gebruiken. |
| MyContext(string) |ElasticScaleContext (ShardMap, TKey) |DbContext (DbConnection, bool) |Hallo-verbinding is een functie van Hallo shard-toewijzing en Hallo gegevensafhankelijke routering sleutel. Een vaste databaserol of verbindingstekenreeks, werken niet als ze validatie omzeilen door Hallo shard-toewijzing. |
| MyContext(DbCompiledModel) |ElasticScaleContext (ShardMap, TKey, DbCompiledModel) |DbContext (DbConnection, DbCompiledModel, bool) |voor de shard-toewijzing en sharding-sleutel met de Hallo model opgegeven gegeven Hallo Hallo verbinding gemaakt. Hallo gecompileerde model worden op basis c'tor toohello doorgegeven. |
| MyContext (DbConnection, bool) |ElasticScaleContext (ShardMap, TKey, bool) |DbContext (DbConnection, bool) |Hallo verbinding moet toobe afgeleid van Hallo shard-toewijzing en het Hallo-sleutel. Deze kan niet worden opgegeven als invoer (tenzij deze invoer is al Hallo shard-toewijzing en Hallo sleutel). Hallo Booleaanse waarde doorgegeven. |
| MyContext (string, DbCompiledModel) |ElasticScaleContext (ShardMap, TKey, DbCompiledModel) |DbContext (DbConnection, DbCompiledModel, bool) |Hallo verbinding moet toobe afgeleid van Hallo shard-toewijzing en het Hallo-sleutel. Deze kan niet worden opgegeven als invoer (tenzij deze invoer is Hallo shard-toewijzing en Hallo sleutel). Hallo gecompileerde model doorgegeven. |
| MyContext (ObjectContext, bool) |ElasticScaleContext (ShardMap TKey, ObjectContext, bool) |DbContext (ObjectContext, bool) |nieuwe Hallo-constructor moet tooensure die een verbinding in Hallo die ObjectContext als invoer doorgegeven omgeleid tooa verbinding beheerd door de elastische Schaalfunctionaliteit is. Een gedetailleerde discussie over ObjectContexts valt buiten bereik Hallo van dit document. |
| MyContext (DbConnection, DbCompiledModel, bool) |ElasticScaleContext (ShardMap TKey, DbCompiledModel, bool) |DbContext (DbConnection, DbCompiledModel, bool); |Hallo verbinding moet toobe afgeleid van Hallo shard-toewijzing en het Hallo-sleutel. Hallo verbinding kan niet worden opgegeven als invoer (tenzij deze invoer is al Hallo shard-toewijzing en Hallo sleutel). Model en Booleaanse waarde doorgegeven toohello basisklassenconstructor. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>Implementatie van de shard-schema via EF-migraties
Automatische Schemabeheer is voor uw gemak geleverd door Hallo Entity Framework. In de context van de Hallo van toepassingen met elastische database-hulpprogramma's, willen we tooretain deze mogelijkheid tooautomatically inrichten Hallo schema gemaakt toonewly shards wanneer databases toohello shard-toepassing worden toegevoegd. Hallo primaire gebruiksvoorbeeld is tooincrease capaciteit op Hallo gegevenslaag voor shard-toepassingen met EF. Afhankelijk van de EF mogelijkheden voor het Schemabeheer van beperkt Hallo database beheer inspanning met een gebouwd op EF shard-toepassing. 

Schema-implementatie via EF migraties werkt het beste op **nog niet gelezen verbindingen**. Dit is daarentegen toohello scenario voor het gegevensafhankelijke routering die afhankelijk van Hallo geopend verbinding geleverd door Hallo elastische databaseclient-API is. Een ander verschil is Hallo consistentie vereiste: tijdens het wenselijk tooensure consistentie voor alle gegevensafhankelijke routering verbindingen tooprotect tegen manipulatie van gelijktijdige shard-kaart, het is niet een probleem met het initiële schema implementatie tooa nieuwe database die nog niet is geregistreerd in Hallo shard-kaart, en nog niet is toegewezen toohold shardlets heeft. We kunnen daarom zijn afhankelijk van de reguliere databaseverbindingen voor dit scenario's, zoals het tegengestelde toodata-afhankelijke routering.  

Dit leidt tooan benadering waarbij schema implementatie via EF migraties met registratie van de nieuwe database Hallo Hallo nauw is gekoppeld als een shard in van de toepassing hello shard-toewijzing. Dit is afhankelijk van Hallo volgende vereisten: 

* Hallo database is al gemaakt. 
* Hallo-database is leeg: deze bevat geen gebruikersschema en geen gebruikersgegevens.
* Hallo-database kan niet nog toegankelijk via Hallo elastische databaseclient-API's voor het doorsturen van afhankelijk zijn van gegevens. 

Met deze vereisten is voldaan, maken we een gewone niet is geopend **SqlConnection** tookick uit EF migraties voor schema-implementatie. Hallo volgende codevoorbeeld ziet u deze methode. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


Dit voorbeeld wordt de methode Hallo **RegisterNewShard** dat registers shard in Hallo shard-kaart, Hallo Hallo schema via EF migraties implementeert en een toewijzing van een sleutel toohello sharding shard bewaart. Is afhankelijk van een constructor Hallo **DbContext** subklasse (**ElasticScaleContext** in Hallo steekproef) waarmee een SQL-verbindingsreeks als invoer. Hallo-code van deze constructor is ongecompliceerde, als het volgende voorbeeld ziet u Hallo: 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Mogelijk gebruikt een versie van Hallo-constructor die zijn overgenomen van de basisklasse Hallo Hallo. Maar Hallo code behoeften tooensure die standaard initialisatiefunctie voor EF Hallo wordt gebruikt om verbinding te maken. Daarom Hallo korte detour Hallo aan de statische methode voordat u aan Hallo basisklassenconstructor met Hallo-verbindingsreeks. Houd er rekening mee dat in een andere app-domein of het proces tooensure Hallo initialisatiefunctie-instellingen voor EF niet conflicteren Hallo registratie van shards moet worden uitgevoerd. 

## <a name="limitations"></a>Beperkingen
Hallo-methoden die worden beschreven in dit document leidt tot een aantal beperkingen: 

* EF-toepassingen die gebruikmaken van **LocalDb** moet eerst toomigrate tooa reguliere SQL Server-database voordat u de clientbibliotheek voor elastische database. Een toepassing via sharding uitbreiden met elastisch schalen is niet mogelijk met **LocalDb**. Houd er rekening mee dat ontwikkeling nog steeds kunt gebruiken **LocalDb**. 
* Alle wijzigingen toohello toepassingen die impliceren schemawijzigingen database moet toogo via EF migraties op alle shards. Hallo voorbeeldcode voor dit document biedt niet laten zien hoe toodo dit. Overweeg het gebruik van de Database bijwerken met een parameter ConnectionString tooiterate via alle shards; of extract Hallo T-SQL-script voor Hallo in behandeling zijnde migratie met behulp van de Update-Database met Hallo - Script optie en toepassing hello T-SQL-script tooyour shards.  
* Een aanvraag opgegeven, wordt ervan uitgegaan dat alle van de verwerking van de database zich in een enkel shard aangeduid met de Hallo sharding sleutel van het Hallo-aanvraag. Echter, deze aanname niet altijd bijhoudt true. Bijvoorbeeld, wanneer is het niet mogelijk toomake een sharding-sleutel beschikbaar. tooaddress deze, Hallo clientbibliotheek biedt Hallo **MultiShardQuery** klasse die een abstractie van de verbinding voor het uitvoeren van query's via meerdere shards implementeert. Learning toouse hello **MultiShardQuery** in combinatie met EF valt buiten bereik Hallo van dit document

## <a name="conclusion"></a>Conclusie
Hallo stappen die worden beschreven in dit document, EF toepassingen kunnen gebruikmaken van Hallo elastische database clientbibliotheek van mogelijkheden voor gegevens afhankelijk routering door een constructors Hallo refactoring **DbContext** subklassen gebruikt in Hallo EF de toepassing. Deze limieten Hallo wijzigingen vereist toothose plaatsen waar **DbContext** klassen bestaan al. EF-toepassingen kunnen bovendien toobenefit uit schema voor automatische implementatie gaan door het combineren van Hallo stappen die Hallo nodig EF migraties met Hallo registratie van nieuwe shards en toewijzingen in de shard-toewijzing Hallo aanroepen. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
