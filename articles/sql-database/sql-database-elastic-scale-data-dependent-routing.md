---
title: Gegevens afhankelijke routering met Azure SQL Database | Microsoft Docs
description: Het gebruik van de klasse ShardMapManager in .NET-toepassingen voor gegevensafhankelijke routering, een functie van shard-databases in Azure SQL Database
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
ms.openlocfilehash: 6b68bbb0133afd1493acdb58f79f3eeaf6a8d7cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="22173-103">Gegevensafhankelijke routering</span><span class="sxs-lookup"><span data-stu-id="22173-103">Data dependent routing</span></span>
<span data-ttu-id="22173-104">**Gegevensafhankelijke routering** is de mogelijkheid om de gegevens in een query voor het routeren van de aanvraag met een juiste database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22173-104">**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database.</span></span> <span data-ttu-id="22173-105">Dit is een fundamenteel patroon bij het werken met shard-databases.</span><span class="sxs-lookup"><span data-stu-id="22173-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="22173-106">De aanvraagcontext kan ook worden gebruikt voor het routeren van de aanvraag, met name als de sleutel sharding geen deel uit van de query maakt.</span><span class="sxs-lookup"><span data-stu-id="22173-106">The request context may also be used to route the request, especially if the sharding key is not part of the query.</span></span> <span data-ttu-id="22173-107">Elke specifieke query of een transactie in een toepassing met gegevensafhankelijke routering is beperkt tot toegang tot een individuele database per aanvraag.</span><span class="sxs-lookup"><span data-stu-id="22173-107">Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request.</span></span> <span data-ttu-id="22173-108">Voor de Azure SQL Database elastische hulpprogramma's voor deze routering wordt uitgevoerd met de  **[ShardMapManager klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  in ADO.NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="22173-108">For the Azure SQL Database Elastic tools, this routing is accomplished with the **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="22173-109">De toepassing hoeft niet te volgen verschillende verbindingsreeksen of DB locaties die zijn gekoppeld aan andere delen van gegevens in de shard-omgeving.</span><span class="sxs-lookup"><span data-stu-id="22173-109">The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment.</span></span> <span data-ttu-id="22173-110">In plaats daarvan de [Shard kaart Manager](sql-database-elastic-scale-shard-map-management.md) wordt geopend verbindingen met de juiste databases indien nodig, op basis van de gegevens in de shard-toewijzing en de waarde van de sharding-sleutel die het doel van de aanvraag van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="22173-110">Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request.</span></span> <span data-ttu-id="22173-111">De sleutel is meestal de *customer_id*, *tenant_id*, *date_key*, of enige andere specifieke id die is een fundamenteel parameter van het verzoek voor database).</span><span class="sxs-lookup"><span data-stu-id="22173-111">The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request).</span></span> 

