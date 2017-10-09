---
title: aaaOperationalize Spark is gebouwd machine learning-modellen | Microsoft Docs
description: Hoe opgeslagen in Azure Blob Storage (WASB) met behulp van Python tooload en score learning-modellen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a>Spark is gebouwd machine learning-modellen operationeel maken
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Dit onderwerp leest hoe toooperationalize een opgeslagen machine learning-model (ML) met behulp van Python op HDInsight Spark-clusters. Hierin wordt beschreven hoe tooload machine learning-modellen die zijn gebouwd met behulp van Spark MLlib en opgeslagen in Azure Blob Storage (WASB) en hoe tooscore ze met gegevenssets die ook in WASB zijn opgeslagen. Er wordt weergegeven hoe toopre proces Hallo invoergegevens, transformatie-onderdelen met de functies voor indexering en codering in Hallo MLlib toolkit en hoe toocreate een gelabelde punt gegevensobject die kan worden gebruikt als invoer voor batchscoreberekening met Hallo ML modellen Hallo. Hallo-modellen gebruikt voor score berekenen bevatten lineaire regressie, Logistic Regression willekeurige Forest modellen en kleurovergang versterking structuur modellen.

## <a name="spark-clusters-and-jupyter-notebooks"></a>Spark-clusters en Jupyter-notebooks
Instellingsstappen en Hallo code toooperationalize ML-model beschikbaar zijn in dit scenario voor het gebruik van een HDInsight Spark 1.6-cluster, evenals een 2.0 Spark-cluster. Hallo-code voor deze procedures is ook beschikbaar in Jupyter-notebooks.

