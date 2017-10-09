---
title: aaaMulti-tenant-toepassingen met elastische database-hulpprogramma's en beveiliging
description: Meer informatie over hoe toouse elastische database hulpprogramma's samen met rijniveau beveiliging toobuild een toepassing met een hoge mate schaalbaar gegevenslaag op Azure SQL Database die ondersteuning biedt voor meerdere tenants shards.
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>Multitenant-toepassingen met elastische database-hulpprogramma's en beveiliging
[Hulpprogramma's voor elastische database](sql-database-elastic-scale-get-started.md) en [rijniveau beveiliging (RLS)](https://msdn.microsoft.com/library/dn765131) bieden een set krachtige mogelijkheden voor het flexibel en efficiënt schalen van de gegevenslaag Hallo van een toepassing met meerdere tenants met Azure SQL Database. Zie [ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) voor meer informatie. 

Dit artikel wordt beschreven hoe toouse deze technologieën bij elkaar toobuild een toepassing met een hoge mate schaalbaar gegevenslaag die ondersteuning biedt voor meerdere tenants shards, met behulp van **ADO.NET SqlClient** en/of **Entity Framework**.  

* **Hulpprogramma's voor elastische database** kunnen ontwikkelaars tooscale u Hallo gegevenslaag van een toepassing via industriestandaard sharding procedures met behulp van een set van .NET-bibliotheken en sjablonen voor Azure-service. Beheren shards met het gebruik van Hallo clientbibliotheek voor elastische Database kunt automatiseren en veel van Hallo infrastructurele taken meestal gekoppeld aan sharding stroomlijnen. 
* **Beveiliging op gebruikersniveau rij** kunnen ontwikkelaars toostore gegevens voor meerdere tenants in Hallo dezelfde database gebruiken met security-beleid toofilter rijen die geen deel uitmaken van een query uit te voeren toohello-tenant. Logica van de toegang voor beveiliging op Rijniveau in Hallo-database, centraliseren in plaats daarvan groeit dan in de toepassing hello, vereenvoudigt u het onderhoud en vermindert risico op Hallo van fout als een toepassing codebase. 

Samen met behulp van deze functies, een toepassing kunt profiteren van kosten besparen en efficiëntie toeneemt door gegevens op te slaan voor meerdere tenants in Hallo dezelfde shard-database. Bij Hallo heeft hetzelfde moment, een toepassing nog steeds Hallo flexibiliteit toooffer geïsoleerd, één tenant shards voor 'premium' tenants die strenger prestaties garanties nodig omdat multitenant shards komen niet gegarandeerd dat gelijk resource verdeling van tenants.  

Kort gezegd: Hallo elastische database-clientbibliotheek van [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) API's automatisch verbinding maken met hun sharding-sleutel (doorgaans een ' TenantId') van tenants toohello juiste shard-database. Eenmaal zijn verbonden, wordt een beveiligingsbeleid RLS binnen Hallo database zorgt ervoor dat tenants alleen toegang tot rijen die hun TenantId bevatten. Ervan wordt uitgegaan dat alle tabellen bevatten een TenantId kolom tooindicate welke rijen tooeach tenant behoren. 

![Blog app-architectuur][1]

## <a name="download-hello-sample-project"></a>Hallo-voorbeeldproject downloaden
### <a name="prerequisites"></a>Vereisten
* Gebruik Visual Studio (2012 of hoger) 
* Drie Azure SQL-Databases maken 
* Download voorbeeldproject: [elastische DB-hulpprogramma's voor Azure SQL - Multitenant-Shards](http://go.microsoft.com/?linkid=9888163)
  * Vul Hallo-informatie voor uw databases aan begin Hallo van **Program.cs** 

Dit project breidt een beschreven in Hallo [elastische DB-hulpprogramma's voor Azure SQL - Entity Framework integratie](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) door ondersteuning voor meerdere tenants shard databases toe te voegen. Dit is een eenvoudige consoletoepassing voor het maken van blogs en berichten, met vier tenants en twee multitenant shard-databases zoals geïllustreerd in Hallo hierboven diagram gebaseerd. 

Toepassing bouwen en uitvoeren Hallo. Dit wordt bootstrap Hallo elastische database extra shard kaart manager en Voer Hallo tests te volgen: 

1. Met behulp van Entity Framework en LINQ, een nieuw blog maken en vervolgens alle blogs voor elke tenant weergeven
2. Alle blogs voor een tenant met behulp van ADO.NET SqlClient weergeven
3. Probeer tooinsert een blog voor Hallo verkeerde tenant tooverify waarvoor een fout is opgetreden  

U ziet dat omdat RLS nog niet is ingeschakeld in de shard-databases hello, elk van deze tests een probleem opgetreden blijkt: tenants kunnen toosee blogs die geen deel van toothem uitmaken zijn en toepassing hello niet wordt verhinderd invoegen van een blog voor Hallo verkeerde tenant. Hallo rest van dit artikel wordt beschreven hoe tooresolve deze problemen door af te dwingen voor de tenantsleutel isolatie voor beveiliging op Rijniveau. Er zijn twee stappen: 

1. **Toepassingslaag**: Hallo toepassingscode wijzigen tooalways set Hallo huidige TenantId in Hallo SESSION_CONTEXT na het openen van een verbinding. Hallo-voorbeeldproject heeft dit al gedaan. 
2. **Gegevenslaag**: maken van een beveiligingsbeleid RLS in elke shard database toofilter rijen op basis van Hallo TenantId in SESSION_CONTEXT opgeslagen. U moet de toodo dit voor elk van de shard-databases, anders rijen in een multitenant shards worden niet gefilterd. 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a>Stap 1) toepassingslaag: TenantId in Hallo SESSION_CONTEXT instellen
Nadat u verbinding probeert te maken tooa shard-database met behulp van Hallo elastische database clientbibliotheek van gegevens die afhankelijke routering API's, de toepassing hello nog moet tootell Hallo database wordt welke TenantId die verbinding gebruikt zodat een beveiligingsbeleid RLS rijen kunt uitfilteren behoren tooother tenants. aanbevolen manier toopass deze informatie is Hallo toostore huidige TenantId voor die verbinding in Hallo Hallo [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx). (Opmerking: U kunt ook [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), maar SESSION_CONTEXT is een betere optie, omdat deze eenvoudiger toouse is, NULL standaard retourneert en sleutel-waardeparen ondersteunt.)

### <a name="entity-framework"></a>Entity Framework
Voor toepassingen met behulp van Entity Framework, is de beste aanpak Hallo tooset hello SESSION_CONTEXT binnen Hallo ElasticScaleContext overschrijven die wordt beschreven in [gegevensafhankelijke routering met EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext). Voordat u terugkeert Hallo verbinding geleverd door het gegevensafhankelijke routering, maken en uitvoeren van een SqlCommand die 'TenantId' ingesteld in Hallo SESSION_CONTEXT toohello shardingKey opgegeven voor die verbinding. Op deze manier hoeft u alleen toowrite code zodra tooset Hallo SESSION_CONTEXT. 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

Nu Hallo SESSION_CONTEXT automatisch ingesteld met de opgegeven Hallo TenantId wanneer ElasticScaleContext wordt opgeroepen: 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a>ADO.NET SqlClient
Voor toepassingen die gebruikmaken van ADO.NET-SqlClient hello aanbevolen benadering toocreate is een functie wrapper rond ShardMap.OpenConnectionForKey() die automatisch wordt ingesteld 'TenantId' in hello SESSION_CONTEXT toohello TenantId corrigeren voordat het retourneren van een de verbinding. tooensure die SESSION_CONTEXT is altijd ingesteld, moet u alleen verbindingen met deze functie wrapper openen.

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a>Stap 2) gegevens laag: rijniveau beveiligingsbeleid maken
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a>Maak een beveiliging beleid toofilter Hallo rijen die elke tenant toegang heeft tot
Nu dat de toepassing hello configureert SESSION_CONTEXT met huidige TenantId Hallo voordat de query wordt uitgevoerd, een beveiligingsbeleid RLS kunt query's filteren en rijen met een andere TenantId uitsluiten.  

RLS is geïmplementeerd in T-SQL: een door de gebruiker gedefinieerde functie Hallo toegang logica wordt gedefinieerd en een beveiligingsbeleid voor deze functie tooany aantal tabellen wordt gebonden. Voor dit project Hallo-functie wordt gewoon Controleer of Hallo toepassing (in plaats een andere SQL-gebruiker) verbonden toohello database, en die Hallo 'TenantId' die is opgeslagen in Hallo SESSION_CONTEXT komt overeen met de Hallo TenantId van een bepaalde rij. Een filterpredicaat kunt rijen die voldoen aan deze voorwaarden toopass via Hallo filter voor SELECT-, UPDATE- en DELETE-query's. en een block-predicaat wordt voorkomen dat de rijen die strijdig zijn met deze voorwaarden niet kan worden ingevoegd of bijgewerkt. Als SESSION_CONTEXT niet is ingesteld, wordt het geretourneerd dat null en geen rijen zijn zichtbaar is of kan het toobe ingevoegd. 

tooenable RLS, Hallo volgende T-SQL op alle shards met behulp van de Visual Studio (SSDT), SSMS, uitvoeren of PowerShell-script is opgenomen in het project Hallo hello (of als u [elastische Database taken](sql-database-elastic-jobs-overview.md), kunt u tooautomate uitvoering deze T-SQL op alle shards): 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> Voor complexere projecten waarvoor tooadd Hallo predikaat op honderden tabellen, kunt u een helper opgeslagen procedure die genereert automatisch een beveiligingsbeleid toe te voegen een predicaat voor alle tabellen in een schema. Zie [toepassen beveiliging tooall tabellen - helper-script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).  
> 
> 

Als u Hallo voorbeeldtoepassing opnieuw uitvoert, wordt tenants kunnen toosee alleen rijen die deel uitmaken van toothem. Bovendien Hallo toepassing kan geen rijen die deel uitmaken van tootenants dan Hallo één momenteel verbonden toohello shard-database invoegen en zichtbare rijen toohave een andere tenant-id kan niet worden bijgewerkt. Als de toepassing hello toodo ofwel probeert, wordt een DbUpdateException verschijnt.

Als u een nieuwe tabel later op gewoon ALTER Hallo beveiligingsbeleid toevoegen en filter en block-predicaten op Hallo nieuwe tabel toevoegen: 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a>Standaard toevoegen beperkingen tooautomatically TenantId voor voegt vullen
U kunt een standaard plaatsen-beperking voor elke tabel tooautomatically vullen Hallo TenantId Hello waarde die momenteel zijn opgeslagen in SESSION_CONTEXT bij het invoegen van rijen. Bijvoorbeeld: 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

Hallo-toepassing heeft nu geen toospecify een TenantId nodig bij het invoegen van rijen: 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> Als u een default-beperkingen voor een Entity Framework-project gebruiken, is het raadzaam dat u Hallo TenantId kolom niet in uw EF-gegevensmodel opnemen. Dit komt doordat de Entity Framework-query's worden automatisch standaardwaarden die overschrijft Hallo default-beperkingen in T-SQL gemaakt die gebruikmaken van SESSION_CONTEXT opgeeft. toouse default-beperkingen in Hallo steekproef project, bijvoorbeeld, moet u TenantId verwijderen uit DataClasses.cs (en voer Add-migratie in Hallo Package Manager Console) en gebruik T-SQL-tooensure die Hallo veld is alleen beschikbaar in databasetabellen Hallo. Op deze manier EF wordt niet automatisch opgeeft onjuiste standaardwaarden bij het invoegen van gegevens. 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a>(Optioneel) Alle rijen van een 'beheerder' tooaccess inschakelen
Sommige toepassingen kunt toocreate een 'beheerder' wie toegang tot alle rijen, bijvoorbeeld, in volgorde tooenable rapportage over alle tenants in alle shards of tooperform gesplitste/Merge-bewerkingen op shards die betrekking hebben op bewegende tenant rijen tussen databases. tooenable, moet u een nieuwe SQL-gebruiker ('superuser' in dit voorbeeld) in elke shard-database maken. Hallo-beveiligingsbeleid met een nieuwe predicaatfunctie waarmee deze gebruiker tooaccess alle rijen wijzigt:

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a>Onderhoud
* **Toevoegen van nieuwe shards**: Hallo T-SQL-script tooenable RLS moet worden uitgevoerd op een nieuwe shards, anders query's in deze shards worden niet gefilterd.
* **Toevoegen van nieuwe tabellen**: U moet een filter toevoegen en predikaat toohello beveiligingsbeleid op alle shards blokkeren wanneer er een nieuwe tabel is gemaakt, anders query's op de nieuwe tabel Hallo worden niet gefilterd. Dit kan worden geautomatiseerd met behulp van een DDL-trigger, zoals beschreven in [toepassen beveiliging automatisch gemaakt van tabellen (blog) in toonewly](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).

## <a name="summary"></a>Samenvatting
Elastische database-hulpprogramma's en de beveiliging kunnen worden gebruikt samen tooscale uit de gegevenslaag van een toepassing met ondersteuning voor multitenant- en één tenant shards. Multitenant shards mag gebruikte toostore gegevens efficiënter (met name in gevallen waarin een groot aantal tenants slechts een paar rijen met gegevens hebben), tijdens één tenant shards mag gebruikte toosupport premium tenants met strengere prestaties en isolatie vereisten.  Zie voor meer informatie [beveiliging verwijzing](https://msdn.microsoft.com/library/dn765131). 

## <a name="additional-resources"></a>Aanvullende bronnen
* [Wat is een Azure elastische groep?](sql-database-elastic-pool.md)
* [Uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md)
* [Ontwerppatronen voor SaaS-toepassingen met meerdere tenants met behulp van Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Verificatie in multitenant-apps met Azure AD en OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [De toepassing Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>Vragen en Functieaanvragen
Voor vragen kunt contact toous op Hallo [SQL Database-forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) en voor functieaanvragen, deze toe te voegen toohello [forum met feedback van SQL-Database](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