<span data-ttu-id="22173-112">Zie voor meer informatie [schalen van SQL Server met gegevensafhankelijke routering](https://technet.microsoft.com/library/cc966448.aspx).</span><span class="sxs-lookup"><span data-stu-id="22173-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-the-client-library"></a><span data-ttu-id="22173-113">Downloaden van de clientbibliotheek</span><span class="sxs-lookup"><span data-stu-id="22173-113">Download the client library</span></span>
<span data-ttu-id="22173-114">Als u de klasse, installeert u de [clientbibliotheek voor elastische Database](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="22173-114">To get the class, install the [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="22173-115">Met behulp van een ShardMapManager in een gegevenstoepassing afhankelijke routering</span><span class="sxs-lookup"><span data-stu-id="22173-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="22173-116">Het instantiëren van toepassingen moeten de **ShardMapManager** tijdens de initialisatie met behulp van de factory-aanroep  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="22173-116">Applications should instantiate the **ShardMapManager** during initialization, using the factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="22173-117">In dit voorbeeld wordt zowel een **ShardMapManager** en een specifieke **ShardMap** die deze bevat zijn geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="22173-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="22173-118">Dit voorbeeld ziet u de GetSqlShardMapManager en [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methoden.</span><span class="sxs-lookup"><span data-stu-id="22173-118">This example shows the GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-the-shard-map"></a><span data-ttu-id="22173-119">Laagste bevoegdheid referenties mogelijk gebruiken voor het ophalen van de shard-kaart</span><span class="sxs-lookup"><span data-stu-id="22173-119">Use lowest privilege credentials possible for getting the shard map</span></span>
<span data-ttu-id="22173-120">Als een toepassing de shard-toewijzing zelf niet bewerken is, de referenties in de fabrieksmethode slechts alleen-lezen toegang moeten hebben op de **globale Shard-toewijzing** database.</span><span class="sxs-lookup"><span data-stu-id="22173-120">If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database.</span></span> <span data-ttu-id="22173-121">Deze referenties zijn meestal verschillen van referenties die worden gebruikt voor het openen van verbindingen met de shard-toewijzing manager.</span><span class="sxs-lookup"><span data-stu-id="22173-121">These credentials are typically different from credentials used to open connections to the shard map manager.</span></span> <span data-ttu-id="22173-122">Zie ook [referenties gebruikt voor toegang tot de clientbibliotheek voor elastische Database](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="22173-122">See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-the-openconnectionforkey-method"></a><span data-ttu-id="22173-123">Roep de methode OpenConnectionForKey</span><span class="sxs-lookup"><span data-stu-id="22173-123">Call the OpenConnectionForKey method</span></span>
<span data-ttu-id="22173-124">De  **[ShardMap.OpenConnectionForKey methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  retourneert een ADO.Net-verbinding gereed is voor het uitgeven van opdrachten op de juiste database op basis van de waarde van de **sleutel** parameter.</span><span class="sxs-lookup"><span data-stu-id="22173-124">The **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands to the appropriate database based on the value of the **key** parameter.</span></span> <span data-ttu-id="22173-125">Shard-gegevens in cache wordt opgeslagen in de toepassing door de **ShardMapManager**, zodat deze aanvragen zoeken in de database op basis van geen doorgaans worden de **globale Shard-toewijzing** database.</span><span class="sxs-lookup"><span data-stu-id="22173-125">Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="22173-126">De **sleutel** parameter wordt gebruikt als een lookup-sleutel in de shard-toewijzing om te bepalen van de juiste database voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="22173-126">The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request.</span></span> 
* <span data-ttu-id="22173-127">De **connectionString** wordt gebruikt voor het doorgeven van de gebruikersreferenties voor de gewenste verbinding.</span><span class="sxs-lookup"><span data-stu-id="22173-127">The **connectionString** is used to pass only the user credentials for the desired connection.</span></span> <span data-ttu-id="22173-128">Er is geen databasenaam of servernaam zijn opgenomen in deze *connectionString* omdat de methode de database en de server met bepaalt de **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="22173-128">No database name or server name are included in this *connectionString* since the method will determine the database and server using the **ShardMap**.</span></span> 
* <span data-ttu-id="22173-129">De  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  moet worden ingesteld op **ConnectionOptions.Validate** als een omgeving waar shard toegewezen kan worden gewijzigd en rijen naar andere databases als gevolg van gesplitste of merge-bewerkingen verplaatsen kunnen.</span><span class="sxs-lookup"><span data-stu-id="22173-129">The **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations.</span></span> <span data-ttu-id="22173-130">Hiervoor moet een korte query naar de lokale shard-toewijzing op de doel-database (en niet naar de globale shard-toewijzing) voordat de verbinding naar de toepassing wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="22173-130">This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application.</span></span> 

<span data-ttu-id="22173-131">Als de validatie op basis van de lokale shard-toewijzing is mislukt (waarmee wordt aangegeven dat de cache onjuist is), query de Shard-toewijzing Manager de globale shard-toewijzing voor het verkrijgen van de nieuwe juiste waarde voor de zoekactie, de cache wordt bijgewerkt en opvragen en verbinding met de juiste database geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="22173-131">If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager will query the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection.</span></span> 

<span data-ttu-id="22173-132">Gebruik **ConnectionOptions.None** alleen wanneer shard-toewijzing wijzigingen wordt niet verwacht terwijl een toepassing online is.</span><span class="sxs-lookup"><span data-stu-id="22173-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="22173-133">In dat geval waarden in het cachegeheugen altijd alleen correct kunnen worden aangenomen en de aanroep extra round trip validatie van de doeldatabase veilig worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="22173-133">In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped.</span></span> <span data-ttu-id="22173-134">Dat vermindert databaseverkeer.</span><span class="sxs-lookup"><span data-stu-id="22173-134">That reduces database traffic.</span></span> <span data-ttu-id="22173-135">De **connectionOptions** kan ook worden ingesteld via een waarde in een configuratiebestand om aan te geven dat sharding wijzigingen worden verwacht of tijdens een bepaalde tijd niet.</span><span class="sxs-lookup"><span data-stu-id="22173-135">The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="22173-136">In dit voorbeeld wordt de waarde van de sleutel van een geheel getal **CustomerID**met een **ShardMap** object met de naam **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="22173-136">This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect to the shard for that customer ID. No need to call a SqlConnection 
    // constructor followed by the Open method.
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

<span data-ttu-id="22173-137">De **OpenConnectionForKey** methode retourneert een nieuwe al open verbinding met de juiste database.</span><span class="sxs-lookup"><span data-stu-id="22173-137">The **OpenConnectionForKey** method returns a new already-open connection to the correct database.</span></span> <span data-ttu-id="22173-138">Verbindingen gebruikt op deze manier kunnen nog steeds profiteren van de ADO.Net verbindingsgroepering.</span><span class="sxs-lookup"><span data-stu-id="22173-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="22173-139">Zolang transacties en aanvragen kunnen worden voldaan door één shard tegelijk, moet dit de enige aanpassing die in een toepassing die al met ADO.Net nodig.</span><span class="sxs-lookup"><span data-stu-id="22173-139">As long as transactions and requests can be satisfied by one shard at a time, this should be the only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="22173-140">De  **[OpenConnectionForKeyAsync methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  is ook beschikbaar als uw toepassing gebruik van asynchrone programmering met ADO.Net maakt.</span><span class="sxs-lookup"><span data-stu-id="22173-140">The **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="22173-141">Het gedrag is de afhankelijke routering equivalent met ADO gegevens. De NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  methode.</span><span class="sxs-lookup"><span data-stu-id="22173-141">Its behavior is the data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="22173-142">Integratie met afhandeling van tijdelijke fout</span><span class="sxs-lookup"><span data-stu-id="22173-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="22173-143">Er is een best practice bij het ontwikkelen van de data access-toepassingen in de cloud om ervoor te zorgen dat de tijdelijke fouten zijn opgepikt door de app en dat de bewerkingen zijn niet opnieuw geprobeerd meerdere keren voordat er wordt een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="22173-143">A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error.</span></span> <span data-ttu-id="22173-144">Tijdelijke fout verwerking voor cloud-toepassingen is besproken in [afhandeling van tijdelijke fout](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="22173-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="22173-145">Afhandeling van tijdelijke fout kan natuurlijk worden gecombineerd met het patroon gegevensafhankelijke routering.</span><span class="sxs-lookup"><span data-stu-id="22173-145">Transient fault handling can coexist naturally with the Data Dependent Routing pattern.</span></span> <span data-ttu-id="22173-146">De belangrijkste vereiste is om opnieuw te proberen de gehele toegang aanvraag, waaronder de **met** blok die de gegevensafhankelijke routering verbinding hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="22173-146">The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection.</span></span> <span data-ttu-id="22173-147">Het bovenstaande voorbeeld kan worden herschreven als volgt (Opmerking gemarkeerd wijzigen).</span><span class="sxs-lookup"><span data-stu-id="22173-147">The example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="22173-148">Voorbeeld - afhankelijke routering met tijdelijke fout afhandeling van gegevens</span><span class="sxs-lookup"><span data-stu-id="22173-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect to the shard for a customer ID. 
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


<span data-ttu-id="22173-149">Pakketten die nodig zijn voor het implementeren van afhandeling van tijdelijke fout worden automatisch gedownload als u de voorbeeldtoepassing elastische database.</span><span class="sxs-lookup"><span data-stu-id="22173-149">Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application.</span></span> <span data-ttu-id="22173-150">Pakketten zijn ook verkrijgbaar afzonderlijk via [Enterprise Library - tijdelijke fout afhandeling van Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="22173-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="22173-151">Versie 6.0 of hoger gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22173-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="22173-152">Transactionele consistentie</span><span class="sxs-lookup"><span data-stu-id="22173-152">Transactional consistency</span></span>
<span data-ttu-id="22173-153">Transactionele eigenschappen zijn gegarandeerd voor alle bewerkingen die lokaal op een shard.</span><span class="sxs-lookup"><span data-stu-id="22173-153">Transactional properties are guaranteed for all operations local to a shard.</span></span> <span data-ttu-id="22173-154">Bijvoorbeeld, uitvoeren transacties die zijn verzonden via het gegevensafhankelijke routering binnen het bereik van de shard doel voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="22173-154">For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection.</span></span> <span data-ttu-id="22173-155">Op dit moment zijn er geen mogelijkheden voor het opnemen van meerdere verbindingen in een transactie en er zijn daarom geen transactionele garanties met betrekking tot de bewerkingen die worden uitgevoerd via shards.</span><span class="sxs-lookup"><span data-stu-id="22173-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22173-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22173-156">Next steps</span></span>
<span data-ttu-id="22173-157">Zie een shard loskoppelen of opnieuw koppelen van een shard [met behulp van de klasse RecoveryManager shard kaart problemen op te lossen](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="22173-157">To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

