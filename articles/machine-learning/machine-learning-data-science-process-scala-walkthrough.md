---
title: aaaData wetenschappelijke met behulp van Scala en Spark in Azure | Microsoft Docs
description: Hoe Hallo toouse Scala voor bewaakte machine learning-taken met Spark schaalbare MLlib en Spark ML pakketten in een Azure HDInsight Spark-cluster.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a>Gegevenswetenschap met Scala en Spark op Azure
Dit artikel laat zien hoe toouse Scala voor bewaakte machine learning taken met Hallo Spark schaalbare MLlib en Spark ML-pakketten in een Azure HDInsight Spark-cluster. Het wordt u begeleid bij Hallo-taken die deel uitmaken van Hallo [proces voor Gegevenswetenschap](http://aka.ms/datascienceprocess): gegevensopname en verkennen, visualisatie, functie-engineering, modellering en model verbruik. Hallo-modellen in Hallo artikel logistic en lineaire regressie, willekeurige forests en verloop boosted structuren (GBTs) omvatten, maar daarnaast tootwo gemeenschappelijke onder supervisie machine learning taken:

* Regressie probleem: voorspelling van Hallo tip bedrag ($) voor een reis taxi
* Binaire classificatie: voorspelling van tip of geen tip (1/0) voor een reis taxi

Hallo modelleren proces is vereist voor trainings- en evaluatie van een testgegevensset en relevante nauwkeurigheid metrische gegevens. In dit artikel leert u hoe toostore deze modellen Azure Blob storage en hoe tooscore en evalueren hun voorspellende prestaties. In dit artikel omvat tevens Hallo geavanceerdere onderwerpen van hoe toooptimize modellen met behulp van sweeping kruisvalidatie en hyper-parameter. Hallo-gegevens die worden gebruikt, is een voorbeeld van Hallo 2013 NYC taxi reis en tarief gegevensset beschikbaar op GitHub.

[Scala](http://www.scala-lang.org/), een taal die op basis van Hallo virtuele Java-machine, objectgeoriënteerd en functionele Taalconcepten integreert. Het is een schaalbare taal die geschikt toodistributed worden verwerkt in de cloud Hallo en wordt uitgevoerd op Azure Spark-clusters.

[Spark](http://spark.apache.org/) is een open source parallelle verwerking framework die ondersteuning biedt voor in-memory verwerking tooboost Hallo prestaties van toepassingen voor big data-analyses. Hallo Spark-verwerkingsengine is gebouwd voor snelheid, gebruiksgemak en geavanceerde analyses. De Spark in-memory gedistribueerde rekencapaciteiten kunnen u een goede keuze voor zich herhalende algoritmen in machine learning- en grafiekberekeningen. Hallo [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pakket biedt een uniforme set op hoog niveau API's die zijn gebouwd op gegevens frames waarmee u kunnen maken en praktische machine learning-pijplijnen afstemmen. [MLlib](http://spark.apache.org/mllib/) is Spark van schaalbare machine learning-bibliotheek, dat het modellering mogelijkheden toothis gedistribueerde omgeving.

[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure gehoste aanbod van open-source Spark is. Dit omvat ook ondersteuning voor Jupyter Scala notitieblokken op Hallo Spark-cluster, en kunt uitvoeren Spark SQL-tootransform in interactieve query's filteren en opgeslagen in Azure Blob storage-gegevens visualiseren. Hallo Scala codefragmenten in dit artikel die Hallo-oplossingen bieden en de relevante waarnemingspunten Hallo toovisualize Hallo gegevens weergeven in Jupyter-notebooks geïnstalleerd op Hallo Spark-clusters worden uitgevoerd. Hallo modellering stappen in deze onderwerpen hebben die toont u hoe tootrain, evalueren, opslaan en gebruiken ieder soort model code.

Hallo installatiestappen en code in dit artikel zijn voor Azure HDInsight 3.4 Spark 1.6. Hallo echter code in dit artikel en Hallo [Scala Jupyter-Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) algemeen zijn en moet werken op een Spark-cluster. Hallo clusterinstallatie en management stappen mogelijk enigszins afwijken van wat wordt weergegeven in dit artikel als u geen van HDInsight Spark gebruikmaakt.

> [!NOTE]
> Zie voor een onderwerp dat toont hoe toouse Python in plaats van Scala toocomplete taken voor een end-to-end-proces voor Gegevenswetenschap [Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md).
> 
> 

## <a name="prerequisites"></a>Vereisten
* U moet een Azure-abonnement hebben. Als u geen hebt nog, [ophalen van een gratis proefversie van Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* U moet een Azure HDInsight 3.4 Spark 1.6 cluster toocomplete Hallo procedures te volgen. toocreate een cluster, Zie de instructies Hallo in [aan de slag: Apache Spark maken in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Hallo-clustertype en -versie instellen op Hallo **clustertype Selecteer** menu.

![Configuratie van het HDInsight-cluster](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

Zie voor een beschrijving van Hallo NYC taxi reis gegevens en instructies over hoe tooexecute code van een Jupyter-notebook in Spark-cluster Hallo Hallo relevante secties in [overzicht van Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md).  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Scala code uitvoeren van een Jupyter-notebook in Spark-cluster Hallo
U kunt een Jupyter-notebook van hello Azure-portal op te starten. Hallo Spark-cluster op uw dashboard zoeken en klik vervolgens op het tooenter Hallo management-pagina voor uw cluster. Klik vervolgens op **Clusterdashboards**, en klik vervolgens op **Jupyter-Notebook** tooopen Hallo laptop die is gekoppeld aan Hallo Spark-cluster.

![Cluster-dashboard en de Jupyter-notebooks](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

U ook toegang tot Jupyter-notebooks op https://&lt;clustername&gt;.azurehdinsight.net/jupyter. Vervang *clustername* met Hallo-naam van het cluster. Hallo-wachtwoord moet u voor uw administrator-account tooaccess hello Jupyter-notebooks.

![Ga tooJupyter laptops met behulp van de clusternaam Hallo](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

Selecteer **Scala** toosee een map met een paar voorbeelden van voorverpakte laptops die gebruik Hallo PySpark-API. Hallo exploratie modelleren en score Scala.ipynb laptop die Hallo-codevoorbeelden bevat voor dit pakket van Spark onderwerpen vindt u op met [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).

U kunt Hallo notebook rechtstreeks vanuit GitHub toohello Jupyter-Notebook server uploaden in uw Spark-cluster. Klik op uw startpagina Jupyter hello **uploaden** knop. Plak de URL van GitHub (onbewerkte inhoud) Hallo van Hallo Scala laptop in Verkenner hello, en klik vervolgens op **Open**. Hallo Scala notebook is beschikbaar op Hallo URL te volgen:

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>Instellen: Voorinstelling Spark en Hive-contexten, Spark magics en Spark bibliotheken
### <a name="preset-spark-and-hive-contexts"></a>Vooraf ingestelde Spark en Hive-contexten
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


Hallo Spark kernels die worden geleverd met Jupyter-notebooks hebben vooraf ingestelde contexten. U hoeft niet tooexplicitly set Hallo Spark of Hive-contexten voordat u begint te werken met Hallo-toepassing die u ontwikkelt. Hallo vooraf ingestelde contexten is zijn:

* `sc`voor SparkContext
* `sqlContext`voor HiveContext

### <a name="spark-magics"></a>Spark magics
Hallo Spark kernel biedt een aantal vooraf gedefinieerde 'magics', die zijn speciale opdrachten die u met aanroepen kunt `%%`. Twee van deze opdrachten worden gebruikt in de volgende codevoorbeelden Hallo.

* `%%local`Hiermee geeft u op dat Hallo-code in de volgende regels lokaal worden uitgevoerd. Hallo-code moet geldige Scala-code.
* `%%sql -o <variable name>`voert een Hive-query op `sqlContext`. Als hello `-o` parameter is doorgegeven, Hallo resultaat van Hallo query wordt bewaard in Hallo `%%local` Scala context als een tijdskader Spark-gegevens.

Voor meer informatie over Hallo kernels voor Jupyter-notebooks en hun vooraf gedefinieerde 'magics' die u aanroept met `%%` (bijvoorbeeld `%%local`), Zie [beschikbare Kernels voor Jupyter-notebooks met HDInsight Spark Linux-clusters op HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

### <a name="import-libraries"></a>Bibliotheken importeren
Hallo Spark, MLlib en andere bibliotheken die u met behulp van de volgende code Hallo moet importeren.

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a>Gegevensopname
Hallo eerste stap bij het proces voor Gegevenswetenschap hello is tooingest Hallo gegevens die u wilt dat tooanalyze. U brengt Hallo gegevens van externe bronnen of systemen waarin deze zich bevindt in uw gegevens te verkennen en modellering omgeving. In dit artikel is Hallo-gegevens die u wilt opnemen een gekoppelde 0,1% voorbeeld van Hallo taxi reis en tarief bestand (opgeslagen als een bestand .tsv). Hallo-gegevens te verkennen en modellering-omgeving is Spark. Deze sectie bevat Hallo code toocomplete Hallo reeks taken te volgen:

1. Instellen van directory-paden voor opslag van gegevens en het model.
2. Lees in Hallo invoer gegevensset (opgeslagen als een bestand .tsv).
3. Een schema voor Hallo en schone Hallo gegevens definiëren.
4. Een kader opgeschoonde gegevens maken en deze in de cache in het geheugen.
5. Hallo-gegevens als een tijdelijke tabel in SQLContext registreren.
6. Hallo querytabel en Hallo resultaten in een gegevensframe importeren.

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>Directory-paden voor opslaglocaties in Azure Blob-opslag instellen
Spark kunt lezen en schrijven tooAzure Blob-opslag. U kunt een van uw bestaande gegevens Spark tooprocess gebruiken en resultaten op te slaan Hallo opnieuw in de Blob-opslag.

toosave modellen of bestanden in Blob storage, moet u tooproperly Hallo pad opgeven. Verwijzing Hallo standaardcontainer toohello Spark-cluster aangesloten via een pad dat met begint `wasb:///`. Verwijzen naar andere locaties met behulp van `wasb://`.

Hallo geeft volgende codevoorbeeld locatie van de Hallo Hallo invoergegevens toobe lezen en Hallo pad tooBlob opslag die is aangesloten toohello Spark-cluster waarin Hallo model moet worden opgeslagen.

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>Gegevens importeren, maakt u een RDD en een gegevensframe volgens toohello schema definiëren
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Uitvoer:**

Tijd toorun Hallo cel: 8 seconden.

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>Hallo querytabel en resulteert in een gegevensframe importeren
Vervolgens Hallo querytabel voor tarief, passagiers en tip gegevens; de gegevens beschadigd en afgelegen; uitfilteren en afdrukken van meerdere rijen.

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

**Uitvoer:**

| fare_amount | passenger_count | tip_amount | punt |
| --- | --- | --- | --- |
|        13.5 |1.0 |2.9 |1.0 |
|        16.0 |2.0 |3.4 |1.0 |
|        10.5 |2.0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>Gegevensverkenning en visualisatie
Nadat u Hallo gegevens naar Spark overbrengen, is de volgende stap Hallo in Hallo proces voor Gegevenswetenschap toogain een beter begrip van gegevens via de exploratie en visualisatie Hallo. In deze sectie kunt u Hallo taxi gegevens controleren met behulp van SQL-query's. Resultaten van importbewerking Hallo in een frame gegevens tooplot Hallo vervolgens target-variabelen en potentiële functies voor visuele inspectie met Hallo automatisch visualisatie functie van Jupyter.

### <a name="use-local-and-sql-magic-tooplot-data"></a>Lokale en SQL-magic tooplot gegevens gebruiken
Hallo-uitvoer van een codefragment die u vanaf een Jupyter-notebook uitvoert is standaard beschikbaar in de context Hallo van Hallo-sessie die is opgeslagen op Hallo worker-knooppunten. Als u toosave een reis toohello worker-knooppunten voor elke berekeningen wilt, en als alle gegevens die u nodig hebt voor de berekening lokaal beschikbaar op Hallo Jupyter-knooppunt is (dit is het hoofdknooppunt Hallo) hello, kunt u Hallo `%%local` magic toorun Hallo code codefragment op Hallo Jupyter-server.

* **SQL-magic** (`%%sql`). Hallo HDInsight Spark kernel ondersteunt eenvoudig inline HiveQL query's op SQLContext. Hallo (`-o VARIABLE_NAME`) argument als een frame Pandas gegevens op Hallo Jupyter server Hallo-uitvoer van de SQL-query Hallo zich blijft voordoen. Dit betekent waarschijnlijk in de lokale modus Hallo beschikbaar.
* `%%local`**magic**. Hallo `%%local` magic Hallo code wordt lokaal uitgevoerd op Hallo Jupyter-server, waarop Hallo hoofdknooppunt van Hallo HDInsight-cluster. Normaal gesproken gebruikt u `%%local` magische in combinatie met Hallo `%%sql` magische Hello `-o` parameter. Hallo `-o` parameter Hallo-uitvoer van lokaal Hallo SQL-query wilt behouden en vervolgens `%%local` magic zou de volgende set Hallo van code codefragment toorun lokaal tegen Hallo uitvoer Hallo SQL-query's die lokaal wordt bewaard.

### <a name="query-hello-data-by-using-sql"></a>Hallo gegevens opvragen met behulp van SQL
Deze query haalt Hallo taxi reizen door tarief, passagiers aantal, en de tip.

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

Hallo in Hallo code te volgen, `%%local` magic lokale gegevensframe sqlResults maakt. U kunt sqlResults tooplot gebruiken met behulp van matplotlib.

> [!TIP]
> Lokale magic wordt meerdere malen gebruikt in dit artikel. Als uw gegevensset te groot is, Geef een steekproef nemen uit toocreate een gegevensframe dat in het lokale geheugen past.
> 
> 

### <a name="plot-hello-data"></a>Hallo gegevens uitzetten
U kunt met behulp van Python code nadat Hallo gegevensframe in de lokale context als een Pandas gegevensframe is uitzetten.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 Hallo-uitvoer van SQL (HiveQL)-query's visualiseren Hallo Spark kernel automatisch nadat u Hallo code uitvoeren. U kunt kiezen tussen verschillende soorten visualisaties:

* Tabel
* Pie
* Regel
* Onderwerp
* Balk

Hier volgt Hallo code tooplot Hallo gegevens:

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


**Uitvoer:**

![Tip bedrag histogram](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Hoeveelheid op het aantal passagiers Tip](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Tip bedrag door tarief bedrag](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>Functies maken en functies transformeren en vervolgens voorbereiding-gegevens voor de invoer in het modelleren van functies
Voor functies op basis van een structuur modellering van Spark ML en MLlib hebt u tooprepare doel en functies met behulp van tal van technieken zoals binning indexeren, één hot codering en vectorization. Hier volgen Hallo procedures toofollow in deze sectie:

1. Maak een nieuwe functie door **binning** uren in verkeer tijd buckets.
2. Van toepassing **indexeren en één hot codering** toocategorical functies.
3. **Gesplitste en voorbeelden Hallo gegevensset** in trainings- en testset breuken.
4. **Geef variabele training en functies**, en vervolgens maken geïndexeerde of op één hot gecodeerd training en testen invoer gelabelde punt flexibele gegevenssets (RDDs) of gegevensframes gedistribueerd.
5. Automatisch **categoriseren en aan functies en doelen vectorize** toouse als invoer voor machine learning-modellen.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Maakt een nieuwe functie met binning uur in verkeer tijd buckets
Deze code leest u hoe een nieuwe functie door uren in verkeer tijd binning toocreate tijdsintervallen en hoe toocache Hallo resulterende gegevensframe in het geheugen. Wanneer gegevens en RDDs frames herhaaldelijk worden gebruikt, leidt opslaan in cache tooimproved uitvoeringstijden. Dienovereenkomstig, zult u RDDs en gegevens frames cache in verschillende stadia in Hallo procedures te volgen.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>Indexeren en één hot codering van categorische functies
Hallo modelleren en functies van MLlib hebben functies met categorische invoergegevens toobe geïndexeerd of eerdere toouse gecodeerd voorspellen. Deze sectie leest u hoe tooindex of categorische functies voor invoer in Hallo modelleren functies coderen.

U moet tooindex of uw modellen coderen op verschillende manieren, afhankelijk van het Hallo-model. Logistic en lineaire regressie modellen vereisen bijvoorbeeld dat een hot codering. Bijvoorbeeld, kan een onderdeel met drie categorieën worden uitgebreid naar drie kolommen van de functie. 0 of 1, afhankelijk van de categorie van een observatie Hallo bevat elke kolom. MLlib biedt Hallo [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) functie voor het coderen van één hot. Deze encoder wijst een kolom van een label indexen tooa kolom van de binaire vectoren met maximaal één one-waarde. Met deze codering kunnen algoritmen die verwacht dat de numerieke waarden functies, zoals logistic regression toegepaste toocategorical functies zijn.

Hier kunt u tekenreeksen voor tooshow-voorbeelden van het slechts vier variabelen transformeren. U kunt ook andere variabelen, zoals weekdag, vertegenwoordigd door numerieke waarden als categorische variabelen index.

Gebruik voor het indexeren, `StringIndexer()`, en gebruiken voor het coderen van één hot, `OneHotEncoder()` functies van MLlib. Hier volgt Hallo code tooindex en coderen categorische functies:

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Uitvoer:**

Tijd toorun Hallo cel: 4 seconden.

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>Gesplitste en voorbeelden Hallo gegevensset in trainings- en testset breuken
Deze code maakt een willekeurige steekproeven van het Hallo-gegevens (in dit voorbeeld 25%). Hoewel steekproeven niet vereist voor dit voorbeeld vanwege toohello grootte van de gegevensset hello is, Hallo artikel ziet u hoe u kunt een steekproef nemen zodat u weet hoe toouse voor uw eigen problemen wanneer deze nodig is. Als voorbeelden groot zijn, kan dit aanzienlijke tijd besparen tijdens het trainen van modellen. Vervolgens Hallo voorbeeld splitsen in trainings-onderdeel (in dit voorbeeld 75%) en een testen deel toouse in classificatie en regressie modellering (in dit voorbeeld 25%).

Een willekeurig getal (tussen 0 en 1) tooeach rij (in een kolom 'RNG') die gebruikte tooselect kruisvalidatie vouwen tijdens de training kan worden toegevoegd.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Uitvoer:**

Tijd toorun Hallo cel: 2 seconden.

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>Geef variabele training en onderdelen, en maak vervolgens geïndexeerde of op één hot gecodeerd trainings- en testdoeleinden invoer met het label punt RDDs of gegevens frames
Deze sectie bevat de code die u ziet hoe tooindex categorische gegevens als een gelabelde wijst gegevenstype en deze te coderen zodat u kunt deze tootrain en test MLlib logistic regression en andere classificatiemodellen kunnen gebruiken. Gelabelde point-objecten zijn RDDs die zijn geformatteerd op een manier die is vereist als de invoergegevens voor de meeste machine learning-algoritmen in MLlib. Een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is een lokale vector, dense of sparse, die is gekoppeld aan een label/antwoord.

In deze code geeft u (afhankelijke) doelvariabele Hallo en Hallo functies toouse tootrain modellen. Vervolgens maakt u geïndexeerde of één hot gecodeerd trainings- en testdoeleinden invoer met het label punt RDDs of gegevens frames.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Uitvoer:**

Tijd toorun Hallo cel: 4 seconden.

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>Automatisch categoriseren en aan functies en doelen toouse vectorize als invoer voor machine learning-modellen
Spark ML toocategorize Hallo doel en functies toouse in op basis van een structuur modellering functies gebruiken. Hallo code bestaat uit twee taken:

* Maakt een binaire doel voor classificatie door de waarde 0 of 1 tooeach gegevenspunt tussen 0 en 1 toewijzen met behulp van een drempelwaarde van 0,5.
* Automatisch categoriseren functies. Als Hallo aantal afzonderlijke numerieke waarden voor de functies die kleiner is dan 32 is, wordt deze functie wordt gecategoriseerd.

Hier volgt Hallo-code voor deze twee taken.

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>Model van de binaire classificatie: voorspellen of een tip moet worden betaald
In deze sectie maakt maken u drie soorten binaire classificatie modellen toopredict al dan niet een tip moet worden betaald:

* Een **logistic regressiemodel** met behulp van Hallo Spark ML `LogisticRegression()` functie
* Een **classificatie van willekeurige forestmodel** met behulp van Hallo Spark ML `RandomForestClassifier()` functie
* Een **kleurovergang prestatieverbetering classificatie boomstructuur** met behulp van Hallo MLlib `GradientBoostedTrees()` functie

### <a name="create-a-logistic-regression-model"></a>Een logistic regressiemodel maken
Maak vervolgens een logistic regressiemodel met behulp van Hallo Spark ML `LogisticRegression()` functie. U maakt Hallo model bouwen code in een reeks stappen:

1. **Train Hallo model** gegevens met één parameter is ingesteld.
2. **Hallo model evalueren** op een test-gegevensset met metrische gegevens.
3. **Hallo model opslaan** in Blob storage voor toekomstig gebruik.
4. **Hallo-score-model** tegen testgegevens.
5. **Hallo resultaten tekenen** met ontvanger kenmerk (ROC) curven besturingssysteem.

Hier is Hallo-code voor deze procedures:

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

Laden, beoordelen en Hallo resultaten opslaan.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


**Uitvoer:**

ROC op testgegevens 0.9827381497557599 =

Python op lokale Pandas gegevens frames tooplot Hallo ROC-curve gebruiken.

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**Uitvoer:**

![Tip of geen tip ROC-curve](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>Maken van een willekeurige indeling forestmodel
Maak vervolgens een willekeurige forestmodel classificatie met behulp van Hallo Spark ML `RandomForestClassifier()` functioneren en vervolgens Hallo-model op testgegevens evalueren.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


**Uitvoer:**

ROC op testgegevens 0.9847103571552683 =

### <a name="create-a-gbt-classification-model"></a>Een classificatie GBT model maken
Maak vervolgens een classificatie GBT model met behulp van MLlib `GradientBoostedTrees()` functioneren en vervolgens Hallo-model op testgegevens evalueren.

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


**Uitvoer:**

Gebied onder ROC-curve: 0.9846895479241554

## <a name="regression-model-predict-tip-amount"></a>Regressiemodel: tip bedrag voorspellen
In deze sectie maakt maken u twee soorten regressie modellen toopredict Hallo tip bedrag:

* Een **overgegaan lineair regressiemodel** met behulp van Hallo Spark ML `LinearRegression()` functie. U Hallo model opslaan en Hallo-model op testgegevens evalueren.
* Een **structuur regressiemodel verloop versterking** met behulp van Hallo Spark ML `GBTRegressor()` functie.

### <a name="create-a-regularized-linear-regression-model"></a>Een overgegaan lineair regressiemodel maken
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Uitvoer:**

Tijd toorun Hallo cel: 13 seconden.

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


**Uitvoer:**

R-sqr op testgegevens 0.5960320470835743 =

Vervolgens testresultaten query Hallo als een gegevensframe en gebruik AutoVizWidget en matplotlib toovisualize deze.

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

Hallo code maakt een frame lokale gegevens van Hallo query-uitvoer en Hallo van de gegevenspunten. Hallo `%%local` magic maakt een frame lokale gegevens `sqlResults`, die u kunt tooplot matplotlib.

> [!NOTE]
> Deze Spark-magic wordt meerdere malen gebruikt in dit artikel. Als Hallo hoeveelheid gegevens te groot is, moet u een steekproef nemen uit toocreate een gegevensframe dat in het lokale geheugen past.
> 
> 

Waarnemingspunten maken met behulp van Python matplotlib.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

**Uitvoer:**

![Tip bedrag: werkelijk vs. voorspelde](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>Een regressiemodel GBT maken
Een regressiemodel GBT maken met behulp van Hallo Spark ML `GBTRegressor()` functioneren en vervolgens Hallo-model op testgegevens evalueren.

[Structuren verloop boosted](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) ensembles van beslissingsstructuren zijn. GBTs train besluit structuren iteratief toominimize een verlies-functie. U kunt GBTs gebruiken voor regressie en classificatie. Ze categorische functies kunnen verwerken, hoeven niet functie schalen en nonlinearities en functie interacties kunnen vastleggen. Ook kunt u ze in een setting multiklasse classificatie.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


**Uitvoer:**

Test R-sqr is: 0.7655383534596654

## <a name="advanced-modeling-utilities-for-optimization"></a>Hulpprogramma's voor geavanceerde modellering voor optimalisatie
In deze sectie gebruikt u de machine learning-hulpprogramma's die ontwikkelaars vaak voor de optimalisatie van het model gebruikt. U kunt in het bijzonder machine learning-modellen drie verschillende manieren optimaliseren met behulp van de parameter sweeping en kruisvalidatie:

* Hallo gegevens splitsen in train en validatie sets, Hallo model optimaliseren door hyper-parameter sweeping in een trainingset en evalueren in een set validatie (lineaire regressie)
* Hallo model optimaliseren door kruisvalidatie en hyper-parameter verstrekkende met behulp van Spark ML CrossValidator functie (binaire classificatie)
* Hallo model optimaliseren door aangepaste kruisvalidatie en code van de parameter-sweeping toouse een machine learning-functie en de parameter ingesteld (lineaire regressie)

**Kruisvalidatie** is een techniek die hoe goed een op een bekende set gegevens getraind model toopredict Hallo functies van gegevenssets waarop deze is niet getraind wordt generalize evalueert. Hallo is algemeen idee achter deze techniek dat een model wordt getraind van een gegevensset van bekende gegevens, en vervolgens hello nauwkeurigheid van de voorspellingen is getest op basis van een onafhankelijke set van gegevens. Een veelvoorkomende implementatie is toodivide een gegevensset in *k*-vouwen en vervolgens trainen Hallo model round-robin toewijst op alle één Hallo vouwen.

**Hyper-parameter optimalisatie** Hallo probleem van het kiezen van een set van hyper-parameters voor een leeralgoritme meestal met Hallo doel voor het optimaliseren van een meting van Hallo-algoritme op de prestaties van een onafhankelijke set van gegevens. Een hyper-parameter is een waarde die u buiten Hallo model training procedure moet opgeven. Veronderstellingen over hyper-parameterwaarden kunnen beïnvloeden Hallo flexibiliteit en de nauwkeurigheid van het Hallo-model. Beslissingsstructuren hyper-parameters hebben, bijvoorbeeld zoals Hallo gewenste omvang en aantal leaves in Hallo-structuur. U moet een misclassification sancties term voor een vectormachine ondersteuning (SVM) instellen.

Een algemene verbetering van de manier tooperform hyper-parameter is toouse een zoekopdracht raster, ook wel een **parameter vegen**. In een zoekopdracht raster wordt een intensieve zoekactie uitgevoerd via Hallo waarden van een subverzameling van Hallo hyper parameter ruimte voor een leeralgoritme. Kruisvalidatie kan voorzien van een prestaties metrische toosort Hallo optimale resultaten die wordt geproduceerd door Hallo raster zoekalgoritme. Als u kruisvalidatie hyper parameter sweeping gebruikt, kunt u problemen zoals de gegevens van een model tootraining overfitting limiet. Op deze manier Hallo model behoudt Hallo capaciteit tooapply toohello algemene set gegevens vanaf welke Hallo trainingsgegevens is opgehaald.

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>Een lineair regressiemodel met hyper-parameter sweeping optimaliseren
Vervolgens gegevens splitsen in train en validatie sets, gebruik hyper-parameter van een training verstrekkende toooptimize Hallo model instelt en evalueren in een set validatie (lineaire regressie).

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


**Uitvoer:**

Test R-sqr is: 0.6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>Hallo binaire classificatie model optimaliseren door sweeping kruisvalidatie en hyper-parameter
Deze sectie leest u hoe toooptimize een binaire indeling met behulp van kruisvalidatie en hyper-parameter sweeping model. Dit maakt gebruik van Hallo Spark ML `CrossValidator` functie.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Uitvoer:**

Tijd toorun Hallo cel: 33 seconden.

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>Hallo lineair regressiemodel met behulp van aangepaste kruisvalidatie en parameter sweeping code optimaliseren
Vervolgens Hallo model optimaliseren door aangepaste code en beste Modelparameters Hallo identificeren door middel van Hallo criterium van hoogste nauwkeurig. Vervolgens maakt u het laatste model Hallo Hallo-model op testgegevens evalueren en Hallo model niet opslaan in Blob-opslag. Ten slotte Hallo model niet laden, testgegevens beoordelen en evalueren nauwkeurig.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


**Uitvoer:**

Tijd toorun Hallo cel: 61 seconden.

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>Spark is gebouwd machine learning-modellen automatisch met Scala gebruiken
Zie voor een overzicht van onderwerpen die helpt u bij het Hallo-taken die Hallo Gegevenswetenschap proces in Azure omvatten, [Team gegevens wetenschap proces](http://aka.ms/datascienceprocess).

[Gegevens wetenschap proces scenario's in een team](data-science-process-walkthroughs.md) beschrijft andere end-to-end-scenario's die laten zien Hallo stappen voor het Hallo-Team gegevens wetenschappelijke processen voor specifieke scenario's. Hallo-scenario's ook laten zien hoe toocombine cloud en on-premises hulpprogramma's en services in een werkstroom of pijplijn toocreate een intelligente toepassing.

[Score Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md) ziet u hoe toouse Scala code tooautomatically geladen en beoordelen van nieuwe gegevens sets met machine learning-modellen in Spark is gebouwd en opgeslagen in Azure Blob-opslag. U kunt instructies te volgen Hallo die er en vervangt u gewoon Hallo Python-code door Scala code in dit artikel voor geautomatiseerde verbruik.

