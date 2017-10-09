---
title: aaaData exploratie en modellering met Spark | Microsoft Docs
description: Showcases hello gegevensverkenning en mogelijkheden van Hallo Spark MLlib toolkit op Azure modelleren.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a>Met Spark gegevens verkennen en modelleren
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

In dit scenario maakt gebruik van HDInsight Spark toodo gegevensverkenning en binaire classificatie en taken van een steekproef van Hallo NYC modelleren regressie taxi reis en ritbedrag 2013 gegevensset.  Dit leidt u door de stappen Hallo Hallo [gegevens wetenschap proces](http://aka.ms/datascienceprocess), end-to-end, met behulp van een HDInsight Spark-cluster gebruikt voor verwerking en Azure blobs toostore Hallo gegevens en het Hallo-modellen. Hallo-proces wordt verkend en gebracht van een Azure Storage-Blob gegevens visualiseren en vervolgens wordt voorbereid Hallo gegevens toobuild voorspellende modellen. Deze modellen zijn samenstellen met Hallo Spark MLlib toolkit toodo binaire classificatie en regressie modelleren van taken.

* Hallo **binaire classificatie** taak toopredict is al dan niet een tip voor Hallo reis wordt betaald. 
* Hallo **regressie** taak toopredict Hallo hoeveelheid Hallo tip op basis van andere functies tip is. 

Hallo modellen we gebruiken omvatten logistic en lineaire regressie, willekeurige forests en kleurovergang gestimuleerd structuren:

* [Lineaire regressie met SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is een lineair regressiemodel die gebruikmaakt van een methode stochastische kleurovergang Daalgradiënt (SGD) en voor optimalisatie en het onderdeel schalen toopredict Hallo tip bedragen betaald. 
* [Logistic regression met LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) of regressie 'logit', is een regressiemodel dat kan worden gebruikt wanneer Hallo afhankelijke variabele categorische toodo gegevensclassificatie is. LBFGS is een quasi toegepast optimalisatie-algoritme dat benadert Hallo Broyden – Fletcher – Goldfarb – Shanno (BFGS) algoritme met een beperkte hoeveelheid computergeheugen en die wordt veel gebruikt in machine learning.
* [Willekeurige forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) ensembles van beslissingsstructuren zijn.  Ze combineren veel decision trees tooreduce Hallo risico te. Willekeurige forests worden gebruikt voor regressie en classificatie en categorische functies kunnen verwerken en toohello multiklassen classificatie instelling kunnen worden uitgebreid. Ze hoeven niet functie schalen en weet kunnen toocapture niet-mogelijkheid tot en interactie van de functie. Willekeurige forests zijn een van de meest succesvolle Hallo-machine learning-modellen voor de indeling en regressie.
* [Verloop boosted structuren](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) ensembles van beslissingsstructuren zijn. GBTs train besluit structuren iteratief toominimize een verlies-functie. GBTs worden gebruikt voor regressie en classificatie en categorische functies kan verwerken, hoeven niet functie schalen en kunnen toocapture niet-mogelijkheid tot zijn en interacties functies. Ze kunnen ook worden gebruikt in een setting multiklasse classificatie.

Hallo modellering stappen bevatten ook een code die laat zien hoe tootrain, evalueren en opslaan van elk type model. Python is gebruikte toocode Hallo-oplossing en tooshow Hallo relevante waarnemingspunten.   

> [!NOTE]
> Hoewel Hallo Spark MLlib toolkit ontworpen toowork op grote gegevenssets is, wordt hier een voorbeeld van een relatief klein (ongeveer 30 Mb met behulp van 170K rijen, ongeveer 0,1% van de oorspronkelijke NYC gegevensset Hallo) gebruikt voor het gemak. Hallo oefening hier opgegeven efficiënt (in ongeveer 10 minuten) op een HDInsight-cluster met 2 worker-knooppunten wordt uitgevoerd. Hallo kan dezelfde code bevatten, met kleine wijzigingen worden gebruikt tooprocess grotere gegevenssets-wordt met de juiste wijzigingen voor het cachen van gegevens in het geheugen en Hallo clustergrootte wijzigen.
> 
> 

## <a name="prerequisites"></a>Vereisten
U moet een Azure-account en een 1.6 Spark (of Spark 2.0) HDInsight-cluster toocomplete in dit scenario. Zie Hallo [overzicht van Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md) voor instructies over het toosatisfy deze vereisten. Dit onderwerp bevat ook een beschrijving van Hallo NYC 2013 Taxi gegevens hier gebruikt en instructies over hoe tooexecute code van een Jupyter-notebook in Spark-cluster Hallo. 

## <a name="spark-clusters-and-notebooks"></a>Spark-clusters en laptops
Instellingsstappen en code vindt u in dit scenario voor het gebruik van een HDInsight Spark 1.6. Maar Jupyter-notebooks zijn opgegeven voor zowel HDInsight Spark 1.6 en 2.0 Spark-clusters. Een beschrijving van het Hallo-notitieblokken en -koppelingen toothem vindt u in Hallo [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) voor Hallo GitHub-opslagplaats met ze. Bovendien Hallo code hier en in notitieblokken Hallo gekoppeld is algemeen en moet werken op een Spark-cluster. Als u geen van HDInsight Spark, Hallo clusterinstallatie gebruikmaakt en management stappen mogelijk enigszins afwijken van wat hier moet worden weergegeven. Voor het gemak vindt hier u koppelingen Hallo toohello Jupyter-notebooks voor Spark 1.6 (toobe worden uitgevoerd in de pySpark-kernel Hallo Hallo Jupyter-Notebook server) en Spark 2.0 (toobe in Hallo pySpark3 kernel Hallo Jupyter-Notebook server worden uitgevoerd):

### <a name="spark-16-notebooks"></a>Spark 1.6 laptops

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): bevat informatie over het tooperform gegevensverkenning, modelleren en batchscoreberekening met diverse verschillende algoritmen.

### <a name="spark-20-notebooks"></a>Spark 2.0-laptops
Hallo regressie en classificatie taken die worden geïmplementeerd met een 2.0 Spark-cluster zich in afzonderlijke notebooks en Hallo classificatie notebook maakt gebruik van een andere gegevensset:

- [Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): dit bestand bevat informatie over hoe tooperform gegevensverkenning, modelleren en scores in Spark 2.0 opslagclusters die gebruikmaken van Hallo NYC Taxi reis en tarief gegevensset-beschreven [hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Deze laptop is mogelijk een goed uitgangspunt voor het snel verkennen Hallo-code die we voor Spark 2.0 hebt opgegeven. Voor een meer gedetailleerde notebook Hallo NYC Taxi gegevens analyseert, Zie de volgende notebook Hallo in deze lijst. Zie na deze lijst Hallo-opmerkingen die deze laptops vergelijken. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): dit bestand ziet u hoe tooperform gegevens worsteling (Spark SQL en dataframe bewerkingen), exploratie, model en score berekenen met behulp van Hallo NYC Taxi reis en tarief set gegevens die worden beschreven [ Hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): dit bestand ziet u hoe tooperform gegevens worsteling (Spark SQL en dataframe bewerkingen), exploratie, model en score berekenen met behulp van bekende luchtvaartmaatschappij tijdige vertrek Hallo de gegevensset van 2011 en 2012. We Hallo luchtvaartmaatschappij gegevensset geïntegreerd met Hallo luchthaven weer gegevens (bijvoorbeeld windsnelheid, temperatuur en hoogte enz.) voorafgaande toomodeling, zodat deze weer-functies kunnen worden opgenomen in het Hallo-model.

<!-- -->

> [!NOTE]
> Hallo luchtvaartmaatschappij dataset is toegevoegd toohello Spark 2.0 notitieblokken toobetter illustreren Hallo gebruik van de classificatie-algoritmen. Zie Hallo koppelingen voor meer informatie over luchtvaartmaatschappij tijdige vertrek gegevensset en weer gegevensset te volgen:

>- Luchtvaartmaatschappij tijdige vertrek gegevens: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Luchthaven weergegevens: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Hallo Spark 2.0 notitieblokken op Hallo NYC taxi en luchtvaartmaatschappij vlucht vertraging-gegevenssets duurt 10 minuten of meer toorun (afhankelijk van de grootte van de Hallo van uw HDI-cluster). Hallo eerste laptop in Hallo boven lijst geeft veel aspecten van Hallo gegevensverkenning, visualisatie en ML-model training in een laptop die minder tijd toorun met een lagere actieve NYC gegevensset duurt, in welke Hallo taxi en tarief bestanden vooraf lid zijn: [ Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) deze notebook neemt een veel kortere tijd toofinish (2-3 minuten) en kan worden een goed startpunt voor Hallo code snel verkennen we hebben opgegeven voor Spark 2.0. 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
onderstaande Hallo beschrijvingen zijn verwante toousing Spark 1.6. Gebruik Hallo notitieblokken beschreven en bovenstaande voor Spark 2.0-versies. 

<!-- -->

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
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>Bibliotheken importeren
Instellen is ook vereist nodig bibliotheken importeren. Context voor spark instellen en importeer nodig bibliotheken Hello code te volgen:

    # IMPORT LIBRARIES
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

## <a name="data-ingestion-from-public-blob"></a>Gegevensopname van een openbare blob
eerste stap van de Hallo in Hallo gegevens wetenschap proces tooingest Hallo gegevens toobe geanalyseerd van bronnen is waar is bevindt zich in uw gegevens te verkennen en modellering omgeving. Hallo-omgeving is Spark in dit scenario. Deze sectie bevat Hallo code toocomplete een reeks taken:

* Hallo gegevens voorbeeld toobe gemodelleerd opnemen
* Lees in invoergegevensset hello (opgeslagen als een bestand .tsv)
* indeling en schone Hallo-gegevens
* maken en objecten (RDDs of gegevens frames) in het geheugen in de cache
* registreren als een temp-tabel in SQL-context.

Hier volgt Hallo-code voor gegevensopname.

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**UITVOER:**

Tijd tooexecute boven cel: 51.72 seconden

## <a name="data-exploration--visualization"></a>Gegevensverkenning & visualisatie
Zodra het Hallo-gegevens weer in Spark, is hello volgende stap in Hallo gegevens wetenschap proces toogain dieper inzicht Hallo gegevens via de exploratie en visualisatie. In deze sectie bekijken we Hallo taxi gegevens met behulp van SQL-query's en tekent Hallo target-variabelen en potentiële functies voor visuele controle. In het bijzonder uitzetten we Hallo frequentie van de passagiers tellingen in taxi reizen, Hallo frequentie van tip bedragen en hoe tips is afhankelijk van de hoeveelheid betaling en het type.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Een histogram van passagiers aantal frequenties in voorbeeld van taxi reizen Hallo tekenen
Deze code en de volgende codefragmenten SQL magische tooquery Hallo voorbeeld en lokale magische tooplot Hallo gegevens gebruiken.

* **SQL-magic (`%%sql`)** hello HDInsight PySpark-kernel ondersteunt eenvoudig inline HiveQL query's op Hallo sqlContext. Hallo (-o naam_variabele) argument als een DataFrame Pandas op Hallo Jupyter server Hallo-uitvoer van de SQL-query Hallo zich blijft voordoen. Dit betekent dat deze beschikbaar zijn in de lokale modus Hallo.
* Hallo  **`%%local` magic** is toorun code lokaal op Hallo Jupyter-server, waarop Hallo headnode van Hallo HDInsight-cluster wordt gebruikt. Normaal gesproken gebruikt u `%%local` magische in combinatie met Hallo `%%sql` met -o parameter magic. Hallo -o parameter Hallo-uitvoer van lokaal Hallo SQL-query wilt behouden en vervolgens %% lokale magic zou de volgende set Hallo van code codefragment toorun lokaal tegen Hallo uitvoer Hallo SQL-query's die lokaal wordt bewaard

Hallo-uitvoer wordt automatisch weergegeven nadat u Hallo code uitvoeren.

Deze query haalt Hallo reizen op het aantal van de passagiers. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

Deze code maakt een lokale gegevens tijdskader van Hallo query-uitvoer en Hallo van de gegevenspunten. Hallo `%%local` magic maakt een lokale gegevens-frame, `sqlResults`, die kan worden gebruikt voor het uitzetten van matplotlib. 

> [!NOTE]
> Deze PySpark-magic wordt meerdere malen gebruikt in dit scenario. Als Hallo hoeveelheid gegevens te groot is, moet u een steekproef nemen uit toocreate een gegevens-frame dat in het lokale geheugen past.
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Hier volgt Hallo code tooplot Hallo reizen door passagiers aantallen

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**UITVOER:**

![De frequentie reis op het aantal passagiers](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

U kunt kiezen uit verschillende soorten visualisaties (tabel-, cirkel, regel, gebied of balk) met behulp van Hallo **Type** menuknoppen in Hallo notebook. Hallo-balk tekent wordt hier weergegeven.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Zet een histogram van de tip bedragen en hoe tip bedrag hangt af van de passagiers telling en het tarief bedragen.
Gebruik een SQL-query toosample-gegevens.

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


**UITVOER:** 

![Tip bedragdistributie](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Hoeveelheid op het aantal passagiers Tip](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Tip bedrag door tarief bedrag](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Functie-engineering, transformatie en gegevens voorbereiding voor modellering
Deze sectie wordt beschreven en vindt Hallo-code voor de procedures gebruikt tooprepare gegevens voor gebruik in ML-model. Er wordt weergegeven hoe toodo Hallo volgende taken:

* Maakt een nieuwe functie met binning uur in verkeer tijd buckets
* Index en categorische functies coderen
* Gelabelde point-objecten voor invoer in ML functies maken
* Onderliggende steekproeven van Hallo gegevens maken en deze te splitsen in trainings- en testdoeleinden sets
* Functie schalen
* Cacheobjecten in het geheugen

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Maakt een nieuwe functie met binning uur in verkeer tijd buckets
Deze code laat zien hoe een nieuwe functie door uren in verkeer tijd binning toocreate tijdsintervallen en hoe toocache Hallo resulterende gegevensframe in het geheugen. Flexibele gegevenssets gedistribueerd (RDDs) en gegevens frames herhaaldelijk gebruikt, leidt opslaan in cache tooimproved uitvoeringstijden. Dienovereenkomstig, we RDDs en gegevensframes cache in verschillende stadia in Hallo overzicht. 

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

**UITVOER:** 

126050

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>Index en het coderen van categorische functies voor invoer in het modelleren van functies
Deze sectie wordt beschreven hoe tooindex of categorische functies voor invoer in Hallo modelleren functies coderen. Hallo modelleren en functies van MLlib hebben functies met categorische invoergegevens toobe geïndexeerd of eerdere toouse gecodeerd voorspellen. Afhankelijk van het Hallo-model of u kunt tooindex ze coderen op verschillende manieren:  

* **Op basis van een structuur modellering** vereist categorieën toobe gecodeerd als numerieke waarden (bijvoorbeeld, een onderdeel met drie categorieën kan worden gecodeerd met 0, 1, 2). Dit wordt geleverd door de MLlib [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) functie. Deze functie codeert een tekenreekskolom van de labels tooa kolom van het label indexen die zijn besteld op het label frequenties. Hoewel geïndexeerd met numerieke waarden voor de invoer- en de verwerking van gegevens, op basis van een structuur Hallo-algoritmen opgegeven tootreat kunnen zijn op de juiste wijze als categorieën. 
* **Logistic en lineaire regressie modellen** vereisen een hot codering, where, bijvoorbeeld, een onderdeel met drie categorieën kan worden uitgebreid naar drie kolommen van de functie, waarbij elke met 0 of 1, afhankelijk van de categorie van een observatie Hallo. MLlib biedt [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) werken toodo één hot codering. Deze encoder wijst een kolom van een label indexen tooa kolom van de binaire aanvalsvectoren, met maximaal één one-waarde. Met deze codering kunt algoritmen die verwacht dat de numerieke waarden functies, zoals logistic regression toobe toegepast toocategorical functies.

Hier volgt Hallo code tooindex en coderen categorische functies:

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

**UITVOER:**

Tijd tooexecute boven cel: 1.28 seconden

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Gelabelde point-objecten voor invoer in ML functies maken
Deze sectie bevat de code die laat zien hoe tooindex categorische tekst gegevenstype als de gegevens van een gelabelde en deze te coderen zodat deze gebruikt tootrain en test MLlib logistic regression en andere classificatie-modellen worden kan. Gelabelde point-objecten zijn robuuste gedistribueerd gegevenssets (RDD) geformatteerd op een manier die is vereist als de invoergegevens voor de meeste ML algoritmen in MLlib. Een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is een lokale vector, dense of sparse, die is gekoppeld aan een label/antwoord.  

Deze sectie bevat de code die laat zien hoe tooindex categorische gegevens als een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) gegevenstype en deze te coderen zodat deze gebruikt tootrain en test MLlib logistic regression en andere classificatie-modellen worden kan. Gelabelde point-objecten zijn robuuste gedistribueerd gegevenssets (RDD) die bestaan uit een label (doel/antwoord-variabele) en de functie vector. Deze indeling is nodig als invoer door veel ML algoritmen in MLlib.

Hier volgt Hallo code tooindex en het coderen van tekstfuncties voor binaire classificatie.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
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
Deze code maakt een willekeurige steekproeven van het Hallo-gegevens (25% wordt hier gebruikt). Hoewel dit niet vereist voor dit voorbeeld vanwege toohello grootte van de gegevensset hello, ziet u hoe u kunt een steekproef nemen hier zodat u weet hoe toouse voor uw eigen probleem wanneer deze nodig is. Als voorbeelden groot zijn, kan dit aanzienlijke tijd tijdens de training modellen opslaan. Naast splitsen we Hallo voorbeeld in trainings-onderdeel (hier 75%) en een test toouse deel (25% hier) in de classificatie en regressie modellering.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

**UITVOER:**

Tijd tooexecute boven cel: 0,24 seconden

### <a name="feature-scaling"></a>Functie schalen
Functie schaal, ook wel bekend als gegevensnormalisatie, weet u zeker dat functies met veel betaald waarden zijn niet opgegeven overmatige afwegen in objective Hallo-functie. Hallo code voor het schalen van de functie maakt gebruik van Hallo [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale Hallo functies toounit variantie. Het wordt geleverd door MLlib voor gebruik in lineaire regressie met stochastische kleurovergang Daalgradiënt (SGD), een populaire algoritme voor het trainen van een breed scala aan andere machine learning-modellen zoals overgegaan regressies of ondersteuning vector machines (SVM).

> [!NOTE]
> We hebben gevonden Hallo LinearRegressionWithSGD algoritme toobe gevoelige toofeature schalen.
> 
> 

Hier volgt Hallo code tooscale variabelen voor gebruik met Hallo overgegaan lineaire SGD algoritme.

    # FEATURE SCALING

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

**UITVOER:**

Tijd tooexecute boven cel: 13.17 seconden

### <a name="cache-objects-in-memory"></a>Cacheobjecten in het geheugen
Hallo-tijd die nodig is voor trainings- en testen van ML algoritmen kunnen worden verkleind door het opslaan in cache Hallo invoergegevens frame objecten die gebruikt worden voor classificatie, regressie, en functies geschaald.

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

**UITVOER:** 

Tijd tooexecute boven cel: 0,15 seconden

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Voorspellen of een tip wordt betaald met binaire classificatie modellen
Deze sectie wordt beschreven hoe gebruik drie modellen voor Hallo binaire classificatietaak van het voorspellen van al dan niet een tip voor een reis taxi wordt betaald. Hallo-modellen die zijn gepresenteerd zijn:

* Logistic regression overgegaan 
* Willekeurige forestmodel
* Kleurovergang prestatieverbetering structuren

Elk model bouwen sectie code opgedeeld in stappen: 

1. **Training model** gegevens met één parameterset
2. **Evaluatie model** op een test-gegevensset met metrische gegevens
3. **Opslaan van model** in blob voor toekomstige verbruik

### <a name="classification-using-logistic-regression"></a>Classificatie met logistic regression
Hallo-code in deze sectie ziet u hoe tootrain, evalueren en opslaan van een regressiemodel logistic met [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) die voorspelt al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald.

**Hallo logistic regression-model met k/l en hyperparameter sweeping trainen**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**UITVOER:** 

Coëfficiënten: [0.0082065285375,-0.0223675576104,-0.0183812028036, -3.48124578069e-05,-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]

Intercept:-0.0111216486893

Tijd tooexecute boven cel: 14.43 seconden

**Hallo binaire classificatie model met standaard metrische gegevens evalueren**

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**UITVOER:** 

Gebied onder PR 0.985297691373 =

Gebied onder ROC 0.983714670256 =

Samenvattende statistieken

Precisie 0.984304060189 =

Intrekken 0.984304060189 =

F1 Score 0.984304060189 =

Tijd tooexecute boven cel: 57.61 seconden

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

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


**UITVOER:**

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>Classificatie van willekeurige forest
Hallo-code in deze sectie laat zien hoe tootrain, evalueren en opslaan van een willekeurige forestmodel die voorspelt al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

**UITVOER:**

Gebied onder ROC 0.985297691373 =

Tijd tooexecute boven cel: 31.09 seconden

### <a name="gradient-boosting-trees-classification"></a>Kleurovergang prestatieverbetering structuren classificatie
Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een kleurovergang prestatieverbetering structuren model die al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald voorspelt opslaat.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


**UITVOER:**

Gebied onder ROC 0.985297691373 =

Tijd tooexecute boven cel: 19.76 seconden

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>Tip bedragen voor taxi reizen met regressie modellen voorspellen
Deze sectie wordt beschreven hoe gebruik drie modellen voor Hallo regressie taak van het voorspellen van Hallo Hallo tip betaald taxi reis op basis van andere functies tip hoeveelheid. Hallo-modellen die zijn gepresenteerd zijn:

* Lineaire regressie overgegaan
* Willekeurige forest
* Kleurovergang prestatieverbetering structuren

Deze modellen zijn in Hallo inleiding beschreven. Elk model bouwen sectie code opgedeeld in stappen: 

1. **Training model** gegevens met één parameterset
2. **Evaluatie model** op een test-gegevensset met metrische gegevens
3. **Opslaan van model** in blob voor toekomstige verbruik

### <a name="linear-regression-with-sgd"></a>Lineaire regressie met SGD
Hallo code in deze sectie toont hoe toouse geschaald functies tootrain een lineaire regressie die stochastische kleurovergang daalgradiënt (SGD), kunnen worden gebruikt en hoe tooscore, evalueren en Hallo-model opslaan in Azure Blob Storage (WASB).

> [!TIP]
> In onze ervaring kunnen er problemen met het Hallo-convergentie van LinearRegressionWithSGD modellen en parameters moeten toobe gewijzigd/geoptimaliseerd zorgvuldig voor het verkrijgen van een geldig model. Schalen van variabelen aanzienlijk helpt bij convergentie. 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER:**

Coëfficiënten: [0.00457675809917,-0.0226314167349,-0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981,-0.000987181489428,-0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995,- 0.00990211159703,-0.00637410344522, 0.545083566179,-0.536756072402, 0.0105762393099,-0.0130117577055, 0.0129304737772,-0.00171065945959]

Intercept: 0.853872718283

RMSE 1.24190115863 =

R sqr 0.608017146081 =

Tijd tooexecute boven cel: 58,42 seconden

### <a name="random-forest-regression"></a>Willekeurige Forest regressie
Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een willekeurige forest regressie die tip bedrag voor Hallo NYC taxi reis gegevens voorspelt opslaan.

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

**UITVOER:**

RMSE 0.891209218139 =

R sqr 0.759661334921 =

Tijd tooexecute boven cel: 49.21 seconden

### <a name="gradient-boosting-trees-regression"></a>Kleurovergang prestatieverbetering structuren regressie
Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een kleurovergang prestatieverbetering structuren model die tip bedrag voor Hallo NYC taxi reis gegevens voorspelt opslaat.

** Trainen en evalueren **

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**UITVOER:**

RMSE 0.908473148639 =

R sqr 0.753835096681 =

Tijd tooexecute boven cel: 34.52 seconden

**Tekenen**

*tmp_results* is geregistreerd als een Hive-tabel in de vorige cel Hallo. Resultaten van de tabel Hallo worden uitgevoerd in Hallo *sqlResults* tijdskader voor het uitzetten van gegevens. Dit is de code Hallo

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

Hier volgt Hallo code tooplot Hallo gegevens met behulp van Hallo Jupyter-server.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


**UITVOER:**

![Werkelijke-vs-voorspeld-tip-bedragen](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>Opschonen van objecten uit het geheugen
Gebruik `unpersist()` toodelete objecten in het cachegeheugen opgeslagen.

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>Record opslaglocaties van Hallo modellen voor gebruiks- en score berekenen
tooconsume en score een onafhankelijke gegevensset beschreven in Hallo [Score en evalueren van Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md) onderwerp, moet u toocopy en plak deze met Hallo opgeslagen modellen hier in Hallo gemaakt bestandsnamen Jupyter-notebook verbruik. Hier volgt Hallo code tooprint uit Hallo paden toomodel bestanden u er moet.

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**UITVOER**

logisticRegFileLoc = modelDir + 'LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568'

linearRegFileLoc = modelDir + 'LinearRegressionWithSGD_2016-05-0317_05_21.577773'

randomForestClassificationFileLoc = modelDir + 'RandomForestClassification_2016-05-0317_04_11.950206'

randomForestRegFileLoc = modelDir + 'RandomForestRegression_2016-05-0317_06_08.723736'

BoostedTreeClassificationFileLoc = modelDir + 'GradientBoostingTreeClassification_2016-05-0317_04_36.346583'

BoostedTreeRegressionFileLoc = modelDir + 'GradientBoostingTreeRegression_2016-05-0317_06_51.737282'

## <a name="whats-next"></a>Volgende stappen
Nu u regressie en classificatie modellen met Hallo Spark MlLib hebt gemaakt, bent u klaar toolearn hoe tooscore en evalueren van deze modellen. Hallo geavanceerde gegevensverkenning en laptop dives diepere naar kruisvalidatie, hyper-parameter inclusief modelleren verstrekkende en model van de evaluatie. 

**Model verbruik:** toolearn hoe tooscore en evalueren Hallo classificatie en regressie modellen in dit onderwerp hebt gemaakt, Zie [Score en evalueren van Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md).

**Kruisvalidatie en hyperparameter sweeping**: Zie [geavanceerde gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) over de manier waarop modellen kunnen getraind met behulp van kruisvalidatie en hyper-parameter sweeping

