---
title: aaaAnalyze Application Insight logboeken met Spark - Azure HDInsight | Microsoft Docs
description: Informatie over hoe toepassing inzicht tooexport tooblob opslag registreert en vervolgens Hallo logboeken met Spark in HDInsight analyseren.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>Application Insights telemetrie logboeken met Spark in HDInsight analyseren

Meer informatie over hoe toouse Spark in HDInsight tooanalyze toepassing inzicht telemetrische gegevens.

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) is een Analyseservice die uw webtoepassingen bewaakt. Telemetriegegevens die zijn gegenereerd door de Application Insights kan geëxporteerde tooAzure opslag zijn. Zodra Hallo gegevens zich in Azure Storage, HDInsight gebruikte tooanalyze mag deze.

## <a name="prerequisites"></a>Vereisten

* Een toepassing die is geconfigureerd toouse Application Insights.

* Als u bekend bent met het maken van een Linux gebaseerde HDInsight-cluster. Zie voor meer informatie [maken Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

  > [!IMPORTANT]
  > Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Een webbrowser.

Hallo zijn volgende resources gebruikt in ontwikkelen en testen van dit document:

* Application Insights-telemetriegegevens is gegenereerd met een [Node.js-web-app geconfigureerd toouse Application Insights](../application-insights/app-insights-nodejs.md).

* Een Spark op basis van Linux in HDInsight-cluster versie 3.5 is gebruikte tooanalyze Hallo gegevens.

## <a name="architecture-and-planning"></a>Architectuur en planning

Hallo volgende diagram illustreert Hallo service architectuur van dit voorbeeld:

![diagram van de gegevens van Application Insights tooblob opslag, en vervolgens wordt verwerkt door Spark in HDInsight](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Azure-opslag

Application Insights kunnen geconfigureerde toocontinuously export telemetrie informatie tooblobs zijn. HDInsight kan vervolgens lezen gegevens opgeslagen in Hallo blobs. Er zijn echter enkele vereisten die u moet volgen:

* **Locatie**: als Hallo Storage-Account en HDInsight zich in verschillende locaties, deze latentie mogelijk verhogen. Het verhoogt ook de kosten, zoals kosten voor uitgaande toegepaste toodata verplaatsen tussen regio's zijn.

    > [!WARNING]
    > Met behulp van een Opslagaccount in een andere locatie dan HDInsight wordt niet ondersteund.

* **BLOB-type**: HDInsight ondersteunt alleen blok-blobs. Application Insights standaard toousing blok-blobs, dus moet werken met HDInsight standaard.

Zie voor informatie over het toevoegen van extra opslagruimte tooan bestaande HDInsight-cluster Hallo [extra opslagaccounts toevoegen](hdinsight-hadoop-add-storage.md) document.

### <a name="data-schema"></a>Gegevensschema

Application Insights biedt [exporteren gegevensmodel](../application-insights/app-insights-export-data-model.md) informatie voor Hallo telemetrie gegevensindeling tooblobs geëxporteerd. Hallo stappen in dit document Spark SQL toowork met Hallo gegevens gebruiken. Spark SQL kan automatisch genereren van een schema voor Hallo JSON-gegevensstructuur is vastgelegd door Application Insights.

## <a name="export-telemetry-data"></a>Exporteren van telemetriegegevens

Volg de stappen Hallo in [configureren met continue Export](../application-insights/app-insights-export-telemetry.md) tooconfigure uw Application Insights tooexport telemetrie informatie tooan Azure storage-blob.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>HDInsight tooaccess Hallo gegevens configureren

Als u een HDInsight-cluster maakt, moet u Hallo-opslagaccount toevoegen tijdens het maken van het cluster.

tooadd hello Azure Storage-Account tooan bestaande cluster, gebruik Hallo informatie in Hallo [extra Opslagaccounts toevoegen](hdinsight-hadoop-add-storage.md) document.

## <a name="analyze-hello-data-pyspark"></a>Hallo gegevens analyseren: PySpark

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw Spark in HDInsight-cluster. Van Hallo **snelkoppelingen** sectie **Clusterdashboards**, en selecteer vervolgens **Jupyter-Notebook** Hallo Cluster Dashboard__ blade.

    ![Hallo clusterdashboards](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. Selecteer in de Hallo rechtsboven Hallo Jupyter pagina, **nieuw**, en vervolgens **PySpark**. Hiermee opent u een nieuw browsertabblad met een Jupyter-Notebook voor op basis van Python.

3. In het eerste veld hello (aangeroepen een **cel**) op pagina Hallo voert u na de tekst hello:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    Deze code configureert Spark toorecursively toegang Hallo-mapstructuur voor Hallo invoergegevens. Application Insights telemetry is vastgelegd tooa directory-structuur lijkt toohello `/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Gebruik **SHIFT + ENTER** toorun Hallo code. Op de linkerkant van de cel Hallo Hallo een '\*' wordt weergegeven tussen vierkante haken-tooindicate Hallo Hallo-code in deze cel wordt uitgevoerd. Nadat deze is voltooid, Hallo '\*' tooa getal en uitvoer vergelijkbare toohello na de tekst wordt weergegeven onder Hallo cel wordt gewijzigd:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Een nieuwe cel wordt gemaakt onder Hallo eerst een. Voer Hallo tekst in de nieuwe cel hello te volgen. Vervang `CONTAINER` en `STORAGEACCOUNT` met hello Azure storage-account en containernaam blob met Application Insights-gegevens.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Gebruik **SHIFT + ENTER** tooexecute deze cel. Er is een resultaat vergelijkbaar toohello volgende tekst:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    Hallo wasb pad geretourneerd is de locatie Hallo Hallo telemetriegegevens Application Insights. Wijziging Hallo `hdfs dfs -ls` regel in Hallo cel toouse hello wasb pad geretourneerd en gebruik vervolgens **SHIFT + ENTER** toorun Hallo cel opnieuw. Deze tijd Hallo resultaten moeten Hallo mappen met telemetrische gegevens worden weergegeven.

   > [!NOTE]
   > Voor Hallo Hallo overige in deze sectie stappen, Hallo `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` directory gebruikt. De directorystructuur van uw zijn anders.

6. Voer in de volgende cel Hallo Hallo code te volgen: Vervang `WASB_PATH` met het pad van de vorige stap Hallo Hallo.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    Deze code maakt een dataframe van Hallo JSON-bestanden is geëxporteerd door Hallo continue exportproces. Gebruik **SHIFT + ENTER** toorun deze cel.
7. In de volgende cel hello, en voert u Hallo na tooview Hallo schema die Spark voor Hallo JSON-bestanden gemaakt uit:

   ```python
   jsonData.printSchema()
   ```

    Hallo-schema voor elk type telemetrie verschilt. Hallo volgende voorbeeld is Hallo-schema dat is gegenereerd voor webaanvragen (opgeslagen gegevens in Hallo `Requests` submap):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. Gebruik Hallo tooregister hello dataframe als een tijdelijke tabel te volgen en een query uitvoert op Hallo gegevens:

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    Deze query retourneert Hallo stad informatie voor de top 20 records Hallo waar context.location.city niet null is.

   > [!NOTE]
   > Hallo context structuur is aanwezig in alle telemetrie vastgelegd door Application Insights. Hallo stad element kan niet worden gevuld in de logboeken. Gebruik Hallo schema tooidentify andere elementen die u kunt een query die gegevens voor uw logboeken kunnen bevatten.

    Deze query retourneert informatie vergelijkbare toohello volgende tekst:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Hallo gegevens analyseren: Scala

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw Spark in HDInsight-cluster. Van Hallo **snelkoppelingen** sectie **Clusterdashboards**, en selecteer vervolgens **Jupyter-Notebook** Hallo Cluster Dashboard__ blade.

    ![Hallo clusterdashboards](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. Selecteer in de Hallo rechtsboven Hallo Jupyter pagina, **nieuw**, en vervolgens **Scala**. Een nieuw browsertabblad met een Scala gebaseerde Jupyter-Notebook wordt weergegeven.
3. In het eerste veld hello (aangeroepen een **cel**) op pagina Hallo voert u na de tekst hello:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    Deze code configureert Spark toorecursively toegang Hallo-mapstructuur voor Hallo invoergegevens. Application Insights telemetrie is vastgelegd tooa directory-structuur lijkt te`/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Gebruik **SHIFT + ENTER** toorun Hallo code. Op de linkerkant van de cel Hallo Hallo een '\*' wordt weergegeven tussen vierkante haken-tooindicate Hallo Hallo-code in deze cel wordt uitgevoerd. Nadat deze is voltooid, Hallo '\*' tooa getal en uitvoer vergelijkbare toohello na de tekst wordt weergegeven onder Hallo cel wordt gewijzigd:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Een nieuwe cel wordt gemaakt onder Hallo eerst een. Voer Hallo tekst in de nieuwe cel hello te volgen. Vervang `CONTAINER` en `STORAGEACCOUNT` met hello Azure storage-accountnaam en de naam van de blob-container met Application Insights-Logboeken.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Gebruik **SHIFT + ENTER** tooexecute deze cel. Er is een resultaat vergelijkbaar toohello volgende tekst:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    Hallo wasb pad geretourneerd is de locatie Hallo Hallo telemetriegegevens Application Insights. Wijziging Hallo `hdfs dfs -ls` regel in Hallo cel toouse hello wasb pad geretourneerd en gebruik vervolgens **SHIFT + ENTER** toorun Hallo cel opnieuw. Deze tijd Hallo resultaten moeten Hallo mappen met telemetrische gegevens worden weergegeven.

   > [!NOTE]
   > Voor Hallo Hallo overige in deze sectie stappen, Hallo `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` directory gebruikt. Deze map bestaat niet, tenzij de telemetriegegevens voor een web-app.

6. Voer in de volgende cel Hallo Hallo code te volgen: Vervang `WASB\_PATH` met het pad van de vorige stap Hallo Hallo.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    Deze code maakt een dataframe van Hallo JSON-bestanden is geëxporteerd door Hallo continue exportproces. Gebruik **SHIFT + ENTER** toorun deze cel.

7. In de volgende cel hello, en voert u Hallo na tooview Hallo schema die Spark voor Hallo JSON-bestanden gemaakt uit:

   ```scala
   jsonData.printSchema
   ```

    Hallo-schema voor elk type telemetrie verschilt. Hallo volgende voorbeeld is Hallo-schema dat is gegenereerd voor webaanvragen (opgeslagen gegevens in Hallo `Requests` submap):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. Gebruik Hallo tooregister hello dataframe als een tijdelijke tabel te volgen en een query uitvoert op Hallo gegevens:

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    Deze query retourneert Hallo stad informatie voor de top 20 records Hallo waar context.location.city niet null is.

   > [!NOTE]
   > Hallo context structuur is aanwezig in alle telemetrie vastgelegd door Application Insights. Hallo stad element kan niet worden gevuld in de logboeken. Gebruik Hallo schema tooidentify andere elementen die u kunt een query die gegevens voor uw logboeken kunnen bevatten.
   >
   >

    Deze query retourneert informatie vergelijkbare toohello volgende tekst:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>Volgende stappen

Zie voor meer voorbeelden van het gebruik van Spark toowork met gegevens en services in Azure Hallo documenten te volgen:

* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-Streaming: Spark in HDInsight voor het bouwen van streamingtoepassingen gebruiken](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

Zie voor informatie over het maken en uitvoeren van Spark toepassingen Hallo documenten te volgen:

* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)
