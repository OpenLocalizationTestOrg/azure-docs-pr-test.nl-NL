---
title: aaaConnecting Apache Spark tooAzure Cosmos DB | Microsoft Docs
description: Gebruik deze zelfstudie toolearn over hello Azure Cosmos DB Spark-connector waarmee u tooconnect Apache Spark tooAzure Cosmos DB tooperform gedistribueerd aggregaties en gegevens sciences op Hallo globaal gedistribueerde database voor meerdere tenants systeem van Microsoft die ontworpen voor cloud Hallo.
keywords: Apache spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="74099-104">Versnellen realtime big data-analyses met Hallo Spark tooAzure Cosmos-DB-connector</span><span class="sxs-lookup"><span data-stu-id="74099-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="74099-105">Hallo Spark tooAzure Cosmos DB connector kunnen Azure Cosmos DB tooact als invoerbron of uitvoerlocatie voor Apache Spark-taken.</span><span class="sxs-lookup"><span data-stu-id="74099-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="74099-106">Verbinding maken met [Spark](http://spark.apache.org/) te[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) versnelt uw mogelijkheid toosolve snel bewegende gegevenswetenschap problemen waar u Azure Cosmos DB tooquickly kunt behouden en gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="74099-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="74099-107">Hallo Spark tooAzure Cosmos-DB-connector maakt efficiënt gebruik Hallo systeemeigen Azure Cosmos DB beheerd indexen.</span><span class="sxs-lookup"><span data-stu-id="74099-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="74099-108">Hallo indexen inschakelen bij te werken kolommen als u analyses uitvoeren en push-down predicaat filteren op basis van snel veranderende globaal gedistribueerd gegevens, die van het Internet der dingen (IoT) toodata wetenschappelijke en analyses scenario's variëren.</span><span class="sxs-lookup"><span data-stu-id="74099-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="74099-109">Zie voor het werken met Spark GraphX en Hallo Gremlin graph API's van Azure Cosmos DB, [grafiek analyses met behulp van Spark en Apache TinkerPop Gremlin uitvoeren](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="74099-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="74099-110">Downloaden</span><span class="sxs-lookup"><span data-stu-id="74099-110">Download</span></span>

<span data-ttu-id="74099-111">tooget gestart, Hallo Spark tooAzure Cosmos DB connector (preview) downloaden van Hallo [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="74099-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="74099-112">Connector-onderdelen</span><span class="sxs-lookup"><span data-stu-id="74099-112">Connector components</span></span>

<span data-ttu-id="74099-113">Hallo-connector maakt gebruik van Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="74099-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="74099-114">[Azure Cosmos DB](http://documentdb.com) kunnen klanten tooprovision en schalen zowel doorvoer en opslag via verschillende geografische regio's.</span><span class="sxs-lookup"><span data-stu-id="74099-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="74099-115">Hallo-service biedt:</span><span class="sxs-lookup"><span data-stu-id="74099-115">hello service offers:</span></span>
   * <span data-ttu-id="74099-116">Schakel sleutel [globale distributie](distribute-data-globally.md) en horizontale schaal</span><span class="sxs-lookup"><span data-stu-id="74099-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="74099-117">Gegarandeerd één cijfer latenties op Hallo 99th percentiel</span><span class="sxs-lookup"><span data-stu-id="74099-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="74099-118">Meerdere goed gedefinieerde consistentie modellen</span><span class="sxs-lookup"><span data-stu-id="74099-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="74099-119">Hoge beschikbaarheid met mogelijkheden voor multihoming gegarandeerd</span><span class="sxs-lookup"><span data-stu-id="74099-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="74099-120">Alle functies worden ondersteund door de toonaangevende, uitgebreide [serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/cosmos-db) (Sla's).</span><span class="sxs-lookup"><span data-stu-id="74099-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="74099-121">[Apache Spark](http://spark.apache.org/) is een krachtige open-source-verwerkingsengine die gebaseerd op snelheid, gebruiksgemak en geavanceerde analyses,.</span><span class="sxs-lookup"><span data-stu-id="74099-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="74099-122">[Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) zodat u Apache Spark in de cloud Hallo voor essentiële implementaties implementeren met behulp van kunt [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="74099-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="74099-123">Officieel ondersteunde versies:</span><span class="sxs-lookup"><span data-stu-id="74099-123">Officially supported versions:</span></span>

| <span data-ttu-id="74099-124">Onderdeel</span><span class="sxs-lookup"><span data-stu-id="74099-124">Component</span></span> | <span data-ttu-id="74099-125">Versie</span><span class="sxs-lookup"><span data-stu-id="74099-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="74099-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="74099-126">Apache Spark</span></span>|<span data-ttu-id="74099-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="74099-127">2.0+</span></span>|
| <span data-ttu-id="74099-128">Scala</span><span class="sxs-lookup"><span data-stu-id="74099-128">Scala</span></span>| <span data-ttu-id="74099-129">2.11</span><span class="sxs-lookup"><span data-stu-id="74099-129">2.11</span></span>|
| <span data-ttu-id="74099-130">Azure DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="74099-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="74099-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="74099-131">1.10.0</span></span> |

<span data-ttu-id="74099-132">In dit artikel helpt u enkele eenvoudige voorbeelden uitvoeren met behulp van Python (via pyDocumentDB) en Hallo Scala-interfaces.</span><span class="sxs-lookup"><span data-stu-id="74099-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="74099-133">Er zijn twee benaderingen tooconnect Apache Spark en Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="74099-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="74099-134">Gebruik pyDocumentDB via Hallo [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="74099-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="74099-135">Een Java gebaseerde Spark tooAzure Cosmos-DB-connector maken door het gebruik van Hallo [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="74099-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="74099-136">pyDocumentDB-implementatie</span><span class="sxs-lookup"><span data-stu-id="74099-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="74099-137">huidige Hallo [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) kunt u tooconnect Spark tooAzure Cosmos DB zoals weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="74099-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure Cosmos DB gegevensstroom via pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="74099-139">Gegevensstroom van Hallo pyDocumentDB implementatie</span><span class="sxs-lookup"><span data-stu-id="74099-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="74099-140">Hallo-gegevensstroom is als volgt:</span><span class="sxs-lookup"><span data-stu-id="74099-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="74099-141">Hallo Spark-hoofdknooppunt verbindt toohello Azure Cosmos DB gateway-knooppunt via pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="74099-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="74099-142">Een gebruiker geeft alleen Hallo Spark en Azure Cosmos DB-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="74099-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="74099-143">Verbindingen toohello respectieve hoofd- en gateway knooppunten zijn transparante toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="74099-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="74099-144">Hallo gateway-knooppunt maakt Hallo-query op Azure Cosmos DB waar Hallo query later wordt uitgevoerd op Hallo verzameling van partities in Hallo gegevensknooppunten.</span><span class="sxs-lookup"><span data-stu-id="74099-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="74099-145">Hallo antwoord voor de query's wordt teruggestuurd toohello gateway-knooppunt en die resultatenset geretourneerd toohello Spark-hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="74099-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="74099-146">Volgende query's (bijvoorbeeld op een Spark-DataFrame) worden verzonden toohello Spark worker-knooppunten voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="74099-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="74099-147">Communicatie tussen Spark en Azure Cosmos DB is beperkt toohello Spark-hoofdknooppunt en Azure Cosmos DB gateway-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="74099-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="74099-148">Hallo-query's gaan snel Hallo transportlaag tussen deze twee knooppunten kunt.</span><span class="sxs-lookup"><span data-stu-id="74099-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="74099-149">PyDocumentDB installeren</span><span class="sxs-lookup"><span data-stu-id="74099-149">Install pyDocumentDB</span></span>
<span data-ttu-id="74099-150">U kunt pyDocumentDB in uw Stuurprogrammaknooppunt installeren met behulp van **pip**, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="74099-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="74099-151">Verbinding maken met Spark tooAzure Cosmos DB via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="74099-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="74099-152">uitvoering van een query uit Spark tooAzure Cosmos DB maakt Hallo eenvoud van Hallo communicatie transport met behulp van pyDocumentDB relatief eenvoudige.</span><span class="sxs-lookup"><span data-stu-id="74099-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="74099-153">Hallo code codefragment wordt getoond hoe na toouse pyDocumentDB in een Spark-context.</span><span class="sxs-lookup"><span data-stu-id="74099-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="74099-154">Zoals vermeld in het codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="74099-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="74099-155">Hello Azure Cosmos DB Python SDK (`pyDocumentDB`) Hallo bevat alle benodigde verbindingsparameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="74099-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="74099-156">Hallo voorkeur bijvoorbeeld locaties parameter kiest Hallo lezen replica en de prioriteit.</span><span class="sxs-lookup"><span data-stu-id="74099-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="74099-157">Hallo nodig bibliotheken Importeer en configureer uw **hoofdsleutel** en **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_ client**).</span><span class="sxs-lookup"><span data-stu-id="74099-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="74099-158">Spark-query's uitvoeren via pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="74099-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="74099-159">Hallo volgen voorbeelden gebruik hello Azure DB die Cosmos-exemplaar dat is gemaakt in de vorige codefragment Hallo Hallo met alleen-lezen sleutels opgegeven.</span><span class="sxs-lookup"><span data-stu-id="74099-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="74099-160">Hallo volgende codefragment verbindt toohello **airports.codes** verzameling in hello DoctorWho account zijn als die eerder is opgegeven en wordt een query tooextract Hallo luchthaven steden uitgevoerd in de staat Washington.</span><span class="sxs-lookup"><span data-stu-id="74099-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

<span data-ttu-id="74099-161">Nadat het Hallo-query is uitgevoerd **query**, Hallo resultaat is een **query_iterable. QueryIterable** die geconverteerde tooa Python-lijst.</span><span class="sxs-lookup"><span data-stu-id="74099-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="74099-162">Een lijst met Python kan eenvoudig geconverteerde tooa Spark DataFrame met behulp van de volgende code Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="74099-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="74099-163">Waarom Hallo pyDocumentDB tooconnect Spark tooAzure Cosmos DB gebruiken?</span><span class="sxs-lookup"><span data-stu-id="74099-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="74099-164">Verbinding maken met Spark tooAzure Cosmos-database met behulp van pyDocumentDB doorgaans voor scenario's is waarbij:</span><span class="sxs-lookup"><span data-stu-id="74099-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="74099-165">Wilt u toouse Python.</span><span class="sxs-lookup"><span data-stu-id="74099-165">You want toouse Python.</span></span>
* <span data-ttu-id="74099-166">U kunt een relatief klein resultaatset uit Azure Cosmos DB tooSpark wilt retourneren.</span><span class="sxs-lookup"><span data-stu-id="74099-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="74099-167">Let op Hallo van onderliggende gegevensset in Azure Cosmos DB kan behoorlijk groot zijn.</span><span class="sxs-lookup"><span data-stu-id="74099-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="74099-168">U zijn filters zijn toegepast, dat wil zeggen, met het predikaat filters uitvoeren in uw Azure Cosmos DB-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="74099-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="74099-169">Spark tooAzure Cosmos-DB-connector</span><span class="sxs-lookup"><span data-stu-id="74099-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="74099-170">Hallo Spark tooAzure Cosmos-DB-connector maakt gebruik van Hallo [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) en worden gegevens verplaatst tussen Hallo Spark worker-knooppunten en Azure Cosmos DB, zoals wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="74099-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Gegevensoverdracht in Hallo Spark tooAzure Cosmos-DB-connector](./media/spark-connector/spark-connector.png)

<span data-ttu-id="74099-172">Hallo-gegevensstroom is als volgt:</span><span class="sxs-lookup"><span data-stu-id="74099-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="74099-173">Hallo Spark-hoofdknooppunt verbindt toohello Azure Cosmos DB gateway knooppunt tooobtain Hallo partitiekaart.</span><span class="sxs-lookup"><span data-stu-id="74099-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="74099-174">Een gebruiker geeft alleen Hallo Spark en Azure Cosmos DB-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="74099-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="74099-175">Verbindingen toohello respectieve hoofd- en gateway knooppunten zijn transparante toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="74099-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="74099-176">Deze informatie wordt verstrekt back toohello Spark-hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="74099-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="74099-177">Op dit moment moet kunnen tooparse Hallo query toodetermine Hallo-partities en de locaties in Azure Cosmos-database moet u tooaccess.</span><span class="sxs-lookup"><span data-stu-id="74099-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="74099-178">Deze informatie wordt verzonden toohello Spark worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="74099-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="74099-179">Hallo Spark worker-knooppunten verbinding toohello Azure Cosmos DB partities direct tooextract Hallo van gegevens en Hallo gegevens toohello Spark partities in Hallo Spark worker-knooppunten retourneren.</span><span class="sxs-lookup"><span data-stu-id="74099-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="74099-180">Communicatie tussen Spark en Azure Cosmos DB is aanzienlijk sneller Hallo gegevensverplaatsing ligt tussen Hallo Spark worker-knooppunten en hello Azure Cosmos DB gegevensknooppunten (partities).</span><span class="sxs-lookup"><span data-stu-id="74099-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="74099-181">Hallo Spark tooAzure Cosmos-DB-connector maken</span><span class="sxs-lookup"><span data-stu-id="74099-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="74099-182">Op dit moment Hallo-connector wordt gebruikt maven.</span><span class="sxs-lookup"><span data-stu-id="74099-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="74099-183">toobuild Hallo-connector zonder de afhankelijkheden die u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="74099-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="74099-184">U kunt ook de meest recente versies Hallo Hallo JAR downloaden van Hallo *releases* map.</span><span class="sxs-lookup"><span data-stu-id="74099-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="74099-185">Hello Azure Cosmos DB Spark JAR opnemen</span><span class="sxs-lookup"><span data-stu-id="74099-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="74099-186">Voordat u code uitvoert, moet u tooinclude hello Azure Cosmos DB Spark JAR.</span><span class="sxs-lookup"><span data-stu-id="74099-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="74099-187">Als u van Hallo gebruikmaakt **spark-shell**, en vervolgens u Hallo JAR opnemen kunt met behulp van Hallo **--potten** optie.</span><span class="sxs-lookup"><span data-stu-id="74099-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="74099-188">Als u tooexecute Hallo JAR zonder afhankelijkheden wilt, gebruikt u Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="74099-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="74099-189">Als u een service notebook zoals Azure HDInsight Jupyter-notebook service gebruikt, kunt u Hallo **spark magic** opdrachten:</span><span class="sxs-lookup"><span data-stu-id="74099-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="74099-190">Hallo **potten** opdracht schakelt u tooinclude Hallo twee JARs die nodig zijn voor **azure-cosmosdb-spark** (zelf en hello Azure DocumentDB Java SDK) en wilt uitsluiten **scala-weer** zodat deze niet van invloed op Hallo Livy aanroepen (Jupyter-notebook > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="74099-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="74099-191">Verbinding maken met Spark tooAzure Cosmos DB met behulp van Hallo connector</span><span class="sxs-lookup"><span data-stu-id="74099-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="74099-192">Hoewel Hallo communicatie transport iets gecompliceerder is, is een query uit te voeren van Spark tooAzure Cosmos DB via Hallo-connector aanzienlijk sneller.</span><span class="sxs-lookup"><span data-stu-id="74099-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="74099-193">Hallo volgende codefragment ziet u hoe toouse Hallo-connector in een Spark-context.</span><span class="sxs-lookup"><span data-stu-id="74099-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="74099-194">Zoals vermeld in het codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="74099-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="74099-195">**Azure-cosmosdb-spark** Hallo bevat alle benodigde verbindingsparameters, waaronder Hallo voorkeur locaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="74099-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="74099-196">U kunt bijvoorbeeld Hallo lezen replica en de prioriteit.</span><span class="sxs-lookup"><span data-stu-id="74099-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="74099-197">NET Hallo nodig bibliotheken importeren en configureren van uw hoofdsleutel en host toocreate hello Azure DB die Cosmos-client.</span><span class="sxs-lookup"><span data-stu-id="74099-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="74099-198">Spark-query's via Hallo connector uitvoeren</span><span class="sxs-lookup"><span data-stu-id="74099-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="74099-199">Hallo volgende voorbeeld maakt gebruik van hello Azure DB die Cosmos-exemplaar dat is gemaakt in de vorige codefragment Hallo Hallo met alleen-lezen sleutels opgegeven.</span><span class="sxs-lookup"><span data-stu-id="74099-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="74099-200">Hallo volgende codefragment verbindt toohello DepartureDelays.flights_pcoll verzameling (in hello DoctorWho account zijn als het eerder opgegeven) en een query tooextract-Hallo vluchtgegevens vertraging van vlucht die zijn afwijkend van Seattle wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="74099-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="74099-201">Waarom Hallo Spark tooAzure Cosmos DB connector-implementatie gebruiken?</span><span class="sxs-lookup"><span data-stu-id="74099-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="74099-202">Verbinding maken met Spark tooAzure Cosmos DB via Hallo-connector doorgaans voor scenario's is waarbij:</span><span class="sxs-lookup"><span data-stu-id="74099-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="74099-203">U wilt dat toouse Scala bij te werken tooinclude een Python-wrapper zoals aangegeven [probleem 3: wrapper Python toevoegen en voorbeelden](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="74099-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="74099-204">U hebt een grote hoeveelheid gegevens tootransfer tussen Apache Spark en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="74099-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="74099-205">toogive ziet u een idee van Hallo query performance verschil Hallo [testruns Query wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="74099-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="74099-206">Voorbeeld van gedistribueerde samenvoeging</span><span class="sxs-lookup"><span data-stu-id="74099-206">Distributed aggregation example</span></span>
<span data-ttu-id="74099-207">Deze sectie vindt enkele voorbeelden van hoe u gedistribueerde aggregaties en analytics doen kunt met behulp van Apache Spark en Azure Cosmos DB samen.</span><span class="sxs-lookup"><span data-stu-id="74099-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="74099-208">Azure Cosmos DB al ondersteunt aggregaties, die wordt besproken in Hallo [wereld scale statistische functies met Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="74099-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="74099-209">Hier ziet u hoe u kunt ook het toohello naast niveau met Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="74099-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="74099-210">Deze aggregaties zijn in verwijzing toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="74099-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="74099-211">Verbinding maken met de voorbeeldgegevens tooflights</span><span class="sxs-lookup"><span data-stu-id="74099-211">Connect tooflights sample data</span></span>
<span data-ttu-id="74099-212">Deze voorbeelden aggregatie toegang tot sommige vlucht prestatiegegevens die zijn opgeslagen in onze **DoctorWho** Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="74099-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="74099-213">tooconnect tooit, moet u tooutilize Hallo codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="74099-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="74099-214">In dit fragment zijn ook gaat toorun een base query dat overdrachten set gefilterde gegevens uit Azure Cosmos DB tooSpark Hallo waar Hallo laatste gedistribueerde statistische functies kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="74099-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="74099-215">In dit geval vragen we voor vlucht die van Seattle (SEA afwijken).</span><span class="sxs-lookup"><span data-stu-id="74099-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="74099-216">Hallo zijn volgende resultaten gegenereerd door het Hallo-query's uitvoeren in Hallo Jupyter-notebook service.</span><span class="sxs-lookup"><span data-stu-id="74099-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="74099-217">Houd er rekening mee dat alle Hallo codefragmenten algemeen zijn en zijn niet specifiek tooany service zijn.</span><span class="sxs-lookup"><span data-stu-id="74099-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="74099-218">Actieve LIMIET en het aantal query 's</span><span class="sxs-lookup"><span data-stu-id="74099-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="74099-219">Net zoals u kunt gebruikt tooin SQL/Spark SQL, laten we beginnen met een **LIMIET** query:</span><span class="sxs-lookup"><span data-stu-id="74099-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Spark LIMIET query](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="74099-221">Hallo volgende query is een eenvoudig en snel **aantal** query:</span><span class="sxs-lookup"><span data-stu-id="74099-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Spark COUNT-query](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="74099-223">GROUP BY-query</span><span class="sxs-lookup"><span data-stu-id="74099-223">GROUP BY query</span></span>
<span data-ttu-id="74099-224">In deze volgende set we eenvoudig kunt uitvoeren **GROUP BY** query's op onze Azure DB die Cosmos-database:</span><span class="sxs-lookup"><span data-stu-id="74099-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Spark GROUP BY-query-grafiek](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="74099-226">UNIEK is, ORDER BY-query</span><span class="sxs-lookup"><span data-stu-id="74099-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="74099-227">Hier vindt een **DISTINCT, ORDER BY** query:</span><span class="sxs-lookup"><span data-stu-id="74099-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Spark GROUP BY-query-grafiek](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="74099-229">Doorgaan Hallo vlucht data-analyse</span><span class="sxs-lookup"><span data-stu-id="74099-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="74099-230">U kunt Hallo voorbeeld query's toocontinue analyse van Hallo vluchtgegevens volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="74099-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="74099-231">Top 5 vertraagde bestemmingen (steden) afwijkend van Seattle</span><span class="sxs-lookup"><span data-stu-id="74099-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Spark bovenste vertragingen grafiek](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="74099-233">Berekenen gemiddelde vertragingen door bestemming steden afwijkend van Seattle</span><span class="sxs-lookup"><span data-stu-id="74099-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Spark mediaan vertragingen grafiek](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="74099-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74099-235">Next steps</span></span>

<span data-ttu-id="74099-236">Als u nog niet gedaan hebt, Hallo Spark tooAzure Cosmos DB connector downloaden van Hallo [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub-opslagplaats en aanvullende bronnen in de opslagplaats Hallo Hallo verkennen:</span><span class="sxs-lookup"><span data-stu-id="74099-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* [<span data-ttu-id="74099-237">Voorbeelden van gedistribueerde aggregaties</span><span class="sxs-lookup"><span data-stu-id="74099-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="74099-238">Voorbeelden van Scripts en laptops</span><span class="sxs-lookup"><span data-stu-id="74099-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="74099-239">U kunt ook tooreview hello [Apache Spark SQL, DataFrames en gegevenssets handleiding](http://spark.apache.org/docs/latest/sql-programming-guide.html) en Hallo [Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="74099-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
