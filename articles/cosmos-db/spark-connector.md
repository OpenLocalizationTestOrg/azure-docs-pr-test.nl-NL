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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>Versnellen realtime big data-analyses met Hallo Spark tooAzure Cosmos-DB-connector

Hallo Spark tooAzure Cosmos DB connector kunnen Azure Cosmos DB tooact als invoerbron of uitvoerlocatie voor Apache Spark-taken. Verbinding maken met [Spark](http://spark.apache.org/) te[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) versnelt uw mogelijkheid toosolve snel bewegende gegevenswetenschap problemen waar u Azure Cosmos DB tooquickly kunt behouden en gegevens opvragen. Hallo Spark tooAzure Cosmos-DB-connector maakt efficiënt gebruik Hallo systeemeigen Azure Cosmos DB beheerd indexen. Hallo indexen inschakelen bij te werken kolommen als u analyses uitvoeren en push-down predicaat filteren op basis van snel veranderende globaal gedistribueerd gegevens, die van het Internet der dingen (IoT) toodata wetenschappelijke en analyses scenario's variëren.

Zie voor het werken met Spark GraphX en Hallo Gremlin graph API's van Azure Cosmos DB, [grafiek analyses met behulp van Spark en Apache TinkerPop Gremlin uitvoeren](spark-connector-graph.md).

## <a name="download"></a>Downloaden

tooget gestart, Hallo Spark tooAzure Cosmos DB connector (preview) downloaden van Hallo [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) opslagplaats op GitHub.

## <a name="connector-components"></a>Connector-onderdelen

Hallo-connector maakt gebruik van Hallo volgende onderdelen:

* [Azure Cosmos DB](http://documentdb.com) kunnen klanten tooprovision en schalen zowel doorvoer en opslag via verschillende geografische regio's. Hallo-service biedt:
   * Schakel sleutel [globale distributie](distribute-data-globally.md) en horizontale schaal
   * Gegarandeerd één cijfer latenties op Hallo 99th percentiel
   * [Meerdere goed gedefinieerde consistentie modellen](consistency-levels.md)
   * Hoge beschikbaarheid met mogelijkheden voor multihoming gegarandeerd
   * Alle functies worden ondersteund door de toonaangevende, uitgebreide [serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/cosmos-db) (Sla's).

* [Apache Spark](http://spark.apache.org/) is een krachtige open-source-verwerkingsengine die gebaseerd op snelheid, gebruiksgemak en geavanceerde analyses,.

* [Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) zodat u Apache Spark in de cloud Hallo voor essentiële implementaties implementeren met behulp van kunt [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Officieel ondersteunde versies:

| Onderdeel | Versie |
|---------|-------|
|Apache Spark|2.0+|
| Scala| 2.11|
| Azure DocumentDB Java SDK | 1.10.0 |

In dit artikel helpt u enkele eenvoudige voorbeelden uitvoeren met behulp van Python (via pyDocumentDB) en Hallo Scala-interfaces.

Er zijn twee benaderingen tooconnect Apache Spark en Azure Cosmos DB:
- Gebruik pyDocumentDB via Hallo [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).
- Een Java gebaseerde Spark tooAzure Cosmos-DB-connector maken door het gebruik van Hallo [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).

## <a name="pydocumentdb-implementation"></a>pyDocumentDB-implementatie
huidige Hallo [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) kunt u tooconnect Spark tooAzure Cosmos DB zoals weergegeven in het volgende diagram Hallo:

![Spark tooAzure Cosmos DB gegevensstroom via pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Gegevensstroom van Hallo pyDocumentDB implementatie

Hallo-gegevensstroom is als volgt:

1. Hallo Spark-hoofdknooppunt verbindt toohello Azure Cosmos DB gateway-knooppunt via pyDocumentDB. Een gebruiker geeft alleen Hallo Spark en Azure Cosmos DB-verbindingen. Verbindingen toohello respectieve hoofd- en gateway knooppunten zijn transparante toohello gebruiker.
2. Hallo gateway-knooppunt maakt Hallo-query op Azure Cosmos DB waar Hallo query later wordt uitgevoerd op Hallo verzameling van partities in Hallo gegevensknooppunten. Hallo antwoord voor de query's wordt teruggestuurd toohello gateway-knooppunt en die resultatenset geretourneerd toohello Spark-hoofdknooppunt.
3. Volgende query's (bijvoorbeeld op een Spark-DataFrame) worden verzonden toohello Spark worker-knooppunten voor verwerking.

Communicatie tussen Spark en Azure Cosmos DB is beperkt toohello Spark-hoofdknooppunt en Azure Cosmos DB gateway-knooppunten.  Hallo-query's gaan snel Hallo transportlaag tussen deze twee knooppunten kunt.

### <a name="install-pydocumentdb"></a>PyDocumentDB installeren
U kunt pyDocumentDB in uw Stuurprogrammaknooppunt installeren met behulp van **pip**, bijvoorbeeld:

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>Verbinding maken met Spark tooAzure Cosmos DB via pyDocumentDB
uitvoering van een query uit Spark tooAzure Cosmos DB maakt Hallo eenvoud van Hallo communicatie transport met behulp van pyDocumentDB relatief eenvoudige.

Hallo code codefragment wordt getoond hoe na toouse pyDocumentDB in een Spark-context.

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

Zoals vermeld in het codefragment Hallo:

* Hello Azure Cosmos DB Python SDK (`pyDocumentDB`) Hallo bevat alle benodigde verbindingsparameters Hallo. Hallo voorkeur bijvoorbeeld locaties parameter kiest Hallo lezen replica en de prioriteit.
*  Hallo nodig bibliotheken Importeer en configureer uw **hoofdsleutel** en **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_ client**).


### <a name="execute-spark-queries-via-pydocumentdb"></a>Spark-query's uitvoeren via pyDocumentDB
Hallo volgen voorbeelden gebruik hello Azure DB die Cosmos-exemplaar dat is gemaakt in de vorige codefragment Hallo Hallo met alleen-lezen sleutels opgegeven. Hallo volgende codefragment verbindt toohello **airports.codes** verzameling in hello DoctorWho account zijn als die eerder is opgegeven en wordt een query tooextract Hallo luchthaven steden uitgevoerd in de staat Washington.

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

Nadat het Hallo-query is uitgevoerd **query**, Hallo resultaat is een **query_iterable. QueryIterable** die geconverteerde tooa Python-lijst. Een lijst met Python kan eenvoudig geconverteerde tooa Spark DataFrame met behulp van de volgende code Hallo zijn:

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>Waarom Hallo pyDocumentDB tooconnect Spark tooAzure Cosmos DB gebruiken?
Verbinding maken met Spark tooAzure Cosmos-database met behulp van pyDocumentDB doorgaans voor scenario's is waarbij:

* Wilt u toouse Python.
* U kunt een relatief klein resultaatset uit Azure Cosmos DB tooSpark wilt retourneren. Let op Hallo van onderliggende gegevensset in Azure Cosmos DB kan behoorlijk groot zijn. U zijn filters zijn toegepast, dat wil zeggen, met het predikaat filters uitvoeren in uw Azure Cosmos DB-gegevensbron.  

## <a name="spark-tooazure-cosmos-db-connector"></a>Spark tooAzure Cosmos-DB-connector

Hallo Spark tooAzure Cosmos-DB-connector maakt gebruik van Hallo [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) en worden gegevens verplaatst tussen Hallo Spark worker-knooppunten en Azure Cosmos DB, zoals wordt weergegeven in het volgende diagram Hallo:

![Gegevensoverdracht in Hallo Spark tooAzure Cosmos-DB-connector](./media/spark-connector/spark-connector.png)

Hallo-gegevensstroom is als volgt:

1. Hallo Spark-hoofdknooppunt verbindt toohello Azure Cosmos DB gateway knooppunt tooobtain Hallo partitiekaart. Een gebruiker geeft alleen Hallo Spark en Azure Cosmos DB-verbindingen. Verbindingen toohello respectieve hoofd- en gateway knooppunten zijn transparante toohello gebruiker.
2. Deze informatie wordt verstrekt back toohello Spark-hoofdknooppunt.  Op dit moment moet kunnen tooparse Hallo query toodetermine Hallo-partities en de locaties in Azure Cosmos-database moet u tooaccess.
3. Deze informatie wordt verzonden toohello Spark worker-knooppunten.
4. Hallo Spark worker-knooppunten verbinding toohello Azure Cosmos DB partities direct tooextract Hallo van gegevens en Hallo gegevens toohello Spark partities in Hallo Spark worker-knooppunten retourneren.

Communicatie tussen Spark en Azure Cosmos DB is aanzienlijk sneller Hallo gegevensverplaatsing ligt tussen Hallo Spark worker-knooppunten en hello Azure Cosmos DB gegevensknooppunten (partities).

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>Hallo Spark tooAzure Cosmos-DB-connector maken
Op dit moment Hallo-connector wordt gebruikt maven. toobuild Hallo-connector zonder de afhankelijkheden die u kunt uitvoeren:
```
mvn clean package
```
U kunt ook de meest recente versies Hallo Hallo JAR downloaden van Hallo *releases* map.

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>Hello Azure Cosmos DB Spark JAR opnemen
Voordat u code uitvoert, moet u tooinclude hello Azure Cosmos DB Spark JAR.  Als u van Hallo gebruikmaakt **spark-shell**, en vervolgens u Hallo JAR opnemen kunt met behulp van Hallo **--potten** optie.  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

Als u tooexecute Hallo JAR zonder afhankelijkheden wilt, gebruikt u Hallo code te volgen:

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

Als u een service notebook zoals Azure HDInsight Jupyter-notebook service gebruikt, kunt u Hallo **spark magic** opdrachten:

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

Hallo **potten** opdracht schakelt u tooinclude Hallo twee JARs die nodig zijn voor **azure-cosmosdb-spark** (zelf en hello Azure DocumentDB Java SDK) en wilt uitsluiten **scala-weer** zodat deze niet van invloed op Hallo Livy aanroepen (Jupyter-notebook > Livy > Spark).

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>Verbinding maken met Spark tooAzure Cosmos DB met behulp van Hallo connector
Hoewel Hallo communicatie transport iets gecompliceerder is, is een query uit te voeren van Spark tooAzure Cosmos DB via Hallo-connector aanzienlijk sneller.

Hallo volgende codefragment ziet u hoe toouse Hallo-connector in een Spark-context.

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

Zoals vermeld in het codefragment Hallo:

- **Azure-cosmosdb-spark** Hallo bevat alle benodigde verbindingsparameters, waaronder Hallo voorkeur locaties Hallo. U kunt bijvoorbeeld Hallo lezen replica en de prioriteit.
- NET Hallo nodig bibliotheken importeren en configureren van uw hoofdsleutel en host toocreate hello Azure DB die Cosmos-client.

### <a name="execute-spark-queries-via-hello-connector"></a>Spark-query's via Hallo connector uitvoeren

Hallo volgende voorbeeld maakt gebruik van hello Azure DB die Cosmos-exemplaar dat is gemaakt in de vorige codefragment Hallo Hallo met alleen-lezen sleutels opgegeven. Hallo volgende codefragment verbindt toohello DepartureDelays.flights_pcoll verzameling (in hello DoctorWho account zijn als het eerder opgegeven) en een query tooextract-Hallo vluchtgegevens vertraging van vlucht die zijn afwijkend van Seattle wordt uitgevoerd.

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>Waarom Hallo Spark tooAzure Cosmos DB connector-implementatie gebruiken?

Verbinding maken met Spark tooAzure Cosmos DB via Hallo-connector doorgaans voor scenario's is waarbij:

* U wilt dat toouse Scala bij te werken tooinclude een Python-wrapper zoals aangegeven [probleem 3: wrapper Python toevoegen en voorbeelden](https://github.com/Azure/azure-cosmosdb-spark/issues/3).
* U hebt een grote hoeveelheid gegevens tootransfer tussen Apache Spark en Azure Cosmos DB.

toogive ziet u een idee van Hallo query performance verschil Hallo [testruns Query wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).

## <a name="distributed-aggregation-example"></a>Voorbeeld van gedistribueerde samenvoeging
Deze sectie vindt enkele voorbeelden van hoe u gedistribueerde aggregaties en analytics doen kunt met behulp van Apache Spark en Azure Cosmos DB samen. Azure Cosmos DB al ondersteunt aggregaties, die wordt besproken in Hallo [wereld scale statistische functies met Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/). Hier ziet u hoe u kunt ook het toohello naast niveau met Apache Spark.

Deze aggregaties zijn in verwijzing toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).

### <a name="connect-tooflights-sample-data"></a>Verbinding maken met de voorbeeldgegevens tooflights
Deze voorbeelden aggregatie toegang tot sommige vlucht prestatiegegevens die zijn opgeslagen in onze **DoctorWho** Azure DB die Cosmos-database. tooconnect tooit, moet u tooutilize Hallo codefragment te volgen:

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

In dit fragment zijn ook gaat toorun een base query dat overdrachten set gefilterde gegevens uit Azure Cosmos DB tooSpark Hallo waar Hallo laatste gedistribueerde statistische functies kunt uitvoeren. In dit geval vragen we voor vlucht die van Seattle (SEA afwijken).

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

Hallo zijn volgende resultaten gegenereerd door het Hallo-query's uitvoeren in Hallo Jupyter-notebook service.  Houd er rekening mee dat alle Hallo codefragmenten algemeen zijn en zijn niet specifiek tooany service zijn.

### <a name="running-limit-and-count-queries"></a>Actieve LIMIET en het aantal query 's
Net zoals u kunt gebruikt tooin SQL/Spark SQL, laten we beginnen met een **LIMIET** query:

![Spark LIMIET query](./media/spark-connector/spark-sql-query.png)

Hallo volgende query is een eenvoudig en snel **aantal** query:

![Spark COUNT-query](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>GROUP BY-query
In deze volgende set we eenvoudig kunt uitvoeren **GROUP BY** query's op onze Azure DB die Cosmos-database:

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Spark GROUP BY-query-grafiek](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>UNIEK is, ORDER BY-query
Hier vindt een **DISTINCT, ORDER BY** query:

![Spark GROUP BY-query-grafiek](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>Doorgaan Hallo vlucht data-analyse
U kunt Hallo voorbeeld query's toocontinue analyse van Hallo vluchtgegevens volgende gebruiken:

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>Top 5 vertraagde bestemmingen (steden) afwijkend van Seattle
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Spark bovenste vertragingen grafiek](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>Berekenen gemiddelde vertragingen door bestemming steden afwijkend van Seattle
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Spark mediaan vertragingen grafiek](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>Volgende stappen

Als u nog niet gedaan hebt, Hallo Spark tooAzure Cosmos DB connector downloaden van Hallo [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub-opslagplaats en aanvullende bronnen in de opslagplaats Hallo Hallo verkennen:

* [Voorbeelden van gedistribueerde aggregaties](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [Voorbeelden van Scripts en laptops](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

U kunt ook tooreview hello [Apache Spark SQL, DataFrames en gegevenssets handleiding](http://spark.apache.org/docs/latest/sql-programming-guide.html) en Hallo [Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) artikel.