### <a name="notebook-for-spark-16"></a>Laptop voor Spark 1.6
Hallo [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter-notebook ziet u hoe toooperationalize een opgeslagen model met behulp van Python op HDInsight-clusters. 

### <a name="notebook-for-spark-20"></a>Laptop voor Spark 2.0
toomodify hello Jupyter-notebook voor Spark 1.6 toouse met een cluster HDInsight Spark 2.0 vervangen Hallo Python code-bestand met [dit bestand](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py). Deze code laat zien hoe tooconsume Hallo modellen gemaakt in Spark 2.0.


## <a name="prerequisites"></a>Vereisten

1. U moet een Azure-account en een 1.6 Spark (of Spark 2.0) HDInsight-cluster toocomplete in dit scenario. Zie Hallo [overzicht van Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md) voor instructies over het toosatisfy deze vereisten. Dit onderwerp bevat ook een beschrijving van Hallo NYC 2013 Taxi gegevens hier gebruikt en instructies over hoe tooexecute code van een Jupyter-notebook in Spark-cluster Hallo. 
2. Moet u ook maken Hallo machine learning-modellen toobe berekend hier doorloopt Hallo [gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-data-exploration-modeling.md) onderwerp voor Hallo 1.6 Spark-cluster of Hallo Spark 2.0-laptops. 
3. Hallo Spark 2.0-notebooks gebruiken een aanvullende gegevensset voor Hallo classificatietaak Hallo bekende luchtvaartmaatschappij tijdige vertrek gegevensset van 2011 en 2012. Een beschrijving van het Hallo-notitieblokken en -koppelingen toothem vindt u in Hallo [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) voor Hallo GitHub-opslagplaats met ze. Bovendien Hallo code hier en in notitieblokken Hallo gekoppeld is algemeen en moet werken op een Spark-cluster. Als u geen van HDInsight Spark, Hallo clusterinstallatie gebruikmaakt en management stappen mogelijk enigszins afwijken van wat hier moet worden weergegeven. 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Setup: opslaglocaties, bibliotheken en Hallo voorinstelling Spark-context
Spark is kunnen tooread en write tooan Azure Storage-Blob (WASB). Dus een van uw bestaande gegevens opgeslagen kunnen worden verwerkt met Spark en Hallo resultaten WASB opgeslagen opnieuw in.

toosave modellen of bestanden in WASB moet Hallo pad toobe juist opgegeven. Hallo standaard verbonden container toohello Spark-cluster kan worden verwezen met behulp van een pad die begint met: *' wasb / / '*. Hallo volgende codevoorbeeld geeft Hallo locatie van Hallo gegevens toobe lezen en Hallo pad voor Hallo model opslag directory toowhich Hallo model uitvoer wordt opgeslagen. 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Directory-paden voor opslaglocaties in WASB instellen
Modellen worden opgeslagen in: "wasb: / / / gebruiker/remoteuser/NYCTaxi/modellen '. Als dit pad is niet correct ingesteld, worden de modellen niet voor score berekenen geladen.

Hallo scored resultaten zijn opgeslagen: "wasb: / / / gebruiker/remoteuser/NYCTaxi/ScoredResults '. Als Hallo pad toofolder onjuist is, worden resultaten niet opgeslagen in de map.   

> [!NOTE]
> Hallo-bestandslocaties pad kunnen worden gekopieerd en geplakt Hallo tijdelijke aanduidingen in deze code uit de uitvoer van de laatste cel Hallo HALLO hallo **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.   
> 
> 

Hier volgt tooset Hallo-directory codepaden: 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

**UITVOER:**

DateTime.DateTime (2016, 4, 25, 23, 56, 19, 229403)

### <a name="import-libraries"></a>Bibliotheken importeren
Context voor spark instellen en benodigde bibliotheken importeren met de volgende code Hallo

    #IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a>Vooraf context voor Spark en PySpark magics
Hallo PySpark kernels die worden geleverd met Jupyter-notebooks hebben een vooraf ingestelde context. Dus hoeft u niet tooset Hallo Spark of Hive-contexten expliciet voordat u begint te werken met Hallo-toepassing die u ontwikkelt. Dit zijn standaard beschikbaar voor u. Deze contexten zijn:

* SC - voor Spark 
* sqlContext - voor Hive

Hallo PySpark-kernel biedt een aantal vooraf gedefinieerde 'magics', die zijn speciale opdrachten die u met aanroepen kunt %%. Er zijn twee dergelijke opdrachten die worden gebruikt in deze codevoorbeelden.

* **%% lokale** opgegeven Hallo-code in de volgende regels lokaal wordt uitgevoerd. De sitecode moet geldige Python-code.
* **%% sql -o<variable name>** 
* Een Hive-query op Hallo sqlContext worden uitgevoerd. Als het Hallo -o parameter is doorgegeven, Hallo resultaat van Hallo query blijft behouden in Hallo %% lokale Python context als een dataframe Pandas.

Voor meer informatie over het Hallo kernels voor Jupyter-notebooks en vooraf gedefinieerde Hallo 'magics' die ze bieden, Zie [beschikbare Kernels voor Jupyter-notebooks met HDInsight Spark Linux-clusters in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a>Voor het opnemen van gegevens en een kader opgeschoonde gegevens maken
Deze sectie bevat Hallo-code voor een reeks van taken vereist tooingest Hallo gegevens toobe berekend. In een gekoppelde 0,1% voorbeeld van Hallo taxi reis en tarief bestand (opgeslagen als een bestand .tsv), indeling Hallo gegevens te kunnen lezen en maakt vervolgens een frame gegevens wissen.

Hallo taxi reis en tarief dat bestanden op basis zijn gekoppeld op Hallo procedure die is opgegeven de: [Hallo Team gegevens wetenschappelijke processen in actie: met behulp van HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md) onderwerp.

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_test_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER:**

Tijd tooexecute boven cel: 46.37 seconden

## <a name="prepare-data-for-scoring-in-spark"></a>Gegevens voorbereiden voor score berekenen in Spark
Deze sectie wordt beschreven hoe u tooindex, coderen en categorische functies tooprepare ze voor gebruik in MLlib onder supervisie learning-algoritmen voor classificatie en regressie schalen.

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a>Functie transformatie: te indexeren en coderen categorische functies voor invoer in modellen voor score berekenen
Deze sectie wordt beschreven hoe tooindex categorische gegevens met een `StringIndexer` en het coderen van functies met `OneHotEncoder` invoer voor Hallo-modellen.

Hallo [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) coderen van een kolom met tekenreeksen van labels tooa kolom van de label-indexen. Hallo-indexen zijn geordend op label frequenties. 

Hallo [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) een kolom van een label indexen tooa kolom van de binaire aanvalsvectoren, met maximaal één one-waarde wordt toegewezen. Met deze codering kunt algoritmen die continue belangrijke functies, zoals logistic regression verwacht toobe toegepast toocategorical functies.

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER:**

Tijd tooexecute boven cel: 5,37 seconden

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a>RDD objecten met de functie matrices voor invoer in modellen maken
Deze sectie bevat de code die laat zien hoe tooindex categorische gegevens als een RDD object en deze een hot coderen zodat deze gebruikt tootrain en test MLlib logistic regression en modellen op basis van een structuur worden kan. Hallo geïndexeerde gegevens worden opgeslagen in [robuuste gedistribueerd gegevensset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objecten. Dit zijn eenvoudige abstractie Hallo in Spark. Een object RDD vertegenwoordigt een niet-wijzigbaar, gepartitioneerde verzameling van elementen die kunnen worden bediend op, in combinatie met Spark.

Bevat ook code die laat zien hoe de gegevens met tooscale Hallo `StandardScalar` geleverd door MLlib voor gebruik in lineaire regressie met stochastische kleurovergang Daalgradiënt (SGD), een populaire algoritme voor het trainen van een breed scala aan machine learning-modellen. Hallo [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) gebruikte tooscale Hallo functies toounit variantie is. Functie schaal, ook wel bekend als gegevensnormalisatie, weet u zeker dat functies met veel betaald waarden zijn niet opgegeven overmatige afwegen in objective Hallo-functie. 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER:**

Tijd tooexecute boven cel: 11.72 seconden

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a>Hello Logistic Regression-Model beoordelen en uitvoer tooblob opslaan
Hallo-code in deze sectie ziet u hoe tooload een Logistic regressiemodel dat is opgeslagen in Azure blob-opslag en toopredict al dan niet een tip wordt betaald op reis taxi gebruiken, deze met standaard classificatie metrische gegevens te beoordelen en vervolgens opslaan en Hallo resultaten tooblob tekenen opslag. Hallo berekend resultaten worden opgeslagen in RDD objecten. 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**UITVOER:**

Tijd tooexecute boven cel: 19.22 seconden

## <a name="score-a-linear-regression-model"></a>Een lineair regressiemodel beoordelen
We hebben gebruikt [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain een lineair regressiemodel met stochastische kleurovergang Daalgradiënt (SGD) voor optimalisatie toopredict Hallo hoeveelheid tip betaald. 

Hallo-code in deze sectie ziet u hoe tooload een lineair regressiemodel uit Azure blob storage, beoordelen geschaalde variabelen gebruiken en sla Hallo resultaten back toohello blob.

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER:**

Tijd tooexecute boven cel: 16.63 seconden

## <a name="score-classification-and-regression-random-forest-models"></a>Classificatie en regressie willekeurige Forest modellen beoordelen
Hallo-code in deze sectie toont hoe tooload Hallo classificatie opgeslagen en regressie willekeurige Forest modellen opgeslagen in Azure blob-opslag score van de prestaties met standaard classificatie en regressie metingen en sla Hallo resultaten back tooblob opslag.

[Willekeurige forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) ensembles van beslissingsstructuren zijn.  Ze combineren veel decision trees tooreduce Hallo risico te. Willekeurige forests kunnen verwerken categorische functies toohello multiklassen classificatie instelling uitbreiden, hoeven niet functie schalen en kunnen toocapture niet-mogelijkheid tot zijn en interacties functies. Willekeurige forests zijn een van de meest succesvolle Hallo-machine learning-modellen voor de indeling en regressie.

[Spark.mllib](http://spark.apache.org/mllib/) willekeurige forests ondersteunt voor binaire en multiklassen classificatie en voor regressie, continue en categorische functies gebruikt. 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**UITVOER:**

Tijd tooexecute boven cel: 31.07 seconden

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a>Classificatie en regressie kleurovergang versterking structuur modellen beoordelen
Hallo-code in deze sectie ziet u hoe tooload classificatie en regressie kleurovergang versterking structuur modellen uit Azure blob-opslag score van de prestaties met standaard classificatie en regressie metingen en sla Hallo resultaten back tooblob opslag. 

**Spark.mllib** GBTs voor binaire classificatie en voor regressie, met behulp van de functies voor continue en categorische ondersteunt. 

[Kleurovergang versterking structuren](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) ensembles van beslissingsstructuren zijn. GBTs train besluit structuren iteratief toominimize een verlies-functie. GBTs categorische functies kan verwerken, hoeven niet functie schalen en kunnen toocapture niet-mogelijkheid tot zijn en interacties functies. Ze kunnen ook worden gebruikt in een setting multiklasse classificatie.

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER:**

Tijd tooexecute boven cel: 14.6 seconden

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a>Opschonen van objecten uit het geheugen en scored bestandslocaties afdrukken
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


**UITVOER:**

logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt

linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949

randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt

randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt

BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt

BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt

## <a name="consume-spark-models-through-a-web-interface"></a>Spark modellen gebruiken via een webinterface
Spark biedt een mechanisme tooremotely indienen batchtaken of interactieve query's via een REST-interface met een component Livy genoemd. Livy is standaard ingeschakeld op uw HDInsight Spark-cluster. Zie voor meer informatie over Livy: [Spark verzenden van taken op afstand met behulp van Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md). 

U kunt Livy tooremotely verzenden van een taak die door de batch scores een bestand dat is opgeslagen in een Azure-blob en hierna schrijft Hallo resultaten tooanother blob. toodo dit u Python-script op Hallo van uploaden  
[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob van Hallo Spark-cluster. U kunt een hulpprogramma zoals **Microsoft Azure Storage Explorer** of **AzCopy** toocopy Hallo script toohello cluster blob. In ons geval geüpload we Hallo script te***wasb:///example/python/ConsumeGBNYCReg.py***.   

> [!NOTE]
> Hallo toegangstoetsen die u kunt u op Hallo-portal voor Hallo storage-account gekoppeld Hallo Spark-cluster vinden nodig. 
> 
> 

Na het uploaden van toothis locatie dit script wordt uitgevoerd binnen een Spark-cluster Hallo in een gedistribueerde context. Hallo-model geladen en voorspellingen op op basis van model Hallo invoerbestanden wordt uitgevoerd.  

U kunt dit script extern aanroepen door een eenvoudige HTTPS/REST-aanvraag op Livy.  Hier volgt een curl-opdracht tooconstruct Hallo HTTP-aanvraag tooinvoke hello pythonscript op afstand. Vervangen door CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME Hallo juiste waarden voor uw Spark-cluster.

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

U kunt een andere taal op Hallo extern systeem tooinvoke Hallo Spark taak via Livy door het maken van een eenvoudige HTTPS-aanroep met basisverificatie.   

> [!NOTE]
> Het handige toouse Hallo Python aanvragen bibliotheek normaal zou zijn bij het maken van deze aanroep HTTP, maar dit momenteel niet standaard ingeschakeld in Azure Functions is geïnstalleerd. Zodat oudere HTTP-bibliotheken in plaats daarvan worden gebruikt.   
> 
> 

Dit is Hallo Python-code voor Hallo HTTP-aanroep:

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


U kunt ook deze Python-code te toevoegen[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger de verzending van een Spark-taak die een blob scores op basis van verschillende gebeurtenissen, zoals een timer, maken of bijwerken van een blob. 

Als u liever een code gratis Clientervaring, gebruik Hallo [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke Hallo Spark batchscoreberekening met het definiëren van een HTTP-actie op Hallo **Logic Apps Designer** en het instellen van de parameters. 

* Maken vanuit Azure-portal een nieuwe logische App door te selecteren **+ nieuw** -> **Web en mobiel** -> **logische App**. 
* toobring up Hallo **Logic Apps Designer**, voer de naam Hallo Hallo logische App en de App Service-Plan.
* Selecteer een HTTP-actie en Voer Hallo parameters die worden weergegeven in de volgende afbeelding Hallo:

![Logic Apps Designer](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a>Volgende stappen
**Kruisvalidatie en hyperparameter sweeping**: Zie [geavanceerde gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) over de manier waarop modellen kunnen getraind met sweeping kruisvalidatie en hyper-parameter.

