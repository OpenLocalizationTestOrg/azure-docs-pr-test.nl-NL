---
title: gegevensverkenning aaaAdvanced en modellering met Spark | Microsoft Docs
description: Gebruik van HDInsight Spark toodo gegevensverkenning en kruisvalidatie en hyperparameter optimalisatie van binaire classificatie en regressie modellen trainen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>Met Spark verkennen en modelleren van geavanceerde gegevens
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

In dit scenario maakt gebruik van HDInsight Spark toodo gegevens te verkennen en train binaire classificatie en regressie modellen met behulp van kruisvalidatie en hyperparameter optimalisatie van een steekproef van de NYC Hallo taxi reis en ritbedrag 2013 gegevensset. Dit leidt u door de stappen Hallo Hallo [gegevens wetenschap proces](http://aka.ms/datascienceprocess), end-to-end, met behulp van een HDInsight Spark-cluster gebruikt voor verwerking en Azure blobs toostore Hallo gegevens en het Hallo-modellen. Hallo-proces wordt verkend en gebracht van een Azure Storage-Blob gegevens visualiseren en vervolgens wordt voorbereid Hallo gegevens toobuild voorspellende modellen. Python is gebruikte toocode Hallo-oplossing en tooshow Hallo relevante waarnemingspunten. Deze modellen zijn samenstellen met Hallo Spark MLlib toolkit toodo binaire classificatie en regressie modelleren van taken. 

* Hallo **binaire classificatie** taak toopredict is al dan niet een tip voor Hallo reis wordt betaald. 
* Hallo **regressie** taak toopredict Hallo hoeveelheid Hallo tip op basis van andere functies tip is. 

Hallo modellering stappen bevatten ook een code die laat zien hoe tootrain, evalueren en opslaan van elk type model. Hallo onderwerp worden enkele van dezelfde als Hallo gemalen Hallo [gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-data-exploration-modeling.md) onderwerp. Maar deze is 'geavanceerder' in de betreffende kruisvalidatie worden ook gebruikt met hyperparameter verstrekkende tootrain optimaal nauwkeurige classificatie en regressie-modellen. 

**Kruisvalidatie (k/l)** is een techniek die evalueert hoe goed een op een bekende set gegevens getraind model generaliseert toopredicting Hallo functies van gegevenssets waarop deze is niet getraind.  Een veelvoorkomende implementatie hier gebruikt toodivide is een gegevensset in K vouwen en vervolgens train model Hallo round-robin toewijst op alle één Hallo vouwen. Hallo mogelijkheid van Hallo model tooprediction nauwkeurig wanneer Hallo onafhankelijke gegevensset in dit model vouwen niet gebruikt tootrain Hallo getest wordt beoordeeld.

**Hyperparameter optimalisatie** Hallo probleem van het kiezen van een reeks hyperparameters voor een leeralgoritme meestal met Hallo doel voor het optimaliseren van een meting van Hallo-algoritme op de prestaties van een onafhankelijke set van gegevens. **Hyperparameters** zijn waarden die buiten Hallo model training procedure moeten worden opgegeven. Veronderstellingen over deze waarden kunnen invloed hebben op Hallo flexibiliteit en de nauwkeurigheid van het Hallo-modellen. Beslissingsstructuren hebben bijvoorbeeld hyperparameters, zoals Hallo gewenste omvang en aantal leaves in Hallo-structuur. Ondersteuning Vector Machines (SVMs) vereist dat een misclassification sancties term. 

Een algemene hyperparameter optimalisatie voor manier tooperform hier gebruikt, wordt een zoekopdracht raster of een **parameter vegen**. Dit proces bestaat uit het uitvoeren van een intensieve zoekactie via Hallo waarden een subverzameling van Hallo hyperparameter ruimte voor een leeralgoritme. Cross-validatie kan voorzien van een prestaties metrische toosort Hallo optimale resultaten die wordt geproduceerd door Hallo raster zoekalgoritme. K/l gebruikt met hyperparameter ingrijpende helpt limiet problemen zoals de gegevens van een model tootraining overfitting zodat hello model behoudt Hallo capaciteit tooapply toohello algemene set gegevens vanaf welke Hallo trainingsgegevens is opgehaald.

Hallo modellen we gebruiken omvatten logistic en lineaire regressie, willekeurige forests en kleurovergang gestimuleerd structuren:

* [Lineaire regressie met SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is een lineair regressiemodel die gebruikmaakt van een methode stochastische kleurovergang Daalgradiënt (SGD) en voor optimalisatie en het onderdeel schalen toopredict Hallo tip bedragen betaald. 
* [Logistic regression met LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) of regressie 'logit', is een regressiemodel dat kan worden gebruikt wanneer Hallo afhankelijke variabele categorische toodo gegevensclassificatie is. LBFGS is een quasi toegepast optimalisatie-algoritme dat benadert Hallo Broyden – Fletcher – Goldfarb – Shanno (BFGS) algoritme met een beperkte hoeveelheid computergeheugen en die wordt veel gebruikt in machine learning.
* [Willekeurige forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) ensembles van beslissingsstructuren zijn.  Ze combineren veel decision trees tooreduce Hallo risico te. Willekeurige forests worden gebruikt voor regressie en classificatie en categorische functies kunnen verwerken en toohello multiklassen classificatie instelling kunnen worden uitgebreid. Ze hoeven niet functie schalen en weet kunnen toocapture niet-mogelijkheid tot en interactie van de functie. Willekeurige forests zijn een van de meest succesvolle Hallo-machine learning-modellen voor de indeling en regressie.
* [Verloop boosted structuren](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) ensembles van beslissingsstructuren zijn. GBTs train besluit structuren iteratief toominimize een verlies-functie. GBTs worden gebruikt voor regressie en classificatie en categorische functies kan verwerken, hoeven niet functie schalen en kunnen toocapture niet-mogelijkheid tot zijn en interacties functies. Ze kunnen ook worden gebruikt in een setting multiklasse classificatie.

Voorbeelden met k/l en Hyperparameter modelleren vegen voor Hallo binair klassificatieprobleem worden weergegeven. Eenvoudiger voorbeelden (zonder de parameter krijgen) worden op Hallo hoofdonderwerp voor regressie taken weergegeven. Maar in Hallo-bijlage validatie met elastische net voor lineaire regressie en k/l met het gebruik van parameter vegen voor willekeurige forest regressie ook worden weergegeven. Hallo **elastische net** is een overgegaan regressiemethode voor het aanpassen van de lineaire regressie die lineair modellen combineert Hallo L1 en L2 metrische gegevens als sancties Hallo [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) en [gleuf](https://en.wikipedia.org/wiki/Tikhonov_regularization) methoden.   

> [!NOTE]
> Hoewel Hallo Spark MLlib toolkit ontworpen toowork op grote gegevenssets is, wordt hier een voorbeeld van een relatief klein (ongeveer 30 Mb met behulp van 170K rijen, ongeveer 0,1% van de oorspronkelijke NYC gegevensset Hallo) gebruikt voor het gemak. Hallo oefening hier opgegeven efficiënt (in ongeveer 10 minuten) op een HDInsight-cluster met 2 worker-knooppunten wordt uitgevoerd. Hallo kan dezelfde code bevatten, met kleine wijzigingen worden gebruikt tooprocess grotere gegevenssets-wordt met de juiste wijzigingen voor het cachen van gegevens in het geheugen en Hallo clustergrootte wijzigen.
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>Instellen: De Spark-clusters en laptops
Instellingsstappen en code vindt u in dit scenario voor het gebruik van een HDInsight Spark 1.6. Maar Jupyter-notebooks zijn opgegeven voor zowel HDInsight Spark 1.6 en 2.0 Spark-clusters. Een beschrijving van het Hallo-notitieblokken en -koppelingen toothem vindt u in Hallo [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) voor Hallo GitHub-opslagplaats met ze. Bovendien Hallo code hier en in notitieblokken Hallo gekoppeld is algemeen en moet werken op een Spark-cluster. Als u geen van HDInsight Spark, Hallo clusterinstallatie gebruikmaakt en management stappen mogelijk enigszins afwijken van wat hier moet worden weergegeven. Voor het gemak vindt hier u koppelingen toohello Jupyter-notebooks voor Spark 1.6 en 2.0 toobe uitvoeren in de pyspark-kernel Hallo Hallo Jupyter-Notebook server Hallo:

### <a name="spark-16-notebooks"></a>Spark 1.6 laptops

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): bevat onderwerpen in de notebook #1 en de ontwikkeling van het model met hyperparameter afstemmen en kruisvalidatie.

### <a name="spark-20-notebooks"></a>Spark 2.0-laptops

[Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): dit bestand bevat informatie over hoe tooperform gegevensverkenning, modelleren en scores in 2.0 Spark-clusters.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Setup: opslaglocaties, bibliotheken en Hallo voorinstelling Spark-context
Spark is kunnen tooread en write tooAzure Storage-Blob (ook wel bekend als WASB). Dus een van uw bestaande gegevens opgeslagen kunnen worden verwerkt met Spark en Hallo resultaten WASB opgeslagen opnieuw in.

toosave modellen of bestanden in WASB moet Hallo pad toobe juist opgegeven. Hallo standaard verbonden container toohello Spark-cluster kan worden verwezen met behulp van een pad die begint met: ' wasb: / / / '. Andere locaties wordt verwezen door ' wasb: / / '.

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Directory-paden voor opslaglocaties in WASB instellen
Hallo volgende codevoorbeeld wordt Hallo locatie van Hallo gegevens toobe lezen en Hallo pad voor Hallo model opslag directory toowhich Hallo model uitvoer wordt opgeslagen:

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**UITVOER**

DateTime.DateTime (2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>Bibliotheken importeren
Benodigde bibliotheken met de volgende code Hallo importeren:

    # LOAD PYSPARK LIBRARIES
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
Hallo PySpark kernels die worden geleverd met Jupyter-notebooks hebben een vooraf ingestelde context. Dus hoeft u niet tooset Hallo Spark of Hive-contexten expliciet voordat u begint te werken met Hallo-toepassing die u ontwikkelt. Deze contexten zijn standaard voor u beschikbaar. Deze contexten zijn:

* SC - voor Spark 
* sqlContext - voor Hive

Hallo PySpark-kernel biedt een aantal vooraf gedefinieerde 'magics', die zijn speciale opdrachten die u met aanroepen kunt %%. Er zijn twee dergelijke opdrachten die worden gebruikt in deze codevoorbeelden.

* **%% lokale** geeft aan dat Hallo-code in de volgende regels toobe lokaal wordt uitgevoerd. De sitecode moet geldige Python-code.
* **%% sql -o <variable name>**  een Hive-query op Hallo sqlContext wordt uitgevoerd. Als het Hallo -o parameter is doorgegeven, Hallo resultaat van Hallo query blijft behouden in Hallo %% lokale Python context als een DataFrame Pandas.

Voor meer informatie over het Hallo kernels voor Jupyter-notebooks en vooraf gedefinieerde Hallo 'magics' die ze bieden, Zie [beschikbare Kernels voor Jupyter-notebooks met HDInsight Spark Linux-clusters in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Gegevensopname van een openbare blob:
Hallo is eerste stap in Hallo gegevens wetenschap proces tooingest Hallo gegevens toobe geanalyseerd van bronnen waarin deze zich in uw gegevens te verkennen en modellering omgeving bevindt. Deze omgeving is Spark in dit scenario. Deze sectie bevat Hallo code toocomplete een reeks taken:

* Hallo gegevens voorbeeld toobe gemodelleerd opnemen
* Lees in invoergegevensset hello (opgeslagen als een bestand .tsv)
* indeling en schone Hallo-gegevens
* maken en objecten (RDDs of gegevens frames) in het geheugen in de cache
* registreren als een temp-tabel in SQL-context.

Hier volgt Hallo-code voor gegevensopname.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
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

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER**

Tijd tooexecute boven cel: 276.62 seconden

## <a name="data-exploration--visualization"></a>Gegevensverkenning & visualisatie
Zodra het Hallo-gegevens weer in Spark, is hello volgende stap in Hallo gegevens wetenschap proces toogain dieper inzicht Hallo gegevens via de exploratie en visualisatie. In deze sectie bekijken we Hallo taxi gegevens met behulp van SQL-query's en tekent Hallo target-variabelen en potentiële functies voor visuele controle. In het bijzonder uitzetten we Hallo frequentie van de passagiers tellingen in taxi reizen, Hallo frequentie van tip bedragen en hoe tips is afhankelijk van de hoeveelheid betaling en het type.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Een histogram van passagiers aantal frequenties in voorbeeld van taxi reizen Hallo tekenen
Deze code en de volgende codefragmenten SQL magische tooquery Hallo voorbeeld en lokale magische tooplot Hallo gegevens gebruiken.

* **SQL-magic (`%%sql`)** hello HDInsight PySpark-kernel ondersteunt eenvoudig inline HiveQL query's op Hallo sqlContext. Hallo (-o naam_variabele) argument als een DataFrame Pandas op Hallo Jupyter server Hallo-uitvoer van de SQL-query Hallo zich blijft voordoen. Dit betekent dat deze beschikbaar zijn in de lokale modus Hallo.
* Hallo  **`%%local` magic** is toorun code lokaal op Hallo Jupyter-server, waarop Hallo headnode van Hallo HDInsight-cluster wordt gebruikt. Normaal gesproken gebruikt u `%%local` magische na Hallo `%%sql -o` magic gebruikte toorun een query is. Hallo -o parameter zou blijven behouden Hallo-uitvoer van lokaal Hallo SQL-query. Vervolgens Hallo `%%local` magische triggers Hallo volgende reeks code codefragmenten toorun lokaal tegen Hallo uitvoer Hallo SQL-query's die lokaal is opgeslagen. Hallo-uitvoer wordt automatisch weergegeven nadat u Hallo code uitvoeren.

Deze query haalt Hallo reizen op het aantal van de passagiers. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


Deze code maakt een lokale gegevens tijdskader van Hallo query-uitvoer en Hallo van de gegevenspunten. Hallo `%%local` magic maakt een lokale gegevens-frame, `sqlResults`, die kan worden gebruikt voor het uitzetten van matplotlib. 

> [!NOTE]
> Deze PySpark-magic wordt meerdere malen gebruikt in dit scenario. Als Hallo hoeveelheid gegevens te groot is, moet u een steekproef nemen uit toocreate een gegevens-frame dat in het lokale geheugen past.
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Hier volgt Hallo code tooplot Hallo reizen door passagiers aantallen

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**UITVOER**

![Frequentie van reizen op het aantal passagiers](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

U kunt kiezen uit verschillende soorten visualisaties (tabel-, cirkel, regel, gebied of balk) met behulp van Hallo **Type** menuknoppen in Hallo notebook. Hallo-balk tekent wordt hier weergegeven.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Zet een histogram van de tip bedragen en hoe tip bedrag hangt af van de passagiers telling en het tarief bedragen.
Gebruik een SQL-query toosample gegevens...

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


Deze codecel Hallo SQL-query toocreate drie waarnemingspunten Hallo gegevens gebruikt.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**UITVOER:** 

![Tip bedragdistributie](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Hoeveelheid op het aantal passagiers Tip](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Tip bedrag door tarief bedrag](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Functie-engineering, transformatie en gegevens voorbereiding voor modellering
Deze sectie wordt beschreven en vindt Hallo-code voor de procedures gebruikt tooprepare gegevens voor gebruik in ML-model. Er wordt weergegeven hoe toodo Hallo volgende taken:

* Maken van een nieuwe functie door uren in verkeer tijd opslaglocaties partitioneren
* Index en categorische functies op hot coderen
* Gelabelde point-objecten voor invoer in ML functies maken
* Onderliggende steekproeven van Hallo gegevens maken en deze te splitsen in trainings- en testdoeleinden sets
* Functie schalen
* Cacheobjecten in het geheugen

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>Een nieuwe functie maken door het verkeer keren in opslaglocaties partitioneren
Deze code laat zien hoe toocreate een nieuwe functie door het partitioneren van verkeer een time-out in opslaglocaties en hoe toocache Hallo resulterende gegevensframe in het geheugen. Opslaan in cache leidt tooimproved uitvoeringstijd waar flexibele gegevenssets gedistribueerd (RDDs) en gegevens frames herhaaldelijk worden gebruikt. Dus cache we RDDs en gegevensframes in verschillende stadia in dit scenario.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**UITVOER**

126050

### <a name="index-and-one-hot-encode-categorical-features"></a>Index en één hot categorische functies coderen
Deze sectie wordt beschreven hoe tooindex of categorische functies voor invoer in Hallo modelleren functies coderen. Hallo modelleren en functies van MLlib vereist dat functies met categorische invoergegevens worden geïndexeerd of worden gecodeerd voorspellen voorafgaande toouse. 

Afhankelijk van het Hallo-model tooindex of u ze op verschillende manieren te coderen. Bijvoorbeeld: Logistic en lineaire regressie modellen vereisen een hot codering, waarbij, bijvoorbeeld, een onderdeel met drie categorieën kan worden uitgebreid naar drie kolommen van de functie, waarbij elke met 0 of 1, afhankelijk van de categorie van een observatie Hallo. MLlib biedt [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) werken toodo één hot codering. Deze encoder wijst een kolom van een label indexen tooa kolom van de binaire aanvalsvectoren, met maximaal één one-waarde. Met deze codering kunt algoritmen die verwacht dat de numerieke waarden functies, zoals logistic regression toobe toegepast toocategorical functies.

Hier volgt Hallo code tooindex en coderen categorische functies:

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
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

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER**

Tijd tooexecute boven cel: 3.14 seconden

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Gelabelde point-objecten voor invoer in ML functies maken
Deze sectie bevat de code die laat zien hoe tooindex categorische tekst als gegevens van een gelabelde gegevenstype en hoe tooencode deze. Hiermee wordt het voorbereid toobe gebruikt tootrain en test MLlib logistic regression en andere classificatie-modellen. Gelabelde point-objecten zijn robuuste gedistribueerd gegevenssets (RDD) geformatteerd op een manier die is vereist als de invoergegevens voor de meeste ML algoritmen in MLlib. Een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is een lokale vector, dense of sparse, die is gekoppeld aan een label/antwoord.

Hier volgt Hallo code tooindex en het coderen van tekstfuncties voor binaire classificatie.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


Hier volgt Hallo code tooencode en index categorische tekst-functies voor lineaire regressie-analyse.

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Onderliggende steekproeven van Hallo gegevens maken en deze te splitsen in trainings- en testdoeleinden sets
Deze code maakt een willekeurige steekproeven van het Hallo-gegevens (25% wordt hier gebruikt). Hoewel dit niet vereist voor dit voorbeeld vanwege toohello grootte van de gegevensset hello, ziet u hoe u kunt voorbeeldgegevens Hallo hier. Weet u hoe toouse voor uw eigen probleem indien nodig. Als voorbeelden groot zijn, kan dit aanzienlijke tijd tijdens de training modellen opslaan. Naast splitsen we Hallo voorbeeld in trainings-onderdeel (hier 75%) en een test toouse deel (25% hier) in de classificatie en regressie modellering.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER**

Tijd tooexecute boven cel: 0.31 seconden

### <a name="feature-scaling"></a>Functie schalen
Functie schaal, ook wel bekend als gegevensnormalisatie, weet u zeker dat functies met veel betaald waarden zijn niet opgegeven overmatige afwegen in objective Hallo-functie. Hallo code voor het schalen van de functie maakt gebruik van Hallo [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale Hallo functies toounit variantie. Het wordt geleverd door MLlib voor gebruik in lineaire regressie met stochastische kleurovergang Daalgradiënt (SGD). SGD is een populair algoritme voor het trainen van een breed scala aan andere machine learning-modellen zoals overgegaan regressies of ondersteuning vector machines (SVM).   

> [!TIP]
> We hebben gevonden Hallo LinearRegressionWithSGD algoritme toobe gevoelige toofeature schalen.   
> 
> 

Hier volgt Hallo code tooscale variabelen voor gebruik met Hallo overgegaan lineaire SGD algoritme.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER**

Tijd tooexecute boven cel: 11.67 seconden

### <a name="cache-objects-in-memory"></a>Cacheobjecten in het geheugen
Hallo gebruikte tijd voor trainings- en testen van ML algoritmen kan worden verkleind door het opslaan in cache Hallo invoergegevens frame objecten gebruikt voor classificatie, regressie en uitgebreide functies.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER** 

Tijd tooexecute boven cel: 0.13 seconden

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Voorspellen of een tip wordt betaald met binaire classificatie modellen
Deze sectie wordt beschreven hoe gebruik drie modellen voor Hallo binaire classificatietaak van het voorspellen van al dan niet een tip voor een reis taxi wordt betaald. Hallo-modellen die zijn gepresenteerd zijn:

* Logistic regression 
* Willekeurige forest
* Kleurovergang prestatieverbetering structuren

Elk model bouwen sectie code opgedeeld in stappen: 

1. **Training model** gegevens met één parameterset
2. **Evaluatie model** op een test-gegevensset met metrische gegevens
3. **Opslaan van model** in blob voor toekomstige verbruik

Laten we zien hoe toodo kruisvalidatie (k/l) met de parameter verstrekkende op twee manieren:

1. Met behulp van **algemene** aangepaste code die toegepast tooany-algoritme in MLlib en tooany parameter worden kan wordt ingesteld in een algoritme. 
2. Met behulp van Hallo **pySpark CrossValidator pijplijn functie**. Houd er rekening mee dat CrossValidator enkele beperkingen voor Spark 1.5.0 heeft: 
   
   * Pijplijn modellen mag niet zijn opgeslagen/persistent voor toekomstig gebruik.
   * Kan niet worden gebruikt voor elke parameter in een model.
   * Kan niet worden gebruikt voor elk algoritme MLlib.

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>Algemene cross-validatie en hyperparameter sweeping gebruikt met Hallo logistic regression-algoritme voor binaire classificatie
Hallo-code in deze sectie ziet u hoe tootrain, evalueren en opslaan van een regressiemodel logistic met [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) die voorspelt al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald. Hallo model wordt getraind met kruisverwijzingen validatie (k/l) en hyperparameter sweeping met aangepaste code die toegepaste tooany Hallo learning-algoritmen in MLlib kan worden geïmplementeerd.   

> [!NOTE]
> Hallo-uitvoering van deze aangepaste k/l-code kan enkele minuten duren.
> 
> 

**Hallo logistic regression-model met k/l en hyperparameter sweeping trainen**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER**

Coëfficiënten: [0.0082065285375,-0.0223675576104,-0.0183812028036, -3.48124578069e-05,-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]

Intercept:-0.0111216486893

Tijd tooexecute boven cel: 14.43 seconden

**Hallo binaire classificatie model met standaard metrische gegevens evalueren**

Hallo-code in deze sectie laat zien hoe tooevaluate een logistic regression model op basis van een test-gegevensset, met inbegrip van tekent Hallo ROC-curve.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER**

Gebied onder PR 0.985336538462 =

Gebied onder ROC 0.983383274312 =

Samenvattende statistieken

Precisie 0.984174341679 =

Intrekken 0.984174341679 =

F1 Score 0.984174341679 =

Tijd tooexecute boven cel: 2.67 seconden

**Hallo ROC-curve wordt getekend.**

Hallo *predictionAndLabelsDF* is geregistreerd als een tabel, *tmp_results*, in de vorige cel Hallo. *tmp_results* kunnen worden gebruikt toodo query's en resultaten in Hallo sqlResults data-frame voor het uitzetten van de uitvoer. Hier volgt Hallo-code.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Hier volgt Hallo code toomake voorspellingen en tekent Hallo ROC-curve.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


**UITVOER**

![Logistic regression ROC-curve voor algemene methode](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**Model in een blob voor toekomstige consumptie behouden**

Hallo-code in deze sectie laat zien hoe toosave hello logistic regression voor het model.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**UITVOER**

Tijd tooexecute boven cel: 34.57 seconden

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>Gebruik van MLlib CrossValidator pipeline-functie met logistic regressiemodel (elastische regressie)
Hallo-code in deze sectie ziet u hoe tootrain, evalueren en opslaan van een regressiemodel logistic met [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) die voorspelt al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald. Hallo model wordt getraind met cross-validatie (k/l) en hyperparameter sweeping geïmplementeerd Hello MLlib CrossValidator pipeline-functie voor k/l met parameter vegen.   

> [!NOTE]
> Hallo-uitvoering van deze code MLlib k/l kan enkele minuten duren.
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**UITVOER**

Tijd tooexecute boven cel: 107.98 seconden

**Hallo ROC-curve wordt getekend.**

Hallo *predictionAndLabelsDF* is geregistreerd als een tabel, *tmp_results*, in de vorige cel Hallo. *tmp_results* kunnen worden gebruikt toodo query's en resultaten in Hallo sqlResults data-frame voor het uitzetten van de uitvoer. Hier volgt Hallo-code.

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

Hier volgt Hallo code tooplot Hallo ROC-curve.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


**UITVOER**

![Logistic regression ROC-curve met behulp van MLlib CrossValidator](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>Classificatie van willekeurige forest
Hallo-code in deze sectie laat zien hoe tootrain, evalueren en opslaan van een willekeurige forest regressie die voorspelt al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER**

Gebied onder ROC 0.985336538462 =

Tijd tooexecute boven cel: 26.72 seconden

### <a name="gradient-boosting-trees-classification"></a>Kleurovergang prestatieverbetering structuren classificatie
Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een kleurovergang prestatieverbetering structuren model die al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald voorspelt opslaat.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER**

Gebied onder ROC 0.985336538462 =

Tijd tooexecute boven cel: 28.13 seconden

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>Tip bedrag voorspellen met regressie modellen (niet via k/l)
Deze sectie wordt beschreven hoe gebruik drie modellen voor Hallo regressie taak: Hallo tip aankoopbedrag voor een taxi reis op basis van andere functies tip voorspellen. Hallo-modellen die zijn gepresenteerd zijn:

* Lineaire regressie overgegaan
* Willekeurige forest
* Kleurovergang prestatieverbetering structuren

Deze modellen zijn in Hallo inleiding beschreven. Elk model bouwen sectie code opgedeeld in stappen: 

1. **Training model** gegevens met één parameterset
2. **Evaluatie model** op een test-gegevensset met metrische gegevens
3. **Opslaan van model** in blob voor toekomstige verbruik   

> AZURE Opmerking: Kruisvalidatie wordt niet gebruikt met Hallo drie regressie modellen in deze sectie, omdat dit is weergegeven in de details voor Hallo logistic regression-modellen. Een voorbeeld weergegeven hoe toouse k/l met elastische Net voor lineaire regressie wordt verstrekt in Hallo bijlage van dit onderwerp.
> 
> AZURE Opmerking: In onze ervaring kunnen er problemen optreden bij convergentie van LinearRegressionWithSGD modellen en parameters moeten toobe gewijzigd/geoptimaliseerd zorgvuldig voor het verkrijgen van een geldig model. Schalen van variabelen aanzienlijk helpt bij convergentie. Elastische net regressie wordt weergegeven in Hallo bijlage toothis onderwerp kan ook worden gebruikt in plaats van LinearRegressionWithSGD.
> 
> 

### <a name="linear-regression-with-sgd"></a>Lineaire regressie met SGD
Hallo code in deze sectie toont hoe toouse geschaald functies tootrain een lineaire regressie die stochastische kleurovergang daalgradiënt (SGD), kunnen worden gebruikt en hoe tooscore, evalueren en Hallo-model opslaan in Azure Blob Storage (WASB).

> [!TIP]
> In onze ervaring kunnen er problemen met het Hallo-convergentie van LinearRegressionWithSGD modellen en parameters moeten toobe gewijzigd/geoptimaliseerd zorgvuldig voor het verkrijgen van een geldig model. Schalen van variabelen aanzienlijk helpt bij convergentie.
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER**

Coëfficiënten: [0.0141707753435,-0.0252930927087,-0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092,-0.00456498588241,-0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632,-0.00289545676449,-0.00791124681938, 0.54396316518,-0.536293513569, 0.0119076553369,-0.0173039244582, 0.0119632796147, 0.00146764882502]

Intercept: 0.854507624459

RMSE 1.23485131376 =

R sqr 0.597963951127 =

Tijd tooexecute boven cel: 38.62 seconden

### <a name="random-forest-regression"></a>Willekeurige Forest regressie
Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een willekeurige forestmodel die tip bedrag voor Hallo NYC taxi reis gegevens voorspelt opslaan.   

> [!NOTE]
> Kruisvalidatie met de parameter verstrekkende met aangepaste code is opgegeven in de bijlage Hallo.
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER**

RMSE 0.931981967875 =

R sqr 0.733445485802 =

Tijd tooexecute boven cel: 25.98 seconden

### <a name="gradient-boosting-trees-regression"></a>Kleurovergang prestatieverbetering structuren regressie
Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een kleurovergang prestatieverbetering structuren model die tip bedrag voor Hallo NYC taxi reis gegevens voorspelt opslaat.

** Trainen en evalueren **

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER**

RMSE 0.928172197114 =

R sqr 0.732680354389 =

Tijd tooexecute boven cel: 20.9 seconden

**Tekenen**

*tmp_results* is geregistreerd als een Hive-tabel in de vorige cel Hallo. Resultaten van de tabel Hallo worden uitgevoerd in Hallo *sqlResults* tijdskader voor het uitzetten van gegevens. Dit is de code Hallo

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Hier volgt Hallo code tooplot Hallo gegevens met behulp van Hallo Jupyter-server.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Werkelijke-vs-voorspeld-tip-bedragen](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>Bijlage: Extra regressie taken met meerdere validatie met parameter krijgen
Deze bijlage bevat de code die laat zien hoe toodo k/l met elastische net voor lineaire regressie en hoe toodo k/l met de parameter sweep met aangepaste code voor willekeurige forest regressie.

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>Cross-validatie met elastische net voor lineaire regressie
Hallo-code in deze sectie laat zien hoe toodo cross-validatie met elastische net voor lineaire regressie en hoe tooevaluate Hallo model met de testgegevens.

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER**

Tijd tooexecute boven cel: 161.21 seconden

**Met R SQR metriek evalueren**

*tmp_results* is geregistreerd als een Hive-tabel in de vorige cel Hallo. Resultaten van de tabel Hallo worden uitgevoerd in Hallo *sqlResults* tijdskader voor het uitzetten van gegevens. Dit is de code Hallo

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


Hier volgt Hallo code toocalculate R sqr.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**UITVOER**

R sqr 0.619184907088 =

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>Cross-validatie met parameter vegen met aangepaste code voor willekeurige forest regressie
Hallo-code in deze sectie laat zien hoe toodo cross-validatie met parameter vegen met aangepaste code voor willekeurige forest regressie en hoe tooevaluate Hallo model met de testgegevens.

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER**

RMSE 0.906972198262 =

R sqr 0.740751197012 =

Tijd tooexecute boven cel: 69.17 seconden

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>Opschonen van objecten uit het geheugen en de locaties van het model met print
Gebruik `unpersist()` toodelete objecten in het cachegeheugen opgeslagen.

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


**UITVOER**

PythonRDD [122] op RDD op PythonRDD.scala: 43

** Afdruk pad toomodel bestanden toobe in Hallo verbruik laptop gebruikt. ** tooconsume en score onafhankelijk-gegevensset, u moet toocopy en plak deze bestandsnamen in Hallo 'Verbruik notebook'.

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**UITVOER**

logisticRegFileLoc = modelDir + 'LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528'

linearRegFileLoc = modelDir + 'LinearRegressionWithSGD_2016-05-0316_51_28.433670'

randomForestClassificationFileLoc = modelDir + 'RandomForestClassification_2016-05-0316_50_17.454440'

randomForestRegFileLoc = modelDir + 'RandomForestRegression_2016-05-0316_51_57.331730'

BoostedTreeClassificationFileLoc = modelDir + 'GradientBoostingTreeClassification_2016-05-0316_50_40.138809'

BoostedTreeRegressionFileLoc = modelDir + 'GradientBoostingTreeRegression_2016-05-0316_52_18.827237'

## <a name="whats-next"></a>Volgende stappen
Nu u regressie en classificatie modellen met Hallo Spark MlLib hebt gemaakt, bent u klaar toolearn hoe tooscore en evalueren van deze modellen.

**Model verbruik:** toolearn hoe tooscore en evalueren Hallo classificatie en regressie modellen in dit onderwerp hebt gemaakt, Zie [Score en evalueren van Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md).

