---
title: aaaData afhankelijke routering met Azure SQL Database | Microsoft Docs
description: Hoe toouse Hallo ShardMapManager klasse in .NET-toepassingen voor gegevensafhankelijke routering, een functie van shard-databases in Azure SQL Database
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="3f12e-103">Gegevensafhankelijke routering</span><span class="sxs-lookup"><span data-stu-id="3f12e-103">Data dependent routing</span></span>
<span data-ttu-id="3f12e-104">**Gegevensafhankelijke routering** Hallo mogelijkheid toouse Hallo gegevens in een query tooroute Hallo aanvraag tooan juiste database is.</span><span class="sxs-lookup"><span data-stu-id="3f12e-104">**Data dependent routing** is hello ability toouse hello data in a query tooroute hello request tooan appropriate database.</span></span> <span data-ttu-id="3f12e-105">Dit is een fundamenteel patroon bij het werken met shard-databases.</span><span class="sxs-lookup"><span data-stu-id="3f12e-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="3f12e-106">Hallo-aanvraagcontext mogelijk ook de gebruikte tooroute Hallo aanvraag, vooral als Hallo sharding sleutel geen deel uit van Hallo query maakt.</span><span class="sxs-lookup"><span data-stu-id="3f12e-106">hello request context may also be used tooroute hello request, especially if hello sharding key is not part of hello query.</span></span> <span data-ttu-id="3f12e-107">Elke specifieke query transactie is of in een toepassing met gegevensafhankelijke routering beperkt tooaccessing een individuele database per aanvraag.</span><span class="sxs-lookup"><span data-stu-id="3f12e-107">Each specific query or transaction in an application using data dependent routing is restricted tooaccessing a single database per request.</span></span> <span data-ttu-id="3f12e-108">Voor hello Azure SQL Database elastische hulpprogramma's voor deze routering wordt gerealiseerd met Hallo  **[ShardMapManager klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  in ADO.NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3f12e-108">For hello Azure SQL Database Elastic tools, this routing is accomplished with hello **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="3f12e-109">Hallo toepassing hoeft niet tootrack verschillende verbindingsreeksen of DB locaties die zijn gekoppeld aan andere delen van gegevens in Hallo shard-omgeving.</span><span class="sxs-lookup"><span data-stu-id="3f12e-109">hello application does not need tootrack various connection strings or DB locations associated with different slices of data in hello sharded environment.</span></span> <span data-ttu-id="3f12e-110">In plaats daarvan Hallo [Shard kaart Manager](sql-database-elastic-scale-shard-map-management.md) wordt geopend verbindingen toohello juiste databases, indien nodig op basis van Hallo-gegevens in Hallo shard-toewijzing en Hallo-waarde van Hallo sharding-sleutel die Hallo doel van de aanvraag van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="3f12e-110">Instead, hello [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections toohello correct databases when needed, based on hello data in hello shard map and hello value of hello sharding key that is hello target of hello application’s request.</span></span> <span data-ttu-id="3f12e-111">Hallo-sleutel is doorgaans Hallo *customer_id*, *tenant_id*, *date_key*, of enige andere specifieke id die is een fundamenteel parameter van het Hallo-verzoek voor database).</span><span class="sxs-lookup"><span data-stu-id="3f12e-111">hello key is typically hello *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of hello database request).</span></span> 

