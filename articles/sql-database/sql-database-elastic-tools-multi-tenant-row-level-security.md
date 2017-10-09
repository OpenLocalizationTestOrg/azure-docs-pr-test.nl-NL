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
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="864b3-103">Multitenant-toepassingen met elastische database-hulpprogramma's en beveiliging</span><span class="sxs-lookup"><span data-stu-id="864b3-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="864b3-104">[Hulpprogramma's voor elastische database](sql-database-elastic-scale-get-started.md) en [rijniveau beveiliging (RLS)](https://msdn.microsoft.com/library/dn765131) bieden een set krachtige mogelijkheden voor het flexibel en efficiënt schalen van de gegevenslaag Hallo van een toepassing met meerdere tenants met Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="864b3-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="864b3-105">Zie [ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="864b3-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="864b3-106">Dit artikel wordt beschreven hoe toouse deze technologieën bij elkaar toobuild een toepassing met een hoge mate schaalbaar gegevenslaag die ondersteuning biedt voor meerdere tenants shards, met behulp van **ADO.NET SqlClient** en/of **Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="864b3-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="864b3-107">**Hulpprogramma's voor elastische database** kunnen ontwikkelaars tooscale u Hallo gegevenslaag van een toepassing via industriestandaard sharding procedures met behulp van een set van .NET-bibliotheken en sjablonen voor Azure-service.</span><span class="sxs-lookup"><span data-stu-id="864b3-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="864b3-108">Beheren shards met het gebruik van Hallo clientbibliotheek voor elastische Database kunt automatiseren en veel van Hallo infrastructurele taken meestal gekoppeld aan sharding stroomlijnen.</span><span class="sxs-lookup"><span data-stu-id="864b3-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="864b3-109">**Beveiliging op gebruikersniveau rij** kunnen ontwikkelaars toostore gegevens voor meerdere tenants in Hallo dezelfde database gebruiken met security-beleid toofilter rijen die geen deel uitmaken van een query uit te voeren toohello-tenant.</span><span class="sxs-lookup"><span data-stu-id="864b3-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="864b3-110">Logica van de toegang voor beveiliging op Rijniveau in Hallo-database, centraliseren in plaats daarvan groeit dan in de toepassing hello, vereenvoudigt u het onderhoud en vermindert risico op Hallo van fout als een toepassing codebase.</span><span class="sxs-lookup"><span data-stu-id="864b3-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="864b3-111">Samen met behulp van deze functies, een toepassing kunt profiteren van kosten besparen en efficiëntie toeneemt door gegevens op te slaan voor meerdere tenants in Hallo dezelfde shard-database.</span><span class="sxs-lookup"><span data-stu-id="864b3-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="864b3-112">Bij Hallo heeft hetzelfde moment, een toepassing nog steeds Hallo flexibiliteit toooffer geïsoleerd, één tenant shards voor 'premium' tenants die strenger prestaties garanties nodig omdat multitenant shards komen niet gegarandeerd dat gelijk resource verdeling van tenants.</span><span class="sxs-lookup"><span data-stu-id="864b3-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="864b3-113">Kort gezegd: Hallo elastische database-clientbibliotheek van [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) API's automatisch verbinding maken met hun sharding-sleutel (doorgaans een ' TenantId') van tenants toohello juiste shard-database.</span><span class="sxs-lookup"><span data-stu-id="864b3-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="864b3-114">Eenmaal zijn verbonden, wordt een beveiligingsbeleid RLS binnen Hallo database zorgt ervoor dat tenants alleen toegang tot rijen die hun TenantId bevatten.</span><span class="sxs-lookup"><span data-stu-id="864b3-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="864b3-115">Ervan wordt uitgegaan dat alle tabellen bevatten een TenantId kolom tooindicate welke rijen tooeach tenant behoren.</span><span class="sxs-lookup"><span data-stu-id="864b3-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![Blog app-architectuur][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="864b3-117">Hallo-voorbeeldproject downloaden</span><span class="sxs-lookup"><span data-stu-id="864b3-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="864b3-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="864b3-118">Prerequisites</span></span>
* <span data-ttu-id="864b3-119">Gebruik Visual Studio (2012 of hoger)</span><span class="sxs-lookup"><span data-stu-id="864b3-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="864b3-120">Drie Azure SQL-Databases maken</span><span class="sxs-lookup"><span data-stu-id="864b3-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="864b3-121">Download voorbeeldproject: [elastische DB-hulpprogramma's voor Azure SQL - Multitenant-Shards](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="864b3-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="864b3-122">Vul Hallo-informatie voor uw databases aan begin Hallo van **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="864b3-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="864b3-123">Dit project breidt een beschreven in Hallo [elastische DB-hulpprogramma's voor Azure SQL - Entity Framework integratie](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) door ondersteuning voor meerdere tenants shard databases toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="864b3-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="864b3-124">Dit is een eenvoudige consoletoepassing voor het maken van blogs en berichten, met vier tenants en twee multitenant shard-databases zoals geïllustreerd in Hallo hierboven diagram gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="864b3-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="864b3-125">Toepassing bouwen en uitvoeren Hallo.</span><span class="sxs-lookup"><span data-stu-id="864b3-125">Build and run hello application.</span></span> <span data-ttu-id="864b3-126">Dit wordt bootstrap Hallo elastische database extra shard kaart manager en Voer Hallo tests te volgen:</span><span class="sxs-lookup"><span data-stu-id="864b3-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="864b3-127">Met behulp van Entity Framework en LINQ, een nieuw blog maken en vervolgens alle blogs voor elke tenant weergeven</span><span class="sxs-lookup"><span data-stu-id="864b3-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="864b3-128">Alle blogs voor een tenant met behulp van ADO.NET SqlClient weergeven</span><span class="sxs-lookup"><span data-stu-id="864b3-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="864b3-129">Probeer tooinsert een blog voor Hallo verkeerde tenant tooverify waarvoor een fout is opgetreden</span><span class="sxs-lookup"><span data-stu-id="864b3-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="864b3-130">U ziet dat omdat RLS nog niet is ingeschakeld in de shard-databases hello, elk van deze tests een probleem opgetreden blijkt: tenants kunnen toosee blogs die geen deel van toothem uitmaken zijn en toepassing hello niet wordt verhinderd invoegen van een blog voor Hallo verkeerde tenant.</span><span class="sxs-lookup"><span data-stu-id="864b3-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="864b3-131">Hallo rest van dit artikel wordt beschreven hoe tooresolve deze problemen door af te dwingen voor de tenantsleutel isolatie voor beveiliging op Rijniveau.</span><span class="sxs-lookup"><span data-stu-id="864b3-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="864b3-132">Er zijn twee stappen:</span><span class="sxs-lookup"><span data-stu-id="864b3-132">There are two steps:</span></span> 

1. <span data-ttu-id="864b3-133">**Toepassingslaag**: Hallo toepassingscode wijzigen tooalways set Hallo huidige TenantId in Hallo SESSION_CONTEXT na het openen van een verbinding.</span><span class="sxs-lookup"><span data-stu-id="864b3-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="864b3-134">Hallo-voorbeeldproject heeft dit al gedaan.</span><span class="sxs-lookup"><span data-stu-id="864b3-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="864b3-135">**Gegevenslaag**: maken van een beveiligingsbeleid RLS in elke shard database toofilter rijen op basis van Hallo TenantId in SESSION_CONTEXT opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="864b3-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="864b3-136">U moet de toodo dit voor elk van de shard-databases, anders rijen in een multitenant shards worden niet gefilterd.</span><span class="sxs-lookup"><span data-stu-id="864b3-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="864b3-137">Stap 1) toepassingslaag: TenantId in Hallo SESSION_CONTEXT instellen</span><span class="sxs-lookup"><span data-stu-id="864b3-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="864b3-138">Nadat u verbinding probeert te maken tooa shard-database met behulp van Hallo elastische database clientbibliotheek van gegevens die afhankelijke routering API's, de toepassing hello nog moet tootell Hallo database wordt welke TenantId die verbinding gebruikt zodat een beveiligingsbeleid RLS rijen kunt uitfilteren behoren tooother tenants.</span><span class="sxs-lookup"><span data-stu-id="864b3-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="864b3-139">aanbevolen manier toopass deze informatie is Hallo toostore huidige TenantId voor die verbinding in Hallo Hallo [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="864b3-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="864b3-140">(Opmerking: U kunt ook [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), maar SESSION_CONTEXT is een betere optie, omdat deze eenvoudiger toouse is, NULL standaard retourneert en sleutel-waardeparen ondersteunt.)</span><span class="sxs-lookup"><span data-stu-id="864b3-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="864b3-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="864b3-141">Entity Framework</span></span>
<span data-ttu-id="864b3-142">Voor toepassingen met behulp van Entity Framework, is de beste aanpak Hallo tooset hello SESSION_CONTEXT binnen Hallo ElasticScaleContext overschrijven die wordt beschreven in [gegevensafhankelijke routering met EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="864b3-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="864b3-143">Voordat u terugkeert Hallo verbinding geleverd door het gegevensafhankelijke routering, maken en uitvoeren van een SqlCommand die 'TenantId' ingesteld in Hallo SESSION_CONTEXT toohello shardingKey opgegeven voor die verbinding.</span><span class="sxs-lookup"><span data-stu-id="864b3-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="864b3-144">Op deze manier hoeft u alleen toowrite code zodra tooset Hallo SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="864b3-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

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

<span data-ttu-id="864b3-145">Nu Hallo SESSION_CONTEXT automatisch ingesteld met de opgegeven Hallo TenantId wanneer ElasticScaleContext wordt opgeroepen:</span><span class="sxs-lookup"><span data-stu-id="864b3-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="864b3-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="864b3-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="864b3-147">Voor toepassingen die gebruikmaken van ADO.NET-SqlClient hello aanbevolen benadering toocreate is een functie wrapper rond ShardMap.OpenConnectionForKey() die automatisch wordt ingesteld 'TenantId' in hello SESSION_CONTEXT toohello TenantId corrigeren voordat het retourneren van een de verbinding.</span><span class="sxs-lookup"><span data-stu-id="864b3-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="864b3-148">tooensure die SESSION_CONTEXT is altijd ingesteld, moet u alleen verbindingen met deze functie wrapper openen.</span><span class="sxs-lookup"><span data-stu-id="864b3-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="864b3-149">Stap 2) gegevens laag: rijniveau beveiligingsbeleid maken</span><span class="sxs-lookup"><span data-stu-id="864b3-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="864b3-150">Maak een beveiliging beleid toofilter Hallo rijen die elke tenant toegang heeft tot</span><span class="sxs-lookup"><span data-stu-id="864b3-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="864b3-151">Nu dat de toepassing hello configureert SESSION_CONTEXT met huidige TenantId Hallo voordat de query wordt uitgevoerd, een beveiligingsbeleid RLS kunt query's filteren en rijen met een andere TenantId uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="864b3-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="864b3-152">RLS is geïmplementeerd in T-SQL: een door de gebruiker gedefinieerde functie Hallo toegang logica wordt gedefinieerd en een beveiligingsbeleid voor deze functie tooany aantal tabellen wordt gebonden.</span><span class="sxs-lookup"><span data-stu-id="864b3-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="864b3-153">Voor dit project Hallo-functie wordt gewoon Controleer of Hallo toepassing (in plaats een andere SQL-gebruiker) verbonden toohello database, en die Hallo 'TenantId' die is opgeslagen in Hallo SESSION_CONTEXT komt overeen met de Hallo TenantId van een bepaalde rij.</span><span class="sxs-lookup"><span data-stu-id="864b3-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="864b3-154">Een filterpredicaat kunt rijen die voldoen aan deze voorwaarden toopass via Hallo filter voor SELECT-, UPDATE- en DELETE-query's. en een block-predicaat wordt voorkomen dat de rijen die strijdig zijn met deze voorwaarden niet kan worden ingevoegd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="864b3-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="864b3-155">Als SESSION_CONTEXT niet is ingesteld, wordt het geretourneerd dat null en geen rijen zijn zichtbaar is of kan het toobe ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="864b3-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="864b3-156">tooenable RLS, Hallo volgende T-SQL op alle shards met behulp van de Visual Studio (SSDT), SSMS, uitvoeren of PowerShell-script is opgenomen in het project Hallo hello (of als u [elastische Database taken](sql-database-elastic-jobs-overview.md), kunt u tooautomate uitvoering deze T-SQL op alle shards):</span><span class="sxs-lookup"><span data-stu-id="864b3-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

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
> <span data-ttu-id="864b3-157">Voor complexere projecten waarvoor tooadd Hallo predikaat op honderden tabellen, kunt u een helper opgeslagen procedure die genereert automatisch een beveiligingsbeleid toe te voegen een predicaat voor alle tabellen in een schema.</span><span class="sxs-lookup"><span data-stu-id="864b3-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="864b3-158">Zie [toepassen beveiliging tooall tabellen - helper-script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="864b3-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="864b3-159">Als u Hallo voorbeeldtoepassing opnieuw uitvoert, wordt tenants kunnen toosee alleen rijen die deel uitmaken van toothem.</span><span class="sxs-lookup"><span data-stu-id="864b3-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="864b3-160">Bovendien Hallo toepassing kan geen rijen die deel uitmaken van tootenants dan Hallo één momenteel verbonden toohello shard-database invoegen en zichtbare rijen toohave een andere tenant-id kan niet worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="864b3-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="864b3-161">Als de toepassing hello toodo ofwel probeert, wordt een DbUpdateException verschijnt.</span><span class="sxs-lookup"><span data-stu-id="864b3-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="864b3-162">Als u een nieuwe tabel later op gewoon ALTER Hallo beveiligingsbeleid toevoegen en filter en block-predicaten op Hallo nieuwe tabel toevoegen:</span><span class="sxs-lookup"><span data-stu-id="864b3-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="864b3-163">Standaard toevoegen beperkingen tooautomatically TenantId voor voegt vullen</span><span class="sxs-lookup"><span data-stu-id="864b3-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="864b3-164">U kunt een standaard plaatsen-beperking voor elke tabel tooautomatically vullen Hallo TenantId Hello waarde die momenteel zijn opgeslagen in SESSION_CONTEXT bij het invoegen van rijen.</span><span class="sxs-lookup"><span data-stu-id="864b3-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="864b3-165">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="864b3-165">For example:</span></span> 

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

<span data-ttu-id="864b3-166">Hallo-toepassing heeft nu geen toospecify een TenantId nodig bij het invoegen van rijen:</span><span class="sxs-lookup"><span data-stu-id="864b3-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="864b3-167">Als u een default-beperkingen voor een Entity Framework-project gebruiken, is het raadzaam dat u Hallo TenantId kolom niet in uw EF-gegevensmodel opnemen.</span><span class="sxs-lookup"><span data-stu-id="864b3-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="864b3-168">Dit komt doordat de Entity Framework-query's worden automatisch standaardwaarden die overschrijft Hallo default-beperkingen in T-SQL gemaakt die gebruikmaken van SESSION_CONTEXT opgeeft.</span><span class="sxs-lookup"><span data-stu-id="864b3-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="864b3-169">toouse default-beperkingen in Hallo steekproef project, bijvoorbeeld, moet u TenantId verwijderen uit DataClasses.cs (en voer Add-migratie in Hallo Package Manager Console) en gebruik T-SQL-tooensure die Hallo veld is alleen beschikbaar in databasetabellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="864b3-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="864b3-170">Op deze manier EF wordt niet automatisch opgeeft onjuiste standaardwaarden bij het invoegen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="864b3-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="864b3-171">(Optioneel) Alle rijen van een 'beheerder' tooaccess inschakelen</span><span class="sxs-lookup"><span data-stu-id="864b3-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="864b3-172">Sommige toepassingen kunt toocreate een 'beheerder' wie toegang tot alle rijen, bijvoorbeeld, in volgorde tooenable rapportage over alle tenants in alle shards of tooperform gesplitste/Merge-bewerkingen op shards die betrekking hebben op bewegende tenant rijen tussen databases.</span><span class="sxs-lookup"><span data-stu-id="864b3-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="864b3-173">tooenable, moet u een nieuwe SQL-gebruiker ('superuser' in dit voorbeeld) in elke shard-database maken.</span><span class="sxs-lookup"><span data-stu-id="864b3-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="864b3-174">Hallo-beveiligingsbeleid met een nieuwe predicaatfunctie waarmee deze gebruiker tooaccess alle rijen wijzigt:</span><span class="sxs-lookup"><span data-stu-id="864b3-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

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


### <a name="maintenance"></a><span data-ttu-id="864b3-175">Onderhoud</span><span class="sxs-lookup"><span data-stu-id="864b3-175">Maintenance</span></span>
* <span data-ttu-id="864b3-176">**Toevoegen van nieuwe shards**: Hallo T-SQL-script tooenable RLS moet worden uitgevoerd op een nieuwe shards, anders query's in deze shards worden niet gefilterd.</span><span class="sxs-lookup"><span data-stu-id="864b3-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="864b3-177">**Toevoegen van nieuwe tabellen**: U moet een filter toevoegen en predikaat toohello beveiligingsbeleid op alle shards blokkeren wanneer er een nieuwe tabel is gemaakt, anders query's op de nieuwe tabel Hallo worden niet gefilterd.</span><span class="sxs-lookup"><span data-stu-id="864b3-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="864b3-178">Dit kan worden geautomatiseerd met behulp van een DDL-trigger, zoals beschreven in [toepassen beveiliging automatisch gemaakt van tabellen (blog) in toonewly](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="864b3-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="864b3-179">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="864b3-179">Summary</span></span>
<span data-ttu-id="864b3-180">Elastische database-hulpprogramma's en de beveiliging kunnen worden gebruikt samen tooscale uit de gegevenslaag van een toepassing met ondersteuning voor multitenant- en één tenant shards.</span><span class="sxs-lookup"><span data-stu-id="864b3-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="864b3-181">Multitenant shards mag gebruikte toostore gegevens efficiënter (met name in gevallen waarin een groot aantal tenants slechts een paar rijen met gegevens hebben), tijdens één tenant shards mag gebruikte toosupport premium tenants met strengere prestaties en isolatie vereisten.</span><span class="sxs-lookup"><span data-stu-id="864b3-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="864b3-182">Zie voor meer informatie [beveiliging verwijzing](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="864b3-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="864b3-183">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="864b3-183">Additional resources</span></span>
* [<span data-ttu-id="864b3-184">Wat is een Azure elastische groep?</span><span class="sxs-lookup"><span data-stu-id="864b3-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="864b3-185">Uitbreiden met Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="864b3-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="864b3-186">Ontwerppatronen voor SaaS-toepassingen met meerdere tenants met behulp van Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="864b3-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="864b3-187">Verificatie in multitenant-apps met Azure AD en OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="864b3-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="864b3-188">De toepassing Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="864b3-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="864b3-189">Vragen en Functieaanvragen</span><span class="sxs-lookup"><span data-stu-id="864b3-189">Questions and Feature Requests</span></span>
<span data-ttu-id="864b3-190">Voor vragen kunt contact toous op Hallo [SQL Database-forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) en voor functieaanvragen, deze toe te voegen toohello [forum met feedback van SQL-Database](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="864b3-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