<span data-ttu-id="3f12e-112">Zie voor meer informatie [schalen van SQL Server met gegevensafhankelijke routering](https://technet.microsoft.com/library/cc966448.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f12e-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-hello-client-library"></a><span data-ttu-id="3f12e-113">Hallo-clientbibliotheek downloaden</span><span class="sxs-lookup"><span data-stu-id="3f12e-113">Download hello client library</span></span>
<span data-ttu-id="3f12e-114">tooget hello klasse, installatie Hallo [clientbibliotheek voor elastische Database](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="3f12e-114">tooget hello class, install hello [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="3f12e-115">Met behulp van een ShardMapManager in een gegevenstoepassing afhankelijke routering</span><span class="sxs-lookup"><span data-stu-id="3f12e-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="3f12e-116">Toepassingen moeten Hallo instantiëren **ShardMapManager** tijdens de initialisatie met Hallo factory aanroep  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="3f12e-116">Applications should instantiate hello **ShardMapManager** during initialization, using hello factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="3f12e-117">In dit voorbeeld wordt zowel een **ShardMapManager** en een specifieke **ShardMap** die deze bevat zijn geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="3f12e-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="3f12e-118">In dit voorbeeld toont Hallo GetSqlShardMapManager en [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methoden.</span><span class="sxs-lookup"><span data-stu-id="3f12e-118">This example shows hello GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a><span data-ttu-id="3f12e-119">Laagste bevoegdheid referenties mogelijk gebruiken voor het ophalen van Hallo shard-kaart</span><span class="sxs-lookup"><span data-stu-id="3f12e-119">Use lowest privilege credentials possible for getting hello shard map</span></span>
<span data-ttu-id="3f12e-120">Als een toepassing Hallo shard-toewijzing zelf niet bewerken is, Hallo referenties in fabrieksmethode Hallo slechts alleen-lezen toegang moeten hebben op Hallo **globale Shard-toewijzing** database.</span><span class="sxs-lookup"><span data-stu-id="3f12e-120">If an application is not manipulating hello shard map itself, hello credentials used in hello factory method should have just read-only permissions on hello **Global Shard Map** database.</span></span> <span data-ttu-id="3f12e-121">Deze referenties zijn meestal af van de referenties die worden gebruikt tooopen verbindingen toohello shard kaart manager.</span><span class="sxs-lookup"><span data-stu-id="3f12e-121">These credentials are typically different from credentials used tooopen connections toohello shard map manager.</span></span> <span data-ttu-id="3f12e-122">Zie ook [referenties gebruikt tooaccess Hallo elastische Database-clientbibliotheek](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="3f12e-122">See also [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-hello-openconnectionforkey-method"></a><span data-ttu-id="3f12e-123">Hallo OpenConnectionForKey methode aanroepen</span><span class="sxs-lookup"><span data-stu-id="3f12e-123">Call hello OpenConnectionForKey method</span></span>
<span data-ttu-id="3f12e-124">Hallo  **[ShardMap.OpenConnectionForKey methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  retourneert een ADO.Net-verbinding gereed is voor het uitgeven van opdrachten toohello juiste database op basis van de Hallo Hallo **sleutel**parameter.</span><span class="sxs-lookup"><span data-stu-id="3f12e-124">hello **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands toohello appropriate database based on hello value of hello **key** parameter.</span></span> <span data-ttu-id="3f12e-125">Shard-gegevens in cache wordt opgeslagen in de toepassing hello door Hallo **ShardMapManager**, zodat deze aanvragen zoeken in de database tegen Hallo geen doorgaans worden **globale Shard-toewijzing** database.</span><span class="sxs-lookup"><span data-stu-id="3f12e-125">Shard information is cached in hello application by hello **ShardMapManager**, so these requests do not typically involve a database lookup against hello **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="3f12e-126">Hallo **sleutel** parameter wordt gebruikt als een zoeksleutel in Hallo shard kaart toodetermine Hallo juiste database voor Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="3f12e-126">hello **key** parameter is used as a lookup key into hello shard map toodetermine hello appropriate database for hello request.</span></span> 
* <span data-ttu-id="3f12e-127">Hallo **connectionString** gebruikte toopass alleen Hallo gebruikersreferenties voor verbinding Hallo gewenst is.</span><span class="sxs-lookup"><span data-stu-id="3f12e-127">hello **connectionString** is used toopass only hello user credentials for hello desired connection.</span></span> <span data-ttu-id="3f12e-128">Er is geen databasenaam of servernaam zijn opgenomen in deze *connectionString* omdat het Hallo-methode wordt bepaald Hallo-database en de server met behulp van Hallo **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="3f12e-128">No database name or server name are included in this *connectionString* since hello method will determine hello database and server using hello **ShardMap**.</span></span> 
* <span data-ttu-id="3f12e-129">Hallo  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  te moet worden ingesteld**ConnectionOptions.Validate** als kan worden gewijzigd in een omgeving waar shard toegewezen en rijen tooother databases als verplaatsen kunnen een resultaat van de gesplitste of merge-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="3f12e-129">hello **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set too**ConnectionOptions.Validate** if an environment where shard maps may change and rows may move tooother databases as a result of split or merge operations.</span></span> <span data-ttu-id="3f12e-130">Hiervoor moet een korte query toohello lokale shard-toewijzing op Hallo doeldatabase (niet toohello globale shard toewijzen) voordat Hallo verbinding toohello toepassing wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="3f12e-130">This involves a brief query toohello local shard map on hello target database (not toohello global shard map) before hello connection is delivered toohello application.</span></span> 

<span data-ttu-id="3f12e-131">Als Hallo validatie met het Hallo lokale shard-toewijzing is mislukt (waarmee wordt aangegeven dat Hallo cache onjuist is), Hallo Shard kaart Manager Hallo globale shard kaart tooobtain Hallo nieuwe correcte waarde query voor het opzoeken van Hallo Hallo-cache, bijwerken en verkrijgen en Hallo retourneren juiste databaseverbinding.</span><span class="sxs-lookup"><span data-stu-id="3f12e-131">If hello validation against hello local shard map fails (indicating that hello cache is incorrect), hello Shard Map Manager will query hello global shard map tooobtain hello new correct value for hello lookup, update hello cache, and obtain and return hello appropriate database connection.</span></span> 

<span data-ttu-id="3f12e-132">Gebruik **ConnectionOptions.None** alleen wanneer shard-toewijzing wijzigingen wordt niet verwacht terwijl een toepassing online is.</span><span class="sxs-lookup"><span data-stu-id="3f12e-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="3f12e-133">In dat geval kunnen Hallo in de cache opgeslagen waarden worden aangenomen tooalways juist zijn en Hallo extra round trip validatie aanroep toohello-doeldatabase veilig worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3f12e-133">In that case, hello cached values can be assumed tooalways be correct, and hello extra round-trip validation call toohello target database can be safely skipped.</span></span> <span data-ttu-id="3f12e-134">Dat vermindert databaseverkeer.</span><span class="sxs-lookup"><span data-stu-id="3f12e-134">That reduces database traffic.</span></span> <span data-ttu-id="3f12e-135">Hallo **connectionOptions** kan ook worden ingesteld via een waarde in een configuratie-bestand tooindicate of sharding wijzigingen worden verwacht, of tijdens een bepaalde tijd niet.</span><span class="sxs-lookup"><span data-stu-id="3f12e-135">hello **connectionOptions** may also be set via a value in a configuration file tooindicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="3f12e-136">In dit voorbeeld wordt Hallo-waarde van de sleutel van een geheel getal **CustomerID**met een **ShardMap** object met de naam **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="3f12e-136">This example uses hello value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="3f12e-137">Hallo **OpenConnectionForKey** methode retourneert een nieuwe al-geopende verbinding toohello juiste database.</span><span class="sxs-lookup"><span data-stu-id="3f12e-137">hello **OpenConnectionForKey** method returns a new already-open connection toohello correct database.</span></span> <span data-ttu-id="3f12e-138">Verbindingen gebruikt op deze manier kunnen nog steeds profiteren van de ADO.Net verbindingsgroepering.</span><span class="sxs-lookup"><span data-stu-id="3f12e-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="3f12e-139">Zolang transacties en aanvragen kunnen worden voldaan door één shard tegelijk, moet dit enige aanpassing Hallo nodig in een toepassing die al met ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="3f12e-139">As long as transactions and requests can be satisfied by one shard at a time, this should be hello only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="3f12e-140">Hallo  **[OpenConnectionForKeyAsync methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  is ook beschikbaar als uw toepassing gebruik van asynchrone programmering met ADO.Net maakt.</span><span class="sxs-lookup"><span data-stu-id="3f12e-140">hello **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="3f12e-141">Het gedrag is Hallo gegevens afhankelijke equivalent met ADO routering. De NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  methode.</span><span class="sxs-lookup"><span data-stu-id="3f12e-141">Its behavior is hello data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="3f12e-142">Integratie met afhandeling van tijdelijke fout</span><span class="sxs-lookup"><span data-stu-id="3f12e-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="3f12e-143">Tooensure of tijdelijke fouten zijn opgepikt door het Hallo-app en dat Hallo operations meerdere keren worden geprobeerd voordat er wordt een fout is door een best practice bij het ontwikkelen van de data access-toepassingen in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="3f12e-143">A best practice in developing data access applications in hello cloud is tooensure that transient faults are caught by hello app, and that hello operations are retried several times before throwing an error.</span></span> <span data-ttu-id="3f12e-144">Tijdelijke fout verwerking voor cloud-toepassingen is besproken in [afhandeling van tijdelijke fout](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="3f12e-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="3f12e-145">Afhandeling van tijdelijke fout kan natuurlijk worden gecombineerd met Hallo gegevensafhankelijke routering patroon.</span><span class="sxs-lookup"><span data-stu-id="3f12e-145">Transient fault handling can coexist naturally with hello Data Dependent Routing pattern.</span></span> <span data-ttu-id="3f12e-146">Hallo belangrijkste vereiste is tooretry Hallo gehele toegangsaanvraag inclusief Hallo **met** blok die Hallo gegevensafhankelijke routering verbinding hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="3f12e-146">hello key requirement is tooretry hello entire data access request including hello **using** block that obtained hello data-dependent routing connection.</span></span> <span data-ttu-id="3f12e-147">Hallo in bovenstaand voorbeeld kan worden herschreven als volgt (Houd er rekening mee gemarkeerde wijzigen).</span><span class="sxs-lookup"><span data-stu-id="3f12e-147">hello example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="3f12e-148">Voorbeeld - afhankelijke routering met tijdelijke fout afhandeling van gegevens</span><span class="sxs-lookup"><span data-stu-id="3f12e-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="3f12e-149">Verwerking van de benodigde tooimplement tijdelijke fout zijn pakketten gedownload automatisch wanneer het bouwen van Hallo elastische database-voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="3f12e-149">Packages necessary tooimplement transient fault handling are downloaded automatically when you build hello elastic database sample application.</span></span> <span data-ttu-id="3f12e-150">Pakketten zijn ook verkrijgbaar afzonderlijk via [Enterprise Library - tijdelijke fout afhandeling van Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="3f12e-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="3f12e-151">Versie 6.0 of hoger gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f12e-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="3f12e-152">Transactionele consistentie</span><span class="sxs-lookup"><span data-stu-id="3f12e-152">Transactional consistency</span></span>
<span data-ttu-id="3f12e-153">Transactionele eigenschappen zijn voor alle bewerkingen lokale tooa shard gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="3f12e-153">Transactional properties are guaranteed for all operations local tooa shard.</span></span> <span data-ttu-id="3f12e-154">Bijvoorbeeld, uitvoeren transacties die zijn verzonden via het gegevensafhankelijke routering binnen Hallo bereik van Hallo doel shard voor Hallo-verbinding.</span><span class="sxs-lookup"><span data-stu-id="3f12e-154">For example, transactions submitted through data-dependent routing execute within hello scope of hello target shard for hello connection.</span></span> <span data-ttu-id="3f12e-155">Op dit moment zijn er geen mogelijkheden voor het opnemen van meerdere verbindingen in een transactie en er zijn daarom geen transactionele garanties met betrekking tot de bewerkingen die worden uitgevoerd via shards.</span><span class="sxs-lookup"><span data-stu-id="3f12e-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f12e-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f12e-156">Next steps</span></span>
<span data-ttu-id="3f12e-157">Zie voor een shard toodetach of tooreattach een shard [hello RecoveryManager klasse toofix shard kaart problemen met](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="3f12e-157">toodetach a shard, or tooreattach a shard, see [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

